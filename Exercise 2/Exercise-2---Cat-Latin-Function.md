Exercise 2
================

# Introduction

Welcome to Exercise 2! Here, we will make a function that will convert
words into the brand new Cat Latin cipher. In Cat Latin, the last letter
of a word is moved to the front, the word is repeated, and the end of
the word has “-meow” added to it.

------------------------------------------------------------------------

# Coding

## Setup

Load these libraries to ensure the following code can run correctly.

``` r
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(tidyverse)
```

    ## Warning: package 'tidyverse' was built under R version 4.3.3

    ## Warning: package 'ggplot2' was built under R version 4.3.3

    ## Warning: package 'tidyr' was built under R version 4.3.3

    ## Warning: package 'readr' was built under R version 4.3.3

    ## Warning: package 'purrr' was built under R version 4.3.3

    ## Warning: package 'stringr' was built under R version 4.3.3

    ## Warning: package 'forcats' was built under R version 4.3.3

    ## Warning: package 'lubridate' was built under R version 4.3.3

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ forcats   1.0.0     ✔ readr     2.1.5
    ## ✔ ggplot2   3.5.1     ✔ stringr   1.5.1
    ## ✔ lubridate 1.9.3     ✔ tibble    3.2.1
    ## ✔ purrr     1.0.2     ✔ tidyr     1.3.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(stringr)
library(testthat)
```

    ## Warning: package 'testthat' was built under R version 4.3.3

    ## 
    ## Attaching package: 'testthat'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     is_null
    ## 
    ## The following objects are masked from 'package:readr':
    ## 
    ##     edition_get, local_edition
    ## 
    ## The following object is masked from 'package:tidyr':
    ## 
    ##     matches
    ## 
    ## The following object is masked from 'package:dplyr':
    ## 
    ##     matches

## Function

This code-chunk creates the function *cat_latin*. It is annotated with
unredered roxygen2 tags.

``` r
#' Convert words into Cat Latin
#'
#' @description
#'Moves the last letter of a word to the front, repeats the word, and adds "-meow" to the end of it. Can be applied to lists of words, and is only applicable to character vectors.
#'
#' @param x The character vector or list of vectors to be used.
#'
#' @return A character vector
#' @export
#'
#' @examples
#' cat_latin("cat")

cat_latin <- function(x) { 
  
  # This stops the function if the input is of the incorrect type
  
  if(!is.character(x)) { 
    stop("Sorry, this function only works on character vectors") 
  }
  
  # This converts the input into Cat Latin by re-arranging the components
  
   str_c(str_sub(x, -1), str_sub(x, end = -2), x, "-meow")
}
```

## Examples

Three examples of *cat_latin()* in use.

``` r
# Convert a one word string to Cat Latin

cat_latin("cat")
```

    ## [1] "tcacat-meow"

``` r
# Apply Cat Latin to multiple words

y <- c("cat", "dog")

cat_latin(y)
```

    ## [1] "tcacat-meow" "gdodog-meow"

``` r
# The following code will result in an error message, as *cat_latin()* cannot be applied to a number. It is commented out so that the file can be knitted.

# cat_latin(1)
```

## Tests

Three tests to demonstrate that *cat_latin()* works as expected.

``` r
# Test 1 - Non-character inputs result in an error

test_that("Non-character input error", {
  expect_error(cat_latin(15))
})
```

    ## Test passed 🎊

``` r
# Test 2 - The function prints the result to the console

test_that("Print result", {
  expect_visible(cat_latin("Hello"))
})
```

    ## Test passed 🎊

``` r
# Test 3 - Output is the expected class

test_that("Expect output to be a character vector", {
  expect_type(cat_latin("Hello"), "character")
})
```

    ## Test passed 🎊

------------------------------------------------------------------------

# Conclusion

In conclusion, this Exercise shows the development of the function
*cat_latin*, which converts words into the newly developed Cat Latin
Cipher. Three examples were shown, and three tests run to show that the
function works properly.
