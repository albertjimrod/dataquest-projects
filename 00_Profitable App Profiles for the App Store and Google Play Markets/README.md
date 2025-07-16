
# Profitable App Profiles for the App Store and Google Play Markets

This project analyzes a dataset of mobile apps from the App Store and Google Play to identify profitable app profiles. The goal is to provide data-driven insights for developers on what types of apps are most likely to succeed.

The consolidated notebook, `Profitable App Profiles For The App Store And Google Play Markets.ipynb`, contains the complete analysis, from data cleaning to final conclusions.

## Dataset

The analysis uses two datasets:

*   **`AppleStore.csv`**: Contains data about approximately 7,000 iOS apps from the App Store.
*   **`googleplaystore.csv`**: Contains data about approximately 10,000 Android apps from Google Play.

## Analysis Performed

The notebook follows a structured workflow to clean, analyze, and visualize the data. Key steps include:

1.  **Data Loading and Initial Cleaning:**
    *   Loading the datasets, ensuring correct character encoding (`UTF-8`).
    *   Identifying and removing duplicate entries to ensure data quality.
    *   Correcting data entry errors and removing apps with non-English names.

2.  **Data Filtering:**
    *   Filtering out non-free apps to focus the analysis on apps with a freemium revenue model.
    *   Isolating apps that are directed toward an English-speaking audience.

3.  **Data Analysis:**
    *   Calculating the average number of ratings for each app genre to identify which categories are most popular.
    *   Determining the most common genres on both platforms.
    *   Analyzing the distribution of apps by genre to find the most common app profiles.

4.  **Conclusions and Recommendations:**
    *   Providing actionable recommendations for developers based on the analysis, suggesting which app profiles are most likely to be profitable on both the App Store and Google Play.

## Requirements

To run this notebook, you need to have the following libraries installed. You can install them using `pip`:

```
pip install -r requirements.txt
```

Contents of the `requirements.txt` file:

```
pandas
numpy
```

## How to Run

1.  Ensure you have the `AppleStore.csv` and `googleplaystore.csv` files in the same directory as the notebook.
2.  Install the dependencies listed in the `requirements.txt` file.
3.  Start Jupyter Lab or Jupyter Notebook:
    ```bash
    jupyter lab
    ```
4.  Open the `Profitable App Profiles For The App Store And Google Play Markets.ipynb` file and run the cells.
