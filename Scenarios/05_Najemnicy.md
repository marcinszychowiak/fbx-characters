# Scenariusz Cutscenki: Najemnicy

## 1. Informacje Ogólne
- **Frakcja:** Najemnicy (Wojacy / Siły Specjalne)
- **ID Scenariusza:** `CS_TAKEDOWN_05_MERCENARIES`
- **Typ Animacji:** Taktyczne poderżnięcie gardła od tyłu / Tactical Throat Slit
- **Czas trwania:** 4.4 sekundy (132 klatki przy 30 fps / 264 klatki przy 60 fps)
- **Plik referencyjny:** `Cutscenes/najemnicy .mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Soldier_Male.fbx` (wariant opcjonalny: `FBX/Soldier_Female.fbx` lub `FBX/BlueSoldier_Male.fbx`)
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/Casual_Male.fbx` lub `FBX/BaseCharacter.fbx`)
- **Rekwizyty (Props):**
  - Wojskowy nóż bojowy / sztylet taktyczny typu Tanto lub Ka-Bar (Socket: `hand_r_socket`)
  - Pochwa na nóż na kamizelce taktycznej (Socket: `chest_knife_sheath_socket`)

### Dźwięki dialogowe (`BloodChess/Najemnicy/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `najemnicy_donosny_01_48k.wav` (Rekomendowany – chłodny, profesjonalny ton)
  - `najemnicy_donosny_02_48k.wav`
  - `najemnicy_donosny_03_48k.wav`
  - `najemnicy_donosny_04_48k.wav`
- **Offset odpalenia głosu:** `0.1s` lub w finale przy odepchnięciu ciała `2.9s`.

### Efekty dźwiękowe (SFX)
- `0.4s`: `sfx_combat_boots_stealth.wav` – stłumiony, sprężysty krok żołnierza.
- `0.9s`: `sfx_tactical_knife_unsheathe.wav` – ciche wyjęcie ostrza z pochewki z kompozytu kydex.
- `1.1s`: `sfx_grab_head_hair.wav` – agresywny chwyt dłoni w rękawicy taktycznej za głowę/włosy.
- `1.4s`: `sfx_knife_cut_throat_deep.wav` – głęboki, mokry dźwięk rozcinanej krtani i skóry.
- `1.5s - 2.8s`: `sfx_blood_spurting_gush.wav` – gwałtowny strumień krwi zalewający klatkę piersiową.
- `1.6s - 2.5s`: `sfx_victim_muted_gasp.wav` – zduszony, bezsilny charkot w płucach ofiary.
- `3.1s`: `sfx_body_shove_dirt.wav` – upadek odepchniętego ciała twarzą do ziemi.
- `3.8s`: `sfx_knife_cloth_wipe.wav` – dźwięk przetarcia zakrwawionej klingi o materiał munduru.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.8** | 0 - 24 | Agresor | Szybkie, ciche podejście z boku/od tyłu. Lewa ręka uniesiona do chwytu, prawa dłoń dobywa noża bojowego. | Beznamiętny profesjonalizm, precyzja komandosa. |
| **0.0 - 0.8** | 0 - 24 | Ofiara | Spogląda przed siebie, nieświadoma zagrożenia z martwego pola widzenia. | Rozluźniona postawa. |
| **0.9 - 1.3** | 27 - 39 | Agresor | Lewa ręka brutalnie chwyta czoło/włosy ofiary i odciąga jej głowę gwałtownie do tyłu, napinając szyję. | Całkowita dominacja fizyczna. |
| **0.9 - 1.3** | 27 - 39 | Ofiara | Szarpnięcie w tył, rozszerzone oczy, gardło odsłonięte. | Paraliżujący szok. |
| **1.4** | 42 | Agresor | **PODCIĘCIE (EXECUTION FRAME):** Płynne, bezlitosne przeciągnięcie ostrza od lewej do prawej krawędzi szyi. | Ostrze zagłębia się w tkankę na 2 cm. |
| **1.5 - 2.6** | 45 - 78 | Ofiara | Z rany na gardle wytryskuje łukiem strumień krwi. Dłonie ofiary w odruchu bezwarunkowym próbują zacisnąć ranę. | Agonia, krew cieknie między palcami na klatkę. |
| **2.0 - 2.8** | 60 - 84 | Agresor | Przytrzymuje ofiarę, kontrolując jej bezwład, po czym puszcza chwyt i odpycha ciało do przodu. | Chłodne, pragmatyczne wykonanie zadania. |
| **2.9 - 3.7** | 87 - 111| Ofiara | Ciało bez sił wali się na kolana, a następnie płasko na klatkę piersiową i twarz. | Zgon, ciało zastyga w bezruchu. |
| **3.2 - 4.4** | 96 - 132| Agresor | Jednym ruchem przeciera klingę o spodnie, chowa nóż i unosi karabin/pistolet, lustrując horyzont. | Gotowość do eliminacji kolejnego celu. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.0s (Infiltracja):**
  - **Typ:** Over-the-Shoulder (zza ramienia najemnika podchodzącego do celu).
  - **FOV:** 45 mm, ostrość ustawiona na kark ofiary.
- **1.1s – 2.2s (Egzekucja):**
  - **Typ:** Tight Side-Profile Close-Up skupiony na twarzy ofiary i dłoni zaciskającej nóż na szyi.
  - **Camera Shake:** Krótki, suchy wstrząs w klatce podcięcia `1.4s` (amplituda `0.45`, czas `0.25s`).
- **2.3s – 4.4s (Odejście):**
  - **Typ:** Frontalny Medium Shot prezentujący stojącego najemnika czyszczącego nóż, z leżącą u jego stóp ofiarą.

---

## 5. Efekty Wizualne (VFX)

- **Wytrysk z Gardła (`VFX_Throat_Cut_BloodJet`):**
  - Socket: `victim_throat_socket`.
  - Szeroki, horyzontalny wachlarz kropel krwi, po którym następuje ciągły strumień spływający kaskadą na klatkę piersiową i odzież.
- **Zbroczenie Tkaniny (`Dynamic_Material_BloodSoak`):**
  - Parametr cieniowania koszuli ofiary stopniowo barwi tkaninę na ciemnoczerwony, mokry kolor.
- **Ociekające Ostrze (`VFX_Dripping_Blade_Blood`):**
  - Drobne krople krwi spadające z czubka noża po wykonaniu cięcia.
- **Kałuża Przed Ciałem (`Decal_BloodPool_Forward`):**
  - Plama krwi formująca się w miejscu, gdzie po odepchnięciu spoczywa głowa ofiary.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_05_MERCENARIES",
  "duration": 4.4,
  "sync_mode": "PairedKinematicWithRagdollTransition",
  "events": [
    { "time": 0.10, "type": "AudioVoice", "cue": "BloodChess/Najemnicy/najemnicy_donosny_01_48k.wav" },
    { "time": 0.85, "type": "AudioSFX", "cue": "sfx_tactical_knife_unsheathe" },
    { "time": 1.10, "type": "AudioSFX", "cue": "sfx_grab_head_hair" },
    { "time": 1.40, "type": "AudioSFX", "cue": "sfx_knife_cut_throat_deep" },
    { "time": 1.40, "type": "VFXSpawn", "effect": "VFX_Throat_Cut_BloodJet", "socket": "victim_throat_socket" },
    { "time": 1.40, "type": "CameraShake", "intensity": 0.45, "duration": 0.25 },
    { "time": 1.50, "type": "AudioSFX", "cue": "sfx_blood_spurting_gush" },
    { "time": 1.60, "type": "AudioSFX", "cue": "sfx_victim_muted_gasp" },
    { "time": 2.80, "type": "EnableRagdoll", "target": "Victim", "impulse": [80, 0, -50] },
    { "time": 3.10, "type": "AudioSFX", "cue": "sfx_body_shove_dirt" },
    { "time": 3.20, "type": "SpawnDecal", "decal": "Decal_BloodPool_Forward", "attach_to_ground": true },
    { "time": 3.80, "type": "AudioSFX", "cue": "sfx_knife_cloth_wipe" },
    { "time": 4.40, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
