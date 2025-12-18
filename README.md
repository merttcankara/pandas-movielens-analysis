# 🎬 MovieLens 1M Data Analysis (Pandas)

This repository contains a Jupyter notebook analyzing the **MovieLens 1M** dataset using **Pandas** (with a little NumPy-style thinking for statistics).

> **Note on originality / ethics**  
> This work is based on a guided learning notebook (course-style exercises) and then organized for portfolio purposes.  
> The goal is to demonstrate **data analysis workflow and Pandas proficiency**, not to claim the dataset or original idea as mine.

---

## What’s inside

- **Notebook:** `notebooks/pandas_movielens.ipynb`
- **Dataset:** MovieLens 1M (download separately; not included in this repo)

---

## Dataset

This notebook expects the classic MovieLens 1M files:

- `users.dat`
- `ratings.dat`
- `movies.dat`

**Source:** GroupLens MovieLens Datasets  
https://grouplens.org/datasets/movielens/

Place the `.dat` files next to the notebook (or update paths inside the notebook).

---

## Analysis Outline (what the notebook does)

### 1) Load & merge tables
- Reads `users.dat`, `ratings.dat`, `movies.dat` with `pd.read_table(..., sep="::", engine="python")`
- Merges into one dataset:
  - `ratings` + `users` + `movies`

### 2) Mean ratings by gender (pivot table)
- Builds a pivot table of average rating per movie, split by gender:
  - `index="title"`, `columns="gender"`, `values="rating"`, `aggfunc="mean"`

### 3) Keep “active” titles (enough ratings)
- Counts ratings per title:
  - `data.groupby("title").size()`
- Filters movies with **at least 250 ratings** (arbitrary threshold used in the notebook to reduce noise)

### 4) Rating disagreement (standard deviation)
- Measures disagreement per movie using rating **standard deviation**:
  - `data.groupby("title")["rating"].std()`
- Finds the titles with the **largest disagreement** among viewers (top 10)

### 5) Occupation-based rating patterns
- Creates a pivot table:
  - average rating by **movie title × occupation**
- Computes **std across occupations** (row-wise) and lists titles with highest occupation disagreement

### 6) Extract year from movie title
- Creates a `year` column (from the title string in the notebook)
- Uses it to analyze **average rating by release year**

### 7) Top-rated movie for each year
- Aggregates ratings per title (average rating)
- For each year, finds the best-rated movie using a custom function and `groupby("year").apply(...)`

---



