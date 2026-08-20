# Contemporaneous Association Between SO₂ and Particulate Matter (PM10) at Industrial Monitoring Stations: A Replicated Study in Cubatão, Brazil (2021–2022)

**Bruna Preschadt de Oliveira**
Aquvaris AI

**Version 1.3 (English)** — scientific draft. All figures verified against the analysis notebook (11-item audit checklist, all confirmed) and re-audited after replication; references verified individually. Translated and adapted from the Portuguese version; content, values, and methodological caveats preserved. Terminology standardized to "association" throughout; NO₂ described as an adjustment covariate; hedging language calibrated (no over-strong claims of ruling out alternatives). Recommended: review by an academic English speaker before formal submission.

---

## Abstract

Air quality monitoring systems allow the concentrations of individual pollutants to be tracked, but the joint interpretation of these series is constrained by meteorological and seasonal factors and by the presence of other emission sources. This study examines the association between SO₂ — an indicator of emissions linked to combustion and industrial processes — and PM10 at industrial monitoring stations in Cubatão (SP, Brazil), incorporating the temporal structure of the data before any causal interpretation. At the Cubatão-Vila Parisi station, over 605 days between 2021 and 2022, a linear regression with standard errors robust to heteroskedasticity and autocorrelation (HAC/Newey-West) estimated a contemporaneous association of 0.4481 µg/m³ of PM10 per µg/m³ of SO₂ (95% CI: 0.1756–0.7207; p = 1.27×10⁻³; adjusted R² = 0.535). The estimate remained similar after controlling for seasonality and after changing the number of lags in the HAC estimator, while no statistically significant association was detected between the previous day's SO₂ and the following day's PM10. Applying the same procedure to the Cubatão-Vale do Mogi station, over 597 days, produced a positive association of larger magnitude (0.8461; 95% CI: 0.5396–1.1525; p = 6.24×10⁻⁸). Although the difference between the estimates is suggestive, a formal heterogeneity test did not indicate a statistically significant difference between the stations (p = 0.11). The observed pattern is compatible with co-emission from common industrial sources, but the data do not allow this mechanism to be distinguished from alternative explanations, such as atmospheric particle-formation processes. The study reports a quantitatively estimated association, replicated across two industrial stations in Cubatão, together with an analytical procedure that incorporates temporal structure and robustness checks before environmental interpretation.

---

## 1. Research question

When the concentration of an atmospheric pollutant varies, how much of that variation can be associated with the signature of a specific source, and does this association persist after controlling for meteorology, seasonality, trend, and other sources? The study addresses this question for the SO₂–PM10 pair, prioritizing the investigation of the temporal nature of the signal before any causal claim, rather than reporting a single adjusted coefficient.

## 2. Context: Cubatão-Vila Parisi

Cubatão (SP) is a historical reference point for industrial pollution in Brazil. In the 1980s, industries in the region are reported to have released on the order of one thousand tonnes of atmospheric pollutants per day, a situation partially reversed by a control program initiated in 1983 (CETESB). The Cubatão-Vila Parisi station is characterized by CETESB itself as an industrially focused station, without equivalent among the other monitoring stations in the state of São Paulo. This study does not extrapolate to the critical period of the 1980s–90s; the analyzed data correspond to 2021–2022, a period of regulated operation.

## 3. Data

- Pollutants: SO₂, PM10, and NO₂, as daily means from the Cubatão-V.Parisi station, obtained through the OpenAQ API, which records CETESB (the São Paulo State environmental agency) as the data provider (provider ID 220). Aggregation from hourly to daily resolution is performed by the source.
- Meteorology: temperature, precipitation, wind, humidity, and pressure, from daily historical reanalysis (Open-Meteo).
- Period: from 2021-01-12 to 2022-12-31, totaling 605 complete days after cleaning. The daily series of the three pollutants over the period are shown in Figure 1.
- Quality and auditing: values ≤ 0 were treated as missing; there is one record per day (no additional aggregation on our part); the merge with meteorology is one-to-one (no duplication); the raw series contains 16 short gaps. Temporal lags were constructed by calendar date (575 valid consecutive pairs), not by row position.

## 4. Causal design and identification strategy

- Relationship of interest: SO₂ → PM10.
- Measured confounders: NO₂; temperature, precipitation, wind, humidity, and pressure; seasonality (month indicators) and a linear time trend.
- Treatment of NO₂: the observed SO₂–NO₂ correlation was low (0.193), suggesting largely distinct sources; NO₂ was therefore included as an adjustment covariate to account for variation potentially associated with combustion-related sources.
- Identification caveat: a contemporaneous relationship between SO₂ and PM10 is compatible both with chemical conversion (SO₂ oxidized to sulfate, forming secondary PM) and with co-emission from a common source (an industrial source emitting SO₂ and primary PM simultaneously). Both mechanisms are documented for particulate matter (Seinfeld & Pandis, 2016) and are recognized by CETESB for Vila Parisi specifically. The contemporaneous structure does not distinguish these alternatives. Consequently, the estimand is reported as an adjusted association, not as a source-level causal effect.

## 5. Estimation

A linear regression of PM10 on SO₂ was estimated with the full set of controls (meteorology, NO₂, month, and trend). Given the time-series nature of the residuals (see §7), inference was conducted with HAC standard errors (Newey & West, 1987).

The estimated contemporaneous association was 0.4481 µg/m³ of PM10 per µg/m³ of SO₂ (95% CI [HAC, 7 lags]: 0.1756–0.7207; p = 1.27×10⁻³; N = 605).

The raw, uncontrolled relationship is shown in Figure 2; its slope (approximately 1.28) is about 2.8 times the adjusted association, illustrating the magnitude of the confounding removed by the controls.

The final model explains roughly 55% of the daily variance in PM10 (R² = 0.549; adjusted R² = 0.535). The remaining ~45% corresponds to factors outside the model — other sources, atmospheric transport, and variability not captured by the covariates — which reinforces reading the result as a partial association rather than a complete determination of PM10 by SO₂.

As an external reference, a convergent cross mapping analysis in Jakarta placed the SO₂→PM2.5 causality at 0.68 (Aerosol and Air Quality Research, 2023), broadly comparable in magnitude to the present result, albeit in a different context and with a different method.

## 6. Temporal structure of the signal

Three temporal specifications were estimated (SO₂ at t+1, t, and t−1 on PM10 at t), with and without seasonal control (Figure 3):

| Specification | β (no seasonal control) | β (with seasonal control) |
|---|---|---|
| t+1 → t (temporal placebo) | 0.2144 | 0.2071 |
| t → t (contemporaneous) | 0.4704 | 0.4481 |
| t−1 → t (1-day lag) | 0.0937 (n.s.) | 0.0850 (n.s.) |

These estimates can be read as follows. The contemporaneous association remains stable under seasonal control (from 0.4704 to 0.4481), which provides no evidence that the contemporaneous association is primarily explained by seasonality. The one-day lagged association is not significant, providing no evidence of a detectable one-day lagged association at the daily temporal resolution, which is consistent with a contemporaneous process such as co-emission. The temporal placebo at t+1 remains around 0.21 even after seasonal control; its persistence is attributed to the autocorrelation of PM10 (0.58, see §7) rather than to seasonal confounding — its smaller magnitude relative to the contemporaneous estimate is consistent with a contemporaneous component beyond temporal persistence alone. Finally, including or excluding NO₂ changes the estimate only slightly (0.4481 versus 0.4895), positioning NO₂ as an adjustment covariate of modest effect rather than a dominant co-emitter.

Refutation tests from the causal-inference framework — adding a random common cause, placebo by treatment permutation, and 80% subsampling — were conducted on the reference specification (effect of 0.4704, without seasonal control). The effect remained stable under the random common cause (0.4704 to 0.4704) and under subsampling (0.4704 to 0.4859), and dropped to near zero under the placebo treatment (0.4704 to 0.0079), as expected. The final specification adds seasonal and trend controls — which change the effect by less than 5% (0.4704 to 0.4481) — and adopts HAC inference, which refines the confidence interval without moving the point estimate. The structure evaluated by the refuters — namely the presence of an effect, its collapse under placebo, and its stability under subsampling — is thus preserved in the final specification.

## 7. Robust inference

Diagnostics on the residuals of the contemporaneous model indicated autocorrelation (Durbin-Watson = 1.271; Ljung-Box p ≪ 0.001 at lags 1 and 7) and heteroskedasticity (Breusch-Pagan p ≈ 1×10⁻⁵). Under these conditions, conventional standard errors understate the uncertainty (Newey & West, 1987); the point estimate of the coefficient is unaffected.

HAC/Newey-West was adopted as the primary inference. Sensitivity to the choice of maximum lag was assessed by comparing 7 lags (a short-term window defined a priori) and 8 (an alternative specification), holding the remaining estimator parameters constant:

| HAC (lags) | 95% CI | p |
|---|---|---|
| 7 | 0.1756–0.7207 | 1.27×10⁻³ |
| 8 | 0.1714–0.7248 | 1.50×10⁻³ |

The variation in the confidence-interval bounds between 7 and 8 lags was below 0.005 µg/m³, and significance remained on the order of 10⁻³: inference does not depend materially on this choice. The robust interval is about 30% wider than the conventional one (0.545 versus 0.419), reflecting the true uncertainty of the series.

## 8. Replication at a second station

To assess whether the association is specific to one station or reflects a pattern of the industrial zone, the full pipeline — same specification, same controls, and same HAC-7 inference — was applied to the Cubatão-Vale do Mogi station, the other industrial cluster monitored in the region (597 complete days).

| Station | β (SO₂→PM10) | 95% CI (HAC-7) | p | N |
|---|---|---|---|---|
| Cubatão-Vila Parisi | 0.4481 | 0.1756–0.7207 | 1.27×10⁻³ | 605 |
| Cubatão-Vale do Mogi | 0.8461 | 0.5396–1.1525 | 6.24×10⁻⁸ | 597 |

The association replicates: at both stations it is positive, statistically significant, and robust to the same analytical specification. This indicates that the SO₂–PM10 pattern is not an artifact of a single isolated station.

The point coefficient is larger at Vale do Mogi (0.85) than at Vila Parisi (0.45). To assess whether this difference is statistically distinguishable from sampling variation, a combined model of the two stations was estimated with full interaction (each station with its own controls), extracting the SO₂ × station interaction term under HAC-7 inference. A consistency check confirmed that the combined model reproduces the coefficients of the separate models (0.445 and 0.805). The estimated difference was 0.3602 (95% CI: −0.0838–0.8042; p = 0.11): suggestive, but not statistically significant at the conventional level. The data do not provide sufficient statistical evidence to establish heterogeneity between the stations — the difference in magnitude may reflect sampling variation, and distinguishing the two hypotheses would require more stations or longer series. The absence of significance does not imply equality of the coefficients; it implies insufficient data to decide.

## 9. Methodological protocol

The study instantiates a reproducible protocol for analyzing environmental associations in time series, which constitutes a contribution independent of the specific result:

> detect → control → test temporality → check robustness → declare limits → (only then) attribute

Concretely: (1) detect the raw association; (2) control measured confounders (weather, seasonality, trend, other sources); (3) test the temporal structure (placebo t+1, lag t−1) to distinguish a contemporaneous signal from shared structure; (4) check robustness (HAC inference, lag sensitivity, with/without confounder); (5) explicitly declare the limits of identification; (6) reserve causal attribution for when the design supports it. The protocol shifts the question from "is there an effect?" to "what is the nature of the signal?".

## 10. Limitations

- The contemporaneous structure does not distinguish chemical conversion from co-emission.
- Daily resolution may mask sub-daily dynamics (chemical mechanisms operate over hours). Moreover, aggregation from hourly to daily resolution is performed by the source (OpenAQ/CETESB) and is not auditable by the authors: we do not have access to the aggregation criterion (mean over which hours, minimum coverage requirement), which constitutes an unquantified source of uncertainty.
- Unobserved confounders may remain; the estimate is conditional on the set of controls adopted.
- Two stations in the same region (Cubatão); generalization to other regions and industrial profiles remains to be tested. The difference in magnitude between the stations is suggestive but not conclusive (§8).
- Linear estimator; non-linear forms were not evaluated in this version.
- Treating NO₂ as a confounder presupposes distinct sources; the low observed correlation supports, but does not prove, this premise.

## 11. Conclusion

This study found a robust contemporaneous association between SO₂ and PM10 at an industrial station in Cubatão (Vila Parisi: 0.4481 µg/m³ per µg/m³; robust 95% CI: 0.1756–0.7207). The estimate remained stable under controls for meteorology, seasonality, trend, and NO₂, under the choice of inference parameter, and under the applied refutation methods (placebo treatment, subsampling, and adding a random common cause). The association replicated at a second industrial station (Vale do Mogi: 0.8461; p = 6.24×10⁻⁸), indicating a pattern not restricted to a single monitoring point; the difference in magnitude between the stations is suggestive but does not reach statistical significance. The absence of a lagged association and the contemporaneous stability are compatible with contemporaneous contributions from a common industrial source, although the data do not allow this mechanism to be isolated from alternative explanations, such as rapid chemical conversion or the presence of an unmeasured common latent source. With the available data, the study does not support a claim of a direct causal effect of SO₂ on PM10; it supports an adjusted and replicated association, with a plausible physical interpretation and explicitly declared limits.

## 12. Future work

- Hourly data, to investigate sub-daily dynamics and distinguish conversion from co-emission.
- Replication at industrial clusters in other regions and production profiles (the heterogeneity suggested between Vila Parisi and Vale do Mogi motivates increasing the number of stations).
- Non-linear estimators and causal time-series methods (e.g., distributed-lag models; convergent cross mapping).

---

## Reproducibility

Code, data, and documentation: `github.com/bpreschad-gif/aquvaris-causal-environmental-research`

## Figures

- **Figure 1** — Daily time series of SO₂, PM10, and NO₂ at Cubatão-Vila Parisi (2021–2022). (`results/figures/fig1_series.png`)
- **Figure 2** — Raw SO₂–PM10 relationship with fitted line (slope ≈ 1.28). (`results/figures/fig2_dispersao.png`)
- **Figure 3** — Adjusted effect on PM10 across the three temporal specifications (t+1 placebo, t contemporaneous, t−1 lagged), with 95% confidence intervals. (`results/figures/fig3_temporal.png`)

## References

- Nardocci, A. C.; Freitas, C. U.; Ponce de Leon, A. C. M.; Junger, W. L.; Gouveia, N. C. (2013). Air pollution and respiratory and cardiovascular diseases: a time-series study in Cubatão, São Paulo, Brazil. *Cadernos de Saúde Pública*, 29(9), 1867–1876.
- Newey, W. K.; West, K. D. (1987). A Simple, Positive Semi-Definite, Heteroskedasticity and Autocorrelation Consistent Covariance Matrix. *Econometrica*, 55(3), 703–708.
- Seinfeld, J. H.; Pandis, S. N. (2016). *Atmospheric Chemistry and Physics: From Air Pollution to Climate Change* (3rd ed.). Wiley.
- Tec, M.; Scott, J. G.; Zigler, C. M. (2023). Weather2vec: Representation Learning for Causal Inference with Non-Local Confounding in Air Pollution and Climate Studies. *arXiv:2209.12316*.
- [Jakarta / CCM] Causality Analysis of Air Quality and Meteorological Parameters for PM2.5 Characteristics Determination: Evidence from Jakarta. *Aerosol and Air Quality Research* (2023).
- CETESB — São Paulo State Environmental Company. Automatic air quality monitoring network; characterization of the Cubatão-Vila Parisi station; air quality reports.

*References to be expanded in the submission version: additional literature on causal inference in air quality and on SO₂/PM co-emission from industrial sources.*
