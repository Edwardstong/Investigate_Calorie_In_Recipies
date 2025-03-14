# InvestigateCaloriesInRecipies
This is a project for DSC 80 at UCSD. changedjio

## H2 Introduction
We have access to two main DataFrames, recipes (83,782 rows × 12 columns) and 
interactions (731,927 rows × 5 columns), from Food.com, containing information 
on thousands of recipes and their nutritional content. This dataset allows us to
explore what contributes to higher-calorie recipes. Specifically, we seek to 
answer: How can we determine the amount of calories?
By analyzing factors such as preparation time, number of steps, and ingredient 
composition, we can identify trends in high-calorie recipes and understand which
attributes contribute to their nutritional density. This insight is valuable for
home cooks, nutritionists, and food enthusiasts looking to make informed choices
about meal planning, whether aiming for indulgence or balanced nutrition.
Our analysis will focus on key columns such as:
nutrition: A list containing calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates, with percentages of the daily recommended value (PDV)

**n_steps: Number of steps in recipe**

**n_ingredients: Number of ingredients in recipe**

**rating: The rating given to the recipe**

By exploring these features, we aim to uncover what defines high-calorie recipes and how they differ from lower-calorie alternatives.
Highly rated recipes (those with a average rating >=4.0) tends to have more calories than their counterparts with average rating <4.0

Whether a recipe is highly rated or not (if it has an average rating >=4.0) does not affect the calories of the recipe.</p>