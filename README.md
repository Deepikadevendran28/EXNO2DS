# EXNO2DS
# AIM:
      To perform Exploratory Data Analysis on the given data set.
      
# EXPLANATION:
  The primary aim with exploratory analysis is to examine the data for distribution, outliers and anomalies to direct specific testing of your hypothesis.
  
# ALGORITHM:
STEP 1: Import the required packages to perform Data Cleansing,Removing Outliers and Exploratory Data Analysis.

STEP 2: Replace the null value using any one of the method from mode,median and mean based on the dataset available.

STEP 3: Use boxplot method to analyze the outliers of the given dataset.

STEP 4: Remove the outliers using Inter Quantile Range method.

STEP 5: Use Countplot method to analyze in a graphical method for categorical data.

STEP 6: Use displot method to represent the univariate distribution of data.

STEP 7: Use cross tabulation method to quantitatively analyze the relationship between multiple variables.

STEP 8: Use heatmap method of representation to show relationships between two variables, one plotted on each axis.

## CODING AND OUTPUT
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

# For local environments, prompt the user to enter the path to the CSV file
file_path = input("Enter the path to your CSV file: ")
dt = pd.read_csv(file_path)

dt
dt.info()
print(f"Number of rows: {dt.shape[0]}")
print(f"Number of columns: {dt.shape[1]}")
dt.set_index('PassengerId', inplace=True)
dt.head()
dt.describe()
categorical_cols = dt.select_dtypes(include=['object', 'category']).columns
for col in categorical_cols:
    print(f"Value counts for '{col}':")
    print(dt[col].value_counts())
    print("\n")
    sns.countplot(x='Survived', data=dt)
plt.title('Univariate Analysis of Survived')
plt.xlabel('Survived')
plt.ylabel('Count')
plt.show()
unique_pclass = dt['Pclass'].unique()
print("Unique values in 'Pclass' column:", unique_pclass)
dt.rename(columns = {'Sex':'Gender'}, inplace = True)
dt
sns.catplot(x='Gender', hue='Survived', data=dt, kind='count', height=5, aspect=1.2)
plt.title('Survival Count by Gender')
plt.show()
fig, ax1 = plt.subplots(figsize=(8,5))
graph = sns.countplot(data=dt, x='Gender', ax=ax1) #USE THE NECESSARY PARAMETERS HERE
graph.set_xticklabels(graph.get_xticklabels())
for p in graph.patches:
    height = p.get_height()
    graph.text(p.get_x()+p.get_width()/2, height + 20.8,height ,ha="left")
plt.show()

# USE BOXPLOT METHOD TO ANALYZE AGE AND SURVIVED COLUMN
sns.boxplot(x='Survived', y='Age', data=dt)
plt.title('Boxplot of Age by Survival Status')
plt.show()

"""**MULTIVARIATE ANALYSIS**"""

# USE BOXPLOT METHOD AND ANALYZE THREE COLUMNS(PCLASS,AGE,GENDER)
plt.figure(figsize=(10,6))
sns.boxplot(x='Pclass', y='Age', hue='Gender', data=dt)
plt.title('Boxplot of Age by Pclass and Gender')
plt.show()


# USE CATPLOT METHOD AND ANALYZE THREE COLUMNS(PCLASS,SURVIVED,GENDER)
sns.catplot(x='Pclass', hue='Survived', col='Gender', data=dt, kind='count', height=5, aspect=1)
plt.subplots_adjust(top=0.85)
plt.suptitle('Survival Count by Pclass and Gender')
plt.show()

# IMPLEMENT HEATMAP AND PAIRPLOT FOR THE DATASET
# Heatmap for correlation matrix
plt.figure(figsize=(10, 6))
sns.heatmap(dt.corr(numeric_only=True), annot=True, cmap='coolwarm')
plt.title('Correlation Heatmap')
plt.show()

# Pairplot for the dataset
sns.pairplot(dt, hue='Survived', diag_kind='kde')
plt.suptitle('Pairplot of Dataset', y=1.02)
plt.show()



<img width="582" height="682" alt="Screenshot 2025-10-16 103241" src="https://github.com/user-attachments/assets/4c3dd97d-dda0-4117-886b-f50eb13fa5da" />
<img width="344" height="666" alt="Screenshot 2025-10-16 103255" src="https://github.com/user-attachments/assets/fb5b880b-da92-4f3f-90f2-5f4859d861c3" />
<img width="441" height="767" alt="Screenshot 2025-10-16 103430" src="https://github.com/user-attachments/assets/ddce7882-9d81-44a3-b203-1a7000a85d37" />
<img width="467" height="767" alt="Screenshot 2025-10-16 103440" src="https://github.com/user-attachments/assets/655a0506-fdc8-4a72-afbe-78c2e42128fd" />


# RESULT
The program is executed successfully.
