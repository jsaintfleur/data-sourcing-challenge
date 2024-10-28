# Geomagnetic Storm Prediction Data Preparation

## Purpose

The **Geomagnetic Storm Prediction Data Preparation** project aims to prepare a dataset to assist the NOAA Space Weather Prediction Center in predicting Geomagnetic Storms (GSTs). These storms, often triggered by Coronal Mass Ejections (CMEs) from the Sun, can disrupt critical infrastructure such as satellites, GPS systems, and power grids. By analyzing the time intervals between CME and GST events using data from NASA's DONKI API, this project provides a foundation for machine learning models to improve NOAA's forecasting accuracy.

Driven by my interest in applying data science to real-world challenges, I created this program to expand my knowledge in data extraction, transformation, and analysis. Through this project, I explored working with APIs, handling time-series data, and preparing datasets for future predictive modeling efforts. The experience allowed me to deepen my Python and data manipulation skills in a practical, impactful scenario.

---

## Overview

The **Geomagnetic Storm Prediction Data Preparation** project follows a structured process to extract, clean, merge, and analyze CME and GST data from NASA's DONKI API. This pipeline prepares a final dataset that captures key temporal relationships, enabling further analysis and predictive modeling. The project addresses essential questions for storm prediction, including:

- How long does it typically take for a CME event to lead to a GST?
- Which CME characteristics correlate with the occurrence of GSTs?
- What is the average time difference between CME and GST events?
  
This project demonstrates the importance of data preparation in forecasting systems, highlighting the value of time-series analysis in predicting space weather events.

---

## Data Dictionary

The dataset includes the following columns:

| Column             | Data Type | Description                                                   |
|--------------------|-----------|---------------------------------------------------------------|
| **activityID_CME** | `object`  | Unique identifier for each CME event.                         |
| **startTime_CME**  | `datetime`| Timestamp when the CME event occurred.                        |
| **GST_ActivityID** | `object`  | Identifier linking CME to its related GST.                    |
| **activityID_GST** | `object`  | Unique identifier for each GST event.                         |
| **startTime_GST**  | `datetime`| Timestamp when the GST event occurred.                        |
| **timeDiff**       | `float64` | Calculated time difference (in minutes) between CME and GST events. |

### Additional Information
- **Row Count**: The dataset includes all available CME-GST linked events from 2013 to 2024.
- **Data Types**: `object` (string), `datetime` (timestamp), and `float64` (numeric for time differences).
- **Non-null Count**: All columns have complete data, ensuring consistency and reliability.

For further information, refer to the NASA API documentation on CME and GST events.

---

## Project Structure

The project files are organized as follows:

- **[`output/`](./output/)**: Contains output data and visualizations.
  - **[`event_analysis_charts/`](./output/event_analysis_charts/)**: Folder with event analysis visualizations.
    - [`cumulative_event_counts.png`](./output/event_analysis_charts/cumulative_event_counts.png)
    - [`event_type_distribution.png`](./output/event_analysis_charts/event_type_distribution.png)
    - [`hourly_event_distribution.png`](./output/event_analysis_charts/hourly_event_distribution.png)
    - [`monthly_event_trends.png`](./output/event_analysis_charts/monthly_event_trends.png)
    - [`yearly_counts_event_type.png`](./output/event_analysis_charts/yearly_counts_event_type.png)
  - **[`merged_cme_gst_data.csv`](./output/merged_cme_gst_data.csv)**: Final merged dataset containing CME and GST data, ready for further analysis and modeling.
- **[`README.md`](./README.md)**: This documentation file, explaining the project purpose, structure, and instructions.
- **[`retrieve_data.ipynb`](./retrieve_data.ipynb)**: The main Jupyter Notebook where data extraction, transformation, and analysis steps are documented and executed.


---

## Visualizations

The project includes the following visualizations to better understand the data and patterns:

1. **[Cumulative Event Counts](./output/event_analysis_charts/cumulative_event_counts.png)**: Shows the cumulative counts of CME and GST events over time.
2. **[Event Type Distribution](./output/event_analysis_charts/event_type_distribution.png)**: Bar chart showing the distribution of different event types.
3. **[Hourly Event Distribution](./output/event_analysis_charts/hourly_event_distribution.png)**: Histogram showing the distribution of events by hour of the day.
4. **[Monthly Event Trends](./output/event_analysis_charts/monthly_event_trends.png)**: Line plot showing trends in the frequency of events by month.
5. **[Yearly Counts by Event Type](./output/event_analysis_charts/yearly_counts_event_type.png)**: Line plot of yearly counts of different event types.

These visuals, found in the [`output/event_analysis_charts`](./output/event_analysis_charts/) directory, provide insights into the temporal distribution of CME and GST events and help identify trends for model training.


---

## Key Steps

### Part 1: Request CME Data

1. **API Query**: Set up the base URL and parameters for NASA's DONKI API to fetch CME data over a specified date range.
   ```python
   base_url = "https://api.nasa.gov/DONKI/"
   specifier = "CME"
   startDate = "2013-05-01"
   endDate = "2024-05-01"

2. **Data Retrieval**: Fetch CME data, convert it to JSON, and load it into a DataFrame.

### Part 2: Request GST Data

1. **API Query**: Use the same base URL and parameters to extract GST data.
   ```python
   base_url = "https://api.nasa.gov/DONKI/"
   specifier = "GST"
   startDate = "2013-05-01"
   endDate = "2024-05-01"

2. **Data Retrieval**: Fetch GST data, convert it to JSON, and load it into a DataFrame.

3. **Data Cleaning**: Retain only necessary columns, and use `explode()` to separate rows with multiple linked events.

4. **Activity ID Extraction**: Extract CME-related `activityID` from linked events.


### Part 3: Merge and Clean Data

1. **Merge Datasets**: Merge the CME and GST DataFrames on their relevant `activityID` columns.

2. **Calculate Time Difference**: Compute the time difference (in minutes) between CME and GST occurrences, adding this as a new column (`timeDiff`).

3. **Summary Statistics**: Use `describe()` to review the average and median time differences between CME and GST events.

4. **Export Data**: Save the final dataset as `merged_cme_gst_data.csv` for future use in machine learning models.

## Use Cases

This project serves as a foundation for future research, analysis, and machine learning applications that can enhance understanding and forecasting of geomagnetic storms (GSTs) triggered by Coronal Mass Ejections (CMEs):

- **Forecast Improvement**: By utilizing this dataset, predictive models can be developed to forecast GST events based on CME characteristics and timing. This can allow NOAA to anticipate the onset of geomagnetic storms with higher accuracy. In particular, models trained on these patterns can help identify high-risk periods following CME events, providing a crucial window for early warnings and mitigating potential impacts on GPS, power grids, and satellites.

- **Pattern Analysis**: The dataset enables researchers to conduct in-depth analyses of time intervals between CME and GST events. By examining these intervals and other CME attributes, researchers can uncover patterns that determine the likelihood and severity of GSTs following specific CMEs. This analysis could lead to improved understanding of space weather conditions and contribute to new scientific findings that enhance space weather forecasting capabilities.

- **Resource Allocation**: Insights derived from this dataset can assist agencies like NASA and NOAA in optimizing their resource allocation. By identifying periods of heightened geomagnetic storm risk, decision-makers can better prioritize satellite monitoring, instrument calibration, and other key resources to maximize preparedness for potential space weather disruptions. This proactive resource planning based on predictive insights can be crucial in ensuring uninterrupted functionality of vital infrastructure during high-risk periods.

- **Event Correlation Analysis**: The time differences and correlations between CME characteristics and subsequent GSTs offer a valuable dataset for scientists studying solar-terrestrial interactions. Analyzing such correlations can contribute to understanding how solar activity affects Earth’s magnetosphere, leading to better-informed models that can predict space weather impacts more accurately.

- **Operational Decision Support**: For agencies reliant on space weather stability, such as aviation, telecommunications, and energy providers, predictive insights from this dataset can enhance operational decision-making. By forecasting GST events more reliably, organizations can preemptively adjust their operations, such as rerouting flights or safeguarding power grid operations, thus minimizing the potential for large-scale disruptions caused by geomagnetic storms.

---

## Technologies Used

- **Python**: The primary programming language used for data extraction, cleaning, and analysis.
- **Pandas**: Essential data manipulation library used for DataFrame transformations, filtering, and calculations.
- **Matplotlib & Seaborn**: Visualization libraries utilized to create charts and graphs for understanding data patterns and trends.
- **NASA DONKI API**: The data source for real-time and historical space weather data, providing information on CMEs and GSTs that drive the dataset.
- **Jupyter Notebook**: An interactive environment where data preparation, exploration, and visualization steps are documented and executed, making the process reproducible and accessible for future analysis.

---

## Recommendations

Leveraging the insights derived from time difference data and event patterns in this dataset, the following strategic recommendations are proposed:

- **Advance Forecasting Models**: Integrate this dataset into advanced machine learning frameworks to enhance predictive models for GST onset. Precise timing and likelihood predictions based on CME data will enable NOAA and partner agencies to issue more accurate, earlier warnings, substantially reducing the risk to critical infrastructure reliant on stable geomagnetic conditions.

- **Optimize Monitoring Protocols**: Prioritize resource allocation during high-frequency CME periods and focus analyses on specific CME attributes correlated with GST occurrences. This data-driven, targeted monitoring approach will allow NOAA to allocate observational and computational resources more efficiently, focusing efforts on high-risk intervals and event types.

- **Develop Comprehensive Response Strategies**: Historical analysis of GST events enables agencies and infrastructure operators to implement preemptive protective measures during predicted high-risk periods. This proactive approach would allow satellite operators to adjust orbits, power grid operators to implement surge protection, and aviation to plan adaptive routing, minimizing potential disruptions from geomagnetic disturbances.

- **Enhance Early Warning Systems**: By integrating nuanced CME data insights into existing early warning systems, agencies can issue more precise, context-aware alerts. This tailored alerting strategy, based on specific CME attributes linked to GST onset, would enable critical sectors to prepare effectively, reducing response times and bolstering resilience across industries.

- **Foster Interagency Collaboration**: Given the cross-sector impacts of geomagnetic storms, collaboration between NOAA, NASA, and other key stakeholders is essential for a unified response. Developing shared standards for data interpretation and event prioritization will enable synchronized, coordinated efforts across sectors, reinforcing national resilience to space weather phenomena.

By implementing these recommendations, agencies can significantly improve predictive capabilities, preparedness, and response efficacy, ensuring that space weather events are managed with greater precision and foresight.

---

## Conclusion

The **Geomagnetic Storm Prediction Data Preparation** project demonstrates the pivotal role of data science in advancing space weather forecasting capabilities. By systematically analyzing the relationships between Coronal Mass Ejections (CMEs) and Geomagnetic Storms (GSTs), this project has generated a robust dataset that serves as a foundational asset for predictive modeling.

Through this project, we explored key temporal patterns between CME and GST events, highlighting the potential to significantly enhance NOAA's forecasting accuracy. This data-driven approach offers insights that empower early-warning systems, support resource allocation decisions, and foster collaboration across agencies tasked with managing space weather impacts. 

Furthermore, the visualizations and patterns uncovered in this dataset underscore the importance of proactive preparation and strategic resource deployment during high-risk periods. By enabling NOAA, NASA, and other stakeholders to predict GST events more accurately, this project contributes to more resilient infrastructure, from satellite operations to power grids, that rely on stable geomagnetic conditions.

In closing, this project not only reinforces the value of data analysis and machine learning in addressing complex, real-world challenges but also exemplifies how interdisciplinary collaboration and innovative analytics can drive meaningful progress in environmental and space sciences. The methodologies and insights from this dataset offer a strong foundation for future research and practical applications, furthering our understanding and management of space weather phenomena.


## License

This project is licensed under the **MIT License** – a permissive license that allows for reuse, modification, and distribution. You are free to use this code and data in any project, provided attribution is given to the original author. 

A copy of the license text can be found in the [`LICENSE`](./LICENSE.txt) file in this repository.


## References

This project was made possible by data provided through NASA’s Space Weather Database Of Notifications, Knowledge, Information (DONKI) API. Special thanks to the NASA/NOAA teams for their open data initiatives and dedication to advancing space weather research.

- **[NASA DONKI API](https://kauai.ccmc.gsfc.nasa.gov/DONKI/)**: The primary source for Coronal Mass Ejection (CME) and Geomagnetic Storm (GST) event data. Detailed API documentation is available [here](https://kauai.ccmc.gsfc.nasa.gov/DONKI/).
- **[NOAA Space Weather Prediction Center](https://www.swpc.noaa.gov/)**: NOAA's contributions and efforts to improve space weather predictions inform the motivation and use cases of this project. Visit their site [here](https://www.swpc.noaa.gov/).
- **[Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/)**: For data manipulation and cleaning processes, the Pandas library documentation was an invaluable resource. More details can be found [here](https://pandas.pydata.org/pandas-docs/stable/).
- **[Matplotlib Documentation](https://matplotlib.org/stable/contents.html)** & **[Seaborn Documentation](https://seaborn.pydata.org/)**: These libraries were used extensively to create visualizations that explore data trends. Visit the [Matplotlib documentation](https://matplotlib.org/stable/contents.html) and [Seaborn documentation](https://seaborn.pydata.org/) for more information.


