<div align="center"><h1>Gender Pay Gap Analysis</h1> </div>
<a href="https://docs.google.com/presentation/d/1_Thn54EwRnlzzFEDCwwoVP457aCFs848OM8gyH6Yu7o/edit?usp=drive_link">Link to presenation</a>
<a href="https://colab.research.google.com/drive/13HoOmvjNymPu7l6T0bQdarvTgRvnHSP_?usp=drive_link">Link to Colab</a>

<!-- TABLE OF CONTENTS -->
   ## Table of Contents
   - [Introduction](#introduction)
   - [Data Source](#datasource)
   - [Installation](#installation)
   - [EDA](#EDA)
   - 
## Introduction
<p>In my project, I dive deep into the realm of statistical analysis to investigate and shed light on the factors contributing to occupational segregation and its impact on pay disparities between genders. 💼🔍</p>
<p></p>
<p>With using the Employment and Earning by Occupation dataset from the US Department of Labor, I uncover valuable insights that will help us understand the root causes of this societal issue. By examining industries and occupations, we can work towards creating a fairer and more equitable future for all. 💪🌟</p>
</body>
<h3>Understand</h3>
<p></p>
<p>1. The factors that contributeAnalyze the data behind the gender pay gap and occupational segregation</p>
<p>2. Analyze the data behind the gender pay gap and occupational segregation</p>
</body>
<h3>Want To Know</h3>
<p></p>
<p>1. Which industries or occupations have the biggest gender disparities in employment and earnings?</p>
<p>2. How does the gender pay gap differ across occupational groups and industries?</p>
<p>3. Why are certain industries or occupations dominated by one gender?</p>
<p>4. Do men and women tend to earn different amounts in various job types?</p>
</body>

## Data Source
<div align="center"><h2>About the Dataset</h2> </div>
<p></p>
This dataset from 2021 from the US Department of Labor is the most recent dataset that offers valuable insights for researchers and stakeholders, shedding light on the intricate workings of the gender pay gap and revealing the underlying factors that perpetuate these disparities. From scrutinizing wage discrepancies to unraveling the prevalence of occupational segregation, this data is a vital resource in the relentless pursuit of gender equality in the workforce. <a href="https://www.dol.gov/agencies/wb/data/occupations">Link to dataset</a>
<p></p>
<p>This dataset contains <u>337 rows</u> and <u>9 main columns</u></p>
<h3>Main Columns Include:</h3>
<p></p>
<p>1. Occupation: This column categorizes various job roles or positions within the dataset, providing a comprehensive breakdown of different occupations. It allows for easy identification and analysis of specific job roles and their associated data.</p>
<p>2. Number of Full-Time Workers: This column provides information on the total count of individuals employed in each occupation on a full-time basis. It offers insights into the scale and workforce size within different job roles, allowing for comparisons and analysis of employment trends.</p>
<p>3. Number of Men: This column indicates the count of male individuals employed in each occupation. It provides a quantitative measure of gender distribution within different job roles, enabling analysis of gender imbalances and disparities in workforce representation.</p>
<p>4. Number of Women: This column represents the count of female individuals employed in each occupation. It offers insights into the gender distribution within different job roles, allowing for analysis of gender representation and potential disparities in workforce composition.</p>
<p>5. Percentage of Women in Occupational Group: This column calculates the proportion of female individuals within each specific job category. It provides a quantitative measure of gender representation, allowing for analysis of gender diversity and potential gender imbalances within different occupational groups.</p>
<p>6. Median Earnings: This column represents the median income for individuals in each occupation, providing insights into the overall earning potential within different job roles.</p>
<p>7. Median Earnings Men: This column specifically focuses on the median earnings for men</p>
<p>8. Median Earnings Women: This column specifically focuses on the median earnings for women , respectively, allowing for a direct comparison of gender-based wage disparities.</p>
<p>9. Women's Earnings as a Percentage of Men's Earnings: This column provides a crucial metric for understanding the gender pay gap within each occupation. It quantifies the difference in earnings between men and women, expressed as a percentage, highlighting the extent of gender-based wage inequality.</p>
</body>

## Installation
- Import and Alias Modules
```python
# import & alias modules
import math
import pandas as pd
from scipy import stats
import seaborn as sns
import matplotlib.pyplot as plt
import plotly.express as px
from google.colab import drive
drive.mount('/content/gdrive')
sns.set()
pd.set_option('display.max_colwidth', None)
 ```
- Bring in the Dataset
```python
#read in data
gender_pay_df = pd.read_csv("/content/gdrive/MyDrive/Thinkful /Capstone 3/Book3.csv")
gender_pay_df.info() # see the information for our dataframe
 ```
## EDA
EDA involved exploring the data to answer these questions:
- Top 10 Jobs with the highest gender pay gap
```python
top_10_occupations = gender_pay_df.sort_values('gender_pay_gap', ascending=True).head(10)
# Plotting the top 10 occupations with the largest gender pay gap
plt.figure(figsize=(12, 6))
plt.bar(top_10_occupations['Occupation'], top_10_occupations['gender_pay_gap'], color='#CD9C8B')
plt.title('Top 10 Occupations with Largest Gender Pay Gap', fontsize=16)
plt.xlabel('Occupation', fontsize=12)
plt.ylabel('Gender Pay Gap', fontsize=12)
plt.xticks(rotation=45, ha='right', fontsize=10)
plt.yticks(fontsize=10)
plt.grid(axis='y', linestyle='--')
plt.legend(['Gender Pay Gap'], loc='upper right', fontsize=10)

# Adding data labels outside the bars and changing color if negative
for i, value in enumerate(top_10_occupations['gender_pay_gap']):
    color = 'red' if value < 0 else 'black'
    plt.text(i, value, f'{value:.2f}', ha='center', va='bottom', fontsize=8, rotation=90, color=color, fontweight='bold')
plt.tight_layout()  # Ensures labels are not cut off
plt.show()
 ```

![image1](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/417b24ac-9f6e-4354-a5e3-6924149891ab)

Running Descriptive Statistics 
```python
gender_pay_df.describe().round() # see the descriptive statistics
 ```
<div align="center"><h2>Hypotheses</h2> </div>
<p></p>
<p>1. The proportion of women in an occupational group is positively correlated with the ratio of women's earnings to men's earnings within that group.</p>
<p>2. There is a notable disparity in the gender pay gap between occupations with below-average proportions of women compared to those with above-average proportions of women in the occupational group.</p>
<p>3. There is a substantial disparity in gender-based occupational segregation within industries or occupations that have lower median earnings.</p>
<div align="center"><h2>Results</h2> </div>
<h3>Hypothesis Analysis 1: </h3>
<p>The correlation coefficient is positive (0.2156), suggesting a weak positive correlation between the variables: "Percentage of women in occupational group" and "Women's Earnings as a percentage of men's earnings" </p>
<p></p>
<p>However, it is important to note that the correlation is relatively weak, as the value is closer to zero than to 1. Therefore, while there is a positive relationship between the variables, it is not very strong.</p>
<h3>Hypothesis Analysis 2: </h3>
<p>The p-value, less than 0.005, shows that the difference in gender pay gap between these two types of occupations is not due to chance</p>
<p>With 95% confidence, the gender pay gap is estimated to be approximately $64-$4,000 higher in occupations with fewer women compared to men.</p>
<h3>Hypothesis Analysis 3: </h3>
<p>TThe p-value is less than 0.005, shows a significant difference in median earnings between occupations with below average and above average proportions of women.</p>
<p>Median earnings are approximately $4,300-$15,000 higher with 95% confidence in occupations where women are below average</p>
