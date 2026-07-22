A multi-sensor satellite-derived bathymetry (SDB) framework for shallow, optically complex tidal deltas, applied to the Eastern Banks in Moreton Bay, Queensland. The pipeline harmonises WorldView-2 (2011–2015) and PlanetScope SuperDove 8 (2022–2025) imagery, retrieves depth with an XGBoost regressor, and analyses the resulting time-series for morphodynamic change at 3 m resolution. Produced as a master's thesis at the University of Queensland (ENVM7133).

# Key results
- Mean MAE 0.18 m, RMSE 0.28 m, R² 0.87 (five-fold spatial block cross-validation)
- The Eastern Banks act as a **sediment trap** and **sedimentary palimpsest**
    - Net elevation increase across 99.2% of significant pixels, median +0.77 m over 14 years
    - Morphodynamic envelope and elevation change are systematically structured by bank, following a proximal–distal gradient from the South Passage
    - Median deposit age of one year, indicating annual surface reworking

# Workflow
1. Preprocessing
    1. [AOI](01_aoi.ipynb)
    2. [Grid alignment](02_grid-align.ipynb)
    3. [Clipping](03_clip.ipynb), etc.
2. Quality assurance including [saturation correction](04_saturation-corr.ipynb) via minimum mean square error (MMSE) estimator ([Zhang & Brainard, 2004](https://doi.org/10.1364/JOSAA.21.002301))
3. [Relative radiometric normalisation](05_PIF-normalisation.ipynb)
    1. Multi-dimensional pseudo-invariant-feature selection (MDPS) ([Paolini et al., 2006](https://doi.org/10.1080/01431160500183057))
    2. Harmonisation to reference image via RANSAC ([Xu et al., 2021](https://doi.org/10.1080/01431161.2021.1934912))
4. [Feature engineering and multicollinearity pruning (VIF, condition number, variance decomposition proportion)](06_feature-stacking.ipynb)
5. Spatial k-fold cross-validation (i.e BlockCV) ([Valavi et al., 2019](https://doi.org/10.1111/2041-210X.13107))
6. [XGBoost regression including prediction interval width](08_time-series.ipynb) ([Chen & Guestrin, 2016](https://doi.org/10.1145/2939672.2939785))
7. [Non-parametric change analysis](09_analysis.ipynb)
    1. DEM of difference
    2. Mann-Kendall / Theil-Sen slope
    3. Stratigraphic volume analysis ([Pearson et al., 2022](https://doi.org/10.1016/j.geomorph.2022.108185))

# Data note

Imagery (WorldView-2, PlanetScope) and reference bathymetry ([Roelfsema et al. 2014](https://doi.org/10.1016/j.rse.2014.05.001); EOMAP 2024) are third-party datasets and are not redistributed here. Sources and access details are documented in /docs.

# Licence

Code released under the MIT Licence. Thesis text and figures under CC BY 4.0. Third-party data remain subject to their original terms.

# Citation

Lamey, S. (2026). Mapping the shifting sands: Over a decade of bathymetric evolution at the Eastern Banks, Moreton Bay, Queensland [Master's thesis, The University of Queensland].

# Acknowledgements

I offer my sincere thanks to our supervisors, Doctor Dylan Cowley, Associate Professor Chris Roelfsema, and Mister David Enrique Carrasco Rivera at the University of Queensland. These pioneers have paved the way for the next generation of coastal researchers at the Eastern Banks. Without their unyielding guidance and support, this thesis would not have come to fruition. I hold in the highest regard their profound contributions to the frontier (and, oftentimes, conundrum) that is remote sensing of coastal ecosystems.

I also acknowledge the Quandamooka peoples, Traditional Owners of Minjerribah, Mulgumpin and the Sea Country in which the Eastern Banks are situated. I acknowledge their ongoing connections to Country and community. I pay my respects to ancestors who stewarded this land for millennia, which has enabled this very research to manifest. It is my hope that this research may be of use in the ongoing management and protection of this vital Sea Country.
