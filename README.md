# Data-Wrangling-airline-data
# Passengers Satisfaction Survey Analysis

## Project Overview

This project involves analyzing a dataset containing survey responses of airline passengers. The dataset includes data about passengers' satisfaction levels regarding various aspects of their travel experiences. The analysis focuses on the data for Business Class passengers, and the project aims to perform data cleansing, exploration, and export the cleaned data.

## Libraries Used

The following Python libraries are used for data manipulation and analysis:

```python
import pandas as pd
import numpy as np
```

## Data Loading

The dataset is loaded from a CSV file named `Passengers_Satisfaction_Survey.csv` using pandas:

```python
# Load the passengers' satisfaction survey dataset from a CSV file into a DataFrame.
df = pd.read_csv('Passengers_Satisfaction_Survey.csv')
```

## Data Subsetting

The analysis focuses specifically on Business Class passengers. To subset the data:

```python
# Subset the DataFrame to include only data about Business Class passengers.
df_business = df[df['Class'] == 'Business']
```

## Data Exploration

The dataset contains information about 50,000 Business Class passengers. Here are some exploratory steps:

- Viewing basic information of the subset:

```python
df_business.info()
```

- Checking the shape of the dataset:

```python
df_business.shape
```

- Displaying unique values for each column to identify possible inconsistencies:

```python
for cols in df_business.columns:
    unique_values = df_business[cols].unique()
    print(f"Unique values in column '{cols}': {unique_values}")
    print('============================')
```

## Data Cleaning

Several data cleansing steps were taken to improve the quality of the dataset:

- **Handling Missing Values**: Count the number of missing values in each column:

```python
df_business.isnull().sum()
```

- **Data Type Conversion**: Convert specified columns to integer type:

```python
df_business['ease_of_online_booking'] = df_business['ease_of_online_booking'].astype(int)
df_business['food_and_drink'] = df_business['food_and_drink'].astype(int)
```

- **Imputation**: Mode imputation of the `flight_distance` column:

```python
df_business['flight_distance'] = df_business['flight_distance'].replace([9000000, 2820000, -5421, 0, 0],[337, 337, 337, 337, 337])
```

- **Removing Duplicates**: Remove fully duplicated rows to clean up the data:

```python
# Removing fully duplicated rows
df_business = df_business.drop_duplicates()

# Optionally, reset the index
df_business.reset_index(drop=True, inplace=True)
```

## Export Cleaned Dataset

After data cleaning, the dataset is exported to an Excel file for further use:

```python
df_business.to_excel('Project_2_Group9.xlsx', sheet_name='Sheet1', index=False)
```

## Summary of Changes

### Before Cleansing
- The dataset contained 50,000 rows and 16 columns.
- Some columns had inconsistent or missing data, and there were fully duplicated rows.

### After Cleansing
- Data points reduced to 38,577 after filtering for Business Class and removing duplicates.
- Handled missing values, converted columns to appropriate types, and replaced incorrect values.

## Conclusion

The project successfully cleansed and filtered the passengers' satisfaction dataset to focus on Business Class passengers. The final cleaned dataset can now be used for further analysis or predictive modeling.

Feel free to contribute or reach out if you have any suggestions!

## How to Run
1. Clone this repository.
2. Ensure you have the required libraries (`pandas`, `numpy`) installed.
3. Run the code in a Jupyter Notebook or Python environment.
