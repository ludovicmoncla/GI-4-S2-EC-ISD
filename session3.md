## Session 3 - Regression & Forecasting

* Date: February 11, 2026, 14:00 - 18:00
* Room: Flash Gordon

### Objectives:

Transition from historical analysis to proactive management. You will build a machine learning model to predict bike availability, allowing the system to anticipate "stockouts" (empty stations) or "overflows" (full stations).

**The Industrial Engineering perspective**: This is Predictive Maintenance for service levels. In supply chain and flow management, being reactive is expensive. If your model predicts with 90% certainty that a station will be empty by 17:00, you can trigger a "preventive" replenishment. This optimizes the service level and ensures customer satisfaction.


Follow the steps below to develop your forecasting model:


#### 1. Problem Definition & Data Preparation

Define your features (`X`) and your target (`y`) for a supervised learning approach:

* Target or output variable (`y`): 
    * Number of bikes available at Station N in T + 1 hour.

* Explanatory or input variables (`X`): 
    * Current availability.
    * Temporal features.
    * Weather data.
    * Station metadata.


#### 2. Machine Learning Modeling

Compare different approaches to handle the complexity of urban mobility:

* **Baseline Model**: Start with a Simple [Linear Regression](https://scikit-learn.org/stable/modules/generated/sklearn.linear_model.LinearRegression.html#sklearn.linear_model.LinearRegression)
* **Advanced Models**: Implement [Random Forest Regressor](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.RandomForestRegressor.html#sklearn.ensemble.RandomForestRegressor) or [Gradient Boosting](https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.HistGradientBoostingRegressor.html#sklearn.ensemble.HistGradientBoostingRegressor).
    * These models capture non-linear relationships. For example, the impact of rain isn't always proportional; a light drizzle might not change behavior, but a heavy downpour stops rentals entirely.


#### 3. Evaluation & Error Analysis


In Machine Learning, we usually train and evaluate on separate sets. So ensure that the model hasn't seen evaluation data during training. This simulates real-world performance. In most cases, the [train/test split](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.train_test_split.html) is done randomly, but for time series data, we must [split chronologically](https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.TimeSeriesSplit.html) to avoid "data leakage" (where future information influences the model). For instance, you might train on data from January to November and test on December.

* Metrics: Calculate the Root Mean Square Error (RMSE) and Mean Absolute Error (MAE) to quantify your prediction gaps.

Traditionnaly, we use metrics like RMSE and MAE to quantify the average prediction error. But beyond numbers, understanding which features drive the model's predictions is crucial for operational insights. For instance, if "Hour of Day" is the most important feature, it confirms the expected daily patterns. If "Rain" is significant, it validates the need for weather-aware logistics.

* Feature Importance: Extract which variables drive the model. Does the "Hour of Day" outweigh "Rain" in Lyon?

> See: https://scikit-learn.org/stable/auto_examples/ensemble/plot_forest_importances.html

* Performance Visualization: Plot a "Prediction vs. Reality" time-series graph for a specific station over a 7-day test period.


**Once the 3 first steps are fully complete, more advanced steps will be released.**

#### 4. Hyperparameter Tuning

#### 5. Advanced Feature Engineering (Temporal "Memory")

#### 6. Multi-Step Forecasting


### Resources & Documentation

* Machine Learning Fundamentals:

    * Scikit-Learn Regression Guide: https://www.datacamp.com/tutorial/sklearn-linear-regression
    * A Gentle Introduction to Gradient Boosting: https://machinelearningmastery.com/gentle-introduction-gradient-boosting-algorithm-machine-learning/

* Feature Engineering for Time Series:

    * https://scikit-learn.org/stable/auto_examples/applications/plot_cyclical_feature_engineering.html

* Evaluation:
    * Understanding RMSE and MAE: https://towardsdatascience.com/what-are-rmse-and-mae-e405ce230383/



### Submission

- A Jupyter notebook documenting the preprocessing, model training and evaluation steps.
* Submission link: [Moodle](https://moodle.insa-lyon.fr/course/view.php?id=10022)
