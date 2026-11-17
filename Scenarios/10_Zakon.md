# Scenariusz Cutscenki: Zakon

## 1. Informacje Ogólne
- **Frakcja:** Zakon (Święci Rycerze / Templariusze / Paladyni)
- **ID Scenariusza:** `CS_TAKEDOWN_10_HOLY_ORDER`
- **Typ Animacji:** Święty wyrok mieczem dwuręcznym / Downward Execution Cleave
- **Czas trwania:** 4.7 sekundy (141 klatek przy 30 fps / 282 klatki przy 60 fps)
- **Plik referencyjny:** `Cutscenes/zakon.mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Knight_Male.fbx` (wariant opcjonalny: `FBX/Knight_Golden_Male.fbx` lub `FBX/Knight_Golden_Female.fbx`)
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/BaseCharacter.fbx` lub `FBX/Casual_Male.fbx`)
- **Rekwizyty (Props):**
  - Długi miecz rycerski / bastard / dwuręczny miecz zakonny (Socket: `hand_r_socket` / `hand_l_socket` - chwyt oburącz)
  - Pochwa na plecach (Socket: `spine_sheath_socket`)

### Dźwięki dialogowe (`BloodChess/Zakon/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `zakon_donosny_02_48k.wav` (Rekomendowany – uroczysty, donośny wyrok: „W imię Zakonu!”)
  - `zakon_ekscytacja_03_48k.wav`
  - `zakon_szept_04_48k.wav`
  - `zakon_wkurzony_06_48k.wav`
- **Offset odpalenia głosu:** `0.1s` (wyrok wygłaszany podczas unoszenia miecza).

### Efekty dźwiękowe (SFX)
- `0.6s`: `sfx_broadsword_draw_metal.wav` – donośny, czysty dźwięk wyjmowania stali z pochwy.
- `1.2s`: `sfx_twohanded_sword_swing_wind.wav` – głęboki, świszczący pęd ciężkiego ostrza tnącego powietrze.
- `1.4s`: `sfx_heavy_slash_armor_flesh.wav` – potężne rozcięcie mięśni, ścięgien i kości klatki piersiowej.
- `1.5s`: `sfx_holy_blood_burst.wav` – gwałtowny wybuch krwi zmieszany z metalicznym pogłosem.
- `1.6s - 2.8s`: `sfx_victim_death_gasp.wav` – ostatnie tchnienie skazańca.
- `3.0s`: `sfx_knight_armored_step.wav` – ciężki krok opancerzonego buta na podłożu.
- `3.2s`: `sfx_body_split_ground.wav` – opadnięcie rozciętego ciała na szachownicę.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.7** | 0 - 21 | Agresor | Rycerz stoi w zbroi płytowej. Płynnym ruchem sięga za plecy i wyjmuje długi miecz z pochwy. | Wyniosły spokój, majestatyczna postawa sędziego. |
| **0.0 - 0.7** | 0 - 21 | Ofiara | Klęczy lub stoi sparaliżowana obliczem zbliżającej się kary. | Świadomość nieuchronnego końca. |
| **0.8 - 1.3** | 24 - 39 | Agresor | Uniesienie miecza oburącz wysoko ponad głowę w klasyczną postawę egzekucyjną (High Guard). | Ciało wyprostowane, pełna koncentracja. |
| **1.4** | 42 | Obaj | **ŚWIĘTE CIĘCIE (CLEAVE FRAME):** Błyskawiczny, pionowo-skośny zamach ostrzem od prawego barku przez klatkę ku lewemu biodru ofiary. | Błysk na ostrzu, uderzenie z pełną masą zbroi. |
| **1.5 - 2.4** | 45 - 72 | Ofiara | Klatka piersiowa rozcięta na wskroś. Masywny łuk krwi tryska w powietrze w ślad za trajektorią miecza. | Ciało łamie się w pasie, opadając bez sił. |
| **1.5 - 2.6** | 45 - 78 | Agresor | Rycerz zatrzymuje miecz w pozycji niskiej (Low Guard), klinga skierowana w ziemię, dłonie stabilne. | Niewzruszony, obojętny na agonię wroga. |
| **2.7 - 3.4** | 81 - 102| Ofiara | Ciało rozpada się do przodu i na bok, uderzając o szachownicę w powiększającą się kałużę krwi. | Zgon, natychmiastowe ustanie funkcji życiowych. |
| **3.5 - 4.7** | 105 - 141| Agresor | Rycerz wbija czubek miecza w pole szachownicy, kładzie obie dłonie na głowicy i pochyla głowę w niemej modlitwie za duszę pokonanego. | Dostojny, uświęcony rytuał Zakonu. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.0s (Wyrok):**
  - **Typ:** Frontalny Full Shot z lekkiego dołu (Low-Angle), uwypuklający złotą/srebrną zbroję rycerza.
  - **FOV:** 40 mm.
- **1.1s – 2.0s (Święte cięcie):**
  - **Typ:** Dynamiczne cięcie kamery na ujęcie skośne z profilu (Dutch Angle 15°).
  - **Camera Shake:** Czysty, potężny impuls w klatce `1.4s` (amplituda `0.75`, czas `0.3s`) oddający wagę uderzenia dwuręcznego miecza.
- **2.1s – 4.7s (Modlitwa rycerza):**
  - **Typ:** Wolny, majestatyczny obrót kamery (Slow Orbit 30°) wokół rycerza opartego o głowicę miecza.

---

## 5. Efekty Wizualne (VFX)

- **Smuga Świętego Miecza (`VFX_Holy_Sword_Arc`):**
  - Złocisto-biała, jaskrawa wstęga światła ciągnąca się za ostrzem w momencie cięcia (`1.2s - 1.5s`).
- **Wielki Łuk Krwi (`VFX_Diagonal_Blood_Arc`):**
  - Socket: `victim_spine_cleave_socket`.
  - Szeroki, skośny wachlarz krwi podążający za ruchem klingi przez tułów.
- **Krople Spływające po Stali (`Dynamic_Blood_Sword_Drip`):**
  - Krew spływająca po zbroczu miecza w stronę czubka wbitego w ziemię.
- **Kałuża Rozciętego Ciała (`Decal_Order_Cleave_Pool`):**
  - Długa, skośna plama krwi na szachownicy odzwierciedlająca trajektorię cięcia.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_10_HOLY_ORDER",
  "duration": 4.7,
  "sync_mode": "PairedKinematicWithPrayerIdle",
  "events": [
    { "time": 0.10, "type": "AudioVoice", "cue": "BloodChess/Zakon/zakon_donosny_02_48k.wav" },
    { "time": 0.60, "type": "AudioSFX", "cue": "sfx_broadsword_draw_metal" },
    { "time": 1.25, "type": "VFXSpawn", "effect": "VFX_Holy_Sword_Arc", "socket": "sword_blade_tip" },
    { "time": 1.30, "type": "AudioSFX", "cue": "sfx_twohanded_sword_swing_wind" },
    { "time": 1.40, "type": "AudioSFX", "cue": "sfx_heavy_slash_armor_flesh" },
    { "time": 1.40, "type": "VFXSpawn", "effect": "VFX_Diagonal_Blood_Arc", "socket": "victim_spine_socket" },
    { "time": 1.40, "type": "CameraShake", "intensity": 0.75, "duration": 0.3 },
    { "time": 1.50, "type": "AudioSFX", "cue": "sfx_holy_blood_burst" },
    { "time": 1.60, "type": "AudioSFX", "cue": "sfx_victim_death_gasp" },
    { "time": 2.50, "type": "SpawnDecal", "decal": "Decal_Order_Cleave_Pool", "attach_to_ground": true },
    { "time": 2.70, "type": "EnableRagdoll", "target": "Victim", "impulse": [-40, -80, -30] },
    { "time": 3.00, "type": "AudioSFX", "cue": "sfx_knight_armored_step" },
    { "time": 3.20, "type": "AudioSFX", "cue": "sfx_body_split_ground" },
    { "time": 4.70, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
