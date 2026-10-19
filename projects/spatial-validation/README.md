# GeoEvidence — Spatial Prediction & Geographic Transfer Validation

**Research case study | Western North Carolina | GIS, spatial machine learning, and frozen external validation**

<table>
<tr>
<td width="53%" valign="top"><img src="assets/workflow.svg" alt="Actual geospatial research workflow: environmental data, occurrence audit, model comparison, and geographic holdout validation" width="100%"></td>
<td valign="top"><strong>Research question</strong><br><br>Can a model trained on historical observations outside a county identify later observations in that withheld county, beyond what proximity to known observations can explain?<br><br><strong>Methods</strong><br>23-county analysis · temporal separation · whole-county holdouts · observer-effort adjustment · distance-only null<br><br><strong>Interpretation</strong><br>Regional ranking evidence, not calibrated occupancy probabilities or a field-validated locator.</td>
</tr>
</table>

## The decision problem

Citizen-science plant observations are not random samples of the landscape. Records cluster where people can travel and where botanists choose to look. A habitat model can therefore seem accurate simply by remembering the geography of previous observations. This project asked a more demanding question:

**Can an environmental model trained on historical observations outside a county rank later, geographically separated observations within that withheld county better than a model based only on distance to known records?**

The case study summarizes completed research analyses, not a hosted prediction product or a validated field-survey locator.

## Study design

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

## Models and validation

Three prespecified approaches were compared:

1. **Uniform-background random forest:** background sampled uniformly from eligible training-county forest, excluding a 200 m zone around training presences.
2. **Effort-aware random forest:** same forest parameters and target presences, with background shaped by historical spring botanist-observer visits, one visit per observer/day/250 m cell; visits jittered at sigma 1 km, with 5% uniform background to maintain support.
3. **Distance-only null:** ranking determined solely by distance to the nearest training occurrence, a direct test of geographic memorization.

Each random forest used 500 trees, minimum leaf size 5, square-root feature selection, balanced class weights, random seed 42, and background at five times the training-presence count. No outcome-driven hyperparameter optimization was performed.

**Primary estimand:** the *county-balanced mean of county-median future-observation landscape percentiles*. Each held-out county contributes equally. Uncertainty for multi-county comparisons comes from 20,000 county-level bootstrap resamples, not bootstrap resampling of individual records.

## Results

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

## Why the validation design matters

- A random train/test split can reward spatial autocorrelation.
- Holding out later observations alone can reward proximity to historical sites.
- Entire-county withholding plus time separation plus 1 km exclusion reduces those shortcuts.
- A distance-only null makes the shortcut measurable.
- County-level bootstrap avoids treating correlated records within one county as independent replications.
- Frozen settings and published negative results resist selective reporting.

## Companion QGIS workflow: experimental landscape screening

**Visual asset status:** Three map exports have been generated locally from the v3 QGIS project, but are not yet available as reviewed, public-safe image files in this repository. They will be added only after geographic extents, map labels, coordinates, legends, and metadata have been screened for sensitive-site disclosure. No map is being recreated from invented data.

| Visual | What it demonstrates | Release requirement |
| --- | --- | --- |
| Terrain layers | Slope and landform characterization from the saved 10 m terrain layer | Generalized or non-identifying extent |
| Environmental predictors | Canopy, soils, hydrology, and climate factor scores on a 0–1 scale | No sensitive target-species references or coordinates |
| Model survey-priority index | Experimental relative 0–100 screening score | Avoid precise locations and any probability or field-validation claim |



A separate, locally developed **v3 QGIS workflow** illustrates how terrain, environmental covariates, and screening rules can be assembled into a transparent ecological decision-support process. It is distinct from the frozen **60 m regional random-forest validation** above.

The workflow has three stages:

1. **Terrain characterization:** a slope surface derived from a saved **10 m** terrain grid reveals local landform structure.
2. **Environmental inputs:** canopy, soils, moisture/hydrology, and climate are represented as **0–1 factor scores** for comparison and review.
3. **Survey prioritization:** screened factors are combined into an experimental **0–100 relative site-priority index**.

**Interpretation and sharing limits:** This is an **experimental ecological screening index**, not a calibrated probability, a field-validated prediction, or an output of the independent bloodroot/mayapple county-holdout tests. Fine-scale mapped priorities and identifying study-area details are intentionally not published, because they could guide searches for a sensitive resource. The 10 m analysis grid also does not imply 10 m source resolution for every environmental factor.

## Scope, materials, and limitations

This folder is a **public-safe, aggregate research write-up with editable SVG diagrams**. It is **not a reproduction package**. It does not include scripts, source rasters, raster predictions, precise occurrence coordinates, or unreviewed derived location layers. A separate, auditable code-and-data release would require reviewing licensing, source snapshots, provenance hashes, spatial-data sensitivity, and reproducibility. The figures are visual presentations of previously calculated summaries; no models were rerun to produce them.

Additional limitations include opportunistic observation bias, incomplete measurement of failed searches and observer-hours, species-by-geography variation, and a single-county black-cohosh contrast. Future evaluations should compare the original expert-weighted GIS model on these same frozen test sets and assess transfer into additional regions.

## Selected public data sources

- [USGS 3DEP](https://www.usgs.gov/3d-elevation-program)
- [Multi-Resolution Land Characteristics (NLCD)](https://www.mrlc.gov/)
- [PRISM Climate Group](https://prism.oregonstate.edu/)
- [USDA NRCS SSURGO](https://www.nrcs.usda.gov/resources/data-and-reports/soil-survey-geographic-database-ssurgo)
- [iNaturalist](https://www.inaturalist.org/)

**Status:** Independent, unpublished research case study. All descriptive values above come from the completed project’s frozen confirmatory result summaries and research manuscript. No peer-review or production-deployment claim is made.

[Back to portfolio](../../README.md)
