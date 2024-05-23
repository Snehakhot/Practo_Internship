# Recruitment Data Analysis

## Introduction
This project involves analyzing recruitment data to understand the impact of different recruiting sources on key performance metrics such as performance rating, sales quota percentage, and attrition rate. The analysis includes handling missing values, calculating summary statistics, and visualizing the data.

## Prerequisites
- Python 3.x
- pandas
- plotnine

## Installation
To install the required libraries, run the following command:

```bash
pip install pandas plotnine
```

## Usage

### Load the Data
The data is loaded from a CSV file named `Recruitment_Data.csv`. Ensure that this file is available in the same directory as the script.

```python
import pandas as pd

# Load the data from a CSV file
data = pd.read_csv('Recruitment_Data.csv')
```

### Data Overview
Display the first few rows of the dataset to understand its structure:

```python
# Display the first few rows of the dataframe
print(data.head())
```

### Check for Missing Values
Check and print the number of missing values in each column:

```python
# Check for missing values in each column
missing_values = data.isnull().sum()

# Print the number of missing values for each column
print("Number of missing values in each column:")
print(missing_values)
```

### Handle Missing Values
Fill missing values in the `recruiting_source` column with the most common value (mode):

```python
# Most common value (mode) in the recruiting_source column
mode_value = data['recruiting_source'].mode()[0]

# Fill missing values with the mode
data['recruiting_source'].fillna(mode_value, inplace=True)

# Verify the missing values are filled
print("Updated missing values in each column:")
print(data.isnull().sum())
```

### Group Data and Calculate Summary Statistics
Group the data by `recruiting_source` and calculate mean performance rating, mean sales quota percentage, and attrition rate for each group:

```python
# Assuming missing values have already been handled, we will group the data by 'recruiting_source'
grouped_data = data.groupby('recruiting_source')

# Calculate mean performance rating, mean sales quota percentage, and attrition rate for each group
performance_avg = grouped_data['performance_rating'].mean()
sales_quota_avg = grouped_data['sales_quota_pct'].mean()
attrition_rate = grouped_data['attrition'].mean()  # Assuming attrition is coded as 1 for yes, 0 for no

# Combine these metrics into a single DataFrame for easier comparison
summary_stats = pd.DataFrame({
    'Average Performance Rating': performance_avg,
    'Average Sales Quota Percentage': sales_quota_avg,
    'Attrition Rate': attrition_rate
})

# Display the summary statistics for each recruitment source
print(summary_stats.sort_values(by='Average Performance Rating', ascending=False))
```

### Calculate and Display Recruitment Performance
Calculate and display the average sales quota percentage and attrition rate for each recruiting source:

```python
# Calculate the average sales quota percentage (used as Sales Numbers) and attrition rate for each recruiting source
average_sales = grouped_data['sales_quota_pct'].mean()
average_attrition = grouped_data['attrition'].mean()

# Creating a DataFrame to display the results more clearly
recruitment_performance = pd.DataFrame({
    'Average Sales Numbers': average_sales,
    'Average Attrition Numbers': average_attrition
})

# Printing out the average Sales Numbers and Attrition Numbers grouped by Recruiting Source
print("Average Sales and Attrition Numbers by Recruiting Source:")
print(recruitment_performance.sort_values(by=['Average Sales Numbers', 'Average Attrition Numbers'], ascending=[False, True]))
```

## Conclusion
This script provides a detailed analysis of recruitment data, including handling missing values and calculating key performance metrics. The summary statistics help in identifying the most effective recruiting sources based on performance ratings, sales numbers, and attrition rates. For further analysis or visualization, consider using the `plotnine` library to create informative plots.
