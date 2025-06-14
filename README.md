# Quick Recipes Analysis
By Jensen Emi

## Introduction
For my project, I decided to do an analysis on the recipes and ratings dataset. Cooking is an important skill to learn as an adult. It's something that many people love to do while others may not enjoy as much. Personally, I think it's fun to try new recipes out but there are some downsides. As someone who is busy with school and work, sometimes I just want to make a quick and easy meal. That's why I chose to focus on the types of recipes that take the shortest amount of time to make. I have two datasets to analyze, recipes and ratings, and hopefully my question will be answered.

Our first dataset, recipes, has 83782 rows and 12 columns. Each row represents one recipe. Here is a description of the columns:

| Column             | Description                                                                                                                                                                                       |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `'name'`           | Recipe name                                                                                                                                                                                       |
| `'id'`             | Recipe ID                                                                                                                                                                                         |
| `'minutes'`        | Minutes to prepare recipe                                                                                                                                                                         |
| `'contributor_id'` | User ID who submitted this recipe                                                                                                                                                                 |
| `'submitted'`      | Date recipe was submitted                                                                                                                                                                         |
| `'tags'`           | Food.com tags for recipe                                                                                                                                                                          |
| `'nutrition'`      | Nutrition information in the form [calories (#), total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat (PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value” |
| `'n_steps'`        | Number of steps in recipe                                                                                                                                                                         |
| `'steps'`          | Text for recipe steps, in order                                                                                                                                                                   |
| `'description'`    | User-provided description                                                                                                                                                                         |
| `'ingredients'`    | Ingredients in recipe                                                                                                                                                                              |
| `'n_ingredients'`  | Number of ingredients in recipe                                                                                                                                                                   |

Our second dataset, ratings, has 731927 rows and 5 columns. Again, each row represents one rating. Here is a description of the columns:

| Column         | Description |
|----------------|-------------|
| 'user_id'      | User ID     |
| 'recipe_id'    | Recipe ID   |
| 'date'         | Date of interaction |
| 'rating'       | Rating given |
| 'review'       | Review text |

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
First, I merged our two datasets together and created a column containing the average rating per recipe. Here are the steps:
1. Left merge the recipes and interactions datasets together.
2. In the merged dataset, fill all ratings of 0 with np.nan.
   Justification: Since our rating scale is from 1 to 5, a rating of 0 indicates that there is a missing value there. We need to fill any 0s with np.nan to make sure missing values have no effect on the average rating. A value of 0 would greatly bring down the rating.
3. Find the average rating per recipe, as a Series.
4. Add this Series containing the average rating per recipe back to the recipes dataset however you’d like (e.g., by merging). Use the resulting dataset for all of your analysis. 

Our resulting dataset has 83782 rows and 13 columns since we added a new columns called 'avg_ratings'.

Now, if we take a look at our nutrition column, we notice that it looks like each row contains a list. However, it turns out that those are just strings that look like lists. I decided to create columns for each of the values in the list. Now, we have columns for calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates. 

Our resulting dataset has 83782 rows and 20 columns since we split up the values in nutrition to be their own column.

Since our question focuses on the types of recipes, I decided to choose five different categories of recipes to compare the cooking time. My five categories are: dessert, breakfast, vegan, dietary, and holiday-event. Each category is its own column. I went through the tags of the recipes and returned True if the tags contained the name of the category and False otherwise.

Our resulting dataframe has 83782 rows and 25 columns since we added boolean values for each of the types of recipes we're analyzing. I removed some of the columns that are unrelated to the question we're trying to answer. Here are the first five rows of the cleaned dataframe:

| name                               | minutes | n_steps | n_ingredients | calories (#) | carbohydrates (PDV) | dessert | breakfast | vegan | dietary | holiday-event |
|------------------------------------|---------|---------|----------------|---------------|----------------------|---------|-----------|-------|---------|----------------|
| 1 brownies in the world best ever  | 40      | 10      | 9              | 138.4         | 6.0                  | True    | False     | False | False   | False          |
| 1 in canada chocolate chip cookies | 45      | 12      | 11             | 595.1         | 26.0                 | False   | False     | False | False   | False          |
| 412 broccoli casserole             | 40      | 6       | 9              | 194.8         | 3.0                  | False   | False     | False | False   | False          |
| millionaire pound cake             | 120     | 7       | 7              | 878.3         | 39.0                 | True    | False     | False | True    | True           |
| 2000 meatloaf                      | 90      | 17      | 13             | 267.0         | 2.0                  | False   | False     | False | False   | False          |

### Univariate Analysis
For the univariate analysis, I created a bar plot of the number of recipes per type. 

<iframe
  src="assets/univariate.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

As we can see, there are almost 50,000 recipes with the tag dietary, less than 15,000 dessert recipes, less than 10,000 holiday-event recipes, about 5,000 breakfast recipes and less than 5,000 recipes with the tag vegan.

### Bivariate Analysis
For the bivariate analysis, I created another bar plot of average number of minutes it takes for each recipe type.

<iframe
  src="assets/bivariate.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

We can see that by far, breakfast takes the least amount of time out of the five categories. The other four recipe types are close in average time.

### Interesting Aggregates
I created a pivot table to show the relationship between the recipe types and calories. I calculated the maximum, mean, median, and minimum of calories for each of the recipe types.

| **category**     | breakfast | dessert  | dietary  | holiday-event | vegan   |
|------------------|-----------|----------|----------|----------------|---------|
| **calorie_stats**|           |          |          |                |         |
| **max_cal**      | 22371.20  | 28930.20 | 36188.80 | 26604.40       | 6485.60 |
| **mean_cal**     | 374.21    | 512.36   | 408.56   | 473.45         | 275.50  |
| **median_cal**   | 285.50    | 287.15   | 292.60   | 292.60         | 196.70  |
| **min_cal**      | 0.90      | 0.30     | 0.00     | 0.00           | 0.00    |

The pivot table shows that vegan recipes tend to be lower in calories compared to other recipes. 

## Assessment of Missingness
### NMAR Analysis
In our merged dataset, 'description', 'rating', and 'review' contain the most missing values. Out of these columns, I think the 'review' column is NMAR. Similar to an example from class, people that feel strongely about the recipe, good or bad, are more likely to leave a review. This results in more missing values for reviews since not everyone will feel strongly about the recipe and want to leave a review. 

### Missingness Dependency
For this section, I chose to analyze the 'rating' column and perform permutation tests to see the dependency of missingness of this column on other columns. First, we'll compare the 'rating' and 'minutes' columns. Our null hypothesis is that the missingness of ratings does not depend on the number of minutes. Our alternate hypothesis is that the missingness of ratings does depend on the number of minutes. The test statistic is the absolute difference in means and the significance level is 0.05. After performing the permutation tests, I created a histogram to display the results. 

<iframe
  src="assets/missing.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The p-value is 0.109 which is greater than our significance level, so we fail to reject the null hypothesis which means the missingness of 'rating' does not depend on 'minutes'.

Now, we'll compare 'rating' and 'n_steps'. Our null hypothesis is that the missingness of ratings does not depend on the number of steps. Our alternate hypothesis is that the missingness of ratings does depend on the number of steps. The test statistic is the absolute difference in means and the significance level is 0.05. After performing the permutation tests, I created another histogram to display the results. 

<iframe
  src="assets/missing2.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The p-value is 0.0 which is less than our significance level, so we reject the null hypothesis which means the missingness of 'rating' depends on the number of steps. 

## Hypothesis Testing
The project is focused on finding whih types of recipes take the shortest amount of time to make. Now, I'll perform a permutation test to answer this question. I chose to do a permutation test over a hypothesis test because as we saw earlier, the number of each recipe type varies in size. The null hypothesis is breakfast takes the same amount of time to make as the other types of recipes. The alternate hypothesis is breakfast takes less time to make than the other types of recipes. The test statistic is the difference in mean between minutes of breakfast recipes and non-breakfast recipes. I chose my test statistic to just be the difference and not the absolute difference since my alternate hypothesis is that breakfast takes less time to make and not that breakfast takes a different amount of time to make than the other recipe types. The significance level is 0.05 which is a common significance level to use. 

<iframe
  src="assets/hyptest.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

The p-value is 0.076 which is greater than 0.05, so we fail to reject the null hypothesis that breakfast recipes take the same amount of time as other recipes. 

## Framing a Prediction Problem
### Problem Identification
My prediction problem is to predict the number of minutes it takes to prepare recipes before cooking starts. This is a regression problem because we're dealing with minutes which is a continuous variable. The response variable is number of minutes to prepare the recipe. I chose minutes as my response variable because it is the best representation of how long something takes to cook. It's helpful in letting people know how long they should plan on cooking for. For my metric, I chose to use root mean squared error because it is able to show how close or far our prediction is from the actual time. It'll give me a better idea of the accuracy of the predictions than other metrics. 

At the time of prediction, we would know all of the information listed in the recipe. Depending on the person and their cooking skill level, we wouldn't know how long the recipe will take to make, but we'll know the number of ingredients, nutritional information, etc.

## Baseline Model
My baseline model uses 'n_ingredients' and 'carbohydrates (PDV)' for the features. All of these features are quantitative with 'carbohydrates (PDV)' being continuous and 'n_ingredients' being discrete. Initially, there were too any outliers so I had to create a new dataframe only containing recipes that took 110 or less minutes to make. I split the data into training and test sets and then created a pipeline with a random forest regressor. After fitting the model and making predictions, I calculated the root mean squared error of my prediction and actual time. The root mean squared error of my baseline model is 22.144 minutes which means my predictions are off. I believe my model could be better. 22 minutes is a lot of time, especially when the recipes included in my model take 110 minutes or less to cook.

## Final Model
My final model uses 'n_ingredients', 'carbohydrates (PDV)', 'n_steps', and 'calories (#)' for the features. I added 'n_steps' because I thought it could be helpful in predicting how long a recipe will take to make. If there are more steps, then it possibly takes longer. I also added 'calories (#)' because I thought there may be some relation between minutes and how many calories are in a recipe. Something quick and easy to make might have less calories in it. Both of these features reflect the complexity of a recipe and how long it takes to make. 

I used the RandomForestRegressor as my modeling algorithm. To improve my baseline model, I also used GridSearchCV to make my final model more accurate. For the hyperparameters, I chose n_estimators and max_depth since they performed the best. When n_estimators was 526 and max_depth was 7, it performed the best. I chose my hyperparameters by trial and error and just seeing what combination had the best result. 

My metric, root mean squared error, for my final model is 20.55 minutes which is about 2 minutes less than my baseline model prediction. Since my final model is a little more accurate than my baseline model, I would say overall it was an improvement. 

## Fairness Analysis
For the fairness analysis, group X consisted of vegan recipes and group Y consisted of non-vegan recipes. I used RMSE as my evaluation metric since I built a regression model. Also, I chose RMSE over R^2 because RMSE makes it easier to see how far off the predictions are from the actual values.

Null Hypothesis: Our model is fair. Its prediction error for vegan recipes and non-vegan recipes are roughly the same, and any differences are due to random chance. 

Alternative Hypothesis: Our model is unfair. Its prediction error for vegan recipes is higher than its prediction error for non-vegan recipes.

For my test statistic, I calculated the RMSE of vegan and non-vegan recipes and subtracted them, vegan RMSE minus non-vegan RMSE. I set the significance level at 0.05. My resulting p-value is 0.276, so we fail to reject the null hypothesis. There is not enough evidence to say the model's error for vegan recipes is higher than its error for non-vegan recipes. 










