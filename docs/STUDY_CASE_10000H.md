# Case Study: Po 10 000 godzin vibecodingu jesteś programistą

## Wpis 1: Od luźnych plików na pulpicie do ustrukturyzowanego silnika bitewnego gry „BloodChess”

### 1. Kontekst wyjściowy (Vibe Coding w praktyce)
Projekt rozpoczął się od typowego, chaotycznego zestawu assetów tworzonych w twórczym transie: 
- 52 modele FBX spakowane w archiwum,
- folder na Pulpicie z 10 plikami wideo MP4 przedstawiającymi surowe animacje manekinów w low-poly dokonujących krwawych egzekucji,
- folder w Pobranych z 39 plikami audio WAV z nagraniami głosowymi 10 unikalnych frakcji bitewnych.

Twórca idei rzucił krótkie, precyzyjne polecenia:
> *„wypchnij to proszę do tego samego repo. To referencje do cutscenek.”*  
> *„też wypchnij do repo. To głosy dla każdej frakcji.”*  
> *„Przygotuj pliki .md ze scenariuszem dla kreatora do zrealizowania każdej z cutscenek. Scenariusze wyślemy do repozytorium dla programu, który buduje grę, żeby wiedział, jak mają wyglądać cutscenki w finalnej wersji gry.”*

W tradycyjnym modelu produkcji gier przygotowanie takiego zestawu zajęłoby zespołowi game designerów, scenarzystów i technical animatorów przynajmniej 2–3 tygodnie spotkań, pisania GDD i rozrysowywania storyboardów. W realiach pracy Architekta Antigravity z twórcą stało się to kwestią jednej spójnej sesji.

---

### 2. Wyzwania inżynieryjne i decyzje architektoniczne

#### A. Multimodalna percepcja wideo przez AI
Jednym z kluczowych kroków było samodzielne obejrzenie przez agenta każdego z 10 plików MP4 za pomocą mechanizmu `read_file`. Agent przeanalizował klatka po klatce:
- `kowboj .mp4`: Strzał z bliska pod brodę rewolwerem.
- `gobliny .mp4`: Oblepienie łatwopalną cieczą z wiadra i podpalenie zapalniczką.
- `horda .mp4`: Kanibalistyczny skok zombie i wyszarpanie tętnicy szyjnej.
- `klan Krwawego Cienia .mp4`: Pozioma dekapitacja kataną i gejzer krwi.
- `najemnicy .mp4`: Taktyczne poderżnięcie gardła nożem z odciągnięciem głowy.
- `pirat.mp4`: Powalenie taranem na deski i trzykrotne wbicie sztyletu w mostek.
- `rzeźnia .mp4`: Wylanie żrącego kwasu na głowę i stopienie twarzy.
- `syndykat .mp4`: Eleganckie pchnięcie stiletto w klatkę piersiową dłużnika.
- `wikingowie .mp4`: Wbicie ciężkiego topora bojowego w klatkę piersiową.
- `zakon.mp4`: Dostojne cięcie egzekucyjne dwuręcznym mieczem ze stojącą modlitwą.

#### B. Most pomiędzy surowym wideo a programowalnym silnikiem gry
Samo obejrzenie to za mało dla programu budującego grę. Kreator gier potrzebuje liczb, gniazd kości, wektorów i precyzyjnych zdarzeń (anim events). 
Zbudowano standard scenariusza `.md`, który zawiera:
1. Mapowanie modeli z katalogu `FBX/` na role Agresora i Ofiary.
2. Przypisanie próbek audio z `BloodChess/` (linie dialogowe) oraz specyfikację efektów SFX.
3. Tabelę klatka-po-klatce w standardzie 30 fps z podziałem na role.
4. Wytyczne dla kamery (typ ujęcia, kąt, FOV, wstrząsy kamery / Camera Shake).
5. Zaawansowane efekty VFX (rozbryzgi krwi, dym, płomienie, shadery dissolve i zwęglenia).
6. Gotowy do bezpośredniego wstrzyknięcia do silnika blok JSON z listą eventów animacyjnych (`AnimNotify`).

---

## Wpis 2: Dedykowane modele frakcyjne GLB i detektywistyczna naprawa assetu (.tmp -> .glb)

### 1. Nowa partia assetów (`modeleBC`)
Użytkownik dostarczył katalog `modeleBC` zawierający dedykowane modele postaci stworzone specjalnie pod unikalne cechy każdej z 10 frakcji. W przeciwieństwie do ogólnych modeli z bazy `FBX/`, te modele reprezentują docelowy styl wizualny gry w nowoczesnym formacie binarnym glTF 2.0 (`.glb`).

### 2. Autonomiczna diagnoza binarnego uszkodzenia
W paczce pojawił się nietypowy plik: `kowboj.tmp` o wadze 8.3 MB, podczas gdy pozostałe pliki miały rozszerzenie `.glb`.
Zamiast przerwać pracę pytaniem do użytkownika, agent przeprowadził inspekcję binarną nagłówka:
- Magiczne bajty: `0x46546C67` (`glTF` w ASCII).
- Wersja: `2` (glTF 2.0).
- Zadeklarowany `HeaderLength`: `8 304 256` bajtów.
- Rzeczywisty rozmiar pliku na dysku: dokładnie `8 304 256` bajtów.

Plik był w 100% kompletnym, nieuszkodzonym modelem GLB, który z przyczyn systemowych zachował rozszerzenie tymczasowe pobierania. Agent automatycznie nadał mu poprawną nazwę `kowboj.glb` i zweryfikował integralność wszystkich 10 modeli przed zasileniem repozytorium.

---

### 3. Rozszerzenie o kluczowe figury i regalia: Koń, Wieża i Korona
Kolejnym krokiem twórcy było dostarczenie dedykowanych modeli kluczowych figur bitewnych oraz regaliów:
- `kon.glb` (12.4 MB) – model konia / skoczka szachowego,
- `wieza.glb` (15.7 MB) – model wieży / podstawy pod wieżę,
- `korona.glb` (16.8 MB) – model korony królewskiej. Zgodnie z wytycznymi twórcy, korona jest współdzielonym zasobem regaliów w armii i w silniku gry wykorzystywana jest dwukrotnie: w wersji większej (dla Króla) oraz mniejszej (dla Hetmana / Królowej).

Agent natychmiast zweryfikował sumy kontrolne i nagłówki glTF 2.0 wszystkich plików, po czym zintegrował je ze strukturą `modeleBC/` i zaktualizował dokumentację projektu.

---

## Wpis 3: Dynamiczna orkiestracja bitwy — architektura systemu ścieżki dźwiękowej (`Soundtrack/`)

### 1. Wizja muzyczna gry
Szachy bitewne „BloodChess” wymagają oprawy muzycznej budującej napięcie i potęgującej powagę pojedynku. Twórca zdefiniował prostą, ale niezwykle elastyczną regułę:
> *„ścieżka dźwiękowa wybierana jest losowo spośród tych przypisanych do armii biorących udział w grze oraz jednej z dwóch ścieżek uniwersalnych. Początkowo będzie tam tylko jedna ścieżka, ale w przyszłości będą dodawane kolejne.”*

### 2. Projekt architektury audio w silniku
Zamiast wrzucać plik muzyczny jako luźny asset, agent opracował kompletną specyfikację techniczną w `Soundtrack/README.md`:
- Dynamiczny selector puli utworu (`MatchMusicPool`): silnik przy starcie meczu aggregeuje utwory Frakcji A, Frakcji B oraz uniwersalne motywy bitewne, losując podkład dla danej partii.
- Zaimplementowano regułę audio duckingu (`-9 dB`), wyciszającą muzykę tła w trakcie odpalania brutalnych egzekucji cutscenkowych, by wyeksponować kwestie głosowe aktorów i mięsiste efekty SFX.
- Dodano pierwszą uniwersalną ścieżkę bitewną (`Universal_Battle_Theme_01.mp3`, 4:04, 5.74 MB) – epicki orkiestrowy utwór z chórem i potężnymi bębnami.

---

## Wpis 4: Od proceduralnych brył do AAA — zarządzanie długiem wizualnym Three.js

### 1. Prześwietlenie prototypu silnika
W fazie szybkiego prototypowania mechanik gry wiele elementów powstało jako proceduralne geometrie Three.js (walce, stożki, prostopadłościany) tworzące prowizoryczne bronie, cokoły i scenografię. Twórca przekazał pełne zestawienie miejsc w kodzie (`pieceBuilder.ts`, `queenCutsceneDirector.ts`, `ChessSceneManager.ts`), które czekają na podmianę na profesjonalne modele 3D.

### 2. Rola Architekta: Zabezpieczenie ciągłości wiedzy
Prawdziwy architekt projektu nie gubi takich ustaleń na czacie. Informacje zostały natychmiast skodyfikowane w oficjalnym dokumencie technicznym `docs/ROADMAP_ASSETOW_3D.md`:
- Podział na 5 obszarów assetów z identyfikatorami zmiennych z silnika.
- Ustalenie ścisłej hierarchii priorytetów (P1: Bronie i tarcze, P2: Cokoły i nakrycia rang, P3: Rekwizyty egzekucji Hetmana, P4: Otoczenie areny).
- Zdefiniowanie specyfikacji technicznej dla przyszłych plików GLB (punkty obrotu pivot, budżet poligonów, standard skali 1:1).

Dzięki temu w kolejnych etapach prac żaden proceduralny element nie zostanie pominięty, a gra płynnie przekształci się z funkcjonalnego prototypu w dopracowaną produkcję.

---

## Wpis 5: Headless Blender w służbie vibecodingu — automatyczny Rigging, Skinning i Sockety

### 1. Dylemat twórcy: Koszty auto-riggingu w AI generatorach
Generatory takie jak Tripo.AI pobierają dodatkowe kredyty lub wysokie opłaty za rigging modeli, a dodatkowo generują surowe pliki o monstrualnej gęstości (nawet 500 000 trójkątów na prostą postać i 15 MB wagi), pozbawione punktów montażowych pod ekwipunek. Twórca zadał kluczowe pytanie:
> *„Czy sam masz możliwość implementacji np. Blendera, żeby zająć się tym problemem za mnie? (...) Wolę, żebyś całą pracę ze szkieletowaniem wykonał w blenderze za mnie, bo Tripo skasuje mnie za auto-rigging.”*

### 2. Architekt wkracza do akcji: Bezzałogowy pipeline 3D
Agent zainstalował w tle **Blendera 4.2 LTS** i napisał skrypt Python do masowego przetwarzania assetów glTF:
1. **Humanoid Rigging:** Dla każdej z 10 frakcji wygenerowano anatomię 19 kości humanoid (miednica, kręgosłup, klatka, szyja, głowa, ręce, nogi, stopy).
2. **Smooth Distance Skinning:** Opracowano odporny na geometrię non-manifold algorytm przypisywania wag wierzchołków do segmentów kości, gwarantujący deformację siatek bez błędów.
3. **Wstrzykiwanie Socketów:** Automatycznie zakotwiczono obiekty Empty (`Socket_Crown`, `Socket_Hand_R`, `Socket_Hand_L`, `Socket_Back` na postaciach oraz `Socket_Rider` w siodle konia i na wieży).
4. **Drastyczna optymalizacja (Decimate):** Każdy model zredukowano z 500k ścianek do 20k, zmniejszając wagę plików z ~15 MB do ok. 1.3 MB (cały pakiet zredukowany ze 150 MB do zaledwie 17 MB!).

---

## Wpis 6: Pierwsza partia oręża — wdrożenie dedykowanego uzbrojenia ról specjalnych

### 1. Przejście od teorii do praktyki
Po ustaleniu mapy drogowej (`docs/ROADMAP_ASSETOW_3D.md`) twórca wygenerował w Tripo.AI pierwszą partię 6 dedykowanych modeli z Priorytetu P1:
- `miecz_krola.glb` i `berlo.glb` (Król),
- `sztylet_krolowa.glb` (Królowa / Hetman),
- `kopia.glb` i `puklerz.glb` (Skoczek),
- `kostur_gonca.glb` (Goniec).

### 2. Automatyczna kalibracja punktów chwytu (Grip Origin)
Pliki pobrane bezpośrednio z Tripo miały domyślnie punkt zerowy na spodzie geometrii (`Z = 0`), co spowodowałoby, że dłoń postaci trzymałaby miecz za czubek głowicy, a puklerz za dolną krawędź.
Headless Blender w locie:
- Obliczył środek geometryczny i przesunął rękojeści miecza, sztyletu, berła, kopii i kostura dokładnie w oś `(0, 0, 0)` na wysokości chwytu dłoni,
- Wypoziomował wewnętrzny uchwyt puklerza na `Y = 0` z centrowaniem `X, Z = 0`,
- Wyeksportował perfekcyjnie skalibrowane modele prosto do silnika gry.

---

### 7. Lekcja z vibecodingu
> **Wniosek:** AI asystent nowej generacji nie zatrzymuje się na pisaniu kodu tekstowego. Gdy pojawia się wąskie gardło budżetowe lub manualne (jak rigging siatek 3D czy kalibracja pivotów), agent przejmuje stery nad profesjonalnymi narzędziami inżynieryjnymi (Headless Blender), wykonując w tle godziny żmudnej pracy 3D artisty w kilkadziesiąt sekund. Zgrany tandem człowiek-AI pozwala w jeden wieczór zamknąć etapy produkcji, które dawniej wymagały całego studia deweloperskiego.
