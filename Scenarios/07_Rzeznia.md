# Scenariusz Cutscenki: Rzeźnia

## 1. Informacje Ogólne
- **Frakcja:** Rzeźnia (Szaleni Rzeźnicy / Kanibalistyczni Kucharze)
- **ID Scenariusza:** `CS_TAKEDOWN_07_SLAUGHTERHOUSE`
- **Typ Animacji:** Rozpuszczenie kwasem przemysłowym / Acid Face Melt
- **Czas trwania:** 4.9 sekundy (147 klatek przy 30 fps / 294 klatki przy 60 fps)
- **Plik referencyjny:** `Cutscenes/rzeźnia .mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Chef_Male.fbx` (wariant opcjonalny: `FBX/Chef_Female.fbx` lub `FBX/Worker_Male.fbx`)
  - Akcesoria: `FBX/Chef_Hat.fbx`
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/Casual_Male.fbx` lub `FBX/BaseCharacter.fbx`)
- **Rekwizyty (Props):**
  - Chemiczna butla / flakon z kwasem siarkowym/żrącym (Socket: `hand_r_socket`)
  - Opcjonalnie tasak rzeźnicki u pasa (Socket: `hip_l_socket`)

### Dźwięki dialogowe (`BloodChess/Rzeznia/`)
- **Plik w silniku (Audio Cue - Voice):**
  - `rzeznia_szalony_06_48k.wav` (Psychopatyczny, niekontrolowany śmiech i mamrotanie rzeźnika)
- **Offset odpalenia głosu:** `0.2s` (chichot przy podejściu) oraz `2.5s` (kulminacja histerycznego rechotu).

### Efekty dźwiękowe (SFX)
- `0.6s`: `sfx_glass_cork_open.wav` – odgłos otwarcia korka / odkorkowania butelki z chemikaliami.
- `0.9s`: `sfx_acid_pour_stream.wav` – strumień cieczy wylewanej na głowę.
- `1.2s - 4.5s`: `sfx_acid_sizzle_flesh_burn.wav` – głośne, agresywne syczenie, skwierczenie i bulgotanie topionego ciała.
- `1.3s - 3.2s`: `sfx_victim_bloodcurdling_scream.wav` – rozdzierający krzyk niewyobrażalnego bólu.
- `3.4s`: `sfx_flesh_sludge_collapse.wav` – rozpad tkanek i plaśnięcie rozmiękłego ciała o ziemię.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.7** | 0 - 21 | Agresor | Rzeźnik podchodzi z kołyszącym się, ociężałym krokiem, trzymając w uniesionej prawej dłoni dymiącą butelkę z kwasem. | Psychopatyczny tik na twarzy, rozszerzone źrenice. |
| **0.0 - 0.7** | 0 - 21 | Ofiara | Zdezorientowana, unosi dłonie w geście próby pertraktacji. | Strach, niepewność. |
| **0.8 - 1.4** | 24 - 42 | Agresor | Rzeźnik wyciąga rękę nad głowę ofiary i zdecydowanym ruchem przechyla butelkę, wylewając żrącą substancję prosto na jej ciemienie i twarz. | Szeroki, maniakalny uśmiech. |
| **1.1 - 2.8** | 33 - 84 | Ofiara | Kwas spływa po czole, oczach i ustach. Ofiara chwyta się oburącz za twarz, szarpiąc skórę palcami w ataku nieopisanego bólu. | Wrzask w agonii, dym bucha spod palców. |
| **1.5 - 3.5** | 45 - 105| Obaj | **REAKCJA CHEMICZNA:** Twarz ofiary zaczyna się topić, traci geometrię i zapada się w bezkształtną masę. Rzeźnik przechyla głowę i rechocze. | Kwas wypala dziury w ciele i odzieży. |
| **2.9 - 3.8** | 87 - 114| Ofiara | Nogi odmawiają posłuszeństwa, ciało opada na kolana, a następnie zwija się w parującej kałuży na szachownicy. | Agonalne drgawki ustające w `3.8s`. |
| **3.8 - 4.9** | 114 - 147| Agresor | Rzeźnik potrząsa pustą butelką, uderza się z zadowolenia w brzuch i wykonuje groteskowy ukłon ku publiczności/przeciwnikowi. | Dumne zadowolenie ze „świeżej porcji”. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.0s (Podanie trucizny):**
  - **Typ:** Medium Close-Up z boku, skupiony na przechylającej się butelce i spadającej stężonej stróżce cieczy.
  - **FOV:** 50 mm.
- **1.1s – 2.8s (Męka i rozpuszczanie):**
  - **Typ:** Frontalny ekstremalny Close-Up (Macro Shot) na twarz ofiary spowitą w gęstym, żółtawo-zielonym dymie i pęcherzach kwasu.
  - **Camera Shake:** Drżenie o wysokiej częstotliwości (amplituda `0.3`, `24 Hz`) potęgujące wrażenie chemicznego wrzenia i agonii.
- **2.9s – 4.9s (Finał w oparach):**
  - **Typ:** Płynne oddalenie (Pull-Back Shot) do szerokiego kadru, ukazującego rzeźnika stojącego obok parujących resztek wroga.

---

## 5. Efekty Wizualne (VFX)

- **Strumień Kwasu (`VFX_Acid_Pour_Stream`):**
  - Socket: `acid_bottle_mouth_socket`.
  - Płynąca, lekko świecąca na żółto-zielono lepkawa ciecz o właściwościach cieczy newtonowskiej.
- **Wrzenie i Pienienie Tkanek (`VFX_Acid_Flesh_Foam`):**
  - Gęste skupiska pękających pęcherzy chemicznych generowane na siatce twarzy i klatki piersiowej ofiary.
- **Toksyczne Opary (`VFX_Chemical_Yellow_Smoke`):**
  - Kłęby żółto-zielonkawego, gryzącego dymu unoszące się pionowo z głowy ofiary przez cały czas trwania egzekucji.
- **Morfing i Dissolve Siatki (`M_Acid_Melt_VertexDisplacement`):**
  - Zastosowanie dynamicznego vertex displacement i dissolve w shaderze głowy: geometria twarzy zapada się do wewnątrz i upłynnia.
- **Żrąca Kałuża (`Decal_Acid_Puddle_Corrosive`):**
  - Zielonawo-żółta, dymiąca plama kwasu na szachownicy, która wypala teksturę podłoża i pozostawia wżery.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_07_SLAUGHTERHOUSE",
  "duration": 4.9,
  "sync_mode": "PairedKinematicWithVertexDeform",
  "events": [
    { "time": 0.20, "type": "AudioVoice", "cue": "BloodChess/Rzeznia/rzeznia_szalony_06_48k.wav" },
    { "time": 0.60, "type": "AudioSFX", "cue": "sfx_glass_cork_open" },
    { "time": 0.90, "type": "AudioSFX", "cue": "sfx_acid_pour_stream" },
    { "time": 0.90, "type": "VFXSpawn", "effect": "VFX_Acid_Pour_Stream", "socket": "acid_bottle_mouth_socket" },
    { "time": 1.10, "type": "AudioSFX", "cue": "sfx_acid_sizzle_flesh_burn" },
    { "time": 1.10, "type": "VFXSpawn", "effect": "VFX_Acid_Flesh_Foam", "socket": "victim_head_socket" },
    { "time": 1.15, "type": "VFXSpawn", "effect": "VFX_Chemical_Yellow_Smoke", "socket": "victim_head_socket" },
    { "time": 1.30, "type": "AudioSFX", "cue": "sfx_victim_bloodcurdling_scream" },
    { "time": 1.50, "type": "StartShaderEffect", "target": "VictimHead", "effect": "M_Acid_Melt_VertexDisplacement" },
    { "time": 1.50, "type": "CameraShakeContinuous", "intensity": 0.3, "duration": 1.8 },
    { "time": 2.80, "type": "SpawnDecal", "decal": "Decal_Acid_Puddle_Corrosive", "attach_to_ground": true },
    { "time": 3.40, "type": "AudioSFX", "cue": "sfx_flesh_sludge_collapse" },
    { "time": 3.50, "type": "EnableRagdoll", "target": "Victim", "impulse": [0, -30, -30] },
    { "time": 4.90, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
