# Amazon Vine Analysis

## Overview of Analysis

The purpose of this analysis is to assess if there are any meaningful differences between vine (paid) and unpaid Amazon reviews.

## Results of Analysis

The first step in the analysis was to filter the results to show only reviews with 20 or more total votes, of which at least 50% considered the review helpful. The purpose of this was to ensure our datapoints are well-supported.

- How many Vine and non-Vine reviews were there?
  - Vine – There were no Vine reviews with 20 or more total votes with a helpful ratio of 50% or more.
  - Non-Vine – There were 65,149 non-Vine reviews.
- How many five-star reviews?
  - Vine – There were none.
  - Non-Vine – There were 24,673 five-star reviews.
- Percentage of five-star reviews?
  - Vine – Unable to be computed due to "divide by zero" as there were no Vine reviews that met the initial criteria mentioned above for this data set. NaN.
  - Non-Vine – 37.87% of the reviews were five-star reviews.

R's Tidyverse was used to compute the results above:

```R
vine_total_votes <- vine_table %>% filter(total_votes >= 20) #filter table by total_votes
vine_helpful_votes <- vine_total_votes %>% filter(helpful_votes / total_votes >= .5) #filter by ratio of helpful_votes
vine_paid <- vine_helpful_votes %>% filter(vine == 'Y') #Extract vine reviews
vine_unpaid <- vine_helpful_votes %>% filter(vine == 'N') #Extract non-Vine reviews

n_total_paid <- vine_paid %>% summarize(n()) #Count Vine reviews
n_fivestar_paid <- vine_paid %>% filter(star_rating == 5) %>% summarize(n()) #Count five-star Vine reviews
pct_fivestar_paid <- n_fivestar_paid / n_total_paid * 100 #Determine percent of five-star Vine reviews

n_total_unpaid <- vine_unpaid %>% summarize(n()) #Count non-Vine reviews
n_fivestar_unpaid <- vine_unpaid %>% filter(star_rating == 5) %>% summarize(n()) #Count five-star non-Vine reviews
pct_fivestar_unpaid <- n_fivestar_unpaid / n_total_unpaid * 100 #Determine percent of five-star non-Vine reviews
```

#### Screenshot of Results

###### Vine Reviews

