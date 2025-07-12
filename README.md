
# Residency Weekend Project – Titanic Dataset Analysis

## Project Overview
This Jupyter Notebook contains an exploratory data analysis (EDA) of the **Titanic dataset** as part of the **Residency Weekend Project** for the course *Advanced Big Data and Data Mining (MSCS-634-M40)*. The analysis was performed collaboratively by **David Andrejsin, Sakchham Sangroula, Milan Bista, and Unique Karanjit**.

The primary goal of this project was to derive insights from the Titanic dataset by performing data cleaning, handling missing values, and visualizing survival patterns based on key features like **passenger class**, **gender**, and **age**.

---

## Dataset Summary
- The dataset used is a CSV version of the Titanic dataset obtained from a Google Sheets URL.
- It includes features such as `age`, `sex`, `pclass`, `survived`, `embarked`, and `cabin`.
- Initial shape: Variable depending on load, but contains typical Titanic data structure with hundreds of entries and several categorical/numerical fields.

### Key Insights
- **Passenger class (pclass)** had a strong correlation with survival—first-class passengers had significantly higher survival rates.
- **Gender** played a major role—female passengers were more likely to survive than males.
- Visualizations confirmed these patterns using grouped bar charts showing survival status distributions.

---

## Data Cleaning & Preprocessing Steps
1. **Handled Missing Values:**
   - `age`: Imputed using the **median**.
   - `embarked`: Filled with the **mode** (most common value).
   - `cabin`: Dropped entirely due to excessive missingness.

2. **Duplicate Detection:**
   - Checked for and removed any duplicate rows (none found in this instance).

3. **Structural Inspection:**
   - Dataset shape and column information were printed and reviewed prior to transformation.

---

## Exploratory Data Analysis (EDA)
- Used **matplotlib** for visualizations.
- Produced bar plots to analyze survival trends across:
  - **Passenger class** (`pclass`)
  - **Sex** (`sex`)
- Style applied: `seaborn-whitegrid` for clean and readable visuals.

---

## Challenges & Resolutions
### Missing Data
- **Challenge:** Missing values in `age`, `embarked`, and `cabin`.
- **Resolution:** Used statistical imputation (median/mode) and removed unusable columns.

### Data Quality
- **Challenge:** Potential for duplicate rows.
- **Resolution:** Verified and confirmed no duplicates present.

---

## Files
- `Residency_Project.ipynb`: Jupyter Notebook containing code, visualizations, and output.
- `README.md`: Project documentation (you’re reading it).

---

## Conclusion
This project successfully cleaned and explored the Titanic dataset, identifying clear survival patterns based on class and gender. The steps followed laid a foundation for more advanced predictive modeling in future phases.
