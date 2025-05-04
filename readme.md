# The Analysis
## 1. What are the most demanding skills for top 3 data roles
## to find the most demanded skills for the top three most popular data roles, I filtered those positions by popularity and identified the top five skills for each of these roles. This query highlights the most popular job titles and their top skills, showing which skills I should pay attention to depending on the role I am targeting. 

## view my notebook here.
[2_skill_demand.ipynb](EDA project\2_skill_demand.ipynb)

## visualize data
''' Python

fig,ax=plt.subplots(len(job_titles),1)
sns.set_theme(style='ticks')   ## useful to make visuals more eyes appealing
for i ,job_title in enumerate(job_titles):
    df_plot=df_skills_perc[df_skills_perc['job_title_short']==job_title].head(5)
    df_plot.plot(kind='barh',x='job_skills',y='skill_perc',ax=ax[i],title=job_title)
    sns.barplot(data=df_plot,x='skill_perc',y='job_skills',ax=ax[i],hue='skill_count',palette='light:r') 
    ax[i].set_ylabel('')
    ax[i].set_xlim(0,75)
    ax[i].legend().set_visible(False)
    for n,v in enumerate(df_plot['skill_perc']):
        ax[i].text(v+2,n-0.1,f'{v:.0f}%',va='center',fontsize=8)
    if i!=len('job_titles')-1:
        ax[i].set_xticks([])    
fig.suptitle('count of top skills for data jobs in india',fontsize=16)
fig.tight_layout(h_pad=0.8)

'''
### results
![alt text](image.png)

### Insights 💡
-SQL is a versatile skill, highly demanded across all three roles, but most prominently for data  engineers (63%) and data analysts (49%). 

-Python is the most requested skill for data scientists and data engineers, appearing in over half the job postings for both roles.

-For data analysts, SQL is the most sought-after skill, appearing in 49% of job postings. Data analysts require more technical skills like excel, tableau, power bi.

-data engineers required cloud based skills like AWS, Azure, and Spark compared to data analysts and data scientists


# The Analysis
## 2. How are in-demand skills trending for Data Analysts
### Visualize data

''' python

from matplotlib.ticker import PercentFormatter
df_plot=df_da_india_percent.iloc[:,:5]
sns.lineplot(data=df_plot,dashes=False,legend=False,palette='dark:g')
ax=plt.gca()  
ax.yaxis.set_major_formatter(PercentFormatter())
plt.tight_layout()  
plt.show()

### Result
![alt text](image-1.png)

### 📌 Top-Level Insights:
SQL is consistently the most in-demand skill, maintaining demand levels above 50% throughout the year, peaking around May and again in December.

Python holds the second position in most months, showing relatively stable demand in the 35–45% range, with minor fluctuations.

Excel, Tableau, and Power BI are the next tier of skills, with Excel slightly ahead overall, though all three show similar trends and occasional crossovers in demand.


# The Analysis
## 3. How well do jobs and skills pay for A Data Analyst ?

### salary analysis for Data Nerds
### Visualize Data
''' python    
from matplotlib.axis import XAxis
sns.boxenplot(data=df_india_top6,x='salary_year_avg',y='job_title_short',order=job_order)
sns.set_theme(style='ticks')
plt.title('Salary distribution in India')
plt.xlabel('yearly salary in USD $')
plt.ylabel('')
ticks_x=plt.FuncFormatter(lambda y,pos:f'${int(y/100)}k')
plt.gca().xaxis.set_major_formatter(ticks_x)
plt.show()     
'''
### Results
![alt text](image-2.png)
#### Box Plot visualizing the salary distributions for top 6 data jobs in India

### 
📈 Key Insights:   

-Senior roles earn substantially more than junior ones, with clear salary gaps.

-Data Scientist and Senior Data Scientist roles offer the most consistent and high salaries, making them financially attractive career paths.

-Engineering roles (Data Engineer, Senior Data Engineer) show slightly more spread, possibly due to differing industry/tech stacks.

-Outliers in junior roles (Data Analyst) may indicate promotions, misclassified roles, or international compensation.

# The Analysis
## 4. Which skills are most demanding and which are most paying for a Data Analyst in India
### Visualize Data

''' python
Limit to top 10    
top10_pay = df_da_top_pay.head(10)      
top10_demand = df_da_skills.head(10)
sns.set_theme(style='ticks')
fig, ax = plt.subplots(nrows=1, ncols=2, figsize=(16, 6))

sns.barplot(data=top10_pay, x='median', y=top10_pay.index, ax=ax[0], hue='median', palette='dark:b')    
ax[0].set_title('Top 10 Highest Paying Skills For Data Analyst in India')   
ax[0].set_ylabel('')    
sns.barplot(data=top10_demand, x='median', y=top10_demand.index, ax=ax[1], hue='median', palette='light:g')   
ax[1].set_title('Top 10 Demanding Skills for Data Analyst in India')  
ax[1].set_ylabel('')

### Result
![alt text](image-3.png)

🔎 Key Observations:   
-Big Data & Cloud-related tools like PySpark, MongoDB, and Data Lake offer very high salaries.

-Even tools like Confluence (a collaboration platform) and API integration skills are highly valued.

-Visualization tools such as Power BI also make the list, emphasizing the value of storytelling with data   

-The most demanded skills include foundational tools like SQL, Excel, Tableau, and Power BI.

-Soft skills like communication, teamwork, and attention to detail are crucial—companies highly value well-rounded candidates.

# The Analysis
## 5. What is the most optimal skill to learn for a data Analyst 
### Visualize data

''' python    
from adjustText import adjust_text    
from matplotlib.patches import ArrowStyle   
from matplotlib.pyplot import gca

sns.scatterplot(
data=df_plot,
x='skills_percent',
y='median_salary',
hue='technology'
)   
sns.despine()  
plt.show()
### result
![alt text](image-4.png)

## 💡 Key Insights:
1. High Salary, Low Prevalence Tools:
Looker, PowerPoint, Power BI and Tableau (Analyst Tools & Libraries) offer high salaries (~$110k) despite low usage (<25%).

These are specialized tools that, though less common, are highly valued in organizations that use them.

2. Widely Used, Moderate Salary Tools:
SQL (48%), Excel (42%), and Python (40%) are the most commonly required skills, offering salaries around $950k to $980k.

These are considered foundational skills for Data Analysts, often expected across the board.

3. Cloud Tools Offer Moderate Pay and Usage:
Azure and AWS show moderate usage (~15%) and salaries around $940k and $800k, respectively.

Shows cloud tools are valuable but not yet widespread in traditional data analyst roles.

4. Low Salary, Low Usage Tools:
Word and Oracle show low relevance both in salary and skill percent—indicating they are less optimal for aspiring data analysts.

5. Programming vs. Analyst Tools:
Programming skills like Python and SQL are essential but don’t yield the highest salaries alone.

Analyst tools like Power BI and Tableau tend to bring higher pay despite being less commonly used, suggesting a niche value.