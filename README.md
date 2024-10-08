# Uber Trip Data Analysis

This project involves analyzing and transforming Uber trip data using Python and `pandas`. The data is structured into a **star schema**, which is commonly used in data warehousing for efficient querying and reporting.

## Table of Contents
- [Project Overview](#project-overview)
- [Data](#data)
- [Data Processing](#data-processing)
- [Schema Design](#schema-design)
- [Usage](#usage)
- [Requirements](#requirements)

## Project Overview

The goal of this project is to load and process Uber trip data into a star schema format. This schema includes multiple dimensions such as time, passenger count, trip distance, and payment type. The project leverages Python and `pandas` to transform raw CSV data into a fact table and several dimension tables that can be used for efficient data analysis.

## Data

The dataset used in this project contains information about Uber rides, including:

- Vendor ID
- Pickup and Dropoff DateTimes
- Passenger Count
- Trip Distance
- Pickup and Dropoff Locations (Longitude/Latitude)
- Rate Codes
- Payment Types
- Fare and Additional Charges

### Sample Data (Before Transformation):
| VendorID | tpep_pickup_datetime  | tpep_dropoff_datetime | passenger_count | trip_distance | pickup_longitude | pickup_latitude | payment_type | fare_amount | tip_amount |
|----------|-----------------------|-----------------------|-----------------|---------------|------------------|-----------------|--------------|-------------|------------|
| 1        | 2016-03-01 00:00:00   | 2016-03-01 00:07:55   | 1               | 2.50          | -73.976746       | 40.765152        | 1            | 9.0         | 2.05       |

## Data Processing

The steps involved in processing the raw Uber trip data:

1. **Load the Data**: The raw data is loaded from a CSV file into a pandas DataFrame.
2. **Convert DateTime Columns**: The pickup and dropoff times are converted from strings to datetime objects for easier manipulation.
3. **Create Dimension Tables**: Dimension tables for passenger counts, trip distances, rate codes, locations, and payment types are created by extracting unique values from the dataset.
4. **Create Fact Table**: The fact table is constructed by merging the dimensions with the original data on relevant keys.

### Processing Flow
1. **Load Data**: Load the CSV file into a pandas DataFrame.
2. **Datetime Conversion**: Convert `tpep_pickup_datetime` and `tpep_dropoff_datetime` columns to `datetime` format.
3. **Create Dimensions**:
    - `datetime_dim`: Extracts year, month, day, hour, and weekday from the pickup and dropoff times.
    - `passenger_count_dim`: Unique passenger count values.
    - `trip_distance_dim`: Unique trip distances.
    - `rate_code_dim`: Rate codes with their descriptions (e.g., Standard, JFK, etc.).
    - `pickup_location_dim` & `dropoff_location_dim`: Unique pickup and dropoff coordinates.
    - `payment_type_dim`: Payment methods with their descriptions (e.g., Credit card, Cash, etc.).
4. **Merge into Fact Table**: The final `fact_table` is created by joining the original data with each of the dimension tables.

## Schema Design

The data is transformed into a **star schema** format, which includes:

- **Fact Table**:
  - Contains ride transactions, keys to dimension tables, and relevant metrics like `fare_amount`, `tip_amount`, `total_amount`.
  
- **Dimension Tables**:
  - **Datetime Dimension**: Contains detailed pickup/dropoff datetime information.
  - **Passenger Count Dimension**: Contains unique passenger counts.
  - **Trip Distance Dimension**: Contains unique trip distances.
  - **Rate Code Dimension**: Contains descriptions for rate codes.
  - **Pickup and Dropoff Location Dimensions**: Contain unique latitude/longitude pairs for pickup and dropoff locations.
  - **Payment Type Dimension**: Contains descriptions for payment methods.

### Fact Table Sample:
| VendorID | datetime_id | passenger_count_id | trip_distance_id | rate_code_id | payment_type_id | fare_amount | tip_amount | total_amount |
|----------|-------------|--------------------|------------------|--------------|-----------------|-------------|------------|--------------|
| 1        | 0           | 0                  | 0                | 0            | 0               | 9.0         | 2.05       | 12.35        |

## Usage

### Run the Jupyter Notebook

1. Clone the repository:
   ```bash
   git clone https://github.com/username/uber-trip-data-analysis.git
   
2. Install the necessary dependencies::
   ```bash
   pip install -r requirements.txt
   
3. Open the Jupyter Notebook:
   ```bash
   jupyter notebook
   
4. Run the notebook to perform data processing and visualize the star schema in action.

