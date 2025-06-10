# Coffee Consumer Analysis


## Project Concept

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

## Data:

Using data from a 2023 survey of “Great American Coffee Taste Test”
viewers, I will be exploring consumer trends of American coffee
enthusiasts, primarily through spending demographics and coffee
preferences.

All of the data comes from the following TidyTuesday publication:
<https://github.com/rfordatascience/tidytuesday/blob/main/data/2024/2024-05-14/readme.md>

Some variables from this study that will be important for grouping
consumers into customer-classes include:

cups: How many cups of coffee do you typically drink per day?

where_drink: Where do you typically drink coffee?

brew: How do you brew coffee at home?

purchase: On the go, where do you typically purchase coffee?

favorite: What is your favorite coffee drink?

additions: Do you usually add anything to your coffee?

expertise: how would you rate your own coffee expertise?

total_spend: In total, much money do you typically spend on coffee in a
month?

number_children: Number of Children

employment_status: Employment Status

gender: Gender

age: Age

ethnicity_race: Ethnicity/Race

education_level: Education Level

## Project Outcomes:

-   From initial observations, it appears that factoring/one-hot
    encoding survey data does not provide enough distance between each
    observation to distinctively separate them into unique, well defined
    clusters. After attempting to use ROCK clustering from the CBA
    package, and obtaining similar results, I switched to Grower/PAM
    which handles one-hot encoded categorical data and obtained similar
    results. We can see that there is a very large amount of overlap
    between the 3 clusters, and through further parameter tuning /
    changing of the amount of clusters, I have been unable to identify
    well-defined, separate groupings based on this survey data. Outliers
    seem to be members of all 3 clusters, and there does not seem to be
    any real evidence that members of each cluster are truly different
    from one another based on the current observable characteristics /
    principal components created for the 2d visual plot.

-   This likely occurs because members of the 2023 survey of “Great
    American Coffee Taste Test” viewers were all likely similar in many
    aspects, including observable aspects like coffee preferences and
    consumer habits. If the viewers are all very similar in their coffee
    preferences, and we force our clustering algorithm to sort them into
    clusters regardless, we end up with a cloud of multiple clusters,
    with no defined unique groupings. Even with further survey data, if
    the individuals of the survey are all closely similar to each other
    in their daily coffee consuming habits, we likely will not be able
    to create well defined clusters. It is obvious that this sample
    alone cannot be used to make predictions on the behavior of other
    American coffee consumers due to the selection bias within our
    sample of these survey respondents.

    ## Monte Carlo Experiment (Project IV)

    In real-world settings, two majors issues with business data is
    sample size and the quality of the data. Following a factorial
    experimental design, In this experiment, i explored how sample size
    and logical matrix sparsity affect the output of the Proximus
    clustering algorithm. Understanding the limitations of the Proximus
    clustering algorithm through a controlled Monte Carlo simulation
    experiment can assist us in understanding when the algorithm is most
    useful to use for analysis. Proximus takes logical matrices as
    input, and produces clusters assignments for each individual
    observation, with the quality of the data greatly affecting the
    output of the algorithm.

    -   In this experiment, I generated new data based on the historic
        distribution of each column, with a normalized error, for each
        instance of a factor-level simulation. I ended up with 90
        randomly generated, similar data to the current survey results,
        each with different amount of observations or sparistiy
        depending on the factor-level specification.
    -   Jaccard similarity of the total approximation is provided for
        each proximus output, and I will be comparing the mean and
        standard deviation of the Jaccard similarity for each
        factor-level.

    ### Outcome:

    ![](https://lh7-rt.googleusercontent.com/slidesz/AGV_vUdJn40DaSiBhMOwC2FAUcpL0oe6TZcIZm2bCr51zuMgeCseYWBNRU5x28v2-GfhFpUieC_FltinAmRMc91LmQHqvRx8PmIT8w5EKww9BgJTQD1jD3n3MvwZ3mgZjnCXuO2YyzQQmA=s2048?key=ufQwwwCAXcnlXMTvaragRA.png)

    We find that as matrix sparsity increases, the Jaccard Similarity
    measure decreases. Sample size has little effect on the average
    Jaccard Similarity score
