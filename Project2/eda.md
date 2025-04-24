# Exploratory Data Analysis


## Research Question:

-   Can coffee consumers be grouped into distinct customer-classes based
    on self-reported data? What customer-class demographic spends the
    most at corporate coffee chains? What characteristics seperate
    consumers from other classes of consumers?

## Analysis Objective:

-   Using CBA - Clustering for Business Analytics by Christian Buchta, I
    am looking to identify distinct “customer-classes” by analyzing
    individual, self reported data on their coffee drinking habits
    (location, preferred roast, preferred brand, home coffee spending)
    and demographic characteristics such as their age, gender, race,
    educational background, and number of children. Identifying
    prominent characteristics that lead to vast differences in consumer
    spending can be beneficial to any corporation looking to target the
    right kind of consumers through advertising.

## Exploratory Data Analysis

### Download Data + Data Cleaning

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

``` r
# Cleaning up the age variable, using the gsub function to replace / remove uneeded words for the visual. 
coffee_survey$age_clean <- tolower(coffee_survey$age) #Converts age to lowercase for string handling
coffee_survey$age_clean <- gsub("years old", "", coffee_survey$age_clean)
coffee_survey$age_clean <- gsub("to", "-", coffee_survey$age_clean)

barplot(table(coffee_survey$age_clean), #Table provides named list, containing the counts of each age group
        col = "skyblue", 
        main = "Age Groups Distribution", 
        ylab = "Count",
        xlab = 'Age Groups')
```

![](eda.markdown_strict_files/figure-markdown_strict/unnamed-chunk-2-1.png)
