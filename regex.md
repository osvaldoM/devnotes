# getting started

[regex one .. the basics tutorial](https://regexone.com/)

## grep
[using regx with grep](https://www.digitalocean.com/community/tutorials/using-grep-regular-expressions-to-search-for-text-patterns-in-linux)


# renaming files

### rename movies

`rename -n 's/(\w+) - (\d{1})x(\d{2}).*$/S0$2E$3\.srt/' *.srt `

### strip initial dash from text files
`rename -n 's/-//' *.txt`

### rename .html to .php files
