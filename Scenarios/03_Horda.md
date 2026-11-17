# Scenariusz Cutscenki: Horda

## 1. Informacje Ogólne
- **Frakcja:** Horda (Nieumarli / Zombie)
- **ID Scenariusza:** `CS_TAKEDOWN_03_HORDE`
- **Typ Animacji:** Kanibalistyczny atak na szyję / Throat Tear & Feeding
- **Czas trwania:** 4.7 sekundy (141 klatek przy 30 fps / 282 klatki przy 60 fps)
- **Plik referencyjny:** `Cutscenes/horda .mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Zombie_Male.fbx` (wariant opcjonalny: `FBX/Zombie_Female.fbx`)
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/Casual_Male.fbx`, `FBX/Doctor_Male_Young.fbx` lub `FBX/BaseCharacter.fbx`)
- **Rekwizyty (Props):** Brak broni – atak wykonywany jest wyłącznie nagimi dłońmi i zębami (naturalna broń nieumarłych).

### Dźwięki dialogowe (`BloodChess/Horda/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `horda_wkurzony_01_48k.wav` (Rekomendowany – gardłowy ryk szału)
  - `horda_wkurzony_02_48k.wav`
  - `horda_wkurzony_03_48k.wav`
  - `horda_wkurzony_04_48k.wav`
  - `horda_wkurzony_05_48k.wav`
- **Offset odpalenia głosu:** `0.1s` (pomruk zbliżającego się zombie) oraz `1.6s` (dziki ryk w momencie skoku i wgryzienia).

### Efekty dźwiękowe (SFX)
- `1.5s`: `sfx_flesh_grab_impact.wav` – uderzenie dłoni o ciało ofiary i siłowy chwyt.
- `1.8s`: `sfx_bite_flesh_tear.wav` – chrzęst miażdżonych kości i odrywanego mięsa.
- `1.9s`: `sfx_blood_gush_arterial.wav` – gwałtowny, pulsujący wytrysk krwi pod ciśnieniem.
- `2.0s - 3.2s`: `sfx_victim_choke_gargle.wav` – krztuszenie się i bulgot krwi w krtani ofiary.
- `2.2s - 4.0s`: `sfx_feeding_gore_chewing.wav` – agresywne przeżuwanie i mlaskanie.
- `3.8s`: `sfx_victim_collapse_wet.wav` – upadek bezwładnego ciała w kałużę krwi.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 1.0** | 0 - 30 | Agresor | Chwiejny, powolny marsz w stronę ofiary (zombie walk). Głowa przechylona nienaturalnie na bok. | Puste, wyblakłe oczy, ślinotok zmieszany z czarną krwią. |
| **0.0 - 1.0** | 0 - 30 | Ofiara | Zastyga w przerażeniu, próbuje cofnąć się o pół kroku. | Oddech przyspieszony, spojrzenie pełne grozy. |
| **1.1 - 1.5** | 33 - 45 | Agresor | Nagle przyspiesza: dynamiczny doskok, pazury wbijają się w ramiona i kark ofiary. | Wściekły ryk, rozszerzone szczęki. |
| **1.6** | 48 | Obaj | **WGRYZIENIE (BITE FRAME):** Zombie wbija zęby prosto w szyję i mięsień czworoboczny ofiary. | Gwałtowne zaciśnięcie szczęk. |
| **1.7 - 2.8** | 51 - 84 | Agresor | Agresywne szarpanie głową w lewo i prawo (head-thrashing), wyrywanie kawałów mięsa z szyi. | Czysty szał głodu. |
| **1.7 - 2.8** | 51 - 84 | Ofiara | Rozpaczliwe próby odepchnięcia głowy potwora. Siły gasną, ręce bezwładnie opadają. | Oczy zachodzą mgłą, krew wylewa się z ust. |
| **2.9 - 3.8** | 87 - 114| Ofiara | Bezwładne ciało osuwa się po torsie agresora na kolana, a następnie na podłoże. | Całkowity brak kontroli nad kończynami. |
| **3.5 - 4.7** | 105 - 141| Agresor | Zombie przełyka kęs, unosi zakrwawioną twarz do góry i wydaje chrapliwy ryk dominacji nad ofiarą. | Krew ścieka po brodzie i klatce piersiowej. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.2s (Groza narastająca):**
  - **Typ:** Low-Angle Dutch Angle (kamera lekko przechylona, potęgująca dyskomfort), śledząca powolny krok potwora.
  - **FOV:** 35 mm.
- **1.3s – 2.5s (Uderzenie i rozszarpanie):**
  - **Typ:** Płynny, agresywny najazd kamery (Snap-Zoom) bezpośrednio na poziom szyi i zębów wgryzających się w ciało.
  - **Camera Shake:** Ciągłe mikro-wstrząsy (amplituda `0.4`, częstotliwość `18 Hz`) synchronizowane z szarpnięciami głowy zombie.
- **2.6s – 4.7s (Finał kanibalizmu):**
  - **Typ:** Medium Shot z góry (30° w dół), pokazujący postać zombie stojącą nad leżącym w kałuży krwi trupem.

---

## 5. Efekty Wizualne (VFX)

- **Fontanna Tętnicza (`VFX_Arterial_Blood_Spray`):**
  - Socket: `victim_neck_r_socket`.
  - Wytrysk krwi pulsujący pod ciśnieniem (3 wyraźne impulsy wyrzutu w rytmie akcji serca od `1.8s` do `2.6s`).
- **Latające Fragmenty Tkanek (`VFX_Flesh_Chunks_Gibs`):**
  - Drobne cząstki mięsa i skrzepów wyrzucane w powietrze podczas ruchów szarpiących głowy zombie.
- **Krew na Twarzy i Ubraniu (`Dynamic_Blood_Mask`):**
  - Dynamiczny vertex paint / nałożenie maski krwi na teksturę twarzy i dłoni zombie.
- **Kałuża Krwi (`Decal_Expanding_BloodPool`):**
  - Duża kałuża krwi na szachownicy pod leżącą ofiarą, powiększająca się promieniście do promienia 1.2m do końca cutscenki.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_03_HORDE",
  "duration": 4.7,
  "sync_mode": "PairedKinematicWithBlend",
  "events": [
    { "time": 0.10, "type": "AudioVoice", "cue": "BloodChess/Horda/horda_wkurzony_01_48k.wav" },
    { "time": 1.40, "type": "AudioSFX", "cue": "sfx_flesh_grab_impact" },
    { "time": 1.60, "type": "AudioSFX", "cue": "sfx_bite_flesh_tear" },
    { "time": 1.60, "type": "AudioVoice", "cue": "BloodChess/Horda/horda_wkurzony_03_48k.wav" },
    { "time": 1.70, "type": "VFXSpawn", "effect": "VFX_Arterial_Blood_Spray", "socket": "victim_neck_r_socket" },
    { "time": 1.80, "type": "VFXSpawn", "effect": "VFX_Flesh_Chunks_Gibs", "socket": "aggressor_jaw_socket" },
    { "time": 1.80, "type": "CameraShakeContinuous", "intensity": 0.4, "duration": 1.2 },
    { "time": 1.90, "type": "AudioSFX", "cue": "sfx_blood_gush_arterial" },
    { "time": 2.00, "type": "AudioSFX", "cue": "sfx_victim_choke_gargle" },
    { "time": 2.20, "type": "SpawnDecal", "decal": "Decal_Expanding_BloodPool", "attach_to_ground": true },
    { "time": 3.00, "type": "EnableRagdoll", "target": "Victim", "impulse": [0, -40, -60] },
    { "time": 3.80, "type": "AudioSFX", "cue": "sfx_victim_collapse_wet" },
    { "time": 4.70, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
