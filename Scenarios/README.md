# Dokumentacja Scenariuszy Cutscenek — BloodChess

Katalog `Scenarios/` zawiera techniczne i reżyserskie specyfikacje scenariuszy dla wszystkich 10 cutscenek takedownów / egzekucji w grze **BloodChess**. Dokumenty te zostały przygotowane w celu precyzyjnej implementacji w silniku gry (Unity, Unreal Engine 5, Godot) oraz dla animatorów i programistów odpowiedzialnych za system walki.

---

## 1. Indeks Frakcji i Scenariuszy

| Nr | Frakcja | ID Scenariusza | Dedykowany Model (`modeleBC/`) | Model Baza (`FBX/`) | Referencja (`Cutscenes/`) | Audio (`BloodChess/`) | Plik Specyfikacji |
| :---: | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **01** | **Kowboj** | `CS_TAKEDOWN_01_COWBOY` | `kowboj.glb` | `Cowboy_Male.fbx` | `kowboj .mp4` | `Kowboj/` (4 pliki) | [01_Kowboj.md](01_Kowboj.md) |
| **02** | **Sabat Goblinów** | `CS_TAKEDOWN_02_GOBLINS` | `goblin.glb` | `Goblin_Male.fbx` | `gobliny .mp4` | `Sabat Goblinów/` (4 pliki) | [02_Sabat_Goblinow.md](02_Sabat_Goblinow.md) |
| **03** | **Horda** | `CS_TAKEDOWN_03_HORDE` | `horda.glb` | `Zombie_Male.fbx` | `horda .mp4` | `Horda/` (5 plików) | [03_Horda.md](03_Horda.md) |
| **04** | **Klan Krwawego Cienia** | `CS_TAKEDOWN_04_BLOOD_SHADOW` | `klan.glb` | `Ninja_Male.fbx` | `klan Krwawego Cienia .mp4` | `Klan Krwawego Cienia/` (4 pliki) | [04_Klan_Krwawego_Cienia.md](04_Klan_Krwawego_Cienia.md) |
| **05** | **Najemnicy** | `CS_TAKEDOWN_05_MERCENARIES` | `najemnicy.glb` | `Soldier_Male.fbx` | `najemnicy .mp4` | `Najemnicy/` (4 pliki) | [05_Najemnicy.md](05_Najemnicy.md) |
| **06** | **Korsarze** | `CS_TAKEDOWN_06_CORSAIRS` | `korsarz.glb` | `Pirate_Male.fbx` | `pirat.mp4` | `Korsarze/` (4 pliki) | [06_Korsarze.md](06_Korsarze.md) |
| **07** | **Rzeźnia** | `CS_TAKEDOWN_07_SLAUGHTERHOUSE` | `rzeznik.glb` | `Chef_Male.fbx` | `rzeźnia .mp4` | `Rzeznia/` (1 plik) | [07_Rzeznia.md](07_Rzeznia.md) |
| **08** | **Syndykat** | `CS_TAKEDOWN_08_SYNDICATE` | `Syndykat.glb` | `Suit_Male.fbx` | `syndykat .mp4` | `Syndykat/` (4 pliki) | [08_Syndykat.md](08_Syndykat.md) |
| **09** | **Wikingowie z krwawego fiordu** | `CS_TAKEDOWN_09_VIKINGS` | `wiking.glb` | `Viking_Male.fbx` | `wikingowie .mp4` | `Wikingowie z krwawego fiordu/` (5 plików) | [09_Wikingowie.md](09_Wikingowie.md) |
| **10** | **Zakon** | `CS_TAKEDOWN_10_HOLY_ORDER` | `zakon.glb` | `Knight_Male.fbx` | `zakon.mp4` | `Zakon/` (4 pliki) | [10_Zakon.md](10_Zakon.md) |

---

## 2. Architektura Systemu Cutscenek w Silniku Gry

### 2.1. Cykl życia sekwencji (Sequence Lifecycle)
Wszystkie takedowny są wykonywane jako **Paired Synchronized Sequences** (Sparowane Sekwencje Kinematyczne). Proces przebiega według poniższego schematu stanów:

```
[Szachownica: Ruch pionka z bicia]
               │
               ▼
   [Inicjalizacja Cutscenki]
   - Zablokowanie wejścia gracza (Input Lock)
   - Ustawienie aktorów w punktach bazowych pola szachowego
   - Ukrycie interfejsu HUD
               │
               ▼
    [Odtworzenie Animacji]
   - Root Motion dla agresora i ofiary zsynchronizowany z punktem zerowym klatki
   - Aktywacja triggerów Audio, VFX, Camera Shake wg tablicy zdarzeń (JSON)
               │
               ▼
       [Punkt Krytyczny]
   - Aplikacja obrażeń śmiertelnych
   - Przełączenie ofiary w stan Ragdoll lub Dismemberment
   - Utworzenie plamy krwi (Ground Decal)
               │
               ▼
     [Zakończenie Sekwencji]
   - Płynny powrót kamery do widoku izometrycznego/szachownicy (Blend 0.5s)
   - Usunięcie zbitego pionka z planszy (Pawn Despawn / Graveyard Transition)
   - Odblokowanie interfejsu i tury kolejnego gracza
```

### 2.2. Standard Nazewnictwa Gniazd Kości (Bone Sockets)
Dla zapewnienia uniwersalnej kompatybilności modeli z folderu `FBX/` oraz dedykowanych modeli z `modeleBC/`, w szkieletach zdefiniowano ustandaryzowane gniazda:
- `hand_r_socket` – prawa dłoń (broń jednoręczna, nóż, pistolet, rewolwer, butelka).
- `hand_l_socket` – lewa dłoń (pochwa, chwyt oburęczny broni długiej).
- `thigh_r_holster_socket` – kabura boczna prawa (Kowboj).
- `hip_l_socket` – mocowanie przy pasie lewym (pochwa katany Klanu Krwawego Cienia).
- `spine_sheath_socket` – mocowanie plecowe (dwuręczny miecz Zakonu).
- `victim_throat_socket` – gardło ofiary (punkt generowania podcięcia / ugryzienia).
- `victim_chest_socket` – klatka piersiowa ofiary (pchnięcia nożem, strzał, wbicie topora).
- `victim_neck_cut_socket` – podstawa szyi do dekapitacji (odłączenie siatki głowy).

---

## 3. Wytyczne Techniczne dla Kreatora / Programu Budującego Grę

1. **Format Czasu i Klatek:**
   - Podstawowy framerate sekwencji referencyjnych wynosi **30 klatek na sekundę**.
   - W silniku 60 fps / 120 fps klatki podlegają interpolacji liniowej krzywych skrętu kości (Quat Slerp).
2. **Krew i Cząsteczki (Particle Systems):**
   - Wszystkie emitery krwi (`VFX_Blood_*`) muszą posiadać włączoną fizykę kolizji ze światem (World Collision) oraz parametr spawnowania dekalów na podłożu w momencie kolizji kropel z posadzką.
3. **Zarządzanie Pamięcią (Garbage Collection):**
   - Po zakończeniu cutscenki (`CutsceneComplete`) i powrocie kamery na planszę, model zbitej ofiary jest wygaszany za pomocą kanału przezroczystości (Alpha Dissolve w czasie 1.0s) i zwalniany z pamięci, aby utrzymać stałą liczbę obiektów na szachownicy.
