# CHANGELOG — finální didakticko-jazyková revize

## Změněné soubory

- `src/build_final_atlas.py`: upraven aktivní generátor textu, popisků, os, legend a automatických kontrol; vědecké výpočty a vstupní datové větve zůstaly beze změny.
- `index.html` a `energy_redistribution_atlas.html`: kompletní česká terminologická a didaktická revize, výraznější hlavní závěr a doplněná vysvětlení EEI, akumulace energie, H_corr, statistické rozlišitelnosti, nejistot, auditu a reprodukovatelnosti.
- `figures/`: všech deset SVG a deset PNG bylo regenerováno ze stávajících auditovaných dat po úpravě čtenářských názvů, os, legend a anotací.
- `data/`: CSV byla znovu vygenerována stejnou pipeline; číselná pole zůstala beze změny. U schématu byly upraveny pouze textové popisy rolí vstupů.
- `README.md`: doplněn odkaz a popis nezávislého auditního balíku.
- `audit/external_audit_bundle_v4.zip`: přiložen již existující auditní balík se zdrojovým kódem, redukovanými referenčními výstupy, testy, specifikacemi downloadů a checksums.
- `CHECKSUMS.sha256`: kontrolní součty všech veřejných souborů atlasu.

## Číselné výsledky

Žádná numerická vědecká hodnota, znaménková konvence, datové období ani závěr nebyly změněny. Bodové trendy H_corr zůstávají +0,77 / −0,11 / +2,75 TW za dekádu na 60°N / 65°N / 70°N; půlšířky základní scénářové obálky 98,85 / 80,12 / 72,84 TW za dekádu.

## Build a testy

- Build `MPLCONFIGDIR=/private/tmp/mpl-final-atlas .venv/bin/python -m src.build_final_atlas`: PASS.
- Projektová testovací sada `.venv/bin/python -m pytest -q tests`: 75 passed.
- Interní self-check atlasu: PASS (odkazy, kotvy, deset popisků, deset CSV, SVG/PNG páry, terminologie, slovníček a shoda bodových výsledků Etapy 11).
- Číselné porovnání všech společných numerických polí deseti grafových CSV proti předchozí publikované verzi: PASS, přesná shoda.
- Neomezené hledání testů přes celý pracovní strom není používáno, protože archivované auditní snapshoty obsahují duplicitně pojmenované testovací moduly; autoritativní projektová sada je adresář `tests/`.
