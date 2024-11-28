# Introduction

 My goal was to learn about the data analyst role, exploring key factors such as the highest-paying jobs, the most in-demand skills, and the optimal skill sets for career growth. The following gives insights into the field of data analysis.
 Additionally, this was my attempt at Luke Barousse's SQL case study challenge, the original can be found **[HERE](https://github.com/lukebarousse/SQL_Project_Data_Job_Analysis).**
###### _This project's SQL queries can be found here:_ [🔴](/project_sql) 
# Tools I used
The following tools were used, each helping to shape my approach and streamline the process:

- **SQL :** I spent most of my time using SQL and worked with Visual Studio Code to run queries on the data.
- **PostgresSQL :** I was recommended PostgreSQL as a great tool for managing SQL queries. It provided a reliable environment for working with large datasets.
- **Google Sheets :** Being very familiar with Excel and Google Sheets, I used this for my visualizations of the data.
- **Git & GitHub :** I used Git for tracking changes to my code and GitHub to manage the project and share it with others.
 
# My Analysis

### 1. Highest Paying Data Analyst Jobs
To view the most lucrative data analyst jobs, I used WHERE to filter for 'Data Analyst' jobs that were in New York. This query shows the top 10 best paying data analyst jobs in New York state.

```SQL
SELECT
    job_id,
    job_title,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date,
    name AS company_name
FROM
    job_postings_fact
LEFT JOIN company_dim ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst' AND 
    job_location = 'New York' AND 
    salary_year_avg IS NOT NULL
ORDER BY
    salary_year_avg DESC
LIMIT 10
``` 
#### **_A few things can be inferred from the data._**

- Position variance was high; positions were more specialized than just general data analysis. Titles included credit management analysis, fraud management analysis, and market research analysis.

- The top 10 highest earners' salaries ranged from $184K to $650K, showing that this industry can be quite lucrative.

- Large companies such as **CITI**, **GOPUFF** and **Nestle** can be seen in the data, showing a range of company size in the industry.


![Highest Pair Data Analyst Jobs Results](/Assets/Highest%20Paid%20Data%20Analyst%20Jobs%20NY.png) <br>
**_Bar graph visualizing the Highest Paid Data Analyst Positions In NY._**


### 2. Most Demanded Analyst Skills
Thie next query used **COUNT** to count the total number of times a given skill was desired in the dataset. I then filtered for data analyst jobs only with **WHERE** and grouped the skills together to get the total amount of 'skills'.

```SQL
SELECT  
    skills,
    COUNT(skills_job_dim.job_id) AS demand_count
FROM 
    job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst'
GROUP BY
    skills
ORDER BY
    demand_count DESC
limit 10
```
The following is a summary of the top skills:
- The demand for **SQL** skills can be found in **~** 94000 jobs.
- **Excel** is in 2nd place with nearly 70000 jobs.
- **Python** is in a close 3rd with about 57000 jobs.

![Top Demanded Data Analyst Skills](/Assets/Top%20Demanded%20Data%20Analyst%20Skills.png) <br>
**_Column chart visualizing the Top Demanded Data Analyst Skills_**

### 3. Highest Paying Analyst Skills

For the 3rd and final query, I took took the field 'salary_year_avg' and put it inside **AVG** (as avg_salary) to get the highest average salaries, filtering for data analyst with **WHERE** again. (_I used **ROUND** because I kept receiving MASSIVE decimals._)

```SQL
SELECT  
    skills,
    ROUND(AVG(salary_year_avg), 0) AS avg_salary

FROM 
    job_postings_fact
INNER JOIN skills_job_dim ON job_postings_fact.job_id = skills_job_dim.job_id
INNER JOIN skills_dim ON skills_job_dim.skill_id = skills_dim.skill_id
WHERE
    job_title_short = 'Data Analyst'
    AND salary_year_avg IS NOT NULL
GROUP BY
    skills
ORDER BY
    avg_salary DESC
limit 10
```
This dataset's results might not be what you expected. From this dataset, I can conclude two things:

- Skills like **SQL** and **Excel** dominate the data analytics world, particularly at the middle and lower levels, where they are essential for day-to-day tasks.

- At the higher and more specialized ends of the industry, different tools and skills are needed, reflecting the varied nature of advanced data analytics roles.


![Top Paid Data Analyst Skills](/Assets/Top%20Paying%20Data%20Analyst%20Skills.png) <br>
**_Column chart visualizing the Top Paying Data Analyst Skills_**
# What I learned
This was my first real attempt at querying, analyzing, and making inferences about data. I gained valuable experience within the SQL ecosystem, advancing my skills beyond the novice level. Through this project, I honed my querying abilities and learned to interpret and draw insights from data, strengthening my foundation in data analysis. 

# Conclusion
As a summary, the three datasets and queries I’ve analyzed have provided some valuable insights. It appears that focusing on the most in-demand skills in the field tends to be more beneficial for career growth than simply pursuing the highest-paying roles. The data clearly shows that while high-paying jobs are appealing, mastering the key skills that employers are actively seeking can lead to more sustainable success in the data analytics industry. Thank you for taking the time to read through my project. This experience has deepened my understanding of the industry, and I’m excited to continue developing my skills further.
