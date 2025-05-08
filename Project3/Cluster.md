# Exploratory Data Analysis


## Preprocess & Load Data:

``` r
source("functions/preprocess.R")
```

    ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ✔ ggplot2   3.5.1     ✔ tibble    3.2.1
    ✔ lubridate 1.9.4     ✔ tidyr     1.3.1
    ✔ purrr     1.0.2     
    ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ✖ dplyr::filter() masks stats::filter()
    ✖ dplyr::lag()    masks stats::lag()
    ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

    Attaching package: 'janitor'


    The following objects are masked from 'package:stats':

        chisq.test, fisher.test


    here() starts at /Users/luke/Documents/GitHub/Stat155

    Rows: 4042 Columns: 113
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr (44): Submission ID, What is your age?, How many cups of coffee do you t...
    dbl (13): Lastly, how would you rate your own coffee expertise?, Coffee A - ...
    lgl (56): Where do you typically drink coffee? (At home), Where do you typic...

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

## Cluster Analysis
