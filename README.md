# Analiza danych F1 (ZSSI)

Projekt zespołowy: eksploracyjna analiza danych F1 2025 i przygotowanie do trenowania modelu.

**Zacznij tutaj → [Wnioski po analizie](Wnioski%20po%20analizie/Wnioski.md)**

## Struktura repozytorium

| Ścieżka | Co zawiera |
|---|---|
| `notebooks/Analiza korelacji parametrow F1 - pelna.ipynb` | główny notebook: pobranie danych (raz, z cache), EDA, korelacje, raport |
| `notebooks/Austrian and Azerbaijan Grand Prix parameters corelations.ipynb` | pierwszy notebook (oryginał) |
| `notebooks/archiwum/` | wcześniejsze wersje, w tym notebook hipotezy o oponach (v2) |
| `Wnioski po analizie/Wnioski.md` | najważniejsze wnioski z analizy danych, prostym językiem |
| `Wnioski po analizie/Analiza_danych.md` | opis analizy krok po kroku, z wykresami |
| `Wnioski po analizie/Hipotezy_i_model.md` | hipotezy (opony, pit stopy) i plan modelu |
| `Raport/` | wykresy PNG i `raport_analizy_F1.html` (otwórz lokalnie w przeglądarce); `Raport/hipoteza_opony/` to wykresy hipotezy |
| `raporty/<imię>/` | raporty i notebooki poszczególnych osób z zespołu |

Tabel CSV nie trzymamy w repozytorium. Notebook generuje je razem z wykresami (`reports.zip`).

## Jak uruchomić

1. Otwórz notebook w **Google Colab** (albo w VS Code przez rozszerzenie Google Colab → *Select Kernel → Colab*).
2. *Uruchom wszystko*. Za pierwszym razem dane (~280 MB) pobiorą się do pamięci podręcznej (cache) na Google Drive (`MyDrive/F1-Research`). Kolejne uruchomienia czytają już tylko cache.
3. Wyniki trafiają do `MyDrive/F1-Research/reports/` i pobierają się jako `reports.zip`. Rozpakuj go do `Raport/`, jeśli chcesz zaktualizować repozytorium. Pliki CSV zostaną lokalnie, git je pomija.

Kolejne wyścigi dodajesz, dopisując je do `EVENTS` w komórce konfiguracji. Pobiorą się tylko nowe.

## Zasady dla zespołu

- Własne analizy wrzucaj do `raporty/<twoje-imię>/`: notebook + krótki `README.md` z wnioskami + wykresy PNG.
- Przed commitem notebooka zrób **Clear All Outputs**, chyba że wyniki są potrzebne. Notebooki z obrazkami ważą dużo.
- Nie commituj danych (`F1-Research/`, `*.parquet`, `*.csv`, RAW JSON). Każdy pobiera je sam przez notebook.
- Wnioski piszemy prostym językiem: co widać → co to znaczy → co z tym robimy.
