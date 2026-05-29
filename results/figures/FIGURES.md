# Figure Gallery — Iraq Displacement Modelling

All PNGs live in `results/figures/`. Open this file in VS Code and use **Ctrl+Shift+V** (or click the preview icon) to browse images inline.
Early figures: 150 dpi. Nature-style figures: 300 dpi. Entries marked **(pending)** are not yet on disk.

---

## Basemaps & Administrative Boundaries

### `iraq_adm2_district_names.png`
![iraq_adm2_district_names](iraq_adm2_district_names.png)
*ADM2 district names overlaid on ADM1 governorate boundaries. ADM1 as background watermarks; ADM2 as foreground labels.*

---

## Spatial & Political Classification Maps

### `iraq_classification_geo.png`
![iraq_classification_geo](iraq_classification_geo.png)
*Geographic zone classification: North / Central / South (3-way).*

### `iraq_classification_north.png`
![iraq_classification_north](iraq_classification_north.png)
*Broad binary North / South regional divide.*

### `iraq_classification_pol.png`
![iraq_classification_pol](iraq_classification_pol.png)
*Political jurisdiction: KRI / Disputed / Federal Iraq.*

### `iraq_classification_conf.png`
![iraq_classification_conf](iraq_classification_conf.png)
*Conflict exposure during ISIS campaign (2014–2017): Heavy / Moderate / Low.*

### `iraq_classification_cap.png`
![iraq_classification_cap](iraq_classification_cap.png)
*Governorate capital districts highlighted in red against grey non-capitals.*

### `iraq_classifications_panel.png`
![iraq_classifications_panel](iraq_classifications_panel.png)
*Combined 2×3 panel of all five classification maps above.*

---

## Thematic ADM2 × Month Heatmaps (North vs South)

One figure per theme. Each figure: rows = ADM2 districts (grouped by ADM1, dashed separators); columns = months. ADM1 labels on right axis. Colormap: RdBu_r for anomaly/index variables, YlOrRd for level variables. Colour range capped at 95th percentile. 300 dpi. Generated from `panel_clean` in `01_data_harmonization0526.ipynb`.

### `conflict_north_south_heatmaps.png`
![conflict_north_south_heatmaps](conflict_north_south_heatmaps.png)
*Conflict indicators (3 rows × 2 cols): conflict events 3-month mean, conflict deaths 3-month mean, conflict incidence — North (left) and South (right). Gray = no data (NaN).*

### `climate_north_south_heatmaps.png`
![climate_north_south_heatmaps](climate_north_south_heatmaps.png)
*Climate indicators (3 rows × 2 cols): SPI-6, temperature anomaly (1m), NDVI anomaly (1m) — North (left) and South (right). Gray = no data (NaN).*

### `prices_north_south_heatmaps.png`
![prices_north_south_heatmaps](prices_north_south_heatmaps.png)
*Price indicators (3 rows × 2 cols): wage non-qualified labour, fuel gas price, food price inflation index — North (left) and South (right). Gray = no data (NaN).*

---

## Data Quality & Imputation Diagnostics

### `diagnostic_month_coverage.png`
![diagnostic_month_coverage](diagnostic_month_coverage.png)
*Two-panel month coverage diagnostic (2014-04 to 2024-08). Top: binary present/absent per month. Bottom: districts reporting per month.*

### `imputation_diagnostics_idp.png`
![imputation_diagnostics_idp](imputation_diagnostics_idp.png)
*Per-district before/after time series for `final_idp_count` gaps filled via ffill/bfill. Dashed red = imputed, solid blue = original.*

### `dist_population_linear_vs_log.png`
![dist_population_linear_vs_log](dist_population_linear_vs_log.png)
*Boxplots of `final_idp_count` and `final_returnee_count` by North/South on linear and symlog scales (2×2 grid).*

### `dist_environmental_economic.png`
![dist_environmental_economic](dist_environmental_economic.png)
*Boxplots of 10 environmental & economic indicators by North/South region (5×2 grid).*

---

## Lag Window Distribution Plots

### `dist_lag_total_best_deaths.png`
![dist_lag_total_best_deaths](dist_lag_total_best_deaths.png)
*North/South boxplots for `total_best_deaths` across lag windows L1–3, L4–6, L7–9, L10–12.*

### `dist_lag_total_events.png`
![dist_lag_total_events](dist_lag_total_events.png)
*Same for `total_events`.*

### `dist_lag_spi6.png`
![dist_lag_spi6](dist_lag_spi6.png)
*Same for `spi6`.*

### `dist_lag_spi6_flood_severity.png`
![dist_lag_spi6_flood_severity](dist_lag_spi6_flood_severity.png)
*Same for `spi6_flood_severity`.*

### `dist_lag_spi6_drought_severity.png`
![dist_lag_spi6_drought_severity](dist_lag_spi6_drought_severity.png)
*Same for `spi6_drought_severity`.*

### `dist_lag_t2m_max_anom_1m.png`
![dist_lag_t2m_max_anom_1m](dist_lag_t2m_max_anom_1m.png)
*Same for `t2m_max_anom_1m`.*

### `dist_lag_ndvi_anom_1m.png`
![dist_lag_ndvi_anom_1m](dist_lag_ndvi_anom_1m.png)
*Same for `ndvi_anom_1m`.*

### `dist_lag_sm1_anom_1m.png`
![dist_lag_sm1_anom_1m](dist_lag_sm1_anom_1m.png)
*Same for `sm1_anom_1m`.*

### `dist_lag_inflation_food_price_index.png`
![dist_lag_inflation_food_price_index](dist_lag_inflation_food_price_index.png)
*Same for `inflation_food_price_index`.*

### `dist_lag_c_fuel_gas.png`
![dist_lag_c_fuel_gas](dist_lag_c_fuel_gas.png)
*Same for `c_fuel_gas`.*

---

## Lag Window Trend Plots

### `trend_lag_total_best_deaths.png`
![trend_lag_total_best_deaths](trend_lag_total_best_deaths.png)
*Time trends of all lag windows for `total_best_deaths`, North vs South. 2018 break marked.*

### `trend_lag_total_events.png`
![trend_lag_total_events](trend_lag_total_events.png)
*Same for `total_events`.*

### `trend_lag_spi6.png`
![trend_lag_spi6](trend_lag_spi6.png)
*Same for `spi6`.*

### `trend_lag_spi6_flood_severity.png`
![trend_lag_spi6_flood_severity](trend_lag_spi6_flood_severity.png)
*Same for `spi6_flood_severity`.*

### `trend_lag_spi6_drought_severity.png`
![trend_lag_spi6_drought_severity](trend_lag_spi6_drought_severity.png)
*Same for `spi6_drought_severity`.*

### `trend_lag_t2m_max_anom_1m.png`
![trend_lag_t2m_max_anom_1m](trend_lag_t2m_max_anom_1m.png)
*Same for `t2m_max_anom_1m`.*

### `trend_lag_ndvi_anom_1m.png`
![trend_lag_ndvi_anom_1m](trend_lag_ndvi_anom_1m.png)
*Same for `ndvi_anom_1m`.*

### `trend_lag_sm1_anom_1m.png`
![trend_lag_sm1_anom_1m](trend_lag_sm1_anom_1m.png)
*Same for `sm1_anom_1m`.*

### `trend_lag_inflation_food_price_index.png`
![trend_lag_inflation_food_price_index](trend_lag_inflation_food_price_index.png)
*Same for `inflation_food_price_index`.*

### `trend_lag_c_fuel_gas.png`
![trend_lag_c_fuel_gas](trend_lag_c_fuel_gas.png)
*Same for `c_fuel_gas`.*

---

## Displacement Heatmaps (District × Time)

### `heatmap_idp_absolute_north_south.png`
![heatmap_idp_absolute_north_south](heatmap_idp_absolute_north_south.png)
*IDP stock heatmap (YlOrRd). North (top) / South (bottom). Colour capped at 98th percentile; black = missing or zero-throughout. 2014-04 to 2024-08.*

### `heatmap_returnee_absolute_north_south.png`
![heatmap_returnee_absolute_north_south](heatmap_returnee_absolute_north_south.png)
*Returnee count heatmap (YlGnBu). Same layout as IDP figure above.*

### `heatmap_idp_flow_north_south.png` **(pending)**
*Month-to-month first difference in IDP stock (RdBu_r). North / South stacked vertically.*

### `heatmap_returnee_flow_north_south.png` **(pending)**
*Same for returnee counts.*

---

## Road Network & Travel Time Matrix

### `open_street_map_drive.png`
![open_street_map_drive](open_street_map_drive.png)
*Figure X. Drivable road network of Iraq derived from OpenStreetMap via OSMnx (`network_type="drive"`, `simplify=True`). Edges represent drivable road segments; nodes (intersections) are suppressed for visual clarity. Edge density reflects the concentration of road infrastructure along the Tigris–Euphrates corridor and major urban centers (Baghdad, Mosul, Kirkuk, Erbil, Basra), with sparse coverage across the western Al Anbar desert and northern mountain corridors.*

### `travel_time_matrix_heatmap.png`
![travel_time_matrix_heatmap](travel_time_matrix_heatmap.png)
*Full ADM2 × ADM2 travel time matrix (rocket_r, shorter = darker). District names on both axes. Values in hours.*

### `travel_time_distribution.png`
![travel_time_distribution](travel_time_distribution.png)
*Histogram + KDE of all pairwise ADM2-to-ADM2 travel times. Median marked with dashed red line.*

---

## Spatial Connectivity (Travel-Time Lag)

### `spillover_al_mosul_k_comparison.png`
![spillover_al_mosul_k_comparison](spillover_al_mosul_k_comparison.png)
*2×2 panel: connectivity from Al-Mosul at K = 10, 30, 50, All. Arrow colour and width encode normalised weight; top-5 neighbours labelled.*

### `spillover_al_rutba_k_comparison.png`
![spillover_al_rutba_k_comparison](spillover_al_rutba_k_comparison.png)
*Same layout for Al-Rutba (Al-Anbar — large remote western district).*

### `spillover_al_basrah_k_comparison.png`
![spillover_al_basrah_k_comparison](spillover_al_basrah_k_comparison.png)
*Same layout for Al-Basrah (southern hub).*

---

## Modelling Results — Descriptive

### `fig1_idp_trend.png`
![fig1_idp_trend](fig1_idp_trend.png)
*Mean ± 1 SD of ln(IDP+1) by month, North and South, with district spaghetti lines and 2018 break.*

### `fig1b_idp_change.png`
![fig1b_idp_change](fig1b_idp_change.png)
*Mean ± 1 SD of monthly Δln(IDP+1) by region. Zero baseline and 2018 break marked.*

---

## Modelling Results — Stage A (Lag Selection)

### `fig2_bivariate_heatmap.png`
![fig2_bivariate_heatmap](fig2_bivariate_heatmap.png)
*1×2 heatmap of max |t-stat| per variable × lag window, pooled `ln_idp`. Blue □ = short-term winner; green ◇ = long-term.*

### `fig3_own_vs_spatial.png`
![fig3_own_vs_spatial](fig3_own_vs_spatial.png)
*Grouped bar: max |t-stat| own-district vs. spatial-neighbour (K=30) per variable, pooled `ln_idp`.*

---

## Modelling Results — Stage B (Model Fit)

### `fig4_r2_progression_north.png`
![fig4_r2_progression_north](fig4_r2_progression_north.png)
*Within R² as blocks added (B1→B2→B3) across 3 samples × 2 outcomes. North Iraq.*

### `fig4_r2_progression_south.png`
![fig4_r2_progression_south](fig4_r2_progression_south.png)
*Same for South Iraq.*

### `fig5_forest_north_ln_idp.png`
![fig5_forest_north_ln_idp](fig5_forest_north_ln_idp.png)
*Forest plot (B3, standardised β, 90% CI), pooled/pre/post. North Iraq, `ln_idp`.*

### `fig5_forest_north_dlog_idp.png`
![fig5_forest_north_dlog_idp](fig5_forest_north_dlog_idp.png)
*Same for `dlog_idp`. North Iraq.*

### `fig5_forest_south_ln_idp.png`
![fig5_forest_south_ln_idp](fig5_forest_south_ln_idp.png)
*Same for `ln_idp`. South Iraq.*

### `fig5_forest_south_dlog_idp.png`
![fig5_forest_south_dlog_idp](fig5_forest_south_dlog_idp.png)
*Same for `dlog_idp`. South Iraq.*

---

## Modelling Results — Diagnostics

### `fig6_time_dependence_north.png`
![fig6_time_dependence_north](fig6_time_dependence_north.png)
*2×6 grid: ACF (top) and time-FE approx (bottom) for B3 residuals, 3 samples × 2 outcomes. North Iraq.*

### `fig6_time_dependence_south.png`
![fig6_time_dependence_south](fig6_time_dependence_south.png)
*Same for South Iraq.*

### `fig7_spatial_fe_map.png`
![fig7_spatial_fe_map](fig7_spatial_fe_map.png)
*2×6 choropleth of demeaned district entity FEs (RdBu_r) from B3; rows = region, cols = sample × outcome.*

---

## Modelling Results — Robustness

### `fig8_robustness_k_north.png`
![fig8_robustness_k_north](fig8_robustness_k_north.png)
*Spatial lag β ± 90% CI for `ln_total_best_deaths` and `spi6` across K = 30/50/100. North Iraq.*

### `fig8_robustness_k_south.png`
![fig8_robustness_k_south](fig8_robustness_k_south.png)
*Same for South Iraq.*

### `fig9_robustness_lag_north.png`
![fig9_robustness_lag_north](fig9_robustness_lag_north.png)
*Own-lag β ± 90% CI across L1–3, L4–6, L7–9, L10–12. North Iraq.*

### `fig9_robustness_lag_south.png`
![fig9_robustness_lag_south](fig9_robustness_lag_south.png)
*Same for South Iraq.*

---

<!-- ADD NEW FIGURES BELOW THIS LINE -->
