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
