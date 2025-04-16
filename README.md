# SQL Customer Analysis

This project uses *PostgreSQL* to analyze a customer dataset sourced from kaggle. The goal is to uncover insights about customer behavior using SQL — focusing on how factors like *gender, age, income, profession, and family size* influence spending habits.

## Tools Used
- PostgreSQL for querying and analysis
- GitHub for documentation and version control

## What I Learned
- How to group and segment data using GROUP BY and CASE
- How to clean data using COALESCE to handle missing values
- How to analyze real-world customer data to generate business insights
- How to structure a SQL project for a portfolio using README and GitHub

## Key Business Questions Answered
- Which gender spends more on average?
- How does age affect spending behavior?
- Do high-income earners really spend more?
- Which professions are the biggest spenders?
- Does family size affect how people spend?

## Dataset
- Source: [Kaggle - Customer Dataset](https://www.kaggle.com/datasets/datascientistanna/customers-dataset)
- Columns: CustomerID, Gender, Age, Annual Income, Spending Score, Profession, Family Size

## SQL Queries & Insights

## 1. Average Spending Score By Gender

SELECT gender,

AVG(spending_score) AS avg_spending

FROM customers

GROUP BY gender;

Explanation:
This query shows the average spending score for male and female customers.

Insight:
Female customers have a slightly higher average spending score than males. Marketing campaigns can be adjusted based on gender behavior.

## 2. Spending Score By Age Group

SELECT 

	CASE
 
		WHEN age BETWEEN 18 AND 25 THEN '18-25'
  
		WHEN age BETWEEN 26 AND 35 THEN '26-25'
  
		WHEN age BETWEEN 36 AND 45 THEN '36-45'
  
		ELSE '46+'
  
	END AS age_group,
 
	COUNT(*) AS total_customers,
 
	AVG(spending_score) AS avg_spending
 
FROM customers

GROUP BY age_group

ORDER BY age_group;

Explanation:
This query groups customers into age ranges and calculates the average spending score per group.

Insight:
The 18–25 age group has the highest average spending score, showing strong purchasing behavior. Adults (26–35) follow closely.

## 3. Spending Score By Age Group And Gender

 SELECT 
 
	CASE
 
		WHEN age BETWEEN 18 AND 25 THEN '18-25'
  
		WHEN age BETWEEN 26 AND 35 THEN '26-35'
  
		WHEN age BETWEEN 36 AND 45 THEN '36-45'
  
		ELSE '46+'
  
	END AS age_group,
 
	gender,
 
	COUNT(*) AS total_customers,
 
	AVG(spending_score) AS avg_spending
 
FROM customers

GROUP BY age_group, gender

ORDER BY age_group, gender;

Explanation:
This query gives deeper insight by combining age group and gender to analyze how each subgroup behaves in terms of spending.

Insight:
Young adult males (18–25) and adult males (26–35) appear to have the highest spending scores. Female customers in general are more active spenders across all age ranges.

## 4. Average Spending Score BY Income Range

SELECT 

	CASE 
 
		WHEN annual_income BETWEEN 0 AND 30000 THEN 'Low'
  
		WHEN annual_income BETWEEN 31000 AND 60000 THEN 'Mid'
  
		WHEN annual_income BETWEEN 61000 AND 90000 THEN 'Upper-mid'
  
		ELSE 'High'
  
	END AS income_level,
 
	COUNT(*) AS total_customers,
 
	AVG(spending_score) AS avg_spending
 
FROM customers 

GROUP BY income_level

ORDER BY income_level;

Explanation:
This query categorizes customers based on their income level and shows the average spending score in each group.

Insight:
The high-income group has the highest average spending score, followed closely by the mid-income group.
However, the upper-mid group spends less on average, which may signal an opportunity for engagement or a need to investigate further.

## 5. Average Spending Score By Profession
   
SELECT 

	COALESCE(profession, 'Unknown') AS profession,
 
	COUNT(*) AS total_customers,
 
	AVG(spending_score) AS avg_spending
 
FROM customers

GROUP BY COALESCE(profession, 'Unknown');

Explanation:
This query groups customers by their profession (replacing missing values with “Unknown”) and calculates the average spending score for each profession. It helps identify which types of professionals are more likely to spend.

Insight:
Customers in the Entertainment and Artist professions have the highest average spending scores (≈52.9 and ≈52.7), showing strong purchasing behavior.
Professions like Doctors and those in Healthcare also have relatively high spending scores.
Meanwhile, Homemakers, Lawyers, and Marketing professionals spend slightly less on average.
The “Unknown” group (those without a listed profession) has the lowest spending score, which may represent students, unemployed individuals, or data gaps.

## 6. Average Spending Score By Family Size

SELECT

 	family_size,
  
	COUNT(*) AS total_customers,
 
	AVG(spending_score) AS avg_spending
 
FROM customers

GROUP BY family_size;

Explanation:
This query analyzes how spending behavior changes depending on the size of a customer’s family. It helps determine if people with larger or smaller families spend more.

Insight:
Customers with a family size of 4 and 5 have the highest average spending scores (≈52.7 and ≈52.2), indicating strong spending behavior among medium-sized families.
Smaller families like those with 1 or 2 members also spend reasonably well (≈49.6–50.3), but not as much as the middle-range.
Interestingly, customers with very large families (7–9) show no significant increase in spending, and in fact, family size 9 has the lowest score (17.0), likely an outlier due to the small count (just 1 customer).
This insight can guide family-oriented promotions or loyalty programs toward 3–5 member households.
