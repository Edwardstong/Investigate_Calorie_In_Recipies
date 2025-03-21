# InvestigateCaloriesInRecipes
This is a project for DSC 80 at UCSD.

## Introduction
We have access to two main DataFrames, recipes (83,782 rows × 12 columns) and 
interactions (731,927 rows × 5 columns), from Food.com, containing information 
on thousands of recipes and their nutritional content. This dataset allows us to
explore what contributes to higher-calorie recipes. Specifically, we seek to 
answer: What types of recipes tend to have the most calories?
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

The histogram displays the distribution of calories in various recipes, showing a right-skewed distribution. Most recipes have a calorie count between 0 and 400, with the highest concentration around 150-250 calories. 

###  Plotly plot of the relationship between total fat/carbohydrates/total sugar and calories
<iframe
  src="assets/figure_28.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This scatter plot visualizes the relationship between Total Fat, Total Sugar, and Carbohydrates with Calories. The positive trend observed suggests that as the nutrient values increase, the calorie content also increases. Notably, Total Sugar (orange) and Carbohydrates (green) exhibit a sharp upward correlation, while many data points of of the total fat category lies in the bottom layer of the plot. **Below is a Plot that only shows the relationship between total fat and calories for clearer depiction.**

###  Plotly plot of the relationship between total fat and calories
<iframe
  src="assets/figure_27.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

### Mean calories for each year.
**Table: Mean calories for each year.**

| submitted_year | 2008  | 2009  | 2010  | 2011  | 2012  | 2013  | 2014  | 2015  | 2016  | 2017  | 2018  |
|---------------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|-------|
| **calories**  | 418.85 | 427.92 | 416.97 | 454.81 | 425.33 | 456.58 | 478.59 | 452.44 | 538.80 | 743.52 | 979.43 |

**Explanation of the Table**  
The table presents the average calorie content of recipes submitted each year from 2008 to 2018. Each column represents a year, while the corresponding values indicate the **average calories per recipe** submitted in that year.  
From 2008 to 2015, the average calorie content fluctuates between **~418 to ~478 calories**, showing **moderate variation** in recipe calorie levels. In 2016, a noticeable increase to **538.8 calories** occurs. The most significant jumps appear in **2017 (743.52 calories)** and **2018 (979.43 calories)**, indicating a rapid rise in high-calorie recipe submissions.  

**Significance of the Table**  
The data suggests that recipes have been gradually increasing in calorie content, with a sharp rise after 2015. This could indicate a **shift towards richer, more indulgent recipes** in recent years. Understanding calorie trends helps analyze **whether people are favoring higher-calorie recipes over time**, which could reflect changes in cooking habits, food preferences, or even societal dietary trends. If the trend continues, it may have implications for **public health, dietary recommendations, and consumer food choices**.

## Assessment of Missingness
I believe the **"description"** column in the dataset could be Not Missing at Random (NMAR). The likelihood of missingness in this column may be related to the nature of the recipes themselves. For example, contributors might intentionally leave the description blank for well-known recipes, assuming users already understand them. Since NMAR missingness depends on the unobserved values of the missing data itself, it is difficult to correct using standard missing data techniques. However, to determine if the missingness could instead be **Missing at Random (MAR)**, I would need additional data, such as Recipe popularity. (If lower-rated recipes tend to have missing descriptions, it may suggest that users are less engaged with them, shifting the missingness toward MAR.)

### **Missingness Permutation Test of description column on submitted column**

The permutation test was conducted to determine whether the missingness of the **"description"** column in the dataset is **dependent on the "submitted" date**. 

#### **Null Hypothesis (H₀)**
The missingness of the **"description"** column is **independent** of the submission date, meaning missing values occur randomly concerning when a recipe was submitted.

#### **Alternative Hypothesis (H₁)**
The missingness of the **"description"** column **depends on the submission date**, indicating that certain time periods have a higher likelihood of missing values.

#### **Results of the Permutation Test**
- The **p-value** from the test is calculated as the proportion of test statistics (from the randomized permutations) that are **greater than or equal** to the observed absolute difference in submission dates for missing vs. non-missing descriptions.
- The result of `p < 0.05` suggests that we **reject the null hypothesis** at a **5% significance level**.

#### **Interpretation**
Since the p-value is less than 0.05, we have **statistical evidence** that the missingness of the **"description"** column is **not missing completely at random (MCAR)**. Instead, it is likely related to the **submission date**, which means the missingness could be **Missing at Random (MAR) or Not Missing at Random (NMAR)**.

This finding suggests that **newer or older recipes might have systematically different levels of missing descriptions**. Further investigation into submission trends, contributor behavior, or platform policy changes over time could help clarify why descriptions are more frequently missing for certain submission periods.

### **The empirical distribution of the test statistic used in the permutation test testing the association of missing description and submitted date, along with the observed statistic.**  
<iframe
  src="assets/plot8.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


### **Missingness Permutation Test of description column on n_steps column**  

The permutation test was conducted to determine whether the missingness of the **"description"** column in the dataset is **dependent on the "n_steps"** column.  

#### **Null Hypothesis (H₀)**  
The missingness of the **"description"** column is **independent** of the number of steps (**n_steps**), meaning missing values occur randomly concerning the complexity of a recipe.  

#### **Alternative Hypothesis (H₁)**  
The missingness of the **"description"** column **depends** on the number of steps (**n_steps**), indicating that recipes with fewer or more steps might be more likely to have missing descriptions.  

#### **Results of the Permutation Test**  
- The **p-value** from the test is calculated as the proportion of test statistics (from the randomized permutations) that are **greater than or equal** to the observed absolute difference in **n_steps** for missing vs. non-missing descriptions.  
- The result of **p > 0.05** suggests that we **fail to reject the null hypothesis** at a **5% significance level**.  

#### **Interpretation**  
Since the **p-value is greater than 0.05**, we **do not have statistical evidence** to suggest that the missingness of the **"description"** column depends on the **number of steps (n_steps)** in a recipe. This indicates that the missingness of the **"description"** column is **Missing Completely at Random (MCAR)** with respect to **n_steps**.  

This finding suggests that the complexity of a recipe (as measured by **n_steps**) **does not influence whether a description is missing**. Further investigation into other variables, such as contributor behavior or recipe submission time, may provide better insight into the missingness pattern.  

####  Plotly plots
<iframe
  src="assets/plot5.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

<iframe
  src="assets/plot6.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>


## **Hypothesis Testing: The Relationship Between Recipe Ratings and Calories**

### **Null Hypothesis (H₀)**  
The **caloric content** of a recipe is **independent** of whether the recipe is **highly rated** (average rating ≥ 4.0). In other words, highly rated recipes do not tend to have significantly different calorie levels compared to lower-rated recipes.

### **Alternative Hypothesis (H₁)**  
Recipes that are **highly rated** (average rating ≥ 4.0) tend to have **higher calorie content** compared to their lower-rated counterparts (average rating < 4.0).

### **Test Statistic and Significance Level**
The test statistic used in this permutation test is the **difference in mean calorie content** between **highly rated recipes** and **lower-rated recipes**.  

- This choice is appropriate because it allows us to measure whether there is a significant difference in calories between the two groups.  
- We set our **significance level (α) at 0.05 (5%)**, which is a common threshold in statistical hypothesis testing.

### **Permutation Test and p-value**  
- The test generates a **null distribution** by randomly shuffling the `"if_highly_rated"` labels across recipes 1,000 times and recalculating the test statistic each time.  
- The **p-value** is calculated as the proportion of test statistics from the permutations that are **less than or equal to the observed difference** in mean calories.  
- The resulting **p-value is less than 0.05** (p < 0.05), which means that the observed difference is unlikely to have occurred by random chance under the null hypothesis.

### **Conclusion**  
Since the **p-value is below our significance threshold (0.05)**, we **reject the null hypothesis** in favor of the alternative hypothesis. This suggests that **highly rated recipes tend to have more calories than lower-rated recipes**.  

However, this result **does not prove causation** we cannot definitively say that higher calorie content causes a recipe to be rated more highly. There may be other factors influencing both **recipe ratings** and **caloric content**, such as taste preferences or the types of recipes that tend to receive more reviews.  


## Framing a Prediction Problem
**Prediction problem: what is the amount of calories in a given recipe.** The prediction of the **calories** column is based on various attributes such as ingredients, preparation time, number of steps, and nutritional components. Since the target variable, **calories**, is a **continuous variable**, this is a **regression problem**, and I have chosen **linear regression**. I selected **R²** as the evaluation metric because it measures how well the independent variables explain the variability in calorie content. Unlike error-based metrics such as **RMSE (Root Mean Squared Error)**, R² provides an intuitive measure of model performance by indicating the proportion of variance explained. A high R² value suggests that our features significantly contribute to predicting calorie content, whereas a low R² would indicate that additional features or more complex models may be needed.


## Baseline Model
The model is a **linear regression model** designed to predict the **calories* using features **average rating_per_recipe and carbohydrates**. All features in the model are **quantitative**. Since I did not include any **ordinal** (ranked categories) or **nominal** (categorical) variables, no encoding was necessary. I trained the model on a cleaned dataset, ensuring that missing values were removed. To evaluate the model’s performance, I used **R² (coefficient of determination)**, which resulted in **0.6727 on the test set**, and an average **cross-validated R² of 0.6403**, indicating that the model explains about **64% of the variance in calorie content**. While this suggests moderate predictive power, I do not believe the current model is "good" enough, as it likely misses other influential factors such as **ingredients, fat content, and preparation methods**. To improve the model, I could incorporate additional **nutritional attributes and interaction terms** to better capture the complexity of calorie prediction.

Baseline Model: **calories = 142.706 + 5.89×avg_rating_per_recipe + 18.67×carbohydrates**


## Final Model
For my final model, I added several new features, including **total fat, total sugar, total protein, carbohydrates, average rating per recipe, number of steps, and number of ingredients** into consideration. Additionally, I created **interaction features** such as **total sugar × carbohydrates** to capture potential relationships between these nutritional components. These features were chosen based on their logical connection to calorie content—recipes high in fat, sugar, or carbohydrates are naturally expected to have higher caloric values. The interaction terms were introduced to account for cases where multiple factors jointly contribute to calorie content rather than acting independently.

I used **linear regression** as the modeling algorithm, similar to the baseline model, but incorporated **QuantileTransformer** for normalizing skewed variables and making seperate features from that, ensuring that the model could capture relationships more effectively. To identify the best combination of features, I performed **exhaustive feature selection using pairwise combinations** and evaluated performance using **5-fold cross-validation**. The best-performing feature combination included **total fat and carbohydrates**, which makes sense as they are the primary factors contributing to calorie count.

Final Model: **calories = 50.230 + 6.59×avg_rating_per_recipe + 11.94×carbohydrates**

Compared to the **baseline model**, which only used **average rating per recipe and carbohydrates** and achieved an **R² of approximately 0.64**, the final model demonstrated a **higher R², improving overall predictive performance**. The inclusion of **nutritionally relevant features and interaction terms** allowed the model to better capture the complexity of calorie determination. This improvement suggests that a more holistic view of recipe composition, rather than relying solely on high-level indicators like ratings, leads to **better calorie predictions**.

## Fairness Test
The fairness analysis aimed to determine whether the model predicts caloric content more accurately for highly-rated recipes (≥ 4.0) compared to lower-rated recipes (< 4.0) using R² scores as the evaluation metric. A permutation test was conducted, randomly shuffling the rating labels and recalculating the difference in R² scores 1000 times to assess whether any observed differences were due to chance. The resulting p-value (0.723) was greater than 0.05, meaning we fail to reject the null hypothesis. This indicates that the model performs similarly for both highly-rated and lower-rated recipes, with no significant bias favoring one group over the other. Therefore, the model is fair in predicting calorie content regardless of a recipe's rating.