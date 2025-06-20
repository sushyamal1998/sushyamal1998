# Customer Churn Analysis in Telcom Using Exploratory Data Analysis(EDA)

## Project Overview

**Project Title**: Customer Churn Analysis

In this project, we explore the Telco Customer Churn dataset to uncover patterns and insights about customer behavior. The primary goal is to understand what factors  contribute to customer churn, i.e why customers leave the service.
This Exploratory Data Analysis (EDA) project includes:
<br>
-  **Data loading, cleaning and preprocessing**<br>
-  **Univariate Analysis**<br>
-  **Bivariate Analysis**<br>
-  **Multivariate Analysis**

## Tools and Libraries used:
- **Python**
- **pandas->** for data manipulation
- **Matplotlib and Seaborn->** for visualization
- **Google Colab->** for interactive analysis

## Dataset:
- **Source->** Kaggle - Telco Customer Churn
- **Rows->** 7043
- **Columns->** 21 features including customerid, gender,churn etc.

  
### 1: Data Loading and Cleaning
- Import necessary python library:

```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```
- Import Dataset:
```python
df = pd.read_csv("/content/WA_Fn-UseC_-Telco-Customer-Churn.csv")
```
- data Cleaning:


  ```python
  # check column for empty string or empty space.
  for col in df.columns:
    if df[col].dtype == 'object': 
        has_empty = df[col].str.strip().eq("").any()
        if has_empty:
            print(f"Column '{col}' contains empty or blank strings.")
  ```
```python
  # replace empty string with 0
  df['TotalCharges'] = df['TotalCharges'].replace(" ", 0)
  df['TotalCharges'] = df['TotalCharges'].astype(float)
```

```python
 # checking for null values
 df.isnull().sum()
```

```python
 df.duplicated().sum()
```
```python
  #converted 0 and 1 values of senior citizen to Yes/No.
  def conv(value):
    if value == 0:
      return "Yes"
    else:
      return "No"
  
  df['SeniorCitizen'] = df['SeniorCitizen'].apply(conv)
```


## 2: Exploratory Data Analysis(EDA)

- **Univariate analysis of categorical variable churn** :
  ```python
  plt.figure(figsize = (4,4))
  ax = sns.countplot(x= 'Churn', data = df)
  ax.bar_label(ax.containers[0])
  plt.title("count of customer by churn")
  plt.show()
  ```
  **conclusion->** most customer did not churn 
- **pie chart of percentage of churn customer**:
  ```python
  plt.figure(figsize = (4,5))
  plt.pie(df['Churn'].value_counts(), labels = df['Churn'].value_counts().index, autopct = '%1.1f%%')
  plt.title('Percentages Of Churn Customer', fontsize = 10)
  plt.show()
  ```

- **univariate analysis of numerical variable tenure**:
  ```python
    plt.figure(figsize = (4,4))
    sns.histplot(df['tenure'])
    plt.title("Distribution of Customer Tenure", fontsize=14)
    plt.xlabel("Tenure (in months)", fontsize=12)
    plt.ylabel("Number of Customers", fontsize=12)
    plt.show() 
  ```
  **conclusion->** A large number of customer habe very sort tenure(1-2 month), means some customer leaves sortly after joining.<br> There is also so manny long term customer.

- **Bivariate analysis**:
  ```python
    plt.figure(figsize = (4,4))
    ax = sns.countplot(x= 'gender', hue = 'Churn',data = df)
    for container in ax.containers:
      ax.bar_label(container)
    plt.xticks(rotation = 45)
    plt.xlabel("Gender")
    plt.ylabel("Count")
    plt.title("churn by gender")
    plt.show()
  ```
  **conclusion->** Ratio of gender of customer are same and there churn ratio almost same

 - **Bivariate analysis**:
   ```python
    plt.figure(figsize = (8,4))
    sns.histplot(x= 'tenure', bins = 30, hue = 'Churn', data = df)
    plt.title("Customer Tenure vs. Churn", fontsize=14, fontweight='bold')
    plt.xlabel("Tenure (in months)", fontsize=12)
    plt.ylabel("Number of Customers", fontsize=12)
    plt.tight_layout()
    plt.show() 
   ```
   **conclusion->** Customer with low tenure(1-10month) has higher churn rate and customer with median to higher have less churn rate.

 - **Bivariate analysis**:
   ```python
      ax = sns.countplot(x= df['Contract'], hue = df['Churn'])
      for container in ax.containers:
          ax.bar_label(container)
      plt.title("Churn by Contract Type")
      plt.xlabel("Contract Type")
      plt.ylabel("Number of Customers")
      plt.legend(title='Churn Status')
      plt.tight_layout()
      plt.show()  
   ```
   **Conclusion->** Customer with month to month contract have higher churn rate and who habe one or two year contract less churn rate.

 - **Bivariate analysis**:
   ```python
      cols = ['PhoneService', 'MultipleLines', 'InternetService',
       'OnlineSecurity', 'OnlineBackup', 'DeviceProtection',
       'TechSupport', 'StreamingTV', 'StreamingMovies']

      n_cols = 3
      n_rows = (len(cols)+n_cols-1)// n_cols
      fig,axes = plt.subplots(n_rows,n_cols,figsize= (15,12))
      axes = axes.flatten()
      for i, col in enumerate(cols):
        sns.countplot(x =col, ax = axes[i], hue = 'Churn', data = df)
        axes[i].set_title(col)
        axes[i].set_ylabel("Count")
        axes[i].tick_params(axis='x', rotation=45)
      plt.tight_layout()
      plt.show()  

   ```

- **Multivariate analysis of monthly charges vs tenure, color by churn**:
  ```python
  plt.figure(figsize=(10,6))
  sns.scatterplot(x='tenure', y='MonthlyCharges', hue='Churn',data=df)
  plt.title("Tenure vs Monthly Charges colored by Churn")
  plt.xlabel("Tenure (months)")
  plt.ylabel("Monthly Charges")
  plt.grid(True)
  plt.tight_layout()
  plt.show()
  ```

- **Multivariate analysis : monthly charges by payment method and churn**:
  ```python
    plt.figure(figsize=(10,6))
    sns.boxplot(x='PaymentMethod', y='MonthlyCharges', hue='Churn', data=df)
    plt.title("Monthly Charges by Payment Method and Churn")
    plt.xticks(rotation=45)
    plt.tight_layout()
    plt.show()
  ```

- **Heatmap of corelation between numeric features**:
  ```python
    df['TotalCharges'] = pd.to_numeric(df['TotalCharges'], errors='coerce')
    plt.figure(figsize=(6,4))
    sns.heatmap(df[['tenure', 'MonthlyCharges', 'TotalCharges']].corr(), annot=True, cmap='coolwarm')
    plt.title("Correlation Between Numeric Features")
    plt.tight_layout()
    plt.show()
  ```
  **Conclusion->** Stronger correlation between Tenure and TotalCharges.

## Conclusion: 
This EDA helped surface valuable insights into customer churn behavior. The analysis can support telecom companies in building targeted retention strategies, especially focused on:
- Improving the experience of new users in the first few months
- Addressing issues for high-paying users who churn early











