# 🎓 Understanding Zero Grades

### Patterns, Associated Features, and Absence–Grade Sensitivity in Mathematics and Portuguese

> *What does a grade of **0** really mean?*
> A failed exam, a dropout, a transfer, a withdrawal, or just a missing record? The dataset doesn't say, and treating zeros as ordinary scores can quietly distort your conclusions.

![Python](https://img.shields.io/badge/Python-3.x-blue)
![Status](https://img.shields.io/badge/status-completed-brightgreen)
![License](https://img.shields.io/badge/license-MIT-lightgrey)

*Small Project of Selected Topic of Data Science, Department of Mathematics, Institut Teknologi Sepuluh Nopember (ITS) Surabaya.*

---

## 📌 Overview

Educational datasets often contain zero grades that look like normal scores but may actually mark a student **leaving the assessment**. This project investigates zero grades in the well-known [UCI Student Performance dataset](https://doi.org/10.24432/C5TG7T) (Cortez & Silva, 2008) and asks a simple but important question:

**Should a zero be analyzed as an academic grade, or as a marker of exiting the assessment?**

We examine how zeros appear across the three grading periods (G1, G2, G3), which student characteristics are associated with them, and how much they change a commonly reported finding: the relationship between **absences** and **final grades**.

## ❓ Why This Matters

- Zero final grades account for **53 records**: **9.6%** of Mathematics and **2.3%** of Portuguese students.
- The dataset has **no label** explaining what a zero means.
- Zeros sit on the same 0–20 scale as valid grades, so they **cannot be told apart by value alone**.
- Left untreated, zeros can **distort correlations** and lead to misleading conclusions.

## 🎯 Research Goals

1. **Identify zero-grade patterns** in G1, G2, and G3 across both subjects (frequency, combinations, persistence) and assess whether a zero behaves like an academic grade or like an exit marker.
2. **Explore associations** between zero grades and student characteristics (past failures, study time, learning support, and more) at comparable initial grade levels.
3. **Assess sensitivity** of the absences–final grade correlation to including or excluding students with zero final grades.

## 📊 Data

| | Mathematics | Portuguese |
|---|---|---|
| Students | 395 | 649 |
| Zero final grades (G3 = 0) | 38 (9.6%) | 15 (2.3%) |

- **Source:** [UCI Machine Learning Repository](https://doi.org/10.24432/C5TG7T), Student Performance (Cortez & Silva, 2008)
- **Schools:** two Portuguese secondary schools, Gabriel Pereira (GP) and Mousinho da Silveira (MS)
- **Features:** 33 attributes per file, covering demographic, social, and school-related factors plus the grades G1, G2, and G3
- **Origin:** grades and absences come from school reports; other attributes from questionnaires
- **Note:** the two subject files overlap and contain no student ID

## 🧩 Zero-Grade Taxonomy

| Type | Definition | Mathematics | Portuguese |
|---|---|---|---|
| **Type A** | G2 = G3 = 0 (persistent zero) | 13 | 7 |
| **Type B** | G3 = 0, G2 > 0 (zero appears at the end) | 25 | 8 |
| **Anomaly** | G1 = 0, G2 > 0, G3 > 0 | n/a | 1 |

## 🔬 Methodology

1. **Pattern analysis:** frequency, transitions, and persistence of zeros across G1 → G2 → G3.
2. **Group comparison:** Type A, Type B, and regular students compared on G1, G2, absences, and other features.
3. **Sensitivity analysis:** absences–G3 correlation under four scenarios:

| Scenario | Treatment |
|---|---|
| **S0** | All students (baseline) |
| **S1** | Exclude Type A |
| **S2** | Exclude Type B |
| **S3** | Exclude Type A & B (all zero-grade students) |

Each scenario reports **Pearson's r with 95% bootstrap confidence intervals**, with **Spearman's ρ** as a robustness check.

## 💡 Key Findings

- **Zeros follow a one-directional pattern.** Every G2 = 0 carries into G3, but a G3 = 0 can appear without an earlier zero (25 Mathematics and 8 Portuguese students still had a valid G2).
- **Zeros rarely come out of nowhere.** Most zero-grade students were already below the pass mark of 10 before their grade dropped to zero.
- **Zero-grade students look different.** They tend to differ in past failures, school, educational support, and study habits, with patterns varying between subjects.
- **The absences–grade correlation depends on how zeros are treated:**

| Subject | S0 (all data) | S3 (zeros removed) |
|---|---|---|
| Mathematics | r = +0.03 | r = −0.21 |
| Portuguese | r = −0.09 | r = −0.20 |

  In Mathematics, removing only Type A barely changes the result (r = −0.02), while removing only Type B goes further (r = −0.10). The negative association becomes clear only when both zero types are excluded.

> ⚠️ **A note on interpretation.** The dataset does not explain *why* zeros occur. They cannot automatically be classified as recording errors or invalid grades, and absenteeism should not be assumed to be the cause: students who never attend may simply have no attendance records.

## 🗂️ Repository Structure

<!-- Adjust to match your actual repository -->
```
.
├── data/              # UCI Student Performance files (student-mat.csv, student-por.csv)
├── notebooks/         # Exploratory analysis and sensitivity experiments
├── src/               # Reusable analysis scripts
├── reports/           # Presentation slides and final report
├── requirements.txt
└── README.md
```

## 🚀 Getting Started

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<your-repo-name>.git
cd <your-repo-name>

# 2. (Optional) Create a virtual environment
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Launch the notebooks
jupyter notebook
```

The dataset can be downloaded from the [UCI repository](https://doi.org/10.24432/C5TG7T) and placed in the `data/` folder.

## 👥 Team: Group 6

| Name | Student ID |
|---|---|
| Haqi Ardika Ramadani | 5002231016 |
| Reza Dwi Rahayu | 5002231049 |
| Layli Nurul Fatimah Zahra | 5002231145 |

Department of Mathematics, Institut Teknologi Sepuluh Nopember (ITS), Surabaya, Indonesia.

## 📚 References

- Cortez, P. (2008). *Student Performance* [Data set]. UCI Machine Learning Repository. https://doi.org/10.24432/C5TG7T
- Cortez, P., & Silva, A. M. G. (2008). Using data mining to predict secondary school student performance. *Proceedings of the 5th FUture BUsiness TEChnology Conference (FUBUTEC 2008)*. EUROSIS-ETI. https://repositorium.uminho.pt/handle/1822/8024
- Cowles, M., & Davis, C. (1982). On the origins of the .05 level of statistical significance. *American Psychologist, 37*(5), 553–558. https://doi.org/10.1037/0003-066X.37.5.553

## 📄 License

This project is released under the [MIT License](LICENSE). The dataset remains subject to the terms of the UCI Machine Learning Repository.
