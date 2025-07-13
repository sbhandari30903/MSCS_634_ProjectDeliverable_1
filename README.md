# Titanic Survival Analysis - MSCS 634 Residency Project

## Team Members
- **David Andrejsin**
- **Sakchham Sangroula** (Sakchham10)
- **Milan Bista**
- **Unique Karanjit**
- **Shimon Bhandari**

**Course:** Advanced Big Data and Data Mining (MSCS-634-M40)  
**Assignment:** Residency Weekend Project

## Dataset Summary

The Titanic dataset contains passenger information from the tragic 1912 sinking, used for dual prediction tasks: fare estimation and survival classification. Our analysis utilized both training and test datasets loaded from Google Sheets.

### Dataset Characteristics
- **Training Data**: 891 passengers with complete information
- **Test Data**: 418 passengers for prediction
- **Original Features**: PassengerId, Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked, Survived
- **Target Variables**: 
  - **Primary Task**: Fare (regression prediction of ticket prices)
  - **Secondary Task**: Survival (binary classification)

### Data Quality Issues
- **Missing Values**: Age (177 missing), Cabin (687 missing), Embarked (2 missing)
- **Data Types**: Mixed numerical and categorical features
- **Outliers**: Extreme fare values requiring careful handling

## Modeling Process

### Data Preprocessing Pipeline
1. **Missing Value Treatment**:
   - Age: Imputed with median (28.0 years)
   - Cabin: Dropped due to 77% missing values
   - Embarked: Filled with mode ('S' - Southampton)

2. **Feature Engineering**:
   - Created FamilySize = SibSp + Parch + 1
   - Age grouping: Child, Teen, Young Adult, Adult, Senior
   - Standardized categorical variables (Sex, Embarked)

3. **Data Transformation**:
   - StandardScaler for numerical features
   - OneHotEncoder for categorical variables
   - Pipeline integration for consistent preprocessing

### Model Implementation

#### Regression Models (Fare Prediction - Primary Task)
- **Linear Regression**: Baseline model for ticket price prediction
- **Ridge Regression**: L2 regularization with cross-validated alpha selection
- **Lasso Regression**: L1 regularization with feature selection capabilities
- **Features Used**: Pclass, Sex, Age, Embarked, FamilySize
- **Evaluation**: 5-fold cross-validation using R², MSE, and RMSE metrics

#### Classification Models (Survival Prediction - Secondary Task)
- **Decision Tree**: Grid search optimization for max_depth and min_samples_split
- **k-Nearest Neighbors**: Distance-based classification
- **Features Used**: Pclass, Sex, Age, Embarked, SibSp, Parch, FamilySize
- **Evaluation**: Accuracy, F1-score, confusion matrices, and ROC curves

## Evaluation Results

### Regression Performance (Fare Prediction)
| Model | Best α | R² Score | MSE | RMSE |
|-------|--------|----------|-----|------|
| Ridge | 10.0 | 0.6891 | 1538.2 | 39.22 |
| Lasso | 1.0 | 0.6889 | 1539.1 | 39.23 |
| Linear | n/a | 0.6889 | 1539.0 | 39.23 |

**Key Findings**: All models performed similarly with R² ≈ 0.69, indicating that passenger characteristics explain approximately 69% of fare variation. Ridge regression showed slight superiority with optimal regularization at α=10.0.

### Classification Performance (Survival Prediction)
| Model | Accuracy | F1-Score |
|-------|----------|----------|
| Decision Tree | 0.8268 | 0.7692 |
| k-NN | 0.8156 | 0.7500 |

**Optimal Decision Tree Parameters**: max_depth=5, min_samples_split=10

## Meaningful Insights and Key Observations

### Fare Prediction Insights
1. **Class-Fare Relationship**: Strong negative correlation (-0.55) between passenger class and fare - first-class tickets significantly more expensive
2. **Passenger Class Impact**: Primary determinant of fare pricing, with clear tier structure
3. **Gender Effect**: Male passengers paid slightly higher average fares, likely due to different travel patterns
4. **Embarkation Influence**: Cherbourg passengers paid highest average fares, suggesting premium route pricing
5. **Family Size Factor**: Larger families showed varied fare patterns, possibly due to group discounts or cabin sharing

### Survival Prediction Insights
1. **Gender Disparity**: Females had 74.2% survival rate vs. 18.9% for males - clear "women and children first" policy
2. **Class Impact**: First-class passengers (62.6% survival) significantly outperformed third-class (24.2% survival)
3. **Age Patterns**: Children showed higher survival rates, with adults having the lowest survival probability
4. **Embarkation Effect**: Cherbourg passengers had highest survival rates (55.4%) compared to Southampton (33.7%)

### Model Performance Insights
1. **Fare Prediction**: Passenger class and embarkation port emerged as strongest fare predictors
2. **Survival Prediction**: Sex and passenger class emerged as strongest survival predictors
3. **Regularization Benefits**: Ridge/Lasso prevented overfitting with minimal performance loss in fare prediction
4. **Classification Success**: Decision tree achieved 82.7% accuracy in survival prediction, demonstrating clear decision boundaries
5. **Model Consistency**: Similar performance across different algorithms suggests robust feature relationships

### Correlation Analysis
- Strong negative correlation between Pclass and Fare (-0.55) - higher class means higher fares
- Weak correlation between Age and Survival (0.08) - age had minimal direct impact on survival
- Family size showed complex relationship with both fare and survival (optimal size around 2-4 members)

## Challenges Encountered and Solutions

### 1. Missing Data Management
**Challenge**: Significant missing values in Age (19.9%) and Cabin (77.1%)
**Solution**: 
- Used median imputation for Age to maintain distribution shape
- Dropped Cabin feature due to excessive missingness
- Applied mode imputation for Embarked (only 2 missing values)

### 2. Dual Target Variable Complexity
**Challenge**: Managing two different prediction tasks with different feature requirements
**Solution**:
- Implemented separate feature engineering pipelines for fare and survival prediction
- Used appropriate evaluation metrics for each task type (R² for regression, accuracy/F1 for classification)
- Maintained clear separation between regression and classification workflows

### 3. Feature Engineering Complexity
**Challenge**: Determining optimal feature combinations and transformations for both prediction tasks
**Solution**:
- Created FamilySize as composite feature combining SibSp and Parch
- Implemented age binning to capture non-linear age effects
- Used systematic preprocessing pipeline for reproducibility
- Tailored feature selection for each prediction task (fare vs. survival)
**Challenge**: Balancing model complexity with generalization
**Solution**:
- Implemented grid search with cross-validation for Decision Tree
- Used built-in cross-validation for Ridge/Lasso alpha selection
- Applied stratified sampling to maintain class balance in train/test splits

### 4. Model Selection and Hyperparameter Tuning
**Challenge**: Comprehensive model comparison across different metrics
**Solution**:
- Implemented multiple evaluation metrics (accuracy, F1, R², RMSE)
- Created visualization suite for model comparison
- Used ROC curves for probabilistic model assessment

### 5. Evaluation Framework Design
**Challenge**: Comprehensive model comparison across different prediction tasks and metrics
**Solution**:
- Implemented task-specific evaluation metrics (R²/RMSE for fare, accuracy/F1 for survival)
- Created visualization suite for model comparison across both tasks
- Used ROC curves for probabilistic survival prediction assessment
- Developed comparative analysis framework for regression and classification results
**Challenge**: Ensuring proper separation between training and test procedures
**Solution**:
- Maintained separate preprocessing for train/test data
- Used cross-validation for honest performance estimation
- Preserved test set integrity throughout development process

### 6. Data Leakage Prevention
**Challenge**: Balancing model accuracy with explainability
**Solution**:
- Chose interpretable models (Decision Tree, Linear models)
- Provided feature importance analysis
- Created comprehensive visualizations for model understanding

### 7. Interpretability vs. Performance Trade-off

### Preprocessing Pipeline
```python
ColumnTransformer([
    ('num', StandardScaler(), ['Age', 'FamilySize', 'Pclass']),
    ('cat', OneHotEncoder(handle_unknown='ignore'), ['Sex', 'Embarked'])
])
```

### Cross-Validation Strategy
- 5-fold cross-validation for robust performance estimation
- Stratified sampling to maintain class distribution
- Consistent random state (42) for reproducibility

## Technical Implementation Notes

## Conclusions

The project successfully demonstrated comprehensive data mining workflow from raw data to dual predictive models. Key achievements include:

1. **Effective Data Preprocessing**: Systematic handling of missing values and feature engineering for multiple prediction tasks
2. **Dual Modeling Approach**: Successful implementation of both fare prediction (regression) and survival prediction (classification)
3. **Robust Evaluation**: Cross-validated performance assessment with task-appropriate metrics
4. **Actionable Insights**: Clear identification of fare determinants and survival factors with their relative importance

**Fare Prediction Results**: The analysis revealed that passenger class and embarkation port were primary determinants of ticket pricing, with the model explaining 69% of fare variation. This suggests a well-structured pricing system based on service class and route.

**Survival Prediction Results**: Social factors (gender, class) were primary determinants of survival, while demographic factors (age, family size) provided additional predictive power. Model performance was consistent across different algorithms, suggesting stable underlying patterns.

The dual prediction approach provided complementary insights into both the commercial (fare structure) and humanitarian (survival patterns) aspects of the Titanic disaster, demonstrating the dataset's rich analytical potential.

---

*This project demonstrates practical application of data mining concepts including exploratory data analysis, supervised learning, model evaluation, and statistical interpretation within an academic framework.*
