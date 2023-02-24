# Exploring the Connection between Cooking Time and Recipe Ratings

February 23, 2023
by Mohit Sridhar (msridhar@ucsd.edu) and Aditya Arun (adarun@ucsd.edu)

---

## Introduction

Welcome to the exploratory data analysis project on the relationship between cooking time and average rating of recipes! This project aims to investigate whether there is a correlation between how long a recipe takes to cook and how highly it is rated by users.

The dataset used for this analysis contains information on a variety of recipes, including their ingredients, cooking times, and user ratings. By exploring this data, we hope to gain insights into the factors that contribute to a recipe's success and popularity. This dataset contains recipes and ratings from <a href='food.com'> food.com </a>.

This website will serve as a platform to share our findings and visualizations with others. It will include an overview of the project, a description of the dataset and methodology, interactive visualizations, and a conclusion summarizing our key findings.

---

### - About the data

The primary dataset used for this analysis is a food.com dataset, which contains information on 83,781 recipes, including ingredients, cooking times, and user ratings.
The dataset contains 13 columns which are the following:

name: the name of the recipe
id: the unique recipe id in the website
contributor_id: the unique id of the recipe contributor
submitted: date of recipe submission
tags: keywords linked to the recipe for easy query
nutrition: nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for "percentage of daily value"
n_steps: number of steps in recipe
steps :ext for recipe steps, in order
description: user-provided description

We used Python and the following libraries to preprocess and analyze the data:

Pandas: for data manipulation and cleaning
Matplotlib: for data visualization
Scipy: for statistical analysis and hypothesis testing
