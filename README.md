# Big Data Analysis with PySpark and MapReduce

Final project for the **Big Data** course.  
The project demonstrates how large datasets can be processed and analyzed using distributed data processing techniques with **PySpark** and **MapReduce**.

Two different datasets were analyzed:

- **Vehicle CO₂ Emissions dataset** – used to build a similarity-based recommendation system.
- **Powerlifting dataset** – used to perform distributed aggregation tasks using the MapReduce model.

The project focuses on demonstrating the **complete data analysis workflow**, from data cleaning and exploratory analysis to scalable processing and evaluation.

---

# Project Structure

```text
big-data-project/
│
├── Task1_PySpark_Recommender.ipynb
├── Task2_MapReduce_Powerlifting.ipynb
└── README.md
```


---

# Task 1 – Vehicle Recommendation System (PySpark)

This part of the project focuses on building a **similarity-based recommendation system for cars** using the **Vehicle CO₂ Emissions dataset**.

The dataset contains information about vehicle characteristics such as:

- engine size  
- number of cylinders  
- fuel type  
- transmission  
- vehicle class  
- fuel consumption (city and highway)  
- CO₂ emissions  

The objective was to analyze the dataset and recommend vehicles with **similar technical characteristics**.

---

## Data Processing

The dataset was loaded into a **PySpark DataFrame** and several preprocessing steps were applied:

- standardizing column names
- converting numerical fields to consistent types
- detecting and removing duplicate records
- cleaning categorical variables

After preprocessing, the dataset was ready for analysis and modeling.

---

## Exploratory Data Analysis

Exploratory analysis was performed to understand the relationships between variables.  
Key observations included:

- strong correlation between **fuel consumption and CO₂ emissions**
- relationship between **engine size and emission levels**
- variation in emissions depending on **vehicle class and fuel type**

Outliers were preserved because they represented real differences between vehicles rather than errors.

---

## Feature Engineering

To represent vehicles as numerical vectors, the following preprocessing steps were applied:

- numerical features were **scaled**
- categorical variables were **encoded using StringIndexer and OneHotEncoder**
- high-cardinality attributes such as **make and model** were excluded from the feature vector to avoid biasing similarity toward brand identity.

The final feature vector represented the **technical characteristics of each vehicle**.

---

## Recommendation Algorithm

The recommendation system uses **cosine similarity** to identify vehicles with similar characteristics.

Workflow:

1. transform each vehicle into a feature vector  
2. select a target vehicle  
3. compute cosine similarity between the target and all other vehicles  
4. rank vehicles by similarity score  
5. return the most similar vehicles as recommendations  

This approach groups vehicles by efficiency, emissions profile, and technical characteristics.

---

## Evaluation

Since similarity-based systems do not predict a target variable, traditional metrics such as **accuracy** or **RMSE** are not applicable.

Instead, evaluation focused on the **coherence of the recommendations**.  
Vehicles with similar technical profiles were successfully grouped together.

Limitations include:

- equal importance assigned to all features
- fewer comparison points for rare vehicle classes

Despite these limitations, the system provides a good baseline for a scalable recommendation approach.

---

# Task 2 – MapReduce Analysis of Powerlifting Competitions

The second part of the project uses **MapReduce principles implemented with PySpark RDDs** to analyze a dataset of powerlifting competitions.

The dataset contains records of athletes, competitions, and performance results.

---

## MapReduce Tasks

Three distributed computations were implemented.

### 1. Participants per Competition

Each athlete record was mapped to a pair:
`(competition_id, 1)`

A `reduceByKey` operation was then used to count participants in each competition.

This revealed large variation between competitions, with some events hosting only a few athletes while others included hundreds.

---

### 2. Competition Summary

Competition metadata was combined with participant counts to create a structured summary including:

- competition name  
- country  
- year  
- number of participants  

This produced a clear overview of competition size and geographic distribution.

---

### 3. Total Weight Lifted per Participant

Each athlete record was mapped to:
`(athlete_name, total_weight)`


A reduction step summed the total weight lifted across all competitions for each athlete.

This allowed identification of athletes with the highest cumulative performance.

---

# Big Data Tools Used

## PySpark

PySpark was used for:

- distributed data processing
- DataFrame operations
- feature engineering
- machine learning preprocessing pipelines

It enables scalable analysis and can handle datasets that are too large for single-machine processing.

---

## MapReduce (RDD API)

The MapReduce model was implemented using **PySpark RDD transformations**, including:

- `map`
- `reduceByKey`
- `join`

RDDs provide a lower-level interface that makes distributed computation steps explicit.

---

# Key Takeaways

This project demonstrates how different big data tools can be used for different types of tasks:

- **PySpark DataFrames and ML pipelines** are effective for machine learning workflows.
- **RDD-based MapReduce** is suitable for large-scale aggregation tasks.

Together, they highlight how distributed computing frameworks support scalable data analysis.

---

# Datasets

Vehicle CO₂ Emissions dataset  
https://www.kaggle.com/datasets/brsahan/vehicle-co2-emissions-dataset

Powerlifting dataset  
https://www.kaggle.com/datasets/dansbecker/powerlifting-database

---
