# Response to the second independent raw-data audit

Každá připomínka byla nejprve reprodukována z existujícího kódu a reduced outputs. Auditní tvrzení nebyla přijata pouze autoritou auditora.

| Reviewer finding | Our reproduction | Status | Change made | Numerical effect | Effect on scientific conclusion |
|---|---|---|---|---|---|
| Původní DGP set neobsahuje true long memory; ARFIMA d=0.45 má coverage ~0.88 a critical ~6.03 | ARFIMA(0,0.45,0), 4500 pooled realizací: coverage 0.894, minimum cell 0.889, q95 5.935 | **CONFIRMED** | Přidány d=0.20/0.35/0.45 jako oddělený stress test | d=0.45 envelope je ~1.30× širší než current 4.57 | Nemění; nula je zahrnuta už v užší obálce |
| Critical 4.569 nebyl přesně reprodukovatelný bez úplného RNG/pooling popisu | Přesný legacy replay = 4.569448; bez bootstrap RNG consumption = 4.371443; cell maximum = 4.746200 | **CONFIRMED** | Přesně popsán RNG, pořadí, pooling a quantile; text používá 4.57 | Žádná změna bodových odhadů; explicitní implementační rozsah | Nemění qualitative non-detection, snižuje falešnou numerickou přesnost |
| `ar2_long` není long-memory | Kořeny odpovídají persistentnímu short-memory AR(2); generator má exponenciální, ne hyperbolický memory decay | **CONFIRMED** | Aktivní název `ar2_persistent`, starý pouze backward alias | Žádný | Žádný |
| Absolutní closure má nealokovaný gap | Reprodukováno H_required/AHT/remainder 3.345/2.788/0.557, 2.551/2.151/0.401, 1.767/1.461/0.305 PW na 60/65/70°N | **CONFIRMED** | Přidán samostatný closure report a CSV; 70°N OHT sanity comparison nechává 0.105 PW k midpointu | Absolutní bodové hodnoty beze změny | Zpřesňuje omezení; remainder se neinterpretuje jako OHT |
| Retired `missing_storage_structural_bounds.csv` se stále generoval a četl | Source audit našel writer i downstream čtení | **CONFIRMED** | Aktivní soubor odstraněn; originál ve snapshotu; zástupce má `RETIRED / DO NOT USE`; downstream čtení odstraněno | Staré safe thresholds nejsou aktivním výsledkem | Nemění; odstraňuje metodicky zrušenou větev |
| `climatology_vs_trend_transport.png` ukazoval trend bez uncertainty | Původní uložený obrázek neobsahoval trendovou nejistotu | **CONFIRMED** | Přidána declared scenario envelope, ARFIMA stress meze, strojová plot-data a explicitní caption | Žádné trendy se nezměnily | Brání vizuálně chybnému dojmu detekce |
| Termín 95% CI byl použit pro DGP-kalibrovanou obálku | Aktivní Stage 10 CSV a dokumentace obsahovaly `calibrated_ci`/`WITH_CI` | **CONFIRMED** | Aktivní výstupy používají `scenario_envelope`; skutečné nominální HAC CI zůstávají odlišeny | Žádný | Zpřesňuje inferenční tvrzení |
| Některé strukturální nejistoty musí zůstat nevyčíslené | Pro tyto složky není v současném workspace nezávislá cap-resolved distribuce/bound | **CONFIRMED** | Explicitní seznam `UNQUANTIFIED`; žádný combined threshold | Žádný nový ad-hoc bound | Non-detection zůstává podmíněná, nikoli důkaz nuly |

## Neměnnost fyzikálních výsledků

Kontrola proti `STAGE11_BASELINE.md` ukazuje změnu hlavních H_corr bodových trendů menší než `1×10⁻¹² TW/dekádu`. Nezměnily se CERES geometry, ERA5 integration, NCEI OHC integration, PIOMAS latent-energy sign, algebra ani absolute transport values.

## Verdict after response

Druhý auditní verdikt zůstává konzistentní s reprodukcí: absolutní redistribuce a storage-corrected budget jsou reprodukovány; trend inference je konzervativní, scénářově podmíněná a zatížená významnými nevyčíslenými strukturálními limity. Nebyl nalezen nový major finding.
