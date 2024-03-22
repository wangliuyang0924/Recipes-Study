# Recipes Study



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
Describe how you cleaned and prepared your data for analysis. Include any exploratory data analysis (EDA) you performed with findings.
### Explarotory Data Anaylsis


## Assessment of Missingness
### NMAR Analysis
Missing 'descriptions' could be NMAR if the missingness relates to the content or nature of the recipes themselves. For example, simpler recipes or those that are widely known may not have a description because the contributor assumes that users are already familiar with the dish. In this case, the missingness is related to the nature of the recipe, which is not observed in the data. Additional data that might help explain the missingness and thereby making it MAR could include the complexity level of the recipe or a categorization of the recipe's commonality/uniqueness.
### Missingness Dependency
Assuming a 90% significance level for interpreting the results of our permutation tests related to the missingness of the description column in your dataset, the findings present a nuanced perspective. For the rating column, where we observed a p-value of 0.058, this value falls below the 90% confidence threshold (equivalent to a significance level of 0.10). This suggests that at a 90% confidence level, there is a statistically significant dependency of description missingness on the recipe ratings. Specifically, the negative observed difference implies that recipes with slightly lower ratings are more likely to be missing descriptions, indicating that user engagement or perceived quality (as inferred from ratings) might influence the completeness of the recipe's metadata, including the presence of descriptions.

Conversely, the permutation test for the minutes column resulted in a p-value of 0.408, which is well above the 0.10 threshold, indicating no significant dependency of description missingness on the preparation time of the recipes. Despite the intuitive expectation that more complex or time-consuming recipes (with longer preparation times) might be more likely to include detailed descriptions, the statistical analysis does not support this hypothesis at the 90% confidence level.

In summary, adopting a 90% significance level allows us to discern a subtle pattern where the presence of ratings (and possibly their values) influences whether a recipe includes a description, while the preparation time does not.

## Hypothesis Testing
Null Hypothesis (H0): There is no correlation between the preparation time (minutes) and the calorie content (calories) of recipes.
Alternative Hypothesis (H1): There is a significant correlation between the preparation time (minutes) and the calorie content (calories) of recipes.
Permutation Test:

To test these hypotheses, we perform a permutation test to assess the significance of the correlation coefficient between minutes and calories. This test will shuffle one of the variables while keeping the other fixed, thereby breaking any real association between them, and then compute the correlation coefficient for each permutation. This approach allows us to create a distribution of correlation coefficients under the null hypothesis that there's no association between preparation time and calorie content.

Interpretation of the Results:
The observed correlation coefficient between preparation time (minutes) and calorie content (calories) of recipes is approximately 0.005, suggesting a slight positive correlation. Given our analysis with a 90% significance level, we find a p-value of 0.024. This p-value indicates that the observed correlation is statistically significant at the 95% level, allowing us to reject the null hypothesis (H0) in favor of the alternative hypothesis (H1). Therefore, there is significant evidence to suggest a correlation between the preparation time of recipes and their calorie content.

This result implies that recipes requiring longer preparation times might tend to have slightly higher caloric content, which could be due to various factors such as the complexity of the recipe, the number of ingredients used, or the cooking methods involved. It's important to note, however, that while the correlation is statistically significant, the strength of the association is relatively weak, as indicated by the correlation coefficient value.


## Framing a Prediction Problem

Explain how you framed the prediction problem within your project. Describe the target variable and the features used for prediction.

## Baseline Model

Describe the baseline model you used for comparison. Include information on how it was implemented and its performance metrics.

## Final Model

Provide details about your final model. Discuss why it was chosen, its architecture, and how it improves upon the baseline model. Include performance metrics.

## Fairness Analysis

Explain how you conducted a fairness analysis of your models. Discuss any biases identified and how you addressed them.
