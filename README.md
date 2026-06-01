# Multivariate Statistical Process Control of Paint Quality Indicators

---

## Overview

This repository contains a complete R Markdown assignment applying **univariate and multivariate Statistical Process Control (SPC)** methods to two paint manufacturing quality datasets. The report demonstrates how Hotelling's T² multivariate control chart detects process anomalies that individual Shewhart charts miss entirely.

The knitted report is available here:  
🔗 **[View the Full Report](https://your-username.github.io/paint-quality-spc/paint-quality-spc.md)**  
*(Replace `your-username` with your actual GitHub username after hosting)*

---

## Datasets

| Dataset | File | Variables | Observations |
|---|---|---|---|
| Dataset 1 | `Paint_data_individual.csv` | Viscosity (cP), Temperature (°C) | 100 |
| Dataset 2 | `paint_data_3vars.csv` | Viscosity (cP), Gloss (GU), Drying Time (min) | 120 |

Both datasets represent individual observations from a paint production process, with measurements taken at successive sampling points.

---

## Analyses Performed

### Dataset 1 — Bivariate (Viscosity & Temperature)
- Scatter plot with 95% Hotelling confidence ellipse
- Shewhart individuals (X) control charts for each variable
- Hotelling's T² multivariate control chart
- Comparison of univariate vs. multivariate out-of-control detections

### Dataset 2 — Trivariate (Viscosity, Gloss & Drying Time)
- Pairwise scatter plot matrix with correlation coefficients
- Shewhart individuals (X) control charts for all three variables
- Hotelling's T² multivariate control chart
- **MYT T² decomposition** — identifies which variable drives each out-of-control signal
- **Principal Component Analysis (PCA)** — scores plot with confidence ellipses

---

## Key Findings

- In Dataset 1, three observations (7, 50, 93) were flagged by the T² chart. Only one (Obs 50) was detected by the individual Shewhart charts — demonstrating the added sensitivity of multivariate monitoring.
- In Dataset 2, Obs 115 produced a T² value of **51.84** against a UCL of 14.16 — more than three times the limit — yet was invisible to all three individual charts.
- T² decomposition revealed that **Gloss** was the dominant driver of the Obs 115 signal, contributing **88%** (45.47 out of 51.84) of the total T² value.
- PCA confirmed that PC1 explains **80.4%** of total variance, with all three variables loading approximately equally — indicating a strong shared quality factor across the process.

---

## Repository Structure

```
paint-quality-spc/
│
├── Paint_Quality_SPC_Assignment.Rmd     # Main R Markdown source file
├── Paint_Quality_SPC_Code.R            # Extracted R code (standalone script)
│
├── data/
│   ├── Paint_data_individual.csv        # Dataset 1 (2 variables)
│   └── paint_data_3vars.csv            # Dataset 2 (3 variables)
│
└── README.md                           # This file
```

---

## R Packages Used

| Package | Purpose |
|---|---|
| `qcc` | Shewhart control charts (individuals X chart) |
| `ggplot2` | All custom visualisations and scatter plots |
| `GGally` | Pairwise scatter plot matrix |
| `FactoMineR` | Principal Component Analysis |
| `factoextra` | PCA visualisation (biplots, scree plots) |
| `knitr` / `kableExtra` | Table formatting in the knitted report |
| `dplyr` / `tidyr` | Data manipulation |
| `bookdown` | Multi-format output (HTML, PDF, Word) |
| `MASS` | Covariance and multivariate computations |

---

## How to Reproduce the Report

### Prerequisites

Make sure you have R (≥ 4.1) and RStudio installed. Then install the required packages:

```r
install.packages(c(
  "bookdown", "ggplot2", "qcc", "MASS", "FactoMineR",
  "factoextra", "kableExtra", "GGally", "ggExtra",
  "gridExtra", "car", "mvtnorm", "dplyr", "tidyr"
))
```

For PDF output, install TinyTeX if you do not have LaTeX:

```r
install.packages("tinytex")
tinytex::install_tinytex()
```

### Steps

1. Clone this repository:
   ```bash
   git clone https://github.com/your-username/paint-quality-spc.git
   cd paint-quality-spc
   ```

2. Open `Paint_Quality_SPC_Assignment.Rmd` in RStudio.

3. Make sure both CSV files are in the same folder as the `.Rmd` file (or inside `data/` if you adjust the file paths in the code).

4. Knit to your preferred format using the **Knit** button in RStudio, or run:
   ```r
   # HTML
   rmarkdown::render("Paint_Quality_SPC_Assignment.Rmd", output_format = "bookdown::html_document2")

   # PDF
   rmarkdown::render("Paint_Quality_SPC_Assignment.Rmd", output_format = "bookdown::pdf_document2")

   # Word
   rmarkdown::render("Paint_Quality_SPC_Assignment.Rmd", output_format = "bookdown::word_document2")
   ```

---

## Author

**Eric Ibaale**  

---

## License

The code is open for reference and learning purposes. Please do not submit it as your own academic work.
