# FBX Characters & Models Collection

Zbiór 52 modeli postaci 3D w formacie FBX (modularne postacie humanoidów, zwierząt oraz akcesoriów), gotowych do wykorzystania w silnikach gier (Unity, Unreal Engine, Godot) oraz programach do animacji i modelowania 3D (Blender, Maya, 3ds Max).

## Zawartość katalogu `FBX/`

Kolekcja zawiera 52 modele FBX:

### Postacie podstawowe i codzienne (Casual)
- `BaseCharacter.fbx`
- `Casual_Male.fbx`
- `Casual_Female.fbx`
- `Casual_Bald.fbx`
- `Casual2_Male.fbx`
- `Casual2_Female.fbx`
- `Casual3_Male.fbx`
- `Casual3_Female.fbx`
- `Suit_Male.fbx`
- `Suit_Female.fbx`
- `OldClassy_Male.fbx`
- `OldClassy_Female.fbx`

### Zawody i profesje
- `Chef_Male.fbx`
- `Chef_Female.fbx`
- `Chef_Hat.fbx`
- `Doctor_Male_Young.fbx`
- `Doctor_Female_Young.fbx`
- `Doctor_Male_Old.fbx`
- `Doctor_Female_Old.fbx`
- `Worker_Male.fbx`
- `Worker_Female.fbx`

### Wojownicy, wojsko i straż
- `Soldier_Male.fbx`
- `Soldier_Female.fbx`
- `BlueSoldier_Male.fbx`
- `BlueSoldier_Female.fbx`
- `Knight_Male.fbx`
- `Knight_Golden_Male.fbx`
- `Knight_Golden_Female.fbx`
- `Ninja_Male.fbx`
- `Ninja_Female.fbx`
- `Ninja_Male_Hair.fbx`
- `Ninja_Sand.fbx`
- `Ninja_Sand_Female.fbx`
- `Cowboy_Male.fbx`
- `Cowboy_Female.fbx`
- `Cowboy_Hair.fbx`
- `Pirate_Male.fbx`
- `Pirate_Female.fbx`
- `Viking_Male.fbx`
- `Viking_Female.fbx`
- `VikingHelmet.fbx`
- `Kimono_Male.fbx`
- `Kimono_Female.fbx`

### Fantasy i stworzenia
- `Elf.fbx`
- `Goblin_Male.fbx`
- `Goblin_Female.fbx`
- `Wizard.fbx`
- `Witch.fbx`
- `Zombie_Male.fbx`
- `Zombie_Female.fbx`
- `Cow.fbx`
- `Pug.fbx`

---

## Referencje do cutscenek (`Cutscenes/`)

Katalog `Cutscenes/` zawiera materiały wideo (MP4) stanowiące referencje narracyjne i animacyjne:
- `gobliny .mp4`
- `horda .mp4`
- `klan Krwawego Cienia .mp4`
- `kowboj .mp4`
- `najemnicy .mp4`
- `pirat.mp4`
- `rzeźnia .mp4`
- `syndykat .mp4`
- `wikingowie .mp4`
- `zakon.mp4`

---

## Głosy frakcji (`BloodChess/`)

Katalog `BloodChess/` zawiera linie dialogowe i kwestie głosowe (pliki audio `.wav`, jakość 48 kHz) podzielone według 10 frakcji:
- **Horda** (5 plików)
- **Klan Krwawego Cienia** (4 pliki)
- **Korsarze** (4 pliki)
- **Kowboj** (4 pliki)
- **Najemnicy** (4 pliki)
- **Rzeźnia** (`Rzeznia/`, 1 plik)
- **Sabat Goblinów** (4 pliki)
- **Syndykat** (4 pliki)
- **Wikingowie z krwawego fiordu** (5 plików)
- **Zakon** (4 pliki)

---

## Scenariusze i Specyfikacje Cutscenek (`Scenarios/`)

Katalog `Scenarios/` zawiera kompletne, techniczne specyfikacje dla programu i kreatora gry **BloodChess** do implementacji i wygenerowania 10 sekwencji takedownów:
- [README.md (Architektura i indeks)](Scenarios/README.md)
- `01_Kowboj.md` – Egzekucja rewolwerem pod brodą
- `02_Sabat_Goblinow.md` – Podpalenie ofiary cieczą łatwopalną
- `03_Horda.md` – Kanibalistyczny atak zombie na gardło
- `04_Klan_Krwawego_Cienia.md` – Dekapitacja kataną i gejzer krwi
- `05_Najemnicy.md` – Taktyczne poderżnięcie gardła nożem bojowym
- `06_Korsarze.md` – Powalenie i wielokrotne sztyletowanie w parterze
- `07_Rzeznia.md` – Rozpuszczenie twarzy kwasem chemicznym
- `08_Syndykat.md` – Mafijna eliminacja pchnięciem stiletto
- `09_Wikingowie.md` – Rozbicie mostka i wbicie topora bojowego
- `10_Zakon.md` – Święte cięcie egzekucyjne dwuręcznym mieczem

---

## Dedykowane modele postaci i figur BloodChess (`modeleBC/`)

Katalog `modeleBC/` zawiera dedykowane modele 3D postaci frakcyjnych oraz kluczowych figur bitewnych stworzonych specjalnie dla gry **BloodChess** w formacie binarnym glTF 2.0 (`.glb`). 

> [!IMPORTANT]
> **Gotowość do animacji i montażu (Rigging & Sockets):**  
> Wszystkie modele postaci zostały wyposażone w **szkielet humanoid (19 kości)** z automatycznymi wagami deformacji (skinning) oraz **wbudowane sockety (Empty Objects)** dla elementów ekwipunku:
> - `Socket_Crown` – punkt na czubku głowy dla korony (`korona.glb`) oraz nakryć ról,
> - `Socket_Hand_R` – punkt w prawej dłoni dla broni głównej,
> - `Socket_Hand_L` – punkt w lewej dłoni dla tarczy/przedmiotu,
> - `Socket_Back` – punkt na plecach pod pelerynę,
> - `Socket_Rider` – punkt siodła w `kon.glb` oraz podestu w `wieza.glb`.  
> Siatki zostały zoptymalizowane do poziomu ~20 000 trójkątów per model (rozmiar każdego pliku zredukowany z ~15 MB do ok. 1.3 MB), co zapewnia natychmiastowe ładowanie i płynne 60 fps.

### Lista modeli (wraz z aliasami angielskimi dla Studio):
- `goblin.glb` (alias: `goblins.glb`) – Sabat Goblinów (Humanoid Rig + Sockets, wzrost: 70 cm)
- `horda.glb` (alias: `undead.glb`) – Horda (Humanoid Rig + Sockets, wzrost: 180 cm)
- `klan.glb` (alias: `ninjas.glb`) – Klan Krwawego Cienia (Humanoid Rig + Sockets, wzrost: 175 cm wyprostowany / 142 cm w przysiadzie)
- `kon.glb` – Koń / Skoczek bitewny (`Socket_Rider` w siodle)
- `korsarz.glb` (alias: `pirates.glb`) – Korsarze (Humanoid Rig + Sockets, wzrost: 180 cm)
- `kowboj.glb` (alias: `cowboys.glb`) – Kowboj (Humanoid Rig + Sockets, wzrost: 180 cm)
- `najemnicy.glb` (alias: `soldiers.glb`) – Najemnicy (Humanoid Rig + Sockets, wzrost: 190 cm)
- `rzeznik.glb` (alias: `butchers.glb`) – Rzeźnia (Humanoid Rig + Sockets, wzrost: 160 cm)
- `Syndykat.glb` (alias: `mafia.glb`) – Syndykat (Humanoid Rig + Sockets, wzrost: 170 cm)
- `wieza.glb` – Wieża / Podstawa wieży (`Socket_Rider` na platformie)
- `wiking.glb` (alias: `vikings.glb`) – Wikingowie z krwawego fiordu (Humanoid Rig + Sockets, wzrost: 215 cm)
- `zakon.glb` (alias: `crusaders.glb`) – Zakon (Humanoid Rig + Sockets, wzrost: 190 cm)
- `korona.glb` – Korona / Atrybut królewski (dolna obręcz wycentrowana na `(0, 0, 0)`)
- `proponowane_skale_studio.png` – Plansza referencyjna skali z siatką wysokości (0.70 m – 2.15 m).

### Dedykowane uzbrojenie i ekwipunek ról (Grip Origin w `0, 0, 0`):
- `miecz_krola.glb` – Miecz królewski (prawa dłoń Króla, chwyt rękojeści z jelcem w `Z = 0`)
- `berlo.glb` – Berło królewskie (lewa dłoń Króla, chwyt w `Z = 0`)
- `sztylet_krolowa.glb` – Sztylet paradny Królowej (lewa dłoń Królowej, chwyt w `Z = 0`)
- `kopia.glb` – Kopia kawaleryjska Skoczka (prawa dłoń jeźdźca, punkt chwytu za tarczką w `Z = 0`)
- `puklerz.glb` – Mała tarcza / puklerz Skoczka (lewa dłoń jeźdźca, wewnętrzny uchwyt w `Y = 0`, centrowanie `X,Z = 0`)
- `kostur_gonca.glb` – Pastorał / kostur Gońca (prawa dłoń Gońca, środek chwytu drzewca w `Z = 0`)
- `kielich_gonca.glb` – Złoty kielich rytualny Gońca (lewa dłoń `Socket_Hand_L`, punkt chwytu za nóżkę w `Z = 0`)
- `mlot_wiezy.glb` – Ciężki młot oblężniczy Wieży (`rook_maul`, prawa dłoń `Socket_Hand_R`, chwyt rękojeści Grip w `Z = 0`)
- `pawez_wiezy.glb` – Wielka pawęż piechoty z herbem dla Wieży (`rook_pavise_shield`, lewa dłoń `Socket_Hand_L`, uchwyt rzemieniowy w `0, 0, 0`)

### Nakrycia głowy i atrybuty ról (`Socket_Crown` w `Z = 0`):
- `korona.glb` – Korona królewska (dwukrotne użycie: duża dla Króla, mniejsza dla Hetmana)
- `czepiec_wiezy.glb` – Stalowy hełm z ochraniaczami policzków dla Wieży (`bc_rook_turret`)
- `czapka_gonca.glb` (alias: `goniec_czapka.glb`) – Trójrożna czapka błazeńska z dzwoneczkami dla Gońca
- `kita_skoczka.glb` – Hełm rycerski z pióropuszem/kitą dla Skoczka (`bc_knight_crest_arch` + `plume`)

### Cokoły pod figury:
- `podstawka.glb` (alias: `cokol.glb`) – Rzeźbiony kamienny cokół bitewny z gruzem i pochyłą krawędzią (średnica `0.95 m` pod pole szachowe `1.15 m`, wysokość `0.135 m`, dno spoczywające dokładnie na `Z = 0`, waga zredukowana ze 124k do 4.3k ścianek — tylko 246 KB).

### Efekty VFX i Mocy Specjalnej:
- `specialpower.glb` – Animowany pionowy słup pulsujących pierścieni energii/aury podczas aktywacji mocy specjalnej (wysokość `2.10 m`, dno na poziomie ziemi `Z = 0`, 4 zintegrowane animacje Take 001). Tymczasowo wspólny dla wszystkich armii, docelowo zindywidualizowany per frakcja.

### Trójwymiarowe Symbole Rang Szachowych (Lewitujące wskaźniki zaznaczenia):
Zestaw modeli 3D glTF 2.0 wygenerowanych z glifów Unicode (wysokość `0.40 m`, pivot w geometrycznym środku `0, 0, 0`, fazowane krawędzie, materiał PBR przystosowany do dynamicznego barwienia kolorem armii):
- `symbol_krol.glb` – Symbol Króla (♔ / ♚)
- `symbol_hetman.glb` – Symbol Hetmana / Królowej (♕ / ♛)
- `symbol_wieza.glb` – Symbol Wieży (♖ / ♜)
- `symbol_goniec.glb` – Symbol Gońca (♗ / ♝)
- `symbol_skoczek.glb` – Symbol Skoczka (♘ / ♞)
- `symbol_pion.glb` – Symbol Piona (♙ / ♟)
- `symbole_szachowe_3d.glb` – Paczka zbiorcza ze wszystkimi 6 symbolami.
- `showcase_symbole_szachowe_3d.png` – Prezentacja wizualna 6 symboli szachowych.
- `showcase_10_frakcji_kolory.png` – Oficjalna paleta 10 frakcji z przypisanymi barwami i emisyjnym blaskiem PBR.

### Scenografia i Arena:
- `sceneria_lochy.glb` – **Kompletna arena lochów 3D (35 MB)**: Zintegrowane, gotowe do natychmiastowego wczytania w Three.js środowisko bitewne zawierające:
  - Centralną, wyniesioną szachownicę ($9.20\text{ m} \times 9.20\text{ m}$, platforma $10.40\text{ m} \times 10.40\text{ m}$),
  - Dwustronne kamienne schody wejściowe ($5.20\text{ m}$ szerokości) ze spadkiem na poziom podłogi lochu ($Z = -3.00\text{ m}$) dla armii Białych (południe) i Czarnych (północ),
  - 4 koksowniki z płonącym ogniem w rogach platformy planszy ($X, Y = \pm 5.35\text{ m}$),
  - Modularne mury kamienne lochów odsunięte na bezpieczny dystans $X = \pm 10.50\text{ m}$ (tworząc szerokie, ponad 4.5-metrowe wolne korytarze boczne gwarantujące $100\%$ czyste, niezasłonięte pole widzenia szachownicy z każdego kąta kamery),
  - Północny i południowy portal wejściowy z monumentalnymi łukami kamiennymi ($Y = \pm 13.50\text{ m}$),
  - 6 masywnych filarów narożnych i międzymurowych,
  - 4 powiewające sztandary heraldyczne (animacja szkieletowa 60 klatek) wiszące na murach tuż za koksownikami na $X = \pm 9.70\text{ m}$ – neutralne, gotowe pod przypisanie kolorów frakcji i nałożenie symboli bierek w Three.js.
- `schody.glb` – Samodzielny model kamiennych schodów (szerokość $5.20\text{ m}$, długość $7.14\text{ m}$, spadek $3.00\text{ m}$) z wycentrowaną osią X i pivotem na krawędzi górnego podestu.
- `sztandar.glb` – Samodzielny model powiewającego sztandaru heraldycznego (szkielet z 10 kośćmi, zapętlona akcja wiatru 60 klatek, skala metryczna: szerokość $0.94\text{ m}$, zwis $4.14\text{ m}$).
- `plansza.glb` (alias: `luxury_onyx_and_marble_chess_board.glb`) – Luksusowy stół szachowy z polerowanego czarnego onyksu, białego marmuru i mosiężnego okuciu. Skalibrowany dokładnie pod silnik: 1 pole = `1.15 m` (szerokość 8x8 pól = `9.20 m`), wierzch kafelków dokładnie na `Y = 0`, z węzłami pomocniczymi `Board_Center`, `Tile_A1_Corner`, `Tile_H8_Corner`.
- `koksownik.glb` – Bojowy koksownik zamkowy (kamienny postument + mosiężna misa, wysokość 1.41 m, podstawa 0.79 m na Z=0, gniazdo `Socket_Flame` w misie na Z=1.22 m).
- `ogien_do_koksownika.glb` – Wieloczęściowy, animowany ogień (192 niezależne meshe płomieni/iskier, zapętlona akcja 30 klatek, średnica 0.49 m, wysokość 0.64 m, punkt zaczepienia w Z=0).
- `koksownik_z_ogniem.glb` – Kompletny, zintegrowany asset (koksownik + animowany ogień w misie, łączna wysokość 1.86 m). Rekomendowany do rozstawienia w 4 rogach szachownicy (`X, Z = ±5.20 m`).
- `preview_arena_lochy_mecz.png` – Wyrenderowana prezentacja areny lochów: zablokowany taktyczny widok kamery meczowej z góry.
- `preview_arena_lochy_biale.png` – Wyrenderowana prezentacja: widok od dołu południowych schodów Białych prowadzących na oświetloną szachownicę.
- `preview_arena_lochy_detal.png` – Wyrenderowana prezentacja: cinematic detal płonącego koksownika, kamiennego muru i powiewającego sztandaru.
- `preview_koksownik_z_ogniem.png` – Wyrenderowana prezentacja wizualna płonącego koksownika na kamiennej posadzce w nastrojowym oświetleniu sali zamkowej.

### Animacje Cutscenek Takedownów i Zbić:
- `horda_bije_hetmana_cutscene.mp4` – Wyrenderowana filmowa cutscenka wideo (H.264, 24 fps, 854x480) przedstawiająca sekwencję zbijania Hetmana Syndykatu przez Hordę (szarża, potężny cios pięścią, śmiertelny upadek Hetmana na marmur, okrzyk triumfu zombie).
- `takedown_horda_syndykat.glb` – Kompletna, zintegrowana scena 3D glTF 2.0 (9.8 MB) zawierająca planszę, obie postacie ze szkieletami, rekwizyty i wielościeżkowe animacje NLA, gotowa do bezpośredniego odtworzenia w silniku Three.js gry.

> [!NOTE]
> **Wykorzystanie korony (`korona.glb`) w armii:**  
> W obrębie danej armii model korony jest wykorzystywany **dwukrotnie** z odpowiednim skalowaniem w silniku gry:
> - **Dla Króla (King):** wersja większa (skalowanie standardowe / powiększone, np. 1.15x - 1.20x),
> - **Dla Hetmana / Królowej (Queen):** wersja mniejsza (skalowanie pomniejszone, np. 0.85x - 0.90x).

---

## Ścieżka dźwiękowa (`Soundtrack/`)

Katalog `Soundtrack/` gromadzi utwory muzyczne (BGM) dla gry **BloodChess**:
- [README.md (Instrukcja i architektura audio)](Soundtrack/README.md)
- `Universal_Battle_Theme_01.mp3` – Główny, orkiestrowy motyw bitewny (4:04)

> [!TIP]
> **Mechanizm losowania muzyki meczu:**  
> W trakcie partii ścieżka dźwiękowa wybierana jest losowo spośród utworów przypisanych do armii biorących udział w grze oraz **jednej z dwóch ścieżek uniwersalnych**. Katalog będzie sukcesywnie uzupełniany o kolejne utwory frakcyjne i uniwersalne.

---

## Dokumentacja Projektowa i Roadmapa (`docs/`)

- [`docs/INSTRUKCJA_STUDIO_INTERAKCJA_KAMERA.md`](docs/INSTRUKCJA_STUDIO_INTERAKCJA_KAMERA.md) – **Instrukcja dla Studio**: Implementacja systemu Double-Tap (PC & Mobile), sztywna blokada kamery meczowej, obsługa symboli 3D oraz warunek poziomu trudności (zasięg rażenia wroga tylko w trybie Easy vs SI).
- [`docs/INSTRUKCJA_MODELI_3D.md`](docs/INSTRUKCJA_MODELI_3D.md) – **Instrukcja przygotowania i dopasowania modeli 3D**: standardy przestrzeni, system socketów (`Socket_Crown`, `Socket_Hand_R`, `Socket_Rider`), obsługa wariantów jeźdźców oraz strategie pracy z generatorami AI (Tripo.AI) i Blenderem.
- [`docs/ROADMAP_ASSETOW_3D.md`](docs/ROADMAP_ASSETOW_3D.md) – **Kompleksowy rejestr i mapa drogowa migracji**: lista elementów 3D generowanych obecnie proceduralnie w Three.js (`pieceBuilder.ts`, `queenCutsceneDirector.ts`, `ChessSceneManager.ts`) z priorytetami podmiany na docelowe modele `.glb`.
- [`docs/DOKUMENT_TECHNOLOGICZNY.md`](docs/DOKUMENT_TECHNOLOGICZNY.md) – Zrozumiałe uzasadnienie doboru formatów (FBX, GLB, WAV 48k, MP3, Markdown/JSON, Git).
- [`docs/STUDY_CASE_10000H.md`](docs/STUDY_CASE_10000H.md) – Dziennik postępów i decyzji architektonicznych w projekcie („Po 10 000 godzin vibecodingu jesteś programistą”).

---

## Zastosowanie
- **Game Engine**: Unity, Unreal Engine 5, Godot Engine.
- **DCC Tools**: Blender, Autodesk Maya, 3ds Max.
- **Rigg / Animacja**: Standardowy szkielet kompatybilny z mechanizmem humanoid / retargeting (np. Mixamo, Unity Mecanim, UE Control Rig).
