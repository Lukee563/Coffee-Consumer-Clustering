# Coffee Consumer Analysis


## Narrative

Using data from a 2023 survey of “Great American Coffee Taste Test”
viewers, I will be exploring consumer trends of American coffee
enthusiasts, primarily through spending demographics and coffee
preferences.

All of the data comes from the following TidyTuesday publication:
<https://github.com/rfordatascience/tidytuesday/blob/main/data/2024/2024-05-14/readme.md>

I’ve worked as a barista at both Starbucks, and on the UC Santa Cruz
Campus, and have a general interest in the subject, as coffee In this
demographic, do coffee drinkers tend to prefer certain chains over
others? Do older coffee enthusiasts tend to spend more money on at-home
equipment? What age group prefers a cappuccino the most? These are the
types of questions I believe I can explore using this dataset.

## Data

Downloads the dataset and cleans it (removes onehot encoding)

``` r
rm(list=ls())
library(tidyverse)
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

``` r
library(janitor)
```


    Attaching package: 'janitor'

    The following objects are masked from 'package:stats':

        chisq.test, fisher.test

``` r
library(here)
```

    here() starts at /Users/luke/Documents/GitHub/Stat155

``` r
library(fs)

#Data Cleaning
working_dir <- here::here("data", "2024", "2024-05-14")

url <- "https://bit.ly/gacttCSV"

raw <- readr::read_csv(url)
```

    Rows: 4042 Columns: 113
    ── Column specification ────────────────────────────────────────────────────────
    Delimiter: ","
    chr (44): Submission ID, What is your age?, How many cups of coffee do you t...
    dbl (13): Lastly, how would you rate your own coffee expertise?, Coffee A - ...
    lgl (56): Where do you typically drink coffee? (At home), Where do you typic...

    ℹ Use `spec()` to retrieve the full column specification for this data.
    ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
# Grab the raw questions for the dictionary.
raw |> 
  colnames() |> 
  cat(sep = "\n")
```

    Submission ID
    What is your age?
    How many cups of coffee do you typically drink per day?
    Where do you typically drink coffee?
    Where do you typically drink coffee? (At home)
    Where do you typically drink coffee? (At the office)
    Where do you typically drink coffee? (On the go)
    Where do you typically drink coffee? (At a cafe)
    Where do you typically drink coffee? (None of these)
    How do you brew coffee at home?
    How do you brew coffee at home? (Pour over)
    How do you brew coffee at home? (French press)
    How do you brew coffee at home? (Espresso)
    How do you brew coffee at home? (Coffee brewing machine (e.g. Mr. Coffee))
    How do you brew coffee at home? (Pod/capsule machine (e.g. Keurig/Nespresso))
    How do you brew coffee at home? (Instant coffee)
    How do you brew coffee at home? (Bean-to-cup machine)
    How do you brew coffee at home? (Cold brew)
    How do you brew coffee at home? (Coffee extract (e.g. Cometeer))
    How do you brew coffee at home? (Other)
    How else do you brew coffee at home?
    On the go, where do you typically purchase coffee?
    On the go, where do you typically purchase coffee? (National chain (e.g. Starbucks, Dunkin))
    On the go, where do you typically purchase coffee? (Local cafe)
    On the go, where do you typically purchase coffee? (Drive-thru)
    On the go, where do you typically purchase coffee? (Specialty coffee shop)
    On the go, where do you typically purchase coffee? (Deli or supermarket)
    On the go, where do you typically purchase coffee? (Other)
    Where else do you purchase coffee?
    What is your favorite coffee drink?
    Please specify what your favorite coffee drink is
    Do you usually add anything to your coffee?
    Do you usually add anything to your coffee? (No - just black)
    Do you usually add anything to your coffee? (Milk, dairy alternative, or coffee creamer)
    Do you usually add anything to your coffee? (Sugar or sweetener)
    Do you usually add anything to your coffee? (Flavor syrup)
    Do you usually add anything to your coffee? (Other)
    What else do you add to your coffee?
    What kind of dairy do you add?
    What kind of dairy do you add? (Whole milk)
    What kind of dairy do you add? (Skim milk)
    What kind of dairy do you add? (Half and half)
    What kind of dairy do you add? (Coffee creamer)
    What kind of dairy do you add? (Flavored coffee creamer)
    What kind of dairy do you add? (Oat milk)
    What kind of dairy do you add? (Almond milk)
    What kind of dairy do you add? (Soy milk)
    What kind of dairy do you add? (Other)
    What kind of sugar or sweetener do you add?
    What kind of sugar or sweetener do you add? (Granulated Sugar)
    What kind of sugar or sweetener do you add? (Artificial Sweeteners (e.g., Splenda))
    What kind of sugar or sweetener do you add? (Honey)
    What kind of sugar or sweetener do you add? (Maple Syrup)
    What kind of sugar or sweetener do you add? (Stevia)
    What kind of sugar or sweetener do you add? (Agave Nectar)
    What kind of sugar or sweetener do you add? (Brown Sugar)
    What kind of sugar or sweetener do you add? (Raw Sugar (Turbinado))
    What kind of flavorings do you add?
    What kind of flavorings do you add? (Vanilla Syrup)
    What kind of flavorings do you add? (Caramel Syrup)
    What kind of flavorings do you add? (Hazelnut Syrup)
    What kind of flavorings do you add? (Cinnamon (Ground or Stick))
    What kind of flavorings do you add? (Peppermint Syrup)
    What kind of flavorings do you add? (Other)
    What other flavoring do you use?
    Before today's tasting, which of the following best described what kind of coffee you like?
    How strong do you like your coffee?
    What roast level of coffee do you prefer?
    How much caffeine do you like in your coffee?
    Lastly, how would you rate your own coffee expertise?
    Coffee A - Bitterness
    Coffee A - Acidity
    Coffee A - Personal Preference
    Coffee A - Notes
    Coffee B - Bitterness
    Coffee B - Acidity
    Coffee B - Personal Preference
    Coffee B - Notes
    Coffee C - Bitterness
    Coffee C - Acidity
    Coffee C - Personal Preference
    Coffee C - Notes
    Coffee D - Bitterness
    Coffee D - Acidity
    Coffee D - Personal Preference
    Coffee D - Notes
    Between Coffee A, Coffee B, and Coffee C which did you prefer?
    Between Coffee A and Coffee D, which did you prefer?
    Lastly, what was your favorite overall coffee?
    Do you work from home or in person?
    In total, much money do you typically spend on coffee in a month?
    Why do you drink coffee?
    Why do you drink coffee? (It tastes good)
    Why do you drink coffee? (I need the caffeine)
    Why do you drink coffee? (I need the ritual)
    Why do you drink coffee? (It makes me go to the bathroom)
    Why do you drink coffee? (Other)
    Other reason for drinking coffee
    Do you like the taste of coffee?
    Do you know where your coffee comes from?
    What is the most you've ever paid for a cup of coffee?
    What is the most you'd ever be willing to pay for a cup of coffee?
    Do you feel like you’re getting good value for your money when you buy coffee at a cafe?
    Approximately how much have you spent on coffee equipment in the past 5 years?
    Do you feel like you’re getting good value for your money with regards to your coffee equipment?
    Gender
    Gender (please specify)
    Education Level
    Ethnicity/Race
    Ethnicity/Race (please specify)
    Employment Status
    Number of Children
    Political Affiliation

``` r
coffee_survey <- raw |> 
  janitor::clean_names() |> 
  # Get rid of one-hot encoding; users can do that if they'd like. Also,
  # "flavorings" columns are empty.
  dplyr::select(
    submission_id,
    age = what_is_your_age,
    cups = how_many_cups_of_coffee_do_you_typically_drink_per_day,
    where_drink = where_do_you_typically_drink_coffee,
    brew = how_do_you_brew_coffee_at_home,
    brew_other = how_else_do_you_brew_coffee_at_home,
    purchase = on_the_go_where_do_you_typically_purchase_coffee,
    purchase_other = where_else_do_you_purchase_coffee,
    favorite = what_is_your_favorite_coffee_drink,
    favorite_specify = please_specify_what_your_favorite_coffee_drink_is,
    additions = do_you_usually_add_anything_to_your_coffee,
    additions_other = what_else_do_you_add_to_your_coffee,
    dairy = what_kind_of_dairy_do_you_add,
    sweetener = what_kind_of_sugar_or_sweetener_do_you_add,
    style = before_todays_tasting_which_of_the_following_best_described_what_kind_of_coffee_you_like,
    strength = how_strong_do_you_like_your_coffee,
    roast_level = what_roast_level_of_coffee_do_you_prefer,
    caffeine = how_much_caffeine_do_you_like_in_your_coffee,
    expertise = lastly_how_would_you_rate_your_own_coffee_expertise,
    starts_with("coffee"),
    prefer_abc = between_coffee_a_coffee_b_and_coffee_c_which_did_you_prefer,
    prefer_ad = between_coffee_a_and_coffee_d_which_did_you_prefer,
    prefer_overall = lastly_what_was_your_favorite_overall_coffee,
    wfh = do_you_work_from_home_or_in_person,
    total_spend = in_total_much_money_do_you_typically_spend_on_coffee_in_a_month,
    why_drink = why_do_you_drink_coffee,
    why_drink_other = other_reason_for_drinking_coffee,
    taste = do_you_like_the_taste_of_coffee,
    know_source = do_you_know_where_your_coffee_comes_from,
    most_paid = what_is_the_most_youve_ever_paid_for_a_cup_of_coffee,
    most_willing = what_is_the_most_youd_ever_be_willing_to_pay_for_a_cup_of_coffee,
    value_cafe = do_you_feel_like_you_re_getting_good_value_for_your_money_when_you_buy_coffee_at_a_cafe,
    spent_equipment = approximately_how_much_have_you_spent_on_coffee_equipment_in_the_past_5_years,
    value_equipment = do_you_feel_like_you_re_getting_good_value_for_your_money_with_regards_to_your_coffee_equipment,
    gender,
    gender_specify = gender_please_specify,
    education_level,
    ethnicity_race,
    ethnicity_race_specify = ethnicity_race_please_specify,
    employment_status,
    number_children = number_of_children,
    political_affiliation
  )
```

``` r
library(tibble)
glimpse(coffee_survey)
```

    Rows: 4,042
    Columns: 57
    $ submission_id                <chr> "gMR29l", "BkPN0e", "W5G8jj", "4xWgGr", "…
    $ age                          <chr> "18-24 years old", "25-34 years old", "25…
    $ cups                         <chr> NA, NA, NA, NA, NA, NA, NA, NA, "Less tha…
    $ where_drink                  <chr> NA, NA, NA, NA, NA, NA, "At a cafe, At th…
    $ brew                         <chr> NA, "Pod/capsule machine (e.g. Keurig/Nes…
    $ brew_other                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ purchase                     <chr> NA, NA, NA, NA, NA, NA, "National chain (…
    $ purchase_other               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ favorite                     <chr> "Regular drip coffee", "Iced coffee", "Re…
    $ favorite_specify             <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ additions                    <chr> "No - just black", "Sugar or sweetener, N…
    $ additions_other              <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ dairy                        <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ sweetener                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ style                        <chr> "Complex", "Light", "Complex", "Complex",…
    $ strength                     <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ roast_level                  <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ caffeine                     <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ expertise                    <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ coffee_a_bitterness          <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_a_acidity             <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_a_personal_preference <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_a_notes               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ coffee_b_bitterness          <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_b_acidity             <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_b_personal_preference <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_b_notes               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ coffee_c_bitterness          <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_c_acidity             <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_c_personal_preference <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_c_notes               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ coffee_d_bitterness          <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_d_acidity             <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_d_personal_preference <dbl> NA, NA, NA, NA, NA, NA, NA, NA, 4, NA, NA…
    $ coffee_d_notes               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ prefer_abc                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ prefer_ad                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ prefer_overall               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ wfh                          <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ total_spend                  <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ why_drink                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ why_drink_other              <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ taste                        <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ know_source                  <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ most_paid                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ most_willing                 <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ value_cafe                   <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ spent_equipment              <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ value_equipment              <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ gender                       <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ gender_specify               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ education_level              <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ ethnicity_race               <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ ethnicity_race_specify       <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ employment_status            <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ number_children              <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…
    $ political_affiliation        <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, N…

``` r
##Lots of NA's in the first few rows, but out of the 4042 rows I should have enough valid data to work with.
```
