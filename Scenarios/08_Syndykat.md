# Scenariusz Cutscenki: Syndykat

## 1. Informacje Ogólne
- **Frakcja:** Syndykat (Mafia / Zorganizowana Przestępczość)
- **ID Scenariusza:** `CS_TAKEDOWN_08_SYNDICATE`
- **Typ Animacji:** Egzekucja mafijna sztyletem / Mob Hitman Chest Stab
- **Czas trwania:** 4.5 sekundy (135 klatek przy 30 fps / 270 klatek przy 60 fps)
- **Plik referencyjny:** `Cutscenes/syndykat .mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Suit_Male.fbx` (wariant opcjonalny: `FBX/Suit_Female.fbx` lub `FBX/OldClassy_Male.fbx`)
- **Ofiara:** `FBX/Casual_Male.fbx` (wariant opcjonalny: `FBX/Casual2_Male.fbx` lub `FBX/BaseCharacter.fbx`)
- **Rekwizyty (Props):**
  - Nóż sprężynowy / stiletto mafijne (Socket: `hand_r_socket` - chwyt odwrotny/reverse grip)
  - Okulary przeciwsłoneczne na twarzy agresora

### Dźwięki dialogowe (`BloodChess/Syndykat/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `suyndykat_smutek_01_48k.wav` (Rekomendowany – zimny, melancholijny ton egzekutora: „Nic osobistego, po prostu biznes”)
  - `suyndykat_smutek_02_48k.wav`
  - `suyndykat_smutek_03_48k.wav`
  - `suyndykat_smutek_04_48k.wav`
- **Offset odpalenia głosu:** `0.1s` (podczas wyciągania noża).

### Efekty dźwiękowe (SFX)
- `0.7s`: `sfx_stiletto_knife_deploy.wav` – ostry, sprężynowy klik otwieranego noża mafijnego.
- `1.8s`: `sfx_stab_pierce_chest_heavy.wav` – uderzenie pięści i chrzęst przebijanych żeber.
- `1.9s`: `sfx_blood_squirt_high.wav` – intensywny, ciśnieniowy trysk krwi.
- `2.0s`: `sfx_victim_gasp_shock.wav` – głęboki, zduszony oddech ofiary w szoku pourazowym.
- `2.7s`: `sfx_blade_pullout_flesh.wav` – mokry dźwięk wyszarpywanego ostrza z rany.
- `3.4s`: `sfx_body_thud_ground.wav` – głuchy odgłos osuwającego się na plecy ciała.
- `4.0s`: `sfx_sunglasses_adjust.wav` – subtelny odgłos poprawiania garnituru/okularów.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.6** | 0 - 18 | Agresor | Stoi wyprostowany w garniturze naprzeciwko dłużnika/celu. Prawa dłoń z tyłu za paskiem. | Beznamiętny, lodowaty spokój. |
| **0.0 - 0.6** | 0 - 18 | Ofiara | Zbliża się lub patrzy pytająco, myśląc, że to zwykła rozmowa. | Nieświadomość wyroku. |
| **0.7 - 1.2** | 21 - 36 | Agresor | Płynnym ruchem wyjmuje nóż zza pleców, trzymając go chwytem odwrotnym (ostrze skierowane w dół). | Precyzyjny chwyt likwidatora. |
| **1.3 - 1.7** | 39 - 51 | Agresor | Uniesienie ramienia w górę do zamachu i krok w przód, skracając dystans do zera. | Spięcie mięśni ramienia. |
| **1.8** | 54 | Agresor | **CIOS (STRIKE FRAME):** Potężne pchnięcie stiletto prosto w klatkę piersiową/serce ofiary. | Wbicie ostrza aż po nasadę rękojeści. |
| **1.9 - 2.6** | 57 - 78 | Ofiara | Oczy ofiary otwierają się szeroko ze zgrozy. Ciało sztywnieje w spazmie bólu. | Krew obficie wsiąka w jasną koszulę. |
| **2.7 - 3.2** | 81 - 96 | Agresor | Bezwzględne wyszarpnięcie noża z piersi w bok, powiększając ranę. | Spojrzenie prosto w gasnące oczy ofiary. |
| **2.8 - 3.6** | 84 - 108| Ofiara | Ugięcie kolan, bezwładny opad w tył na plecy, ręce bezradnie rozpostarte na ziemi. | Zgon, wzrok skierowany w sufit. |
| **3.7 - 4.5** | 111 - 135| Agresor | Mafiozo strzepuje krople krwi z noża, poprawia dwoma palcami okulary na nosie i odwraca się plecami. | Wykonanie zlecenia bez zbędnych emocji. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.2s (Wprowadzenie):**
  - **Typ:** Medium Two-Shot z boku pod kątem 30 stopni, z wyraźnym planem garnituru i dłoni sięgającej po broń za plecami.
  - **FOV:** 45 mm.
- **1.3s – 2.5s (Pchnięcie):**
  - **Typ:** Dynamiczne zbliżenie (Chest Close-Up) na klatkę piersiową i wbijające się ostrze.
  - **Camera Shake:** Ostre, krótkie tąpnięcie w momencie uderzenia w klatkę w `1.8s` (amplituda `0.6`, czas `0.2s`).
- **2.6s – 4.5s (Zimna krew):**
  - **Typ:** Low-Angle Shot skupiający się na twarzy mafioza poprawiającego okulary przeciwsłoneczne, z bezwładnym ciałem ofiary na dolnym planie.

---

## 5. Efekty Wizualne (VFX)

- **Masywny Rozbryzg z Klatki (`VFX_Chest_Blood_Burst`):**
  - Socket: `victim_chest_stab_socket`.
  - Szeroki stożek czerwonych cząstek krwi wystrzeliwujący na boki i do tyłu ofiary w klatce `1.8s`.
- **Plama Krwi na Odzieży (`Dynamic_Decal_ChestSoak`):**
  - Błyskawicznie powiększająca się ciemnoczerwona plama na białym t-shircie ofiary, wsiąkająca w materiał od `1.9s` do `4.0s`.
- **Krople Opadające (`VFX_Blood_Drips_Floor`):**
  - Seria kropel krwi spadających z końcówki wyszarpniętego noża na pole szachowe.
- **Czysta Kałuża Mafijna (`Decal_Syndicate_BloodPuddle`):**
  - Lśniąca kałuża krwi zbierająca się pod korpusem leżącego dłużnika.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_08_SYNDICATE",
  "duration": 4.5,
  "sync_mode": "PairedKinematicWithRagdollBlend",
  "events": [
    { "time": 0.10, "type": "AudioVoice", "cue": "BloodChess/Syndykat/suyndykat_smutek_01_48k.wav" },
    { "time": 0.70, "type": "AudioSFX", "cue": "sfx_stiletto_knife_deploy" },
    { "time": 0.75, "type": "AttachProp", "prop": "Stiletto_Knife", "socket": "hand_r_socket" },
    { "time": 1.80, "type": "AudioSFX", "cue": "sfx_stab_pierce_chest_heavy" },
    { "time": 1.80, "type": "VFXSpawn", "effect": "VFX_Chest_Blood_Burst", "socket": "victim_chest_socket" },
    { "time": 1.80, "type": "CameraShake", "intensity": 0.6, "duration": 0.2 },
    { "time": 1.85, "type": "SpawnDecalOnMesh", "target": "Victim", "decal": "Dynamic_Decal_ChestSoak" },
    { "time": 1.90, "type": "AudioSFX", "cue": "sfx_blood_squirt_high" },
    { "time": 2.00, "type": "AudioSFX", "cue": "sfx_victim_gasp_shock" },
    { "time": 2.70, "type": "AudioSFX", "cue": "sfx_blade_pullout_flesh" },
    { "time": 2.80, "type": "EnableRagdoll", "target": "Victim", "impulse": [0, -70, -40] },
    { "time": 3.00, "type": "SpawnDecal", "decal": "Decal_Syndicate_BloodPuddle", "attach_to_ground": true },
    { "time": 3.40, "type": "AudioSFX", "cue": "sfx_body_thud_ground" },
    { "time": 4.00, "type": "AudioSFX", "cue": "sfx_sunglasses_adjust" },
    { "time": 4.50, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
