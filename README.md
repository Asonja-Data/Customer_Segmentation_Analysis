# Customer_Segmentation_Analysis

## Table of Contents
1. [Project Overview](#project-overview)
2. [Scope](#scope)
3. [Column Description](#column-description)
4. [Data Loading and Cleaning](#data-loading-and-cleaning)
   - [Installation and Setup](#installation-and-setup)
   - [Load the Dataset](#load-the-dataset)
   - [Check Data Structure](#check-data-structure)
   - [Convert Date Column to DateTime](#convert-date-column-to-datetime)
5. [Descriptive Statistics](#descriptive-statistics)
   - [Age Distribution](#age-distribution)
   - [Gender Distribution](#gender-distribution)
6. [Time Series Analysis](#time-series-analysis)
   - [Monthly Sales Trend](#monthly-sales-trend)
   - [Daily Sales Trend](#daily-sales-trend)
7. [Customer and Product Analysis](#customer-and-product-analysis)
   - [Total Spending per Customer](#total-spending-per-customer)
   - [Purchase Frequency](#purchase-frequency)
   - [Top-Selling Product Categories](#top-selling-product-categories)
   - [Revenue Contribution by Product Category](#revenue-contribution-by-product-category)
8. [Visualization](#visualization)
   - [Customer Segmentation using RFM Analysis](#customer-segmentation-using-rfm-analysis)
     - [Compute RFM Metrics](#compute-rfm-metrics)
     - [Apply K-Means with Optimal K](#apply-k-means-with-optimal-k)
9. [Recommendations](#recommendations)
10. [Repository Structure](#repository-structure)
11. [Author](#author)
12. [License](#license)

## Overview
This project focuses on customer segmentation on a dataset from an e-commerce platform using data analysis techniques. The objective is to clean, analyze, and understand customer behavior and segment them into different groups based on their purchasing patterns.

## Project Scope
This project scope defines the boundaries and deliverables for the customer segmentation analysis. It clarifies what is included in the project and what is excluded to manage expectations and ensure project focus.
Inclusions:
- Data Cleaning and Preprocessing
- Exploratory Data Analysis (EDA)
- Descriptive analysis
- Customer Segmentation using K-Means Clustering
- Visualization
- Insights and recommendations

## Data source
- <a href="https://github.com/Asonja-Data/Customer_Segmentation_Analysis/blob/main/ifood_df.csv">Dataset</a>

## Dataset Descriptions
- File Name: Customer_Segmentation_Analysis.ipynb
- Size: 2205 rows x 39 columns 
- Column Description

| Column Name	| Description |
|-------------|-------------|
| Income	| Annual income of the customer |
| Kidhome	| Number of children at home |
| Teenhome	| Number of teenagers at home |
| Recency |	Number of days since the last purchase |
| MntWines	| Amount spent on wine products |
| MntFruits	| Amount spent on fruit products |
| MntMeatProducts |	Amount spent on meat products |
| MntFishProducts	| Amount spent on fish products |
| MntSweetProducts |	Amount spent on sweet products |
| MntGoldProds	| Amount spent on gold products |
| NumDealsPurchases	| Number of purchases using a discount |
|NumWebPurchases	| Number of purchases made through the website |
| NumCatalogPurchases	| Number of purchases made using a catalog |
| NumStorePurchases	| Number of purchases made directly in-store |
| NumWebVisitsMonth	| Number of visits to the company’s website in a month |
| AcceptedCmp3	1 | if customer accepted campaign 3, 0 otherwise |
| AcceptedCmp4	1 | if customer accepted campaign 4, 0 otherwise |
| AcceptedCmp5	1 | if customer accepted campaign 5, 0 otherwise |
| AcceptedCmp1	1   | if customer accepted campaign 1, 0 otherwise |
| AcceptedCmp2	1 | if customer accepted campaign 2, 0 otherwise | 
| Complain	1 | if customer complained in the last 2 years, 0 otherwise |
| Z_CostContact |	Constant feature (unused in analysis) |
| Z_Revenue |	Constant feature (unused in analysis) |
| Response	1 | if customer accepted the last campaign, 0 otherwise |
| Age	| Customer’s age |
| Customer_Days |	Number of days since the customer’s registration |
| marital_Divorced	1 | if the customer is divorced, 0 otherwise |
| marital_Married	1 | if the customer is married, 0 otherwise |
| marital_Single	1 | if the customer is single, 0 otherwise |
| marital_Together	1 | if the customer is in a relationship, 0 otherwise |
| marital_Widow	1 | if the customer is a widow, 0 otherwise |

## Methodology
1. Data Loading
  Pandas library was used to load the dataset, also, the required libraries for the analysis were imported.
  Libraries Used:
  •	numpy – Provides support for numerical computations.
  •	pandas – Used for data manipulation and analysis.
  •	seaborn – Helps in creating statistical visualizations.
  •	matplotlib.pyplot – A plotting library for data visualization.
  •	scipy.stats – Contains statistical functions, including correlation measures.
  The first five rows were  displayed to ensure the dataset is successfully loaded and ready for exploration.

2.  Initial Data Exploration
  - Step 1: Missing values check (no missing values found)
  - Step 2: Duplicate rows check (184 duplicate rows)
  - Step 3: Data type inspection
  - Step 4: Unique values count
  
3. Data Cleaning
  - Step 1: Removing duplicates

  This step was to ensure data integrity and prevents skewed analysis due to redundant entries. 
  
  - Step 2: Removal of Unnecessary Columns

  The columns Z_CostContact and Z_Revenue have all the same values. These columns will not help us to understand our customers better, hence, were deemed unnecessary for 
  the customer segmentation analysis and were therefore dropped from the dataset using the data.drop() function.


4. Explorative Data Analysis
  - Step 1: Descriptive Analysis
  - Step 2: Visualization 
  - Step 3: Correlation Analysis

      - Pearson Correlation for MntTotal, income, and age
      - Correlation analysis of MntTotal with demographics and children

        Analysis of the correlation matrix reveals a strong positive correlation between 'MntTotal' and income, and a moderate negative correlation between 'MntTotal' and 
        'Kidhome'. Furthermore, income demonstrates a moderate negative correlation with 'Kidhome', similar in magnitude to the correlation observed between 'MntTotal' and 
        'Kidhome', this suggests a potential relationship between income level and household size.
      
      - Point-Biserial correlations between MntTotal and marital status
      - Point-Biserial correlations MntTotal and education
      
        Statistical analysis indicates no strong point-biserial correlation between 'MntTotal' and marital status. Similarly, while education level demonstrates a weak 
        association with 'MntTotal' (with marginally higher spending observed among customers with PhDs and lower spending among those with Basic education), the magnitude 
        of 
        the effect suggests that other factors are more salient in predicting spending behavior.

8. Data Transformation

  Feature Engineering: For analytical purposes, a binary variable, 'In_relationship', derived from the 'marital_status' data was created. This feature indicates whether a 
  customer is married or living with a partner, allowing us to explore the relationship between relationship status and other customer attributes. 
  For plotting purposes, a 'marital' column was created. This new column combines the data from the five one-hot encoded marital status columns ('marital_Divorced', 
  'marital_Married', 'marital_Single', 'marital_Together', 'marital_Widow') into a single 'marital' category, enabling the creation of more informative visualizations.
   
 

9. Customer Segmentation

K-means clustering was applied to segment customers based on behaviour and purchase patterns. 

- Step 1: Standardization

  The mean value for all columns is almost zero and the standard deviation is almost 1. All the data points were replaced by their z-scores, thus ensuring that all features 
  have equal importance in the model.
  
- Step 2: Principal component analysis

  PCA reduces the dimensionality to two principal components and then adds these two principal components as new columns ('pc1' and 'pc2') to the DataFrame. The first 
  principal component (pc1) captures the most variance, followed by the second (pc2).

- Step3: K-Means clustering

  Elbow method:
  Based on this Elbow Method plot, K=4 appears to be the most likely candidate for the optimal number of clusters. However, the lack of a very sharp elbow suggests that the 
  data might not have very well-defined clusters or that other values of K (5 or 6) could also be explored

  Silhouette Score Analysis:
  There is a peak in the line graph around K=5, suggesting that 5 might be the optimal number of clusters.
  Since the Elbow Method suggested K = 5, and the Silhouette Score also improves slightly at K = 5–6, K = 5 is a reasonable choice.
  
- Step 4: Cluster profiling


## Insights
Cluster Descriptions: 
  - "Cluster 1: High-Spending Professionals. This segment is characterized by high income, high total spending ('MntTotal'), and a moderate number of children at home. They 
   tend to purchase wine and meat products frequently." 
  - "Cluster 2: Budget-Conscious Families. This segment has moderate income, lower total spending, and a higher number of children at home. They are more price-sensitive and 
   tend to make more purchases using discounts."

Business Implications:
  - "Cluster 1: High-Spending Professionals. This segment represents a valuable target for premium products and personalized offers. They are less price-sensitive and more 
   likely to respond to targeted marketing campaigns focused on quality and exclusivity."
  - "Cluster 2: Budget-Conscious Families. This segment is more likely to respond to promotions and discounts. They might be interested in bundled offers or loyalty 
   programs."

## Recommendations: 
- "Develop targeted marketing campaigns for each cluster, tailored to their specific needs and preferences."
- "Consider developing new products or services that cater to the needs of specific clusters."
- "Implement a loyalty program to reward high-value customers in Cluster 1."

## Limitations:
- "The K-means algorithm is sensitive to the initial choice of centroids, and the results might vary slightly with different initializations." 
- "The data is from a single e-commerce platform and might not be representative of all customers." 
- "The analysis is based on past purchase behavior and might not accurately predict future behavior."


