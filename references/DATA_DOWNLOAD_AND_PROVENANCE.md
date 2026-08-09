# Official data download and provenance

The historical input volume is **1,843,950,436 bytes (1.717 GiB)**.  Allow at
least another GiB for temporary archives, decoded arrays and generated files.
Exact machine-readable requests are in `download_specs/`; the human-readable
full specification is `download_specs/DATA_DOWNLOAD_SPEC.md`.

## CERES EBAF Edition4.2.1

- Institution: NASA Langley Research Center.
- Official OPeNDAP: `https://opendap.larc.nasa.gov/opendap/CERES/EBAF/Edition4.2.1/CERES_EBAF_Edition4.2.1_200003-202603.nc`.
- Requested native data: 2000-03–2026-03; 180 zonal latitude rows plus global
  monthly scalars; variables listed in
  `download_specs/ceres_ebaf_ed4.2.1.json`.
- Historical local subset: 1,654,948 bytes, SHA-256
  `7739eb63b1440dcd2f13a2c1c12c0b1dbb91a45e091e4178ba6c013f9742f2b5`.
- The download script builds the zonal/global NetCDF directly from the official
  OPeNDAP response; it does not use an author-reduced time series.

## ERA5 mass-consistent energy/moisture budget v1.0

- Institution: ECMWF/Copernicus Climate Change Service.
- Dataset: `derived-reanalysis-energy-moisture-budget`.
- API endpoint: `https://cds.climate.copernicus.eu/api`; credentials are
  required in the reviewer's normal CDS configuration.
- Variables: `vertical_integral_of_northward_total_energy_flux` and
  `tendency_of_vertical_integral_of_total_energy`.
- Period: AHT 2000-01–2022-12; SH atmospheric storage 2005-01–2022-12.
- Fifteen exact requests, areas, years, months, original filenames, sizes and
  SHA-256 values are in `download_specs/era5_requests.json`; immutable original
  request copies are in `code/era5/original_requests/`.
- Historical total: 1,757,939,898 bytes.

## NCEI OHC 0–2000 m monthly

- Institution: NOAA NCEI/NODC Ocean Climate Laboratory.
- Official file: `https://www.ncei.noaa.gov/data/oceans/woa/DATA_ANALYSIS/3M_HEAT_CONTENT/NETCDF/heat_content/heat_content_anomaly_0-2000_monthly.nc`.
- Full global 1° file; use `h18_hc` in `10^18_joules`; analysis window
  2005-01–2022-12.
- Historical retrieval: 66,430,205 bytes, SHA-256
  `c9bfadc494dccf3f1cfeb9f1ffa4d6cebb6d79bbf0bdadd3aa64ef639524a05d`.
- The live rolling file may later be extended.  Record decoded coverage and
  subset the declared historical window.

## PIOMAS v2.1

- Institution: University of Washington APL Polar Science Center.
- Data page: `https://psc.apl.uw.edu/research/projects/arctic-sea-ice-volume-anomaly/data/`.
- Official aggregate CSV:
  `https://psc.apl.uw.edu/wordpress/wp-content/uploads/schweiger/ice_volume/PIOMAS.monthly.Current.v2.1.csv`.
- Annual `heff` base:
  `https://pscfiles.apl.uw.edu/zhang/PIOMAS/data/v2.1/heff/`.
- Files: `heff.H2005.nc.gz` through `heff.H2022.nc.gz` plus the aggregate CSV;
  17,925,385 historical bytes total.  Per-file names, sizes and SHA-256 are in
  `download_specs/piomas_original_files.json`.

## Checksum policy

Historical SHA-256 values identify the original run.  Fresh services may
repackage NetCDF/ZIP files or extend rolling products.  A byte mismatch is
reported but does not automatically fail the science.  Product/version,
variables, dimensions, coordinates, units, time coverage and decoded numerical
fields are mandatory checks and can fail the audit.

## Reproducible commands

Dry-run the request inventory without downloading:

```bash
./download_all_original_data.sh --mode dry-run
```

Full blind chain:

```bash
./run_v4_blind_reproduction.sh
```

The master downloader records actual size/SHA in
`provenance/download_report.csv`; metadata validation records its results in
`provenance/metadata_validation.csv`.  If a source fails, report
`DATASET_DOWNLOAD_FAILED`; do not insert bundled reference tables into the
calculation.

CERES EBAF and NCEI OHC are not fully statistically independent because EBAF
uses a global energy-balance constraint informed by OHC.  Regional NCEI OHC
adds spatial information not fixed by that global constraint, but shared
information and covariance must be acknowledged.
