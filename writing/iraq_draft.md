# Iraq Displacement Modelling

*Working draft prepared by by Chungmann Ki*

*Last updated: 2026-05-29.*

## 1. Introduction (Placeholder)

- **Motivation:** Iraq experienced one of the largest internal displacement crises with peak IDP stocks exceeding xx million during the 2014–2017 Islamic State (IS) conflict.
- **Gap:** Existing literature focuses on conflict as the primary driver.
- **Research question:** What are the relative contributions of conflict, climate, and economic shocks to IDP accumulation (Refugee and Returnee movement) in Iraq by region, and how do these channels operate through local conditions versus spatial spillovers from neighboring districts?
- **Contribution:**
  - First district-month panel covering the full 2014–2024 IDP cycle in Iraq (N ≈ 100 districts × 81 months; Al-Salman excluded — no IDP data; months with no data across all districts dropped)
  - Explicit decomposition of own-district vs. spatial-neighbor effects using a travel-time-based weights matrix
  - Time-split analysis to reveal a structural transition of drivers
  - Evidence that spatial spillovers dominate local effects in the North — regional pressure, not local shocks, explains most of the variation.

---

## 2. Background (Placeholder)

### Iraq context (Sani's input needed)
- Post‑2003 political fragmentation and state fragility.
- 2014 IS territorial expansion triggered mass internal displacement; peak IDP stocks were ~3.4 million in 2014
- Geography: KRI as a major receiver, IS‑affected governorates (Ninewa, Anbar, Salah al‑Din, Kirkuk, Diyala) as primary origins.
- Economy: oil‑dependent revenues, fragmented labor markets, and household exposure to fuel/food subsidy changes?
- Climate: largely arid/semi‑arid?

### Literature notes
- Conflict–displacement: works related to conflict is a principal push factor, but few studies use subnational panel designs
- Climate–displacement: drought, heat, and crop shocks link to mobility?
- Spatial spillovers: neighboring shocks shape local displacement decisions and motivate spatial lag specifications?
- Iraq evidence: extensive operational reporting (IOM, UNHCR, ICG) but limited econometric ADM2 panel analyses
- Gap this paper fills: a district‑month FE panel with travel‑time spatial weights, simultaneous conflict/climate/economic channels, and a pre/post‑2018 regime comparison
---

## 3. Conceptual Framework (Placeholder)

### Core Mechanisms

Displacement decisions emerge from the intersection of three broad categories stress: physical insecurity arising from armed conflict, livelihood disruption driven by climate variability or weather shocks (e.g. drought and flood), and erosion of market access reflected in food and fuel price movements. They tend to interact to shape whether and when households choose—or are forced—to leave their place of origin.

### Spatial Spillovers

What motivates our the empirical design is that displacement decisions are not confined to the conditions prevailing within a household's own district. Shocks originating in neighboring administrative units can affect local mobility.

---

## 4. Study design

### 4.1 Unit of analysis
- The unit of analysis is the ADM2 district-month.
- The analytical window spans April 2014 to August 2024.
- After harmonization to a common ADM2 P-code framework, the working panel contains 100 districts and 8,100 district-month observations.
  - Al-Salman is excluded because no IDP data are available.
  - Months with no usable data across districts are dropped from the estimation sample; Appendix Figure A1a shows the month-coverage diagnostic that motivates this restriction.

### 4.2 Outcomes (IDP focus)
- The primary outcome is `ln_idp`, defined as `log(IDP stock + 1)`.
- IDP stock data are drawn from IOM DTM, with values prioritized in the order `raw > API > interpolated`.
- A secondary outcome, `dlog_idp`, captures the month-to-month change in `ln(IDP + 1)` and is used to approximate short-run flow dynamics.
- Additional outcomes, including returnee and refugee stock measures, can be incorporated in later iterations once those series are finalized.

### 4.3 Spatial logic
- The empirical design jointly estimates own-district and neighboring-district associations.
- The own-district effect captures the association between `X_{d,t-\tau}` and the outcome in district `d`.
- The neighbor or spillover effect captures the association between the spatially weighted average `WX_{d,t-\tau}` and the outcome in district `d`.

### 4.4 Temporal logic
- We allow both shorter-run and longer-run associations to emerge in the estimates.
- Shorter-run effects are captured through lag windows `L1-3` and `L4-6`.
- Longer-run effects are captured through lag windows `L7-9` and `L10-12`.

### 4.5 Spatial weights matrix (W)
- The spatial weights matrix is constructed from the Iraq road network using OSMnx.
- ADM2 centroids are snapped to network nodes, and shortest-path travel times are computed between districts.
- Travel times are converted to proximity weights using `w_{ij} = 1 / T_{ij}`, truncated to the `k` nearest neighbors, and then row-normalized.
- The main specification uses `K = 30`; robustness checks use `K = 50` and `K = ALL`.

> **Figure 1.** Iraq administrative districts (ADM2) by North/South classifications.

![Figure 1: Iraq North/South Classifications](../results/figures/iraq_classification_north.png)

*Note: The figure illustrates the North/South distinction used for stratification. Models use the regional split listed below ("South" vs "Central & North").*

### 4.5 Regional stratification

Models are estimated separately for two regional groups (ref. Mac Skelton):

- **South (9 governorates):** Wassit, Thi Qar, Al‑Basrah, Al‑Muthanna, Al‑Najaf, Maysan, Al‑Qadissiya, Kerbala, Babil
- **Central & North (9 governorates):** Ninewa, Al‑Anbar, Salah al‑Din, Kirkuk, Diyala, Baghdad, Duhok, Erbil, Al‑Sulaymaniyah

*The figure above illustrates the North/South distinction used for the analysis.*

---

## 5. Data Overview

### 5.1 Outcome Variables

**Table 1. Outcome Variables**

| Variable | Source | Definition | Obs | Coverage |
|----------|--------|-----------|-----|----------|
| IDP Stock | IOM DTM (raw + API) | log(IDP count + 1) | District-month | Apr 2014 – Aug 2024 |
| IDP Change  | IOM DTM | Month-over-month Δln(IDP+1) | District-month | Apr 2014 – Aug 2024 |
| Returnee Stock  | UNHCR / IOM DTM | log(returnee count + 1) | District-month | Partial 2017–2024 |
| Returnee Change  | UNHCR / IOM DTM | Month-over-month Δln(returnee+1) | District-month | Partial 2017–2024 |

*Note: IDP records reconciled from two overlapping sources (raw DTM + API) via hierarchical priority rule: raw hand-coded values preferred, then API values, then linear interpolation for residual gaps.*

### 5.2 Conflict Measures

- Georeferenced event data from UCDP [CITE: UCDP GED, Sundberg & Melander 2013], aggregated to district-month level
- Key variables: total battle-related deaths, total conflict events
- Zero-conflict months assigned 0 (not missing) - 13 districts; entered as log(x+1) in main specs

### 5.3 Climate Measures

- **SPI-6** [CITE: McKee et al. 1993]: Standardized Precipitation Index (6-month), from CHIRPS [CITE: Funk et al. 2015]; values <−1.3 = drought; >+1.3 = excess moisture
- **Temperature anomaly**: Monthly maximum temperature deviation from long-run calendar-month mean, ERA5-Land [CITE: Hersbach et al. 2020]
- **NDVI anomaly**: Vegetation greenness deviation from baseline, MODIS [CITE: Didan 2015]
- **Soil moisture anomaly**: Top-layer soil moisture deviation, ERA5-Land

### 5.4 Economic Measures

- **Food price inflation**: month-over-month % change in district-level food price basket [CITE: WB price estiamtes, Bo Andree]
- **Fuel gas price** (log-transformed): district-level or nearest-market quote [CITE: WB price estiamtes, Bo Andree]

### 5.5 Descriptive Statistics

**Table 2. Key Descriptive Statistics by Region** *(Apr 2014 – Aug 2024)*

| Variable | North Mean (SD) | North Coverage | South Mean (SD) | South Coverage |
|----------|----------------|---------------|----------------|---------------|
| IDP stock (raw count) | 33,697 (60,357) | 99.6% | 4,377 (10,269) | 100% |
| Conflict deaths | 10.4 (63.7) | 100% | 0.5 (9.9) | 100% |
| Conflict events | 0.71 (3.00) | 100% | 0.02 (0.17) | 100% |
| SPI-6 | 0.27 (1.11) | 100% | 0.26 (1.12) | 100% |
| Temperature anomaly (max, °C) | 0.62 (2.04) | 100% | 0.72 (2.10) | 100% |
| NDVI anomaly | 0.010 (0.046) | 100% | 0.008 (0.029) | 100% |
| Soil moisture anomaly | 0.004 (0.044) | 100% | 0.002 (0.038) | 100% |
| Flood severity (SPI-based) | 2.25 (6.10) | 100% | 2.56 (6.91) | 100% |
| Drought severity (SPI-based) | 0.62 (2.33) | 100% | 0.56 (2.27) | 100% |
| Food price inflation (%) | 0.36 (5.57) | 100% | 0.21 (6.11) | 100% |
| Fuel gas price | 7,743 (647) | 100% | 6,502 (617) | 100% |

*N = 4,860 obs (60 districts × 81 months) for North; N = 3,240 obs (40 districts × 81 months) for South. Full distributional statistics in Appendix Table A1.*

### 5.6 Spatiotemporal Patterns

> **Figure 2.** IDP stock dynamics 2014–2024, by region. Mean ln(IDP+1) across districts by month, with ±1 SD band and individual district traces. Dashed vertical line marks the 2018 structural break.

![Figure 2: IDP Stock Trends](../results/figures/fig1_idp_trend.png)

- **North:** Pronounced peak in 2014–2016 (IS occupation); gradual decline through 2019; stabilization post-2020. High between-district variance throughout
- **South:** Lower baseline, more diffuse temporal variation, continued idp resolvement post-2018
- The 2017(2016-2018) break is visually clear in the North time series and motivates the pre/post regime split

> **Figure 3.** Conflict indicators (e.g., conflict events, conflict-induced deaths, conflict incidences) by district and month, North vs South. Rows = ADM2 districts (grouped by governorate); columns = months. YlOrRd colormap; gray = no data.

![Figure 3: Conflict Heatmaps](../results/figures/conflict_north_south_heatmaps.png)

- **North:** Geographically concentrated conflict intensity in 2014–2017, particularly in Ninewa, Salah Al-Din, Anbar, Kirkuk, and Diyala. Few changes in volume Post 2018 with some reported deaths in Duhok and Erbil.
- **South:** Sparse and episodic conflict throughout; no sustained high-intensity periods
- The geographic and temporal differences between North and South supports the regional stratification decision

---

## 6. Data Handling and Measurement

### 6.1 Harmonization: P-Code Alignment

All data sources were unified to a common ADM2 geographic reference by constructing a master district list from Iraq P-codes combined with GeoBoundaries shapefiles [CITE: GeoBoundaries]. Each source was cross-walked to this master list, with naming inconsistencies resolved through exact and fuzzy string matching followed by manual review.

### 6.2 IDP Reconciliation (Raw vs. API)

IDP records were classified as: exact match, minor mismatch, major mismatch, source-specific absence. Priority rule applied: raw hand-coded values → API values → linear interpolation within district.

### 6.3 Outcome Transformations

- `ln_idp = log-transformed IDP` — accounts for zeros; percentage-change interpretation of coefficients
- `dlog_idp = ln_idp(t) − ln_idp(t−1)` — isolates monthly flow dynamics; differences out time-invariant district characteristics

### 6.4 Temporal Lag Construction

Lagged predictors constructed at windows L ∈ {1–3, 4–6, 7–9, 10–12} months (quarterly-block averages), requiring all lags within a window to be non-missing. Interpretation:
- L1–3: immediate displacement response (~1 quarter)
- L4–6: logistical preparation?
- L7–9: medium-term shock propagation
- L10–12: long-term impact

### 6.5 Spatial Lag Construction

For any district-level variable \(X\), the spatial lag is defined as:

$$
WX_{d,t} = \sum_{j \neq d} W_{dj} \cdot X_{j,t}
$$

In practice, spatial lags are computed through matrix multiplication, \(\mathbf{WX} = \mathbf{W} \times \mathbf{X}\), after reshaping each variable into a district-by-month matrix and then converting the result back to long format. The same lag windows used for own-district covariates are applied to the spatial lag terms so that local and neighboring exposures remain directly comparable across specifications.

| Figure a. Drivable road network of Iraq | Figure b. Example spatial connectivity from Al-Basrah |
|---|---|
| ![OpenStreetMap road network](../results/figures/open_street_map_drive.png) | ![Spatial connectivity from Al-Basrah](../results/figures/spillover_al_basrah_k_comparison.png) |
| *The national drivable road network extracted from OpenStreetMap using OSMnx. This network provides the basis for computing shortest-path travel times between ADM2 district centroids and, in turn, the spatial weights matrix \(W\).* | *This figure illustrates how the travel-time-based spatial weights matrix links Al-Basrah to neighboring districts under different values of \(K\). Arrow width and intensity reflect normalized inverse travel-time weights, showing how the effective neighborhood expands as more connected districts are retained.* |

---

## 7. Empirical Strategy

### 7.1 Main Estimating Framework

The empirical analysis uses a two-way fixed-effects panel model with both own-district and neighboring-district exposures. In the default specification, all included indicators enter at two common temporal horizons: a short-run window (`L1-3`) and a longer-run window (`L10-12`).

$$	
\ln(\text{IDP}_{d,t}) =
\alpha + \gamma_d + \lambda_t + \rho \ln(\text{IDP})_{d,t-1}
+ \sum_{n=1}^{k} \sum_{\tau \in \{\text{L1-3}, \text{L10-12}\}}
\left(
\beta_{1n\tau}^{own} X_{n,d,t-\tau}
+
\beta_{2n\tau}^{neigh} WX_{n,d,t-\tau}
\right)
+ \epsilon_{d,t}
$$

where:

- \(d\) indexes districts and \(t\) indexes months.
- \(\alpha\) is the intercept.
- \(\gamma_d\) denotes district fixed effects, which absorb time-invariant district characteristics such as geography, baseline population structure, and pre-crisis infrastructure.
- \(\lambda_t\) denotes month fixed effects, which absorb nationwide shocks, macroeconomic conditions, and seasonality common to all districts.
- \(W\ln(\mathrm{IDP})_{d,t-1}\) is the one-period lagged spatially weighted average of neighboring districts’ logged IDP stocks.
- \(\rho\) captures spatial persistence in displacement stocks across connected districts.
- \(X_{n,d,t-\tau}\) is the own-district exposure for indicator \(n\), evaluated at lag window \(\tau \in \{\text{L1-3}, \text{L10-12}\}\).
- \(WX_{n,d,t-\tau}\) is the neighboring-district exposure for the same indicator, evaluated at the same lag window \(\tau\).
- \(\beta_{1n\tau}^{\mathrm{own}}\) measures the association between local exposure and local IDP stock at horizon \(\tau\).
- \(\beta_{2n\tau}^{\mathrm{neigh}}\) measures the association between neighboring exposure and local IDP stock at horizon \(\tau\).
- \(\epsilon_{d,t}\) is the error term.

Standard errors are clustered at the district level throughout.

### 7.2 Interpretation of the Local and Spillover Terms

The model is designed to distinguish two conceptually different channels for each indicator.

- The own-district term captures whether conditions within district \(d\) are associated with IDP stock accumulation in that same district.
- The spatial-lag term captures whether conditions in connected neighboring districts are associated with IDP stock accumulation in district \(d\).

This distinction is central to the paper’s design. For every included indicator, the specification allows both a local association and a regional spillover association to enter simultaneously.

### 7.3 Fixed Lag Structure

The main specification imposes a common temporal structure across all indicators rather than selecting different lag windows variable by variable.

Specifically, each own-district and spatial-neighbor term enters twice:

- once at `L1-3`, representing short-run exposure
- once at `L10-12`, representing longer-run exposure

This fixed-lag design is used to make coefficients more directly comparable across indicators and across own versus spatial channels. It also reduces dependence on variable-specific lag optimization, which can otherwise make cross-indicator comparison harder to interpret.

As a result, the final specification includes:
- both own-district and spatial-neighbor terms for each included indicator
- both shorter-run (`L1-3`) and longer-run (`L10-12`) terms for each indicator
- the same temporal structure across thematic blocks, regions, and sample splits

Alternative lag windows (`L4-6` and `L7-9`) are retained for sensitivity checks and exploratory diagnostics, but they are not part of the default estimating framework reported here.

### 7.4 Three Thematic Blocks

The full estimating framework is implemented through three nested thematic blocks based on the reduced indicator set used in the fixed-lag specification.

- **B1 (Conflict only):** log conflict deaths, included as both own-district and spatial-neighbor terms at `L1-3` and `L10-12`.
- **B2 (+ Climate):** B1 plus SPI-based flood severity, SPI-based drought severity, maximum temperature anomaly, NDVI anomaly, and soil moisture anomaly, again each included as both own-district and spatial-neighbor terms at `L1-3` and `L10-12`.
- **B3 (+ Economic):** B2 plus food price inflation, included as both own-district and spatial-neighbor terms at `L1-3` and `L10-12`.

Thus, the B3 specification is the full model, while B1 and B2 are restricted versions used to assess how explanatory power changes as additional thematic channels are added.

### 7.5 Regional Stratification and Sample Splits

All models are estimated separately for North and South Iraq.

For each region, three samples are considered:

- **Pooled:** April 2014 to August 2024
- **Pre-break:** April 2014 to December 2017
- **Post-break:** January 2018 to August 2024

The January 2018 break is motivated by the near-complete territorial defeat of IS and the sharp decline in conflict intensity visible in Figure 3.

This regional and temporal stratification allows the analysis to assess whether:
- the relative importance of conflict, climate, and economic indicators differs across North and South Iraq
- the balance between own-district and spillover associations changes between the conflict-intensive and post-conflict periods

---

## 8. Robustness and Model Extensions

- **Alternative K:** K = 50 and K = 100 neighbors tested alongside main K = 30 (see Appendix Figure C1–C2)
- **Alternative lag windows:** individual lag coefficients plotted across all four windows to test stability (Appendix Figure C3–C4)
- **dlog_idp outcome:** all main regressions repeated for monthly change outcome (Appendix Figures B3–B4)
- **Planned extensions:** interaction terms with district characteristics (population size, pre-crisis IDP stock, urbanization); alternative W matrices based on adjacency or urbanization [CITE: to add]

---

## 9. Results

### 9.1 Descriptive: IDP Stock Dynamics

- North Iraq IDP stock peaked in late 2014–early 2016, corresponding to the IS territorial expansion [CITE: IOM DTM 2014–2016 reports]
- Mean ln(IDP+1) in the North ≈ 5× higher than the South over the pooled period (raw mean: 33,697 vs. 4,377)
- The 2018 structural break is clearly visible in the North time series: a sharp inflection point corresponding to IS defeat and early-phase return movements
- Post-2018 North dynamics show partial stabilization, not monotonic return — consistent with protracted displacement literature [CITE: Jacobsen / UNHCR protracted displacement]
- South shows low but persistent IDP levels throughout, with modest post-2018 accumulation — likely driven by secondary displacement from the North and climate-induced livelihood shocks

### 9.2 Lag Selection and Model Fit

> **Figure 4.** Own-district vs. spatial-neighbor lag signal (pooled sample, K=30). Grouped bars show max |t-statistic| for each predictor; dashed line = p=0.10 threshold.

![Figure 4: Own vs Spatial Signal](../results/figures/fig3_own_vs_spatial.png)

**Key findings from lag selection:**
- For conflict variables in the North, spatial lags consistently exceed own-district lags in signal strength — regional pressure precedes local outbreak 
- For economic variables in the South, own-district lags dominate — local market conditions matter more than neighbor spillovers for livelihood-driven displacement
- Climate variables show mixed patterns — temperature and flood severity have strong spatial signals; drought and NDVI more local

**Figure 5.** Within-\(R^2\) progression by thematic block for North and South Iraq. Lines show \(R^2\) at B1 (conflict), B2 (+climate), and B3 (+economic) for pooled, pre-break, and post-break samples, separately for IDP stock and IDP change outcomes.

| **North Iraq** | **South Iraq** |
|---|---|
| ![Figure 5: R² Progression North](../results2/figures/fig4_r2_progression_north.png) | ![Figure 5: R² Progression South](../results2/figures/fig4_r2_progression_south.png) |

**Table 3. Within-R² by Block, Sample, and Region**

| Region | Sample | N | B1 (Conflict) | B2 (+Climate) | B3 (+Econ) | Δ B1→B3 |
|--------|--------|----:|--------------:|--------------:|-----------:|---------:|
| North | Pooled | 4,140 | 0.892 | 0.893 | **0.893** | +0.001 |
| North | Pre-2018 | 1,920 | 0.846 | 0.848 | **0.849** | +0.003 |
| North | Post-2018 | 2,220 | 0.822 | 0.826 | **0.826** | +0.004 |
| South | Pooled | 2,760 | 0.908 | 0.909 | **0.910** | +0.002 |
| South | Pre-2018 | 1,280 | 0.671 | 0.690 | **0.693** | +0.022 |
| South | Post-2018 | 1,480 | 0.891 | 0.894 | **0.898** | +0.007 |

*All values are taken from the Stage B model output for `ln_idp`. Within-\(R^2\) is reported from the two-way fixed-effects specifications.*

- Model fit is high for `ln_idp` throughout, with within-\(R^2\) ranging from `0.671` to `0.910`; this likely reflects the strong explanatory role of district fixed effects, month fixed effects, and displacement persistence.
- Adding climate and economic blocks improves fit only modestly in North (`+0.001` to `+0.004`), but more noticeably in South, especially pre-2018 (`+0.022`).

### 9.3 Main Coefficient Estimates (B3 Full Model, ln_idp)

> **Figure 6.** Forest plot — North Iraq, IDP stock (ln_idp), B3 full model. Three columns: pooled / pre-2018 / post-2018. Bars = standardized β (90% CI); filled = p<0.10, grey = p≥0.10. Y-axis color-coded by theme: red = conflict, blue = climate, green = economic.

![Figure 6: Forest Plot North ln_idp](../results2/figures/fig5_forest_north_ln_idp.png)

> **Figure 7.** Forest plot — South Iraq, IDP stock (ln_idp), B3 full model. Same layout as Figure 6.

![Figure 7: Forest Plot South ln_idp](../results2/figures/fig5_forest_south_ln_idp.png)
**Table 4. Significant Coefficients from the B3 Full Model for `ln_idp`** *(p < 0.05; raw coefficients with clustered SEs)*

**Panel A. North Iraq**

| Sample | Theme | Variable | Exposure | Lag window | β | SE | p-value |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Pooled | Conflict | Deaths (log) | Spatial | L1–3 | +0.1970 | 0.0619 | 0.001 |
| Pooled | Climate | Drought severity | Spatial | L10–12 | +0.0378 | 0.0184 | 0.040 |
| Pooled | Climate | Flood severity | Spatial | L1–3 | +0.0195 | 0.0095 | 0.040 |
| Pooled | Climate | Flood severity | Spatial | L10–12 | -0.0147 | 0.0073 | 0.043 |
| Pooled | Climate | Soil moisture | Own | L10–12 | +0.9259 | 0.4421 | 0.036 |
| Pooled | Climate | Soil moisture | Spatial | L1–3 | -2.7152 | 1.2876 | 0.035 |
| Pooled | Climate | Temp anomaly (max) | Own | L1–3 | +0.0343 | 0.0139 | 0.014 |
| Pre-2018 | Conflict | Deaths (log) | Spatial | L1–3 | +0.1896 | 0.0726 | 0.009 |
| Pre-2018 | Conflict | Deaths (log) | Spatial | L10–12 | -0.2833 | 0.1207 | 0.019 |
| Pre-2018 | Climate | Flood severity | Spatial | L1–3 | +0.0975 | 0.0395 | 0.014 |
| Pre-2018 | Climate | NDVI anomaly | Spatial | L10–12 | +5.8411 | 2.5498 | 0.022 |
| Pre-2018 | Climate | Temp anomaly (max) | Own | L1–3 | +0.0750 | 0.0316 | 0.018 |
| Pre-2018 | Climate | Temp anomaly (max) | Spatial | L10–12 | -0.1763 | 0.0861 | 0.041 |

**Panel B. South Iraq**

| Sample | Theme | Variable | Exposure | Lag window | β | SE | p-value |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Pooled | Conflict | Deaths (log) | Spatial | L10–12 | +0.2589 | 0.0851 | 0.002 |
| Pooled | Climate | NDVI anomaly | Spatial | L1–3 | -3.0846 | 1.4821 | 0.038 |
| Pooled | Climate | Soil moisture | Spatial | L1–3 | -1.7409 | 0.7664 | 0.023 |
| Pooled | Climate | Temp anomaly (max) | Own | L10–12 | +0.0230 | 0.0085 | 0.007 |
| Pooled | Economic | Food inflation | Own | L10–12 | +0.0014 | 0.0006 | 0.015 |
| Pre-2018 | Climate | Flood severity | Own | L1–3 | +0.0308 | 0.0100 | 0.002 |
| Pre-2018 | Climate | Flood severity | Own | L10–12 | -0.0500 | 0.0146 | 0.001 |
| Pre-2018 | Climate | Flood severity | Spatial | L10–12 | +0.0862 | 0.0334 | 0.010 |
| Pre-2018 | Climate | Soil moisture | Own | L1–3 | +1.7524 | 0.7674 | 0.023 |
| Pre-2018 | Climate | Temp anomaly (max) | Own | L10–12 | +0.0442 | 0.0149 | 0.003 |
| Post-2018 | Climate | NDVI anomaly | Own | L1–3 | +0.4320 | 0.1591 | 0.007 |
| Post-2018 | Climate | NDVI anomaly | Spatial | L1–3 | -3.0249 | 1.0273 | 0.003 |
| Post-2018 | Climate | Temp anomaly (max) | Spatial | L10–12 | -0.1007 | 0.0436 | 0.021 |
| Post-2018 | Economic | Food inflation | Own | L1–3 | +0.0022 | 0.0007 | 0.002 |
| Post-2018 | Economic | Food inflation | Own | L10–12 | +0.0022 | 0.0006 | 0.000 |
| Post-2018 | Economic | Food inflation | Spatial | L10–12 | +0.0090 | 0.0035 | 0.010 |

*Raw coefficients (`β`) and clustered standard errors are reported from the B3 specification. Full coefficient outputs are available in Appendix Table A2 (`model_results_b3_ln_idp.csv`); `dlog_idp` results are reported in Appendix Table A3.*

### 9.4 Regional and Temporal Comparison

**Table 5. North vs. South Summary — Pooled Sample, ln_idp, B3 Full Model**

| Dimension | North | South |
|-----------|-------|-------|
| Pooled significant terms (total) | 7 | 5 |
| Pooled conflict terms | 1 (`Deaths`, spatial, `L1–3`) | 1 (`Deaths`, spatial, `L10–12`) |
| Pre-2018 dominant pattern | Spatial conflict plus mixed climate | Climate-only |
| Post-2018 dominant pattern | No coefficients at p < 0.05 | Climate plus food inflation |
| Largest pooled coefficient (abs. β) | Spatial soil moisture `L1–3`: `−2.715` | Spatial NDVI `L1–3`: `−3.085` |
| Largest post-break coefficient (abs. β) | None at p < 0.05 | Spatial NDVI `L1–3`: `−3.025` |

### 9.5 Synthesis

**Finding 1: The North and South differ mainly in timing and thematic mix.** In the pooled results, both regions show a spatial conflict term, but the North retains a stronger pre-2018 conflict pattern while the South looks more climate-linked and, after 2018, more tied to food inflation.

**Finding 2: The pre/post break is much clearer in the South than in the North.** In the North, pre-2018 combines spatial conflict with mixed climate terms, but post-2018 no coefficient remains significant at `p < 0.05`. In the South, post-2018 climate and food-inflation predictors remain visible, while conflict drops out of the significant set.

**Finding 3: Spillovers stand out more than local effects.** Several of the largest pooled coefficients in both regions come from neighboring rather than own-district variables, especially neighboring soil moisture in the North and neighboring NDVI in the South, which reinforces the idea that displacement responds to shocks unfolding across connected districts.

**Finding 4: These results should still be read cautiously.** The largest raw coefficients come from environmental variables on different scales, and some signs vary across periods and exposure types, so they are better treated as clues for refinement than as settled causal effects. The updated results also do not support the earlier draft's stronger claims about a clean post-2018 North climate transition or fuel price as the dominant economic channel.

---

## 10. Discussion (Placeholder)


---

## 11. Limitations

- No direct origin-pulling factor modeling.
- policy Impact?

---

## 12. Conclusion

---

## Appendix A. Distributional Figures

**Figure A1a: Month Coverage Diagnostic**
![Month Coverage Diagnostic](../results/figures/diagnostic_month_coverage.png)
*Coverage diagnostic for the district-month panel from April 2014 to August 2024. The top panel shows whether usable data are present in each month, while the bottom panel shows the number of reporting districts by month. This figure documents the months excluded from the estimation sample because no usable data are available across districts.*

**Figure A1: Population Displacements — Linear vs. Logarithmic Scale**
![Population Displacements](../results/figures/dist_population_linear_vs_log.png)
*Boxplots of IDP and returnee counts by North/South on linear (top) and symlog (bottom) scales.*

**Figure A2: Environmental and Economic Shock Distributions by Region**
![Environmental Distributions](../results/figures/dist_environmental_economic.png)
*Regional boxplots for SPI-6, temperature, NDVI, soil moisture, food inflation, fuel price.*

**Figure A3: IDP Monthly Change — North vs South**
![IDP Monthly Change](../results/figures/fig1b_idp_change.png)
*Mean Δln(IDP+1) with ±1 SD band. Volatile outflows 2014–2016 in North; more symmetric fluctuation in South.*

**Figure A4: Lag Window Selection — Bivariate |t-statistic| Heatmap**
![Bivariate t-stat Heatmap](../results/figures/fig2_bivariate_heatmap.png)
*Maximum |t-statistic| from bivariate Stage A regressions for each variable × lag window (pooled, own lags only).*

**Figure A5: Climate Thematic Heatmaps — North vs South**
![Climate Heatmaps](../results/figures/climate_north_south_heatmaps.png)
*SPI-6, temperature anomaly, NDVI anomaly by district and month.*

**Figure A6: Price Thematic Heatmaps — North vs South**
![Price Heatmaps](../results/figures/prices_north_south_heatmaps.png)
*Wage, fuel price, food inflation by district and month.*

**Figure A7: Forest Plots — North Iraq, IDP Monthly Change (dlog_idp)**
![Forest Plot North dlog_idp](../results/figures/fig5_forest_north_dlog_idp.png)

**Figure A8: Forest Plots — South Iraq, IDP Monthly Change (dlog_idp)**
![Forest Plot South dlog_idp](../results/figures/fig5_forest_south_dlog_idp.png)

**Figure A9: R² Progression — South Iraq**
![R² South](../results/figures/fig4_r2_progression_south.png)

**Figure A10: District Fixed Effects Map**
![Spatial FE Map](../results/figures/fig7_spatial_fe_map.png)
*Demeaned entity FEs from B3 model (RdBu_r). Positive (red) = systematic IDP over-retention; negative (blue) = under-retention relative to model.*

---

## Appendix B. Robustness Figures

**Figure B1: Spatial K Robustness — North Iraq** *(K = 30/50/100)*
![K Robustness North](../results/figures/fig8_robustness_k_north.png)

**Figure B2: Spatial K Robustness — South Iraq**
![K Robustness South](../results/figures/fig8_robustness_k_south.png)

**Figure B3: Own Lag Window Stability — North Iraq**
![Lag Stability North](../results/figures/fig9_robustness_lag_north.png)

**Figure B4: Own Lag Window Stability — South Iraq**
![Lag Stability South](../results/figures/fig9_robustness_lag_south.png)

---

## Appendix C. Spatial Connectivity

**Figure C1–C3: Travel-Time Spatial Connectivity from Key Districts**
![Spillover Al-Mosul](../results/figures/spillover_al_mosul_k_comparison.png)
*Al-Mosul: connectivity at K=10, 30, 50, All. Arrow width and color = normalized inverse travel-time weight.*

![Spillover Al-Rutba](../results/figures/spillover_al_rutba_k_comparison.png)
*Al-Rutba: remote western district; sparse connectivity.*

![Spillover Al-Basrah](../results/figures/spillover_al_basrah_k_comparison.png)
*Al-Basrah: southern hub; dense connectivity across the South.*

---

## Appendix D. Full Statistical Tables

**Table A1.** Full descriptive statistics — `summary_stats_north_south_2014_present.csv`

**Table A2.** Full standardized coefficient table, ln_idp — `model_results_b3_ln_idp.csv`

**Table A3.** Full standardized coefficient table, dlog_idp — `model_results_b3_dlog_idp.csv`

**Table A4.** Significance summary across all cells — `model_results_b3_significance.csv`

---
