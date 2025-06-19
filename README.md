# Customer Churn Analysis in Telcom Using Exploratory Data Analysis(EDA)

## Project Overview

**Project Title**: Customer Churn Analysis

In this project, we explore the Telco Customer Churn dataset to uncover patterns and insights about customer behavior. The primary goal is to understand what factors  contribute to customer churn, i.e why customers leave the service.
This Exploratory Data Analysis (EDA) project includes:
<br>
-  **Data loading, cleaning and preprocessing**<br>
-  **Exploratory Data Analysis**<br>
-  **Visualization of churn patterns**<br>
-  **Statistical summaries**

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






