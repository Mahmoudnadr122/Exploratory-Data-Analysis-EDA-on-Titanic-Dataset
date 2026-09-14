# Titanic Dataset - Exploratory Data Analysis (EDA)

An end-to-end, reproducible Exploratory Data Analysis (EDA) project on the classic **Titanic: Machine Learning from Disaster** dataset. This project explores demographic profiles, socio-economic factors, data cleaning methodologies, detailed statistical analyses, and data visualizations.

---

## 📸 Project Showcase & Jupyter Notebook Previews

> **Tip:** You can place your screenshots taken from VS Code / Jupyter inside an `assets/` or `images/` directory in this repository, and they will render directly below.

### 1. VS Code Environment & Data Inspection
![VS Code Notebook Overview](./notebook_overview.png)

### 2. Group Statistics & Distribution Analysis
![Statistical Summaries in VS Code](./eda_statistics.png)

### 3. Visualizations & Correlation Heatmaps
![Visualizations Output](./eda_visualizations.png)
---

## 🗂️ Dataset Information & Local Path

* **Dataset Source:** Kaggle Titanic Competition (`train.csv`)
* **Local Workspace Directory:** `C:\Users\mahmo\Downloads\مجلد جديد\titanic\train.csv`
* **Target Feature:** `Survived` (0 = Did not survive, 1 = Survived)

### Features Schema:
| Feature | Data Type | Description |
| :--- | :--- | :--- |
| `PassengerId` | Integer | Unique identifier for each individual passenger |
| `Survived` | Integer (Binary) | Survival status (0 = Deceased, 1 = Survived) |
| `Pclass` | Integer (Ordinal) | Ticket class (1 = 1st Class, 2 = 2nd Class, 3 = 3rd Class) |
| `Name` | Object / String | Passenger name (including titles such as Mr, Mrs, Miss, Master) |
| `Sex` | Categorical / String | Biological sex (`male`, `female`) |
| `Age` | Float (Continuous) | Passenger age in years |
| `SibSp` | Integer (Discrete) | Number of siblings or spouses aboard |
| `Parch` | Integer (Discrete) | Number of parents or children aboard |
| `Ticket` | Object / String | Ticket identifier number |
| `Fare` | Float (Continuous) | Passenger fare paid (British Pounds) |
| `Cabin` | Object / String | Cabin room number |
| `Embarked` | Categorical / String | Port of Embarkation (C = Cherbourg, Q = Queenstown, S = Southampton) |

---

## 🔬 Detailed Step-by-Step Methodology & Statistics

### Step 1: Environment Setup & Data Loading
* Configured visualization style using `seaborn.set_theme(style="whitegrid")`.
* Loaded the raw data directly from the local path via Pandas `pd.read_csv()`.
* Checked dimensions: **891 rows and 12 columns**.

---

### Step 2: Missing Data Auditing & Data Cleaning
An audit of missing records revealed:
* **`Cabin`**: 687 missing values (~77.10%).
* **`Age`**: 177 missing values (~19.87%).
* **`Embarked`**: 2 missing values (~0.22%).

#### Cleaning Decisions:
1. **Dropping `Cabin`**: Because more than 77% of entries are absent, imputing would introduce heavy bias and distort statistical inference.
2. **Conditional Median Imputation for `Age`**:
   Instead of using an overall mean/median that distorts class differences, missing age values were imputed based on the median of `Sex` and `Pclass` sub-groups:
   $$\text{Age}_{\text{imputed}} = \text{Median}(\text{Age} \mid \text{Sex}, \text{Pclass})$$
3. **Mode Imputation for `Embarked`**:
   The two missing records were filled with the mode (`'S'` - Southampton), representing over 72% of the dataset.

---

### Step 3: Comprehensive Statistical Analysis

#### A. Five-Number Summary (Numerical Features)
* **Age**: Ranging from **0.42** to **80.0** years, with a median age around **26.0** years after demographic imputation.
* **Fare**: Displays strong positive skewness.
  * Minimum: `0.0`
  * 25th percentile (Q1): `7.91`
  * Median (Q2): `14.45`
  * 75th percentile (Q3): `31.00`
  * Maximum: `512.33` (outlier entries corresponding to luxury suites).

#### B. Survival Rate Statistics by Demographics
* **Overall Survival Rate**: **38.38%** (342 out of 891 survived).
* **By Gender (`Sex`)**:
  * **Female**: 74.20% survival rate (233 / 314 survived).
  * **Male**: 18.89% survival rate (109 / 577 survived).
  * *Statistical implication:* Female passengers were roughly **3.9x** more likely to survive than male passengers.
* **By Socio-Economic Class (`Pclass`)**:
  * **1st Class**: 62.96% survival rate (136 / 216 survived).
  * **2nd Class**: 47.28% survival rate (87 / 184 survived).
  * **3rd Class**: 24.24% survival rate (119 / 491 survived).
* **Two-Way Interaction (`Pclass` $\times$ `Sex`)**:
  * 1st Class Female: **96.8%** survival rate.
  * 2nd Class Female: **92.1%** survival rate.
  * 3rd Class Female: **50.0%** survival rate.
  * 1st Class Male: **36.9%** survival rate.
  * 2nd Class Male: **15.7%** survival rate.
  * 3rd Class Male: **13.5%** survival rate.

---

### Step 4: Visualizations & Pattern Discovery

1. **Demographic Bar Plots (`countplot` & `barplot`)**:
   * Evaluated survival counts segmented by biological sex.
   * Quantified monotonic decline in survival rate as passenger class moves from 1st to 3rd.
   * Compared embarkation points, showing Cherbourg (`C`) had the highest relative survival rate due to higher proportions of 1st class passengers.

2. **Continuous Variable Distributions (`histplot` & `boxplot`)**:
   * **Age Distribution**: Kernel Density Estimation (KDE) highlights higher survival spikes in infants and young children (< 10 years old).
   * **Fare Distribution**: Box plots (with outlier handling) show survivors had significantly higher median fare expenditures.

3. **Heatmap & Correlation Matrix (Bonus)**:
   * **Pearson Correlation Matrix**: Displays notable negative correlation between `Pclass` and `Survived` ($r \approx -0.34$), and positive correlation between `Fare` and `Survived` ($r \approx +0.26$).
   * **Bivariate Survival Heatmap**: Highlights that class privilege offered substantial protection, yet gender remained the dominant determinant of survival.

---

## 📂 Repository File Structure

```text
titanic-eda/
├── data/
│   └── train.csv                   # Dataset file
├── images/
│   ├── notebook_overview.png       # Screenshot: VS Code Jupyter environment
│   ├── eda_statistics.png          # Screenshot: Code output & summary tables
│   └── eda_visualizations.png      # Screenshot: Plots & correlation heatmaps
├── Titanic_EDA.ipynb               # Complete Jupyter Notebook with code & markdown
├── README.md                       # Detailed project documentation & report
└── requirements.txt                # Python package dependencies
```

---

## 🖥️ How to Add Your Screenshots from VS Code

1. In your local project folder, create a subfolder named **`images`**:
   ```bash
   mkdir images
   ```
2. Take screenshots of your notebook running in **Visual Studio Code** (using `Win + Shift + S` on Windows).
3. Save the images into the `images/` folder with these names:
   * `notebook_overview.png`
   * `eda_statistics.png`
   * `eda_visualizations.png`
4. Commit and push them to GitHub:
   ```bash
   git add images/
   git commit -m "Add notebook screenshots from VS Code"
   git push origin main
   ```
*(The markdown links above are already configured to display them automatically).*

---

## ⚙️ How to Reproduce & Run

1. **Clone the repository:**
   ```bash
   git clone https://github.com/<your-username>/titanic-eda.git
   cd titanic-eda
   ```

2. **Install the dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
   *(Or manually install: `pip install pandas numpy matplotlib seaborn jupyter`)*

3. **Open in VS Code:**
   * Open the project folder in VS Code.
   * Select your Python kernel in the top-right corner.
   * Run cells interactively (`Shift + Enter`).

---

## 📈 Summary of Findings
* **"Women and Children First"**: Maritime safety conventions heavily governed evacuation outcomes.
* **Class Disparity**: First-class passengers enjoyed preferential physical access to lifeboat decks.
* **Multivariate Synergy**: While 3rd-class females had a 50% survival rate, 1st-class females survived at nearly 97%, showing how gender and wealth compounded passenger outcomes.
