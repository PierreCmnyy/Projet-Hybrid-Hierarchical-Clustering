# 📘 High-Dimensional Data Analysis Project (Project B)

## 1. Project Overview

This project was carried out as part of the *High-Dimensional Data Analysis and Machine Learning* course at the **Toulouse School of Economics**.

### Objectives
- Select and preprocess an **open-source dataset** with at least 80 observations, 6 numerical variables, and 1 categorical variable.  
- Apply and interpret **seven statistical methods** studied in class:
  1. Principal Component Analysis (PCA)  
  2. Clustering  
  3. Discriminant Analysis (DA)  
  4. CART  
  5. Bootstrap  
  6. Bagging  
  7. Random Forests  
- Implement and explain a **specific additional method** depending on the assigned project.  
  For **Project B**, this was **Hybrid Hierarchical Clustering (HHC)**, from *Chipman & Tibshirani (2006)*, implemented using the **hybridHclust** R package.

---

## 2. Data Description

### Source
The dataset comes from the **2024 Current Population Survey – Annual Social and Economic Supplement (CPS-ASEC)**, conducted by the **U.S. Census Bureau**.

### Selected Variables
| Variable | Description |
|-----------|-------------|
| `NOW_PRIV` | Dummy: private insurance (1) or not (0) |
| `A_AGE` | Age |
| `PTOT_VAL` | Total income |
| `PEARN_VAL` | Earnings |
| `POTH_VAL` | Other income not from earnings |
| `PMED_VAL` | Expenditures on medical care |
| `POTC_VAL` | Expenditures on over-the-counter medications |
| `DSAB_VAL` | Aid/benefits related to disability |
| `FPERSONS` | Number of persons in the household |

The initial dataset contained **177,000 observations**.  
For computational feasibility, it was **randomly reduced to 10,000 individuals**.

---

## 3. Team Contributions

- **Pierre** → Data processing, CART, Bagging, Bootstrap  
- **Rémi** → Clustering, Discriminant Analysis, Random Forests, Hybrid Hierarchical Clustering  
- **Anas** → Report structure, data and context explanation, understanding of HHC  
- **Célia** → PCA, understanding of HHC  

---

## 4. Data Preparation

1. Imported the dataset (`bdd_cluster.csv`) into R.  
2. Selected relevant variables and recoded `NOW_PRIV` as 0/1.  
3. Checked for missing values → none found.  
4. Standardized numerical variables before PCA and clustering.

---

## 5. Exploratory Analysis

Descriptive statistics and visual summaries were produced to explore the data.  
Findings included:
- Strong variability in income and medical expenses.  
- Presence of outliers.  
- Majority of individuals were insured (`NOW_PRIV = 1` ≈ 63%).  

---

## 6. Methods Implemented

### 6.1. Principal Component Analysis (PCA)
- PCA performed on scaled quantitative variables using `Factoshiny`.  
- First 4–5 components explained ~80% of total variance.  

**Interpretation of components:**
- **Dim 1:** Income & earnings  
- **Dim 2:** Age & medical expenditures  
- **Dim 3:** “Vulnerability” (low income, high medical aid)  
- **Dim 5:** Access to healthcare (medical vs OTC spending)

---

### 6.2. Clustering
- Hierarchical clustering using **Ward’s method** on **Euclidean distances**.  
- Dendrogram visualization with 4 clusters (`k = 4`).  
- Identified socioeconomic groups based on expenditure and income similarities.

---

### 6.3. Discriminant Analysis (DA)
- Linear Discriminant Analysis to predict insurance status.  
- Addressed linearity issues by removing one variable.  
- Achieved moderate classification accuracy.

---

### 6.4. CART, Bootstrap, Bagging, Random Forests
- **CART:** Provided interpretable decision trees explaining insurance status.  
- **Bootstrap/Bagging:** Improved model stability and reduced variance.  
- **Random Forests:** Highest predictive accuracy; key variables were *income* and *age*.

---

### 6.5. Hybrid Hierarchical Clustering (Project B Specific Method)
- **Hybrid HClust** combines hierarchical clustering and partitioning algorithms (e.g., k-means).  
- Based on *Chipman & Tibshirani (2006)* and the **hybridHclust** R package.  
- Due to package and memory limitations, analysis was done on **100 randomly selected observations**.  
- Results revealed meaningful groupings but were **limited in generalizability** due to the reduced sample.

---

## 7. Difficulties Encountered

- Dataset **too large** (177k obs.), causing memory issues.  
- **hybridHclust package** failed on full dataset → used subset of 100.  
- Variable **linearity constraints** in DA required manual adjustments.  
- Managing multiple high-dimensional visualizations required careful interpretation.

---

## 8. Conclusions and Perspectives

- Key differences between insured and uninsured individuals were mainly explained by **income** and **medical expenditures**.  
- Classical methods (PCA, clustering, DA) provided complementary structure insights.  
- Ensemble methods (Bagging, Random Forests) increased model reliability.  
- Hybrid HClust is conceptually useful but requires dimensionality reduction for large-scale data.

### Future directions
- Apply HHC on a reduced feature space to enable full-sample clustering.  
- Compare HHC performance with traditional clustering methods.  
- Integrate additional socioeconomic or demographic variables to refine results.

---

## 9. Reproducibility

- Entire project developed in **R** using **Quarto (.qmd)**.  
- **Random seed fixed** for consistent results:  
  ```r
  set.seed(1)
