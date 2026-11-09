# Retail Sales-Forecasting and inventory optimisation
README.md
Retail Sales Forecasting and Inventory Optimization Using ARIMA, Prophet, and LSTM
Project Overview

This project develops and compares multiple time series forecasting models to predict retail sales demand and support inventory optimization decisions. The study utilizes historical retail sales data together with transaction records, store information, holiday events, and oil price data to identify sales patterns, forecast future demand, and generate inventory recommendations.

Three forecasting models were evaluated:

AutoRegressive Integrated Moving Average (ARIMA)
Prophet
Long Short-Term Memory (LSTM)

The best-performing model was subsequently used to generate future sales forecasts and support inventory optimization through safety stock and reorder point calculations.

#### Background Information

Accurate sales forecasting plays a critical role in retail operations by supporting inventory management, demand planning, resource allocation, and strategic decision-making. Retail sales are influenced by several factors including promotional campaigns, holidays, customer purchasing behavior, store characteristics, and economic conditions, making demand prediction a challenging task.

Poor forecasting can result in stockouts, excess inventory, increased operational costs, and reduced customer satisfaction. Recent advances in machine learning and deep learning have enabled organizations to develop more sophisticated models capable of capturing complex sales patterns. This project uses historical retail sales data alongside transaction, holiday, store, and oil price information to develop forecasting models and support inventory optimization through data-driven decision-making.

#### Problem Statement

Retail businesses operate in dynamic environments characterized by seasonal fluctuations, promotional activities, changing customer preferences, and economic uncertainty. These factors make accurate sales forecasting difficult and often lead to poor inventory management decisions.

Traditional forecasting techniques such as ARIMA may struggle to capture complex nonlinear sales patterns present in retail environments. Although newer approaches such as Prophet and Long Short-Term Memory (LSTM) networks have demonstrated strong forecasting capabilities, their effectiveness in retail sales forecasting requires further investigation.

Therefore, this study seeks to compare ARIMA, Prophet, and LSTM models in forecasting retail sales demand and utilize the resulting forecasts to support inventory optimization through safety stock and reorder point calculations.

### Objectives
General Objective

To develop and compare ARIMA, Prophet, and LSTM models for retail sales forecasting and utilize the best-performing model to support inventory optimization.

###### Specific Objectives
To preprocess and integrate retail sales, transaction, store, holiday, and oil price datasets for forecasting analysis.
To explore and analyze historical sales trends, seasonality, and demand patterns.
To develop ARIMA, Prophet, and LSTM forecasting models.
To evaluate model performance using MAE, RMSE, and R² metrics.
To identify the best-performing forecasting model.
To forecast future retail sales demand.
To determine safety stock and reorder point levels for inventory optimization.
To provide recommendations that support effective inventory management and demand planning.
## Dataset Description

The project uses the Store Sales Time Series Forecasting dataset.

Dataset	Descriptiontrain.csv	Historical sales records and promotions
stores.csv	Store characteristics and locations
transactions.csv	Daily customer transactions
oil.csv	Daily oil prices
holidays_events.csv	Holiday and special event information
Project Workflow
Phase 1: Data Preprocessing
Missing Values

The oil.csv dataset contained 43 missing observations in the oil price variable (dcoilwtico).

Missing values were handled using:

.ffill()
.bfill()


to preserve temporal continuity.

After merging datasets, missing transaction records were identified and imputed using median values.

df["transactions"] = df["transactions"].fillna(
    df["transactions"].median()
)

Duplicate Detection

Duplicate records were checked across all datasets before merging.

train.duplicated().sum()
oil.duplicated().sum()
stores.duplicated().sum()
transactions.duplicated().sum()
holiday.duplicated().sum()

Dataset Integration

The datasets were merged using:

store_nbr
date
date + store_nbr

This produced a unified analytical dataset containing:

Sales
Promotions
Transactions
Store Characteristics
Oil Prices
Holiday Information
Phase 2: Exploratory Data Analysis (EDA)

The following analyses were performed:

Sales Distribution Analysis
Histogram
Boxplot
Outlier Detection
Findings
Highly positively skewed sales distribution.
Presence of multiple sales spikes.
Significant sales variability across observations.
Trend Analysis
Daily Sales Trend
Monthly Sales Trend
Yearly Sales Trend
30-Day Moving Average
Findings
Sustained business growth between 2013 and 2017.
Strong seasonality throughout the year.
Increased sales during holiday periods.
Store Performance Analysis

Identified top-performing stores based on total sales.

Findings
Store 44 generated the highest total sales.
Significant variation exists between store locations.
Product Family Analysis

Examined sales contribution by product category.

Findings

Highest performing categories:

Grocery
Beverages
Produce

Lowest performing categories:

Frozen Foods
Prepared Foods
Liquor, Wine and Beer
Promotion Analysis

Evaluated promotional impact on sales.

Findings

Promotions demonstrated a positive influence on sales performance and demand generation.

Holiday Analysis

Compared sales during holiday and non-holiday periods.

Findings

Sales were generally higher during holidays.

Correlation Analysis

Major findings:

Variable	Correlation with SalesOn Promotion	0.43
Transactions	0.22
Oil Prices	-0.07

Promotions exhibited the strongest relationship with sales performance.

Phase 3: Feature Engineering

Several time-series features were created.

Time Features
year
month
quarter
day
dayofweek
weekofyear
is_weekend

Lag Features
lag_1
lag_7
lag_30

Rolling Features
rolling_mean_7
rolling_mean_30


These features were designed to capture trend, seasonality, and temporal dependencies.

Phase 4: Forecasting Models
1. ARIMA

ARIMA was implemented as the baseline statistical model.

Results
Metric	ValueMAE	143,276
RMSE	187,473
R²	-0.0197
Interpretation

ARIMA produced the weakest performance and struggled to capture complex sales dynamics.

2. Prophet

Prophet was implemented to model trend and seasonality.

Results
Metric	ValueMAE	134,705
RMSE	172,880
R²	0.1328
Interpretation

Prophet outperformed ARIMA but was less effective than LSTM.

3. LSTM

A deep learning model based on Long Short-Term Memory networks.

Architecture
LSTM(100)
Dropout(0.2)

LSTM(100)
Dropout(0.2)

Dense(1)

Results
Metric	ValueMAE	92,942
RMSE	135,511
R²	0.4653
Interpretation

LSTM achieved the highest forecasting accuracy, demonstrating its ability to learn nonlinear sales patterns and temporal dependencies.

Model Comparison
Model	MAE	RMSE	R²ARIMA	143,276	187,473	-0.0197
Prophet	134,705	172,880	0.1328
LSTM	92,942	135,511	0.4653
Best Model

✅ LSTM

Hyperparameter Tuning

The following hyperparameters were evaluated:

LSTM Units
50
100
150
200

Dropout Rate
0.1
0.2
0.3
0.4

Epochs
20
50
100

Batch Size
16
32
64

Findings
50 epochs produced the best performance.
Batch size of 32 produced the highest R².
Lower dropout rates generally performed better.
None of the tuned configurations outperformed the original LSTM architecture.
Sales Forecasting

The final LSTM model was retrained using the complete historical dataset.

A 24-month forecast was generated.

Forecast Findings

Historical sales showed continuous growth between 2013 and 2017.

The forecast initially followed historical trends but declined significantly afterward due to forecast drift, a known limitation of recursive multi-step forecasting.

Inventory Optimization

Forecasted sales were used to determine inventory control parameters.

Results
Metric	ValueAverage Demand	629,892
Safety Stock	422,097
Reorder Point	4,831,344
Interpretation

The business is expected to sell approximately 629,892 units during the forecast period.

An additional 422,097 units should be maintained as safety stock to handle uncertainty and demand fluctuations.

When inventory levels fall to approximately 4.83 million units, replenishment orders should be initiated to avoid stock shortages.

Technologies Used
Python
Pandas
NumPy
Matplotlib
Seaborn
Scikit-learn
Statsmodels
Prophet
TensorFlow/Keras
Key Findings
Sales exhibit strong seasonality and upward trends.
Promotions positively influence sales demand.
Holiday periods generate increased sales activity.
LSTM outperformed ARIMA and Prophet.
Inventory optimization provides actionable reorder thresholds.
Deep learning techniques demonstrate strong potential for retail sales forecasting.
Recommendations
Adopt LSTM-based forecasting for demand planning.
Incorporate promotional and holiday information into forecasting workflows.
Utilize safety stock and reorder point calculations for inventory management.
Regularly retrain forecasting models using newly available sales data.
Monitor forecast drift when generating long-term forecasts.
Future Work

Future studies may:

Explore Temporal Fusion Transformers (TFT).
Incorporate weather and economic indicators.
Integrate customer behavior information.
Develop real-time forecasting dashboards using Streamlit.


Grace Obonyo

Retail Sales Forecasting and Inventory Optimization Using ARIMA, Prophet, and LSTM

README.md
Retail Sales Forecasting and Inventory Optimization Using ARIMA, Prophet, and LSTM
Project Overview

This project develops and compares multiple time series forecasting models to predict retail sales demand and support inventory optimization decisions. The study utilizes historical retail sales data together with transaction records, store information, holiday events, and oil price data to identify sales patterns, forecast future demand, and generate inventory recommendations.

Three forecasting models were evaluated:

AutoRegressive Integrated Moving Average (ARIMA)
Prophet
Long Short-Term Memory (LSTM)

The best-performing model was subsequently used to generate future sales forecasts and support inventory optimization through safety stock and reorder point calculations.

Background Information

Accurate sales forecasting plays a critical role in retail operations by supporting inventory management, demand planning, resource allocation, and strategic decision-making. Retail sales are influenced by several factors including promotional campaigns, holidays, customer purchasing behavior, store characteristics, and economic conditions, making demand prediction a challenging task.

Poor forecasting can result in stockouts, excess inventory, increased operational costs, and reduced customer satisfaction. Recent advances in machine learning and deep learning have enabled organizations to develop more sophisticated models capable of capturing complex sales patterns. This project uses historical retail sales data alongside transaction, holiday, store, and oil price information to develop forecasting models and support inventory optimization through data-driven decision-making.

Problem Statement

Retail businesses operate in dynamic environments characterized by seasonal fluctuations, promotional activities, changing customer preferences, and economic uncertainty. These factors make accurate sales forecasting difficult and often lead to poor inventory management decisions.

Traditional forecasting techniques such as ARIMA may struggle to capture complex nonlinear sales patterns present in retail environments. Although newer approaches such as Prophet and Long Short-Term Memory (LSTM) networks have demonstrated strong forecasting capabilities, their effectiveness in retail sales forecasting requires further investigation.

Therefore, this study seeks to compare ARIMA, Prophet, and LSTM models in forecasting retail sales demand and utilize the resulting forecasts to support inventory optimization through safety stock and reorder point calculations.

Objectives
General Objective

To develop and compare ARIMA, Prophet, and LSTM models for retail sales forecasting and utilize the best-performing model to support inventory optimization.

Specific Objectives
To preprocess and integrate retail sales, transaction, store, holiday, and oil price datasets for forecasting analysis.
To explore and analyze historical sales trends, seasonality, and demand patterns.
To develop ARIMA, Prophet, and LSTM forecasting models.
To evaluate model performance using MAE, RMSE, and R² metrics.
To identify the best-performing forecasting model.
To forecast future retail sales demand.
To determine safety stock and reorder point levels for inventory optimization.
To provide recommendations that support effective inventory management and demand planning.
Dataset Description

The project uses the Store Sales Time Series Forecasting dataset.

Dataset	Descriptiontrain.csv	Historical sales records and promotions
stores.csv	Store characteristics and locations
transactions.csv	Daily customer transactions
oil.csv	Daily oil prices
holidays_events.csv	Holiday and special event information
Project Workflow
Phase 1: Data Preprocessing
Missing Values

The oil.csv dataset contained 43 missing observations in the oil price variable (dcoilwtico).

Missing values were handled using:

.ffill()
.bfill()


to preserve temporal continuity.

After merging datasets, missing transaction records were identified and imputed using median values.

df["transactions"] = df["transactions"].fillna(
    df["transactions"].median()
)

Duplicate Detection

Duplicate records were checked across all datasets before merging.

train.duplicated().sum()
oil.duplicated().sum()
stores.duplicated().sum()
transactions.duplicated().sum()
holiday.duplicated().sum()

Dataset Integration

The datasets were merged using:

store_nbr
date
date + store_nbr

This produced a unified analytical dataset containing:

Sales
Promotions
Transactions
Store Characteristics
Oil Prices
Holiday Information
Phase 2: Exploratory Data Analysis (EDA)

The following analyses were performed:

### Sales Distribution Analysis
Histogram
Boxplot
Outlier Detection
Findings
Highly positively skewed sales distribution.
Presence of multiple sales spikes.
Significant sales variability across observations.
##### Trend Analysis
Daily Sales Trend
Monthly Sales Trend
Yearly Sales Trend
30-Day Moving Average

###### Findings
Sustained business growth between 2013 and 2017.

Strong seasonality throughout the year.

Increased sales during holiday periods.

##### Store Performance Analysis

Identified top-performing stores based on total sales.

###### Findings
Store 44 generated the highest total sales.
Significant variation exists between store locations.
Product Family Analysis

##### Examined sales contribution by product category.

Findings

Highest performing categories:

Grocery
Beverages
Produce

Lowest performing categories:

Frozen Foods
Prepared Foods
Liquor, Wine and Beer
Promotion Analysis

Evaluated promotional impact on sales.

Findings

Promotions demonstrated a positive influence on sales performance and demand generation.

##### Holiday Analysis

Compared sales during holiday and non-holiday periods.

Findings

Sales were generally higher during holidays.

##### Correlation Analysis

Major findings:

Variable	Correlation with SalesOn Promotion	0.43
Transactions	0.22
Oil Prices	-0.07

Promotions exhibited the strongest relationship with sales performance.

## Feature Engineering

Several time-series features were created.

Time Features
year
month
quarter
day
dayofweek
weekofyear
is_weekend

Lag Features
lag_1
lag_7
lag_30

Rolling Features
rolling_mean_7
rolling_mean_30


These features were designed to capture trend, seasonality, and temporal dependencies.

## Forecasting Models
1. ARIMA

ARIMA was implemented as the baseline statistical model.

Results
Metric	ValueMAE	143,276
RMSE	187,473
R²	-0.0197
Interpretation

ARIMA produced the weakest performance and struggled to capture complex sales dynamics.

2. Prophet

Prophet was implemented to model trend and seasonality.

Results
Metric	ValueMAE	134,705
RMSE	172,880
R²	0.1328
Interpretation

Prophet outperformed ARIMA but was less effective than LSTM.

3. LSTM

A deep learning model based on Long Short-Term Memory networks.

Architecture
LSTM(100)
Dropout(0.2)

LSTM(100)
Dropout(0.2)

Dense(1)

Results
Metric	ValueMAE	92,942
RMSE	135,511
R²	0.4653
Interpretation

LSTM achieved the highest forecasting accuracy, demonstrating its ability to learn nonlinear sales patterns and temporal dependencies.

Model Comparison
Model	MAE	RMSE	R²ARIMA	143,276	187,473	-0.0197
Prophet	134,705	172,880	0.1328
LSTM	92,942	135,511	0.4653


Best Model

LSTM

## Hyperparameter Tuning

The following hyperparameters were evaluated:

LSTM Units
50
100
150
200

Dropout Rate
0.1
0.2
0.3
0.4

Epochs
20
50
100

Batch Size
16
32
64

#### Findings
50 epochs produced the best performance.

Batch size of 32 produced the highest R².

Lower dropout rates generally performed better.

None of the tuned configurations outperformed the original LSTM architecture.

## Sales Forecasting

The final LSTM model was retrained using the complete historical dataset.

A 24-month forecast was generated.

### Forecast Findings

Historical sales showed continuous growth between 2013 and 2017.

The forecast initially followed historical trends but declined significantly afterward due to forecast drift, a known limitation of recursive multi-step forecasting.

### Inventory Optimization

Forecasted sales were used to determine inventory control parameters.

Results
Metric	ValueAverage Demand	629,892
Safety Stock	422,097
Reorder Point	4,831,344
Interpretation

The business is expected to sell approximately 629,892 units during the forecast period.

An additional 422,097 units should be maintained as safety stock to handle uncertainty and demand fluctuations.

When inventory levels fall to approximately 4.83 million units, replenishment orders should be initiated to avoid stock shortages.

## Technologies Used
Python
Pandas
NumPy
Matplotlib
Seaborn
Scikit-learn
Statsmodels
Prophet
TensorFlow/Keras

## Key Findings
Sales exhibit strong seasonality and upward trends.

Promotions positively influence sales demand.

Holiday periods generate increased sales activity.

LSTM outperformed ARIMA and Prophet.
Inventory optimization provides actionable reorder thresholds.

Deep learning techniques demonstrate strong potential for retail sales forecasting.

## Recommendations
Adopt LSTM-based forecasting for demand planning.

Incorporate promotional and holiday information into forecasting workflows.

Utilize safety stock and reorder point calculations for inventory management.

Regularly retrain forecasting models using newly available sales data.

Monitor forecast drift when generating long-term forecasts.

## Future Work

Future studies may:

Explore Temporal Fusion Transformers (TFT).
Investigate N-BEATS forecasting architectures.
Incorporate weather and economic indicators.
Integrate customer behavior information.


Grace Obonyo