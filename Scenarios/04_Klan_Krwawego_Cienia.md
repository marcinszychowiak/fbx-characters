# Scenariusz Cutscenki: Klan Krwawego Cienia

## 1. Informacje Ogólne
- **Frakcja:** Klan Krwawego Cienia (Ninja / Asasyni Shinobi)
- **ID Scenariusza:** `CS_TAKEDOWN_04_BLOOD_SHADOW`
- **Typ Animacji:** Precyzyjna dekapitacja kataną / Decapitation Strike
- **Czas trwania:** 4.6 sekundy (138 klatek przy 30 fps / 276 klatek przy 60 fps)
- **Plik referencyjny:** `Cutscenes/klan Krwawego Cienia .mp4`

---

## 2. Wymagane Zasoby (Assets)

### Modele 3D (`FBX/`)
- **Agresor (Główny):** `FBX/Ninja_Male.fbx` (wariant opcjonalny: `FBX/Ninja_Female.fbx`, `FBX/Ninja_Sand.fbx` lub `FBX/Kimono_Male.fbx`)
  - Akcesoria: `FBX/Ninja_Male_Hair.fbx`
- **Ofiara:** Dowolny pion przeciwnika (w referencji: `FBX/Casual_Male.fbx` lub `FBX/BaseCharacter.fbx`)
  - Wymóg techniczny: model ofiary musi posiadać odłączalną głowę (`SeparableMesh_Head` lub maskowanie kości `neck_01`).
- **Rekwizyty (Props):**
  - Katana (Socket: `hand_r_socket`)
  - Pochwa Saya (Socket: `hip_l_socket`)

### Dźwięki dialogowe (`BloodChess/Klan Krwawego Cienia/`)
- **Pliki do wyboru w silniku (Audio Cue - Voice):**
  - `klan_krwawego_cienia_ekscytacja_01_48k.wav` (Rekomendowany)
  - `klan_krwawego_cienia_ekscytacja_02_48k.wav`
  - `klan_krwawego_cienia_ekscytacja_03_48k.wav`
  - `Klan_48k.wav`
- **Offset odpalenia głosu:** `0.1s` (szept z cienia przed atakiem).

### Efekty dźwiękowe (SFX)
- `0.6s`: `sfx_blade_draw_sheath.wav` – metaliczny, ostry świst wysuwanego ostrza z pochwy saya.
- `1.2s`: `sfx_sword_whoosh_fast.wav` – ultraszybki świst cięcia powietrza kataną.
- `1.3s`: `sfx_clean_slice_decapitation.wav` – chrupnięcie przecinanych kręgów szyjnych i cięcie tkanek.
- `1.4s`: `sfx_arterial_spray_high_pressure.wav` – wysoki, syczący dźwięk krwi tryskającej pod ogromnym ciśnieniem.
- `2.2s`: `sfx_head_bounce_ground.wav` – głuchy odgłos uderzenia i toczenia się odciętej głowy po podłożu.
- `3.0s`: `sfx_body_drop_heavy.wav` – upadek bezgłowego tułowia.
- `3.9s`: `sfx_sword_resheath_click.wav` – charakterystyczny klik (tsuba) ostrza wracającego do pochwy.

---

## 3. Oś Czasu i Choreografia (Timeline)

| Czas (s) | Klatka (30fps) | Rola | Działanie postaci | Emocje / Detale |
| :--- | :--- | :--- | :--- | :--- |
| **0.0 - 0.5** | 0 - 15 | Agresor | Niskie zejście na nogach (pozycja iaijutsu). Lewa dłoń na pochwie, prawa dłoń spoczywa na rękojeści (tsuka). | Pełne skupienie, nieruchome ciało, śmiertelna precyzja. |
| **0.0 - 0.5** | 0 - 15 | Ofiara | Zaskoczona obecnością wroga, nie zdążyła nawet podnieść rąk do obrony. | Bezradność, szok. |
| **0.6 - 1.2** | 18 - 36 | Agresor | Błyskawiczny krok w przód (dash) połączony z obrotowym cięciem kataną na wysokości gardła. | Smuga światła ciągnąca się za ostrzem (Weapon Trail). |
| **1.3** | 39 | Obaj | **CIĘCIE (SLICING FRAME):** Ostrze przechodzi poziomo przez szyję ofiary. | Błysk cięcia (Slash Arc). |
| **1.4 - 2.2** | 42 - 66 | Ofiara | **DEKAPITACJA:** Siatka głowy odłącza się od szyi, wiruje w powietrzu w stronę kamery i upada na ziemię. | Z kikuta szyi wystrzeliwuje fontanna krwi na wysokość 2 metrów. |
| **1.4 - 2.8** | 42 - 84 | Agresor | Płynne dokończenie obrotu, przejście za plecy ofiary i zatrzymanie się w postawie z kataną skierowaną w dół. | Ostrze ocieka krwią. |
| **2.3 - 3.2** | 69 - 96 | Ofiara | Bezgłowy tułów chwieje się przez ułamek sekundy, po czym kolana uginają się i ciało wali się do przodu. | Fontanna krwi słabnie, tworząc ogromną kałużę. |
| **3.3 - 4.6** | 99 - 138| Agresor | Ruch strzepnięcia krwi (chiburi) jednym energicznym machnięciem, po czym powolne schowanie katany do pochwy (noto) zakończone klikiem. | Zimna dyscyplina asasyna. |

---

## 4. Praca Kamery (Cinematics)

- **0.0s – 1.0s (Napięcie):**
  - **Typ:** Side-View Profile Medium Shot. Widać niską sylwetkę ninja i stojącą ofiarę.
  - **FOV:** 50 mm.
- **1.1s – 2.0s (Cięcie i dekapitacja):**
  - **Typ:** Dynamiczne zwolnienie tempa (Slow-Motion 50% w klatkach 38-50), najazd kamery z poziomu torsu.
  - **Kamera śledząca:** Kamera lekko śledzi trajektorię odciętej głowy wirującej w powietrzu.
  - **Camera Shake:** Ostre, punktowe szarpnięcie kamery w klatce `1.3s` (amplituda `0.8`, czas `0.2s`).
- **2.1s – 4.6s (Chiburi i finał):**
  - **Typ:** Low-Angle Shot zza pleców schodzącego z pola walki Ninja, z widokiem na leżące w tle bezgłowe ciało i toczącą się głowę.

---

## 5. Efekty Wizualne (VFX)

- **Smuga Ostrza (`VFX_Katana_Slash_Trail`):**
  - Czysta, półprzezroczysta, srebrzysto-czerwona wstęga wygenerowana przez krawędź tnącą ostrza podczas zamachu.
- **Wystrzał Tętniczy Dekapitacji (`VFX_Decapitation_Geyser`):**
  - Socket: `victim_neck_severed_socket`.
  - Potężny pionowy gejzer krwi wyrzucany na wysokość 1.8 - 2.2 metra, rozpraszający się u góry w gęsty deszcz kropel.
- **Fizyka Odciętej Głowy (`Head_Dismemberment_Physics`):**
  - W klatce `1.3s` głowa zamienia się w niezależny obiekt fizyczny z nadanym wektorem rotacji `(Yaw: 720 deg/s)` i wektorem wyrzutu `(X: 1.5, Y: 0.8, Z: 1.2)`.
- **Deszcz Krwi i Plamy (`Decal_Radial_Blood_Splatter`):**
  - Ślady kropel krwi rozchodzące się promieniście w promieniu 2.5m od punktu dekapitacji.

---

## 6. Integracja z Silnikiem Gry (Engine Triggers)

```json
{
  "sequence_id": "CS_TAKEDOWN_04_BLOOD_SHADOW",
  "duration": 4.6,
  "sync_mode": "PairedKinematicWithDismemberment",
  "events": [
    { "time": 0.10, "type": "AudioVoice", "cue": "BloodChess/Klan Krwawego Cienia/klan_krwawego_cienia_ekscytacja_01_48k.wav" },
    { "time": 0.60, "type": "AudioSFX", "cue": "sfx_blade_draw_sheath" },
    { "time": 1.15, "type": "VFXSpawn", "effect": "VFX_Katana_Slash_Trail", "socket": "katana_blade_edge" },
    { "time": 1.25, "type": "AudioSFX", "cue": "sfx_sword_whoosh_fast" },
    { "time": 1.30, "type": "DismemberBone", "target": "Victim", "bone": "Head", "spawn_physics_prop": "Prop_Head_Severed" },
    { "time": 1.30, "type": "AudioSFX", "cue": "sfx_clean_slice_decapitation" },
    { "time": 1.30, "type": "CameraShake", "intensity": 0.8, "duration": 0.2 },
    { "time": 1.35, "type": "VFXSpawn", "effect": "VFX_Decapitation_Geyser", "socket": "victim_neck_cut_socket" },
    { "time": 1.40, "type": "AudioSFX", "cue": "sfx_arterial_spray_high_pressure" },
    { "time": 2.20, "type": "AudioSFX", "cue": "sfx_head_bounce_ground" },
    { "time": 2.30, "type": "EnableRagdoll", "target": "VictimTorso", "impulse": [0, 60, -30] },
    { "time": 3.00, "type": "AudioSFX", "cue": "sfx_body_drop_heavy" },
    { "time": 3.30, "type": "SpawnDecal", "decal": "Decal_Radial_Blood_Splatter", "attach_to_ground": true },
    { "time": 3.90, "type": "AudioSFX", "cue": "sfx_sword_resheath_click" },
    { "time": 4.60, "type": "CutsceneComplete", "cleanup_victim_piece": true }
  ]
}
```
