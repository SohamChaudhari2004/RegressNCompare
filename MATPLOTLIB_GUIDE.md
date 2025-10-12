# Matplotlib & Seaborn Visualization Reference

## Quick Reference for Updated Visualizations

### Library Information

**Matplotlib** (`matplotlib.pyplot as plt`)
- Core plotting library for Python
- Highly customizable
- Industry standard for scientific visualization
- Version: 3.7.0+

**Seaborn** (`seaborn as sns`)
- Built on top of matplotlib
- Statistical data visualization
- Beautiful default styles
- Version: 0.12.0+

---

## Visualizations in the App

### 1. Model Comparison Chart (2x2 Grid)

**Function**: `plot_comparison(results)`

**Output**: 
- 4 subplots in 2x2 grid
- Top-left: R² Score (blue bars)
- Top-right: MSE (coral bars)
- Bottom-left: MAE (green bars)
- Bottom-right: RMSE (gold bars)

**Features**:
- Seaborn whitegrid style
- Rotated x-axis labels (45°)
- Grid lines for easy reading
- Alpha transparency (0.7)

**Customization Options**:
```python
# Change style
sns.set_style("darkgrid")  # or "whitegrid", "dark", "white", "ticks"

# Change colors
colors = ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728']

# Adjust figure size
fig, axes = plt.subplots(2, 2, figsize=(16, 12))
```

---

### 2. Feature Importance Plot

**Function**: `plot_feature_importance(importance_df, top_n=10)`

**Output**:
- Horizontal bar chart
- Sorted by importance (descending)
- Shows top N features
- Steelblue color

**Features**:
- Uses seaborn barplot
- Grid lines on x-axis
- Clean, professional look

**Customization Options**:
```python
# Change color
sns.barplot(data=plot_df, y='Feature', x='Importance', color='coral', ax=ax)

# Change orientation to vertical
sns.barplot(data=plot_df, x='Feature', y='Importance', color='steelblue', ax=ax)

# Use color palette
sns.barplot(data=plot_df, y='Feature', x='Importance', palette='viridis', ax=ax)
```

---

### 3. Predicted vs Actual Scatter Plot

**Function**: `plot_predictions(y_true, y_pred, title)`

**Output**:
- Scatter plot of actual vs predicted values
- Red dashed line for perfect predictions
- R² score in title
- Grid for reference

**Features**:
- Alpha transparency (0.6)
- Navy edge colors
- Legend showing perfect prediction line
- Square aspect ratio (8x8)

**Customization Options**:
```python
# Change marker style
ax.scatter(y_true, y_pred, alpha=0.6, s=30, marker='o', color='steelblue')

# Change colors
ax.scatter(y_true, y_pred, alpha=0.6, s=30, c=y_true, cmap='viridis')

# Add regression line
from scipy import stats
slope, intercept, r_value, p_value, std_err = stats.linregress(y_true, y_pred)
ax.plot(y_true, slope * y_true + intercept, 'g--', label='Regression Line')
```

---

### 4. Residual Plot

**Function**: `plot_residuals(y_true, y_pred)`

**Output**:
- Scatter plot of residuals vs predicted values
- Red dashed line at y=0
- Coral colored points
- Dark red edges

**Features**:
- Shows error distribution
- Zero reference line
- Grid for analysis
- Legend

**Customization Options**:
```python
# Add histogram on side
from matplotlib.gridspec import GridSpec
gs = GridSpec(1, 2, width_ratios=[3, 1])
ax1 = plt.subplot(gs[0])
ax2 = plt.subplot(gs[1])
ax1.scatter(y_pred, residuals, ...)
ax2.hist(residuals, orientation='horizontal')

# Color by residual magnitude
colors = np.where(np.abs(residuals) > threshold, 'red', 'blue')
ax.scatter(y_pred, residuals, c=colors, alpha=0.6)
```

---

### 5. Partial Dependence Plots

**Function**: `plot_partial_dependence(pipeline, X_train, feature_names, features_to_plot)`

**Output**:
- 1-2 line plots side by side
- Shows marginal effect of features
- Steelblue lines
- Grid for reference

**Features**:
- Subplots for multiple features
- Bold titles
- Clean line plots
- Tight layout

**Customization Options**:
```python
# Add confidence intervals
from sklearn.inspection import partial_dependence
pd_result = partial_dependence(model, X, features=[0], kind='average')
# Plot with std deviation bands

# Change line style
axes[idx].plot(x, y, linewidth=3, color='darkblue', linestyle='--')

# Add markers
axes[idx].plot(x, y, linewidth=2, color='steelblue', marker='o')
```

---

## Styling Guide

### Global Style Settings

**Set Once at App Start**:
```python
# In app.py after imports
import matplotlib.pyplot as plt
import seaborn as sns

# Set default style
sns.set_style("whitegrid")
sns.set_context("notebook", font_scale=1.1)
plt.rcParams['figure.dpi'] = 100
plt.rcParams['savefig.dpi'] = 300
```

### Available Seaborn Styles

```python
# Light backgrounds
sns.set_style("white")      # White background, no grid
sns.set_style("whitegrid")  # White with grid lines (current)
sns.set_style("ticks")      # White with ticks

# Dark backgrounds
sns.set_style("dark")       # Dark background, no grid
sns.set_style("darkgrid")   # Dark with grid lines
```

### Color Palettes

```python
# Categorical palettes
sns.set_palette("deep")       # Default
sns.set_palette("pastel")     # Soft colors
sns.set_palette("bright")     # Vibrant colors
sns.set_palette("dark")       # Dark colors
sns.set_palette("colorblind") # Colorblind-friendly

# Sequential palettes
sns.set_palette("Blues")
sns.set_palette("Reds")
sns.set_palette("Greens")

# Diverging palettes
sns.set_palette("RdBu")       # Red-Blue
sns.set_palette("coolwarm")   # Cool-Warm
```

---

## Common Customizations

### Change Figure Size

```python
# In plotting functions, modify:
fig, ax = plt.subplots(figsize=(12, 8))  # width, height in inches
```

### Add Annotations

```python
# Add text to plot
ax.text(x, y, 'Important Point', fontsize=12, color='red')

# Add arrow
ax.annotate('Max Value', xy=(x, y), xytext=(x+1, y+1),
            arrowprops=dict(arrowstyle='->', color='red'))
```

### Change Fonts

```python
# Global font settings
plt.rcParams['font.family'] = 'sans-serif'
plt.rcParams['font.sans-serif'] = ['Arial']
plt.rcParams['font.size'] = 12

# Or per-plot
ax.set_title('Title', fontsize=16, fontfamily='serif')
```

### Save Figures

```python
# High quality PNG
fig.savefig('plot.png', dpi=300, bbox_inches='tight')

# Vector format (scalable)
fig.savefig('plot.pdf', bbox_inches='tight')
fig.savefig('plot.svg', bbox_inches='tight')

# With transparency
fig.savefig('plot.png', dpi=300, bbox_inches='tight', transparent=True)
```

---

## Troubleshooting

### Issue: Plots Not Displaying

**Solution**:
```python
# Ensure figure is returned
return fig

# In Streamlit, use
st.pyplot(fig)

# Close figure after display (prevent memory leak)
plt.close(fig)
```

### Issue: Text Overlapping

**Solution**:
```python
# Use tight_layout
plt.tight_layout()

# Or adjust manually
plt.subplots_adjust(left=0.1, right=0.9, top=0.9, bottom=0.1)

# Rotate labels
ax.tick_params(axis='x', rotation=45)
```

### Issue: Legend Covering Data

**Solution**:
```python
# Move legend
ax.legend(loc='best')           # Auto position
ax.legend(loc='upper right')    # Specific corner
ax.legend(bbox_to_anchor=(1.05, 1))  # Outside plot
```

### Issue: Colors Don't Match

**Solution**:
```python
# Use exact color codes
colors = {
    'steelblue': '#4682B4',
    'coral': '#FF7F50',
    'mediumseagreen': '#3CB371',
    'gold': '#FFD700'
}

ax.bar(x, y, color=colors['steelblue'])
```

---

## Performance Tips

### For Large Datasets

```python
# Reduce marker size
ax.scatter(x, y, s=1, alpha=0.3)

# Sample data
sample_size = 10000
indices = np.random.choice(len(x), sample_size, replace=False)
ax.scatter(x[indices], y[indices], ...)

# Use rasterization for PDF
ax.scatter(x, y, rasterized=True)
```

### Memory Management

```python
# Close figures when done
plt.close(fig)

# Or close all
plt.close('all')

# Use context manager
with plt.ioff():  # Turn off interactive mode
    fig, ax = plt.subplots()
    # ... plotting code ...
    st.pyplot(fig)
    plt.close(fig)
```

---

## Advanced Techniques

### Subplots with Different Sizes

```python
from matplotlib.gridspec import GridSpec

fig = plt.figure(figsize=(12, 8))
gs = GridSpec(3, 3, figure=fig)

ax1 = fig.add_subplot(gs[0, :])    # Top row, all columns
ax2 = fig.add_subplot(gs[1, :-1])  # Middle row, first 2 columns
ax3 = fig.add_subplot(gs[1:, -1])  # Right column, bottom 2 rows
```

### Multiple Y-Axes

```python
fig, ax1 = plt.subplots()

# First y-axis
ax1.plot(x, y1, 'b-')
ax1.set_ylabel('Y1', color='b')

# Second y-axis
ax2 = ax1.twinx()
ax2.plot(x, y2, 'r-')
ax2.set_ylabel('Y2', color='r')
```

### Seaborn Statistical Plots

```python
# Regression plot with confidence interval
sns.regplot(x=y_true, y=y_pred, ax=ax)

# Distribution plot
sns.histplot(residuals, kde=True, ax=ax)

# Box plot for outliers
sns.boxplot(data=df, ax=ax)

# Violin plot
sns.violinplot(data=df, ax=ax)
```

---

## Quick Reference Table

| Task | Code |
|------|------|
| Create figure | `fig, ax = plt.subplots()` |
| Bar chart | `ax.bar(x, y)` |
| Scatter plot | `ax.scatter(x, y)` |
| Line plot | `ax.plot(x, y)` |
| Horizontal line | `ax.axhline(y=0)` |
| Vertical line | `ax.axvline(x=0)` |
| Set title | `ax.set_title('Title')` |
| Set labels | `ax.set_xlabel('X')`, `ax.set_ylabel('Y')` |
| Add legend | `ax.legend()` |
| Add grid | `ax.grid(True)` |
| Save figure | `fig.savefig('file.png')` |
| Display in Streamlit | `st.pyplot(fig)` |
| Close figure | `plt.close(fig)` |

---

## Resources

**Official Documentation**:
- Matplotlib: https://matplotlib.org/stable/
- Seaborn: https://seaborn.pydata.org/
- Matplotlib Gallery: https://matplotlib.org/stable/gallery/index.html
- Seaborn Examples: https://seaborn.pydata.org/examples/index.html

**Tutorials**:
- Matplotlib Tutorial: https://matplotlib.org/stable/tutorials/index.html
- Seaborn Tutorial: https://seaborn.pydata.org/tutorial.html

**Cheat Sheets**:
- Matplotlib Cheatsheet: https://matplotlib.org/cheatsheets/
- Seaborn Cheatsheet: https://s3.amazonaws.com/assets.datacamp.com/blog_assets/Python_Seaborn_Cheat_Sheet.pdf

---

**Updated**: October 12, 2025
**App Version**: 2.0
**Libraries**: matplotlib 3.7.0+, seaborn 0.12.0+
