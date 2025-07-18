# Exploring eBay Kleinanzeigen Car Sales Data

## Introduction

This project involves a comprehensive analysis of a dataset of used cars from *eBay Kleinanzeigen*, a classifieds section of the German eBay website. The original dataset was scraped and uploaded to Kaggle and contains 50,000 data points, providing a rich source for data cleaning and exploratory analysis.

The primary goal of this project is to clean the data, handle inconsistencies and outliers, and perform an exploratory analysis to uncover insights about the used car market on this platform.

The final consolidated analysis can be found in the Jupyter Notebook: `Ebay_Car_Sales_Analysis_Consolidated.ipynb`.

## Data Dictionary

The dataset contains 20 columns, most of which are strings. Some columns have null values.

| Column                | Description                                                                 |
|-----------------------|-----------------------------------------------------------------------------|
| `dateCrawled`         | When this ad was first crawled.                                             |
| `name`                  | Name of the car.                                                            |
| `seller`              | Whether the seller is private or a dealer.                                  |
| `offerType`           | The type of listing.                                                        |
| `price`                 | The price on the ad to sell the car.                                        |
| `abtest`              | Whether the listing is included in an A/B test.                             |
| `vehicleType`         | The vehicle Type.                                                           |
| `yearOfRegistration`  | The year in which the car was first registered.                             |
| `gearbox`               | The transmission type.                                                      |
| `powerPS`               | The power of the car in PS (Pferdestärke, German for horsepower).           |
| `model`                 | The car model name.                                                         |
| `odometer`              | How many kilometers the car has driven.                                     |
| `monthOfRegistration` | The month in which the car was first registered.                            |
| `fuelType`            | What type of fuel the car uses.                                             |
| `brand`                 | The brand of the car.                                                       |
| `notRepairedDamage`   | If the car has damage which is not yet repaired.                            |
| `dateCreated`           | The date on which the eBay listing was created.                             |
| `nrOfPictures`        | The number of pictures in the ad.                                           |
| `postalCode`            | The postal code for the location of the vehicle.                            |
| `lastSeen`            | When the crawler saw this ad last online.                                   |

## Analysis and Cleaning Steps

The consolidated notebook performs the following key steps:

1.  **Initial Data Loading**: The notebook starts by detecting the file's character encoding (`chardet`) to ensure proper data loading and prevent errors.
2.  **Column Cleaning and Standardization**:
    *   Column names were converted from `camelCase` to `snake_case` to align with Python's standard naming conventions (e.g., `yearOfRegistration` becomes `registration_year`).
    *   Columns with little to no variance or relevance for this analysis (like `seller`, `offerType`, `nrOfPictures`) were dropped.
3.  **Data Type Conversion**:
    *   Numeric columns stored as text (e.g., `price` and `odometer`) were cleaned of non-numeric characters (like `$`, `,`, `km`) and converted to numeric types (`int`, `float`) to enable calculations.
4.  **Detailed Outlier Analysis**:
    *   A thorough investigation of outliers in the `price` column was conducted. Instead of blindly removing all high-priced vehicles, их values were researched.
    *   It was discovered that the `sonstige_autos` (other cars) category contained legitimate high-value vehicles like Ferraris and Rolls Royces.
    *   Erroneous high prices for common cars (like Opel Vectra) were identified and selectively removed.
    *   A specific incorrect price for a classic Maserati was manually corrected based on market research, showcasing a detailed and careful data cleaning approach.
5.  **Date and Categorical Data Cleaning**:
    *   The `registration_year` was validated to ensure it fell within a logical range (e.g., not after the ad was crawled in 2016).
    *   Categorical data in German (e.g., in `vehicle_type` and `fuel_type`) was translated to Spanish/English to make the analysis more accessible and understandable.
6.  **Aggregate Analysis**:
    *   The top car brands were identified, and their average price and mileage were calculated and compiled into a summary DataFrame for easy comparison. This helps to understand the trade-offs between brand, price, and vehicle usage.

## How to Use

To explore the analysis, open and run the `Ebay_Car_Sales_Analysis_Consolidated.ipynb` notebook in a Jupyter environment. The notebook is self-contained and includes all the steps from data loading to final analysis.
