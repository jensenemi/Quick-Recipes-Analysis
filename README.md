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
