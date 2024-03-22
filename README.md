# The Impact of Nutritional Values on Recipe Popularity
Liuyang Wang

## Introduction
Our investigation revolves around the intriguing question: What common features are associated with the highest-rated recipes? This question seeks to explore various aspects of recipes, such as the number of ingredients, preparation time, nutritional values, and specific ingredients, to determine their impact on a recipe's rating.

This inquiry holds significance for several reasons:
Culinary Enthusiasts and Home Cooks: Understanding the traits of highly rated recipes can inspire cooks to experiment with new recipes or tweak existing ones for better outcomes.
Food Industry Professionals: Insights from this analysis can guide menu planning, recipe development, and marketing strategies.
Nutrition and Health: Analyzing the nutritional aspects of top-rated recipes can offer valuable information for those interested in healthy eating.

The datasets consist of the following:
RAW_interactions.csv has 731,927 rows and 5 columns, containing the information of all recipes. RAW_recipes.csv has 83,782 rows and 12 columns, containing contains reviews and ratings submitted for the recipes in RAW_recipes.csv.

For the purpose of our investigation, the following columns are particularly relevant:
Relevant Columns:
recipe_id: Links recipes with their reviews and ratings.
rating: Represents the average rating a recipe has received from users, crucial for identifying highly rated recipes.
minutes: The time required to prepare the recipe, which could influence its popularity.
nutrition: Details nutritional information, potentially correlating with higher ratings.
n_ingredients: The number of ingredients in a recipe, affecting its appeal.
ingredients: The specific ingredients used, to see if certain ingredients are more common in higher-rated recipes.

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
The data cleaning process commences with a left merge of two datasets, recipes_df and interactions_df, based on the recipe IDs, ensuring all recipes are retained while supplementing them with user interactions. In an effort to refine the dataset further, ratings of 0 are treated as missing values and replaced with np.nan, acknowledging that such ratings could distort the calculation of average ratings by being artificially low. This acknowledgment leads to the calculation of average ratings per recipe, a pivotal step that aggregates user feedback into a meaningful metric, which is then merged back into the recipes dataset, effectively enhancing it with a new column, average_rating, that represents the consensus of user opinions.

Subsequently, the nutrition column undergoes a transformation from a string representation of lists to actual Python lists using ast.literal_eval, facilitating the extraction of detailed nutritional information into distinct columns. This transformation is not just a technical necessity but a significant enhancement that unlocks the nutritional data for more nuanced analysis, allowing for an exploration of recipes in the context of their caloric content, fat, sugar, sodium, protein, saturated fat, and carbohydrates.

Following the nutritional data transformation, the cleaned and enhanced recipes dataset is merged again with the interactions dataset, updating the merged DataFrame with a comprehensive view that includes both recipe details and user interactions. Moreover, the conversion of date and submitted columns to datetime format marks the final touch in the cleaning process, standardizing these columns for any subsequent temporal analysis. This meticulous approach to data cleaning sets a solid foundation for further analysis, ensuring the data is not only comprehensive and detailed but also accurately represents the multifaceted nature of user interactions and recipe details.

| name | id | minutes | contributor_id | submitted | tags | nutrition | n_steps | steps | description | ingredients | n_ingredients | average_rating | calories | total_fat | sugar | sodium | protein | saturated_fat | carbohydrates | user_id | recipe_id | date | rating | review |
|------|----|---------|----------------|-----------|------|-----------|---------|-------|-------------|-------------|----------------|----------------|----------|-----------|-------|--------|---------|---------------|---------------|---------|-----------|------|--------|--------|
| 1 brownies in the world best ever | 333281 | 40 | 985201 | 2008-10-27 00:00:00 | '60-minutes-or-less', 'time-to-make', 'course', 'main-ingredient', 'preparation', 'for-large-groups', 'desserts', 'lunch', 'snacks', 'cookies-and-brownies', 'chocolate', 'bar-cookies', 'brownies', 'number-of-servings' | 138.4, 10.0, 50.0, 3.0, 3.0, 19.0, 6.0 | 10 | 'heat the oven to 350f and arrange the rack in the middle', 'line an 8-by-8-inch glass baking dish with aluminum foil', 'combine chocolate and butter in a medium saucepan and cook over medium-low heat, stirring frequently, until evenly melted', 'remove from heat and let cool to room temperature', 'combine eggs, sugar, cocoa powder, vanilla extract, espresso, and salt in a large bowl and briefly stir until just evenly incorporated', 'add cooled chocolate and mix until uniform in color', 'add flour and stir until just incorporated', 'transfer batter to the prepared baking dish', 'bake until a tester inserted in the center of the brownies comes out clean, about 25 to 30 minutes', 'remove from the oven and cool completely before cutting' | these are the most; chocolatey, moist, rich, dense, fudgy, delicious brownies that you'll ever make.....seriously! there's no doubt that these will be your fav brownies ever for you can add things to them or make them plain.....either way they're pure heaven! | 'bittersweet chocolate', 'unsalted butter', 'eggs', 'granulated sugar', 'unsweetened cocoa powder', 'vanilla extract', 'brewed espresso', 'kosher salt', 'all-purpose flour' | 9 | 4 | 138.4 | 10 | 50 | 3 | 3 | 19 | 6 | 386585 | 333281 | 2008-11-19 00:00:00 | 4 | These were pretty good, but took forever to bake. I would send it ended up being almost an hour! Even then, the brownies stuck to the foil, and were on the overly moist side and not easy to cut. They did taste quite rich, though! Made for My 3 Chefs. |


### Explarotory Data Anaylsis
#### Univariate Analysis
![Alt text](/2.1.png)
![Alt text](/2.2.png)

#### Bivariate Analysis
![Alt text](/newplot.png)
![Alt text](/2.3.png)

#### Interesting Aggregate
| rating_category | calories | minutes | n_ingredients | total_fat |
|:----------------|---------:|--------:|--------------:|----------:|
| Low             |  468.513 | 98.9261 |       9.05613 |   35.1172 |
| Medium          |  425.791 | 87.4976 |       9.20092 |   31.6405 |
| High            |  405.047 | 91.585  |       9.10076 |   29.9404 |
| Very High       |  415.213 |106.924  |       9.04675 |   31.7924 |

## Assessment of Missingness
### NMAR Analysis
Missing 'descriptions' could be NMAR if the missingness relates to the content or nature of the recipes themselves. For example, simpler recipes or those that are widely known may not have a description because the contributor assumes that users are already familiar with the dish. In this case, the missingness is related to the nature of the recipe, which is not observed in the data. Additional data that might help explain the missingness and thereby making it MAR could include the complexity level of the recipe or a categorization of the recipe's commonality/uniqueness.
### Missingness Dependency
Assuming a 90% significance level for interpreting the results of our permutation tests related to the missingness of the description column in your dataset, the findings present a nuanced perspective. For the rating column, where we observed a p-value of 0.058, this value falls below the 90% confidence threshold (equivalent to a significance level of 0.10). This suggests that at a 90% confidence level, there is a statistically significant dependency of description missingness on the recipe ratings. Specifically, the negative observed difference implies that recipes with slightly lower ratings are more likely to be missing descriptions, indicating that user engagement or perceived quality (as inferred from ratings) might influence the completeness of the recipe's metadata, including the presence of descriptions.
![Alt text](/newplot(2).png)

Conversely, the permutation test for the minutes column resulted in a p-value of 0.408, which is well above the 0.10 threshold, indicating no significant dependency of description missingness on the preparation time of the recipes. Despite the intuitive expectation that more complex or time-consuming recipes (with longer preparation times) might be more likely to include detailed descriptions, the statistical analysis does not support this hypothesis at the 90% confidence level.
![Alt text](/newplot(3).png)

In summary, adopting a 90% significance level allows us to discern a subtle pattern where the presence of ratings (and possibly their values) influences whether a recipe includes a description, while the preparation time does not.

## Hypothesis Testing
Null Hypothesis (H0): There is no correlation between the preparation time (minutes) and the calorie content (calories) of recipes.
Alternative Hypothesis (H1): There is a significant correlation between the preparation time (minutes) and the calorie content (calories) of recipes.

To test these hypotheses, we perform a permutation test to assess the significance of the correlation coefficient between minutes and calories. This test will shuffle one of the variables while keeping the other fixed, thereby breaking any real association between them, and then compute the correlation coefficient for each permutation. This approach allows us to create a distribution of correlation coefficients under the null hypothesis that there's no association between preparation time and calorie content.

The observed correlation coefficient between preparation time (minutes) and calorie content (calories) of recipes is approximately 0.005, suggesting a slight positive correlation. Given our analysis with a 90% significance level, we find a p-value of 0.024. This p-value indicates that the observed correlation is statistically significant at the 95% level, allowing us to reject the null hypothesis (H0) in favor of the alternative hypothesis (H1). Therefore, there is significant evidence to suggest a correlation between the preparation time of recipes and their calorie content.

This result implies that recipes requiring longer preparation times might tend to have slightly higher caloric content, which could be due to various factors such as the complexity of the recipe, the number of ingredients used, or the cooking methods involved. It's important to note, however, that while the correlation is statistically significant, the strength of the association is relatively weak, as indicated by the correlation coefficient value.


## Framing a Prediction Problem
Prediction Problem: The objective is to predict the average rating ('average_rating') that a recipe will receive. This is a regression problem because the response variable is continuous, ranging from the lowest to the highest possible rating.

Response Variable: The response variable is 'average_rating'. It is chosen because it quantitatively reflects how well the recipes are received by users, which is the primary interest of this investigation.

Metric for Evaluation: For this project, we choose to use the Root Mean Squared Error (RMSE), which is the square root of the MSE. It is useful because it scales the error to be on the same unit as the response variable and gives a relatively high weight to large errors. This means that improving the RMSE by a small amount could imply significant improvements in model performance.


## Baseline Model
The Linear Regression model was trained to predict the average_rating of recipes based on two quantitative features: minutes and n_steps. These features represent the time required to prepare the recipe and the number of steps in the recipe, respectively. Both features were preprocessed with a StandardScaler to normalize their scale.

The performance of the model is evaluated using the Root Mean Squared Error (RMSE), with a value of approximately 0.490. This metric indicates the average deviation of the predicted ratings from the actual ratings. An RMSE of 0.490 suggests that, on average, the model's predictions are less than half a rating point away from the actual ratings, which could be acceptable depending on the rating scale (typically 1 to 5). However, whether this is considered "good" can vary based on domain-specific thresholds for prediction accuracy.

The coefficients for the model are very small: approximately -0.000751 for minutes and -0.000366 for n_steps, with a y-intercept of about 4.676. The small magnitude of the coefficients suggests that changes in the number of minutes and steps have a very slight impact on the predicted ratings. In practical terms, this could mean that these features do not have a strong influence on how users rate the recipes, or it might indicate that other features not included in the model could have a more significant impact on the ratings.

Given the small coefficients and the RMSE value, while the model might serve as a basic benchmark, its predictive power is limited. It is likely not capturing all the nuances that contribute to a recipe's rating. For the model to be considered "good" in a practical sense, it would ideally need a lower RMSE, suggesting more accurate predictions, and more substantial coefficients for the features, indicating a clearer relationship between these features and the ratings. Further exploration with additional or different features, more complex models, and possibly feature engineering could lead to improved performance.

## Final Model
The final model's performance indicates that it has been successfully fitted with a more complex algorithm (RandomForestRegressor) than the baseline model (which was presumably a simpler model, like Linear Regression). The RandomForestRegressor is an ensemble method that combines the predictions of several decision trees to improve generalizability and robustness over a single decision tree.

The grid search process explored a range of values for n_estimators (the number of trees in the forest) and max_depth (the maximum depth of the trees). The best parameters indicated by the grid search are:

max_depth: None (which means the trees are grown until all leaves are pure or contain less than min_samples_split samples)
n_estimators: 200 (a larger number of trees in the forest, contributing to the ensemble's ability to model the data more accurately)
The model achieved a Root Mean Squared Error (RMSE) of approximately 0.3504, which measures the average magnitude of the errors between the predicted values and the actual values. Lower values of RMSE indicate better fit.

The features added were calories and total_fat, on top of the previously used minutes and n_steps. These were chosen because:

Calories: This is a core nutritional metric that users may consider when rating a recipe, particularly in contexts where dietary preferences or restrictions are relevant (e.g., low-calorie diets).
Total Fat: Similar to calories, the fat content of a recipe could significantly impact user preferences and, subsequently, their ratings, especially considering different health and wellness trends.
These features are good for the prediction task because they directly relate to users' perceptions and decisions about food, which are likely factors in how they rate recipes. By capturing more aspects of the recipes that could influence user ratings, the model can make more informed predictions.

The RandomForestRegressor was chosen because it's less likely to overfit than a single decision tree, is robust to noise, and can model non-linear relationships, which are common in real-world data. The hyperparameters were selected using a grid search with cross-validation, which is a systematic approach to testing different combinations of hyperparameters to find the one that performs best on unseen data.

Comparing the final model's RMSE to the baseline model's RMSE would show an improvement if the baseline RMSE were higher than 0.3504. This would indicate that the final model predicts more accurately, likely due to both the additional features and the more complex modeling algorithm.

## Fairness Analysis
We define Group X as recipes with low-calorie content and Group Y as recipes with high-calorie content. We evaluate the model's performance using the Root Mean Squared Error (RMSE) metric, which measures the average difference between predicted and actual ratings.

Our null hypothesis asserts that the model performs similarly for both groups, and any observed differences are due to random chance. Conversely, the alternative hypothesis posits that there is a significant difference in the model's performance between low-calorie and high-calorie recipes, indicating potential bias.

Test Statistic and Significance Level:
The observed difference in RMSE between the two groups is calculated as 0.022. We conduct a permutation test with a significance level (α) set at 0.05, representing a 5% chance of rejecting the null hypothesis when it is true.

With a resulting p-value of 0.01, which is less than the significance level, we reject the null hypothesis. This indicates strong evidence of a significant difference in model performance between low-calorie and high-calorie recipes. Thus, we conclude that the model may exhibit bias in its predictions based on calorie content, requiring further investigation and potential adjustments to ensure fair and accurate predictions for all recipe types.
