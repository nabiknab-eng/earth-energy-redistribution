# Posouzení absolutní energetické uzávěry

## Stav připomínky

**CONFIRMED.** Absolutní účetní rozdíl `H_required − ERA5 AHT` byl znovu odvozen přímo z existujícího `storage_corrected_transport_profile.csv`. Algebraická identita se na všech šesti hranicích uzavírá lépe než `1,4×10⁻¹⁵ PW`, ale fyzikální rozdělení zbytku není nezávisle uzavřeno.

`H_required` zde znamená klimatologický **known-storage-corrected required transport** (`H_known+SI`) za společné období 2006-01 až 2022-01. Není to nezávisle pozorovaný actual total transport.

## Absolutní rozklad

| hranice | H_required | ERA5 AHT | unresolved remainder | remainder / total | OHT sanity range | gap k midpointu | mimo sanity range |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 50°N | 4,767 | 3,883 | 0,884 | 18,54 % | — | — | — |
| 60°N | 3,345 | 2,788 | **0,557** | 16,66 % | — | — | — |
| 65°N | 2,551 | 2,151 | **0,401** | 15,71 % | — | — | — |
| 70°N | 1,767 | 1,461 | **0,305** | 17,29 % | 0,15–0,25 | **0,105** | 0,055 |
| 75°N | 1,048 | 0,896 | 0,152 | 14,54 % | — | — | — |
| 80°N | 0,483 | 0,434 | 0,050 | 10,27 % | — | — | — |

Všechny transporty a gapy jsou PW; kladné znamená poleward/northward přes hranici severní čepičky.

## Co znamená „closure gap“

Bez boundary-matched nezávislého OHT produktu zůstává nealokovaný absolutní remainder na 60/65/70°N **0,557 / 0,401 / 0,305 PW**. Druhý audit poskytl pouze řádové literární sanity comparison `0,15–0,25 PW` poblíž 70°N. Toto rozmezí nebylo v Etapě 11 znovu odvozeno a není vstupem výpočtu.

Při porovnání 70°N remainderu 0,305 PW s midpointem 0,20 PW zůstává přibližně **0,105 PW**, tedy rozpočet je zde prakticky uzavřen jen na řád **0,1 PW**. Nad horní hranicí sanity range zůstává 0,055 PW. Obě definice jsou v CSV explicitně odděleny.

## Omezení interpretace

`H_corr − AHT` je unresolved/non-atmospheric remainder. **Není to automaticky OHT.** Může obsahovat:

- oceánský transport;
- storage pod 2000 m;
- land heat a glacier/ice-sheet enthalpy;
- neúplné sea-ice enthalpy terms;
- regionální systematickou chybu CERES;
- NCEI OHC mapping/sampling error;
- ERA5 structural error;
- rozdíly masek, období a produktových reprezentací.

Proto lze bezpečně tvrdit pouze to, že ERA5 atmosféra vysvětluje přibližně 81–90 % klimatologického required transportu na 50–80°N a zbytek zůstává fyzikálně nerozložený. Z tabulky nelze odvodit trend oceánského transportu.

Strojově čitelný zdroj: `absolute_closure_assessment.csv`.
