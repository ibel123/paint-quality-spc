```markdown
---
title: "Paint Quality SPC"
author: "Eric Ibaale"
date: "June 01, 2026"
---

# 1. Group Members

**Table 1: Group 3 – Member Registration Details**

| Name                    | Registration Number | Student Number | Group |
|-------------------------|---------------------|----------------|-------|
| Mark Muganzi Joseph M   | 23/U/11525/PS       | 2300711525      | 3     |
| Jonathan Maganda        | 23/U/10933/PS       | 2300710933      | 3     |
| Eric Ibaale             | 23/U/08288/PS       | 2300708288      | 3     |
| Kenneth Lukyamuzi       | 23/U/10799/PS       | 2300710799      | 3     |
| Fred Kakungulu          | 23/U/0485           | 2300700485      | 3     |
| Grace Mahoro            | 23/U/10967/PS       | 2300710967      | 3     |
| Francis Kabila Edrias   | 22/U/6012           | 2200706012      | 3     |
| Trussy Nimusiima        | 23/U/15901/PS       | 2300715901      | 3     |
| Dorothy Nakirembe       | 23/U/13804/PS       | 2300713804      | 3     |
| Allan Matovu            | 23/U/11115/PS       | 2300711115      | 3     |
| Agnes Nakabiri          | 23/U/1000           | 2300701000      | 3     |
| Michelle Wanyana        | 23/U/1530           | 2300701530      | 3     |

# 2. Introduction

Statistical Process Control (SPC) uses data from a running process to detect unusual variation before it leads to defective output. Traditional Shewhart charts monitor one quality characteristic at a time. When several characteristics are measured simultaneously and are correlated with each other, monitoring them independently inflates the chance of false alarms and can miss joint deviations that no single chart would catch. Hotelling's $T^2$ statistic extends the univariate Shewhart approach to multiple variables by incorporating the full covariance structure, giving a single sensitive signal for multivariate out-of-control conditions.

This report applies both approaches to two paint quality datasets: a bivariate dataset (viscosity and temperature, $n = 100$) and a trivariate dataset (viscosity, gloss, and drying time, $n = 120$).

# 3. Dataset 1: Bivariate Analysis (Viscosity and Temperature)

## 3.1 Loading Data

Data loaded from `Paint_data_individual.csv` containing columns: Sample, Viscosity, Temperature.

## 3.2 Scatter Plot with 95% Confidence Ellipse

**Figure 1: Scatter plot of Viscosity vs. Temperature with 95% Hotelling confidence ellipse. Red points fall outside the ellipse and are flagged as multivariate outliers.**

The ellipse is oriented along a negative diagonal, confirming the expected inverse relationship between viscosity and temperature. Points labelled outside the ellipse represent observations whose combined values are statistically unusual relative to the multivariate mean, even though individual variables might appear within their own univariate limits. These multivariate outliers are the primary targets for the Hotelling's $T^2$ analysis.

## 3.3 Univariate Shewhart Individuals (X) Control Charts

### 3.3.1 Viscosity – Individuals Chart

**Figure 2: Shewhart Individuals (X) chart for Viscosity (Dataset 1).**

The viscosity chart reveals a strong upward trend across the 100 samples. Because the individuals chart uses a moving-range estimate of $\sigma$, the control limits are narrow. The systematic drift across the chart rather than random scatter around the centre line suggests a non-stationary process. This long-run trend warrants investigation into raw material batch changes or equipment drift over the production run.

- **Viscosity chart – Points beyond control limits:** None  
- **Center (mean):** 99.9993  
- **UCL:** 128.9397  
- **LCL:** 71.0589

### 3.3.2 Temperature – Individuals Chart

**Figure 3: Shewhart Individuals (X) chart for Temperature (Dataset 1). Out-of-control points are highlighted in red.**

Temperature is generally stable across the run, with one exception: Obs 50 (recorded at 32.0 °C) exceeds the UCL of 30.45 °C. This observation represents a genuine process upset where the temperature exceedance alone is sufficient to explain its out-of-control status.

- **Temperature chart – Points beyond control limits:** 50  
- **Center (mean):** 25.021  
- **UCL:** 30.4523  
- **LCL:** 19.5897

## 3.4 Hotelling's T² Control Chart

**Figure 4: Hotelling's $T^2$ control chart for Viscosity and Temperature jointly. The red dashed line denotes the UCL based on the chi-squared approximation (Phase II). Points above the UCL are flagged as multivariate out-of-control.**

**Table 2: Out-of-Control Observations – Hotelling $T^2$ (Dataset 1)**

| Sample | Viscosity (cP) | Temperature (°C) | T² Value | Mahalanobis Distance |
|--------|----------------|------------------|----------|----------------------|
| 7      | 105.0          | 22.0             | 12.2353  | 3.4979               |
| 50     | 95.0           | 32.0             | 12.0213  | 3.4672               |
| 93     | 105.0          | 30.0             | 12.6247  | 3.5531               |

The $T^2$ chart identifies three out-of-control observations (7, 50, 93) against a UCL of 11.829. All three appear to record set-point values (round numbers in both variables), suggesting they may correspond to calibration checks or deliberately altered process conditions. Obs 93, with the highest $T^2$ of 12.625, records viscosity at 105.0 cP and temperature at 30.0 °C — a combination that lies well outside the joint in-control region. Notably, Obs 7 and 93 are not flagged by the temperature chart, demonstrating the added sensitivity of the multivariate approach.

## 3.5 Univariate vs. Multivariate Comparison

The temperature chart flags only Obs 50 (temperature = 32 °C, beyond UCL of 30.45). The $T^2$ chart flags all three: Obs 50 is caught by both, while Obs 7 and 93 are detected only through multivariate monitoring. This illustrates the core advantage of $T^2$: it accounts for correlation between variables and can detect joint deviations that a pair of individual charts would miss entirely.

# 4. Dataset 2: Trivariate Analysis (Viscosity, Gloss and Drying Time)

## 4.1 Data Loading

Data loaded from `paint_data_3vars.csv` containing columns: Viscosity, Gloss, DryingTime.

## 4.2 Pairwise Scatter Plots

**Figure 5: Pairwise scatter plot matrix for all three paint quality variables in Dataset 2. The lower triangle shows bivariate scatter with LOESS smoothing; diagonal panels show marginal density plots; the upper triangle shows Pearson correlation coefficients.**

All three pairs exhibit strong positive correlations, with viscosity and drying time sharing the strongest association ($r = 0.86$). This is consistent with paint chemistry: higher-viscosity formulations retain solvent longer and consequently take more time to dry. These substantial correlations mean that monitoring the three variables independently would produce correlated false-alarm signals and would not correctly represent the joint process state.

## 4.3 Univariate Shewhart Control Charts

**Figure 6: Individuals chart for Viscosity (Dataset 2).**  
**Figure 7: Individuals chart for Gloss (Dataset 2).**  
**Figure 8: Individuals chart for Drying Time (Dataset 2).**

- **Viscosity OOC points:** None  
- **Gloss OOC points:** None  
- **Drying Time OOC points:** 18

The viscosity and gloss charts show no out-of-control points and both appear stable. The drying time chart flags Obs 18, which is a borderline univariate signal.

## 4.4 Hotelling's T² Control Chart

**Figure 9: Hotelling's $T^2$ control chart for the trivariate paint quality dataset. Red points exceed the chi-squared UCL and are flagged as multivariate out-of-control signals.**

**Table 3: Out-of-Control Observations – Hotelling $T^2$ (Dataset 2)**

| Sample | Viscosity (cP) | Gloss (GU) | Drying Time (min) | T² Value |
|--------|----------------|------------|-------------------|----------|
| 18     | 102.0          | 84.0       | 72.0              | 15.4295  |
| 115    | 105.0          | 72.5       | 74.0              | 51.8402  |

Obs 115 produces a $T^2$ value of 51.84 — more than three and a half times the UCL of 14.157. This is a severe multivariate signal. The observation combines above-average viscosity, notably below-average gloss, and above-average drying time. While each measurement is within its own univariate limits, it is the unusual pattern across all three simultaneously — specifically, high viscosity paired with low gloss — that drives the extreme $T^2$ value. The decomposition analysis below identifies the variable primarily responsible.

# 5. T² Decomposition Analysis

A critical advantage of the multivariate $T^2$ chart is the ability to decompose an out-of-control signal to identify which variable(s) are responsible. We applied the **MYT (Mason--Young--Tracy) decomposition**, which partitions $T^2$ into independent, interpretable components.

The decomposition is based on conditional $T^2$ values: for each out-of-control observation, the contribution of each variable is computed by comparing the full $T^2$ to a reduced $T^2$ obtained by removing that variable. A large reduction indicates that the removed variable contributes substantially to the signal.

**Table 4: $T^2$ Decomposition – Variable Contributions for Out-of-Control Observations**

| Sample | T² Total | Viscosity ΔT² | Visc % | Gloss ΔT² | Gloss % | Dry Time ΔT² | Dry % | Dominant Variable |
|--------|----------|---------------|--------|-----------|---------|--------------|-------|-------------------|
| 18     | 15.4295  | 6.8828        | 44.61  | 5.5231    | 35.80   | 3.0236       | 19.60 | Viscosity         |
| 115    | 51.8402  | 10.4323       | 20.12  | 45.4698   | 87.72   | -4.0619      | -7.84 | Gloss             |

## 5.1 Decomposition Visualisation

**Figure 10: Stacked bar chart showing the absolute $T^2$ contributions of each variable for every out-of-control observation in Dataset 2. The dashed horizontal line represents the UCL; bars are coloured by contributing variable.**

Gloss accounts for 88% of the total $T^2$ signal. The recorded gloss of 72.5 GU is markedly below the process mean of 80.1 GU, and when this deviation is evaluated within the full covariance context, it generates a contribution of 45.47 to the $T^2$ statistic. In practical terms, this observation exhibits a gloss level far too low for its level of viscosity. The paint appears to have dried with reduced surface reflectance despite high viscosity, which could indicate a problem with pigment dispersion, film formation, or substrate interaction at this particular production point. Viscosity contributes a secondary 20%, and drying time is not a meaningful driver of the signal.

# 6. Conclusion

The two datasets together demonstrate that multivariate monitoring provides a materially richer and more reliable picture of process behaviour than univariate Shewhart charts alone. In Dataset 1, three observations (Obs 7, 50, and 93) were flagged by Hotelling's $T^2$, while only one (Obs 50) was caught by the individual temperature chart; viscosity and temperature, treated separately, gave almost no useful signal despite the process being out of control. In Dataset 2, all three univariate charts were clean apart from a marginal flag on drying time, yet the $T^2$ chart identified Obs 115 with a statistic of 51.84 — more than three times the UCL. The $T^2$ decomposition revealed that gloss was overwhelmingly responsible for this signal (88% of $T^2$), pointing to a specific formulation or surface-quality issue at that production point. Overall, the process in both datasets is largely stable, but the multivariate approach is clearly necessary to detect the anomalies that univariate monitoring would leave undetected.
```
