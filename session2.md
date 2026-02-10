## Session 2 - Clustering & Segmentation

* Date: February 10, 2026, 8:00 - 12:00
* Room: Flash Gordon

### Objectives:

Move from data exploration to strategic segmentation. By identifying recurring patterns in station behavior, you will define "profile types" to optimize the system's rebalancing strategy.

**The Industrial Engineering perspective**: Efficient logistics requires categorization. You cannot manage 400+ stations individually. By clustering stations with similar demand profiles, you can design specialized logistics routes, predict stockouts, and optimize the deployment of regulation trucks for nighttime rebalancing.


Follow the steps below to build your segmentation model:


#### 1. Feature Engineering (Aggregated Descriptors)

To cluster the stations, you must first characterize their "behavior." For each station, calculate the following indicators:


* **Daily Volume**: Average total departures and arrivals per day.
* **Commuter Dynamics**: Average bike  or arrivals during Morning Rush vs. Evening Rush.
* **Weekly Rhythm**: Ratio of average departures or arrivals on Weekends vs. Weekdays.
* **Day of week patterns**: Average departures or arrivals for each day of the week (Monday to Sunday).

> Pro tip: Use `groupby` and `pivot` methods in Pandas to compute these aggregated features efficiently.


#### 2. Unsupervised Learning: K-Means Clustering

Once you have your feature set, it's time to apply clustering algorithms to identify natural groupings among the stations based on their usage patterns. Unsupervised learning or clustering is a powerful technique to discover hidden structures in data without predefined labels. It allows us to segment the stations into distinct groups based on their behavior, which can inform targeted operational strategies.

    - Experiment the [K-Means algorithm](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html#sklearn.cluster.KMeans) to group similar stations together. Try with different values of k (number of clusters): 2, 3, 4, etc.

> Use the [Scikit-Learn library](https://scikit-learn.org/stable/) for K-Means clustering.

- **Standardization**: As clustering works with distance metrics, it is important to scale your features (e.g., using [StandardScaler](https://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.StandardScaler.html)) so that distance-based metrics aren't biased by different units.

- **Optimization**: Use the Elbow Method (Within-Cluster Sum of Square) to determine the optimal number of clusters (k).


#### 3. Spatial Visualization

- Project your clusters onto an interactive map of Lyon using different colors for each group.
- Goal: Does the data reveal the urban structure? Observe the spatial distribution of "Work" clusters vs. "Residential" clusters across the Lyon metropolis.


#### 4. Cluster Profiling & Interpretation

Clustering is useless if we doesn't know what "Cluster 1" actually means. After running K-Means, you need to "humanize" the groups.

* **Cluster Centers**: Extract the cluster centers (the "average station" for each group) and analyze their feature values to understand the typical behavior of stations in each cluster.

* **Cluster Visualization**: Create visualizations (e.g., bar charts, scatter plots) to compare the feature values across clusters.

* **Radar Charts**: Create radar (spider) charts for each cluster to visualize their "DNA" (e.g., high morning rush, low weekend activity).

* **Operational Implications**: For each cluster, describe the operational strategy you would implement. For example, "Cluster 1: 'Workhorse' stations with high commuter traffic require frequent rebalancing during rush hours. Cluster 2: 'Residential' stations with high weekend activity can be deprioritized for weekday rebalancing but need attention on Fridays and Saturdays."


#### 5. Dimensionality Reduction (PCA)

With "Day of week patterns" (7 features) plus "Commuter Dynamics" and "Volume," you might be hitting 10+ dimensions. K-Means struggles with high-dimensional "noise."
* **Task**: Use Principal Component Analysis (PCA) to reduce your features to 2 or 3 principal components before clustering. 
Visualize the clusters in this reduced space. If the clusters are well-separated, it means your features capture meaningful patterns. Compare this visualization with the original feature space. Does PCA help in distinguishing the clusters more clearly? 
* Explain what is PCA in your own terms and how it helps in this context.

> Pro tip: PCA is not just a "preprocessing step" for clustering. It can also help you understand which features contribute most to the variance in your data, giving insights into what drives station behavior.


#### 6. Temporal Stability Analysis (The "Weather" Factor)

Instead of using weather as a feature for clustering, we will use it as a stress test.

* **The Question**: Does a "Workhorse" station stay a "Workhorse" when it rains, or does its behavior collapse?
* **Task**: Compare the cluster assignments on a sunny Monday vs. a rainy Monday. If 30% of stations change clusters, your logistics plan needs a "Rainy Day" contingency route.
To quantify this, create a 'Stability Matrix' (Confusion Matrix) comparing Cluster IDs on Sunny days vs. Rainy days. Which clusters are 'weather-proof' and which ones vanish when it pours?"

> Pro tip: Create a "Weather Condition" feature (e.g., "Sunny," "Rainy," "Snowy") and analyze how cluster memberships change under different weather conditions. This can reveal the robustness of your clusters and inform dynamic operational strategies.


### Resources & Documentation


* Dataframe Groupby: 
    - https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.groupby.html
    - https://www.datacamp.com/tutorial/pandas-groupby

* Scikit-Learn Clustering:
    - https://scikit-learn.org/stable/modules/clustering.html
    - [K-Means Documentation](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.KMeans.html#sklearn.cluster.KMeans)
    - [Preprocessing and Scaling](https://scikit-learn.org/stable/modules/preprocessing.html)

* Advanced Visualization:
    - https://plotly.com/python/plotly-express/
    - https://python-visualization.github.io/folium/
    - https://geopandas.org/en/stable/gallery/plotting_with_folium.html




### Submission

- A Jupyter notebook documenting the preprocessing, clustering and visualization steps.
* Submission link: [Moodle](https://moodle.insa-lyon.fr/course/view.php?id=10022)
