---
title: "Dealing with currencies in php"
published: 2020-10-10
updated: 2021-02-09
summary: "One recurring mistake developers make is to perform mathematical operations on currencies using floats(floating point numbers), which might cause rounding errors and other issues."
tags: [ 'php' ]
---

## How we operate with currencies in PHP and what problems does it have?

One recurring mistake developers make is to perform mathematical operations on currencies, using floats(floating point numbers),
which might cause rounding errors and other issues due to how floats are represented in computer hardware. A good explanation for this, can be found in this [article](https://docs.python.org/release/2.5.1/tut/node16.html).

One common approach to working with currencies is to use Martin Fowler's money pattern which in summary means:
- Deal in the currencies smallest unit (for dollars that's cents, but don't assume all currencies have the same smallest unit).
- Store amounts as strings (for some cases, integers can be used)
- Perform all arithmetic operations using the BC or GMP extensions. For this example I used BCMath

This approach is valid for cryptocurrencies as well, but we have to define a base fractional unit for the specific cryptocurrency we want to work with.

An example of a Money class using this pattern that also takes some ideas from the Money class described in [Kent Beck's TDD by example Book](https://www.amazon.com/Test-Driven-Development-Kent-Beck/dp/0321146530) is below:

```php
<?php

class Money
{
    /**
     * The smallest unit of the currency
     *
     * @var int
     */
    protected $fractional_unit;

    protected $currency;

    public function __construct($amount, $currency)
    {
        $this->fractional_unit = strval($amount);
        $this->currency = $currency;;
    }

    /**
     * A static function to create a new instance of Money.
     *
     * @param int $amount numeric value representing the amount
     * @param string $currency
     * @return Money
     */
    public static function init($amount, $currency)
    {
        if(!is_numeric($amount)){
            throw new InvalidArgumentException('amount must be a numeric value');
        }
        return new Money($amount, $currency);
    }

    public function getAmount() {
        return $this->fractional_unit;
    }

    public function getCurrency() {
        return $this->currency;
    }

    public static function isSameCurrency(Money $left_operand, Money $right_operand)
    {
        return $left_operand->currency == $right_operand->currency;
    }

    /**
     * A static function to return the sum of two instances of Money.
     *
     * @param Money $left_operand
     * @param Money $right_operand
     * @return Money
     * @throws InvalidArgumentException
     */
    public static function add(Money $left_operand, Money $right_operand) {
        if(!static::isSameCurrency($left_operand, $right_operand) ){
            throw new InvalidArgumentException("operands must be of same currency");
        }
        return Money::init(bcadd($left_operand->getAmount(), $right_operand->getAmount()), $left_operand->getCurrency());
    }
    /**
     * A static function to return the difference between two instances of Money.
     *
     * @param Money $left_operand
     * @param Money $right_operand
     * @return Money
     * @throws InvalidArgumentException
     */
    public static function subtract(Money $left_operand, Money $right_operand) {
        if(!static::isSameCurrency($left_operand, $right_operand) ){
            throw new InvalidArgumentException("operands must be of same currency");
        }
        return Money::init(bcsub($left_operand->getAmount(), $right_operand->getAmount()), $left_operand->getCurrency());
    }
    /**
     * A static function to return the multiplication of two instances of Money.
     *
     * @param Money $left_operand
     * @param Money $right_operand
     * @return Money
     * @throws InvalidArgumentException
     */
    public static function multiply(Money $left_operand, Money $right_operand) {
        if(!static::isSameCurrency($left_operand, $right_operand) ){
            throw new InvalidArgumentException("operands must be of same currency");
        }
        return Money::init(bcmul($left_operand->getAmount(), $right_operand->getAmount()), $left_operand->getCurrency());
    }
    /**
     * A static function to return the division of two instances of Money.
     *
     * @param Money $left_operand
     * @param Money $right_operand
     * @return Money
     * @throws InvalidArgumentException
     */
    public static function divide(Money $left_operand, Money $right_operand) {
        if(!static::isSameCurrency($left_operand, $right_operand) ){
            throw new InvalidArgumentException("operands must be of same currency");
        }
        return Money::init(bcdiv($left_operand->getAmount(), $right_operand->getAmount()), $left_operand->getCurrency());
    }
}
```

## Testing the class

I added a few tests to verify that this class works properly. After having spent weeks reading Kent Beck's Book, I probably should have started
by adding the tests before implementing the class but well, here goes nothing:

```php
<?php
require 'Money.php';
use PHPUnit\Framework\TestCase;

class product extends TestCase
{
    public function testMoneyCanBeCreatedFromValidAmountAndCurrency()
    {
        $this->assertInstanceOf(
            Money::class,
            Money::init(3050,'USD')
        );
    }

    public function testMoneyCannotBeCreatedFromInvalidAmountAndCurrency()
    {
        $this->expectException(InvalidArgumentException::class);
         Money::init('3050B','USD');
    }


    public function testCanSumTwoMoneys()
    {
        $m1 = Money::init(200, 'USD');

        $m2 = Money::init(4000.5, 'USD');

        $sum = Money::add($m1, $m2);

        $this->assertEquals(
            4200,
            $sum->getAmount()
        );
    }

    public function testCanDiffTwoMoneys()
    {
        $m1 = Money::init(200, 'USD');

        $m2 = Money::init(400.544, 'USD');

        $difference = Money::subtract($m2, $m1);

        $this->assertEquals(
            200,
            $difference->getAmount()
        );
    }
    public function testCanMultiplyTwoMoneys()
    {
        $m1 = Money::init(2, 'USD');

        $m2 = Money::init(250.5, 'USD');

        $product = Money::multiply($m1, $m2);

        $this->assertEquals(
            501,
            $product->getAmount()
        );
    }
    public function testCanDivideTwoMoneys()
    {
        $m1 = Money::init(610, 'USD');

        $m2 = Money::init(3, 'USD');

        $quotient = Money::divide($m1, $m2);

        $this->assertEquals(
            203,
            $quotient->getAmount()
        );
    }
}

```



## What is the best way to store them in the Database?

I believe that the best way for storing currencies in the database whenever possible would be to store the value as a decimal/numeric data type in one column and store the currency in a separate column (either a Foreign Key or an ISO currency code). Decimal/numeric data types have enough precision to support most common operations on currencies without losing accuracy.

Alternatively, they could be stored as strings(eg: 250 USD) but this could make arithmetic database operations more difficult, which would also make reporting/analytics for instance, more complicated.



## Articles about Martin Fowler's pattern:
https://code.tutsplus.com/tutorials/money-pattern-the-right-way-to-represent-value-unit-pairs--net-35509
https://culttt.com/2014/05/28/handle-money-currency-web-applications/
https://culttt.com/2014/06/04/working-money-currency-php/
https://www.reddit.com/r/PHP/comments/4sxukz/how_to_properly_handle_money_in_php_and_mysql/


## Comparison of several patterns for the Money class

https://deque.blog/2017/08/17/a-study-of-4-money-class-designs-featuring-martin-fowler-kent-beck-and-ward-cunningham-implementations/

