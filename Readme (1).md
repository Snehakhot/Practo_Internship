```markdown
# Recruitment Data Analysis

This project performs data analysis on a recruitment dataset to gain insights into the performance and attrition rates of employees based on their recruiting sources. The analysis includes handling missing values, calculating summary statistics, and visualizing key metrics.

## Installation

To run the analysis, you need to install the following Python packages:
```bash
pip install pandas plotnine
```

## Usage

1. **Load the Data**
    - The data is loaded from a CSV file named `Recruitment_Data.csv`.
    - The first few rows of the dataframe are displayed to understand the structure of the data.

    ```python
    import pandas as pd

    # Load the data from a CSV file
    data = pd.read_csv('Recruitment_Data.csv')

    # Display the first few rows of the dataframe
    print(data.head())
    ```

2. **Check for Missing Values**
    - Check and display the number of missing values in each column.

    ```python
    # Check for missing values in each column
    missing_values = data.isnull().sum()

    # Print the number of missing values for each column
    print("Number of missing values in each column:")
    print(missing_values)
    ```

3. **Handle Missing Values**
    - Fill missing values in the `recruiting_source` column with the most common value (mode).

    ```python
    # Most common value (mode) in the recruiting_source column
    mode_value = data['recruiting_source'].mode()[0]

    # Fill missing values with the mode
    data['recruiting_source'].fillna(mode_value, inplace=True)

    # Verify the missing values are filled
    print("Updated missing values in each column:")
    print(data.isnull().sum())
    ```

4. **Group Data by Recruiting Source**
    - Group the data by `recruiting_source` to calculate summary statistics for each group.

    ```python
    # Group the data by 'recruiting_source'
    grouped_data = data.groupby('recruiting_source')
    ```

5. **Calculate Summary Statistics**
    - Calculate mean performance rating, mean sales quota percentage, and attrition rate for each recruiting source.
    - Combine these metrics into a single DataFrame for easier comparison and display the results.

    ```python
    # Calculate mean performance rating, mean sales quota percentage, and attrition rate for each group
    performance_avg = grouped_data['performance_rating'].mean()
    sales_quota_avg = grouped_data['sales_quota_pct'].mean()
    attrition_rate = grouped_data['attrition'].mean()  # Assuming attrition is coded as 1 for yes, 0 for no

    # Combine these metrics into a single DataFrame
    summary_stats = pd.DataFrame({
        'Average Performance Rating': performance_avg,
        'Average Sales Quota Percentage': sales_quota_avg,
        'Attrition Rate': attrition_rate
    })

    # Display the summary statistics for each recruitment source
    print(summary_stats.sort_values(by='Average Performance Rating', ascending=False))
    ```

6. **Visualize Results**
    - Calculate the average sales quota percentage (used as Sales Numbers) and attrition rate for each recruiting source.
    - Create a DataFrame to display these metrics clearly and sort by average sales and attrition numbers.

    ```python
    # Calculate the average sales quota percentage and attrition rate for each recruiting source
    average_sales = grouped_data['sales_quota_pct'].mean()
    average_attrition = grouped_data['attrition'].mean()

    # Create a DataFrame to display the results
    recruitment_performance = pd.DataFrame({
        'Average Sales Numbers': average_sales,
        'Average Attrition Numbers': average_attrition
    })

    # Print the average Sales Numbers and Attrition Numbers grouped by Recruiting Source
    print("Average Sales and Attrition Numbers by Recruiting Source:")
    print(recruitment_performance.sort_values(by=['Average Sales Numbers', 'Average Attrition Numbers'], ascending=[False, True]))
    ```

## Conclusion

This analysis provides valuable insights into the performance and attrition rates of employees based on their recruiting sources. By identifying which sources yield the best performance and lowest attrition, organizations can optimize their recruitment strategies to improve overall workforce quality.

