
## Session 1 - Data Exploration, Cleaning & Enrichment

* Date: February 4, 2026, 14:00 - 18:00
* Room: Thorgal

### Objectives:

Transform raw data into actionable insights and understand the temporal and spatial dynamics of the bike-sharing system.

**The Industrial Engineering perspective**: Understanding demand 'seasonality.' As engineer you must know when the system is under strain to plan maintenance and determine exactly when to redistribute bikes to specific locations.

Follow the steps below:

1. Load the dataset and perform initial exploration (e.g., checking for missing values, data types, basic statistics).
    - The dataset can be found at: [https://huggingface.co/datasets/lmoncla/lyon-velov-bike-sharing-dataset](https://huggingface.co/datasets/lmoncla/lyon-velov-bike-sharing-dataset)

2. Data Cleaning
   - Handle missing or inconsistent data.

3. Feature Engineering
   - Temporal variables: Extract day of the week, hour, month, and create flags for `is_weekend`.
   - Weather integration: Import the weather dataset available here: [https://huggingface.co/datasets/lmoncla/lyon-weather-23-25](https://huggingface.co/datasets/lmoncla/lyon-weather-23-25).
     - Analysis: Correlate rain/temperature with rental counts.

4. Data Visualization
   - Temporal heatmap: Create a matrix of Hour of the day vs Day of the week to visualize usage peaks.
   - Interactive map (using Folium/Plotly): Display stations on a map of Lyon with point sizes proportional to station capacity.

> The list of stations can be found here: [https://huggingface.co/datasets/lmoncla/lyon-velov-bike-sharing-dataset/resolve/main/stations-velov.json](https://huggingface.co/datasets/lmoncla/lyon-velov-bike-sharing-dataset/resolve/main/stations-velov.json)

```python 
# sample of code to load the list of stations (with their GPS coordinates)
import pandas as pd
df_stations = pd.read_json('https://huggingface.co/datasets/lmoncla/lyon-velov-bike-sharing-dataset/resolve/main/stations-velov.json')
df_stations.head()
```


### Starter packs and tutorials

* Pandas Dataframe:
   - https://www.datacamp.com/tutorial/pandas-tutorial-dataframe-python 
   - https://pandas.pydata.org/docs/user_guide/10min.html
   - https://pandas.pydata.org/docs/user_guide/cookbook.html#cookbook

* Data Visualization with Matplotlib/Seaborn:
   - https://www.geeksforgeeks.org/python/how-to-plot-a-pandas-dataframe-with-matplotlib/
   - https://pandas.pydata.org/docs/getting_started/intro_tutorials/04_plotting.html
   - https://tryolabs.com/blog/2017/03/16/pandas-seaborn-a-guide-to-handle-visualize-data-elegantly

* Folium for Interactive Maps:
   - https://python-visualization.github.io/folium/
   - https://nbviewer.org/github/python-visualization/folium/blob/main/examples/Index.ipynb


### Submission

- A Jupyter notebook documenting the data cleaning, enrichment, and visualization steps.
* Submission link: [Moodle](https://moodle.insa-lyon.fr/course/view.php?id=10022)
