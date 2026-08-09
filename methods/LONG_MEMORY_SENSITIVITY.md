# ARFIMA long-memory sensitivity

## Stav připomínky

**CONFIRMED.** Původní `ar2_long` nebyl proces s dlouhou pamětí; byl přejmenován na `ar2_persistent`. Nezávislá ARFIMA(0,d,0) citlivost potvrzuje, že při `d=0,45` je historická deklarovaná scénářová obálka užší, než vyžaduje tento stress test.

## Implementace

- proces: stacionární Gaussian ARFIMA(0,d,0), `0 ≤ d < 0,5`;
- koeficienty `(1-L)^(-d)` jsou počítány stabilní rekurzí;
- 4096měsíční filtr a 4096měsíční burn-in;
- 216měsíční syntetický záznam, stejná integrace na stav a stejné tři storage derivátory jako v deklarované matici;
- 1500 realizací na každou z pravdivých trendových buněk 0/10/40 TW/dekádu, celkem 4500 standardizovaných chyb pro každé `d` a derivátor;
- samostatný dokumentovaný PCG64 seed pro každé `d`;
- q95: `numpy.quantile(method="linear")`, pooled přes tři pravdivé trendy uvnitř jednoho `d` a derivátoru;
- ARFIMA není automaticky přidána do hlavního DGP obalu.

## Hlavní derivátor `block_12m_means`

| d | seed | n na trend / pooled n | coverage pod současnou obálkou 4,57 | minimum cell coverage | q95 `|error|/SE` | empirical SD | mean SE | bias |
|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| 0,20 | 20262809 | 1500 / 4500 | 0,954 | 0,947 | 4,446 | 31,77 | 16,78 | −0,29 |
| 0,35 | 20264309 | 1500 / 4500 | 0,934 | 0,927 | 4,987 | 55,28 | 25,94 | +0,16 |
| 0,45 | 20265309 | 1500 / 4500 | 0,894 | 0,889 | **5,935** | 85,22 | 34,35 | −1,08 |

SD, SE a bias jsou v TW/dekádu. Monte Carlo SE coverage pro `d=0,45` je 0,0046.

Auditní hodnoty přibližně coverage 0,88 a critical 6,03 se tedy reprodukovaly s rozdílem odpovídajícím odlišnému seedu, konečné délce frakčního filtru a Monte Carlo kolísání. Prakticky se long-memory stress násobek reportuje jako **5,94 (přibližně 6,0)**.

## Dvě oddělené obálky

A. **Current declared DGP scenario envelope:** critical 4,57 pro hlavní derivátor. Pokrývá předem deklarované white/AR(1)/persistent AR(2) scénáře.

B. **Long-memory stress envelope:** critical 5,94 pro ARFIMA `d=0,45`. Je to citlivost mimo hlavní deklarovanou DGP množinu.

Tyto obálky se nesčítají ani neslučují. ARFIMA rozšiřuje intervaly přibližně o faktor `5,935/4,569 = 1,30`, ale kvalitativní závěr se nemění: znaménko ani velikost trendu `H_corr` nebyly rozlišeny už pod užší deklarovanou obálkou.

Strojově čitelné výsledky jsou v `long_memory_sensitivity.csv` a metadata v `long_memory_sensitivity_metadata.json`.
