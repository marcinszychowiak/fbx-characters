# Scenariusz Cutscenki: Wikingowie z Krwawego Fiordu

## 1. Informacje Ogólne
- **Frakcja:** Wikingowie z Krwawego Fiordu (Berserkerzy / Wojownicy Północy)
- **ID Scenariusza:** `CS_TAKEDOWN_09_VIKINGS`
- **Typ Animacji:** Wbicie topora bojowego w klatkę piersiową / Battleaxe Cleave & Embed
- **Czas trwania:** 4.6 sekundy (138 klatek przy 30 fps / 276 klatek przy 60 fps)
- **Plik referencyjny:** `Cutscenes/wikingowie .mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Viking_Male.fbx` (wariant opcjonalny: `FBX/Viking_Female.fbx`)
  - Akcesoria: `FBX/VikingHelmet.fbx` (hełm rogaty/normański)
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/BaseCharacter.fbx` lub `FBX/Casual_Male.fbx`)
- **Rekwizyty (Props):**
  - Ciężki topór bojowy wikingów (Danish Two-Handed Axe / Bearded Axe) (Socket: `hand_r_socket` / `hand_l_socket` - chwyt oburącz)

### Dźwięki dialogowe (`BloodChess/Wikingowie z krwawego fiordu/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `wojownik_w_wirze_bitwy_wkurzony_01_48k.wav` (Rekomendowany – dziki berserkerski ryk)
  - `wojownik_w_wirze_bitwy_wkurzony_02_48k.wav`
  - `wojownik_pion_wkurzony_03_48k.wav`
  - `wojownik_pion_ekscytacja_04_48k.wav`
  - `wojownik_pion_szept_05_48k.wav`
- **Offset odpalenia głosu:** `0.0s` (okrzyk wojenny na wejściu) oraz `3.5s` (potężny ryk triumfu ku bogom Valhalli).

### Efekty dźwiękowe (SFX)
- `0.6s`: `sfx_axe_swing_heavy_whoosh.wav` – świst potężnego, ciężkiego ostrza tnącego powietrze.
- `1.2s`: `sfx_axe_flesh_bone_crush.wav` – ogłuszające trzaśnięcie łamanego mostka i żeber.
- `1.3s`: `sfx_blood_explosion_gush.wav` – gwałtowny wybuch krwi i wnętrzności.
- `1.4s - 2.5s`: `sfx_victim_bone_crunch_gasp.wav` – agonalny skurcz płuc ofiary przebitych ostrzem.
- `2.5s`: `sfx_axe_rip_out.wav` – dźwięk wyrywania zaklinowanego topora z klatki piersiowej.
- `3.1s`: `sfx_heavy_body_slam_ground.wav` – ciężkie uderzenie bezwładnego ciała o ziemię.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.7** | 0 - 21 | Agresor | Zbliża się ciężkim krokiem, topór trzymany oburącz w prawej/dolnej pozycji. | Oczy pełne żądzy krwi, żyły nabrzmiałe na szyi. |
| **0.0 - 0.7** | 0 - 21 | Ofiara | Sparaliżowana potęgą wroga, zastyga w bezruchu. | Beznadzieja, rezygnacja. |
| **0.8 - 1.1** | 24 - 33 | Agresor | Zamach z biodra i pchnięcie ostrzem topora prosto w przód jak taranem. | Pełna masa mięśniowa włożona w cios. |
| **1.2** | 36 | Obaj | **WBICIE TOPORA (CRUSH FRAME):** Ostrze topora wbija się prosto w mostek ofiary na głębokość 15 cm. | Złamanie kości klatki piersiowej. |
| **1.3 - 2.2** | 39 - 66 | Ofiara | Klatka piersiowa zapada się. Ofiara odgina się w łuk ku tyłowi, wisząc na wbitym ostrzu. | Masywny wytrysk krwi w górę i na boki. |
| **1.3 - 2.4** | 39 - 72 | Agresor | Trzyma trzonek wbitego topora, dociskając go z całej siły w głąb ciała ofiary. | Grymas szału bojowego. |
| **2.5 - 2.8** | 75 - 84 | Agresor | Zapiera się nogą o brzuch ofiary i z impetem wyszarpuje topór z rany. | Krew tryska wraz z wyszarpywanym ostrzem. |
| **2.9 - 3.5** | 87 - 105| Ofiara | Odgięte ciało traci oparcie i bezwładnie wali się plecami na szachownicę. | Śmierć na miejscu, wielka rana otwarta w klatce. |
| **3.5 - 4.6** | 105 - 138| Agresor | Wiking unosi zakrwawiony topór w jednej dłoni wysoko nad głowę, drugą pięścią bije się w pierś i ryczy ku niebiosom. | Zwycięski okrzyk Berserkera. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.0s (Nacierający kolos):**
  - **Typ:** Low-Angle Tilt-Up, ukazujący masywną sylwetkę wikinga i potężne ostrze topora.
  - **FOV:** 35 mm.
- **1.1s – 2.4s (Wbicie i impakt):**
  - **Typ:** Dynamiczne ujęcie z profilu 90 stopni, pokazujące głębokość wbicia ostrza w korpus ofiary.
  - **Camera Shake:** Potężne, ciężkie tąpnięcie w `1.2s` (amplituda `0.85`, czas trwania `0.4s`) symulujące siłę uderzenia topora.
- **2.5s – 4.6s (Valhalla):**
  - **Typ:** Szeroki kąt z dołu, rotujący wokół wzniesionego ku niebu topora ociekającego krwią.

---

## 5. Efekty Wizualne (VFX)

- **Masywny Gejzer Krwi (`VFX_Heavy_Cleave_BloodExplosion`):**
  - Socket: `victim_sternum_socket`.
  - Szeroka, objętościowa eksplozja czerwonych cząstek krwi rozchodząca się na boki i w górę na wysokość 1.5 metra.
- **Odłamki Kości i Mięsa (`VFX_Bone_Splinters_Gibs`):**
  - Fragmenty roztrzaskanych żeber i skrzepów wyrzucone w momencie impaktu.
- **Rozbryzg na Rękojeści (`Dynamic_Blood_Axe_Coating`):**
  - Ostrze i trzonek topora pokrywają się grubą warstwą lśniącej krwi w klatce `1.2s`.
- **Zbroczone Podłoże (`Decal_Viking_Carnage_Pool`):**
  - Ciężki, gęsty rozbryzg krwi na pole szachownicy wokół leżącej ofiary.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_09_VIKINGS",
  "duration": 4.6,
  "sync_mode": "PairedKinematicWithWeaponLock",
  "events": [
    { "time": 0.05, "type": "AudioVoice", "cue": "BloodChess/Wikingowie z krwawego fiordu/wojownik_w_wirze_bitwy_wkurzony_01_48k.wav" },
    { "time": 0.80, "type": "AudioSFX", "cue": "sfx_axe_swing_heavy_whoosh" },
    { "time": 1.20, "type": "AudioSFX", "cue": "sfx_axe_flesh_bone_crush" },
    { "time": 1.20, "type": "VFXSpawn", "effect": "VFX_Heavy_Cleave_BloodExplosion", "socket": "victim_sternum_socket" },
    { "time": 1.20, "type": "VFXSpawn", "effect": "VFX_Bone_Splinters_Gibs", "socket": "victim_sternum_socket" },
    { "time": 1.20, "type": "CameraShake", "intensity": 0.85, "duration": 0.4 },
    { "time": 1.30, "type": "AudioSFX", "cue": "sfx_blood_explosion_gush" },
    { "time": 1.40, "type": "AudioSFX", "cue": "sfx_victim_bone_crunch_gasp" },
    { "time": 2.50, "type": "AudioSFX", "cue": "sfx_axe_rip_out" },
    { "time": 2.80, "type": "EnableRagdoll", "target": "Victim", "impulse": [0, -90, -40] },
    { "time": 2.90, "type": "SpawnDecal", "decal": "Decal_Viking_Carnage_Pool", "attach_to_ground": true },
    { "time": 3.10, "type": "AudioSFX", "cue": "sfx_heavy_body_slam_ground" },
    { "time": 3.50, "type": "AudioVoice", "cue": "BloodChess/Wikingowie z krwawego fiordu/wojownik_pion_ekscytacja_04_48k.wav" },
    { "time": 4.60, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
