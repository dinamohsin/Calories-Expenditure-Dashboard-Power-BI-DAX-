# **Calories Expenditure Dashboard (Power BI & DAX)**

This project analyzes **calorie expenditure** data using **Power BI** and **DAX**. The dataset comes from a Kaggle Playground Series competition and is designed to predict caloric energy expenditure based on biometric and activity-related features.

---

## Table of Contents

* [1. Data Analysis Workflow](#1-data-analysis-workflow)
* [2. Project Goal](#2-project-goal)
* [3. Dataset Source & Preparation](#3-dataset-source--preparation)
* [4. DAX Calculations (New Columns & Measures)](#4-dax-calculations-new-columns--measures)
* [5. Power BI Dashboard Visualizations](#5-power-bi-dashboard-visualizations)
* [6. Insights Q\&A](#6-insights-qa)
* [7. Technologies Used](#7-technologies-used)
* [8. Final Thoughts](#8-final-thoughts)

---

## **1. Data Analysis Workflow**

1. Download the **Predict Calorie Expenditure** dataset from Kaggle.
2. Import `train.csv` into **Power BI**.
3. Clean and validate the data.
4. Create calculated columns using **DAX**: `Calories_Level`, `Age_Group`, `BMI`, `Weight_Status`.
5. Develop **measures** for KPIs: `Avg Calories`, `Avg Duration`, etc.
6. Build a polished **dashboard** to illustrate key metrics and patterns.

---

## **2. Project Goal**

To create an informative and interactive **Power BI dashboard** that reveals how calories are expended across demographics like **age**, **gender**, **weight status**, and **heart rate**. This aims to enable data-driven insights into energy expenditure behaviors.

---

## **3. Dataset Source & Preparation**

* **Dataset:** [Predict Calorie Expenditure (Kaggle)](https://www.kaggle.com/datasets/adilshamim8/predict-calorie-expenditure)
* **Usage:** Only `train.csv` was used in this project.
* **Key Features Included:**

  * `Age` (numeric)
  * `Height` (cm)
  * `Weight` (kg)
  * `Duration` (minutes)
  * `Heart_Rate` (bpm)
  * `Calories` (target variable)

---

## **4. DAX Calculations (New Columns & Measures)**

### **New Columns (DAX)**

```DAX
Calories_Level = 
IF(CaloriesData[Calories] <= 100, "Low", 
   IF(CaloriesData[Calories] <= 180, "Medium", "High"))

Age_Group = 
SWITCH(
    TRUE(),
    [Age] <= 29, "20s",
    [Age] <= 39, "30s",
    [Age] <= 49, "40s",
    [Age] <= 59, "50s",
    [Age] <= 69, "60s",
    "70s"
)

BMI = 
DIVIDE([Weight], ([Height] / 100) * ([Height] / 100))

Weight_Status = 
SWITCH(
    TRUE(),
    [BMI] < 18.5, "Underweight",
    [BMI] < 25, "Normal",
    [BMI] >= 25, "Overweight"
)
```

### **Measures (DAX)**

```DAX
Avg Calories = AVERAGE(CaloriesData[Calories])
Avg Duration = AVERAGE(CaloriesData[Duration])
Avg Heart_Rate = AVERAGE(CaloriesData[Heart_Rate])

Calories per Hour = 
DIVIDE(
    SUM(CaloriesData[Calories]),
    SUM(CaloriesData[Duration]) / 60
)

Total Calories = SUM(CaloriesData[Calories])
```

---

## **5. Power BI Dashboard Visualizations**

The dashboard now features these visuals:

* **KPI Cards**:

  * Calories per Hour
  * Avg Calories
  * Avg Duration
  * Avg Height
  * Avg Heart Rate

* **Bar Chart**: Age Group by Gender (shows counts for male vs. female by age group)

* **Donut Chart**: Age Distribution (percentage share per age group)

* **Stacked Bar**: Duration by Calories\_Level & Age\_Group (shows average duration per calorie level across ages)

* **Bar Chart**: Calories by Weight Status (Avg Calories for Underweight, Normal, Overweight)

* **Line Chart**: Calories vs. Heart Rate

* **Line Chart**: Heart Rate by Gender across Age Groups

  
```

```

---

## **6. Insights Q\&A**

**Examples:**

* **Q:** Which age group is most prevalent in the dataset?
  **A:** The 20s group leads with around 206.9K entries (\~27.6% of total).

* **Q:** Which weight status burns the most calories on average?
  **A:** Overweight individuals average \~92 calories, followed by Normal (\~86) and Underweight (\~77).

* **Q:** How does heart rate relate to calorie burn?
  **A:** Calorie output increases with heart rate, exceeding ~250 calories at a heart rate of around ~120 bpm.

* **Q:** How does average heart rate vary by gender across age groups?
  **A:** In the 20s, 30s, and 60s, males show a higher average heart rate (e.g., 95 bpm vs. 90 bpm). However, starting from the 40s and 50s, females have a slightly higher average heart rate compared to males.

---

## **7. Technologies Used**

* **Power BI** – Data modeling and dashboard development
* **DAX** – For all custom calculated columns and measures
* **CSV** – Source data format from Kaggle

---

## **8. Final Thoughts**

This project showcases an end-to-end usage of **Power BI and DAX** to extract, transform, and visualize calorie expenditure data. The updated dashboard design—with gender-age group heart rate comparison—delivers more meaningful insight and improves interpretability.
