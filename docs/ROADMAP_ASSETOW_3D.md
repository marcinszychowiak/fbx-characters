# Roadmap i Rejestr Elementów 3D: Migracja Proceduralnych Brył Three.js do Modeli GLB

Dokument stanowi oficjalny rejestr techniczny i mapę drogową (Backlog Inżynieryjny) dla projektu **BloodChess**. Inwentaryzuje wszystkie elementy oprawy wizualnej, które w obecnej fazie prototypu budowane są proceduralnie z prymitywów geometrycznych Three.js (`CylinderGeometry`, `BoxGeometry`, `ConeGeometry`, `TorusGeometry`), oraz definiuje priorytety i standardy ich podmiany na dedykowane modele 3D w formacie glTF 2.0 (`.glb`).

---

## 1. Matryca Priorytetów Podmiany (Asset Migration Priority)

| Priorytet | Obszar Assetów | Plik w Kodzie Silnika | Uzasadnienie | Status |
| :---: | :--- | :--- | :--- | :---: |
| **P1** | **Zestaw Broni i Tarcz Ról Specjalnych** | `pieceBuilder.ts` | Najbardziej rzuca się w oczy podczas zbliżeń kamery i animacji takedownów; obecne bryły kanciaste zaburzają immersję. | **KOMPLETNY (100% WDROŻONY)**<br>Król, Królowa, Skoczek, Goniec, Wieża |
| **P1.5** | **Bronie Frakcyjne (Piony i Królowe)** | `pieceBuilder.ts` | Specyficzne oręże dla poszczególnych frakcji (topory, kosy, katany, broń palna). | Assety dostarczone (`bronie2`), przygotowane do kolejnej partii |
| **P2** | **Cokoły (Podstawki) i Nakrycia Ról** | `pieceBuilder.ts` | Kluczowe dla natychmiastowej czytelności hierarchii szachowej (Król, Hetman, Goniec, Skoczek, Wieża). | **KOMPLETNY (100% WDROŻONY)**<br>`podstawka.glb`, `korona.glb`, `czepiec_wiezy.glb`, `czapka_gonca.glb`, `kita_skoczka.glb` |
| **VFX** | **Efekty Mocy Specjalnej** | `pieceBuilder.ts` / Silnik | Wizualizacja ładowania i aktywacji unikalnych umiejętności figur. | **WDROŻONO** (`specialpower.glb` animowany słup energii) |
| **P3** | **Rekwizyty Cutscenek Egzekucji** | `queenCutsceneDirector.ts` | Wyświetlane na pełnym ekranie w zbliżeniach makro podczas bicia Hetmana (wiadro, kwas, odcięta głowa). | Oczekuje na GLB |
| **P4** | **Otoczenie Areny i Szachownica** | `ChessSceneManager.ts` | Tło sceny (koksowniki, kolumny cytadeli, rzeźbiona rama stołu szachowego). | Szachownica: WDROŻONO (`plansza.glb`)<br>Otoczenie: W toku |
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
  - *Lewa dłoń:* Rytualna kadzielnica na łańcuchu lub święty kielich (`bishop_censer`). **Status:** WDROŻONO model `kielich_gonca.glb` (złoty kielich ze szmaragdami, chwyt za nóżkę w `Z = 0`).
- **Wieża (Rook — Strażnik na baszcie `wieza.glb`):**
  - *Prawa dłoń:* Ciężki dwuręczny młot oblężniczy (`rook_maul`). **Status:** WDROŻONO model `mlot_wiezy.glb` (młot z runicznym obuszkiem, chwyt rękojeści Grip w `Z = 0`).
  - *Lewa dłoń:* Wielka prostokątna tarcza piechoty / pawęż (`rook_pavise_shield`). **Status:** WDROŻONO model `pawez_wiezy.glb` (pawęż z herbem, uchwyt rzemieniowy w `0, 0, 0`).

#### B. Bronie Frakcyjne (Piony i Królowe wg `weaponStyle`):
Modele wejściowe dostarczone w pakiecie `bronie2` (przygotowane do kalibracji w kolejnym etapie):
- **Wikingowie / Rzeźnicy:** Topór bojowy jednoręczny/dwuręczny (`axe_shield`, `butcher_cleaver`) + tarcza wikingów. *Dostępny asset:* `set_of_five_viking_medieval_axes_blood_texture.glb` (zestaw 5 toporów z krwią) oraz `baseball_bat_covered_in_blood.glb`.
- **Nieumarli (Horda):** Długa kosa ponurego żniwiarza (`scythe`).
- **Ninja (Klan) / Piraci (Korsarze):** Zakrzywiona katana (`katana`) / piracka szabla/kordelas (`scimitar`) + sztylet tanto/sztylet ninja.
- **Żołnierze / Kowboje / Mafia:** 
  - *Karabin piechoty:* Dostępny asset `low-poly_springfield_model_1873.glb`.
  - *Rewolwer kowbojski:* Dostępny asset `default_gun__roblox_murder_mystery_2_aka_mm2.glb`.
  - *Pistolet maszynowy Tommy Gun:* Dostępny asset `gangster_tommy_gun.glb`.
- **Piony Tarczowe (Pozostałe armie):** Okrągła tarcza piechura z okuciem stalowym (`round_shield_pawn`).

---

### 2.2. Podstawki pod Figury i Oznaczenia Rang (`pieceBuilder.ts`) — [PRIORYTET P2 - WDROŻONY]

Każda figura osadzona jest na cokole determinującym przynależność do drużyny i hierarchię.

#### A. Podstawka Bitewna:
- **Status:** **WDROŻONO** model **`podstawka.glb`** (alias: `cokol.glb`).
  - Rzeźbiony kamienny cokół bitewny z detalami gruzu i pochyłą krawędzią.
  - Średnica bazowa: `0.95 m` (dokładnie dopasowana do pola `1.15 m`).
  - Wysokość: `0.135 m`.
  - Dno spoczywa idealnie na `Z = 0` (Three.js `Y = 0`), a wierzch tworzy platformę na stopy figurki.
  - Zoptymalizowana siatka (Decimate): waga zmniejszona z 5.1 MB do zaledwie **246 KB** (4 361 ścianek).

#### B. Szaty i Zbroja Rang:
- Peleryny rangowe (`rank_cape`) – obecnie płaskie płaszczyzny geometryczne dla Króla, Królowej i Gońca.
- Naramienniki z kolcami (`rank_pauldron`), kołnierze królewskie (`royal_collar_*`), haftowane stuły Gońca (`bishop_stole_trim`).

#### C. Nakrycia Głowy Ról (WDROŻONE W CAŁOŚCI):
- **Król i Hetman:** Model `korona.glb` (duża dla Króla, mniejsza dla Hetmana).
- **Wieża:** Model `czepiec_wiezy.glb` (stalowy hełm z ochraniaczami policzków i grzebieniem, podstawa w `Z = 0`).
- **Goniec:** Model `czapka_gonca.glb` (trójrożna czapka błazeńska z dzwoneczkami, podstawa w `Z = 0`).
- **Skoczek:** Model `kita_skoczka.glb` (pełny hełm rycerski z kitą/pióropuszem na szczycie, podstawa w `Z = 0`).

---

### 2.2.1. Efekty Mocy Specjalnej (VFX) — [NOWOŚĆ - WDROŻONY]
- **Status:** **WDROŻONO** model **`specialpower.glb`**.
  - Animowany, wielowarstwowy słup pulsujących pierścieni energii / aury.
  - Wysokość: `2.10 m` (obejmuje sylwetkę wojownika o wzroście 1.8 m), podstawa na `Z = 0`.
  - Zawiera 4 niezależne ścieżki animacji glTF (`Take 001_Plane001_4` do `Plane004_3`).
  - W obecnym etapie pełni rolę efektu uniwersalnego dla wszystkich armii (w kolejnych etapach każda armia otrzyma unikalną odmianę kolorystyczną lub geometryczną).

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
- **Szachownica i Rama:** Płyta obsydianowa z mosiężnym obramowaniem (`outerFrame`, `trimBox`, `tileGeo`). **Status:** WDROŻONO model `plansza.glb` (rzeźbiony stół z czarnego onyksu i białego marmuru; skala skalibrowana do 1 pole = `1.15 m`, 64 pola = `9.20 m`, powierzchnia kafelków w `Y = 0`, z węzłami pomocniczymi `Board_Center`, `Tile_A1_Corner`, `Tile_H8_Corner`).
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
