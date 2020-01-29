Test statistical assignment
================
Emilia Korobowicz
22 January 2020

## Introduction

Please change the author and date fields above as appropriate. Do not
change the output format. Once you have completed the assignment you
want to knit your document into a markdown document in the
“github\_document” format and then commit both the .Rmd and .md files
(and all the associated files with graphs) to your private assignment
repository on Github.

## Reading data (40 points)

First, we need to read the data into R. For this assignment, I ask you
to use data from the youth self-completion questionnaire (completed by
children between 10 and 15 years old) from Wave 9 of the Understanding
Society. It is one of the files you have downloaded as part of SN6614
from the UK Data Service. To help you find and understand this file you
will need the following documents:

1)  The Understanding Society Waves 1-9 User Guide:
    <https://www.understandingsociety.ac.uk/sites/default/files/downloads/documentation/mainstage/user-guides/mainstage-user-guide.pdf>
2)  The youth self-completion questionnaire from Wave 9:
    <https://www.understandingsociety.ac.uk/sites/default/files/downloads/documentation/mainstage/questionnaire/wave-9/w9-gb-youth-self-completion-questionnaire.pdf>
3)  The codebook for the file:
    <https://www.understandingsociety.ac.uk/documentation/mainstage/dataset-documentation/datafile/youth/wave/9>

View(Data$i\_sex\_dv)

``` r
library(tidyverse)
```

    ## Warning in as.POSIXlt.POSIXct(Sys.time()): unknown timezone 'zone/tz/2019c.
    ## 1.0/zoneinfo/Europe/London'

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.2.1     ✔ purrr   0.2.5
    ## ✔ tibble  1.4.2     ✔ dplyr   0.7.8
    ## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
    ## ✔ readr   1.3.0     ✔ forcats 0.3.0

    ## Warning: package 'tibble' was built under R version 3.4.3

    ## Warning: package 'tidyr' was built under R version 3.4.4

    ## Warning: package 'readr' was built under R version 3.4.4

    ## Warning: package 'purrr' was built under R version 3.4.4

    ## Warning: package 'dplyr' was built under R version 3.4.4

    ## Warning: package 'stringr' was built under R version 3.4.4

    ## Warning: package 'forcats' was built under R version 3.4.3

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
Data <- read_tsv("/Users/emiliakorobowicz/Desktop/DataScience3/EmilysRepo/NewRepo/Data/UKDA-6614-tab/tab/ukhls_w9/i_youth.tab")
```

    ## Parsed with column specification:
    ## cols(
    ##   .default = col_double()
    ## )

    ## See spec(...) for full column specifications.

## Tabulate variables (10 points)

In the survey children were asked the following question: “Do you have a
social media profile or account on any sites or apps?”. In this
assignment we want to explore how the probability of having an account
on social media depends on children’s age and gender.

Tabulate three variables: children’s gender, age (please use derived
variables) and having an account on social media.

``` r
Data <- mutate(Data, Age = 2019 - i_ypdoby)
```

    ## Warning: package 'bindrcpp' was built under R version 3.4.4

``` r
select(Data, i_sex, Age, i_ypsocweb)
```

    ## # A tibble: 2,821 x 3
    ##    i_sex   Age i_ypsocweb
    ##    <dbl> <dbl>      <dbl>
    ##  1     2    16          1
    ##  2     1    14          1
    ##  3     1    15          1
    ##  4     2    16          1
    ##  5     1    14          1
    ##  6     1    16          1
    ##  7     1    16          1
    ##  8     2    13          1
    ##  9     1    17          2
    ## 10     1    18          1
    ## # ... with 2,811 more rows

The column Age is here, just at the very end

## Recode variables (10 points)

We want to create a new binary variable for having an account on social
media so that 1 means “yes”, 0 means “no”, and all missing values are
coded as NA. We also want to recode gender into a new variable with the
values “male” and “female” (this can be a character vector or a
factor).

?recode\_factor

``` r
Data$i_sex_dv = recode_factor(Data$i_sex_dv, `1` = "male", `2` = "female")
```

    ## Warning: Unreplaced values treated as NA as .x is not compatible. Please
    ## specify replacements exhaustively or supply .default

``` r
Data$i_ypsocweb = recode_factor(Data$i_ypsocweb, `1` = "1", `2` = "0", .missing = "missing")
```

    ## Warning: Unreplaced values treated as NA as .x is not compatible. Please
    ## specify replacements exhaustively or supply .default

``` r
Data$i_ypsocweb1 = recode_factor(Data$i_ypsocweb, `1` = "1", `2` = "0", missing = "missing")
```

data\(sex <- NA data\)sex\[Data$i\_ypsocweb == 1\] \<- 1
data\(sex[Data\)i\_ypsocweb == 2\] \<- 0 table(data$sex)

## Calculate means (10 points)

Produce code that calculates probabilities of having an account on
social media (i.e. the mean of your new binary variable produced in the
previous problem) by age and
gender.

?glm

## ;m is for contionous dependent variables. use glm instead; Thats a categorical

## check use of glm; check use of logodds

## glm()

## g

## Write short interpretation (10 points)

WIth each year of age the kids are 0.09064 less likely to have a social
media account. Females are also 0.06108 less likely to have a social
media account.

## Visualise results (20 points)

Create a statistical graph (only one, but it can be faceted)
illustrating your results (i.e. showing how the probability of having an
account on social media changes with age and gender). Which type of
statistical graph would be most appropriate for this?

## Conclusion

This is a test formative assignment and the mark will not count towards
your final mark. If you cannot answer any of the questions above this is
fine – we are just starting this module\! However, please do submit this
assignment in any case to make sure that you understand the procedure,
that it works correctly and you do not have any problems with summative
assignments later.
