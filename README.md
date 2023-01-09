# IBM Attrition Prediction - People Analytics #
“Why do my employees want to leave?”

This is a question that many leaders would ask when they notice an increasing trend of turnover rate at their company. Possible explanations for this trend include factors such as “income level”, “age generation”, “job satisfaction”, “work life balance”, etc. While there are many reasons that employees may leave, what are the most important for company leaders to focus on, given limited time and resources? Is it possible to predict future attrition and prevent its negative effects on the business? 

By analyzing the IBM Attrition Dataset using five different machine learning algorithms and performing exploratory data analysis, we can make recommendations and create an attrition model to help predict employee attrition and assist business leaders in developing strategies to improve retention and workforce planning. 
![High-employee-turnover](https://user-images.githubusercontent.com/117051182/211091642-b6042f6a-242d-4b3c-893d-b0cc626e8fe8.jpeg)

## Dataset Description ##
“Attrition at IBM” dataset consists of 1470 data points, of which 237 correspond to employees who left the company. The dataset was retrieved from [Kaggle](https://www.kaggle.com/datasets/pavansubhasht/ibm-hr-analytics-attrition-dataset/"Kaggle") on January 2, 2022.

The dataset includes employees information for three departments: Sales, Human Resources, Research & Development.  

On the dataset there were 35 features populated, including: income, personal information, job satisfaction, training time, department, job level, etc.

Other features might be useful for the analysis but were not included: termination reason (involuntary/voluntary), location, employee type (regular or contract).

## Preprocessing - Data Cleaning and Feature Engineering ##
We ran a heatmap to examine the correlations between different features and removed the following columns for data cleaning purposes:
* Job Level: highly correlated with income. Removed due to redundancy. 
* Monthly Rate and Hourly Rate: inaccurate labeling of the data. Removed due to inaccuracy. 
* Over 18: only one unique value in the dataset. Removed due to the lack of useful information. 

The following features are created to the deepen the analysis: 
* Turnover rate: examining the ratio of attrition among different generations, income levels, ratings (job satisfaction, involvement, worklifebalance), etc. 
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
As shown in the chart below, there are more male workers than females in all departments. R&D has more employees than the Sales and HR departments. To account for the differences in the number of employees across departments, we will calculate turnover rate to display the proportion of certain classes. 


![general gender](https://user-images.githubusercontent.com/117051182/211094026-c1380278-719c-4b9d-af23-2a90e1a56704.png)

#### Age vs Annual Income vs Attrition ####
The green dots represent the employees who are no longer with IBM. The chart shows that the majority of these employees are around 30 years old and have an annual income of less than $50,000. As the age increases above 30, the number of employee who leave the company decreases, and the annual income increases to around $100,000. 
Note that 0 indicates the active employees and 1 indicates the attrition employees. 


![Attrition age ](https://user-images.githubusercontent.com/117051182/211094587-ada867d6-00a2-45ba-afcd-4eaf67771c34.png)


#### Years of Service and Salary Increase Hike Percentage ####
The data also suggests that employees who have been with IBM for less than 5 years and have received a salary increase of less than 12.5% are more likely to leave the company.


![yearsatcompany](https://user-images.githubusercontent.com/117051182/211096093-18cabe09-4032-4a50-8250-f5cb7d61b627.png) ![percentsalaryhike](https://user-images.githubusercontent.com/117051182/211096044-daba60b4-9858-41da-a5b7-7b75b330500d.png)

#### Turnover Rate by Different Job Roles ####
In terms of turnover rate by job roles, sales reps have the highest rate of turnover, followed by laboratory technicians and human resources.


![turnover rate by dept](https://user-images.githubusercontent.com/117051182/211094740-8b6998a3-44cd-444f-af11-7f30e057303b.png)

#### Income Distribution for Departed Employees ####
When comparing the income level of active and departing employees, there’s a spike in the number of departing employees with an annual income of less than $50,000. 

Attrition Employee Income Distribution

![income distribution](https://user-images.githubusercontent.com/117051182/211094972-bf34ac16-da90-489a-8860-1ce1dfe1cd9f.png)

#### Job Satisfaction, Job Involvement, Work Life Balance vs Attrition Employees ####
For job satisfaction, job involvement, worklifebalance, the results are consistent that the higher scores of these factors the more likely that employees are willing to stay at the company.

![Turnover Rate Job Satisfaction](https://user-images.githubusercontent.com/117051182/211095285-aea855df-a9c2-4b4c-a732-c2b96427d7dd.png)

Human Resources has the highest turnover among employees who rated their Job Satisfaction as 1 (45% turnover).

![turnover job involvement](https://user-images.githubusercontent.com/117051182/211095339-73f9c247-6959-429b-9828-572fa20ea210.png)

Sales has the highest turnover among employees who rated their Job Involvement as 1 (45% turnover).

![turnover rate worklife bal](https://user-images.githubusercontent.com/117051182/211095372-7b409475-9c60-41e7-b39d-f7fb4a9103e5.png)

Sales has the highest turnover among employees who rated their WorkLifeBalance as 1 (37.5% turnover).

#### Age Generation vs Turnover Rate ####
Younger age groups such as Millennials and Gen Z, have higher turnover rates

![gen](https://user-images.githubusercontent.com/117051182/211095577-8c0f27aa-392a-4b66-b3ce-e117aaf26dbf.png)

#### Distance from home vs Attrition ####
Out of curiosity, we created a chart to review the correlation between distance from home and attrition. Interestingly, distance from home does not seem to significantly impact attrition. 

![distancefromhome](https://user-images.githubusercontent.com/117051182/211096654-9e8020e7-d086-4fc8-a1e6-5fe9286715be.png)

## Prediction Machine Learning Models ##
There were five machine learning model performed and below are the results after tuning:

<img width="724" alt="Screen Shot 2023-01-06 at 3 45 08 PM" src="https://user-images.githubusercontent.com/117051182/211097135-d45b18e4-6d6b-4575-b2ba-bca84b24d59e.png">

Among the prediction results from the five models, we selected Logistic Regression model result because it had the highest overall scores.

The 'Rate of Change' line graph below supports our selection, as the yellow line (Logistic Regression) is closer towards the 1.0 True positive value. 

![download](https://user-images.githubusercontent.com/117051182/211097338-99f7d986-b70a-46e0-bd11-6d9aed80e396.png)

Based on the results, the prediction model is able to achieve an accuracy of more than 80%. However, due to the limited size of the dataset, it is difficult to predict higher scores for precision, recall, and F1. Because the dataset for the target feature is imbalanced, it is important to consider all scores to avoid a biased analysis".

The confusion matrix below shows the overall test scores for the prediction model:

![confusion](https://user-images.githubusercontent.com/117051182/211097530-7a4c7c1b-5cb2-4d79-8f41-71d6b601d218.png)


True Attrition (positive): 18 False Attrition (positive): 24 True Active (negative): 243 False Active (negative): 12

While the prediction model can be improved with further adjustment and a larger dataset, it is important to identify the key features that contribute to both departing and active employees.

![factors](https://user-images.githubusercontent.com/117051182/211098243-f2a0bac8-5e74-44fc-b80e-fbdbbe9e5b95.png)

To address the business problem at hand, we created a weighted feature chart to display the major factors that contribute to employee attrition and the factors that encourage employees to stay. The weights reflect the importance of each feature in relation to the problem being addressed. 

Main factors for Attrition: 
* Yearly Income, EnvironmentSatisfaction, Age
* Main factors for staying at the company:
* Education, Numcompaniesworked, YearsWithCurrentMgr


## Recommendations to IBM ##
To reduce turnover rate in the Sales, HR, and R&D department, we recommend considering the following strategies: 
*Increasing salary and improving the work environment.
*Implementing employee retention programs for younger employees to decrease the likelihood of leaving IBM at an early career stage. 
*Providing managerial training on talent retention, as years with current manager is one of the top factors for retaining employees.
*Offering an education assistance program to help employees further their education. 

## Summary: Challenges and Next Step ##

Since the dataset was extracted from an online source, it is missing important information such as the reasons for employee departure (voluntary or involuntary), time series information for performance score, attendance, and job satisfaction. To more accurately predict attrition, external factors such as unemployment rate, industry information, inflation rate should also be considered. 

For future work, I hope to obtain the missing data and rebuild the prediction model to improve its prediction results. 



