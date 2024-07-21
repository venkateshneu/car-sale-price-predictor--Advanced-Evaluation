Introduction and Dataset Overview:
In today’s competitive automotive market, understanding customer demographics and their impact on car pricing is crucial for effective sales strategies. To assist a recent car dealership in navigating this complex landscape, we are building a predictive model to estimate car prices based on various customer attributes. This model aims to provide the dealership with valuable insights into how different demographic factors influence car pricing, enabling them to set strategic prices and better target their marketing efforts. The goal is to enhance their decision-making process and gain a competitive edge in the market.

The dataset employed in this analysis includes 15,000 records with 13 features that provide a comprehensive view of both car sales and customer demographics. Key variables include the target price paid and several customer attributes, such as age and income, which are critical for predicting pricing. Categorical features like vehicle type and brand add depth to the analysis by capturing customer preferences. This diverse dataset is instrumental in developing a predictive model that reflects real-world dynamics and supports the dealership in making informed, data-driven decisions.

Data Cleaning:
1. Handling Outliers:
Outlier Removal Process:

Age Criterion:

Reasoning: Individuals under 18 are not legally eligible to buy a car. Data from those under 20 may be less representative of typical car buyers, leading to skewed analysis.
Action Taken: Removed records where age was below 20 to reflect a realistic customer profile.
Number of Rows Removed: 285 out of 15,000 rows were removed due to age being below 20.
Income Distribution:

Income data for individuals under 20 was unrealistic and inconsistent with typical car-buying patterns, which led to their removal for more accurate analysis.
Inconsistencies Observed:

Income: Values were inconsistent with expected car-buying behavior.
Credit Score: Scores were unusually high or low.
PreviousCarOwned: Numbers sometimes exceeded plausible limits.
PricePaid: Amounts paid were inconsistent with the buyer's age and reported income.
Impact on Dataset: Out of the initial 15,000 rows, 285 were removed, leaving 14,715 rows. By addressing outliers early, the dataset’s integrity is preserved, leading to more reliable insights for car price prediction.

2. Handling Missing Data:
Age: 12.23% missing. KNN imputer was used after age-related outliers were removed. Group mean imputation distorted the distribution, so KNN was chosen to better preserve the age distribution and handle missing values.
Income: 21.94% missing. KNN imputer was applied to maintain consistency in the income distribution. The method ensured that the imputed values did not skew the distribution, preserving its realism for car price predictions.
CreditScore: 7.99% missing. KNN imputer was used to handle missing values while maintaining the integrity of the distribution. This approach preserved the CreditScore distribution, which is crucial for accurate predictive modeling.
MaritalStatus: 21.04% missing. Mode imputation by YearsOwnedPrevCar was applied, resolving all missing values. This approach was chosen to reflect the most common marital status within each group, ensuring consistency with real-world patterns.
3. Duplicates:
No duplicate records were found in the dataset.

4. Encoding:
VehicleType: Applied ordinal encoding due to inherent order (e.g., SUV vs. Sedan), resulting in a significant increase in the R-squared score.
Other Categorical Variables: One-hot encoding was used for Brand, Gender, and Region to convert them into numerical format for model compatibility.
Exploratory Data Analysis (EDA):
1. Description of Income Data for Ages Under 20:
Histogram: Shows the distribution of income for individuals under 20. It reveals a concentration of incomes around $67,000 to $77,000 with a slight skew towards higher incomes.
Boxplot: Highlights income outliers and provides a summary of income distribution. The median income is about $77,000, with some significant outliers indicating incomes beyond $100,000.
2. Violin Plots Analysis:
VehicleType: SUVs exhibit a wider price distribution compared to Sedans, indicating greater variability in the prices paid for SUVs.
Brand: Ford, Chevy, and Dodge exhibit distinct patterns. Ford and Chevy have relatively similar price distributions, but Dodge stands out with a slightly higher median price and a more compact distribution.
3. Bar Chart Analysis:
The average prices are consistent across regions and vehicle types, with minor variations based on the number of cars owned previously.
Checking Multicollinearity and P-values Calculation:
Multicollinearity:
Age (VIF = 20.35) and Income (VIF = 28.40) show high multicollinearity, suggesting they may be redundant.
CreditScore (VIF = 61.04) has the highest VIF, indicating a strong correlation with other features.
VehicleType (VIF = 1.99) and other categorical variables like Brand and Region have lower VIFs, implying less multicollinearity.
P-values:
Income (p < 1e-200) and CreditScore (p < 1e-121) are highly significant predictors of PricePaid.
VehicleType (p = 0.00) shows significant influence on PricePaid.
Age (p = 0.2719) and PreviousCarOwned (p = 0.9395) are less significant.
Brand_Ford (p = 0.2816) and Gender_Male (p = 0.4615) have higher p-values, implying lower relevance in predicting the target variable.
Model-1: Development and Evaluation
Model Development:
Feature Scaling: All features were standardized using StandardScaler to ensure equal contribution to the model's performance.
Model Training: A linear regression model was trained on the standardized data.
Model Evaluation:
R-squared Value: The R-squared value for the model was 0.584, indicating that approximately 58.4% of the variability in car prices can be explained by the features included in the model.
Akaike Information Criterion (AIC): The AIC for the model was 234,092.01.
Model-2: Stepwise Selection Process
Model Development:
In Model 2, a stepwise selection process was used to identify the most relevant predictors. Initially, no features were included in the model. Features were added sequentially based on their p-values, selecting those with values below 0.05 to ensure statistical significance.

Model Evaluation:
R-squared Value: The stepwise model had an R-squared of 0.5831.
Akaike Information Criterion (AIC): The AIC for the stepwise model was 234,080.12, indicating a better fit after accounting for the complexity of the model.
Comparison:
The stepwise selection model's lower AIC suggests a more efficient model. While the R-squared values are similar, the stepwise model's focus on significant variables offers better interpretability and relevance.

Recommendations for Business Focus:
1. Vehicle Type:
Coefficient: 4967.65
Implications: Tailor inventory and marketing strategies to highlight SUVs, which command higher prices.
2. Brand (Dodge):
Coefficient: 2375.46
Implications: Focus on promoting Dodge vehicles to maximize profits.
3. Income:
Coefficient: 1226.72
Implications: Set strategic pricing tiers and tailor financing options to different income groups.
4. Number of Kids:
Coefficient: -1130.74
Implications: Promote family-friendly vehicles and offer special financing plans for families.
5. Credit Score:
Coefficient: 1003.29
Implications: Implement risk-based pricing strategies and provide resources to help customers improve their credit scores.
Conclusion:
Focusing on these significant variables—VehicleType, Brand_Dodge, Income, NumKids, and CreditScore—will enable the dealership to make data-driven decisions that align with customer preferences and purchasing power. By strategically managing inventory and customizing marketing and financing plans, the dealership can enhance its market positioning, attract more customers, and ultimately drive higher sales and profitability.

