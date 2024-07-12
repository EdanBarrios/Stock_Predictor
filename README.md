
## Data Preparation

- **Data Source:** The historical data for the S&P 500 index is fetched using the `yfinance` library.
- **Preprocessing:** The data includes columns such as `Open`, `High`, `Low`, `Close`, and `Volume`. We calculate the `Target` variable, which indicates whether the next day's closing price is higher than the current day's.

## Model Training

- **Model:** We use a `RandomForestClassifier` from the `scikit-learn` library.
- **Initial Parameters:** The initial model is trained with 100 estimators and a minimum sample split of 100.

## Hyperparameter Tuning

We use Grid Search to find the best hyperparameters for the Random Forest model. The parameters tuned include:
- Number of estimators (`n_estimators`)
- Minimum samples required to split an internal node (`min_samples_split`)
- Maximum depth of the tree (`max_depth`)

## Feature Engineering

- **Rolling Averages:** Calculated for different horizons (e.g., 2, 5, 60, 250, 1000 days).
- **Trend Indicators:** Calculated based on the sum of the target variable over different horizons.

## Prediction and Evaluation

- **Prediction Function:** Uses the trained model to predict the next day's closing price.
- **Evaluation Metric:** Precision score is used to evaluate the model's performance.

## Results

The model's precision score and the distribution of predictions are displayed in the notebook. The best parameters found through Grid Search are used to retrain the model and improve accuracy.

