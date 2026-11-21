# 🎲 Lotto Quest

**Przeglądarkowa gra w stylu roguelike.**
Wspinaj się po rozgałęzionej mapie, wybieraj walki, rzucaj kością D100 i sprawdź, z iloma punktami uda ci się wyjść — jeśli szanse na to pozwolą.

Stworzona w [Phaser 3](https://phaser.io/) podczas **Hackathonu Bydgoszcz 2025**.

<!-- Wskazówka: dodaj tu screenshot albo GIF, np. ![Rozgrywka](docs/screenshot.png) -->

---

## 🕹️ Jak grać

1. Kliknij **GRAJ** i wpisz swoją nazwę.
2. Zaczynasz przy ognisku ze **100 punktami** i **3 życiami** ❤️.
3. Na każdym poziomie wybierasz jedną z maksymalnie trzech ścieżek strzałkami:

   | Klawisz | Ruch |
   |---------|------|
   | `←` | lewa ścieżka |
   | `↑` | środkowa ścieżka |
   | `→` | prawa ścieżka |

4. Wejście na teren potwora oznacza **rzut kością D100**. Każdy potwór ma widoczny próg (np. `D65+`) — wyrzuć tyle albo więcej, żeby wygrać.
5. Dotrzyj do **Bossa** na szczycie mapy i zagraj o wszystko rzutem monetą: punkty **×2** albo **×0,5**.
6. Twój wynik trafia do lokalnego rankingu **Top 10**.

Gra kończy się wcześniej, jeśli stracisz wszystkie 3 życia albo twoje punkty spadną prawie do zera — wtedy wynik wynosi 0.

## 👹 Potwory

| Potwór | Szansa na wygraną | Wygrana | Przegrana |
|--------|------------------|---------|-----------|
| 🟢 **Niskie ryzyko** | 60–90% | mały zysk | tracisz 20–35% punktów i 1 życie |
| 🔴 **Wysokie ryzyko** | 20–50% | duży zysk | tracisz 50–80% punktów i 1 życie |
| 💀 **Boss** | 50% | punkty ×2 | punkty ×0,5 |

Szanse każdego potwora są losowane od nowa, więc liczba nad nim ma znaczenie — przyjrzyj się mapie, zanim ruszysz.

## 📐 Matematyka w tle

Lotto Quest to nie tylko losowość — pod spodem działa prawdziwy model gry hazardowej. Każde zwykłe starcie ma **RTP (zwrot dla gracza) na poziomie 85%**:

```
zysk = (1 − szansaWygranej) × procentStraty / szansaWygranej × RTP
```

Oznacza to, że każda zwykła walka ma **ujemną wartość oczekiwaną**: średnio im dłużej grasz, tym więcej tracisz — dokładnie jak w prawdziwych grach losowych. Potwory wysokiego ryzyka płacą więcej, ale nie pokonają „kasyna”. Jedyny zakład na twoją korzyść to Boss (wartość oczekiwana ×1,25), więc prawdziwe pytanie brzmi: *czy dojdziesz do niego z czymkolwiek w kieszeni?*

Gra pokazuje też komunikaty „O MAŁY WŁOS!” — ten sam rodzaj informacji zwrotnej, którego używają prawdziwe produkty hazardowe, żeby zatrzymać gracza przy grze. Zwróć uwagę, jak to działa na ciebie.

## 🚀 Uruchomienie lokalnie

Bez budowania i bez instalowania zależności — Phaser ładuje się z CDN.

```bash
git clone https://github.com/pilarhz/Lotto-Quest.git
cd Lotto-Quest
python3 -m http.server 8000
```

Następnie otwórz <http://localhost:8000>.

> Otwarcie `index.html` bezpośrednio z dysku może w niektórych przeglądarkach blokować ładowanie grafik, dlatego uruchom folder przez dowolny lokalny serwer (Python, `npx serve`, Live Server w VS Code…).

## 📁 Struktura projektu

```
Lotto-Quest/
├── index.html    # szkielet strony + okno wpisywania nazwy gracza
├── main.js       # logika gry: model szans, sceny, ranking
├── style.css     # wygląd strony i okna nakładki
└── assets/       # mapa, potwory, boss, postać gracza, ognisko
```

Sceny: `PreloadScene` → `MenuScene` → `GameScene` / `RulesScene` / `LeaderboardScene`.
Wyniki są zapisywane w `localStorage` przeglądarki (klucz `lottoScores`), więc ranking jest osobny dla każdego urządzenia.

## 🛠️ Technologie

- [Phaser 3.87](https://phaser.io/) (Arcade Physics, tweeny, kamery)
- Czysty JavaScript, HTML, CSS

