# Výsledky po druhém raw-data auditu a minor revision

## Hlavní závěr

> Within the declared Monte Carlo calibrated scenario envelope, the present observational/reanalysis assembly does not distinguish the sign or magnitude of a trend in known-storage-corrected required poleward transport across the principal Arctic boundaries. This non-detection is not evidence of zero trend.

A long-memory ARFIMA sensitivity broadens the envelope further but does not change the qualitative conclusion.

`H_corr` je **known-storage-corrected required transport**, nikoli nezávisle pozorovaný actual total transport. Bodové klimatické výsledky se v Etapě 11 nezměnily.

## Hlavní trendové výsledky

Monte Carlo kalibrovaná scénářová obálka používá pro hlavní derivátor zaokrouhlený critical 4,57. Je kalibrována na cílové empirical coverage 95 % v deklarované DGP matici; není univerzálním 95% confidence intervalem.

| hranice | H_corr best | scenario envelope | půlšířka | ERA5 AHT best | AHT scenario envelope | unresolved remainder best | rozhodnutí |
|---:|---:|---:|---:|---:|---:|---:|---|
| 50°N | +16,62 | [−139,00; +172,25] | 155,63 | +56,84 | [−45,53; +159,22] | −40,22 | NOT DETECTED |
| 60°N | +0,77 | [−98,08; +99,62] | 98,85 | +12,26 | [−61,36; +85,88] | −11,49 | NOT DETECTED |
| 65°N | −0,11 | [−80,23; +80,02] | 80,12 | +2,66 | [−58,79; +64,12] | −2,77 | NOT DETECTED |
| 70°N | +2,75 | [−70,08; +75,59] | 72,84 | −2,18 | [−47,47; +43,12] | +4,93 | NOT DETECTED |
| 75°N | +5,13 | [−53,01; +63,28] | 58,15 | +1,43 | [−22,28; +25,14] | +3,71 | NOT DETECTED |
| 80°N | +5,03 | [−34,79; +44,85] | 39,82 | +1,94 | [−5,23; +9,11] | +3,09 | NOT DETECTED |

Trendy jsou TW/dekádu. Strukturální chyba ERA5 ani další níže uvedené nevyčíslené strukturální chyby nejsou v obálkách zahrnuty.

## Current declared versus long-memory stress

- současná deklarovaná DGP obálka: critical **4,57**;
- ARFIMA `d=0,45` stress: critical **5,94**, coverage současné obálky 0,894;
- stress obálka je asi 1,30× širší;
- obě varianty zahrnují nulu na hlavních hranicích, takže hlavní závěr se nemění;
- obálky se neslučují a strukturální nejistoty se k nim nepřičítají ad-hoc součtem.

## Raw CERES versus regionální storage correction

Na 60/65/70°N jsou raw CERES apparent trendy +22,07 / +18,12 / +14,94 TW/dekádu. Po korekci na známý regionální storage včetně sea ice jsou H_corr trendy +0,77 / −0,11 / +2,75 TW/dekádu. Odpovídající storage alias je +21,30 / +18,23 / +12,18 TW/dekádu.

To je významný bilanční výsledek, ale nikoli dvě nezávislá pozorování. Platí konstrukcí:

`H_raw = <N>global A_cap − N_cap`

`H_alias = <N>global A_cap − dE_known/dt`

`H_corr = H_raw − H_alias = dE_known/dt − N_cap`.

Storage alias ukazuje rozdíl mezi uniformním global-storage proxy a známým regionálním storage. Raw implied transport se neinterpretuje jako actual transport.

## Absolutní budget

Klimatologické `H_required / ERA5 AHT / unresolved remainder` na 60/65/70°N jsou:

- 60°N: 3,345 / 2,788 / 0,557 PW;
- 65°N: 2,551 / 2,151 / 0,401 PW;
- 70°N: 1,767 / 1,461 / 0,305 PW.

Na 70°N dává pouze orientační OHT sanity range 0,15–0,25 PW rozdíl 0,105 PW k midpointu. Absolutní rozpočet je zde fakticky uzavřen jen na řád 0,1 PW. Remainder není OHT; podrobnosti jsou v `ABSOLUTE_CLOSURE_ASSESSMENT.md`.

## Zrušené numerické structural bounds

Původní `missing_storage_structural_bounds.csv` a combined safe threshold se nepoužívají. Originál je pouze ve zmrazeném snapshotu; aktivní auditní zástupce `RETIRED_missing_storage_structural_bounds.csv` obsahuje `status=RETIRED` a `DO NOT USE FOR INFERENCE`. Žádný aktivní downstream skript z něj nečte.

Jako **UNQUANTIFIED** zůstávají:

- CERES regional systematic uncertainty;
- cap-resolved NCEI OHC mapping/sampling error;
- ERA5 structural trend uncertainty;
- deep-ocean storage;
- land heat;
- glacier/ice-sheet enthalpy;
- full PIOMAS structural uncertainty.

Nevyčísleno neznamená nula a nevytváří se nový combined threshold.

## Reprodukovatelnost inference

Přesné historické 4,569448 vyžaduje jeden sdílený PCG64 stream, přesné pořadí DGP/trend/derivátor a spotřebu nepoužitých bootstrap draws. Bez této spotřeby je DGP-pooled maximum 4,371443; per-cell maximum 4,746200. Proto text používá robustní zaokrouhlení 4,57 a úplný algoritmus je v `MC_CALIBRATION_REPRODUCIBILITY.md`.

## Auditní stopa

- baseline: `STAGE11_BASELINE.md`, `stage11_pre_minor_revision_snapshot/`, `stage11_baseline_checksums.sha256`;
- výsledky: `POST_AUDIT_KEY_RESULTS.csv`, `POST_AUDIT_UNCERTAINTY.csv`, `STORAGE_ALIAS_SCENARIO_ENVELOPE.csv`;
- MC: `monte_carlo_calibration_metadata.json`, `mc_critical_value_reproducibility.csv`, `long_memory_sensitivity.csv`;
- closure: `absolute_closure_assessment.csv`;
- druhý audit: `ROUND2_AUDIT_RESPONSE.md`;
- grafická data: `climatology_vs_trend_transport_envelope_data.csv`.

Žádný závěr zde neattribuuje změnu ASR, transport nebo Arctic amplification na CO₂, clouds, aerosols ani forcing.
