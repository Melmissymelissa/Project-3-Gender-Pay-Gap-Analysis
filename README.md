<div align="center"><h1>Gender Pay Gap Analysis</h1> </div>
<a href="https://docs.google.com/presentation/d/1_Thn54EwRnlzzFEDCwwoVP457aCFs848OM8gyH6Yu7o/edit?usp=drive_link">Link to presenation</a>
<a href="https://colab.research.google.com/drive/13HoOmvjNymPu7l6T0bQdarvTgRvnHSP_?usp=drive_link">Link to Colab</a>

<!-- TABLE OF CONTENTS -->
   ## Table of Contents
   - [Introduction](#introduction)
   - [Data](#data)
   - [Installation](#installation)
   - [EDA](#EDA)
   - [Analysis](#analysis)
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

## Data
<div align="left"><h3>About the Dataset</h3> </div>
<p></p>
This dataset from 2021 from the US Department of Labor is the most recent dataset that offers valuable insights for researchers and stakeholders, shedding light on the intricate workings of the gender pay gap and revealing the underlying factors that perpetuate these disparities. From scrutinizing wage discrepancies to unraveling the prevalence of occupational segregation, this data is a vital resource in the relentless pursuit of gender equality in the workforce. <a href="https://www.dol.gov/agencies/wb/data/occupations">Link to dataset</a>
<p></p>
<p>This dataset contains <u>337 rows</u> and <u>9 main columns</u></p>
Main Columns Include:
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
- Running Descriptive Statistics 
```python
gender_pay_df.describe().round() # see the descriptive statistics
 ```
![image2](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/a5a89e0b-dde4-4a7e-ad8b-dbeda5d27efb)

## EDA
EDA involved exploring the data to answer these questions:
- What are the top 10 Jobs with the highest gender pay gap?
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

- What are the top 10 Jobs with the lowest gender pay gap?
```python
plt.figure(figsize=(12, 6))
plt.bar(below_10_occupations['Occupation'], below_10_occupations['gender_pay_gap'], color='#5F758E')
plt.title('Top 10 Occupations with Lowest Gender Pay Gap', fontsize=16)
plt.xlabel('Occupation', fontsize=12)
plt.ylabel('Gender Pay Gap', fontsize=12)
plt.xticks(rotation=45, ha='right', fontsize=10)
plt.yticks(fontsize=10)
plt.grid(axis='y', linestyle='--')
plt.legend(['Gender Pay Gap'], loc='upper right', fontsize=10)

for i, value in enumerate(below_10_occupations['gender_pay_gap']):
    plt.text(i, value, f'{value:.2f}', ha='center', va='bottom', fontsize=8)


plt.tight_layout()  # Ensures labels are not cut off
plt.show()
 ```
![image3](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/082b9523-5ff1-4a16-a61f-b2ca728e768a)
- What is the the distribution of the percentage of women in occupational groups?
```python
ax = sns.histplot(gender_pay_df['Percentage of women in occupational group'], bins=16, color='#5F758E')
 ```
![image4](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/244d8390-4ba5-4a1b-90c5-83abee9b8c8e)

- How does the percentage of women in occupational groups relate to the earnings of women compared to men?
```python
sns.scatterplot(x="Women's earnings as a percentage of men's earnings", y="Percentage of women in occupational group", data=gender_pay_df)
```
![image5](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/9e23f05c-ce98-494a-a68c-529163847f1e)

- How does the distribution of median earnings for men vary across different occupations?
```python
plt.figure(figsize=(10, 6))
sns.boxplot(x='Median earnings men', data=gender_pay_df)
plt.xlabel('Median earnings men')
plt.ylabel('Y-axis Label')
plt.title('Distribution of median earnings for men vary across different occupations')
plt.show()
```
![image6](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/8d6a8e5f-f3bb-474b-9f71-a74eb98cab31)
- How does the distribution of median earnings for women vary across different occupations?
```python
plt.figure(figsize=(10, 6))
sns.boxplot(x='Median earnings women', data=gender_pay_df, color = '#EBACA4')
plt.xlabel('Median earnings women')
plt.title('Distribution of median earnings for women vary across different occupations')
plt.show()
```
![image7](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/d2fa3d70-6f5d-4225-b9e9-cc7bef39e60e)

## Analysis
<div align="center"><h2>Hypotheses</h2> </div>
<h3>1. As the percentage of women in an occupational group increases, the median earnings of women in that group tend to decrease.</h3>

```python
stats.pearsonr(gender_pay_df["Median earnings women"], gender_pay_df["Percentage of women in occupational group"])
```
![image8](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/583f3737-fee7-405d-aa48-64c3bdfeceea)
```python
sns.scatterplot(x="Percentage of women in occupational group", y="Median earnings women", data=gender_pay_df)
plt.title("Relationship between Percentage of Women in an Occupation and Women's Median Earnings")
```
Based on these results, I can conclude that there is a weak negative correlation; when the percentage of women in a job group goes up, the median earnings of women tend to go down a little bit. Although the relationship is not very strong, the statistical significance of the correlation indicates that this relationship is unlikely to have occurred by chance.
![image9](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/933e1387-1817-43e2-b184-8ec61b6f9919)


<h3> 2.As the percentage of women in an occupational group increases, the gender pay gap tends to be larger.</h3>

```python
stats.pearsonr(gender_pay_df["Percentage of women in occupational group"], gender_pay_df["gender_pay_gap"])
```
![image10](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/593e633a-65ee-427e-8d9d-6c050600b9b8)

With, 95% cofidence, the correlation coefficient is positive (0.165), suggesting a positive correlation between the variables. This means that as the percentage of women in a job group increases, the gender pay gap tends to be larger.
![image11](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/18468166-2bd8-47a7-844f-cf9f548f429c)


<h3> 3. The gender pay gap significantly differs between occupations with below-average proportions of women compared to men, and occupations with above-average proportions of women compared to men</h3>

```python
# Spliting the data for a t-test into 2 samples
above_df = gender_pay_df.loc[gender_pay_df['Percentage of women in occupational group'] > 48] #sample of above average Percentage of Women
below_df = gender_pay_df.loc[(gender_pay_df['Percentage of women in occupational group'] < 48)]#sample of below average Percentage of Women
```
```python
# run two sample t-test
t_test = stats.ttest_ind(above_df["gender_pay_gap"], below_df["gender_pay_gap"])
print(t_test)
```
![image13](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/ce7b2074-2b6a-4472-996b-72276f3ddf68)
```python
#confidence interval range for the difference in means
sample_1_n = above_df.shape[0]
sample_2_n = below_df.shape[0]
sample_1_mean = above_df['gender_pay_gap'].mean()
sample_2_mean = below_df['gender_pay_gap'].mean()
sample_1_var = above_df['gender_pay_gap'].var()
sample_2_var = below_df['gender_pay_gap'].var()
#print(sample_1_mean)
#print(sample_2_mean)
std_err_difference = math.sqrt((sample_1_var/sample_1_n)+(sample_2_var/sample_2_n))

mean_difference = sample_2_mean - sample_1_mean

margin_of_error = 1.96 * std_err_difference
ci_lower = mean_difference - margin_of_error
ci_upper = mean_difference + margin_of_error

print("The difference in means at the 95% confidence interval is between "+str(ci_lower)+" and "+str(ci_upper)+".")
```
![image15](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/4fe6a1d0-dd4e-4e10-8881-3e3ff18b4abe)

With 95% confidence, the confidence interval (CI) suggests that the gender pay gap in occupations where the proportion of women is below average is approximately $64 to $4,000 more compared to occupations where the proportion of women is above average.

It suggests that factors such as occupational segregation and unequal representation of women in certain fields contribute to the wider pay gap. These findings highlight the importance of addressing gender disparities in occupational distribution and promoting equal opportunities for women in all professions.

![image16](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/763b4617-62a5-4321-81ef-b7c67f3b3b31)

<h3> 4. The gender pay gap significantly differs between occupations with below-average proportions of women compared to men, and occupations with above-average proportions of women compared to men</h3>

```python
# run two sample t-test
t_test = stats.ttest_ind(above_df["Median earnings"], below_df["Median earnings"])
print(t_test)
```
```python
#confidence interval range for the difference in means
sample_3_n = below_df.shape[0]
sample_4_n = above_df.shape[0]
sample_3_mean = below_df['Median earnings'].mean()
sample_4_mean = above_df['Median earnings'].mean()
sample_3_var = below_df['Median earnings'].var()
sample_4_var = above_df['Median earnings'].var()
std_err_difference = math.sqrt((sample_3_var/sample_3_n)+(sample_4_var/sample_4_n))

mean_difference = sample_4_mean - sample_3_mean

margin_of_error = 1.96 * std_err_difference
ci_lower = mean_difference - margin_of_error
ci_upper = mean_difference + margin_of_error

print("The difference in means at the 95% confidence interval is between "+str(ci_lower)+" and "+str(ci_upper)+".")
```

![image17](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/7afe5377-1f78-4e85-b2fb-5943d36120f5)
![image18](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/7d09a0e1-2ced-4d97-987e-c2d1bbd13f50)

With 95% confidence, there is a significant difference in median earnings between occupations with below-average percentages of women and occupations with above-average percentages of women in the occupational group. The confidence interval (CI) suggests that the median earnings in occupations with above-average percentages of women are approximately $4,300 to $15,000 less compared to occupations with below-average percentages of women.

The difference in earnings between jobs based on the percentage of men and women reveals societal expectations and biases regarding suitable occupations for each gender. These biases influence job choices and can lead to occupational segregation, where certain jobs are predominantly held by either men or women. Unfortunately, this segregation also contributes to a gender pay gap, with jobs considered more "for women" often paying less than those considered more "for men." This significant difference in earnings highlights the influence of societal biases on work and pay. It is crucial to challenge and change these biases to ensure equal opportunities and fair treatment for everyone in their careers.

![image19](https://github.com/Melmissymelissa/Project-3-Gender-Pay-Gap-Analysis/assets/142250108/b8722a43-1c73-4948-83cd-6296602df05a)
