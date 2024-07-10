# Stock_Predictor

Uses the Yahoo Finance API and Pandas dataframe to access and visualize stock market data. The stock tracked is the S&P 500 index.

The initial table made contains a date, opening/closing price, lowest/highest price, and total volume traded. The dividends and stock splits columns are deleted since they typically are only relevant to individual stocks, not an index.

A "Tomorrow" column is created by shifting the existing upcoming days' closing price data back by one day. 

A "Target" column is created with the purpose to see if tomorrow's price will be greater than today's price which is visualized as a one (increase) or zero (decrease) based on the evaluation of a boolean statement.

The inital ML model deployed is a RandomForestClassifier. This model trains individual decision trees with randomized parameters and averaging the results. This model makes it more resitant to overfitting than other models, runs quickly, and are good at picking up non-linear relationships in data (ideal for stock predictions).

Parameters for model:
    - The higher the "number of estimators" makes it more accurate up to a certain point. 

    - The "minimum sample split" has a tradeoff that makes the model less accurate the higher it is while also making it less likely to overfit.

    - The "random state" is set to one so that the random numbers generated are in a predictable sequence which is good for observing effects of changes made to model as it removes the possibility for external factor influence.

Data is split into a training and testing set since cross-validation with a set of time series data will result in leakage from future data which will affect the predictor's real life accuracy since it relies on future knowledge.

Initially, all but the last hundred rows are put into the training set. The last hundred rows are put into the test set.

The opening/closing price, volume, and high/low price columns are used as predictors to train and fit the model. 

A precision score module is imported to measure accuracy of model. Predictions are then generated using our test set and predictors. This is originally a Numpy set which is converted to a Pandas set. 

In order to plot the data we concatenate the test target and predicted values to visualize the difference between the model's predictions and actual stock behavior.

A prediction function is created that fits the model using training vectors and target. It then models predictions using our predictors before combining everything together. 

A backtest option is created using the stock data, model data, predictors, start, and step size. The start parameter tells the function how many days worth of data to use initially. The step size allows you to get a prediction for every step of the series that increases by the amount set by user. 

Each succeeding year uses the data set of all previous years as time goes on which makes it more accurate as the amount of data grows with each year.