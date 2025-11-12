# Queensland, Australia Traffic Crash Analysis
### An Exploratory Data Analysis (EDA) to Understand the Factors Behind Crash Severity

This project performs a comprehensive exploratory data analysis (EDA) on over 400,000 traffic crash records from Queensland, Australia. The primary goal is to deeply understand the data, uncover hidden patterns, and identify the key factors that contribute to the severity of a crash.

The analysis serves as the complete preprocessing and feature-discovery phase for a future machine learning model designed to predict crash severity.

**Dataset:** [Queensland Government Open Data - Road Traffic Crashes](https://www.data.qld.gov.au/dataset/crash-data-from-queensland-roads)

---

## Analysis Approach

The analysis was conducted in the `MAIN DS Polimi Project - ver2.ipynb` Jupyter Notebook and follows a structured approach:

1.  **Data Loading & Cleaning:** Loaded the dataset and handled missing values.
2.  **Target Variable Analysis:** Investigated the target variable, `Crash_Severity`, to understand its distribution and any changes over time.
3.  **Feature Engineering:** Created new, more intuitive features from existing ones (e.g., binning `Crash_Hour` into `Crash_Time_Of_Day`, `Crash_Day_Of_Week` into `Is_Weekend`).
4.  **Temporal Analysis:** Explored how time (hour, day of the week, month) impacts crash frequency and severity.
5.  **Environmental Analysis:** Analyzed the effect of road conditions, weather (`Crash_Atmospheric_Condition`), and lighting on crash outcomes.
6.  **Geospatial Analysis:** Plotted crash locations on an interactive `folium` map to identify geographical hotspots.
7.  **Key Finding & Conclusion:** Identified a critical data-reporting change that dictates the entire strategy for predictive modeling.

---

## Key Findings & Visualizations

This EDA uncovered several key factors that are highly correlated with crash severity:

* **Time of Day:** Crash frequency spikes during the 'Morning_Rush' (5-9 AM) and 'Evening_Rush' (4-7 PM). However, crashes occurring at 'Night' show a higher proportion of severe outcomes.
* **Day of Week:** Weekdays and Weekends show different patterns. Weekends, particularly late at night, are strongly associated with more severe 'Hospitalisation' and 'Fatal' crashes.
* **Speed Limit:** There is a clear and strong positive correlation between the posted speed limit and crash severity. The analysis shows that most of the 'Hospitalisation' and 'Medical treatment' are related to 60 km/hr, 'Fatal' and 'Hospitalisation' outcomes rise significantly in 100-110 km/h zones compared to higher than 50-60 km/h zones.
* **Environmental Conditions:** As expected, adverse conditions significantly increase risk. 'Wet' road surfaces, 'Raining' weather, and 'Darkness' all show a clear correlation with increased crash severity.
* **Crash Nature:** The `Crash_Nature` (e.g., 'Head-on', 'Hit pedestrian') and `Crash_Type` ('Single Vehicle' vs. 'Multi-Vehicle') are some of the most powerful predictors in the dataset.
* **Geospatial Hotspots:** The `folium` map visualization confirms that crashes are not random. They are heavily concentrated in specific hotspots, such as major intersections, highway segments, and urban centers. This proves that longitude and latitude (or a clustered version of them) will be a critical feature.

## The "Data Shift" Discovery: A Critical Insight

The most important finding of this analysis is a **major data shift that occurred after 2010**.

While analyzing the `Crash_Severity` target variable over time, it became clear that one of the severity classes was **no longer recorded after 2010**.

![Severity Class Distribution Over Time](httpsV-image_63ecda.png)
*(This chart, generated in the notebook, shows a severity class disappearing post-2010)*

This "bug" is not an error in the data but a **change in reporting methodology**. The poor performance of initial models was due to them being trained on data with conflicting class definitions.

## Conclusion & Next Steps for Modeling

This EDA confirms that the dataset is highly predictive, but it *must* be handled correctly based on the 2010 data shift.

**The primary conclusion is that any valid predictive model MUST be trained only on data from 2011 onwards.**

The next phase of this project will involve:
1.  **Filtering the dataset** to include only data `where Crash_Year > 2010`.
2.  **Engineering a `cluster_id` feature** from the geospatial data (using DBSCAN) to represent crash hotspots.
3.  **Building and tuning** a predictive model (e.g., `CatBoost` or `XGBoost`) on this clean, consistent, and relevant dataset to predict the 4 remaining severity classes.

---

## How to Use This Repository

1.  Clone the repository:
    ```bash
    git clone [your-repo-link]
    ```
2.  Install the required libraries:
    ```bash
    pip install pandas numpy matplotlib seaborn folium
    ```
3.  Run the Jupyter Notebook:
    ```bash
    jupyter notebook "MAIN DS Polimi Project - ver2.ipynb"
    ```
