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

**Head of the cleaned DataFrame**

**Note:** [...] was used to shorten long values for tags, steps, and description.

| Name                                   | ID       | Minutes | Contributor ID | Submitted  | Tags  | Nutrition                                    | N Steps | Steps | Description                                 | Avg Rating Per Recipe | Calories | Total Fat | Total Sugar | Total Sodium | Total Protein | Saturated Fat | Carbohydrates | 
|----------------------------------------|----------|---------|---------------|------------|-------|---------------------------------------------|---------|-------|--------------------------------------------|-----------------------|----------|-----------|-------------|--------------|--------------|--------------|--------------|
| 1 brownies in the world best ever     | 333281   | 40      | 985201        | 2008-10-27 | [...] | [138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0]    | 10      | [...] | these are the most; chocolatey, moist,... | 4.0                   | 138.4    | 10.0      | 50.0        | 3.0          | 3.0          | 19.0         | 6.0          |
| 1 in Canada chocolate chip cookies    | 453467   | 45      | 1848091       | 2011-04-11 | [...] | [595.1, 46.0, 211.0, 22.0, 13.0, 51.0, 26.0] | 12      | [...] | this is the recipe that we use at my ...  | 5.0                   | 595.1    | 46.0      | 211.0       | 22.0         | 13.0         | 51.0         | 26.0         |
| 412 broccoli casserole                | 306168   | 40      | 50969         | 2008-05-30 | [...] | [194.8, 20.0, 6.0, 32.0, 22.0, 36.0, 3.0]   | 6       | [...] | since there are already 411 recipes f... | 5.0                   | 194.8    | 20.0      | 6.0         | 32.0         | 22.0         | 36.0         | 3.0          |
| Millionaire pound cake                | 286009   | 120     | 461724        | 2008-02-12 | [...] | [878.3, 63.0, 326.0, 13.0, 20.0, 123.0, 39.0] | 7       | [...] | why a millionaire pound cake? Because... | 5.0                   | 878.3    | 63.0      | 326.0       | 13.0         | 20.0         | 123.0        | 39.0         |
| 2000 meatloaf                         | 475785   | 90      | 2202916       | 2012-03-06 | [...] | [267.0, 30.0, 12.0, 12.0, 29.0, 48.0, 2.0]  | 17      | [...] | ready, set, cook! special edition co... | 5.0                   | 267.0    | 30.0      | 12.0        | 12.0         | 29.0         | 48.0         | 2.0          |



###  Plotly plot of the calories column
<iframe
  src="assets/dist_calories.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>