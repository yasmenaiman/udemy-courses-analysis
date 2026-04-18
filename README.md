#  Udemy Courses Analysis — EDA & Machine Learning

##  Project Goal
The goal of this project is to analyze Udemy courses data to understand
what makes a course successful, and build a machine learning model
that predicts how many subscribers a course will get.

---

##  Dataset
- 3678 Udemy courses
- Features: price, subject, level, num_lectures, content_duration,
  num_reviews, published_timestamp, is_paid

---

##  Project Pipeline

###  Step 1 — Data Cleaning
Before any analysis, the data needed cleaning:
- Removed duplicate rows
- Dropped courses with 0 lectures (illogical entries)
- Removed irrelevant columns: `course_id`, `url`
- Parsed `published_timestamp` and extracted `year` and `month`

---

###  Step 2 — Exploratory Data Analysis (EDA)

** Paid vs Free Courses**
- Visualized the distribution using a count plot and a donut chart
- Compared average subscribers between free and paid courses
- Finding: Although 91.56% of courses are paid, free courses attract
  significantly more subscribers — meaning price alone does not
  drive enrollment



** Subject Analysis**
- Analyzed the number of courses per subject
- Compared total subscribers per subject split by paid vs free
- Finding: Web Development leads in both number of courses
  and total subscribers across all subjects

** Course Level Distribution**
- Explored how courses are distributed across difficulty levels
- Finding: Most courses target "All Levels" or "Beginner" audiences,
  while "Expert Level" courses are rare

** Price Distribution**
- Plotted a histogram with KDE to understand pricing patterns
- Finding: Most prices fall between $20 and $200 with a right-skewed
  distribution, indicating a few very expensive outliers

** Relationships Between Features**
- Used scatter plots and regression plots to explore how price,
  number of lectures, and content duration relate to subscribers
- Finding: None of these features alone strongly predict subscribers —
  which motivated the feature engineering step

** Outlier Detection**
- Used boxplots to detect outliers in price, num_subscribers,
  and num_reviews
- Finding: Heavy outliers exist in num_subscribers and num_reviews —
  a small number of courses have extremely high values while
  most have very few, which is typical for online platforms



** Correlation Heatmap**
- Built a heatmap across all numeric features
- Finding: num_reviews has the strongest correlation with
  num_subscribers (0.65), while price, level, and duration
  show very weak correlation — this directly guided
  which features to prioritize in the model



** Publication Trends**
- Analyzed courses published per year and per month
- Finding: Course publications peaked in certain years,
  and January to March sees the highest publishing activity

---

###  Step 3 — Feature Engineering
Two new features were created to give the model more signal:

| Feature | Formula | Why? |
|---------|---------|------|
| `review_rate` | num_reviews / (num_subscribers + 1) | Captures engagement quality |
| `avg_lecture_duration` | content_duration / (num_lectures + 1) | Captures lecture depth |

---

###  Step 4 — Machine Learning Model

**Model:** Random Forest Regressor
**Target:** Predict `num_subscribers`
**Split:** 80% training / 20% testing

**📈 Results:**
| Metric | Value |
|--------|-------|
| MAE | 384 subscribers |
| RMSE | 2,703 subscribers |
| R² Score | **0.8887** ✅ |

> R² of 0.88 means the model explains 88% of the variation
> in subscriber counts — a strong result for this type of data.

** Most Important Features:**
The model confirmed what the EDA suggested — num_reviews is by far
the most important predictor (importance > 0.6), followed by
review_rate which was a newly engineered feature.
This means the EDA directly guided the model.


---

##  Tools Used
![Python](https://img.shields.io/badge/Python-3.10-blue)
![Pandas](https://img.shields.io/badge/Pandas-grey)
![Scikit--learn](https://img.shields.io/badge/ScikitLearn-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-teal)
![Matplotlib](https://img.shields.io/badge/Matplotlib-blue)

---

##  How to Run
1. Clone the repo
2. Make sure `udemy_courses.csv` is in the same folder
3. Open `udemy_analysis_final.ipynb` and run all cells
