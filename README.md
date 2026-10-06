DataCo Supply Chain Analytics

Overview

This project presents a statistical and predictive analysis of supply chain delivery performance using the DataCo Supply Chain dataset.

The main objective is to investigate delivery delays, compare different shipping modes, identify geographical patterns, and evaluate whether operational characteristics are associated with the probability of late delivery.

The analysis is performed at the order level, rather than at the individual product-line level, in order to obtain a more meaningful representation of overall order performance.

⸻

Objectives

The main objectives of the analysis are:

* Analyze the distribution of delivery statuses.
* Compare delivery performance across different shipping modes.
* Measure the association between shipping mode and delivery status.
* Evaluate the relationship between delivery performance and order profitability.
* Compare scheduled and actual shipping times.
* Investigate geographical differences in delivery performance.
* Build a predictive logistic regression model for late deliveries.
* Evaluate the predictive performance of the model.

⸻

Dataset

The analysis uses the DataCo Supply Chain Dataset, containing information about orders, customers, products, markets, shipping modes, delivery status, sales and profitability.

The original dataset contains:

* 180,519 observations
* 53 variables

Several variables containing sensitive, unnecessary or unsuitable information for the analysis were removed, including:

* Customer Email
* Customer Password
* Product Image
* Product Description
* Order Zipcode

After cleaning, the dataset contains 48 variables.

The final analysis is performed at the order level, resulting in:

* 65,752 unique orders

⸻

Data Preparation

The original dataset contains multiple rows for individual products belonging to the same order.

Before aggregation, consistency checks were performed to verify that variables describing the overall order were not conflicting within the same order.

In particular, no order was found to have multiple values for:

* Delivery Status
* Shipping Mode
* Market

Therefore, these variables could be represented by their first value when aggregating the dataset by Order Id.

Sales and Order Profit Per Order were aggregated at the order level.

⸻

Exploratory Analysis

Delivery Status

The distribution of delivery status shows a substantial proportion of delayed orders.

Delivery Status

Orders

Percentage

Late delivery

36,048

54.82%

Advance shipping

15,127

23.01%

Shipping on time

11,722

17.83%

Shipping canceled

2,855

4.34%

Shipping Mode and Delivery Performance

Delivery performance varies substantially across shipping modes.

The percentage of late deliveries within each shipping mode is approximately: 

Shipping Mode

Late deliveries

First Class

95.27%

Second Class

76.72%

Same Day

46.15%

Standard Class

38.13% 

The results indicate a strong descriptive relationship between shipping mode and delivery status.

However, these results should not be interpreted as causal effects, since shipping mode is closely related to the scheduled delivery time and other operational characteristics.

Statistical Test

To formally investigate the relationship between Shipping Mode and Delivery Status, a Chi-square test of independence was performed.

The results were:

* Chi-square statistic: 20,168.77
* Degrees of freedom: 9
* p-value: p < 0.001
* Cramér’s V: 0.320

The null hypothesis of independence is rejected.

Therefore, there is a statistically significant association between shipping mode and delivery status.

The value of Cramér’s V indicates a moderate association between the two categorical variables.

Importantly, statistical association does not imply causation.

⸻

Economic Analysis

The relationship between delivery status and order profitability was also investigated.

Mean profit by delivery status was: 
Delivery Status

Mean Profit

Shipping on time

$62.37

Advance shipping

$61.82

Late delivery

$59.37

Shipping canceled

$56.21 

Late deliveries show a slightly lower average profit compared with orders delivered on time.

A Welch’s t-test was then used to compare the mean profit of late and on-time orders.

The results were:

* Mean profit — Late deliveries: $59.37
* Mean profit — On-time deliveries: $62.37
* Difference: -$3.01
* 95% confidence interval: [-6.96, 0.94]
* p-value: 0.136

At the 5% significance level, the difference is not statistically significant.

Therefore, this analysis does not provide sufficient statistical evidence of a difference in average order profit between late and on-time deliveries.

⸻

Shipping Time Analysis

The analysis also compares scheduled and actual shipping times.

A delay variable was defined as:

Delay_Days = Actual Shipping Days - Scheduled Shipping Days

Average results by shipping mode were: 
Shipping Mode

Scheduled

Actual

Difference

Same Day

0.00

0.48

+0.48

First Class

1.00

2.00

+1.00

Second Class

2.00

4.00

+2.00

Standard Class

4.00

4.00

~0.00 
These results provide a descriptive view of operational performance.

However, the relationship between these variables and Delivery Status must be interpreted carefully because delivery status itself is closely related to the comparison between scheduled and actual delivery times.

⸻

Geographical Analysis

Delivery performance was also examined across geographical regions.

A specific analysis was conducted for First Class shipments.

The late-delivery rate remained very high across the regions considered, generally exceeding 90%.

This suggests that the poor delivery performance of First Class shipments is not limited to a single geographical region.

However, regional sample sizes should also be considered before drawing strong conclusions about individual regions.

⸻

Predictive Modeling

A logistic regression model was developed to predict whether an order would be classified as a late delivery.

Canceled orders were excluded from the predictive analysis because they do not represent either late or non-late completed deliveries.

The target variable was defined as:

* 1 = Late delivery
* 0 = Not late

The model uses:

* Shipping Mode
* Market
* Order Region
* Scheduled shipping time

Categorical variables were transformed using one-hot encoding.

Because the dataset contains perfect or near-perfect separation for some categories, a penalized logistic regression was used instead of relying on a standard unregularized logistic regression.

⸻

Model Evaluation

The dataset was divided into:

* 80% training set
* 20% test set

The final test set contained 12,580 orders.

The model achieved:

* Accuracy: 0.693
* ROC-AUC: 0.741

The ROC-AUC value indicates that the model has a meaningful ability to distinguish between late and non-late deliveries. 
The classification results on the test set were:
Class

Precision

Recall

F1-score

Not late

0.59

0.90

0.71

Late

0.88

0.54

0.67 
The model therefore identifies late deliveries with relatively high precision, while its recall for late deliveries is more moderate.

⸻

Key Findings

The main findings of the analysis are:

1. Late deliveries represent 54.82% of all orders, making them the most common delivery status.
2. Shipping mode and delivery status are significantly associated, with a Chi-square statistic of 20,168.77 and Cramér’s V of 0.320.
3. First Class shipments show a particularly high late-delivery rate, with approximately 95% of orders classified as late.
4. Delivery performance differs substantially across shipping modes, although these differences should be interpreted as associations rather than causal effects.
5. Average profit is slightly lower for late deliveries, but the Welch’s t-test does not provide statistically significant evidence of a difference between late and on-time orders.
6. The logistic regression model achieves a ROC-AUC of approximately 0.74, indicating useful predictive information in shipping mode, market and geographical characteristics.

⸻

Methodology

The analysis combines exploratory, inferential and predictive statistical techniques.

The main methods used are:

* Data cleaning and preprocessing
* Aggregation from product-line level to order level
* Descriptive statistics
* Cross-tabulation
* Chi-square test of independence
* Cramér’s V
* Welch’s t-test
* Logistic regression
* Penalized logistic regression
* One-hot encoding
* Train/test split
* Classification metrics
* ROC-AUC
* Data visualization

⸻

Tools

The project was developed using Python.

Main libraries:

* pandas
* numpy
* matplotlib
* scipy
* scikit-learn
* statsmodels

The analysis was developed in Jupyter Notebook. 

Limitations

Several limitations should be considered when interpreting the results.

First, the analysis is observational. Therefore, statistical associations should not be interpreted as causal effects.

Second, shipping mode and scheduled shipping time are strongly related by construction. Consequently, their effects in a predictive model should be interpreted with caution.

Third, the original dataset contains multiple product-level records for the same order. Aggregating these records to the order level simplifies the analysis but may hide product-specific information.

Finally, the Order Profit Per Order variable is aggregated to the order level and should therefore be interpreted as an order-level economic measure rather than as a direct causal measure of the financial impact of delivery delays.

⸻

Conclusion

This project demonstrates how statistical analysis and predictive modeling can be applied to a real-world supply chain dataset.

The analysis identifies substantial differences in delivery performance across shipping modes and geographical areas and confirms a statistically significant association between shipping mode and delivery status.

The predictive model further demonstrates that operational and geographical characteristics contain useful information for identifying orders at higher risk of late delivery.

Overall, the project combines data cleaning, exploratory analysis, statistical inference and machine learning to investigate a practical business problem: understanding and predicting supply chain delivery performance.


