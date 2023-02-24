# Exploring the Connection between Cooking Time and Recipe Ratings

February 23, 2023 \
https://adityaarun2.github.io/exploratory-data-analysis-project/ \
by Mohit Sridhar (msridhar@ucsd.edu) and Aditya Arun (adarun@ucsd.edu)

---

## Introduction

Welcome to the exploratory data analysis project on the relationship between cooking time and average rating of recipes! This project aims to investigate whether there is a correlation between how long a recipe takes to cook and how highly it is rated by users. Our research is centered around the question: 

The dataset used for this analysis contains information on a variety of recipes, including their ingredients, cooking times, and user ratings. By exploring this data, we hope to gain insights into the factors that contribute to a recipe's success and popularity. This dataset contains recipes and ratings from <a href='food.com'> food.com </a>.

This website will serve as a platform to share our findings and visualizations with others. It will include an overview of the project, a description of the dataset and methodology, interactive visualizations, and a conclusion summarizing our key findings.

### Question

The question we are going to investigate with this data is: Do recipes with a higher number of ingredients (complex recipes) receive higher ratings on average than those with fewer ingredients (simple recipes)?

The reason we decided on this question is because we want to investigate whether people tend to rate more complicated recipes higher compared to simpler recipes. This would be important to consider when looking at the data above because the values of the ratings for a given recipe may be correlated with its complexity (in this case, the complexity is the number of ingredients since recipes with more ingredients are usually more complicated). However, complicated recipes might be more rewarding and ultimately a tastier dish compared to simpler recipes. After considering these nuances, answering this question can be helpful in determining why a certain recipe is rated a certain way.

Another important aspect of this question is determining the cutoff for a low or high recipe. In order to find this value, we decided to plot the distribution of the n_ingredients column so we could get a general sense of how the recipes in this dataset compare to one another in terms of their ingredient count. The histogram we generated is included below in the Cleaning and EDA section. As you can see, the median of this distribution is around 9. Therefore, we decided to classify recipes with an ingredient count of **9 or less as simple** and recipes with an ingredient count **greater than 9 as complex**. Additionally, choosing the median as the cutoff would help eliminate any sampling bias since we would have an equal amount of data on either side of the median (the median is the 50th percentile). Lastly, 9 ingredients is intuitively a good cutoff. It is reasonable to assume, in general, that a dish with less than 9 ingredients should be fairly simple and easy to make compared to dishes with 10 or more ingredients.

### About the data

The primary dataset used for this analysis is a food.com dataset, which contains information on 83,781 recipes, including ingredients, cooking times, and user ratings.
The dataset contains 13 columns which are the following:


| column     |   description |
|:------------|--------:|
| name   |       the name of the recipe |
| id |     the unique recipe id in the website |
| minutes | time taken in minutes to cook recipe |
| contributor_id |     the unique id of the recipe contributor |
| submitted |       date of recipe submission |
| tags   |      keywords linked to the recipe for easy query |
| nutrition | nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)] |
| n_steps |  number of steps in recipe  |
| steps | text for recipe steps, in order|
| description | user-provided description |
| ingredients	| ingredients required for recipe |
| n_ingredients |	number of ingredients required for recipe |
| avg_rating | average rating given by users |

We used Python and the following libraries to preprocess and analyze the data:

Pandas: for data manipulation and cleaning \
Matplotlib: for data visualization \
Scipy: for statistical analysis and hypothesis testing

### Why we replace 0 with NaN

The reason why we should replace the ratings of value 0 with NaN is because these ratings are often missing values from people who want to simply comment or forgot to leave an actual review. Thus, we wouldn't want extreme missing values, such as 0, to significantly alter our mean. By replacing 0's with NaN, Pandas automatically ignores the missing values and calculates the mean on the rest of the ratings.

---
