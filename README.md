# wine-quality-eda
wine-quality-eda : End-to-end data analysis of the wine quality dataset (4,898 samples) using Python. Covers data cleaning, duplicate and outlier handling (IQR capping/removal), feature engineering, EDA with visualizations, filtering, grouping, correlation analysis, and t-tests. Built with pandas, NumPy, Matplotlib, Seaborn, and SciPy.
wine-quality-analysis/
├── wine_analysis.py          # Main analysis script
├── data/
│   └── wine_quality.csv      # Input dataset
├── wine_cleaned.csv          # Output: cleaned data (with new features)
├── wine_cleaned_capped.csv   # Output: cleaned data with outliers capped
└── README.md

Raw Data
   │
   ▼
1. Load ──► 2. Inspect ──► 3. Clean ──► 4. EDA
                                          │
                                          ▼
9. Save ◄── 8. Stats Test ◄── 7. Group ◄── 6. Sort ◄── 5. Filter
10. def load(path):
    try:
        return pd.read_csv(path)
    except (UnicodeDecodeError, pd.errors.ParserError):
        return pd.read_excel(path, engine="openpyxl")

    [Q1 − k × IQR,  Q3 + k × IQR]

    [21:56, 03/10/2026] Sakshi😊: high_q      = df[df["quality"] >= 7]                                  # simple condition
strong      = df[(df["alcohol"] > 12) & (df["quality"] >= 7)]         # AND
either      = df[(df["ph"] < 3.0) | (df["ph"] > 3.6)]                 # OR
in_range    = df[df["alcohol"].between(10, 12)]                       # range
in_list     = df[df["quality"].isin([3, 4])]                          # membership
by_query    = df.query("alcohol > 11 and residual_sugar < 5 and quality >= 6")
top_alcohol = df[df["alcohol"] > df["alcohol"].quantile(0.9)]         # top 10%
[21:56, 03/10/2026] Sakshi😊: t, p = stats.ttest_ind(hi, lo, equal_var=False)
[21:56, 03/10/2026] Sakshi😊: df.to_csv("wine_cleaned.csv", index=False)
df_capped.to_csv("wine_cleaned_capped.csv", index=False
