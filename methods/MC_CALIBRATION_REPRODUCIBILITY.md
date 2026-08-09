# Reprodukovatelnost Monte Carlo kalibrace

## Stav připomínky

**CONFIRMED.** Hodnota 4,5694479449 je bitově reprodukovatelná při přesném zopakování historického algoritmu, ale závisí na implementačně nepodstatné spotřebě společného RNG streamu bootstrapem. Proto se v textu reportuje zaokrouhleně jako **4,57** a označuje se jako násobek Monte Carlo kalibrované scénářové obálky, nikoli jako univerzální kritická konstanta.

## Přesný historický algoritmus

1. Použije se `numpy.random.default_rng(20260808)`, tedy jeden PCG64 stream.
2. Pořadí DGP je `white`, `ar1_0.3`, `ar1_0.6`, `ar1_0.9`, `ar2_persistent`.
3. Uvnitř DGP se projdou pravdivé trendy `0`, `10`, `40` TW/dekádu.
4. Pro každou DGP/trend buňku se jednou vytvoří 600 společných syntetických stavů a tři derivátory.
5. Pořadí derivátorů je `block_12m_means`, `central_12m_endpoints`, `annual_difference`.
6. Po analytických HAC výpočtech spotřebuje tentýž RNG stream 299 moving-block a 299 non-overlap bootstrap výběrů pro každý derivátor a realizaci. Tyto bootstrap SE nejsou vstupem výsledné vybrané HAC obálky, ale posunou RNG před další buňkou.
7. Vybraným SE je HAC(24) pro oba měsíční derivátory a opravený automatický HAC(2) pro annual difference.
8. V každém DGP a derivátoru se spojí hodnoty `|estimate−truth|/SE` ze všech tří pravdivých trendů.
9. Počítá se `numpy.quantile(..., 0.95, method="linear")`.
10. Násobek derivátoru je maximum pěti DGP-specifických q95.

Pro hlavní `block_12m_means` dává tento postup 4,5694479449; maximum pochází z `ar1_0.9`.

## Citlivost na implementační variantu

| Konfigurace | Pooling | Výsledek |
|---|---|---:|
| přesný historický stream včetně bootstrap spotřeby | trend cells pooled within DGP, pak maximum DGP | 4,569448 |
| stejný stream bez nepoužitých bootstrap draws | trend cells pooled within DGP, pak maximum DGP | 4,371443 |
| stejný stream bez bootstrap draws | maximum q95 jednotlivých DGP/trend cells | 4,746200 |
| nezávislá `SeedSequence` pro každou DGP/trend buňku | trend cells pooled within DGP, pak maximum DGP | 4,118552 |
| přesný historický stream | všechny DGP i trendy pooled najednou | 3,736175 |

Auditorův interval přibližně 4,27–4,75 je tedy reprodukován v podstatě přesně pro věcně plausibilní varianty pořadí RNG a poolingu. Rozdíl není chyba klimatických dat ani trendového bodového odhadu; je to Monte Carlo implementační citlivost.

## Současná reportovací konvence

- Strojově čitelná metadata zachovávají přesnou historickou hodnotu a úplný RNG/pooling popis.
- Text a grafy používají `4,57`.
- Výsledek je označen jako **Monte Carlo kalibrovaná scénářová obálka s cílovým empirical coverage 95 % v deklarované DGP matici**.
- Není označen jako standardní 95% confidence interval.
- ARFIMA long-memory citlivost je reportována odděleně a není sloučena do hlavní obálky.

Úplná tabulka variant je v `mc_critical_value_reproducibility.csv`; reprodukční kód je `src/run_stage11_mc_reproducibility.py`.
