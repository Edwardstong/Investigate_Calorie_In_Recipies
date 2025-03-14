# InvestigateCaloriesInRecipies
This is a project for DSC 80 at UCSD.

## Introduction
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

- **nutrition: A list containing calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates, with percentages of the daily recommended value (PDV)**

- **n_steps: Number of steps in recipe**

- **n_ingredients: Number of ingredients in recipe**

- **rating: The rating given to the recipe**

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning Process
1. Left merge the recipes and interactions datasets together.

2. In the merged dataset, fill all ratings of 0 with np.nan

3. Find the average rating per recipe, as a Series.

4. Add this Series containing the average rating per recipe back to the recipes dataset

The data cleaning and transformation steps I performed were essential for ensuring that the dataset was structured, meaningful, and ready for analysis. First, I merged the recipes and interactions datasets using a left merge, ensuring that all recipes remained in the dataset even if they had no associated interactions. This step was crucial to preserving as much data as possible while linking recipe information with user interactions. During this process, I replaced all ratings of 0 with NaN, as a rating of 0 likely represents a missing or invalid rating rather than a true numerical value. Keeping 0s in the dataset could bias average ratings downward, misrepresenting user feedback.

To further enhance our understanding of recipe popularity, the average rating per recipe was calculated from the interactions dataset. This transformation enabled me to quantify recipe quality based on user feedback. I then added this Series back to the recipes dataset, allowing future models or analysis to incorporate a recipe’s average rating as an additional feature. By doing this, I ensured that recipes could be ranked and compared based on user preferences. 

Lastly, I addressed the nutrition column, which contained values stored as strings that resembled lists. Since this format prevented direct numerical analysis, I converted the string into an actual list and extracted each nutrient into separate columns (calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates). This allowed for easier feature selection, filtering, and numerical computations in later analysis.

These steps improved the usability of the dataset, eliminated inconsistencies, and provided structured, numerical data for more accurate and insightful analysis.

<iframe
  src="assets/file-name.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>