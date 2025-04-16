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
sns.heatmap(correlation_matrix, annot=True, cmap='crest', fmt=".2f")

plt.title("Correlation Matrix")
plt.show()
import sys
print(sys.version)
# cleaning data using Power BI
Changing data type of Genderid as text from numerical
Replacing values ( 1 = male , 2 = female)
<img width="752" alt="data cleaning sc 1" src="https://github.com/user-attachments/assets/3b828d77-d993-460d-a47b-9a43deb5263c" />

Added conditional column
<img width="759" alt="data cleaning sc 2" src="https://github.com/user-attachments/assets/af037844-cba8-46a8-b853-173b38fb259f" />

Changing data type of BRid
Replacing values(1=Retail, 2=Institutional, 3=Private Bank, 4=Commercial)
<img width="677" alt="data cleaning sc 3" src="https://github.com/user-attachments/assets/aa650eb4-7304-4a97-83e5-bd2e96913f8d" />

# Calculated Functions – 
# Sum : 
The power bi sum function will add all the numbers in a column and the column contains numbers to sum. It returns a decimal number.
Syntax :
total deposit = SUM(banking[Bank Deposits])+SUM(banking[Saving Accounts])+SUM(banking[Checking Accounts])+SUM(banking[Foreign Currency Account])

Total Loan = 
SUMX(
    banking, 
    banking[Bank Loans] + banking[Business Lending] + banking[Credit Card Balance]
)

year of joining = YEAR(banking[Joined Bank])

KPI’S: 

In which followings KPIS are present :
# Total Clients : 

Total Clients KPI represents total number of clients in banking.

Total Clients = DISTINCTCOUNT('Clients - Banking'[IAId] )
<img width="176" alt="TC" src="https://github.com/user-attachments/assets/a05259ff-c6b2-4857-b49a-779106aed13c" />
# Total Loan :

Total Loan gives you information about the Bank Loans, Business Lending, Credit Card Balance
Total Loan = 
SUMX(
    banking, 
    banking[Bank Loans] + banking[Business Lending] + banking[Credit Card Balance]
)
<img width="176" alt="TOTAL LOAN" src="https://github.com/user-attachments/assets/684db8e9-db7e-437e-b978-ed12041521a6" />

# Bank Loan :
Bank Loan gives you information what is the loan amount of loan to be repaid by the client to bank.
Bank Loan = SUM('Clients - Banking'[Bank Loans] )
<img width="143" alt="BANK LOAN" src="https://github.com/user-attachments/assets/103889b8-eda3-4554-b737-cc0de9e4c2f7" />

# Business Lending :
Business lending gives you information about the loan amount given to small business.
Business Lending = SUM('Clients - Banking'[Business Lending] )
<img width="178" alt="BUSINESS LENDING" src="https://github.com/user-attachments/assets/d60fcc57-aaab-4228-9eb3-210b858bb791" />

# Total Deposit 
Total Deposit gives you information about the amount deposited by particular investors in bank
total deposit = SUM(banking[Bank Deposits])+SUM(banking[Saving Accounts])+SUM(banking[Checking Accounts])+SUM(banking[Foreign Currency Account])
<img width="177" alt="TOTAL DEPOSIT" src="https://github.com/user-attachments/assets/ce19ff3a-b070-45c0-885c-af7f677b2b3a" />

# Total Fees :
Total Fees is nothing but the amount charged by the bank for account set-up , maintenance charges etc.
Total Fees = SUMX('Clients - Banking' , [Total Loan] * 'Clients - Banking'[Processing Fees] )
<img width="141" alt="TOTAL FEE" src="https://github.com/user-attachments/assets/f6e8e952-f6d1-49e8-99ec-d6d8d47596eb" />

# Bank Deposit :
Bank deposit is the money put in the bank.
Bank Deposit = 
SUM('Clients - Banking'[Bank Deposits] )
<img width="143" alt="bank deposit" src="https://github.com/user-attachments/assets/2bd3f0be-5910-4c33-945a-d8cd785426a1" />

# Checking Account Amount :
Checking account amount  is nothing but which offers easy access to your money for daily transactional needs.
Checking Accounts = 
SUM('Clients - Banking'[Checking Accounts] )
<img width="142" alt="CHECKING AMOUNT" src="https://github.com/user-attachments/assets/8de0b5d6-f006-47d6-afe6-3f5614ac36ef" />

# Total CC Amount :
Total CC Amount is a short-term source of financing for a company by a bank.
Total CC Amount = SUM('Clients - Banking'[Amount of Credit Cards] )
<img width="145" alt="TOTAL CC AMOUNT" src="https://github.com/user-attachments/assets/9dbbd1b6-c3ed-445c-b955-efbc0564a63d" />

# Saving Account Amount :
A savings account is an interest-bearing deposit account held at a bank.
Savings Account = SUM('Clients - Banking'[Saving Accounts] ) 
<img width="178" alt="SAVINGS ACCOUNT" src="https://github.com/user-attachments/assets/e72a9e14-f73a-470a-9ee2-1c5cf6094aa9" />

# Foreign Currency Amount :
Foreign Currency Account means an account held in a currency that is not the currency of India or Bhutan or Nepal.
Foreign Currency Account = 
SUM('Clients - Banking'[Foreign Currency Account] ) 
<img width="140" alt="FOREIGN CURRENCY" src="https://github.com/user-attachments/assets/f4e62f45-a37b-497c-a529-116f402d76a2" />
# Visualization And Result –
# Home 
<img width="612" alt="home" src="https://github.com/user-attachments/assets/6792f28f-723d-4178-a0d3-d107634c6564" />

# Loan analysis
<img width="611" alt="loan analysis" src="https://github.com/user-attachments/assets/360e709b-978d-4399-bc06-3d3efcea3dfc" />

# Deposit analysis
<img width="611" alt="deposit analysis" src="https://github.com/user-attachments/assets/b4e4a7f0-ae82-4087-a89a-4023cf0d05ee" />

# Summary
<img width="608" alt="summary" src="https://github.com/user-attachments/assets/29fc7c14-9b50-46db-a6db-cea2aba5f3e0" />

# Question and Answer
<img width="611" alt="last" src="https://github.com/user-attachments/assets/76420b91-a5ca-4209-aa72-ce423f4a143c" />
# Conclusion –
Empowered by the latest data visualization techniques, Power BI dashboards are among the most effective resources for using in banking sector. As outlined in this write-up, a banking  operations dashboard in Power BI can be developed with key banking related metrics and KPIs.
# Future Work –
With these dashboards banks can easily know what is the total loan amount and all other things of a particular investor.
It also helps which type of banks have more number of clients as we can see private banks have more number of clients so it can helps other banks can build their strategies to increase clients.
It also provides insights about which nationality has highest bank loans.
It gives information about various types of amount involved in different types of accounts by investors
