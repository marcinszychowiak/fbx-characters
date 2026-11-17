# Scenariusz Cutscenki: Korsarze

## 1. Informacje Ogólne
- **Frakcja:** Korsarze (Piraci / Wilki Morskie)
- **ID Scenariusza:** `CS_TAKEDOWN_06_CORSAIRS`
- **Typ Animacji:** Powalenie i wielokrotne sztyletowanie w parterze / Tackle & Ground Stabbing
- **Czas trwania:** 4.7 sekundy (141 klatek przy 30 fps / 282 klatki przy 60 fps)
- **Plik referencyjny:** `Cutscenes/pirat.mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Pirate_Male.fbx` (wariant opcjonalny: `FBX/Pirate_Female.fbx`)
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/Casual2_Male.fbx` lub `FBX/BaseCharacter.fbx`)
- **Rekwizyty (Props):**
  - Ciężki sztylet piracki / kordelas (Socket: `hand_r_socket`)
  - Opcjonalnie butelka rumu u pasa (Socket: `belt_l_socket`)

### Dźwięki dialogowe (`BloodChess/Korsarze/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `Korsarze 1.wav` (Rekomendowany – piracki okrzyk bojowy)
  - `Korsarze 2.wav`
  - `Korsarze 3.wav`
  - `Korsarze 4.wav`
- **Offset odpalenia głosu:** `0.0s` (przy szarży) oraz `3.8s` (triumfalny śmiech).

### Efekty dźwiękowe (SFX)
- `0.4s`: `sfx_pirate_tackle_impact.wav` – uderzenie taranujące i dźwięk kolizji dwóch ciał.
- `0.7s`: `sfx_body_slam_wood.wav` – potężne trzaśnięcie pleców ofiary o deski/szachownicę.
- `1.2s`: `sfx_dagger_draw_rough.wav` – wyciągnięcie sztyletu z pochwy.
- `1.5s`: `sfx_knife_stab_01_heavy.wav` – pierwsze głębokie pchnięcie w mostek.
- `1.9s`: `sfx_knife_stab_02_heavy.wav` – drugie pchnięcie w klatkę piersiową.
- `2.3s`: `sfx_knife_stab_03_heavy.wav` – trzecie dobijające pchnięcie.
- `1.5s - 2.8s`: `sfx_blood_squirt_wet_rapid.wav` – chlupot krwi i pękających tkanek.
- `1.6s - 2.5s`: `sfx_victim_groan_agony.wav` – urywane jęki przebijanych płuc.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.6** | 0 - 18 | Agresor | Brutalna szarża na ofiarę z obniżonym środkiem ciężkości (rugby tackle / body slam). | Dzika furia, piracka brawura. |
| **0.0 - 0.6** | 0 - 18 | Ofiara | Próbuje uniknąć ataku, lecz zostaje zepchnięta z nóg. | Utrata równowagi, panika. |
| **0.7 - 1.1** | 21 - 33 | Obaj | **POWALENIE NA ZIEMIĘ:** Ofiara ląduje na plecach. Pirat natychmiast siada okrakiem na jej brzuchu (pełny dosiad). | Ofiara uderza potylicą o ziemię. |
| **1.2 - 1.4** | 36 - 42 | Agresor | Błyskawiczne wyciągnięcie sztyletu prawą ręką i uniesienie ramienia wysoko nad głowę. | Szaleńczy uśmiech, zęby zaciśnięte. |
| **1.5** | 45 | Agresor | **CIOS 1:** Potężne wbicie ostrza prosto w klatkę piersiową. | Wstrząs ciała ofiary, pierwszy gejzer krwi. |
| **1.9** | 57 | Agresor | **CIOS 2:** Błyskawiczne wyszarpnięcie i ponowne, jeszcze głębsze pchnięcie w to samo miejsce. | Ostrze chrzęści o żebra. |
| **2.3** | 69 | Agresor | **CIOS 3 (FINISHER):** Ostatnie, oburęczne dociśnięcie ostrza aż po rękojeść w serce ofiary. | Śmiertelny cios kończący opór. |
| **2.4 - 3.2** | 72 - 96 | Ofiara | Ostatnie spazmy mięśni nóg i rąk, po czym ciało wiotczeje. Oczy zamierają w martwym spojrzeniu. | Zgon na polu bitwy. |
| **3.3 - 4.7** | 99 - 141| Agresor | Pirat wyrywa nóż, wstaje powoli, otrzepuje kolana, po czym spluwa na zwłoki i unosi nóż w geście pirackiego wiwatu. | Bezczelna dominacja i triumf. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 0.8s (Taran):**
  - **Typ:** Dynamiczny Tracking Shot z boku, pędzący równolegle do szarżującego pirata.
  - **Camera Shake:** Potężne tąpnięcie w momencie uderzenia o ziemię `0.7s` (amplituda `0.7`, czas `0.3s`).
- **0.9s – 2.6s (Brutalne pchnięcia):**
  - **Typ:** High-Angle Top-Down (ujęcie pionowo z góry pod kątem 75°), skierowane na klatkę piersiową ofiary i wbijający się rytmicznie nóż.
  - **Camera Shake:** Seria trzech kolejnych mikro-wstrząsów przy każdym pchnięciu (`1.5s`, `1.9s`, `2.3s`).
- **2.7s – 4.7s (Wstanie i triumf):**
  - **Typ:** Low-Angle Hero Shot od ziemi w górę ku wstającej sylwetce pirata na tle nieba szachownicy.

---

## 5. Efekty Wizualne (VFX)

- **Podmuch Powalenia (`VFX_Ground_Impact_Dust`):**
  - Chmura kurzu i pyłu wyrzucona spod pleców ofiary przy zderzeniu z podłożem w `0.7s`.
- **Wielopunktowe Rozbryzgi Krwi (`VFX_MultiStab_BloodBurst`):**
  - Emiter trzykrotnie wyrzucający gęste fontanny krwi pod kątem 45 stopni w takt uderzeń ostrza (`1.5s`, `1.9s`, `2.3s`).
- **Rozbryzg na Kamerę (`Screen_Space_Blood_Drops`):**
  - Subtelne czerwone krople krwi lądujące na wirtualnym obiektywie kamery po 3. ciosie.
- **Wielka Kałuża Parterowa (`Decal_Corsair_BloodSpill`):**
  - Rozlewanie się krwi spod pleców i boków ofiary, tworzącej nieregularną, lśniącą kałużę na szachownicy.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_06_CORSAIRS",
  "duration": 4.7,
  "sync_mode": "PairedKinematicGroundMount",
  "events": [
    { "time": 0.05, "type": "AudioVoice", "cue": "BloodChess/Korsarze/Korsarze 1.wav" },
    { "time": 0.40, "type": "AudioSFX", "cue": "sfx_pirate_tackle_impact" },
    { "time": 0.70, "type": "AudioSFX", "cue": "sfx_body_slam_wood" },
    { "time": 0.70, "type": "VFXSpawn", "effect": "VFX_Ground_Impact_Dust", "socket": "victim_spine_socket" },
    { "time": 0.70, "type": "CameraShake", "intensity": 0.7, "duration": 0.3 },
    { "time": 1.20, "type": "AudioSFX", "cue": "sfx_dagger_draw_rough" },
    { "time": 1.50, "type": "AudioSFX", "cue": "sfx_knife_stab_01_heavy" },
    { "time": 1.50, "type": "VFXSpawn", "effect": "VFX_MultiStab_BloodBurst", "socket": "victim_chest_socket" },
    { "time": 1.50, "type": "CameraShake", "intensity": 0.5, "duration": 0.15 },
    { "time": 1.90, "type": "AudioSFX", "cue": "sfx_knife_stab_02_heavy" },
    { "time": 1.90, "type": "VFXSpawn", "effect": "VFX_MultiStab_BloodBurst", "socket": "victim_chest_socket" },
    { "time": 1.90, "type": "CameraShake", "intensity": 0.5, "duration": 0.15 },
    { "time": 2.30, "type": "AudioSFX", "cue": "sfx_knife_stab_03_heavy" },
    { "time": 2.30, "type": "VFXSpawn", "effect": "VFX_MultiStab_BloodBurst", "socket": "victim_chest_socket" },
    { "time": 2.30, "type": "ScreenEffect", "effect": "Screen_Space_Blood_Drops", "intensity": 0.6 },
    { "time": 2.30, "type": "CameraShake", "intensity": 0.65, "duration": 0.2 },
    { "time": 2.50, "type": "SpawnDecal", "decal": "Decal_Corsair_BloodSpill", "attach_to_ground": true },
    { "time": 3.80, "type": "AudioVoice", "cue": "BloodChess/Korsarze/Korsarze 4.wav" },
    { "time": 4.70, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
