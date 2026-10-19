# GeoEvidence — visual release checklist

## Editorial direction

Use the GitHub portfolio's established **actual visual on the left, short interpretation on the right** layout. Do not use stock maps, invented spatial patterns, or simulated model scores.

## Assets to review

These files were previously exported from the local v3 QGIS project, but are **not included in this repository**:

| Expected filename | Source/meaning | Safe caption |
| --- | --- | --- |
| `terrain_layers.png` | Slope from saved 10 m terrain layer | “Terrain characterization from the research GIS workflow. The grid resolution does not establish the native resolution of every input.” |
| `environmental_predictors.png` | Canopy, soil, hydrology, and climate factor scores (0–1) | “Environmental screening factors standardized for comparison and review.” |
| `model_suitability.png` | Experimental screened relative index (0–100) | “Relative ecological survey-priority index. Not a calibrated probability or field-validated prediction.” |

## Mandatory review before publishing

- [ ] Remove the sensitive target-species name and its synonyms from map labels, legends, filenames, metadata, and captions.
- [ ] Ensure coordinates, detailed geographic labels, identifiable landmarks, and fine-scale extents cannot reveal survey targets.
- [ ] If the priority surface remains spatially actionable, publish a generalized, blurred, cropped, or non-geolocated version instead of the original.
- [ ] Review EXIF and embedded metadata, not just visible text.
- [ ] Confirm the terrain, predictor, and screening maps are correctly attributed to the separate **v3 QGIS workflow**, not the **60 m county-holdout random-forest study**.
- [ ] Keep scores described as relative rankings; do not claim calibrated occupancy probabilities, field validation, or exact plant locations.
- [ ] Review copyright and dataset-attribution requirements.
- [ ] Have the project owner approve each export for public release.

## Proposed placement

1. **Research pipeline:** current `assets/workflow.svg` beside the study design.
2. **Out-of-sample evidence:** current `assets/transfer-effects.svg` beside the holdout findings.
3. **GIS workflow:** three reviewed images in a compact gallery with the captions above, followed by the methodological separation note.

## How to supply images

Upload the three PNGs to the conversation. If any includes precise spatial clues, also supply generalized or cropped alternatives. They will not be committed until disclosure review is complete.

## Methodological boundary

The frozen regional validation uses 60 m analysis cells, county-level holdouts, and independently observed future records. The v3 QGIS screening workflow uses a saved 10 m terrain grid and a separate experimental 0–100 relative index. They are complementary examples of research engineering, **not the same trained or validated model**.
