# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To find the most demanded skills for the top 3 most popular data roles. I filetered out these positions by which one were the most popular, and got the top 5 skills for these top 3 roles. This query highlights the most popular jobs titles and their top skills showing which skills I should pay attention to depending on the role I'm targeting.

View my notebook with detailed steps here: [2_Skill_Demand.ipynb](3_Project\2_Skills_Count.ipynb)

### Visualize Data

```python
fig,ax=plt.subplots(len(job_titles),1)

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_prec[df_skills_perc['job_title_short'] == job_title ].head(5)[::-1]
    sns.barplot(data=df_plot, x='skill_percent',y='job_skills',ax=ax[i], hue='skill_count', palette='dark:b_r' )

plt.show()
```

### Results
![Visualization of Top Skills for Data Nerds](3_Project\images\skill_demand_all_data.png)

### Insights

- Python is a versatile skill. highly demanded across all three roles, but most prominently for Data Scientists (72%)  and Data Engineers (65%).
- SQL is the most requested skill for Data Analysts and Data Scientists, with it in over half job postings for both roles. For Data Engineers, python is the most sought-after skill, appearing in 68% of job postings.
- Data Engineers require more specialized technical skills (AWS, Azure, Spark) compared to Data Analysts and Data Scientists who are expected to be proficient in more general data management and analysis tools (Excel, Tableau).

## 2. How are in-demand skills trending for Data Analysts?

### Visualization

```python
from matplotlib.ticker import PercentFormatter

df_plot = df_da_us_perc.iloc[:, :5]
sns.lineplot(data = df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()


plt.title('Trending Top Skills for Data Analyst in the US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()

ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

for i in range(5):
    plt.text(11.2,df_plot.iloc[-1, i], df_plot.columns[i])
```
![Trending Top skills for Data Analysts in the US](3_Project\images\skill_trend.png)
*Bar graph visualizing the trending top skills for data anlaysts in the US in 2023.*

### Insights:
- SQL remains the most consistently demanded skill throughout the year, although it shows a gradual decrease in demand.
- Excel experienced a significant increase in demand starting around September, surpassing both Python and Tableau by the end the year.
- Both Python and Tableau show relatively stable demand throughout the eyar with some fluctuations but remain essential skills for data analysts. Power BI, while less demanded compared to the others, show a slight upward trend towards the year's end.

## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Nerds

#### Visualize Data

```python
sns.boxplot(data = df_us_top6, x='salary_year_avg', y='job_title_short', order=job_order)
sns.set_theme(style='ticks')

# this is all the same
plt.title('Salary Distributions in United States')
plt.xlabel('Yearly Salary ($USD)')
plt.ylabel('')
plt.xlim(0,600000)
ticks_x = plt.FuncFormatter(lambda y,pos: f'{int(y/1000)}K')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()
```

#### Results
![Salary Distributions of Data Jobs in the US](3_Project\images\Salary_analysis.png)

*Box plot visualizing the salary distribution for the top 6 data job titles*

### Insights

- There is a significant variation in the salary ranges across different job titles. Senior Data Scientist positions tend to have the highest salary potential, with up to $600K, indicating the high value placed on advanced data skills and experience in the industry.

- Senior Data Engineer and Senior Data Scientist roles show a considerable number of outliers on the high end of the salary spectrum, suggesting that exceptional skill or circumstances can lean to high pay in these roles. In contrast, Data Analyst roles demonstrate more consistency in salary, with fewer outliers.

- The median salaries increases with the seniority and speicalization fo the roles. Senior rles(Senior Data Scientist, Senior Data Engineer) not only have the larger differences in typical salaries, reflecting greater variance in compensation as reponsibilities increase.

## 3. How well do jobs and skills pay for Data
### Highest Paid & Most Demanded Skills for Data
#### Visualize data

```python
fig,ax = plt.subplots(2,1)

sns.set_theme(style='ticks')
# Top 10 highest paid skills for data analyst
sns.barplot(data=df_da_top_pay, x='median', y=df_da_top_pay.index, ax=ax[0], hue='median', palette='dark:b_r', legend=False)
ax[0].set_title('Top 10 Highest Paid skills for data analysts')
ax[0].set_ylabel('')
ax[0].set_xlabel('')
ax[0].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,_ : f'{int(x/1000)}K'))

# top 10 mist in-demand skills for data analyst
sns.barplot(data=df_da_skills, x='median', y=df_da_skills.index, ax=ax[1], hue='median', palette='light:b', legend=False)
ax[1].set_xlim(ax[0].get_xlim())
ax[1].set_title('Top 10 Most In-Demand Skills for Data Analyst')
ax[1].set_ylabel('')
ax[1].set_xlabel('Median Salary ($USD)')
ax[1].xaxis.set_major_formatter(plt.FuncFormatter(lambda x,_ : f'{int(x/1000)}K'))

fig.tight_layout()
```

![The Highest Paid & Most In-Demand Skills for Data Analyst in the US](3_Project\images\Highest_Paid_In_Demand_Skills.png)
*Two seperate bar graphs visualizing the highest paid skills and most in-demand skills for data analysis in the US*

## Insights

- The top graph shows specialized technical skills like `dplyr`, `Bitbucket`, and `Gitlab` are associated with higher salaries, some reaching up to $200K, suggesting that advanded technical proficiency can increse earning potential. 

- The bottom graph highlights that foundatioal skills like `Excle`, `Power Point`, and `SQL` are the most in-demand, even though they may not offer the highest salaries. This demonstrates the importance fo these core skills for employability in data anlaysis roles.

- There's a clean distinction between the skills that are highest paid andthese that are the most in-demand. Data analysts aiming to amximize their career potential should consider developing a diverse skill set hat includes both high-paying specialized skills and widely demanded foundational skills.

## 4. What is the most optimal skill to lean for 

#### Results

![Most Optimal Skills for Data Analysts in the US]
(3_Project\images\Optimal_skills_for_Data_analyst.png)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysts in the US.*

#### Insights:
- The Scatter pot shows that most of the `programming` skills (colored blue) tend to cluster at higher slalary levels compared to other categories, indicating that programing expertise might offer greater salary beneits within the data analytics field.

- Analyst tools (colored green), including Tableau and Power BI, are prevalent in job postings and offer competitive salariesm showing that visalization and data analysts software crucial for current data roles. This category not only has good salaries but is also versatile across different types fo data tasks.

- The database skills (colored orange), such as Oracle and SQL Server, are associated with some of the highest salaries among data analyst tools. This indicates a significant demand and valuation for data amangement and manipulation expertise in the industry.