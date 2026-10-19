# Analiza F1 — kontekst projektu

Projekt studencki (ZSSI): analiza korelacji parametrów F1 2025, później trening modelu.
Etap obecny: **neutralna analiza wszystkich parametrów** (bez założonego celu). Pomysł „model kiedy zmieniać opony” to tylko hipoteza — nie kierować pod nią analizy bez prośby.

## Pliki
- `notebooks/Analiza korelacji parametrow F1 - pelna.ipynb` — główny notebook (cache, katalog parametrów, macierze, ranking par, odporność, tory, nieliniowe, η² kategorii, telemetria próbkowa, wnioski).
- `notebooks/Austrian and Azerbaijan Grand Prix parameters corelations.ipynb` — oryginał użytkownika (nie ruszać bez prośby).
- `notebooks/archiwum/` — kopie archiwalne (v1 oryginał, v2 hipoteza opon).
- `Raport/` — lokalna kopia wyników (raport_analizy_F1.html + PNG + CSV; CSV są w .gitignore); `Raport/hipoteza_opony/` — wykresy hipotezy opon. Notebook generuje je w `reports/`.
- `Wnioski po analizie/` — `Wnioski.md` (neutralne wnioski), `Analiza_danych.md` (opis EDA), `Hipotezy_i_model.md` (hipoteza opon/pit stopów + plan modelu).
- `Eksploracyjna analiza danych.pdf` — wykład ZSSI o EDA; notebook pokrywa jego elementy (typy atrybutów, statystyki, jakość danych, IR, tabele krzyżowe, wykresy słupkowe/pudełkowe/skrzypcowe/liniowe/rozrzutu/pairplot/heatmapa, wnioski).

## Uruchamianie
- Docelowo **Google Colab** (także z VS Code przez rozszerzenie `google.colab`). Drive: `MyDrive/F1-Research/{cache,reports}`.
- Bez Drive → `/content/F1-Research` (cache nietrwały); lokalnie → `./F1-Research` lub `F1_ROOT`.
- Zakres: Austrian GP + Azerbaijan GP 2025, **tylko Race**.

## Dane (TracingInsights-Archive/2025, surowe JSON)
- `{Event}/Race/{DRV}/laptimes.json` (klucze skrócone: time,s1..s3,compound,stint,life,pos,status,pin,pout,vi1,vi2,vfl,vst,wAT,wTT,…; 'None' jako string), `{lap}_tel.json` → `tel`: time,rpm,speed,gear,throttle,brake,drs(0/1!),distance,DriverAhead,DistanceToDriverAhead,acc_x/y/z,x,y,z.
- `corners.json` (CornerNumber, Distance), `weather.json`, `rcm.json`, `drivers.json`.
- TrackStatus: 1 zielona, 2 żółta, 4 SC, 5 czerwona, 6/7 VSC.
- RAW pobierany raz (sparse clone do temp) → parquet w `cache/2025/`; `PARSER_VERSION` podbić przy zmianie liczenia cech.

## Konwencje
- Komentarze i markdown po polsku; wykresy matplotlib/seaborn; kolory torów: Austria `#2a78d6`, Baku `#eb6834`.
- Główne korelacje liczone na czystych okrążeniach (`Clean`); pary „definicyjne” oznaczane osobno.
