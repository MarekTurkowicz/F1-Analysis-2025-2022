# Wnioski po analizie danych F1

**Dane:** Austrian GP i Azerbaijan GP 2025, tylko wyścigi. 2095 okrążeń, 20 kierowców, pełna telemetria każdego okrążenia.
**Szczegóły i wszystkie wykresy:** [Analiza danych](Analiza_danych.md) · [raport HTML](../Raport/raport_analizy_F1.html) (otwórz lokalnie w przeglądarce) · [hipotezy i plan modelu](Hipotezy_i_model.md) · [notebook](../notebooks/Analiza%20korelacji%20parametrow%20F1%20-%20pelna.ipynb) · [wszystkie wykresy](../Raport/)

---

## Najkrócej: co pokazały dane

| # | Wniosek | Pewność |
|---|---|---|
| 1 | Czas okrążenia zależy przede wszystkim od **prędkości w zakrętach**, a nie od prędkości na prostej. | wysoka, oba tory |
| 2 | **Jazda za rywalem** daje DRS i wyższą prędkość maksymalną; wpływ na sektory zależy od toru. | wysoka / średnia |
| 3 | **Pogoda** zmienia się razem z upływem wyścigu, więc jej wpływu nie da się na razie oddzielić. | — |
| 4 | Część parametrów (pozycja, biegi, obroty) opisuje **auto i kierowcę**, a nie konkretne okrążenie. | wysoka |
| 5 | **Opony** słabo korelują z innymi parametrami; degradacja jest widoczna tylko w Austrii. | niska, za mało danych |
| 6 | Okrążenia za **Safety Car** dominują dane i trzeba je odfiltrowywać. | wysoka |
| 7 | **Jakość danych** jest dobra: brak duplikatów, braki tylko tam, gdzie wynikają z definicji. | wysoka |

---

## Co to znaczy, po ludzku

### 1. Szybkie okrążenie = szybkie zakręty
Liczyliśmy korelację, czyli to, jak mocno dwa parametry zmieniają się razem. Wartość bliska −1 lub +1 oznacza silny związek, a bliska 0 brak związku.
- Czas okrążenia a średnia prędkość minimalna w zakrętach: **−0.90** (Austria) i **−0.86** (Baku). Im szybciej przez zakręty, tym krótsze okrążenie.
- Związek nie znika, gdy patrzymy na **jednego kierowcę** naraz. Nie chodzi więc tylko o to, że lepsze auto jest szybsze wszędzie. Także w obrębie jednego auta lepsze okrążenie to lepsze zakręty.
- Prędkość maksymalna na prostej **prawie nie** wiąże się z czasem okrążenia.

### 2. Jazda za rywalem
- Gdy auto jedzie < 1 s za innym, częściej ma otwarty DRS (korelacja ok. **0.8**), a wtedy osiąga wyższą prędkość maksymalną (ok. **0.75**).
- W części sektorów ten efekt ma **przeciwny znak** w Austrii i w Baku, więc zależy od toru.

### 3. Pogoda to w tych danych głównie zegar
Tor stygnie w trakcie wyścigu: temperatura toru a numer okrążenia daje korelację **−0.87**. Każda zależność „temperatura → czas” jest więc pomieszana z tym, że im dalej w wyścig, tym mniej paliwa i inne opony. Żeby zbadać pogodę, potrzeba wyścigów w różnych warunkach.

### 4. Co jest cechą auta i kierowcy
Pozycję, liczbę zmian biegów i średnie obroty w **50–90%** wyjaśnia sam kierowca lub zespół. Przykład: pozycja koreluje z czasem okrążenia (0.4), ale u jednego kierowcy ta zależność znika. Auta z przodu są szybsze, a pozycja sama w sobie tempa nie zmienia. Wniosek dla modelu: **kierowcę i zespół trzeba podać jako zmienną**.

### 5. Opony
- Rodzaj mieszanki wyjaśnia **≤ 10%** zmienności dowolnego parametru na normalnych okrążeniach.
- Wstępny model degradacji (szczegóły: [Hipotezy i plan modelu](Hipotezy_i_model.md)):
  - **Austria:** opona traci ok. **0.05–0.06 s na okrążenie** (MEDIUM i HARD).
  - **Baku:** ok. **0.015 s** (HARD), a MEDIUM bez istotnej straty.
- Pit stopów jest bardzo mało: 54 na oba wyścigi. To ok. 1 okrążenie z pit stopem na 33–45 zwykłych.

### 6. Safety Car
Status toru (zielona flaga, SC, VSC) wyjaśnia **82% (Austria) i 96% (Baku)** zmienności czasu okrążenia, gdy liczymy wszystkie okrążenia. Bez odfiltrowania tych okrążeń każda analiza pokazuje głównie różnicę „SC vs normalna jazda”.

---

## Hipotezy i plan modelu
Czy trenowanie modelu ma sens, hipoteza o oponach i rekomendowane kroki: **[Hipotezy i plan modelu](Hipotezy_i_model.md)**.

---

## Ograniczenia
- Tylko 2 wyścigi, a część zależności zmienia się między torami.
- Korelacja ≠ przyczyna.
- Okrążenia jednego kierowcy nie są niezależne, więc p-wartości są zbyt optymistyczne. Patrzymy głównie na siłę i powtarzalność zależności.
