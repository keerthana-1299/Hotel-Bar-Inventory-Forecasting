# Hotel Bar Inventory Demand Forecasting

## Project Overview

This project develops a data-driven inventory forecasting and replenishment approach for a hotel bar chain.

The objective is to forecast item-level demand, recommend inventory par levels, and simulate an inventory replenishment policy to help reduce stockouts while maintaining appropriate inventory levels.

## Business Problem

Hotel bars can face two major inventory challenges:

- Stockouts of high-demand products can affect guest satisfaction, revenue, and service quality.
- Overstocking slow-moving products can increase working capital, storage requirements, and the risk of waste or spoilage.

This project uses historical bar inventory transaction data to develop a forecasting and inventory planning approach.

## Objectives

- Clean and validate historical inventory transaction data.
- Aggregate consumption into daily demand by bar and brand.
- Analyze demand patterns and potential stockout events.
- Forecast future demand for individual bar-brand combinations.
- Calculate recommended inventory par levels using demand variability and safety stock.
- Simulate the proposed inventory replenishment policy.
- Identify bar-brand combinations with higher simulated stockout risk.

## Dataset

The dataset contains historical inventory transactions with information including:

- Date and time served
- Bar name
- Alcohol type
- Brand name
- Opening inventory balance
- Purchases
- Consumption
- Closing inventory balance

The analysis covers 6 bars and 16 brands, resulting in 96 bar-brand combinations for inventory simulation.

## Methodology

### 1. Data Cleaning and Validation

- Converted date/time fields into appropriate formats.
- Checked missing values and data types.
- Validated the inventory conservation relationship:

`Opening Balance + Purchase - Consumed = Closing Balance`

### 2. Exploratory Data Analysis

The analysis includes:

- Brand-level consumption
- Bar-level consumption
- Day-of-week demand patterns
- ABC-style demand classification
- Historical stockout indicators

### 3. Demand Forecasting

A chronological train-test split was used to avoid data leakage.

Two approaches were evaluated:

- 7-day rolling mean baseline
- Random Forest regression using lag, rolling statistics, calendar, and weekend features

Performance was evaluated using:

- MAE
- RMSE
- WAPE

### 4. Inventory Optimization

Recommended par levels were calculated using:

- Estimated daily demand
- Supplier lead time
- Demand variability
- Safety stock
- 95% service-level factor

The current simulation assumes a 2-day supplier lead time.

### 5. Inventory Simulation

The simulated policy:

1. Starts with the recommended inventory level.
2. Deducts daily consumption.
3. Places a replenishment order when inventory falls below the required level.
4. Receives orders after the assumed lead time.
5. Tracks stockout days, lost volume, average inventory, and order count.

## Key Results

The analysis produced:

- Demand forecasts for individual bar-brand combinations.
- Recommended par levels for inventory planning.
- Simulation results across 96 bar-brand combinations.
- Identification of combinations with higher simulated stockout days and lost volume.

## Project Structure

```text
Hotel-Bar-Inventory-Forecasting/
│
├── data/
│   └── Consumption Dataset - Dataset.csv
│
├── notebooks/
│   └── hotel_bar_inventory_forecasting_solution.ipynb
│
└── README.md


Technologies Used
Python
Pandas
NumPy
Matplotlib
Scikit-learn
Jupyter Notebook
Random Forest
Time-Series Forecasting
Inventory Optimization
Limitations and Future Improvements

The current approach assumes a constant supplier lead time and primarily uses historical consumption as the demand signal.

Future improvements could include:

Variable supplier lead times
Holiday and seasonal effects
Promotions and special events
Real-time POS data
Waste, breakage, and spillage tracking
Advanced forecasting models
Production monitoring and forecast drift detection
Author

Keerthana Seelam

Computer Science and Engineering
