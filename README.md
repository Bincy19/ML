# ML
This study forecasts solar electricity generation in Swedish homes using weather data- temperature, precipitation, snow depth and sunshine. Linear Regression, XGBoost and Random Forest are evaluated. Results show that Random Forest provides the best predictive performance, supporting efficient energy management and renewable energy integration.
# Weather and Sunshine Prediction Using Machine Learning

## Overview

This project explores the use of machine learning techniques to analyze and predict weather-related variables using meteorological data from the Swedish Meteorological and Hydrological Institute (SMHI).

The project focuses on weather stations located in the Swedish electricity price zone **SE3** and uses historical weather observations from 2022 onward.

Several machine learning approaches are explored, including:

* Random Forest Regression
* XGBoost
* Logistic Regression

The project also includes a data collection and preprocessing pipeline for obtaining weather observations from the SMHI Open Data API.

---

## Project Objectives

The main objectives of the project are:

1. Collect historical weather data from SMHI.
2. Select relevant weather stations based on their geographical location.
3. Restrict the analysis to the Swedish electricity zone SE3.
4. Prepare and clean the collected weather data.
5. Aggregate sunshine observations into daily values.
6. Train machine learning models using weather-station data.
7. Predict weather-related variables for stations.
8. Explore sunshine-related classification and prediction.

---

## Data Source

The weather data is collected from the **Swedish Meteorological and Hydrological Institute (SMHI)** Open Data API.

The project uses the following SMHI parameters:

| Parameter | Description     | Frequency  |
| --------- | --------------- | ---------- |
| 2         | Air temperature | Daily mean |
| 5         | Precipitation   | Daily sum  |
| 8         | Snow depth      | Daily      |
| 10        | Sunshine time   | Hourly     |

The data is restricted to observations starting from **2022-01-01** so that the weather data period can be aligned with the project data.

SMHI Open Data API documentation:

https://opendata.smhi.se/apidocs/

---

## Project Workflow

The project consists of three main stages.

### 1. Data Collection

The `get_smhi_data_.ipynb` notebook:

* Connects to the SMHI Open Data API.
* Retrieves available weather stations.
* Retrieves station latitude and longitude.
* Determines the electricity zone of each station.
* Keeps stations located in SE3.
* Downloads weather observations for the selected stations.
* Processes the downloaded CSV files.
* Keeps data from 2022 onward.

### 2. Sunshine Analysis

The `sunshine.ipynb` notebook explores sunshine observations.

The notebook:

* Loads sunshine observations.
* Converts date and time information into datetime values.
* Performs exploratory data analysis.
* Calculates daily average sunshine values.
* Handles class imbalance using `RandomOverSampler`.
* Creates temporal features such as weekday, month, quarter and day of year.
* Uses Logistic Regression for sunshine-quality classification.
* Uses XGBoost-based regression for further prediction experiments.
* Evaluates predictions using MAE, MSE, RMSE and R².

### 3. Random Forest Prediction

The `Random forest.ipynb` notebook trains separate Random Forest regression models for:

* Air temperature
* Precipitation
* Snow depth
* Sunshine duration

The models use:

* Day of year
* Latitude
* Longitude

as input features.

The notebook also generates station-level predictions for the following day and saves the results to a CSV file.

---

## Machine Learning Models

### Random Forest Regression

Random Forest Regression is used to predict several weather variables independently.

Four Random Forest models are trained:

```text
Air Temperature
Precipitation
Snow Depth
Sunshine Duration
```

Each model uses 100 decision trees with a fixed random state.

---

### Logistic Regression

Logistic Regression is used in the sunshine analysis to classify the `Quality` variable.

The classification features include:

* Sunshine duration
* Weekday
* Next-day sunshine intensity

The quality values are converted into binary labels for classification.

---

### XGBoost

The sunshine notebook also experiments with an XGBoost-based regression model.

Temporal features are extracted from the date, including:

* Weekday
* Quarter
* Month
* Day of month
* Year
* Day of year
* Sine of day of year
* Cosine of day of year

Hyperparameter tuning is also explored using `GridSearchCV`.

---

## Model Evaluation

The notebooks use several standard regression/classification evaluation metrics, including:

* Mean Absolute Error (MAE)
* Mean Squared Error (MSE)
* Root Mean Squared Error (RMSE)
* R² score

The notebooks also contain plots comparing actual and predicted values.

---

## Repository Structure

```text
.
├── README.md
│
├── code/
│   ├── XGBoost and Linear/
│   │   ├── README.md
│   │   └── sunshine.ipynb
│   │
│   ├── Random forest/
│   │   ├── README.md
│   │   └── Random forest.ipynb
│   │
│   └── ws1/
│       └── wettersol/
│           ├── README.md
│           └── get_smhi_data_.ipynb
```

---

## Technologies Used

The project is implemented in Python using Jupyter Notebooks.

Main libraries include:

* Python
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Scikit-learn
* XGBoost
* imbalanced-learn
* Requests
* Pathlib

---

## Installation

Install the main dependencies using pip:

```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost imbalanced-learn requests jupyter
```

Then start Jupyter Notebook:

```bash
jupyter notebook
```

Open the required notebook from the repository.

---

## Running the Project

A recommended execution order is:

### Step 1 — Download and prepare SMHI data

Run:

```text
code/ws1/wettersol/get_smhi_data_.ipynb
```

This downloads and processes the required SMHI weather data.

### Step 2 — Run the Random Forest models

Run:

```text
code/Random forest/Random forest.ipynb
```

This trains Random Forest models for the weather variables and generates station-level predictions.

### Step 3 — Run the sunshine/XGBoost analysis

Run:

```text
code/XGBoost and Linear/sunshine.ipynb
```

This performs sunshine data analysis and experiments with Logistic Regression and XGBoost.

---

## Output

The prediction workflow produces station-level prediction data containing variables such as:

```text
StationNumber
Date
Average_AirTemperature
Average_Precipitation
Average_SnowDepth
Average_Sunshine(Minutes)
```

The notebooks also generate visualizations for predicted weather and sunshine values.

---

## Notes

The notebooks were originally developed using local file paths. Before running them on another computer, update the paths used to load and save the datasets.

For example, paths such as:

```text
D:\user\MachineLearning\...
```

should be replaced with paths appropriate for the local environment.

Similarly, the sunshine notebook expects the sunshine dataset to be available at the path specified in the notebook.

---

## Data and Reproducibility

The project relies on external SMHI weather data. The data-download notebook can be used to retrieve the required observations from SMHI.

Because SMHI data and API responses may change over time, results may not be identical when the notebooks are executed at a later date.

---

## Author

Machine Learning project focused on weather and sunshine prediction using Swedish meteorological station data.
