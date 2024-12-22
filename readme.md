# Ultramarathon Data Analysis

This project focuses on analyzing ultramarathon race data spanning two centuries. The dataset provides insights into event distances, athlete performance, and seasonal trends in races such as 50km and 50-mile events.

## Table of Contents

1. [Introduction](#introduction)
2. [Dataset Overview](#dataset-overview)
3. [Steps Performed](#steps-performed)
4. [Key Insights](#key-insights)
5. [Installation](#installation)
6. [Usage](#usage)

---

### Introduction

This analysis aims to uncover:
- Trends in race distances and athlete performance.
- Seasonal effects on ultramarathon events.
- Relationships between athlete attributes (age, gender) and performance metrics.

### Dataset Overview

- **Filename**: `TWO_CENTURIES_OF_UM_RACES.csv`
- **Attributes**:
  - Event details, athlete demographics, performance metrics, etc.
- **Key Fields Processed**:
  - Event Name, Event Distance/Length, Athlete Average Speed, Athlete Age, and more.

### Steps Performed

1. **Data Loading and Exploration**
   - Imported necessary libraries (`pandas`, `numpy`, `seaborn`, `matplotlib`).
   - Read the dataset using:
     ```python
     df = pd.read_csv('TWO_CENTURIES_OF_UM_RACES.csv')
     ```
   - Previewed data with `.head()` and checked dimensions with `.shape`.

2. **Data Cleaning**
   - Stripped extra spaces from column names.
   - Filtered data for specific distances (e.g., `50km`, `50mi`) and event years (e.g., 2020).
   - Processed event names to extract country information and standardized naming.
   - Calculated athlete age:
     ```python
     df2['athlete_age'] = 2020 - df2['Athlete year of birth']
     ```
   - Dropped irrelevant columns and missing values.

3. **Feature Engineering**
   - Created a new column `athlete_average_speed` and converted it to float.
   - Renamed columns for consistency:
     ```python
     df2 = df2.rename(columns={
         'Year of event': 'year',
         'Event name': 'race_name',
         'Event distance/length': 'race_length',
         ...
     })
     ```
   - Added seasonal information based on race month:
     ```python
     df2['race_season'] = df2['race_month'].apply(lambda x: 'Winter' if x>11 else ...)
     ```

4. **Visualizations**
   - Analyzed athlete performance across distances using various plots:
     - **Histogram**:
       ```python
       sns.histplot(df2['race_length'])
       ```
     - **Scatter Plot**:
       ```python
       sns.scatterplot(data=df2, x='athlete_age', y='athlete_average_speed', hue='athlete_gender')
       ```
     - **Violin Plot**:
       ```python
       sns.violinplot(data=df2, x='race_length', y='athlete_average_speed', hue='athlete_gender')
       ```
     - **Line Plot**:
       ```python
       sns.lineplot(data=df2.groupby(...).mean(), x='athlete_age', y='athlete_average_speed')
       ```

5. **Group Analysis**
   - Explored performance by:
     - Gender and race length.
     - Seasonal trends:
       ```python
       df2.groupby('race_season')['athlete_average_speed'].mean()
       ```

### Key Insights

- **Distance Trends**:
  - Athletes performed differently across `50km` and `50mi` races.
- **Seasonal Impact**:
  - Performance varied by season, with notable trends in summer and fall.
- **Athlete Attributes**:
  - Older athletes showed consistent average speeds, especially in long races.

### Installation

Ensure the following libraries are installed:

```bash
pip install pandas numpy seaborn matplotlib
```

### Usage

1. Place the dataset `TWO_CENTURIES_OF_UM_RACES.csv` in your working directory.
2. Run the Python script to analyze data and generate visualizations:

```python
python ultramarathon_analysis.py
```

3. Explore generated plots and insights.