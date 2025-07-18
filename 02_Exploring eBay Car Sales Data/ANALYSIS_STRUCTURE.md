# Replicable Analysis Structure for Tabular Data

This document outlines a structured, step-by-step workflow for cleaning, exploring, and analyzing tabular datasets, based on the "eBay Car Sales" analysis. It can be used as a template for future data analysis projects.

---

### Phase 1: Setup and Data Loading

**Objective:** To correctly load the data into a pandas DataFrame and set up the analysis environment.

**Actions:**
1.  **Import Libraries:** Load necessary libraries like pandas, numpy, and matplotlib.
    ```python
    import pandas as pd
    import numpy as np
    import matplotlib.pyplot as plt
    import chardet # For encoding detection
    %matplotlib inline
    ```
2.  **Detect File Encoding (Optional but Recommended):** For files with potential encoding issues, use a library like `chardet` to prevent errors.
    ```python
    with open('your_dataset.csv', 'rb') as file:
        encoding_result = chardet.detect(file.read())
    print(encoding_result)
    ```
3.  **Load Data:** Load the data into a pandas DataFrame using the detected encoding.
    ```python
    df = pd.read_csv('your_dataset.csv', encoding=encoding_result['encoding'])
    ```
4.  **Initial Inspection:** Get a first look at the data.
    ```python
    print(df.info())
    print(df.head())
    ```

---

### Phase 2: Initial Cleaning & Preprocessing

**Objective:** To perform high-level cleaning tasks that prepare the dataset for more detailed analysis.

**Actions:**
1.  **Standardize Column Names:** Convert column names to a consistent format (e.g., snake_case) for easier access.
    ```python
    # Example of renaming specific columns
    df.rename({'camelCaseName': 'snake_case_name'}, axis=1, inplace=True)
    
    # Or create a function to clean all columns
    def clean_col(col):
        # custom cleaning logic
        return col.lower()
    df.columns = [clean_col(c) for c in df.columns]
    ```
2.  **Drop Irrelevant Columns:** Remove columns that do not add value to the analysis (e.g., columns with a single unique value, or IDs that are not needed).
    ```python
    columns_to_drop = ['column_a', 'column_b']
    df.drop(columns_to_drop, axis=1, inplace=True)
    ```
3.  **Clean and Convert Numeric Columns:** Identify columns that are numeric but stored as text. Remove non-numeric characters and convert to the correct data type.
    ```python
    # Example for a price column
    df['price_usd'] = df['price_usd'].str.replace('$', '').str.replace(',', '').astype(float)
    
    # Example for an odometer column
    df['odometer_km'] = df['odometer_km'].str.replace('km', '').str.replace(',', '').astype(int)
    ```

---

### Phase 3: In-depth Data Exploration & Outlier Handling

**Objective:** To understand the distribution of key numeric columns and handle outliers in a logical, informed way.

**Actions:**
1.  **Explore Numeric Distributions:** Use `.describe()` and `.value_counts()` to understand the range, central tendency, and frequency of values.
    ```python
    print(df['numeric_column'].describe())
    print(df['numeric_column'].value_counts().sort_index(ascending=False).head(10))
    ```
2.  **Identify and Investigate Outliers:** Look for values that seem unrealistic (e.g., extremely high or low prices, impossible years).
    *   **Rationale:** Instead of blindly removing outliers, investigate them. They could be data entry errors or legitimate, rare occurrences.
3.  **Filter Data Based on Logical Constraints:** Remove or correct rows that are impossible or don't fit the context of the analysis.
    ```python
    # Example: Keep only cars within a realistic price range
    df = df[df['price_usd'].between(500, 400000)]

    # Example: Keep only cars with a realistic registration year
    # (e.g., not registered after the data was collected)
    df = df[df['registration_year'].between(1920, 2017)]
    ```
4.  **Manual Correction (If Necessary):** For specific, identifiable errors, manual correction can be more precise than broad filtering.
    ```python
    # Example: Correcting a single erroneous data point
    # df.loc[df['id'] == 'some_unique_id', 'column_to_fix'] = new_value
    ```

---

### Phase 4: Feature Engineering & Transformation

**Objective:** To modify or create features to make them more useful for analysis.

**Actions:**
1.  **Translate Categorical Data:** If the data is in a foreign language, translate it to make it more accessible.
    ```python
    # Create a mapping dictionary
    translator_map = {'german_word': 'english_equivalent', 'another_word': 'another_equivalent'}
    # Apply the map
    df['categorical_column'] = df['categorical_column'].map(translator_map)
    ```
2.  **Handle Missing Values:** Decide on a strategy for `NaN` values (e.g., fill with a common value, drop rows, or use a more advanced imputation method).
    ```python
    # Example: Fill with the mode (most frequent value)
    mode_value = df['column_with_nan'].mode()[0]
    df['column_with_nan'].fillna(mode_value, inplace=True)
    ```

---

### Phase 5: Aggregate Analysis

**Objective:** To derive insights by grouping data and calculating summary statistics.

**Actions:**
1.  **Group by Categorical Columns:** Use `groupby()` to aggregate data and calculate metrics for different categories.
    ```python
    # Example: Average price by brand
    brand_avg_price = df.groupby('brand')['price_usd'].mean().sort_values(ascending=False)
    print(brand_avg_price)
    ```
2.  **Combine Multiple Aggregations:** Create a summary DataFrame to compare different metrics across categories.
    ```python
    # Using a dictionary to store aggregated data
    brands_agg = {}
    for brand in top_brands:
        subset = df[df['brand'] == brand]
        brands_agg[brand] = {
            'mean_price': subset['price_usd'].mean(),
            'mean_mileage': subset['odometer_km'].mean()
        }
    
    summary_df = pd.DataFrame.from_dict(brands_agg, orient='index')
    print(summary_df)
    ```

---

### Phase 6: Visualization

**Objective:** To visually represent the findings for easier interpretation.

**Actions:**
1.  **Histograms for Distributions:**
    ```python
    df['numeric_column'].hist(bins=20)
    plt.title('Distribution of ...')
    plt.show()
    ```
2.  **Bar Charts for Categorical Comparisons:**
    ```python
    summary_df['mean_price'].plot(kind='bar')
    plt.title('Average Price by Brand')
    plt.show()
    ```
3.  **Scatter Plots for Relationships:**
    ```python
    summary_df.plot(kind='scatter', x='mean_mileage', y='mean_price')
    plt.title('Price vs. Mileage')
    plt.show()
    ```
