# GeoEvidence | County-holdout GIS map release checklist

## Visual direction

Use the portfolio's existing **visual on the left, short interpretation on the right** layout. Do not fabricate maps, interpolate pixels, or treat model evaluation percentiles as occupancy probabilities. The source files were created locally through a reproducible **QGIS 4.2** export workflow: `scripts/export_bloodroot_cohosh_maps.py`.

The intended image files are currently **not present in the public repository**. Add the images and replace the status below only after inspecting the actual exported pixels.

## Four expected exports

| Filename | Map content | Concise public caption | Suggested alt text |
| --- | --- | --- | --- |
| `terrain_layers.png` | Shared WNC elevation and slope layers | **Terrain context.** Elevation and slope surfaces used to characterize Western North Carolina's landforms. | "Maps showing Western North Carolina elevation and slope layers used in the spatial modeling workflow." |
| `environmental_predictors.png` | Canopy, topographic wetness, July maximum temperature, and growing-season precipitation | **Environmental predictors.** Selected canopy, terrain moisture, and climate covariates in the regional modeling stack. | "Maps of Western North Carolina canopy, topographic wetness, July maximum temperature, and growing-season precipitation predictors." |
| `bloodroot_model_output.png` | County-level held-out bloodroot model summary for 11 qualifying counties | **Bloodroot geographic transfer.** Median future-observation landscape percentiles across 11 county holdouts; scores are rankings, not occupancy probabilities. | "County-level held-out evaluation map for bloodroot across 11 Western North Carolina counties, summarizing future-record landscape percentiles without individual occurrence locations." |
| `black_cohosh_model_output.png` | Buncombe-only black cohosh holdout with 17 future test records | **Black cohosh limitation.** Buncombe was the only qualifying holdout (17 future observations); the frozen replication criterion was not met. | "Buncombe County-only held-out black cohosh evaluation map with 17 qualifying future observations; the prespecified replication criterion was not met." |

These descriptions reflect the requested exports, **not verified visual inspection of files that are not yet accessible in the repository**. Confirm labels, panel order, ranges, and contents against the PNGs before publication.

## Validation boundary

- County-level map values are the **median future-record percentiles from held-out tests** compared with the eligible reference landscape. They are **not occupancy probabilities**.
- Bloodroot: **11 county holdouts**, **288 qualifying future observations** in the documented confirmatory analysis; the effort-aware random forest exceeded the distance-only null in the county-balanced primary metric (**+0.158**, 95% county-bootstrap interval **+0.030 to +0.280**).
- Black cohosh: **Buncombe only**, **17 qualifying future observations**. Distance-only outperformed the environmental models there, and the frozen replication criterion was not met. Do not present this as successful multi-county replication or a meaningful one-county bootstrap interval.
- Never overlay raw plant occurrence coordinates or imply that a map pixel marks a confirmed plant location.
- Terrain and environmental predictors are **input maps**; county-level percentile summaries are **holdout evaluation maps**. Distinguish these clearly.
- The related regional analysis used a **60 m** harmonized model grid and predictors with different source resolutions. Do not claim uniform measurement support or field-scale resolution for all inputs.

## Before committing files

- [ ] Review all four PNGs visually for correct extent, clipping, readable text, legends, accurate labels, and scientific meaning.
- [ ] Confirm the maps show **no individual plant observation coordinates**, markers, identifying records, or other sensitive location information.
- [ ] Review PNG metadata and ancillary text, including authoring/export paths.
- [ ] Ensure no legacy sensitive-target maps or labels are accidentally included.
- [ ] Check that bloodroot has 11 qualifying counties, while the black-cohosh exhibit shows Buncombe only and clearly describes the failed criterion.
- [ ] Ensure that county-level percentile color scales and legends do **not** imply occurrence probability.
- [ ] Check source attributions and project ownership for public distribution.
- [ ] Verify the export README and QGIS 4.2 script are consistent with the captions.
- [ ] Commit the four PNGs under `projects/spatial-validation/assets/`, embed each with descriptive alt text, and confirm the GitHub README renders without broken images.
- [ ] Refresh the profile teaser to show one of the actual verified map assets once committed.

## Source and publication status

The local working export folder is `reports/portfolio_maps/`. Neither that Windows folder nor its four map files can be inferred from the current GitHub repository's contents. The map gallery should stay unlinked until all four actual binary assets are accessible and verified.
