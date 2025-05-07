# Water Quality Classification for Agricultural Use

This machine learning project analyzes groundwater quality data collected from Telangana, India (2018) to predict the suitability of water samples for irrigation. We use supervised classification techniques to model chemical indicators and determine the most accurate model for classifying water into one of several quality categories.

---

## Dataset Overview

The dataset originates from [Kaggle](https://www.kaggle.com/datasets/sivapriyagarladinne/telangana-post-monsoon-ground-water-quality-data) and includes water samples across multiple villages. Each row represents a water sample with measurements from chemical and environmental attributes. The **goal** is to classify each sample into a **C1S1–C4S4** category representing salinity and sodium levels relevant for agricultural use.

### Key Columns

| Column | Description |
|--------|-------------|
| `sno` | Serial number (unique ID for each row) |
| `District`, `Mandal`, `Village` | Categorical identifiers of the sample's location |
| `Latitude`, `Longitude` | Geographic coordinates |
| `gwl` | Ground water level |
| `Season` | Season during which sample was taken (e.g., Post-Monsoon) |
| `pH` | Acidity/alkalinity of water |
| `E.C` | Electrical Conductivity – reflects salinity |
| `T.D.S` | Total Dissolved Solids – minerals & impurities concentration |
| `CO3`, `HCO3`, `Cl`, `F`, `NO3`, `SO4` | Chemical compounds (Carbonates, Fluorides, Nitrates, etc.) |
| `Na`, `K`, `Ca`, `Mg` | Major ion concentrations (Sodium, Potassium, Calcium, Magnesium) |
| `Total Hardness` | Measure of water hardness |
| `RSC`, `SAR` | Residual Sodium Carbonate and Sodium Adsorption Ratio |
| `Classification` | **Target variable** (C1S1–C4S4), denotes water quality for irrigation |

Only **numeric chemical features** and the `Classification` column were retained for modeling to focus on the predictive performance of chemical indicators.

---

## Problem Statement

Classify each water sample into one of the `Classification` labels (e.g., C3S1, C2S1) using chemical indicators. These categories correspond to combinations of **salinity (C1–C4)** and **sodium hazard (S1–S4)** and are used to guide agricultural irrigation planning.

---

## Methods Used

### Data Preprocessing
- Dropped location-based categorical fields (`District`, `Village`, etc.)
- Retained only numeric features relevant to water chemistry
- Filled missing values with `0.0` to ensure consistency
- Removed rare classification labels (fewer than 5 samples) to improve cross-validation reliability

### Feature Selection
Only the following features were retained after filtering:
- `pH`, `E.C`, `T.D.S`, `CO3`, `HCO3`, `Cl`, `F`, `NO3`, `SO4`, `Na`, `K`, `Ca`, `Mg`, `Total Hardness`, `SAR`

### Model Training & Evaluation
Two supervised classifiers were implemented:
- **Decision Tree**
- **K-Nearest Neighbors (KNN)**

Each model was evaluated using:
- **5-fold cross-validation** (reduced to 3-fold if needed based on class size)
- **Mean Accuracy**
- **Weighted Precision**

### Hyperparameter Tuning
- **Decision Tree**: Tuned `max_depth` values: 3, 5, 7
- **KNN**: Tuned `n_neighbors` values: 5, 10, 15

---

## 📈 Results

| Model | Hyperparameter | Mean Accuracy | Precision |
|-------|----------------|----------------|-----------|
| Decision Tree | max_depth=5 | **91.0%** | **91.3%** |
| KNN | k=10 | 90.6% | 83.5% |
| KNN | k=5 | 89.9% | **85.2%** |

🔍 **Conclusion**:  
The **Decision Tree (max_depth=5)** outperformed KNN in both accuracy and precision, making it the more reliable choice for groundwater classification based on chemical indicators.

---

## 📌 Key Learnings

- Simpler models like Decision Trees can outperform instance-based models like KNN on structured numeric datasets.
- Data preprocessing, class balancing, and evaluation strategy have a major impact on model performance and reliability.
- The chemical features alone are highly predictive of irrigation quality, suggesting potential for streamlined testing in the field.

---

## 📚 Technologies Used
- Python
- pandas, matplotlib, seaborn
- scikit-learn (DecisionTreeClassifier, KNeighborsClassifier)
- Jupyter Notebook

---

## ✅ To Run the Notebook

1. Clone the repository or download the `.ipynb` file
2. Ensure the CSV dataset file (`ground_water_quality_2018_post.csv`) is in the same directory
3. Run the notebook using Jupyter or VSCode
4. Follow along each step: data loading, cleaning, model training, and evaluation

---

## 📌 Acknowledgments

Dataset: [Kaggle - Telangana Groundwater Quality](https://www.kaggle.com/datasets/sivapriyagarladinne/telangana-post-monsoon-ground-water-quality-data)  
Author: Fabrice Faustin  
Course: CSCI 4371 – Introduction to Machine Learning
