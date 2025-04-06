# Car Purchase AI Webapp

[Live Demo](https://entzyeung.github.io/car-purchase-ai/index.html)

## Overview

This webapp helps users evaluate the quality of a used car based on its price, maintenance costs, and physical features. Using machine learning models, it rates a car as **Unacceptable**, **Acceptable**, **Good**, or **Very Good**, assisting users in making smarter buying decisions. The app is built with Python, HTML, PyScript, and Bootstrap, providing an interactive interface to train models and get AI recommendations.

I originally built the machine learning models in 2020 and developed the webapp, then converted it from a Flask-based front-end and back-end to PyScript in 2022. At that time, PyScript was still experimental and not yet officially published, making this project an early exploration of running Python in the browser. Additionally, models like XGBoost were a big hit back then, reflecting the data science trends of the era. I’m now revisiting and fixing this old, broken app in 2025 to preserve this piece of my data science journey—I don’t want to let it go to waste and want to keep it as a historical milestone of my growth as a data scientist.

## What Does This App Do?

The app uses machine learning to assess a used car’s quality based on six parameters:
- **Buying Price**: The cost to purchase the car.
- **Annual Maintenance Cost**: The estimated yearly maintenance expense.
- **Number of Doors**: The car’s door count (2, 3, 4, or 5+).
- **Number of Persons**: The car’s seating capacity (2, 4, or more than 6).
- **Luggage Space**: The trunk capacity (Small, Medium, or Large).
- **Safety**: The safety features (Low, Medium, or High, based on airbag presence).

It employs two models—Logistic Regression (default settings) and Gradient Boosting (optimized with `n_estimators=100`, `max_depth=4`)—to predict a quality rating, helping users decide if a car is worth considering.

## Data Source

The data comes from the [Car Evaluation Dataset](https://archive.ics.uci.edu/ml/datasets/Car+Evaluation) from the UCI Machine Learning Repository, collected in the 1990s. It contains 1,728 instances with the six features mentioned above and a target variable (`score`) that rates cars as `unacc` (unacceptable), `acc` (acceptable), `good`, or `vgood` (very good). Since the data is from the 1990s, the price and maintenance cost categories (`low`, `med`, `high`, `vhigh`) may not align perfectly with today’s market, but I’ve mapped them to approximate British Pounds (£) for better user understanding.

## Conversion to Pounds

The original dataset uses categorical values (`vhigh`, `high`, `med`, `low`) for buying price and maintenance cost. To make these more relatable, I mapped them to approximate ranges in British Pounds (£) based on the 2025 UK used car market:
- **Buying Price**:
  - `vhigh` → > £15,000
  - `high` → £10,000 - £15,000
  - `med` → £5,000 - £10,000
  - `low` → < £5,000
- **Annual Maintenance Cost**:
  - `vhigh` → > £2,000
  - `high` → £1,000 - £2,000
  - `med` → £500 - £1,000
  - `low` → < £500

These ranges are approximate and reflect typical used car prices and maintenance costs in the UK as of 2025, adjusted for inflation and market trends since the 1990s.

## How to Use the App

1. **Train the Model**:
   - Navigate to the "Train Your Model" section.
   - Choose a model type: Logistic Regression or Gradient Boosting.
   - Select a test size (between 0.1 and 0.5) to split the dataset for training and testing.
   - Click "Start Training" to train the model. A spinner will indicate the process, and a summary (accuracy and F1 score) will display once completed.

2. **Get AI Recommendation**:
   - Go to the "Get AI Recommendation" section.
   - Use the dropdowns to input your car’s parameters (default values are provided for convenience).
   - Click "Ask AI" (enabled after training) to get a quality rating.

## Interpreting the Results

The app outputs a quality rating for the car:
- **Unacceptable**: The car may have high costs or poor features (e.g., low safety, limited capacity).
- **Acceptable**: The car is decent but not outstanding.
- **Good**: The car offers a good balance of cost and features.
- **Very Good**: The car is highly desirable with low costs and excellent features.

A brief explanation accompanies the rating, highlighting factors like cost, safety, or capacity that influenced the result. Use this rating to gauge if the car meets your needs and preferences.

## Technical Details

- **Models Used**:
  - **Logistic Regression**: Default settings from scikit-learn.
  - **Gradient Boosting**: Optimized with `GradientBoostingClassifier(n_estimators=100, max_depth=4)`.

- **Other Models Explored**:
  I trained two additional models—XGBoost and LightGBM—in 2020, optimizing them by tuning the number of iterations and max depth. However, at the time of deployment in 2022, PyScript did not support XGBoost or LightGBM libraries, so I had to drop them.

- **Development Journey**:
  I built the machine learning models in 2020 and developed the webapp, initially using Flask for the front-end and back-end. In 2022, I converted it to PyScript, which was still experimental and not yet officially published, making this project a pioneering effort in browser-based Python applications. At that time, XGBoost was a popular model in the data science community, reflecting the trends of the era. I’m now updating this app in 2025 to fix issues and preserve this piece of my data science history, as I don’t want to let this early work go to waste.

## Remarks

Since the data originates from the 1990s, the price and maintenance cost categories may feel outdated. The £ mappings are approximate and adjusted for 2025 UK market conditions, but they still reflect the dataset’s original categorical structure. For more accurate modern predictions, a newer dataset with numerical prices and additional features (e.g., mileage, year) would be ideal, but this app serves as a functional proof-of-concept and a nostalgic milestone in my data science journey.