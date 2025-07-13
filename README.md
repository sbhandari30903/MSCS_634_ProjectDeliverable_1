# Titanic Survival Analysis - MSCS 634 Residency Project

## Team Members
- **David Andrejsin**
- **Sakchham Sangroula** (Sakchham10)
- **Milan Bista**
- **Unique Karanjit**
- **Shimon Bhandari**

**Course:** Advanced Big Data and Data Mining (MSCS-634-M40)  
**Assignment:** Residency Weekend Project

# Titanic Data Mining Project

This project was completed as part of a graduate-level Data Mining course and applies key data mining techniques to the well-known Titanic dataset from [Kaggle's Titanic Competition](https://www.kaggle.com/competitions/titanic/overview). It includes data preparation, exploratory analysis, feature engineering, classification, clustering, regression modeling, and association rule mining.

## 📁 Dataset

We used the official Titanic competition dataset provided by Kaggle, which includes two files:
- `train.csv`: Training data with known survival outcomes.
- `test.csv`: Test data without survival labels (used for predictions only).

---

## 🔍 Phase 1: Data Exploration & Cleaning

### Tasks Performed:
- **Data Inspection:** Loaded `df_train` and `df_test` using pandas.
- **Missing Values:** Imputed missing `Age` with median, `Embarked` with mode, and `Fare` with median (in test set).
- **Duplicates & Inconsistencies:** Checked and confirmed dataset is clean.
- **Exploratory Data Analysis (EDA):**
  - KDE plot: Age distribution by survival status.
  - Bar plot: Survival by sex.
  - Box plot: Fare outlier detection.
  - Data summary: `.describe()` used for quick stats.

### Key Insights:
- Most survivors were female and/or 1st or 2nd class passengers.
- Fare has many outliers, but they reflect real variation due to class.
- Age and Fare are skewed and required normalization for regression.

---

## 🔨 Phase 2: Regression Modeling

Although survival is a classification problem, we applied regression on continuous targets for academic purposes.

### Target Variable: `Fare`

#### Feature Engineering:
- Converted `Sex` to numeric.
- Created `FamilySize = SibSp + Parch + 1`.

### Models Used:
- Linear Regression
- Ridge Regression (with alpha tuning via GridSearchCV)
- Lasso Regression (with alpha tuning)

### Evaluation Metrics:
- R², MSE, RMSE
- Cross-validation was used for model reliability.

#### Results:
| Model | Best α | R²    | RMSE   |
|-------|--------|-------|--------|
| Ridge | 20.0   | 0.425 | 39.28  |
| Linear | —     | 0.422 | 39.32  |
| Lasso | 0.1    | 0.419 | 39.41  |

> Ridge slightly outperformed other models. However, overall R² was low, indicating that Fare is influenced by complex or non-linear factors.

---

## 🤖 Phase 3: Classification, Clustering & Pattern Mining

### 1. Classification

- **Models Used:** K-Nearest Neighbors (KNN) and Decision Tree
- **Hyperparameter Tuning:** GridSearchCV used to optimize K in KNN
- **Metrics:**
  - Accuracy
  - F1 Score
  - Confusion Matrix
  - ROC Curve

> Both models performed reasonably well. Decision Trees provided better interpretability, while KNN offered slightly higher accuracy with tuned K.

### 2. Clustering

- **Algorithm:** K-Means (k=3)
- **Preprocessing:** PCA used to reduce features to 2D for visualization
- **Insights:**
  - Clusters revealed meaningful separations based on Age, Fare, and FamilySize.
  - Cluster 0: Young, large family size, low Fare (likely 3rd class families)
  - Cluster 1: Older passengers with high Fare (likely 1st class)
  - Cluster 2: Adults with small family size and low Fare

### 3. Association Rule Mining

- **Algorithm:** Apriori (with mlxtend)
- **Focus:** Only rules with consequent = `'Survived'`
- **Metrics:**
  - Support
  - Confidence
  - Lift

#### Example Rules:
- `(1st Class, Female) → Survived` — confidence = 96.8%, lift = 2.52
- `(2nd Class, Female) → Survived` — confidence = 92.1%, lift = 2.40

> Females and 1st/2nd class passengers had the strongest association with survival.

---

## 📊 Tools & Libraries

- Python 3.10
- pandas, numpy
- matplotlib, seaborn
- scikit-learn
- mlxtend

---

## 📌 Conclusion

This project demonstrates a complete data mining pipeline:
- We explored and cleaned the Titanic dataset.
- Built regression and classification models.
- Performed unsupervised clustering.
- Applied pattern mining to extract interpretable survival rules.

Each method contributed unique insights and reinforced the importance of gender, class, and fare in predicting survival outcomes on the Titanic.
