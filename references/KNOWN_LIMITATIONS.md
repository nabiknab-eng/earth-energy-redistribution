# Known limitations after Stage 11

## Unquantified structural uncertainty

The following terms remain explicitly **UNQUANTIFIED**. Unquantified does not mean zero, and no new combined threshold is constructed:

1. CERES regional systematic uncertainty;
2. cap-resolved NCEI OHC mapping/sampling error and its spatial covariance;
3. ERA5 atmospheric-transport structural trend uncertainty, including observing-system changes;
4. storage below 2000 m;
5. land heat storage;
6. glacier and ice-sheet enthalpy;
7. full PIOMAS structural uncertainty and omitted sensible/other ice enthalpy terms.

## Estimand limitations

- `H_raw` is CERES-implied transport under a uniform global-storage proxy; it is not actual transport.
- `H_corr = dE_known/dt − N_cap` is known-storage-corrected required transport; it is not independently observed actual total transport.
- `H_corr − ERA5 AHT` is an unresolved/non-atmospheric remainder; it is not automatically OHT.
- NCEI OHC covers only 0–2000 m and does not resolve every cap cell with equal observational support.
- SH sea-ice storage is not symmetrically included in the NH-focused corrected branch.
- CERES EBAF and OHC are partly statistically dependent through the EBAF global energy-balance constraint; regional OHC adds spatial information but is not wholly independent.

## Statistical limitations

- The common trend record is short (about 2006–2022 after derivative alignment) and strongly serially dependent.
- The current scenario envelope is calibrated only on the declared white/AR(1)/persistent-AR(2) matrix.
- Its exact historical critical 4.569 depends on shared RNG consumption; 4.57 is therefore reported as a rounded scenario multiplier.
- ARFIMA `d=0.45` reduces coverage of the current envelope to 0.894 and requires q95 about 5.94 in the reproduced stress test.
- ARFIMA is a sensitivity, not a proven model for the observed residual process.
- One multiplier need not transfer equally to CERES raw, H_corr, storage alias, ERA5 AHT, and the unresolved remainder.
- Neither current nor long-memory envelope includes the unquantified structural terms above.
- Non-detection is not evidence of a zero trend or absence of physical change.

## Absolute closure limitation

The climatological unresolved remainder is 0.557/0.401/0.305 PW at 60/65/70°N. Near 70°N, comparison with the second auditor's literature sanity range for OHT leaves roughly 0.1 PW to the range midpoint. The absolute budget is therefore not independently physically closed below order 0.1 PW at that boundary.

## Scope

No result attributes ASR, meridional transport, or Arctic amplification to CO₂, clouds, aerosols, forcing, or any other cause.
