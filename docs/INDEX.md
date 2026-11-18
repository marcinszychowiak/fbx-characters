# Spis Treści i Przewodnik Nawigacyjny Repozytorium BloodChess (`INDEX.md`)

> **Dla Studia / Dewelopera / Agentów AI:**  
> Ten dokument stanowi **centralną mapę całego repozytorium**. Pozwala błyskawicznie zlokalizować właściwy plik techniczny bez konieczności czytania obszernych dokumentów i bez ryzyka przekroczenia limitu czasu zapytania (timeout).

---

## 🗺️ Szybka Mapa: Gdzie co znaleźć?

| Zadanie w projekcie | Rekomendowany plik do odczytania | Zawartość i przeznaczenie |
| :--- | :--- | :--- |
| **Implementacja kamer i sterowania** | [docs/INSTRUKCJA_STUDIO_INTERAKCJA_KAMERA.md](INSTRUKCJA_STUDIO_INTERAKCJA_KAMERA.md) | Kod TypeScript/Three.js, system Double-Tap (PC+Mobile), zablokowana kamera, symbole 3D, warunkowy zasięg wroga (Easy). |
| **Wczytywanie modeli 3D w grze** | [modeleBC/README.md](../modeleBC/README.md) | Pełny katalog 30 modeli `.glb`: postacie, szkielety (rig), sockety broni i głowy, pivoty, animacje, plansza i arena lochów. |
| **Plan wymiany brył Three.js na GLB** | [docs/ROADMAP_ASSETOW_3D.md](ROADMAP_ASSETOW_3D.md) | Backlog inżynieryjny: priorytety P1-P5 wymiany prymitywów proceduralnych na dedykowane meshe. |
| **Uzasadnienie technologii** | [docs/DOKUMENT_TECHNOLOGICZNY.md](DOKUMENT_TECHNOLOGICZNY.md) | Wybór Three.js, glTF 2.0, Blendera, TypeScriptu – uzasadnienie zrozumiałe dla osób nietechnicznych. |
| **Studium przypadku (Case Study)** | [docs/STUDY_CASE_10000H.md](STUDY_CASE_10000H.md) | Indeks i streszczenie 15 wpisów kroniki „Po 10 000 godzin vibecodingu jesteś programistą”. |
| **Reżyseria i animacje takedownów** | [Scenarios/README.md](../Scenarios/README.md) | Architektura 10 sekwencji bicia Hetmana z podziałem na role, klatki kluczowe i pozycje kamer. |
| **Muzyka i dynamika bitwy** | [Soundtrack/README.md](../Soundtrack/README.md) | Dynamiczny miks audio Three.js, system filtrów Low-Pass, wyciszanie muzyki podczas takedownu. |
| **Kwestie dialogowe frakcji (WAV)** | [BloodChess/README.md](../BloodChess/README.md) | 39 plików audio 48 kHz podzielonych na 10 frakcji. |
| **Referencje wideo MP4** | [Cutscenes/README.md](../Cutscenes/README.md) | 10 wzorcowych filmów referencyjnych dla każdej frakcji. |
| **Surowa baza 52 modeli FBX** | [FBX/README.md](../FBX/README.md) | Biblioteka surowych modeli humanoidów, zwierząt i rekwizytów. |

---

## 📚 Struktura Dokumentacji w `docs/`

```
docs/
├── INDEX.md                              # (Ten plik) Centralny hub nawigacyjny
├── DOKUMENT_TECHNOLOGICZNY.md            # Architektura technologiczna i uzasadnienia wyborów
├── INSTRUKCJA_STUDIO_INTERAKCJA_KAMERA.md# Gotowy kod i parametry sterowania / kamery / symboli
├── INSTRUKCJA_MODELI_3D.md               # Standardy metryczne, riggowanie i punkty montażowe
├── ROADMAP_ASSETOW_3D.md                 # Rejestr migracji proceduralnych brył do GLB
├── STUDY_CASE_10000H.md                  # Streszczenie i rejestr 15 wpisów kroniki
└── study_case/                           # Modułowe tomy studium przypadku
    ├── tom_1_fundamenty_i_rigging.md     # Wpisy 1–5: FBX, GLB, audio, headless rigging
    ├── tom_2_figury_animacje_i_skala.md  # Wpisy 6–10: Oręż, plansza, cokoły, takedown, skala
    └── tom_3_symbole_interakcja_i_sceneria.md # Wpisy 11–15: Symbole Unicode 3D, double-tap, arena lochów
```

---

## 🎬 Scenariusze Egzekucji (`Scenarios/`)

Każdy plik zawiera klatki animacji, czas trwania, zachowanie kamer oraz wyzwalacze audio i VFX:
- `01_Kowboj.md` – Rewolwer pod brodą i strzał w zbliżeniu
- `02_Sabat_Goblinow.md` – Obleczenie łatwopalną miksturą i podpalenie
- `03_Horda.md` – Kanibalistyczny atak zombie na gardło
- `04_Klan_Krwawego_Cienia.md` – Mgnienie katany, dekapitacja i gejzer krwi
- `05_Najemnicy.md` – Taktyczne podcięcie i poderżnięcie gardła
- `06_Korsarze.md` – Powalenie i wielokrotne ciosy sztyletem w parterze
- `07_Rzeznia.md` – Rozpuszczenie twarzy kwasem chemicznym
- `08_Syndykat.md` – Mafijne pchnięcie sztyletem stiletto pod żebro
- `09_Wikingowie.md` – Rozbicie mostka i wbicie topora w pierś
- `10_Zakon.md` – Rytualne ścięcie dwuręcznym mieczem krzyżowca

---

## ⚙️ Kluczowe Zasady Techniczne dla Studia (Pigułka)

1. **Skala planszy i pól:**  
   Plansza ($8 \times 8$) ma wymiary $9.20\text{ m} \times 9.20\text{ m}$. Jedno pole szachowe = dokładnie `1.15 m x 1.15 m`.
2. **Kamera meczowa:**  
   Zablokowana na sztywno (`controls.enabled = false`), pozycja: `(0, 7.8, 8.2)`, cel: `(0, 0, -0.4)`, FOV: `42°`–`45°`.
3. **Selekcja bierek (Double-Tap):**  
   - 1. klik: Inspekcja (obracający się symbol Unicode 3D nad głową w kolorze armii + podświetlenie pól ruchu/bicia).
   - 2. klik: Potwierdzenie akcji (ruch / takedown).
   - Kliknięcie wroga na sucho: Bezpieczne, pokazuje jego symbol; zasięg wroga podświetlany **tylko na poziomie Easy przeciwko AI**.
4. **Punkty montażowe postaci (`modeleBC/`):**  
   Każdy wojownik ma wbudowane sockety: `Socket_Crown`, `Socket_Hand_R`, `Socket_Hand_L`, `Socket_Back`.
