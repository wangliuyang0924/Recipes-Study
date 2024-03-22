# Recipes Study
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


## Introduction

Provide an overview of your project here. Explain the purpose of the project and any relevant background information.

## Data Cleaning and Exploratory Data Analysis

Describe how you cleaned and prepared your data for analysis. Include any exploratory data analysis (EDA) you performed with findings.

## Assessment of Missingness

Discuss how you assessed the missingness in your data. Explain the methods used to handle missing data and justify your choices.

## Hypothesis Testing

Detail the hypothesis tests you performed. Describe the statistical tests used, your hypotheses, and the results.

## Framing a Prediction Problem

Explain how you framed the prediction problem within your project. Describe the target variable and the features used for prediction.

## Baseline Model

Describe the baseline model you used for comparison. Include information on how it was implemented and its performance metrics.

## Final Model

Provide details about your final model. Discuss why it was chosen, its architecture, and how it improves upon the baseline model. Include performance metrics.

## Fairness Analysis

Explain how you conducted a fairness analysis of your models. Discuss any biases identified and how you addressed them.
