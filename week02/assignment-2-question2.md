Solution to Assignment 2.2
================
Kenneth Benoit
16/10/2017

Question 2
----------

### Question 2.2

This comes straight from the lecture notes:

``` r
library("reshape2", warn.conflicts = FALSE)
load("cmpdata.Rdata")

cmpdataLong <- melt(cmpdata,
                    id.vars = c("countryname", "party", "date"),
                    measure.vars = names(cmpdata)[21:76],
                    variable.name = "category",
                    value.name = "catcount")
head(cmpdataLong, 10)
```

    ##    countryname party   date category catcount
    ## 1      Austria 42420 199010   per101        0
    ## 2      Austria 42110 199010   per101        0
    ## 3      Austria 42320 199010   per101        0
    ## 4      Austria 42520 199010   per101        5
    ## 5      Austria 42420 199410   per101        0
    ## 6      Austria 42421 199410   per101        0
    ## 7      Austria 42110 199410   per101        0
    ## 8      Austria 42320 199410   per101        0
    ## 9      Austria 42520 199410   per101        0
    ## 10     Austria 42520 199512   per101        0

### Question 2.2

To "spread" this back into wide format, using the **tidyr** package:

``` r
library("tidyr", warn.conflicts = FALSE)
cmpdataWide <- spread(cmpdataLong, category, catcount)
head(cmpdataWide)
```

    ##   countryname party   date per101 per102 per103 per104 per105 per106
    ## 1     Austria 42110 199010      0      0      2      0      3      0
    ## 2     Austria 42110 199410      0      0      0      0      0      3
    ## 3     Austria 42110 199512      0      0      0      0      1      1
    ## 4     Austria 42110 199910      0      0      0      0     12      2
    ## 5     Austria 42110 200211      0      0      0      0      9      4
    ## 6     Austria 42110 200610      0      0      0      3      9      2
    ##   per107 per108 per109 per110 per201 per202 per203 per204 per301 per302
    ## 1     17      0      0      3     79    230     24      0     14      2
    ## 2      2      2      0      1     20     67     21      0      0      0
    ## 3      1      6      2      6     12      7      1      0      0      0
    ## 4      2      0      0      1     15      3      0      0      0      0
    ## 5      7     13      0      0     37     17      0      0      0      0
    ## 6     52     36     11      0     36     17      1      0      0      0
    ##   per303 per304 per305 per401 per402 per403 per404 per405 per406 per407
    ## 1     67     39     14      5      8      3      2      0      2      0
    ## 2     19     27     83      1      0      4      0      0      0      0
    ## 3      1      0     17      0      0      1      0      0      0      0
    ## 4      0      1     20      0      0      0      0      0      0      0
    ## 5      0      0     14      0      6      2      0      0      0      0
    ## 6      3      0      1      2      6     20      0      0      0      0
    ##   per408 per409 per410 per411 per412 per413 per414 per415 per416 per501
    ## 1     24      2      5     11      5      0      0      0     38    317
    ## 2     21      0     32     68      0      0      0      0      1    239
    ## 3      9      0      5      2      0      0      5      0      0      9
    ## 4      1      0      0      0      0      0      0      0      4     25
    ## 5      3      4      1     22      0      0      0      0     34     42
    ## 6      1      1      0     38     17      1      0      0     13     62
    ##   per502 per503 per504 per505 per506 per507 per601 per602 per603 per604
    ## 1     45    105     73      0     17      0      0     14     20     20
    ## 2      0      3      3      0      1      0      0      0      0      0
    ## 3      0     14      3      0      2      0      0      4      1      0
    ## 4      0     20     19      0      0      0      0      0      0      4
    ## 5     18     45     35      0     33      0      0      2      0      1
    ## 6     48     83     24      0     46      0     14      0      0     20
    ##   per605 per606 per607 per608 per701 per702 per703 per704 per705 per706
    ## 1     29     23     14      0     36      0     33      2    100     49
    ## 2      0      6      0      0      0      0     51      0     90      1
    ## 3      0      3      0      0      0      0      0      0      4      0
    ## 4      1      1      0      0      1      0      0      0      7     17
    ## 5      8      0     12      0     35      0      6      0     15     35
    ## 6      9     10     15      5     33      0     13      9      0     32
