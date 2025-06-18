# Customer Churn Analysis in Telcom Using Exploratory Data Analysis(EDA)

## Project Overview

**Project Title**: Customer Churn Analysis

In this project, we explore the Telco Customer Churn dataset to uncover patterns and insights about customer behavior. The primary goal is to understand what factors  contribute to customer churn, i.e why customers leave the service.
This Exploratory Data Analysis (EDA) project includes:
<br>
-  **Data loading, cleaning and preprocessing**<br>
-  **Univariate and bivariate analysis**<br>
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




