# Sales-Analysis-Dashboard 
# Problem Statement –
Develop a basic understanding of risk analytics in banking and financial services and understand how data is used to minimise the risk of losing money while lending to customers.
# Solution – 
With our dashboards which are created using Power BI latest tools helps the company to make a decision based on the applicant’s profile like if the applicant is likely to repay the loan then approving the loan otherwise not.
# About Dataset – 
This dataset basically contains information about bank details ,various client details which consists of multiple tables which are interlinked with each other through keys like primary key and foreign key.
The various tables are Banking Relationship, Client-Banking, Gender, Investment Advisor and Period.
# Data Cleaning –
Codes used in python 
Importing all the liabraries
import mysql.connector    -- to connect python withmysql
import seaborn as sns     
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
from sqlalchemy import create_engine  -- to visualise graphs
# MySQL connection parameters
username = "root"
password = "root"
host = "localhost"
database = "banking_case"
# Create SQLAlchemy engine
engine = create_engine(f"mysql+pymysql://{username}:{password}@{host}/{database}")

# SQL query
query = "SELECT * FROM banking"

# Fetch data into DataFrame
df = pd.read_sql(query, engine)
# Display the DataFrame
print(df)
print(df.head(5))
# Generate descriptive statistics for the dataframe
print(df.describe())
bins = [0, 100000, 300000, float('inf')]
labels = ['Low', 'Med', 'High']
df['Income Band'] = pd.cut(df['Estimated Income'], bins=bins, labels=labels, right=False)
print(df)
df['Income Band'].value_counts().plot(kind='bar')
plt.show()
# Examine the distribution of unique cataegories in categorical columns
categorical_cols = df[["BRId", "GenderId", "IAId", "Amount of Credit Cards", "Nationality", "Occupation", "Fee Structure", "Loyalty Classification", "Properties Owned", "Risk Weighting", "Income Band"]].columns

for col in categorical_cols:
  print(f"Value Counts for '{col}':")
  print(df[col].value_counts())
  for col in categorical_cols:
  print(f"Value Counts for '{col}':")
  print(df[col].value_counts())
 # Plot the value counts as a bar chart
    plt.df[col].value_counts().plot(kind="bar", title=f"{col} Distribution")
    plt.xlabel(col)
    plt.ylabel("Count")
    plt.show()
    # Loop through the categorical columns and plot their distributions
for i, predictor in enumerate(df[["BRId", "GenderId", "IAId", "Amount of Credit Cards", "Nationality", "Occupation", "Fee Structure", "Loyalty Classification", "Properties Owned", "Risk Weighting", "Income Band"]].columns):
    plt.figure(i)      #  Create a new figure for each plot
        # Plot the distribution using seaborn
    sns.countplot(data=df, x=predictor)
    
    # Add labels and title
    plt.title(f'Distribution of {predictor}by Nationality')
    plt.xlabel(predictor)
    plt.ylabel('Count')

    # Display the plot
    plt.show()
  # HIstplot of value counts for different Occupation
  for col in categorical_cols:
  if col == "Occupation":
    continue
  plt.figure(figsize=(8,4))
  sns.histplot(df[col])
  plt.title('Histogram of Occupation Count')
  plt.xlabel(col)
  plt.ylabel("Count")
  plt.show()

numerical_cols = ['Estimated Income', 'Superannuation Savings', 'Credit Card Balance', 'Bank Loans', 'Bank Deposits', 'Checking Accounts', 'Saving Accounts', 'Foreign Currency Account', 'Business Lending']

# Univariate analysis and visualization
plt.figure(figsize=(15,10))
for i,col in enumerate(numerical_cols):
  plt.subplot(4,3,i+1)
  sns.histplot(df[col],kde=True)
  plt.title(col)
plt.show()
#heatmaps
numerical_cols = ['Estimated Income', 'Superannuation Savings', 'Credit Card Balance', 'Bank Loans', 'Bank Deposits', 'Checking Accounts', 'Saving Accounts', 'Foreign Currency Account', 'Business Lending']

correlation_matrix = df[numerical_cols].corr()

plt.figure(figsize=(12,12))
sns.heatmap(correlation_matrix, annot=True, cmap='crest', fmt=".2f")<img width="752" alt="data cleaning sc 1" src="https://github.com/user-attachments/assets/b9388c36-cfa8-4651-9a69-131eb2450d2a" />
<img width="752" alt="data cleaning sc 1" src="https://github.com/user-attachments/assets/1dcbe0ce-e039-48f3-abee-dd9ff93ac317" />

plt.title("Correlation Matrix")
plt.show()
import sys
print(sys.version)
# cleaning data using Power BI
Changing data type of Genderid as text from numerical
Replacing values ( 1 = male , 2 = female)
