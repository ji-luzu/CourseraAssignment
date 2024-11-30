# CourseraAssignment

I have no idea if this wooooorks
Let's hope this is right
Looook that's my code :)

boston_df.head()
boston_df.info()
boston_df.describe()
boston_df.isnull().sum()

import seaborn as sns
import matplotlib.pyplot as plt

sns.boxplot(y=boston_df['MEDV'])
plt.title("Boxplot of Median Value of Owner-Occupied Homes")
plt.ylabel("MEDV ($1000's)")
plt.show()

chas_counts = boston_df['CHAS'].value_counts()
chas_counts.plot(kind='bar', color=['blue', 'orange'])
plt.title("Number of Houses Bounded by the Charles River")
plt.xlabel("CHAS (0 = Not Bounded, 1 = Bounded)")
plt.ylabel("Count")
plt.show()

boston_df['AGE_group'] = pd.cut(boston_df['AGE'], bins=[0, 35, 70, 100], labels=['<=35', '35-70', '>70'])

sns.boxplot(x='AGE_group', y='MEDV', data=boston_df)
plt.title("Median Value of Homes by Age Group")
plt.xlabel("Age Group of Houses")
plt.ylabel("MEDV ($1000's)")
plt.show()

sns.scatterplot(x='INDUS', y='NOX', data=boston_df)
plt.title("Relationship Between NOX and INDUS")
plt.xlabel("Proportion of Non-Retail Business Acres (INDUS)")
plt.ylabel("Nitric Oxide Concentration (NOX)")
plt.show()

boston_df['PTRATIO'].plot(kind='hist', bins=10, edgecolor='black')
plt.title("Distribution of Pupil-Teacher Ratio")
plt.xlabel("Pupil-Teacher Ratio")
plt.ylabel("Frequency")
plt.show()

from scipy.stats import ttest_ind

chas_0 = boston_df[boston_df['CHAS'] == 0]['MEDV']
chas_1 = boston_df[boston_df['CHAS'] == 1]['MEDV']

t_stat, p_value = ttest_ind(chas_0, chas_1)
print("T-Statistic:", t_stat, "P-Value:", p_value)

from scipy.stats import f_oneway

age_group1 = boston_df[boston_df['AGE_group'] == '<=35']['MEDV']
age_group2 = boston_df[boston_df['AGE_group'] == '35-70']['MEDV']
age_group3 = boston_df[boston_df['AGE_group'] == '>70']['MEDV']

f_stat, p_value = f_oneway(age_group1, age_group2, age_group3)
print("F-Statistic:", f_stat, "P-Value:", p_value)

from scipy.stats import pearsonr

corr, p_value = pearsonr(boston_df['NOX'], boston_df['INDUS'])
print("Correlation Coefficient:", corr, "P-Value:", p_value)

from sklearn.linear_model import LinearRegression

X = boston_df[['DIS']]
y = boston_df['MEDV']

model = LinearRegression().fit(X, y)
print("Coefficient (Impact of DIS):", model.coef_[0], "Intercept:", model.intercept_)
