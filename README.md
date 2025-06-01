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

Our resulting dataframe has 83782 rows and 25 columns since we added boolean values for each of the types of recipes we're analyzing. Here is the cleaned dataframe:







