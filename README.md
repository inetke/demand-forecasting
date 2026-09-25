# 💊 FarmaCast — Demand Forecasting for Pharmacy Inventory Planning

> Turning real pharmacy sales data into demand forecasts to support better inventory planning.

🚀 **[Live Demo – FarmaCast](https://farmacast-demand-forecasting.streamlit.app)**

FarmaCast is an end-to-end Machine Learning project designed to forecast product demand and support inventory planning for a real pharmacy.

The project uses **117,415 real sales records from 2025**, covering more than **7,500 products**, to identify demand patterns and generate future demand forecasts.

The solution covers the complete workflow from raw operational data to a deployed forecasting application: **data cleaning, exploratory analysis, feature engineering, model comparison, hyperparameter tuning, forecasting, and interactive visualization with Streamlit**.

### 📊 Key Results

- **117,415** real sales records analyzed
- **7,500+** different products
- **CatBoost** selected as the final forecasting model
- **R² Test: 0.72**
- **RMSE Test: 4.71**
- Interactive forecasts for **1, 2, 4 and 8 weeks**
- Deployed **Streamlit application** for exploring and exporting predictions

---

## 🎯 Business Problem

The project is based on a real pharmacy in Buenos Aires, Argentina, where inventory planning relied largely on staff experience, historical sales review, and manual decision-making.

This reactive approach makes it difficult to anticipate changes in product demand and can contribute to:

- Stockouts of high-demand products
- Excess inventory and products with low turnover
- Inefficient use of working capital
- More reactive purchasing and inventory decisions

The goal of FarmaCast is to use historical sales data to **forecast future product demand**, providing a data-driven input that can support inventory and purchasing decisions.

Rather than attempting to calculate an "optimal stock" level directly, the model focuses on predicting expected demand. These forecasts can then be combined with additional business variables — such as current inventory, supplier lead times, safety stock policies, and purchasing constraints — to support inventory planning.

---

## 👩‍💻 My Contribution

This was a collaborative project developed by a team of three. My main contributions were:

- Contributed to **data cleaning and exploratory data analysis (EDA)**. Each team member explored the data independently, and the findings were later consolidated into a shared final analysis.
- Independently **experimented with and compared several Machine Learning models** during the model-selection phase, contributing to the team's evaluation of different forecasting approaches.
- Took full ownership of the **Streamlit application**, designing and developing the complete user-facing layer of the project.
- Implemented the workflow for **uploading new sales data, detecting duplicate records, updating the historical dataset, and recalculating temporal features** required for forecasting.
- Built the application's **1, 2, 4 and 8-week forecasting workflows**, including product-level predictions and broader demand views.
- Developed the **interactive visualizations and CSV export functionality**, making the forecasting results accessible and usable outside the modeling notebooks.

My primary ownership in the project was the application layer: turning the team's Machine Learning work into an interactive tool that could be used to explore forecasts and support inventory planning.

---

## 📊 Dataset

The project uses **real transactional sales data from a pharmacy in Buenos Aires, Argentina**, covering sales activity throughout 2025.

The original dataset contains:

- **117,415 sales records**
- **20 numerical and categorical variables**
- More than **7,500 unique products**
- Products across pharmaceuticals, medical supplies, supplements, personal care and related categories
- Transaction-level information including dates, quantities, prices, payment methods, product categories and sales totals

### Data Quality Challenges

Because the data comes from a real operational system, the dataset contained many of the challenges commonly found in real-world business data:

- Missing and inconsistent values
- Duplicate records
- Heterogeneous formats
- Inconsistent text and product naming
- Outliers and noisy transactional data

Before modeling, the data went through a cleaning, normalization and validation process to create a more reliable dataset for exploratory analysis and demand forecasting.

---

## ⚙️ Technical Approach

FarmaCast was developed as an end-to-end Machine Learning workflow, from raw operational data to an interactive forecasting application.

### 1. Data Ingestion & Storage

The original sales data came from a real pharmacy management system and was exported as encrypted Excel files.

The data was decrypted, converted to CSV and processed with **Python and Pandas**. A **SQLite database** was also used during the project to store and query the data using SQL.

### 2. Data Cleaning & Validation

The raw transactional data required extensive preprocessing before it could be used for analysis and modeling.

The process included:

- Handling missing and duplicate records
- Standardizing text and product names
- Converting and validating date fields
- Reviewing inconsistent values and outliers
- Creating a cleaner and more consistent analytical dataset

### 3. Exploratory Data Analysis

EDA was used to understand sales behavior and identify patterns relevant to demand forecasting.

The analysis included:

- Product sales frequency and distribution
- Temporal demand patterns
- Product and category-level behavior
- Descriptive statistics and outlier analysis
- Visual exploration of sales trends

### 4. Feature Engineering & Temporal Splitting

The cleaned data was transformed into a modeling dataset with temporal and product-level features.

Because this is a forecasting problem, the data was split **chronologically rather than randomly**, preserving the temporal order of the observations.

The modeling workflow uses separate **training, validation and test periods** so that validation can be used during model development while the test period remains reserved for evaluating performance on later observations.

### 5. Model Experimentation

Several regression algorithms were explored for the forecasting task, including:

- Random Forest
- XGBoost
- LightGBM
- CatBoost

The experiments were used to compare different approaches and understand their generalization behavior before continuing with **CatBoost** for further hyperparameter tuning and evaluation.

### 6. Application Layer

The final forecasting workflow was integrated into a **Streamlit application**, allowing users to upload recent sales data, generate forecasts, explore results visually and export predictions for further use.

---

## 📈 Model Evaluation

Several regression models were compared to evaluate their ability to generalize to later time periods.

| Model | RMSE (Test) | R² (Train) | R² (Test) |
|---|---:|---:|---:|
| Random Forest | 4.98 | 0.96 | 0.68 |
| XGBoost | 4.82 | 0.87 | 0.70 |
| LightGBM | 5.47 | 0.90 | 0.62 |
| CatBoost | 4.82 | 0.87 | 0.70 |

In the initial comparison, **XGBoost and CatBoost achieved similar test performance**, while Random Forest showed a larger gap between training and test results.

CatBoost was selected for the next stage of the project. One practical advantage was its ability to work directly with categorical features such as `product`, avoiding the need for One-Hot Encoding within the modeling pipeline.

### Hyperparameter Tuning

CatBoost was subsequently tuned using randomized hyperparameter sampling and a separate validation period for model selection and early stopping.

The best-performing configuration was then evaluated on the test period:

- **R² Train:** 0.77
- **R² Test:** 0.72
- **RMSE Test:** 4.71
- **MSE Test:** 22.15

These results indicate that the final model retained most of its predictive performance when evaluated on later observations that were not used for training.

The trained CatBoost model is saved as a reusable `.pkl` artifact and integrated into the Streamlit forecasting application.

---

## 🖥️ Streamlit Application

The forecasting workflow is deployed through an interactive **Streamlit application**, turning the Machine Learning model into a tool that can be used without interacting directly with the underlying notebooks or code.

🚀 **[Open the Live Application](https://farmacast-demand-forecasting.streamlit.app)**

### Main Features

#### 📥 Upload & Update Sales Data

Users can upload new sales data in CSV format. The application automatically:

- Cleans and normalizes the uploaded data
- Detects new and duplicate records
- Updates the historical sales dataset
- Recalculates the temporal features required by the forecasting pipeline

#### 🔮 Demand Forecasting

The application provides two forecasting modes:

**Individual Forecast**
- Select a specific product
- Generate demand forecasts for **1, 2, 4 or 8 weeks**
- Explore the expected demand through interactive visualizations

**Global Forecast**
- Explore projected demand across multiple products
- Analyze products by group or category
- Identify products with higher projected demand

#### 📊 Visualization & Export

Forecasting results can be explored through:

- Time-series visualizations
- Product and category-level views
- Comparative prediction tables
- Downloadable **CSV files** for further analysis or integration into other workflows

The application was designed to make the forecasting output easier to interpret and use as an input for inventory and purchasing decisions.
