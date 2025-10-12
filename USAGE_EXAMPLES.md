# 📖 Usage Examples & Tutorials

## Table of Contents
1. [Basic Usage](#basic-usage)
2. [Working with Built-in Datasets](#working-with-built-in-datasets)
3. [Uploading Custom CSV Files](#uploading-custom-csv-files)
4. [Understanding the Visualizations](#understanding-the-visualizations)
5. [Interpreting Results](#interpreting-results)
6. [Advanced Tips](#advanced-tips)

---

## Basic Usage

### Example 1: Quick Start with California Housing

**Objective**: Train all models on California Housing dataset and compare results.

**Steps**:
1. Run the app: `streamlit run app.py`
2. Default dataset (California Housing) is already selected
3. Navigate to **Tab 2: Training & Evaluation**
4. Click **"🚀 Train All Models"** button
5. Wait 10-20 seconds for training to complete
6. View results in the metrics table

**Expected Results**:
- R² scores around 0.75-0.85
- HistGradientBoosting typically performs best
- Training completes in under 30 seconds

**What You'll Learn**:
- How to train multiple models simultaneously
- Which model performs best on housing data
- Feature importance (square footage, location, etc.)

---

### Example 2: Understanding Model Explanations

**Objective**: Learn how HistGradientBoostingRegressor works.

**Steps**:
1. Go to **Tab 1: Model Explanation & Visualization**
2. Expand **"🔍 What is HistGradientBoostingRegressor?"**
3. Read about histogram binning and gradient boosting
4. Expand **"⚖️ How does it compare to other models?"**
5. Review the comparison table
6. Expand **"🏗️ Algorithm Architecture"**
7. Study the boosting process diagram

**What You'll Learn**:
- Histogram binning concept (255 bins vs 1000s of split points)
- Sequential tree building process
- Native missing value handling
- When to use HistGradientBoosting vs alternatives

---

## Working with Built-in Datasets

### Example 3: Diabetes Dataset Analysis

**Objective**: Analyze the Diabetes dataset and identify important features.

**Steps**:
1. In sidebar, select **"Diabetes"** from dataset dropdown
2. Note: Target column is automatically set to "target"
3. Go to **Tab 2: Training & Evaluation**
4. View dataset preview (442 samples, 10 features)
5. Click **"🚀 Train All Models"**
6. After training, select **"HistGradientBoosting"** for analysis
7. View **Feature Importance** section
8. Check which features are most predictive

**Expected Results**:
- R² scores around 0.40-0.55 (this is a harder problem)
- Features like BMI, blood pressure may rank high
- Smaller dataset trains very quickly (<5 seconds)

**Insights**:
- Medical data is often harder to predict (lower R²)
- Some models may show overfitting on small datasets
- Feature importance reveals biological markers

---

### Example 4: Comparing All Models

**Objective**: Systematically compare model performances.

**Steps**:
1. Use California Housing dataset
2. Ensure all models are selected (HistGradientBoosting, LinearRegression, RandomForest, XGBoost)
3. Train all models
4. Navigate to **Tab 3: Model Comparison & Insights**
5. Study the 4-panel comparison chart
6. Review the metrics table
7. Check the "Overfit Gap" column

**What to Look For**:
- **Best R² Score**: Which model predicts best?
- **Lowest RMSE**: Which has smallest errors?
- **Overfit Gap**: Which generalizes best?
- **Speed**: Which trained fastest?

**Typical Rankings** (California Housing):
1. HistGradientBoosting: R² ~0.83
2. XGBoost: R² ~0.82
3. RandomForest: R² ~0.80
4. LinearRegression: R² ~0.60

---

## Uploading Custom CSV Files

### Example 5: Using the Sample Dataset

**Objective**: Upload and analyze the provided sample_data.csv.

**Steps**:
1. In sidebar, select **"Upload CSV"**
2. Click **"Browse files"**
3. Select `sample_data.csv`
4. Dataset preview appears (20 rows, 6 columns)
5. Select **"house_price"** as target column
6. Note: Features include age, income, education_level, etc.
7. Click **"🚀 Train All Models"**
8. View results

**Expected Results**:
- Very high R² scores (0.95+) - this is synthetic data
- Education level and income likely most important
- Categorical feature (education_level) is automatically encoded

**What You'll Learn**:
- How to upload your own data
- Automatic categorical encoding
- Feature importance with mixed data types

---

### Example 6: Creating Your Own Dataset

**Objective**: Prepare and upload a custom CSV for analysis.

**Your CSV Requirements**:
```csv
feature1,feature2,feature3,target
10,20,A,100
15,25,B,150
20,30,A,200
```

**Format Guidelines**:
- ✅ First row must be column names (headers)
- ✅ At least 2 columns (1 feature + 1 target)
- ✅ Can include numerical and categorical columns
- ✅ Missing values (NaN) are handled automatically
- ✅ No index column needed

**Steps**:
1. Create CSV file with proper format
2. Upload through sidebar
3. Select target column
4. Train models

**Common Issues**:
- ❌ No headers: Add column names in first row
- ❌ Too few samples: Need at least 20 rows for meaningful results
- ❌ All categorical: Need at least one numerical feature
- ❌ Single column: Need multiple features

---

## Understanding the Visualizations

### Example 7: Interpreting Feature Importance

**Visualization**: Horizontal bar chart showing top features.

**How to Read**:
- **Longer bars** = More important features
- **Top features** = Most influential on predictions
- **Zero importance** = Feature not used by model

**Example Interpretation** (California Housing):
```
MedInc (Median Income)         |████████████████| 0.52
Latitude                       |████████|         0.28
Longitude                      |██████|           0.12
AveRooms (Avg Rooms)          |███|              0.05
...
```

**What This Means**:
- Income explains 52% of price variation
- Location (lat/long) adds 40% more explanation
- Other features have minor impact

**Actions**:
- Focus data collection on important features
- Consider removing unimportant features
- Investigate why certain features matter

---

### Example 8: Analyzing Predicted vs Actual Plot

**Visualization**: Scatter plot with red diagonal line.

**How to Read**:
- **Red line**: Perfect predictions (y = x)
- **Points near line**: Good predictions
- **Points above line**: Overpredicted (predicted > actual)
- **Points below line**: Underpredicted (predicted < actual)
- **R² score**: Overall goodness of fit

**Example Scenarios**:

**Scenario A - Good Model**:
```
Points clustered around red line
R² = 0.85
→ Model is accurate and consistent
```

**Scenario B - Systematic Bias**:
```
Points systematically below line at high values
R² = 0.70
→ Model underestimates expensive houses
```

**Scenario C - High Variance**:
```
Points widely scattered around line
R² = 0.45
→ Model is inconsistent, needs improvement
```

---

### Example 9: Understanding Residual Plots

**Visualization**: Scatter plot of predictions vs errors.

**How to Read**:
- **Y-axis**: Residuals (Actual - Predicted)
- **X-axis**: Predicted values
- **Zero line**: Perfect predictions
- **Random scatter**: Good model
- **Patterns**: Model problems

**Pattern Analysis**:

**Pattern 1 - Random Scatter** ✅
```
Points randomly distributed around zero
→ Model assumptions are met
→ No systematic errors
```

**Pattern 2 - Funnel Shape** ⚠️
```
Spread increases with predicted value
→ Heteroscedasticity (non-constant variance)
→ Consider log transformation
```

**Pattern 3 - Curved Pattern** ❌
```
Residuals form a curve
→ Non-linear relationship not captured
→ Need more complex model
```

**Pattern 4 - Outliers** ⚠️
```
Most points near zero, few far away
→ Outliers in data
→ Consider robust regression or outlier removal
```

---

### Example 10: Partial Dependence Plots

**Visualization**: Line plots showing feature effects.

**How to Read**:
- **X-axis**: Feature values
- **Y-axis**: Predicted target (holding other features constant)
- **Slope**: Direction and strength of relationship

**Example Interpretation** (Income vs House Price):
```
Graph shows upward trend
Steep slope at low income, flatter at high income
→ Income strongly affects price for cheaper houses
→ Other factors matter more for expensive houses
```

**Use Cases**:
- Understand feature-target relationships
- Identify non-linear patterns
- Detect threshold effects
- Validate domain knowledge

---

## Interpreting Results

### Example 11: Evaluating Model Performance

**Metrics Guide**:

**R² Score** (0 to 1, higher is better):
- **0.9+**: Excellent - Model captures 90%+ of variance
- **0.7-0.9**: Good - Solid predictive performance
- **0.5-0.7**: Moderate - Useful but room for improvement
- **<0.5**: Poor - Consider different approach

**RMSE** (lower is better):
- Same units as target variable
- Penalizes large errors heavily
- Compare to target's standard deviation
  - RMSE < 0.5 * std: Excellent
  - RMSE < std: Good
  - RMSE > std: Poor

**MAE** (lower is better):
- Average absolute error
- More robust to outliers than RMSE
- Easier to interpret than RMSE
- If MAE << RMSE: Outliers present

**Overfitting Gap** (train R² - test R²):
- **<0.05**: Well-generalized ✅
- **0.05-0.10**: Moderate overfitting ⚠️
- **>0.10**: Significant overfitting ❌

---

### Example 12: Diagnosing Model Issues

**Problem**: R² = 0.30 on test set

**Diagnosis Steps**:
1. Check overfitting gap
   - Gap > 0.10? → Overfitting
   - Gap < 0.05? → Underfitting

2. For **Underfitting**:
   - Try more complex model
   - Add feature engineering
   - Check data quality

3. For **Overfitting**:
   - Reduce model complexity
   - Add regularization
   - Get more training data

4. Check visualizations:
   - Feature importance: Meaningful?
   - Residual plot: Patterns?
   - Predicted vs Actual: Systematic bias?

---

### Example 13: Selecting the Best Model

**Decision Framework**:

**If accuracy is critical**:
→ Choose model with highest test R²

**If speed is critical**:
→ Choose LinearRegression or HistGradientBoosting

**If interpretability is critical**:
→ Choose LinearRegression or check feature importance

**If handling missing data**:
→ Choose HistGradientBoosting or XGBoost

**If mixed data types**:
→ Choose HistGradientBoosting (native categorical support)

**Balanced choice**:
→ HistGradientBoosting (fast + accurate + flexible)

---

## Advanced Tips

### Example 14: Optimal Test Set Size

**Trade-offs**:

**Large Test Set (30-40%)**:
- ✅ More reliable performance estimates
- ✅ Better detection of overfitting
- ❌ Less data for training
- ❌ Potentially worse model

**Small Test Set (10-20%)**:
- ✅ More data for training
- ✅ Better model performance
- ❌ Less reliable test metrics
- ❌ Overfitting harder to detect

**Recommendation**:
- **Large datasets** (>10K): 10-20% test
- **Medium datasets** (1K-10K): 20-30% test
- **Small datasets** (<1K): 30-40% test or use cross-validation

---

### Example 15: Feature Engineering Ideas

**Based on Feature Importance Results**:

**If location features are important**:
- Create distance features (to city center, amenities)
- Cluster locations into neighborhoods
- Add interaction: location × income

**If time features exist**:
- Extract cyclical features (month, day of week)
- Create time since event
- Add seasonal indicators

**If continuous features are important**:
- Try polynomial features (x²)
- Create binned versions
- Add ratio features (income/age)

**If categorical features have low importance**:
- Try different encoding (target encoding)
- Combine rare categories
- Create interaction with numerical features

---

### Example 16: Improving Model Performance

**Checklist**:

1. **Data Quality**:
   - [ ] Remove duplicates
   - [ ] Handle outliers
   - [ ] Fix data entry errors
   - [ ] Validate feature distributions

2. **Feature Engineering**:
   - [ ] Create interaction features
   - [ ] Transform skewed features (log)
   - [ ] Encode categoricals differently
   - [ ] Add domain knowledge features

3. **Model Tuning**:
   - [ ] Adjust learning_rate
   - [ ] Change max_depth
   - [ ] Modify min_samples_leaf
   - [ ] Tune max_iter

4. **Ensemble Methods**:
   - [ ] Average predictions from top models
   - [ ] Use weighted average by R²
   - [ ] Stack models

5. **More Data**:
   - [ ] Collect additional samples
   - [ ] Use data augmentation
   - [ ] Combine multiple sources

---

### Example 17: Downloading and Using Trained Models

**Steps to Download**:
1. Navigate to **Tab 3: Model Comparison & Insights**
2. Scroll to **"💾 Download Results"** section
3. Click **"💾 Save Best Model"**
4. Model saved as `.pkl` file with timestamp

**Using the Downloaded Model**:

```python
import joblib
import pandas as pd

# Load the model
model = joblib.load('HistGradientBoosting_model_20250112_143022.pkl')

# Prepare new data (same format as training)
new_data = pd.DataFrame({
    'feature1': [10, 20],
    'feature2': [30, 40],
    # ... all features used in training
})

# Make predictions
predictions = model.predict(new_data)
print(predictions)
```

**Important Notes**:
- Model includes preprocessing pipeline
- New data must have same features as training data
- Categorical features must use same categories
- Model expects same column order

---

### Example 18: Batch Processing Multiple Datasets

**Workflow**:

1. **Prepare datasets**: Multiple CSV files in a folder
2. **For each dataset**:
   - Upload to app
   - Select target
   - Train models
   - Download metrics CSV
   - Download best model
3. **Compare across datasets**: Analyze which models work best for different data types

**Automation Idea** (outside app):
```python
# Pseudo-code for batch processing
for csv_file in dataset_folder:
    df = pd.read_csv(csv_file)
    # Train models programmatically
    # Log results to spreadsheet
```

---

## 🎯 Summary of Best Practices

1. **Always start with built-in datasets** to understand the app
2. **Read the Model Explanation tab** before training
3. **Train all models** initially, then focus on best performers
4. **Check overfitting** before trusting results
5. **Study feature importance** to understand your data
6. **Examine residual plots** to validate model assumptions
7. **Download results** for reporting and documentation
8. **Iterate**: Try different test sizes, feature engineering
9. **Compare metrics** across multiple runs
10. **Save best models** for deployment

---

## 📚 Further Learning

**After mastering these examples**:
1. Study hyperparameter tuning (GridSearchCV)
2. Learn about cross-validation
3. Explore SHAP values for advanced interpretability
4. Try classification tasks (modify for classification)
5. Build production pipelines with saved models

**Happy modeling! 🚀📊**
