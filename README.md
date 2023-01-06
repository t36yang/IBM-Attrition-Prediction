# IBM Attrition Prediction - People Analytics #
“Why did my employees want to leave?”

This is the first question that most leaders would ask when there’s an increasing trend of turnover rate at their company. Popular hypotheses to answer this question are related to “income level”, “age generation”, “job satisfaction”, “work life balance”, etc. While there are numerous reasons for employees' departure, what are the factors that company leads should target the most with limited time and resources? Is it possible to predict attrition in the future to prevent the serious implications for the business? 

Through conducting calculations over IBM Attrition Dataset using five different machine learning algorithms and exploratory data analysis, recommendations and an attrition model will be made to predict attrition in employees and help business leaders formulate strategies to improve employees retention and workforce planning. 
![High-employee-turnover](https://user-images.githubusercontent.com/117051182/211091642-b6042f6a-242d-4b3c-893d-b0cc626e8fe8.jpeg)

## Dataset Description ##
“Attrition at IBM” dataset consists of 1470 data points, of which 237 belong to the employees who left the company. The dataset was retrieved from [Kaggle](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset/"Kaggle") on January 2, 2022.

The dataset includes the employees information for three departments: Sales, Human Resources, Research & Development.  

On the dataset there were 35 features populated, including: income, personal information, job satisfaction, training time, department, job level, etc.

Other features might be needed for the analysis but were not included: termination reason (involuntary/voluntary), location, employee type (regular or contract).

## Preprocessing - Data Cleaning and Feature Engineering ##
Through running a heatmap to examine the correlations between different features, the following columns are removed for data cleanness:
* Job Level: highly correlated with income. Removed due to redundancy. 
* Monthly Rate and Hourly Rate: inaccurate labeling of the data. Removed due to inaccuracy. 
* Over 18: only one unique value in the dataset. Removed due to purposeless information. 

The following features are created to the deepen the analysis: 
* Turnover rate: examining the ratio of attrition workers in different generations, income level, ratings (job satisfaction, involvement, worklifebalance), etc. 
* Yearly Income (Annualized income): for easier visualization and interpretation. 
* Income Distribution: grouping employees’ annualized incomes by 20, 50, 75 percentiles to analyze target income levels on the same scale. 

The following features are converted to binary categories for model fitting:
* Target: ‘Attrition’ - Yes : 1, No : 0
* Overtime - Yes : 1, No : 0

## Variables and Hypothesis
Dependent variable is “Attrition”  and independent variables are : 'Age', 'DistanceFromHome', 'Education', 'EnvironmentSatisfaction', 'JobInvolvement', 'JobSatisfaction', 'NumCompaniesWorked', 'OverTime', 'PercentSalaryHike', 'PerformanceRating', 'RelationshipSatisfaction','StockOptionLevel', 'TotalWorkingYears', 'TrainingTimesLastYear','WorkLifeBalance', 'YearsAtCompany', 'YearsInCurrentRole','YearsSinceLastPromotion', 'YearsWithCurrManager', 'YearlyIncome'.

The classification prediction model is expected to use the Independent Variables to predict the Dependent variable. 

Null Hypothesis: there’s no influence of the independent variables to dependent variable
Alternative Hypothesis: there’s an impact of the independent variables to the dependent variable. 

## Exploratory Data Analysis ##
#### Department vs Gender ####
As the chart shows below, there are more male workers than females in all departments. R&D has more employees than Sales and HR. Due to the differences in the number of employees for the three departments, turnover rate will be calculated to display the proportion of certain classes. 


![general gender](https://user-images.githubusercontent.com/117051182/211094026-c1380278-719c-4b9d-af23-2a90e1a56704.png)

#### Age vs Annual Income vs Attrition ####
The green dots are the employees who are no longer with IBM. As the chart shows, the majority of the attrition employees are ~ 30 years old and below 50k. As the age progresses to above 30, the number of attrition begins to reduce and the income enters in the 100k range. 
Note that 0 indicates the active employees and 1 indicates the attrition employees. 


![Attrition age ](https://user-images.githubusercontent.com/117051182/211094587-ada867d6-00a2-45ba-afcd-4eaf67771c34.png)


#### Years of Service and Salary Increase Hike Percentage ####
The data also indicates that employees who are with IBM less than 5 years and have less than 12.5 percent salary hike are most likely to leave the company.


![yearsatcompany](https://user-images.githubusercontent.com/117051182/211096093-18cabe09-4032-4a50-8250-f5cb7d61b627.png) ![percentsalaryhike](https://user-images.githubusercontent.com/117051182/211096044-daba60b4-9858-41da-a5b7-7b75b330500d.png)

#### Turnover Rate by Different Job Roles ####
In terms of turnover rate by job roles, the sales reps are showing to have the highest turnover following laboratory technicians and human resources.


![turnover rate by dept](https://user-images.githubusercontent.com/117051182/211094740-8b6998a3-44cd-444f-af11-7f30e057303b.png)

#### Income Distribution for Departed Employees ####
Comparing the income level for active and attrition employees, there’s a spike in the number of attrition employees below 50k. 

Attrition Employee Income Distribution

![income distribution](https://user-images.githubusercontent.com/117051182/211094972-bf34ac16-da90-489a-8860-1ce1dfe1cd9f.png)

#### Job Satisfaction, Job Involvement, Work Life Balance vs Attrition Employees ####
For job satisfaction, job involvement, worklifebalance, the results are consistent that the higher scores of these factors the more likely that employees are willing to stay at the company.

![Turnover Rate Job Satisfaction](https://user-images.githubusercontent.com/117051182/211095285-aea855df-a9c2-4b4c-a732-c2b96427d7dd.png)

Human Resources (45%)  has the highest turnover in the employees who rated "1" for Job Satisfaction 

![turnover job involvement](https://user-images.githubusercontent.com/117051182/211095339-73f9c247-6959-429b-9828-572fa20ea210.png)

Sales has the highest turnover in the employees who rated "1" for Job Involvement 

![turnover rate worklife bal](https://user-images.githubusercontent.com/117051182/211095372-7b409475-9c60-41e7-b39d-f7fb4a9103e5.png)

Sales (37.5%) has the highest turnover in the employees who rated "1" for work life balance 

#### Age Generation vs Turnover Rate ####
Younger age groups (Millennials and Gen Z) have higher turnover rates

![gen](https://user-images.githubusercontent.com/117051182/211095577-8c0f27aa-392a-4b66-b3ce-e117aaf26dbf.png)

#### Distance from home vs Attrition ####
Out of curiosity, a chart was produced to review the correlation between distance from home and attrition. Surprisingly, distance from home doesn’t influence attrition result. 

![distancefromhome](https://user-images.githubusercontent.com/117051182/211096654-9e8020e7-d086-4fc8-a1e6-5fe9286715be.png)

## Prediction Machine Learning Models ##
There were five machine learning model performed and below are the results after tuning:

<img width="724" alt="Screen Shot 2023-01-06 at 3 45 08 PM" src="https://user-images.githubusercontent.com/117051182/211097135-d45b18e4-6d6b-4575-b2ba-bca84b24d59e.png">

Amongst the prediction results from the five models, Logistic Regression model result was chosen as it displays higher scores overall. 

The Rate of Change line graph below confirms the selection as the yellow line (Logistic Regression) is closer towards the 1.0 True positive. 

![download](https://user-images.githubusercontent.com/117051182/211097338-99f7d986-b70a-46e0-bd11-6d9aed80e396.png)

Based on the result, the prediction model is able to achieve a higher than 80% for Accuracy but there’s not enough dataset to predict a better score for Precision, Recall and F1. Due to the imbalanced dataset for the target feature, it is more reasonable to review all scores to avoid a biased analysis. 

Below is the confusion matrix that it displays the overall test scores for the prediction model:

![confusion](https://user-images.githubusercontent.com/117051182/211097530-7a4c7c1b-5cb2-4d79-8f41-71d6b601d218.png)


True Attrition (positive): 18 False Attrition (positive): 24 True Active (negative): 243 False Active (negative): 12

Although the prediction model requires further adjustment and dataset to achieve a higher prediction score, it is important to review what are the important features that contribute to both Attrition and Active employees.

![factors](https://user-images.githubusercontent.com/117051182/211098243-f2a0bac8-5e74-44fc-b80e-fbdbbe9e5b95.png)

Depending on the business problem that the team aims to tackle, a weighted feature chart was created to display the major factors that contribute to result employee Attrition and the factors that made employees stay. 

Main factors for Attrition: 
* Yearly Income, EnvironmentSatisfaction, Age
* Main factors for staying at the company:
* Education, Numcompaniesworked, YearsWithCurrentMgr


## Recommendations to IBM ##
* To reduce turnover rate for the Sales, HR and R&D department, it is recommended to consider increasing the salary, improving the work environment.
* Emphasizing on implementing employee retention programs for younger age employees to decrease the chances of leaving IBM at an early career stage. 
* Conduct managerial training for managers to get managers educated over the topic of talent retention as Years with Current Manager is one of the top factors for retaining employees.
* Provide an education assistance program if there’s any to help employees get more educated. 

## Summary: Challenges and Next Step ##

As the dataset was extracted from an online source, the dataset is missing certain important information such as the reasons for employee leaving (voluntary or involuntary), time series information for performance score, attendance, job satisfaction, etc. To predict attrition, external factors should also be considered such as unemployment rate, industry information, inflation rate, etc. 

For next steps, I hope to obtain the missing data and re-build the prediction model to achieve better prediction results. 



