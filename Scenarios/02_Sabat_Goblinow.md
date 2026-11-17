# Scenariusz Cutscenki: Sabat Goblinów

## 1. Informacje Ogólne
- **Frakcja:** Sabat Goblinów
- **ID Scenariusza:** `CS_TAKEDOWN_02_GOBLINS`
- **Typ Animacji:** Podpalenie cieczą łatwopalną / Incendiary Execution
- **Czas trwania:** 4.8 sekundy (144 klatki przy 30 fps / 288 klatek przy 60 fps)
- **Plik referencyjny:** `Cutscenes/gobliny .mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Goblin_Male.fbx` (wariant opcjonalny: `FBX/Goblin_Female.fbx` lub `FBX/Witch.fbx`)
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/Casual_Male.fbx` lub `FBX/BaseCharacter.fbx`)
- **Rekwizyty (Props):**
  - Wiadro z łatwopalną naftą/kwasem (Socket: `hand_r_socket` / `hand_l_socket` - chwyt oburącz)
  - Średniowieczna zapalniczka krzesiwowa lub pochodnia/zapałka (Socket: `hand_r_socket`)

### Dźwięki dialogowe (`BloodChess/Sabat Goblinów/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `Goblin.wav` (Rekomendowany – złośliwy chichot)
  - `Goblin2.wav`
  - `Goblin3.wav`
  - `Goblin4.wav`
- **Offset odpalenia głosu:** `0.1s` (chichot goblina na wejściu) oraz opcjonalnie `2.3s` (histeryczny śmiech podczas zapłonu).

### Efekty dźwiękowe (SFX)
- `0.6s`: `sfx_liquid_bucket_splash.wav` – głośny chlust cieczy rozlewającej się po ciele i ubraniu.
- `1.8s`: `sfx_lighter_flick_spark.wav` – metaliczny dźwięk krzesiwa / pstryknięcia zapalniczki.
- `2.1s`: `sfx_fire_whoosh_ignite.wav` – gwałtowny świst wybuchu płomieni (whoosh).
- `2.2s - 4.5s`: `sfx_fire_burning_loop.wav` – trzaskający ogień i skwierczenie spalanego ciała.
- `2.3s - 3.8s`: `sfx_victim_scream_burning.wav` – wrzask przerażenia i agonii ofiary.
- `4.0s`: `sfx_charred_bodyfall.wav` – głuchy łomot upadającego zwęglonego ciała na pole szachownicy.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.5** | 0 - 15 | Agresor | Goblin podbiega zgarbiony z ciężkim wiadrem trzymanym oburącz. | Szczerzy kły, nerwowe tiki głowy. |
| **0.5 - 1.2** | 15 - 36 | Agresor | Energiczny zamach wiadrem: wylanie gęstej, ciemnożółtej cieczy prosto w twarz i na klatkę piersiową ofiary. | Płyn rozbryzguje się wokół. Wiadro odrzucone na bok. |
| **0.7 - 1.5** | 21 - 45 | Ofiara | Zaskoczenie i odruch zasłaniania oczu dłońmi. Ciecz oblepia tułów i głowę. | Szok, dławienie się oparami. |
| **1.5 - 2.0** | 45 - 60 | Agresor | Goblin cofa się o krok, zza pazuchy wyjmuje zapalniczkę/krzesiwo, unosi rękę i patrzy na ofiarę. | Szaleńczy, sadystyczny uśmiech. |
| **2.1** | 63 | Agresor | **ZAPŁON (IGNITION FRAME):** Goblin krzesze iskrę. Rzuca iskrę/zapałkę w stronę nasączonej ofiary. | Błysk iskry i natychmiastowa eksplozja ognia. |
| **2.1 - 3.5** | 63 - 105| Ofiara | Całe ciało natychmiast staje w słupie płomieni. Ofiara miota się w panice, machając rękami. | Niekontrolowane ruchy, agonia. |
| **3.5 - 4.2** | 105 - 126| Ofiara | Nogi odmawiają posłuszeństwa. Ciało czernieje (przejście materiału do spalonego węgla), upadek na kolana i twarz. | Gęsty czarny dym zasłania sylwetkę. |
| **3.8 - 4.8** | 114 - 144| Agresor | Goblin podskakuje w miejscu, klaszcze w dłonie i tańczy z radości wokół dogasającego truchła. | Histeryczna, chaotyczna animacja tańca. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.8s (Wylanie cieczy):**
  - **Typ:** Frontalny Medium Shot z poziomu torsu (niski kąt, uwypuklający mały wzrost goblina).
  - **FOV:** 40 mm. Płynny ruch kamery śledzący strumień cieczy z wiadra na ofiarę.
- **1.9s – 2.5s (Zapłon):**
  - **Typ:** Zbliżenie na profil twarzy goblina i rękę krzeszącą iskrę, po czym szybki snap-zoom na ofiarę w chwili zapłonu (`2.1s`).
  - **Camera Shake:** Średni wstrząs w chwili wybuchu płomienia (amplituda `0.5`, czas `0.4s`).
- **2.6s – 4.8s (Pożar i taniec):**
  - **Typ:** Orbit Camera (obrót o 45 stopni wokół płonącej sceny) pokazujący na pierwszym planie tańczącego goblina, a w tle dymiące szczątki ofiary.

---

## 5. Efekty Wizualne (VFX)

- **Chlust Płynu (`VFX_Liquid_Splash_Fuel`):**
  - Emiter z krawędzi wiadra: gęsty strumień lepkiej cieczy uderzający w korpus ofiary i spływający po siatce modelu.
- **Eksplozja Płomienia (`VFX_Fire_Burst_Ignite`):**
  - Rozbłysk sferyczny w punkcie kontaktu iskry (`2.1s`), po którym natychmiast aktywuje się emiter płomieni na kościach ofiary (`Pelvis`, `Spine`, `Head`, `Hands`).
- **Płomienie Ciągłe i Dym (`VFX_Body_Flames_Dense` & `VFX_Black_Smoke_Column`):**
  - Ogień wolumetryczny otaczający sylwetkę ofiary.
  - Gęsty, smolisty, czarny dym unoszący się w pionowym słupie.
- **Dynamiczny Shader Zwęglenia (`M_Charred_Burn_Dissolve`):**
  - Parametr `BurnProgress` materiału ofiary rośnie liniowo od `0.0` (w `2.2s`) do `1.0` (w `4.2s`).
  - Tekstura zmienia się z normalnej na czarną, spękaną, z żarzącymi się na czerwono krawędziami.
- **Wypalona Szachownica (`Decal_Scorched_Earth`):**
  - Czarna, zwęglona plama sadzy wypalona na powierzchni pola szachowego pod ofiarą.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_02_GOBLINS",
  "duration": 4.8,
  "sync_mode": "PairedKinematicWithMaterialLerp",
  "events": [
    { "time": 0.10, "type": "AudioVoice", "cue": "BloodChess/Sabat Goblinów/Goblin.wav" },
    { "time": 0.60, "type": "AudioSFX", "cue": "sfx_liquid_bucket_splash" },
    { "time": 0.65, "type": "VFXSpawn", "effect": "VFX_Liquid_Splash_Fuel", "socket": "bucket_rim_socket" },
    { "time": 1.20, "type": "DropProp", "prop": "Bucket", "physics_enabled": true },
    { "time": 1.80, "type": "AudioSFX", "cue": "sfx_lighter_flick_spark" },
    { "time": 2.10, "type": "AudioSFX", "cue": "sfx_fire_whoosh_ignite" },
    { "time": 2.10, "type": "VFXSpawn", "effect": "VFX_Fire_Burst_Ignite", "socket": "victim_chest_socket" },
    { "time": 2.10, "type": "AttachEmitterToSkeleton", "effect": "VFX_Body_Flames_Dense", "target": "Victim" },
    { "time": 2.10, "type": "CameraShake", "intensity": 0.5, "duration": 0.4 },
    { "time": 2.20, "type": "StartMaterialLerp", "target": "Victim", "property": "BurnProgress", "duration": 2.0 },
    { "time": 2.30, "type": "AudioSFX", "cue": "sfx_victim_scream_burning" },
    { "time": 3.50, "type": "SpawnDecal", "decal": "Decal_Scorched_Earth", "attach_to_ground": true },
    { "time": 4.00, "type": "AudioSFX", "cue": "sfx_charred_bodyfall" },
    { "time": 4.80, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
