# InvestigateCaloriesInRecipies
This is a project for DSC 80 at UCSD. changedjio

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Introduction Page</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 40px;
            padding: 20px;
            background-color: #f4f4f4;
        }
        .container {
            max-width: 800px;
            background: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.1);
        }
        h1 {
            text-align: center;
            color: #333;
        }
        .content {
            margin-top: 20px;
            padding: 20px;
            min-height: 300px; /* Space for adding content */
            border: 2px dashed #ccc;
            background-color: #fafafa;
        }
    </style>
</head>
<body>

    <div class="container">
        <h1>Introduction</h1>

        <div class="content">
            <p>We have access to two main DataFrames, recipes (83,782 rows × 12 columns) and interactions (731,927 rows × 5 columns), from Food.com, containing information on thousands of recipes and their nutritional content. This dataset allows us to explore what contributes to higher-calorie recipes. Specifically, we seek to answer: What types of recipes tend to have the most calories?
By analyzing factors such as preparation time, number of steps, and ingredient composition, we can identify trends in high-calorie recipes and understand which attributes contribute to their nutritional density. This insight is valuable for home cooks, nutritionists, and food enthusiasts looking to make informed choices about meal planning, whether aiming for indulgence or balanced nutrition.
Our analysis will focus on key columns such as:
minutes: Total time required to prepare the recipe.
nutrition: A list containing calories, total fat, sugar, sodium, protein, saturated fat, and carbohydrates, with percentages of the daily recommended value (PDV).
tags: Food.com’s categorization of the recipe (e.g., "dessert," "low-carb").
description: User-provided descriptions that may hint at rich or calorie-dense ingredients.
By exploring these features, we aim to uncover what defines high-calorie recipes and how they differ from lower-calorie alternatives.
Highly rated recipes (those with a average rating >=4.0) tends to have more calories than their counterparts with average rating <4.0

Whether a recipe is highly rated or not (if it has an average rating >=4.0) does not affect the calories of the recipe.</p>
        </div>
    </div>

</body>
</html>
