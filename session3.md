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



#### 4. Hyperparameter Tuning

Default models (like a standard Random Forest) are rarely optimal for specific problems. To improve accuracy without changing the data, you must tune the model's internal settings (hyperparameters).

* **Grid Search** or **Random Search**: Use `GridSearchCV` or `RandomizedSearchCV` from Scikit-Learn to test different combinations of parameters.

    * For Random Forest: Try varying `n_estimators` (number of trees), `max_depth` (complexity of trees), and `min_samples_split`.

* **Regularization**: If your model works perfectly on training data but fails on testing data (overfitting), increase constraints (e.g., limit `max_depth`).


#### 5. Advanced Feature Engineering (Temporal "Memory")

The current availability is useful, but the trend of that availability is even more powerful. In time-series forecasting, we often use Lag Features and Rolling Statistics to give the model "memory."

* **Lag Features**: Include the number of bikes available 1 hour ago (t−1), 2 hours ago (t−2), and 24 hours ago (t−24). This helps the model understand if the station is currently emptying or filling up.
Concept: If a station is empty now, but was full 1 hour ago, it is experiencing a "shock." If it was empty 1 hour ago too, it is in a stable state.

* **Rolling Statistics**: Calculate the moving average or standard deviation of the last 3 hours.

    * $RollingMean=\frac{1}{3} \sum_{i=1}^{3} y_{t-i}$


> The Industrial Engineering perspective: This is analogous to "derivative control". You aren't just looking at the current error (current stock); you are looking at the rate of change to dampen the system response.



#### 6. Multi-Step Forecasting

Predicting T+1 (1 hour ahead) is good, but logistical operations (trucks) are slow. They need more lead time. A truck cannot teleport to a station instantly.

* **Expand the Horizon**: Train a model to predict availability at T+3 or T+4 hours.

* **Strategy**: Compare a Direct Strategy (training separate models for each future hour) vs. a Recursive Strategy (using the prediction of T+1 as an input to predict T+2).

> The Industrial Engineering perspective: This defines your "Reaction Window." If your lead time to dispatch a truck is 2 hours, a T+1 prediction is useless for reactive maintenance—it's too late. You need a T+3 forecast to trigger an effective intervention.


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
