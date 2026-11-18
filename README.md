# BloodChess 3D — Repozytorium Assetów i Dokumentacji Inżynieryjnej

> **BloodChess** to taktyczna, brutalna gra szachowa 3D czasu rzeczywistego (Three.js / WebGL) łącząca klasyczne zasady szachowe z unikalnymi zdolnościami 10 zróżnicowanych frakcji, filmowymi sekwencjami egzekucji Hetmana (Takedowns) oraz monumentalną scenografią gotyckich lochów.

---

## 🗺️ Główny Spis Treści (Master Index)

Aby ułatwić pracę w programie **Studio** oraz zapobiec przekraczaniu limitów czasu zapytań (timeout), dokumentacja została podzielona na wyspecjalizowane, zwięzłe moduły:

| Moduł dokumentacji | Ścieżka | Opis zawartości |
| :--- | :--- | :--- |
| 📍 **Centralny Spis Treści** | [docs/INDEX.md](docs/INDEX.md) | Szczegółowa mapa całego projektu, tabelaryczny przewodnik nawigacyjny |
| 🤖 **Instrukcja dla Studio** | [docs/INSTRUKCJA_STUDIO_INTERAKCJA_KAMERA.md](docs/INSTRUKCJA_STUDIO_INTERAKCJA_KAMERA.md) | Kod TypeScript, system selekcji Double-Tap (PC/Mobile), blokada kamery, symbole 3D |
| 📦 **Katalog Modeli 3D** | [modeleBC/README.md](modeleBC/README.md) | Rejestr 30 modeli `.glb` (postacie, szkielety, sockety, bronie ról, cokoły, arena lochów) |
| ⚔️ **Scenariusze Egzekucji** | [Scenarios/README.md](Scenarios/README.md) | Choreografia i klatki kluczowe 10 filmowych cutscenek bicia Hetmana |
| 🗺️ **Roadmapa Assetów 3D** | [docs/ROADMAP_ASSETOW_3D.md](docs/ROADMAP_ASSETOW_3D.md) | Backlog migracji procedularnych brył Three.js do dedykowanych modeli GLB |
| 🛠️ **Dokument Technologiczny** | [docs/DOKUMENT_TECHNOLOGICZNY.md](docs/DOKUMENT_TECHNOLOGICZNY.md) | Uzasadnienie stosu technologicznego (Three.js, glTF, Blender, TypeScript) |
| 📖 **Studium Przypadku (Case Study)** | [docs/STUDY_CASE_10000H.md](docs/STUDY_CASE_10000H.md) | Kronika „Po 10 000 godzin vibecodingu jesteś programistą” (15 wpisów w 3 tomach) |

---

## 📁 Struktura Katalogów w Repozytorium

```
.
├── docs/               # Dokumentacja inżynieryjna, instrukcje wdrożeniowe i Case Study
├── modeleBC/           # Dedykowane, zoptymalizowane modele produkcyjne 3D (.glb) i podglądy
├── Scenarios/          # Specyfikacje techniczne 10 sekwencji filmowych takedownów
├── BloodChess/         # Studyjne linie dialogowe i kwestie audio frakcji (.wav 48 kHz)
├── Soundtrack/         # Ścieżka dźwiękowa i system dynamicznego miksu audio
├── Cutscenes/          # Referencyjne pliki wideo MP4 do animacji takedownów
└── FBX/                # Biblioteka 52 surowych modeli postaci i rekwizytów
```

---

## ⚡ Standardy Projektowe (Ściągawka dla Studia)

1. **Wymiary planszy i siatka bitewna:**
   - Platforma szachownicy: $10.40\text{ m} \times 10.40\text{ m}$.
   - Szachownica ($8 \times 8$ pól): $9.20\text{ m} \times 9.20\text{ m}$.
   - Dokładny wymiar 1 pola szachowego: **`1.15 m x 1.15 m`**.
   - Model produkcyjny: `modeleBC/plansza.glb`.

2. **Kamera Meczowa (Locked Gameplay Camera):**
   - Pozycja dla Białych: `(0, 7.8, 8.2)`, cel: `(0, 0, -0.4)`, FOV: `42°`–`45°`.
   - `OrbitControls` muszą być zablokowane na czas partii (`controls.enabled = false`).

3. **System Selekcji Double-Tap (PC + Ekran Dotykowy):**
   - **Tap 1 (Inspekcja):** Lewitujący symbol 3D roli Unicode obraca się nad głową figury w barwie jej armii + podświetlenie pól ruchu/ataku.
   - **Tap 2 (Wykonanie):** Kliknięcie podświetlonego kafelka uruchamia ruch / filmowy atak.
   - **Kliknięcie wroga:** Bezpieczne (nigdy nie powoduje pomyłkowego ruchu). Zasięg wroga podświetlany **wyłącznie w poziomie Easy przeciwko AI**.

4. **Kompletna Scenografia Areny (`modeleBC/sceneria_lochy.glb`):**
   - Centralna szachownica, dwustronne schody wejściowe (szerokość $5.20\text{ m}$), 4 narożne koksowniki z płonącym ogniem ($X, Y = \pm 5.35\text{ m}$), mury odsunięte na $X = \pm 10.50\text{ m}$ (ponad $4.5\text{ m}$ wolnego korytarza dla $100\%$ czystego widoku planszy) oraz 4 powiewające sztandary.

5. **Postacie i Sockety (`modeleBC/`):**
   - Wszystkie modele postaci posiadają szkielet 19 kości oraz wbudowane punkty montażowe: `Socket_Crown`, `Socket_Hand_R`, `Socket_Hand_L`, `Socket_Back`.
