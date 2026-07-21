# 🎬 Movie Data Analysis — TMDB 5000 Movies Dataset

A full data science workflow — cleaning, EDA, feature engineering, visualization, and a bonus revenue prediction model — built on the TMDB 5000 Movies dataset.

**Subject:** Data Analytics
**Lecturer:** Heng Sovanmonynuth

**Group Members**
- Srors Muyyi (B20231302)
- Houn Sopheak (B20231681)
- Poeng Lyheng (B20233531)

---

## 📌 Project Objective

This project applies the complete data science workflow — from raw data to actionable insight — to explore what drives a movie's box-office performance. It goes beyond descriptive statistics to ask practical questions: does a bigger budget guarantee a better movie? Does genre popularity translate into genre profitability? Can revenue be predicted from a movie's known characteristics before release?

## 📂 Dataset

- **Name:** TMDB 5000 Movies Dataset
- **Source:** [Kaggle — tmdb/tmdb-movie-metadata](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata)
- **Size:** ~4,800 movies, with variables including budget, revenue, popularity, vote average, vote count, genres, runtime, release date, and more.

> The raw CSV (`tmdb_5000_movies.csv`) is included in this repo for reproducibility. All rights to the original data belong to TMDB / Kaggle.

## 🧭 Workflow Overview

The notebook (`Movie_Analysis-G1.ipynb`) is organized into the following stages:

1. **Understand & Explore** — initial inspection of structure, data types, and variable descriptions.
2. **Data Cleaning & Preprocessing**
   - Dropped `homepage` (64%+ missing)
   - Filled missing `tagline` with a placeholder rather than a numeric substitute
   - Dropped rows missing `overview`, `runtime`, or `release_date` (<0.1% of data)
   - Converted invalid `0` values in `budget`, `revenue`, and `runtime` to `NaN`
   - Filtered `status` to `Released` movies only
   - Parsed nested JSON-like columns (`genres`, `keywords`, `production_companies`, etc.) into readable comma-separated strings
   - Checked and intentionally kept outliers (blockbusters like *Avatar*, *Avengers* are genuine, not data errors)
   - Encoded `original_language` for modeling
3. **Exploratory Data Analysis (EDA)**
   - Distribution and skewness analysis of key numeric variables
   - Correlation heatmap
   - Genre frequency analysis
   - Trend of movies released per year (1916–2017)
   - Revenue/budget by genre and by decade
4. **Feature Engineering**
   - `profit` (revenue − budget)
   - `release_year` / `release_month`
   - `budget_tier` (binned budget categories)
5. **Data Visualization** — box plots, pair plots, pie chart, and scatter plots
6. **Prediction Model (Bonus)**
   - Linear Regression vs. Random Forest Regression (plus a log-transformed Random Forest variant)
   - Evaluated with MAE, RMSE, and R²
   - 5-fold cross-validation to check for overfitting
   - Feature importance analysis
7. **Insight Generation** — five key findings backed by evidence from the analysis above

## 🔑 Key Findings

1. **Budget drives revenue, but not quality.** Budget–revenue correlation is 0.71, while budget–rating correlation is only 0.02. Median rating stays flat (6.2–6.4) across all budget tiers even as median revenue jumps ~27x from Low to Blockbuster tier.
2. **A handful of blockbusters distort the "average" movie.** Revenue skew ≈ 3.88 and budget skew ≈ 2.22 — most movies cluster at low values with a long right tail.
3. **Genre popularity ≠ genre profitability.** Drama is the most-produced genre (2,291 movies) but doesn't crack the top 10 by median revenue; Animation, Adventure, Fantasy, and Family earn far more per film.
4. **Top performers and biggest flops both cluster at high budgets.** Big-budget bets carry big upside and big risk alike.
5. **The most critically loved films aren't the top earners.** Highly-rated films like *The Shawshank Redemption* and *The Godfather* don't appear among the top box-office performers.

## 🛠️ Tech Stack

- **Language:** Python
- **Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn` (`LinearRegression`, `RandomForestRegressor`, `train_test_split`, `cross_val_score`, `StandardScaler`, `LabelEncoder`)
- **Environment:** Jupyter Notebook

## 📁 Repository Structure

```
.
├── Movie_Analysis-G1.ipynb   # Full analysis notebook
├── tmdb_5000_movies.csv      # Raw dataset (from Kaggle)
└── README.md                 # Project documentation
```

## ▶️ How to Run

1. Clone the repo:
   ```bash
   git clone https://github.com/azureohizone/<repo-name>.git
   cd <repo-name>
   ```
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```
3. Launch the notebook:
   ```bash
   jupyter notebook Movie_Analysis-G1.ipynb
   ```

## ⚠️ Limitations

- Missing financial records reduced the number of movies usable for modeling.
- Revenue is highly right-skewed, making blockbuster outcomes hard to predict precisely.
- Popularity, vote count, and vote average are measured *after* release, which limits their usefulness for true pre-release prediction.
- Dataset is weighted toward modern films (sharp growth in records from the 1990s onward).

## 📄 License

This project is for academic purposes as part of a Data Analytics course assignment. Dataset license follows the original [Kaggle dataset terms](https://www.kaggle.com/datasets/tmdb/tmdb-movie-metadata).
