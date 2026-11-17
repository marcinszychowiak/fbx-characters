# Roadmap i Rejestr Elementów 3D: Migracja Proceduralnych Brył Three.js do Modeli GLB

Dokument stanowi oficjalny rejestr techniczny i mapę drogową (Backlog Inżynieryjny) dla projektu **BloodChess**. Inwentaryzuje wszystkie elementy oprawy wizualnej, które w obecnej fazie prototypu budowane są proceduralnie z prymitywów geometrycznych Three.js (`CylinderGeometry`, `BoxGeometry`, `ConeGeometry`, `TorusGeometry`), oraz definiuje priorytety i standardy ich podmiany na dedykowane modele 3D w formacie glTF 2.0 (`.glb`).

---

## 1. Matryca Priorytetów Podmiany (Asset Migration Priority)

| Priorytet | Obszar Assetów | Plik w Kodzie Silnika | Uzasadnienie | Status |
| :---: | :--- | :--- | :--- | :---: |
| **P1** | **Zestaw Broni i Tarcz** | `pieceBuilder.ts` | Najbardziej rzuca się w oczy podczas zbliżeń kamery i animacji takedownów; obecne bryły kanciaste zaburzają immersję. | Role specjalne: WDROŻONE (`modeleBC/`)<br>Frakcyjne: W toku |
| **P2** | **Cokoły (Podstawki) i Nakrycia Ról** | `pieceBuilder.ts` | Kluczowe dla natychmiastowej czytelności hierarchii szachowej (Król, Hetman, Goniec, Skoczek, Wieża). | Częściowo (`korona.glb`) |
| **P3** | **Rekwizyty Cutscenek Egzekucji** | `queenCutsceneDirector.ts` | Wyświetlane na pełnym ekranie w zbliżeniach makro podczas bicia Hetmana (wiadro, kwas, odcięta głowa). | Oczekuje na GLB |
| **P4** | **Otoczenie Areny i Szachownica** | `ChessSceneManager.ts` | Tło sceny (koksowniki, kolumny cytadeli, rzeźbiona rama stołu szachowego). | Oczekuje na GLB |
| **P5** | **Warianty Postaci Frakcji** | `modeleBC/` | Opcjonalne warianty siatki postaci dla poszczególnych ról (alternatywa dla dekorowania bazowego wojownika). | Baza frakcyjna gotowa |

---

## 2. Szczegółowy Rejestr Elementów Proceduralnych

### 2.1. Bronie Główne, Tarcze i Przedmioty Podręczne (`pieceBuilder.ts`) — [PRIORYTET P1]

Wszystkie obiekty trzymane w rękach figur na szachownicy składane są obecnie z walców i prostopadłościanów.

#### A. Bronie Ról Specjalnych (Wspólne dla wszystkich armii):
- **Król (King):**
  - *Prawa dłoń:* Miecz królewski z jelcem i głowicą (`royal_hilt`, `royal_guard`, `blade`). **Status:** WDROŻONO model `miecz_krola.glb` (chwyt w `Z = 0`).
  - *Lewa dłoń:* Berło królewskie i jabłko panowania (`king_scepter_rod`, `king_orb`). **Status:** WDROŻONO model `berlo.glb` (chwyt w `Z = 0`).
- **Królowa / Hetman (Queen):**
  - *Lewa dłoń:* Sztylet paradny z ozdobną rękojeścią (`queen_dagger_hilt` + ostrze). **Status:** WDROŻONO model `sztylet_krolowa.glb` (chwyt w `Z = 0`).
- **Skoczek (Knight — Jeździec na `kon.glb`):**
  - *Prawa dłoń:* Długa kopia kawaleryjska z proporcem (`cavalry_lance`). **Status:** WDROŻONO model `kopia.glb` (chwyt za tarczką w `Z = 0`).
  - *Lewa dłoń:* Mała okrągła tarcza kawaleryjska / puklerz (`knight_buckler`). **Status:** WDROŻONO model `puklerz.glb` (uchwyt w `Y = 0`).
- **Goniec (Bishop):**
  - *Prawa dłoń:* Długi kostur / pastorał zwieńczony klejnotem lub grotem (`bishop_staff`). **Status:** WDROŻONO model `kostur_gonca.glb` (środek chwytu w `Z = 0`).
  - *Lewa dłoń:* Rytualna kadzielnica na łańcuchu lub święty kielich (`bishop_censer`).
- **Wieża (Rook — Strażnik na baszcie `wieza.glb`):**
  - *Prawa dłoń:* Ciężki dwuręczny młot oblężniczy (`rook_maul`).
  - *Lewa dłoń:* Wielka prostokątna tarcza piechoty / pawęż (`rook_pavise_shield`).

#### B. Bronie Frakcyjne (Piony i Królowe wg `weaponStyle`):
- **Wikingowie / Rzeźnicy:** Topór bojowy jednoręczny/dwuręczny (`axe_shield`, `butcher_cleaver`) + tarcza wikingów.
- **Nieumarli (Horda):** Długa kosa ponurego żniwiarza (`scythe`).
- **Ninja (Klan) / Piraci (Korsarze):** Zakrzywiona katana (`katana`) / piracka szabla/kordelas (`scimitar`) + sztylet tanto/sztylet ninja.
- **Żołnierze / Kowboje / Mafia:** Karabin piechoty z bagnetem (`rifle_bayonet`), rewolwer kowbojski z lassem (`revolver_lasso`), pistolet maszynowy Tommy Gun z kastetem (`tommy_knuckles`).
- **Piony Tarczowe (Pozostałe armie):** Okrągła tarcza piechura z okuciem stalowym (`round_shield_pawn`).

---

### 2.2. Podstawki pod Figury i Oznaczenia Rang (`pieceBuilder.ts`) — [PRIORYTET P2]

Każda figura osadzona jest na cokole determinującym przynależność do drużyny i hierarchię.

#### A. Podstawka Bitewna:
- **Obecny stan:** Prosty walec z proceduralną teksturą kamienia (`plinth`) + świecący pierścień drużyny z `TorusGeometry` (biały / czerwony) oraz dodatkowe stopnie podwyższenia (`royal_step`, `bishop_step`).
- **Rekomendowane rozwiązanie docelowe:** Jeden wspólny, rzeźbiony model cokołu figurkowego **`podstawka.glb`**, skalowany dynamicznie w kodzie:
  - Skala bazowa (Pion, Skoczek, Wieża): `1.0x`
  - Skala podwyższona (Goniec): `1.1x`
  - Skala majestatyczna (Hetman, Król): `1.2x`
  - Slot na materiał emissive (kolor armii).

#### B. Szaty i Zbroja Rang:
- Peleryny rangowe (`rank_cape`) – obecnie płaskie płaszczyzny geometryczne dla Króla, Królowej i Gońca.
- Naramienniki z kolcami (`rank_pauldron`), kołnierze królewskie (`royal_collar_*`), haftowane stuły Gońca (`bishop_stole_trim`).

#### C. Nakrycia Głowy Ról (poza zintegrowaną już `korona.glb`):
- **Wieża:** Minisylwetka baszty / czepiec z blankami (`bc_rook_turret` + `merlon`) na głowie strzelca.
- **Goniec:** Stożkowa mitra biskupia (`bc_bishop_mitre`) oraz aureola z torusa (`halo`) za głową.
- **Skoczek:** Grzebień hełmowy i powiewająca kita końska (`bc_knight_crest_arch` + `plume`) na głowie jeźdźca.

---

### 2.3. Rekwizyty Cutscenek Egzekucji Hetmana (`queenCutsceneDirector.ts`) — [PRIORYTET P3]

W scenach bicia Hetmana używane są dedykowane, przeskalowane rekwizyty cinematic:
- **Broń do egzekucji:**
  - Katana Klanu Krwawego Cienia,
  - Wielki Topór Wikingów,
  - Dwuręczny Miecz Krzyżowców (Zakon),
  - Stiletto / Sztylety (Piraci, Żołnierze, Mafia),
  - Rewolwer Kowboja.
- **Odcięta Głowa Hetmana:** Obecnie gładka kula z walcem szyi (na której osadzana jest `korona.glb`). Wymaga modelu `severed_queen_head.glb` z przygotowanym socketem szyjnym (`victim_neck_cut_socket`).
- **Wiadro z łatwopalnym paliwem (Gobliny):** Obecnie stalowy walec z płonącą powierzchnią. Docelowo: `prop_fuel_bucket.glb`.
- **Butla / kolba z żrącym kwasem (Rzeźnia):** Obecnie zielony cylinder emisyjny. Docelowo: `prop_acid_flask.glb`.

---

### 2.4. Arena i Otoczenie Szachownicy (`ChessSceneManager.ts`) — [PRIORYTET P4]

Elementy scenografii sali bitewnej:
- **Szachownica i Rama:** Płyta obsydianowa z mosiężnym obramowaniem (`outerFrame`, `trimBox`, `tileGeo`). Docelowo rzeźbiony stół bitewny `arena_board_frame.glb`.
- **Koksowniki Narożne (4 sztuki):** Stojaki ze stożkowymi bryłami ognia (`stand`, `bowl`, `coals`, `flameGroup`). Docelowo gotowy model koksownika `prop_brazier.glb` ze zintegrowanym punktem emisyjnym dla cząsteczek ognia.
- **Kolumny Cytadeli w Tle (8 sztuk):** Walce geometryczne (`bgPillarGeo`). Docelowo modułowe kolumny kamienne `arch_citadel_pillar.glb`.
- **Kamienna Posadzka:** Płaski okrąg (`floor`).

---

## 3. Standardy Techniczne dla Nowych Modeli .GLB

Dla zachowania spójności z dotychczas wdrożonymi modelami z folderu `modeleBC/`:
1. **Format:** Wyłącznie binarny **glTF 2.0 (`.glb`)** z osadzonymi teksturami i materiałami PBR.
2. **Skalowanie:** Skala metryczna `1 jednostka = 1 metr` w przestrzeni Three.js / Blender.
3. **Punkty Obrotu (Pivot / Origin):**
   - *Bronie i rekwizyty ręczne:* Punkt obrotu dokładnie w miejscu chwytu dłoni (`Grip Origin`).
   - *Nakrycia głowy i korony:* Punkt obrotu u podstawy wewnętrznej krawędzi nakrycia (dokładnie na styku z czubkiem głowy).
   - *Cokoły / Podstawki:* Punkt obrotu w środku geometrycznym dolnej płaszczyzny podstawy (`Y = 0`).
4. **Budżet Poligonów (LOD0):**
   - Bronie podręczne: 500 – 1 800 trójkątów.
   - Cokół bazowy: 800 – 2 000 trójkątów.
   - Rekwizyty otoczenia (koksownik, kolumna): 1 200 – 3 500 trójkątów.
