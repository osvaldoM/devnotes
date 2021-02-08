### Dealing with currencies

#### How we operate with currencies in PHP and what problems does it have?

One recurring mistake developers make is to perform mathematical operations on currencies using floats(floating point numbers), which might cause rounding errors and other issues.
One common approach to working with currencies is to use Martin Fowler's money pattern which in summary means:.
- Deal in the currencies smallest unit (for dollars that's cents, but don't assume all currencies have the same smallest unit).
- Store amounts as strings (for some cases, integers can be used)
- Perform all arithmetic operations using the BC or GMP extensions. For this example I used BCMath

This approach is valid for cryptocurrencies as well, but we have to define a base fractional unit for the specific cryptocurrency we want to work with.

#### What is the best way to store them in the Database?

I believe that the best way for storing currencies in the database whenever possible would be to store the value as a decimal/numeric data type in one column and store the currency in a separate column (either a Foreign Key or an ISO currency code). Decimal/numeric data types have enough precision to support most common operations on currencies without losing accuracy.

Alternatively, they could be stored as strings(eg: 250 USD) but this could make arithmetic database operations more difficult, which would also make reporting/analytics for instance, more complicated.



#### Articles about Martin Fowler's pattern:
https://code.tutsplus.com/tutorials/money-pattern-the-right-way-to-represent-value-unit-pairs--net-35509
https://culttt.com/2014/05/28/handle-money-currency-web-applications/
https://culttt.com/2014/06/04/working-money-currency-php/
https://www.reddit.com/r/PHP/comments/4sxukz/how_to_properly_handle_money_in_php_and_mysql/


#### Comparison of several patterns for the Money class

https://deque.blog/2017/08/17/a-study-of-4-money-class-designs-featuring-martin-fowler-kent-beck-and-ward-cunningham-implementations/

