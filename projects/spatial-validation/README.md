# GeoEvidence — Spatial Prediction & Geographic Transfer Validation

**Research case study | Western North Carolina | GIS, spatial machine learning, and frozen external validation**

> **Revision in progress (October 2026).** An audit of the modeling pipeline found that the original background sampler accepted candidate locations in sorted grid order, which distorted the background sample. The random-forest results on this page come from the original v1.0 analysis and are being revised. Preliminary corrected reruns change some conclusions, including whether effort-aware background improves on uniform background. The corrected manuscript is in preparation; this page will be updated when it is final.

<table>
<tr>
<td width="53%" valign="top"><img src="assets/workflow.svg" alt="Actual geospatial research workflow: environmental data, occurrence audit, model comparison, and geographic holdout validation" width="100%"></td>
<td valign="top"><strong>Research question</strong><br><br>Can a model trained on historical observations outside a county identify later observations in that withheld county, beyond what proximity to known observations can explain?<br><br><strong>Methods</strong><br>23-county analysis · temporal separation · whole-county holdouts · observer-effort adjustment · distance-only null<br><br><strong>Interpretation</strong><br>Regional ranking evidence, not calibrated occupancy probabilities or a field-validated locator.</td>
</tr>
</table>

## 01 · The problem: ecological signal or observer geography?

Citizen-science plant observations are not random samples of the landscape. Records cluster where people can travel and where botanists choose to look. A habitat model can therefore seem accurate simply by remembering the geography of previous observations. This project asked a more demanding question:

**Can an environmental model trained on historical observations outside a county rank later, geographically separated observations within that withheld county better than a model based only on distance to known records?**

The case study summarizes completed research analyses, not a hosted prediction product or a validated field-survey locator.


## 02 · The method: correct observation bias without inventing negatives

The principal modeling innovation is to change **which available locations enter the background sample**, not to manually weight predictor importance. Historical observer visits provide a proxy for where plants were more likely to be looked for. The method contrasts uniform forest background with effort-aware background under otherwise frozen model settings.

### Observer-effort-aware background sampling

<table><tr><td width="52%" valign="top"><img src="assets/effort-background.svg" alt="Diagram comparing uniform and observer-effort background sampling, with identical random forest settings" width="100%"></td><td valign="top"><strong>What changes?</strong><br><br>Positive observations and model settings stay fixed. The comparison varies how negative/background locations are sampled: uniformly from eligible forest or near recorded spring botanist visits, with 1 km jitter and a 5% uniform component.<br><br><strong>Why?</strong><br><br>Presence-only data can reflect observer accessibility and search behavior as much as ecology. This is background-sampling correction, <em>not</em> manually assigning weights to environmental features.</td></tr></table>

## Models and validation

Three prespecified approaches were compared:

1. **Uniform-background random forest:** background sampled uniformly from eligible training-county forest, excluding a 200 m zone around training presences.
2. **Effort-aware random forest:** same forest parameters and target presences, with background shaped by historical spring botanist-observer visits, one visit per observer/day/250 m cell; visits jittered at sigma 1 km, with 5% uniform background to maintain support.
3. **Distance-only null:** ranking determined solely by distance to the nearest training occurrence, a direct test of geographic memorization.

Each random forest used 500 trees, minimum leaf size 5, square-root feature selection, balanced class weights, random seed 42, and background at five times the training-presence count. No outcome-driven hyperparameter optimization was performed.

**Primary estimand:** the *county-balanced mean of county-median future-observation landscape percentiles*. Each held-out county contributes equally. Uncertainty for multi-county comparisons comes from 20,000 county-level bootstrap resamples, not bootstrap resampling of individual records.


## 03 · The challenge: beat a geographic-memory null

A model can look predictive by learning proximity to prior records. Here, the deliberately simple distance-only baseline makes that alternative explanation testable, while whole-county withholding and later observations raise the bar for genuine geographic transfer.

### Distance-only baseline and external holdout

<table><tr><td width="52%" valign="top"><img src="assets/distance-null.svg" alt="Four-step diagram of frozen training, independent future observations, distance-only baseline, and county-level comparison" width="100%"></td><td valign="top"><strong>The challenge</strong><br><br>A baseline ranks the landscape solely by proximity to historical occurrences. It has no environmental predictors. Environmental models must improve on this benchmark for later observations in completely withheld counties.<br><br><strong>Why it matters</strong><br><br>Random train/test splits can reward spatial autocorrelation. The combination of whole-county holdouts, later observations, and a 1 km historical-occurrence exclusion makes geographic memorization less persuasive.</td></tr></table>


## 04 · Measured results: transferable signal, with uncertainty

<table>
<tr>
<td width="53%" valign="top"><img src="assets/transfer-effects.svg" alt="Observed county-balanced transfer effects for three forest-herb models, including uncertainty and a contrary single-county result" width="100%"></td>
<td valign="top"><strong>Measured results</strong><br><br>Effort-aware environmental models outperformed the geographic-memory baseline in two multi-county tests. A third, single-county case favored the distance-only model.<br><br><strong>Why it matters</strong><br>Spatial autocorrelation can make models appear effective when they are simply learning where observers have already looked. A frozen external validation design tests that shortcut.</td>
</tr>
</table>

| Species | Qualifying counties | Future observations | Effort RF | Uniform RF | Distance null | Effort minus distance (95% county-bootstrap interval) |
| --- | ---: | ---: | ---: | ---: | ---: | --- |
| Bloodroot | 11 | 288 | 0.684 | 0.653 | 0.526 | **+0.158** (0.030 to 0.280) |
| Mayapple | 10 | 246 | 0.666 | 0.596 | 0.509 | **+0.157** (0.068 to 0.241) |
| Black cohosh | 1 | 17 | 0.378 | 0.317 | 0.720 | **−0.342**; single-county descriptive result |

**Two multi-county tests succeeded against geographic memory.** Bloodroot and mayapple both showed positive effort-aware environmental-model advantages over the distance null, with the lower bounds of county-bootstrap 95% intervals above zero.

**Observer-effort correction was not universally better.** For mayapple, effort-aware versus uniform RF was +0.069 (95% CI +0.030 to +0.108). For bloodroot it was +0.031 (−0.055 to +0.121), an inconclusive comparison.

**The contrary result matters.** Only one county qualified for black cohosh; in that county the distance null exceeded both random forests. This cannot support a species-wide estimate. Adding regional SSURGO pH and water capacity did not consistently improve transfer for the two multi-county species.

For bloodroot, the effort-aware model captured 32.6% of future observations in the highest-ranking 10% of eligible reference landscape; mayapple captured 15.0%. Generalized ranking skill and top-decile concentration are different claims.


## 05 · Replication failure and what it teaches

The same frozen protocol was carried forward to additional species rather than redesigned around their observed outcomes. Mayapple replicated the primary geographic-transfer advantage; black cohosh did not in its only qualifying county. This contrast is a substantive research finding, not a defect to remove from the portfolio.

### Prespecified replication protocol

<table><tr><td width="52%" valign="top"><img src="assets/frozen-replication.svg" alt="Diagram of frozen predictors and hyperparameters, replication threshold, and both successful and failed outcomes" width="100%"></td><td valign="top"><strong>Prespecified success criterion</strong><br><br>The effort-aware RF must exceed the distance-only null on the county-balanced primary endpoint, with the lower bound of the 95% county-bootstrap interval above zero.<br><br><strong>Observed outcomes</strong><br><br>Mayapple replicated the bloodroot transfer advantage. Black cohosh did not replicate in its sole qualifying county, which is a descriptive counterexample rather than a generalizable species-wide estimate.</td></tr></table>


## 06 · Limitations, evidence boundaries, and GIS exhibits

### Scope, materials, and limitations

This folder is a **public aggregate research write-up with editable SVG methods diagrams and four original QGIS map PNGs**. It is **not a reproduction package**. It does not include scripts, source rasters, raster predictions, precise occurrence coordinates, or unreviewed derived location layers. A separate, auditable code-and-data release would require reviewing licensing, source snapshots, provenance hashes, spatial-data sensitivity, and reproducibility. The figures are visual presentations of previously calculated summaries; no models were rerun to produce them.

Additional limitations include opportunistic observation bias, incomplete measurement of failed searches and observer-hours, species-by-geography variation, and a single-county black-cohosh contrast. Future evaluations should compare the original expert-weighted GIS model on these same frozen test sets and assess transfer into additional regions.

### Why the validation design matters

- A random train/test split can reward spatial autocorrelation.
- Holding out later observations alone can reward proximity to historical sites.
- Entire-county withholding plus time separation plus 1 km exclusion reduces those shortcuts.
- A distance-only null makes the shortcut measurable.
- County-level bootstrap avoids treating correlated records within one county as independent replications.
- Frozen settings and published negative results resist selective reporting.

### GIS supporting exhibits: terrain, predictors, and held-out model validation

The companion cartographic exports come from the **Western North Carolina environmental stack and geographic holdout analysis**, using a reproducible **QGIS 4.2** layout/export workflow. They distinguish the covariates used in model development from the **county-level evaluation results**. The four original map exhibits appear below, alongside the workflow and transfer-effect diagrams.

| Map exhibit | What it shows | Reading the evidence |
| --- | --- | --- |
| **Terrain layers** | Shared Western North Carolina elevation and slope layers. | Environmental context and topographic structure, not a species occurrence map. |
| **Environmental predictors** | Canopy, topographic wetness, July maximum temperature, and growing-season precipitation. | Predictor surfaces on their respective measurement scales, not field-observed species presence. |
| **Bloodroot held-out model output** | County-level median future-record landscape percentiles across **11 held-out counties**, with **288 qualifying future observations** in the combined confirmatory analysis. | Evidence of geographic transfer from future observations excluded by county and time; not a pixel-level occupancy probability. |
| **Black cohosh held-out model output** | **Buncombe County only**, the sole qualifying county, with **17 qualifying future test records**. | The **frozen replication criterion was not met**. The one-county finding is descriptive, not a species-wide transfer estimate. |

#### Regional predictor inputs: how the model sees the landscape

<table><tr><td width="54%" valign="top"><img src="assets/terrain_layers.png" alt="Original QGIS maps of elevation and slope across the 23-county Western North Carolina study region" width="100%"></td><td valign="top"><strong>Terrain: elevation and slope</strong><br><br>Two inputs from the shared 60 m regional analysis grid. Terrain structure supports the environmental feature engineering, but by itself does not demonstrate predictive skill.<br><br><strong>Role:</strong> Explanatory variables in the spatial random forest, not species locations or a prediction map.</td></tr></table>

<table><tr><td width="54%" valign="top"><img src="assets/environmental_predictors.png" alt="Original QGIS panels for canopy cover, topographic wetness index, July maximum temperature, and growing-season precipitation" width="100%"></td><td valign="top"><strong>Environmental covariates</strong><br><br>Canopy, wetness, summer temperature, and growing-season precipitation provide complementary ecological signals. The model learns from these surfaces and the other prespecified predictors.<br><br><strong>Role:</strong> Measured or derived predictors, not field-confirmed occurrences. Native source resolution varies despite the common 60 m grid.</td></tr></table>

#### Held-out counties: what future observations actually tested

<table><tr><td width="54%" valign="top"><img src="assets/bloodroot_model_output.png" alt="Original bloodroot county choropleth showing median future-observation landscape percentiles in 11 qualifying withheld counties" width="100%"></td><td valign="top"><strong>Bloodroot: heterogeneous but positive aggregate transfer</strong><br><br>Eleven qualifying held-out counties. The map displays the median rank of future observations within each county, with substantial between-county variation.<br><br>The county-balanced primary comparison favored the effort-aware random forest over the distance-only null by <strong>+0.158</strong> (95% county-bootstrap interval <strong>+0.030 to +0.280</strong>).<br><br><strong>Interpretation:</strong> Ranking evidence across withheld counties, not a plant-location map or calibrated probability.</td></tr></table>

<table><tr><td width="54%" valign="top"><img src="assets/black_cohosh_model_output.png" alt="Original black cohosh county map showing only Buncombe County qualified, with median future-observation landscape percentile approximately 0.38" width="100%"></td><td valign="top"><strong>Black cohosh: a valuable failed replication</strong><br><br>Only Buncombe County met the independent-test threshold (17 records). Its effort-aware model median was approximately <strong>0.38</strong>, while the distance-only null scored <strong>0.72</strong>.<br><br><strong>Interpretation:</strong> The frozen replication criterion was not met. With only one qualifying county, this is a descriptive negative result, not a species-wide conclusion.</td></tr></table>

### How to interpret these maps

**Map scores represent the median landscape percentile assigned to future observation records within a held-out county**, calculated against the eligible reference landscape. They are **not calibrated occupancy probabilities**, ground-truth presence/absence maps, predicted plant counts, or field-validated occurrence locations. The maps are intended to show county-level summary statistics only, **without plant occurrence coordinates**. The images show regional geographic context and county boundaries, but no individual plant occurrence coordinates.

The terrain and environmental layers are shared analytical inputs. The county-level output maps summarize out-of-sample evaluation rather than fine-resolution survey priorities. They must not be confused with an independently calibrated habitat probability surface.

### Detailed study design and data provenance

- **Study area:** 23 Western North Carolina counties on an EPSG:5070, 60 m analysis grid.
- **Target species:** bloodroot (*Sanguinaria canadensis*), mayapple (*Podophyllum peltatum*), and black cohosh (*Actaea racemosa*).
- **Occurrence audit:** research-grade iNaturalist observations, wild/noncaptive, publicly georeferenced, stated positional accuracy above zero and no more than 100 m, de-duplicated and thinned to one record per 100 m cell.
- **Temporal split:** observations through December 31, 2021 for training; January 1, 2022 through September 15, 2026 for future testing.
- **Independent future test:** observations at least 1 km from every historical focal-species occurrence.
- **Geographic holdouts:** remove every historical target occurrence from the test county and train only on other counties; background also excludes the withheld county.
- **Primary scope:** counties meeting the prespecified threshold of at least 15 eligible future observations.

### GIS and predictor pipeline

| Input | Derived information |
| --- | --- |
| USGS 3DEP elevation | Elevation, slope, directional aspect, TPI, wetness, drainage distance, and heat load |
| NLCD 2021 | Forest analysis mask and tree-canopy percentage |
| PRISM 1991–2020 normals | July maximum temperature and growing-season precipitation |
| USDA NRCS SSURGO | Soil pH and available-water capacity, prespecified secondary sensitivity extension |
| iNaturalist plant observations | Target-species presences and spring botanist-observation-effort proxy |

The frozen **Core-12** predictor set was elevation, slope, northness, eastness, approximately 300 m and 900 m TPI, TWI, distance to drainage, canopy cover, July maximum temperature, April–October precipitation, and McCune–Keon heat load.

The 60 m grid supports **regional ranking**, not fine-scale habitat suitability or exact plant location guidance. Underlying PRISM and soil datasets have coarser measurement support. The habitat scores are **presence/background discrimination scores, not calibrated occupancy probabilities**.

## Selected public data sources

- [USGS 3DEP](https://www.usgs.gov/3d-elevation-program)
- [Multi-Resolution Land Characteristics (NLCD)](https://www.mrlc.gov/)
- [PRISM Climate Group](https://prism.oregonstate.edu/)
- [USDA NRCS SSURGO](https://www.nrcs.usda.gov/resources/data-and-reports/soil-survey-geographic-database-ssurgo)
- [iNaturalist](https://www.inaturalist.org/)

**Project status:** Independent research, not yet peer reviewed. Values above are from the v1.0 frozen confirmatory summaries; a corrected manuscript is in preparation (co-authored).

[Back to portfolio](../../README.md)
