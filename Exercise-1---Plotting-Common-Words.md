Exercise 1
================

# Introduction

Welcome to Exercise 1! Here, the 10 most common words in Jane Austen’s
novel <u>Persuasion</u>, excluding stop words, will be plotted.

------------------------------------------------------------------------

# Code

## Setup

Load the following libraries to ensure the code runs correctly.

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
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.1
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(tidytext)
```

    ## Warning: package 'tidytext' was built under R version 4.3.3

``` r
library(dplyr)
library(janeaustenr)
```

    ## Warning: package 'janeaustenr' was built under R version 4.3.3

``` r
library(stopwords)
```

    ## Warning: package 'stopwords' was built under R version 4.3.3

``` r
library(purrr)
```

## Filtering the dataset

Here, the data from the *janeaustenr* package, specifically the data for
<u>Persuasion</u>, will be ordered into a table, with one column for
words and one for the count, or number of occurrences, of each word.
Additionally, white-space, punctuation, and stop words will be removed.

``` r
# First, let's take a look at what we're starting with

glimpse(persuasion)
```

    ##  chr [1:8328] "Persuasion" "" "" "by" "" "Jane Austen" "" "(1818)" "" "" "" ...

``` r
# Now, let's split all the words apart, render them in lowercase, and remove whitespace

words_per <- strsplit(janeaustenr::persuasion, "\\s+") %>%
  unlist() %>%
  tolower() %>%
  str_remove_all("[^a-z\\s]")

# Lastly, we need to remove stop words and make a tibble with the counts of each word

stopwords_list <- str_to_lower(stopwords("en"))

per_table <- words_per[!words_per %in% stopwords_list] %>%
  table() %>%
  as.tibble() %>%
  setNames(c("words", "count")) %>%
  arrange(desc(count))
```

    ## Warning: `as.tibble()` was deprecated in tibble 2.0.0.
    ## ℹ Please use `as_tibble()` instead.
    ## ℹ The signature and semantics have changed, see `?as_tibble`.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

``` r
glimpse(per_table)
```

    ## Rows: 5,843
    ## Columns: 2
    ## $ words <chr> "anne", "captain", "mrs", "mr", "elliot", "one", "must", "lady",…
    ## $ count <int> 445, 303, 291, 255, 254, 230, 228, 214, 205, 191, 176, 173, 169,…

## Plotting the words

This code-chunk makes a new table, which is a subset of the above. This
new table contains only the ten most common words and their counts.

``` r
# First, we need to make a subset of the data with only the ten most common words

top_per_table <- per_table %>%
  top_n(10)
```

    ## Selecting by count

This code-chunk renders the plot of the ten most common words in
<u>Persuasion</u>. The bars are in descending order and have the counts
displayed in text on them.

``` r
# Then, we must render the plot of the words

ggplot(top_per_table, aes(x = reorder(words, count, decreasing = TRUE), y = count, fill = words)) +
  geom_col() +
  geom_text(size = 3,position = position_stack(vjust = 0.5), aes(label = count, fontface = "bold")) + 
  labs(x = "Top 10 words", y = "Number of occurrences", title = "Ten most common words in Persuasion by Jane Austen") +
  guides(fill = "none") +
  theme_bw()
```

![](Exercise-1---Plotting-Common-Words_files/figure-gfm/plot-1.png)<!-- -->

------------------------------------------------------------------------

# Conclusion

In conclusion, the top ten words from Jane Austen’s novel
<u>Persuasion</u> were extracted from the *janeaustenr* package and
plotted in a graph.
