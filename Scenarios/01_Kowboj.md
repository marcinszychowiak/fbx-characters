# Scenariusz Cutscenki: Kowboj

## 1. Informacje Ogólne
- **Frakcja:** Kowboj (Pogranicze / Dziki Zachód)
- **ID Scenariusza:** `CS_TAKEDOWN_01_COWBOY`
- **Typ Animacji:** Egzekucja bezpośrednia / Point-Blank Execution
- **Czas trwania:** 4.5 sekundy (135 klatek przy 30 fps / 270 klatek przy 60 fps)
- **Plik referencyjny:** `Cutscenes/kowboj .mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Cowboy_Male.fbx` (wariant opcjonalny: `FBX/Cowboy_Female.fbx`)
  - Akcesoria: `FBX/Cowboy_Hair.fbx`
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/Casual_Male.fbx` lub `FBX/BaseCharacter.fbx`)
- **Rekwizyty (Props):**
  - Rewolwer rewolwerowca (Socket: `hand_r_socket`)
  - Kabura na pasie (Socket: `thigh_r_holster_socket`)

### Dźwięki dialogowe (`BloodChess/Kowboj/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `kowboj_wkurzony_01_48k.wav` (Rekomendowany)
  - `kowboj_wkurzony_02_48k.wav`
  - `kowboj_wkurzony_03_48k.wav`
  - `kowboj_wkurzony_04_48k.wav`
- **Offset odpalenia głosu:** `0.2s` (klatka 6 przy 30 fps)

### Efekty dźwiękowe (SFX)
- `0.8s`: `sfx_leather_holster_draw.wav` – dźwięk szybkiego wysunięcia rewolweru z kabury.
- `1.8s`: `sfx_revolver_cock.wav` – odciągnięcie kurka rewolweru z metalicznym klikiem.
- `2.1s`: `sfx_gunshot_heavy_revolver.wav` – ogłuszający wystrzał z bliska z pogłosem i basowym uderzeniem.
- `2.2s`: `sfx_gore_impact_headshot.wav` – mięsisty rozbryzg tkanek i czaszki.
- `3.2s`: `sfx_bodyfall_heavy_dirt.wav` – bezwładny upadek bezwładnego ciała na podłoże.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.7** | 0 - 21 | Agresor | Stoi twarzą w twarz z ofiarą (odległość 0.8m). Prawa dłoń spoczywa swobodnie przy pasie. | Zimne, bezwzględne spojrzenie spod ronda kapelusza. |
| **0.0 - 0.7** | 0 - 21 | Ofiara | Sparaliżowana strachem, dłonie lekko uniesione w geście poddania. | Rozszerzone źrenice, drżenie mięśni. |
| **0.8 - 1.5** | 24 - 45 | Agresor | Błyskawiczny ruch prawą ręką (quick-draw). Rewolwer wyjęty z kabury i skierowany wprost pod brodę ofiary. | Płynny, wyćwiczony odruch rewolwerowca. |
| **1.6 - 2.0** | 48 - 60 | Agresor | Lufa rewolweru dotyka spodu żuchwy ofiary, wymuszając odchylenie jej głowy w tył. | Kciuk agresora odciąga kurek (`revolver_cock`). |
| **2.1** | 63 | Obaj | **STRZAŁ (IMPACT FRAME):** Agresor pociąga za spust. Odrzut broni unosi lufę o 15 stopni w górę. | Błysk wystrzału (Muzzle Flash), dym prochowy. |
| **2.1 - 2.8** | 63 - 84 | Ofiara | Głowa zostaje gwałtownie odrzucona w tył pod wpływem impetu kuli. Ciało traci napięcie mięśniowe. | Niekontrolowany odrzut tułowia do tyłu. |
| **2.8 - 3.8** | 84 - 114 | Ofiara | Bezwładne osuwanie się na plecy / ragdoll. Upadek na deski szachownicy. | Uderzenie o podłoże, krew rozlewa się pod głową. |
| **3.5 - 4.5** | 105 - 135| Agresor | Efektowny obrót rewolweru na palcu (gun spin), zdmuchnięcie dymu z lufy i powolne schowanie do kabury. | Triumfalny, surowy uśmieszek. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.5s (Ujęcie wprowadzające):**
  - **Typ:** Medium Shot z profilu (kąt 45°).
  - **FOV:** 45 mm (portretowy, płytka głębia ostrości). Ostrość na agresorze.
- **1.6s – 2.5s (Ujęcie ciosu krytycznego):**
  - **Typ:** Dynamiczne zbliżenie Low-Angle (Close-Up) od dołu lufy rewolweru pod brodą ofiary.
  - **Camera Shake:** Impuls wstrząsu o amplitudzie `0.7` i czasie wygasania `0.35s` dokładnie w momencie strzału (`2.1s`).
- **2.6s – 4.5s (Ujęcie finałowe):**
  - **Typ:** Szerokie ujęcie z góry (High-Angle) śledzące upadek ofiary na szachownicę i zatrzymujące się na sylwetce Kowboja chowającego broń.

---

## 5. Efekty Wizualne (VFX)

- **Muzzle Flash (`VFX_MuzzleFlash_Revolver`):**
  - Socket: `gun_barrel_socket` na rewolwerze.
  - Czas trwania: 2 klatki, jaskrawy żółto-pomarańczowy błysk świetlny (Light Source: Radius 3.5m, Intensity 8.0, rzucający cienie).
- **Proch i Dym (`VFX_GunSmoke`):**
  - Subtelny obłok szarego dymu unoszący się z lufy po wystrzale przez kolejne 1.5s.
- **Rozbryzg Krwi (`VFX_Blood_ExitWound_Heavy`):**
  - Emiter stożkowy skierowany pod kątem 60° w górę i w tył za głową ofiary w momencie uderzenia pocisku (`2.1s`).
  - Cząsteczki krwi w locie (Blood droplets + misty red haze).
- **Ślad na podłożu (`Decal_BloodSplatter_Floor`):**
  - Projekcja plam krwi na pole szachownicy pod i za upadającym ciałem.
  - Płynne rozszerzanie się kałuży (grow animation) od `2.3s` do `4.5s`.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_01_COWBOY",
  "duration": 4.5,
  "sync_mode": "PairedKinematicWithRagdollBlend",
  "events": [
    { "time": 0.20, "type": "AudioVoice", "cue": "BloodChess/Kowboj/kowboj_wkurzony_01_48k.wav" },
    { "time": 0.80, "type": "AudioSFX", "cue": "sfx_leather_holster_draw" },
    { "time": 0.85, "type": "AttachProp", "prop": "Revolver", "socket": "hand_r_socket" },
    { "time": 1.80, "type": "AudioSFX", "cue": "sfx_revolver_cock" },
    { "time": 2.10, "type": "VFXSpawn", "effect": "VFX_MuzzleFlash_Revolver", "socket": "gun_barrel_socket" },
    { "time": 2.10, "type": "VFXSpawn", "effect": "VFX_Blood_ExitWound_Heavy", "socket": "victim_head_back_socket" },
    { "time": 2.10, "type": "CameraShake", "intensity": 0.7, "duration": 0.35 },
    { "time": 2.10, "type": "AudioSFX", "cue": "sfx_gunshot_heavy_revolver" },
    { "time": 2.15, "type": "SpawnDecal", "decal": "Decal_BloodSplatter_Floor", "attach_to_ground": true },
    { "time": 2.80, "type": "EnableRagdoll", "target": "Victim", "impulse": [0, -120, 40] },
    { "time": 4.20, "type": "DetachPropToHolster", "prop": "Revolver", "socket": "thigh_r_holster_socket" },
    { "time": 4.50, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
