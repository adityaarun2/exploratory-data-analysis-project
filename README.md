# Exploring the Connection between Cooking Ingredients and Recipe Ratings

February 23, 2023 \
https://adityaarun2.github.io/exploratory-data-analysis-project/ \
by Mohit Sridhar (msridhar@ucsd.edu) and Aditya Arun (adarun@ucsd.edu)

---

## Introduction

Welcome to the exploratory data analysis project on the relationship between cooking ingredients and average rating of recipes! This project aims to investigate whether there is a correlation between the number of ingredients a recipe needs to cook and how highly it is rated by users. Our research is centered around the question: 

The dataset used for this analysis contains information on a variety of recipes, including their ingredients, cooking times, and user ratings. By exploring this data, we hope to gain insights into the factors that contribute to a recipe's success and popularity. This dataset contains recipes and ratings from <a href='food.com'> food.com</a>.

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
Plotly: for data visualization \
Scipy: for statistical analysis and hypothesis testing

### Why we replace 0 with NaN

The reason why we should replace the ratings of value 0 with NaN is because these ratings are often missing values from people who want to simply comment or forgot to leave an actual review. Thus, we wouldn't want extreme missing values, such as 0, to significantly alter our mean. By replacing 0's with NaN, Pandas automatically ignores the missing values and calculates the mean on the rest of the ratings.

---

## Cleaning and EDA (Exploratory Data Analysis)

### Data Cleaning
Here, we remove an outlier recipe that is not really a recipe, but rather a dating advice. Then, we convert the nutrition, tags, steps, and ingredients columns to actual arrays since they are currently represented as a strings. Lastly, we add a complexity column which will help us classify a dish as either simple or complex.

| name                                 |     id |   minutes |   contributor_id | submitted   | tags                                                                                                                                                                                                                                                                                                                                                          | nutrition                                                         |   n_steps | steps                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | description                                                                                                                                                                                                                                                                                                                                                                       | ingredients                                                                                                                                                                                                                             |   n_ingredients |   avg_rating | complexity   |
|:-------------------------------------|-------:|----------:|-----------------:|:------------|:--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:------------------------------------------------------------------|----------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------:|-------------:|:-------------|
| 1 brownies in the world    best ever | 333281 |        40 |           985201 | 2008-10-27  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings']                                                                                          | ['138.4', ' 10.0', ' 50.0', ' 3.0', ' 3.0', ' 19.0', ' 6.0']      |        10 | ['heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat , stirring frequently , until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs , sugar , cocoa powder , vanilla extract , espresso , and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean , about 25 to 30 minutes', 'remove from the oven and cool completely before cutting']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....sereiously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven!                                                                                                              | ['bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour']                                                          |               9 |            4 | simple       |
| 1 in canada chocolate chip cookies   | 453467 |        45 |          1848091 | 2011-04-11  | ['60-minutes-or-less', 'time-to-make', 'cuisine', 'preparation', 'north-american', 'for-large-groups', 'canadian', 'british-columbian', 'number-of-servings']                                                                                                                                                                       | ['595.1', ' 46.0', ' 211.0', ' 22.0', ' 13.0', ' 51.0', ' 26.0']  |        12 | ['pre-heat oven the 350 degrees f', 'in a mixing bowl , sift together the flours and baking powder', 'set aside', 'in another mixing bowl , blend together the sugars , margarine , and salt until light and fluffy', 'add the eggs , water , and vanilla to the margarine / sugar mixture and mix together until well combined', 'add in the flour mixture to the wet ingredients and blend until combined', 'scrape down the sides of the bowl and add the chocolate chips', 'mix until combined', 'scrape down the sides to the bowl again', 'using an ice cream scoop , scoop evenly rounded balls of dough and place of cookie sheet about 1 - 2 inches apart to allow for spreading during baking', 'bake for 10 - 15 minutes or until golden brown on the outside and soft & chewy in the center', 'serve hot and enjoy !']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | this is the recipe that we use at my school cafeteria for chocolate chip cookies. they must be the best chocolate chip cookies i have ever had! if you don't have margarine or don't like it, then just use butter (softened) instead.                                                                                                                                            | ['white sugar', 'brown sugar', 'salt', 'margarine', 'eggs', 'vanilla', 'water', 'all-purpose flour', 'whole wheat flour', 'baking soda', 'chocolate chips']                                                                             |              11 |            5 | complex      |
| 412 broccoli casserole               | 306168 |        40 |            50969 | 2008-05-30  | ['60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'side-dishes', 'vegetables', 'easy', 'beginner-cook', 'broccoli']                                                                                                                                                                             | ['194.8', ' 20.0', ' 6.0', ' 32.0', ' 22.0', ' 36.0', ' 3.0']     |         6 | ['preheat oven to 350 degrees', 'spray a 2 quart baking dish with cooking spray , set aside', 'in a large bowl mix together broccoli , soup , one cup of cheese , garlic powder , pepper , salt , milk , 1 cup of french onions , and soy sauce', 'pour into baking dish , sprinkle remaining cheese over top', 'bake for 25 minutes or until cheese is lightly browned', 'sprinkle with rest of french fried onions and bake until onions are browned and cheese is bubbly , about 10 more minutes']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | since there are already 411 recipes for broccoli casserole posted to "zaar" ,i decided to call this one  #412 broccoli casserole.i don't think there are any like this one in the database. i based this one on the famous "green bean casserole" from campbell's soup. but i think mine is better since i don't like cream of mushroom soup.submitted to "zaar" on may 28th,2008 | ['frozen broccoli cuts', 'cream of chicken soup', 'sharp cheddar cheese', 'garlic powder', 'ground black pepper', 'salt', 'milk', 'soy sauce', 'french-fried onions']                                                                   |               9 |            5 | simple       |
| millionaire pound cake               | 286009 |       120 |           461724 | 2008-02-12  | ['time-to-make', 'course', 'cuisine', 'preparation', 'occasion', 'north-american', 'desserts', 'american', 'southern-united-states', 'dinner-party', 'holiday-event', 'cakes', 'dietary', 'christmas', 'thanksgiving', 'low-sodium', 'low-in-something', 'taste-mood', 'sweet', '4-hours-or-less'] | ['878.3', ' 63.0', ' 326.0', ' 13.0', ' 20.0', ' 123.0', ' 39.0'] |         7 | ['freheat the oven to 300 degrees', 'grease a 10-inch tube pan with butter , dust the bottom and sides with flour , and set aside', 'in a large mixing bowl , cream the butter and sugar with an electric mixer and add the eggs one at a time , beating after each addition', 'alternately add the flour and milk , stirring till the batter is smooth', 'add the two extracts and stir till well blended', 'scrape the batter into the prepared pan and bake till a cake tester or knife blade inserted in the center comes out clean , about 1 1 / 2 hours', 'cool the cake in the pan on a rack for 5 minutes , then turn it out on the rack to cool completely']                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | why a millionaire pound cake?  because it's super rich!  this scrumptious cake is the pride of an elderly belle from jackson, mississippi.  the recipe comes from "the glory of southern cooking" by james villas.                                                                                                                                                                | ['butter', 'sugar', 'eggs', 'all-purpose flour', 'whole milk', 'pure vanilla extract', 'almond extract']                                                                                                                                |               7 |            5 | simple       |
| 2000 meatloaf                        | 475785 |        90 |          2202916 | 2012-03-06  | ['time-to-make', 'course', 'main-ingredient', 'preparation', 'main-dish', 'potatoes', 'vegetables', '4-hours-or-less', 'meatloaf', 'simply-potatoes2']                                                                                                                                                                           | ['267.0', ' 30.0', ' 12.0', ' 12.0', ' 29.0', ' 48.0', ' 2.0']    |        17 | ['pan fry bacon , and set aside on a paper towel to absorb excess grease', 'mince yellow onion , red bell pepper , and add to your mixing bowl', 'chop garlic and set aside', 'put 1tbsp olive oil into a saut pan , along with chopped garlic , teaspoons white pepper and a pinch of kosher salt', 'bring to a medium heat to sweat your garlic', 'preheat oven to 350f', 'coarsely chop your baby spinach add to your heated pan , stir frequently for approximately 5 min to wilt', 'add your spinach to the mixing bowl', 'chop your now cooled bacon , and add it to the mixing bowl', 'add your meatloaf mix to the bowl , with one egg and mix till thoroughly combined', 'add your goat cheese , one egg , 1 / 8 tsp white pepper and 1 / 8 tsp of kosher salt and mix till thoroughly combined', 'transfer to a 9x5 meatloaf pan , and cook for 60 min or until the internal temperature is at least 160f', 'let stand for 5min', 'melt 1tbsp unsalted butter into a frying pan , and cook up to three eggs at a time', 'crack each egg into a separate dish , in order to prevent egg shells from reaching the pan , then add salt and pepper to taste', 'wait until the egg whites are firm looking , but slightly runny on top before flipping your eggs', 'after flipping , wait 10~20 seconds before removing each egg and placing it over your slices of meatloaf'] | ready, set, cook! special edition contest entry: a mediterranean flavor inspired meatloaf dish. featuring: simply potatoes - shredded hash browns, egg, bacon, spinach, red bell pepper, and goat cheese.                                                                                                                                                                         | ['meatloaf mixture', 'unsmoked bacon', 'goat cheese', 'unsalted butter', 'eggs', 'baby spinach', 'yellow onion', 'red bell pepper', 'simply potatoes shredded hash browns', 'fresh garlic', 'kosher salt', 'white pepper', 'olive oil'] |              13 |            5 | complex      |


### Univariate Analysis

Below is the histogram representing the distribution of values for the n_ingredients column. This helps give us a deeper understanding of how many ingredients are contained in each recipe and also explains why 9 ingredients is a good cutoff for determining whether a dish is complex or simple. The red line represents the median value of the distribution and, as you can see, it is centered around 9.

<iframe src="univariateplot1.html" width=800 height=600 frameBorder=0></iframe> 

Below is a histogram showing the distribution of avg_rating for all the recipes. As you can see, the red line represents the mean average rating across all recipes. This plot will be helpful for explaining the bivariate analysis as well.

<iframe src="univariateplot2.html" width=800 height=600 frameBorder=0></iframe> 

### Bivariate Analysis

Below is a bar chart which examines the mean avg_rating for simple recipes vs. complex recipes. The plot shows that the mean is about the same for each group because, as seen in the histogram above, most of the ratings across all recipes are 5. Therefore, when we group the number of ingredients, we would expect that the average rating across groups is close to 5.

<iframe src="bivariateplot1.html" width=800 height=600 frameBorder=0></iframe>

### Interesting Aggregates

Grouping the number of ingredients and examining the aggregate statistics mean can help us to understand if there is a relationship between the complexity of a recipe (as indicated by the number of ingredients) and its cooking time and rating. This is because recipes with a higher number of ingredients may require longer cooking times, but may also result in more complex and flavorful dishes, leading to higher ratings. By grouping the recipes based on the number of ingredients and calculating the average cooking time and rating for each group, we can identify any patterns or trends in the data and determine if there is a correlation between the number of ingredients, cooking time, and rating. This can help us to make more informed decisions about recipe development, as well as provide insights into the preferences of consumers when it comes to recipe complexity and cooking time.


|   minutes |   n_steps |   n_ingredients |   avg_rating |   calories |   total_fat (PDV) |   sugar (PDV) |   sodium (PDV) |   protein (PDV) |   saturated_fat (PDV) |   carbohydrates (PDV) |
|----------:|----------:|----------------:|-------------:|-----------:|------------------:|--------------:|---------------:|----------------:|----------------------:|----------------------:|
|   96.9493 |  12.6287  |        12.7353  |      4.62307 |    503.609 |           38.6573 |       69.3078 |        33.3543 |         41.6396 |               46.1697 |               15.71   |
|  106.663  |   8.20179 |         6.55755 |      4.62708 |    374.326 |           28.0727 |       68.1805 |        25.6126 |         26.7148 |               35.7703 |               12.3359 |

---

## Assessment of Missingness

The columns in the ``recipes`` DataFrame that contain missing values are: ``name``, ``description``, and ``avg_rating``.

Here, we will conduct permutation tests on two columns against the ``description_missing`` column in order to determine whether the ``description`` column is Missing at Random (MAR) since it would depend on the values of that other column. In order to conduct the test, we will consider the following hypotheses with an $\alpha$ of 0.05:

* **Null Hypothesis:** There is no significant difference between the two distributions of the column when the description is missing or not missing.
* **Alternate Hypothesis:** There is a significant difference between the distributions of the column when the description is missing vs. when the description is not missing.

Additionally, we will be using the **Total Variation Distance (TVD)** as our test statistic in this permutation test since we are dealing with a categorical distribution.

