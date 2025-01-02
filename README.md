# Student_Depression Analysis

#### What is depression? 
In simple term, depression is a common and serious mental disorder that negatively affects how you feel, think, act, and perceive the world.

#### What is Suicidal thoughts? 

Suicidal thoughts is having abstract thoughts about ending your life or feeling that people would be better off without you. 

## Project Overview

This project analyse the underlying factors contributing to suicidal thoughts and depression among students. The study analyzed a comprehensive dataset of 27,898 students, comprising 12,352 females and 15,546 males, providing valuable insights into the mental health challenges faced by this demographic.
## Data Source and Content 

The main source of this data is Kaggle [Download Here] (https://www.kaggle.com/datasets/hopesb/student-depression-dataset)

This dataset contains these columns:
   * Student ID
   * Gender
   * Age
   * City
   * Profession
   * Cumulative Grade Point Average (CGPA)
   * Sleep Duration
   * Dietary Habits
   * Degree
   * Have you had suicidal thoughts?
   * Work/Study Hours
   * Family History of Mental illness
   * Academic Stress
   * Work Stress
   * Study satisfaction
   * Job satisfaction
   * Depression
   * Financial stress

## Tools Applied

* Power Query for data cleaning
* Power BI for visualization
* SQL for data quering

## Data Cleaning 

To ensure the accuracy of my analysis, I began by removing duplicate entries from my dataset using Excel's shortcut ALT+H+O+I. Next, I imported the data into Power Query for further cleaning and processing.

Upon examining the data, I noticed that certain columns, such as Academic Pressure, Study Satisfaction, Work Pressure, and Financial Stress, contained numerical rankings. To enhance interpretability, I used Power Query's "Conditional Column" feature to assign descriptive labels (e.g., "Low", "Medium", "High") to these rankings, providing a clearer understanding of the data.

Upon further review of the data, I identified three blank rows that required removal. Given the substantial number of students in the dataset, I determined that eliminating these rows would have a negligible impact on my analysis. To efficiently remove the blank rows, I utilized SQL, as I prefer working with SQL queries to streamline data manipulation tasks.

```
SELECT *
FROM [Student Depression Dataset]
WHERE Financial_Stress IS NULL

DELETE FROM [Student Depression Dataset]
WHERE id IN ( 22377,68910,97610)

```

To enhance the clarity of my visualizations, I categorized the "Work/Study Hours" column, creating distinct groups to facilitate easier interpretation. To achieve this, I employed SQL and utilized specific lines of code to efficiently categorize the data.
```
ALTER TABLE [Student Depression Dataset]
ADD Study_Hours_Range VARCHAR(50)

UPDATE [Student Depression Dataset]
SET Study_Hours_Range = 
CASE
WHEN Work_Study_Hours BETWEEN 0 AND 2 THEN '0-2 hrs'
WHEN Work_Study_Hours BETWEEN 3 AND 5 THEN '3-5 hrs'
WHEN Work_Study_Hours BETWEEN 6 AND 8 THEN '6-8 hrs'
WHEN Work_Study_Hours BETWEEN 9 AND 11 THEN '9-11 hrs'
ELSE '12hrs'
END

```
 
## Data Quering

What is the total number of students that are depressed?

```
SELECT Depression, Gender, COUNT(Depression) Total_Depressed
FROM [Student Depression Dataset]
WHERE Depression LIKE 0
GROUP BY Gender, Depression

```

![Depressed (2)](https://github.com/user-attachments/assets/0db32ef7-8765-486e-9cd4-cd8ee9c2a4df)

What is the total number of student who have suicidal thoughts?

```
SELECT Have_you_ever_had_suicidal_thoughts, Gender, COUNT(Have_you_ever_had_suicidal_thoughts) Suicidal_thoughts
FROM [Student Depression Dataset]
WHERE Have_you_ever_had_suicidal_thoughts LIKE 0
GROUP BY Gender, Have_you_ever_had_suicidal_thoughts

```

![Suicidal thoughts (2)](https://github.com/user-attachments/assets/c20c1ed7-81bd-4b55-a553-cf169e4cd4e5)

## Data Visualization

What percentage of students have history of mental illness in their family?

![Md (2)](https://github.com/user-attachments/assets/826d53bb-30fc-4e2a-95d3-36aae67a599a)

This dashboard below answers questions the following questions;

1. What percentage of students that are depressed?
2. What is the relationship between financial stress, academic stress and having suicidal thoughts?
3. What is the relationship between financial stress, academic stress and being depressed?
4. What is the average CGPA?
5. How satisfied they while studying or working?
6. How intense is the work pressure and academic stress? etc.

![Student Depression Dashboasrd 1_page-0001 (1)](https://github.com/user-attachments/assets/4d58d4d6-6512-48b1-8459-48afa05bcaff)

## Conclusion

The analysis reveals that financial stress and family history of mental illness are significant contributors to suicidal thoughts and depression. Notably, financial stress emerges as the predominant factor, highlighting its substantial impact on mental health.

* Key policies to ease financial stress;
    * Increased financial aid
    * Flexible payment sysytem
    * Affordable housing options
    * Mental health support, among others.
  
* Ways to reduce academic stress
    * Time management
    * Good hours of sleep
    * Realistic goals
    * Positive mindset etc. 
