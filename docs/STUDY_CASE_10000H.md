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

## Wpis 7: Luksusowa arena z onyksu i marmuru — kalibracja szachownicy (plansza.glb)

### 1. Krok ku immersji wizualnej
Dotychczasowa arena opierała się na proceduralnej geometrii generowanej w locie przez kod `ChessSceneManager.ts` (proste kafelki Three.js). Twórca dostarczył wysokiej klasy model 3D: `luxury_onyx_and_marble_chess_board.glb` – rzeźbioną planszę łączącą polerowany czarny onyks, biały marmur oraz zdobioną mosiężną ramę.

### 2. Wyzwanie architektoniczne: Geometria vs Silnik Gry
W modelach 3D wymiary siatki pól rzadko pokrywają się z matematyką logiki gry:
- W silniku BloodChess każde z 64 pól szachownicy ma dokładnie szerokość **1.15 m** (cała siatka $8 \times 8$ to **9.20 m**).
- Płaszczyzna gry, po której stąpają figury, musi znajdować się dokładnie na wysokości **$Y = 0$** ($Z = 0$ w Blenderze).
Oryginalny model posiadał pole o szerokości 0.445 m, a powierzchnia kafelków znajdowała się na wysokości $Z = 0.152\text{ m}$. Bez korekty figury zapadałyby się w marmur lub lewitowały nad stołem, a pola nie pokrywałyby się ze współrzędnymi ruchów logicznych szachów.

### 3. Zautomatyzowana interwencja w Blenderze Headless
Agent przeprowadził matematyczną kalibrację assetu w skrypcie Python:
1. **Precyzyjne skalowanie:** Zastosowano współczynnik skali $2.584836$, idealnie dopasowując szerokość pojedynczego pola do $1.15\text{ m}$ (rozpiętość samej siatki gry $8 \times 8$ wynosi dokładnie $9.20\text{ m}$, a całości z obramowaniem $9.74\text{ m}$).
2. **Niwelacja płaszczyzny gry:** Wierzch marmurowych kafelków przesunięto o $-0.152108\text{ m}$, ustawiając płaszczyznę stóp figur idealnie na $Y = 0$.
3. **Punkty referencyjne silnika:** Dodano precyzyjne węzły Empty: `Board_Center` w $(0, 0, 0)$, `Tile_A1_Corner` w $(-4.60, -4.60, 0)$ oraz `Tile_H8_Corner` w $(4.60, 4.60, 0)$, umożliwiające silnikowi natychmiastowe kotwiczenie logiki raycastingu i przemieszczania bierek.

Wyeksportowano gotowy do użycia model `modeleBC/plansza.glb` (oraz alias `luxury_onyx_and_marble_chess_board.glb`) w standardzie glTF 2.0 PBR.

---

## Wpis 8: Armia Ogólna i Wizualny Przełom — wdrożenie zestawu ról, nakryć głowy, cokołu i mocy specjalnej

### 1. Pakiet zasobów z linii frontu
Twórca przekazał kolejny bogaty pakiet assetów (`bronie2`), zamykający dwie kluczowe luki w prototypie silnika:
- **Wyposażenie ról specjalnych:** lewa ręka Gońca (`kielich_gonca.glb`), prawa ręka Wieży (`mlot_wiezy.glb`) oraz lewa ręka Wieży (`pawez_wiezy.glb`).
- **Identyfikacja hierarchii figur:** rzeźbiony kamienny cokół bitewny (`podstawka.glb`) oraz dedykowane nakrycia głowy (`czepiec_wiezy.glb`, `czapka_gonca.glb`, `kita_skoczka.glb`).
- **Nowa mechanika rozgrywki — Efekt Mocy Specjalnej:** animowany słup energetyczny VFX (`specialpower.glb`), tworzący uniwersalną bazę pod przyszłe unikalne moce frakcyjne.
- **Arsenał broni frakcyjnych:** zdeponowano i zinwentaryzowano broń dla kolejnego etapu (topory wikingów, karabin Springfield, rewolwer, Tommy Gun, zakrwawiona maczuga).

### 2. Wyzwania inżynieryjne: Ukryte macierze, skala i optymalizacja
Surowe modele pochodzące z różnych bibliotek charakteryzowały się drastycznie odmiennymi układami odniesienia:
1. **Cokół bitewny (drastyczna optymalizacja wagi):** Model podstawki posiadał aż 124 644 ścianek (5.1 MB) i środek geometryczny przesunięty o -26.7 m. Headless Blender wycentrował bryłę w `(0, 0)`, osadził spód idealnie na `Z = 0`, przeskalował średnicę do `0.95 m` (pod pole szachowe `1.15 m`) oraz zastosował modyfikator Decimate, zmniejszając polycount do 4 361 ścianek i wagę pliku do zaledwie **246 KB** (redukcja o ponad 95%).
2. **Ukryte hierarchie w pawęży:** Płyta tarczy posiadała w węzłach pośrednich skalę $100\times$, a rzemienie uchwytu $0.0347\times$. Agent zaimplementował funkcję `bake_mesh_transforms`, wypiekającą przekształcenia bezpośrednio do geometrii świata, a następnie wycentrował wewnętrzny uchwyt w `(0, 0, 0)` na wysokości dłoni `Socket_Hand_L`.
3. **Kielich i Młot:** Wyzerowano punkty chwytu (`Grip Origin`) na nóżce kielicha oraz rękojeści młota (`Grip`), eliminując lewitowanie lub zniekształcenia chwytu.
4. **Animowany słup energii (VFX):** Przeskalowano efekt z 0.54 m do 2.10 m (aby otaczał postać o wzroście 1.8 m), zachowując wszystkie 4 zintegrowane ścieżki animacji glTF (`Take 001`).

Dzięki temu cała hierarchia armii ogólnej (Król, Królowa, Skoczek, Goniec, Wieża) dysponuje kompletnym zestawem uzbrojenia, pancerza i nakryć głowy w formacie glTF 2.0.

---

## Wpis 9: Pierwsza filmowa egzekucja Hetmana — choreografia takedownu Horda vs Syndykat (cutscenka w Blenderze & Three.js)

### 1. Wizja Twórcy i Cel: Podgląd przed wdrożeniem
W myśl nadrzędnej zasady projektowania gry, Twórca zgłosił zapotrzebowanie na przetestowanie i weryfikację wizualną pełnej sceny zabicia figury (takedownu) **zanim** kod Three.js zacznie przetwarzać ją w czasie rzeczywistym.
Scenariusz testowy: **Zombie Hordy** dokonuje brutalnej egzekucji na **Hetmanie Syndykatu** (eleganckiej kobiecie w garniturze z koroną i sztyletem) na nowo wdrożonej marmurowej szachownicy z onyksu.

### 2. Wyzwania inżynieryjne w Headless Pipeline:
1. **Niewidzialność materiałów z importera FBX (Alpha = 0):**
   Standardowy importer FBX w Blenderze 4.2 LTS po zaimportowaniu materiałów Principled BSDF ustawia domyślnie suwak `Alpha` na `0.0`. Powodowało to całkowitą przezroczystość postaci w silniku EEVEE Next. Agent zaimplementował w locie automatyczny skrypt naprawczy przechodzący po `bpy.data.materials` i korygujący `Alpha = 1.0` oraz tryb miksowania na `OPAQUE`.
2. **Kompilacja wielościeżkowego Non-Linear Animation (NLA):**
   Zamiast statycznych póz, zaaranżowano pełną choreografię filmową (105 klatek, 24 fps):
   - **Klatki 1–24:** Szarża Zombie w stronę Hetmana (`Run`), Hetman stoi niewzruszona (`Idle`).
   - **Klatki 25–40:** Potężny cios pięścią Zombie prosto w twarz/korpus (`Punch`), natychmiastowa reakcja Hetmana na uderzenie (`RecieveHit`).
   - **Klatki 41–105:** Śmiertelne osuwanie się Hetmana i bezwładny upadek na marmurowe kafle (`Death`), podczas gdy Zombie unosi ramiona ku niebu w dzikim ryku triumfu (`Victory`).
3. **Dynamiczna kamera i oświetlenie filmowe:**
   Skonfigurowano kamerę 28mm z constraintem `TRACK_TO` śledzącym epicentrum starcia, z miękkim oświetleniem punktowym z góry i kontrowym światłem chłodnym, podkreślającym luksusowe żyłki marmuru i dramatyzm sceny.

### 3. Rezultat i Artefakty
Wygenerowano dwa kluczowe zasoby gotowe do natychmiastowego użycia:
- **`modeleBC/horda_bije_hetmana_cutscene.mp4`** – Wyrenderowane wideo MP4 (H.264, 24 fps, 854x480), dające Twórcy 100% pewność co do tempa, dramaturgii i kompozycji uderzenia.
- **`modeleBC/takedown_horda_syndykat.glb`** (9.8 MB) – Kompletna, animowana scena 3D glTF z siatkami, kośćmi i ścieżkami NLA, którą silnik WebGL gry może natychmiast odtworzyć w Three.js jako interaktywną cutscenkę.

---

## Wpis 10: Anatomiczna kalibracja skal bierek w silniku — od Goblinów (70 cm) po Wikingów (215 cm) oraz rozwiązanie zagadki przysiadu Ninja

### 1. Diagnoza wizualna: Pułapka normalizacji modeli AI
Wszystkie surowe assety wygenerowane przez Tripo.AI zostały domyślnie znormalizowane do identycznej wysokości wierzchołkowej $1.00\text{ m}$ (100 cm). Po zaimportowaniu ich do silnika ze stałym mnożnikiem skali pojawiły się kuriozalne dysproporcje:
- **Goblin:** mający w założeniach fabularnych zaledwie 70 cm wzrostu, w silniku miał rozmiary dorosłego człowieka (~180 cm)!
- **Wiking:** potężny barbarzyńca o wzroście 215 cm wyglądał na przysadzistego i mniejszego od żołnierzy.
- **Ninja:** kluczowy problem biomechaniczny – model został wygenerowany w głębokim przysiadzie bojowym (*kiba-dachi*, rozstaw stóp 0.84 m, ugięcie kolan ~40°). Proste przeskalowanie go do 175 cm sprawiłoby, że po wyprostowaniu miałby ponad 2.07 m wzrostu, a jego głowa i dłonie byłyby karykaturalnie wielkie!

### 2. Matematyczne opracowanie geometrii przysiadu Ninja
Agent przeprowadził dekonstrukcję łańcucha kostnego i siatki wierzchołków:
1. Dla człowieka o wzroście wyprostowanym 175 cm:
   - Nogi (od podłoża do panewki miednicy): ~85 cm,
   - Tułów + głowa: ~90 cm.
2. W szerokim rozstawie stóp (0.84 m) i ugięciu kolan o 40°:
   - Wysokość miednicy obniża się z 85 cm do ~60 cm (spadek o 25 cm).
   - Lekkie pochylenie tułowia w pozie szermierczej skraca rzut pionowy o kolejne ~8 cm.
   - Prawdziwy wzrost wojownika w tym przysiadzie wynosi **142 cm** (1.42 m).
3. Wyznaczenie mnożnika dla modelu:
   - Model `klan.glb` ma bazową wysokość siatki $0.9614\text{ m}$.
   - Aby proporcje anatomiczne (wielkość czaszki, długość rąk, szerokość klatki) odpowiadały człowiekowi o wzroście 175 cm, model musi zostać przeskalowany o współczynnik:
     $$\text{Scale} = \frac{1.42\text{ m}}{0.9614\text{ m}} \approx \mathbf{1.48}$$
   Dzięki temu stojąc w przysiadzie, jego głowa znajduje się na poziomie 1.42 m, a jego ciało ma idealnie naturalne proporcje w zestawieniu z resztą armii!

### 3. Weryfikacja w Headless Blenderze i aliasy plików
- Wyrenderowano wzorcową planszę porównawczą `modeleBC/proponowane_skale_studio.png` z liniami odniesienia wysokości (0.70 m – 2.15 m).
- Zarejestrowano pełną tabelę skal metrycznych oraz znormalizowanych do wdrożenia w kodzie Three.js Studio.
- Utworzono aliasy nazw angielskich (`vikings.glb`, `crusaders.glb`, `undead.glb`, etc.), gwarantując 100% kompatybilność z dowolną konwencją nazewniczą w silniku gry.

---

### Podsumowanie lekcji z vibecodingu
> **Wniosek:** AI asystent nowej generacji nie zatrzymuje się na pisaniu kodu tekstowego. Gdy pojawia się wąskie gardło budżetowe lub manualne (jak rigging siatek 3D czy kalibracja pivotów i wymiarów pól), agent przejmuje stery nad profesjonalnymi narzędziami inżynieryjnymi (Headless Blender), wykonując w tle godziny żmudnej pracy 3D artisty w kilkadziesiąt sekund. Zgrany tandem człowiek-AI pozwala w jeden wieczór zamknąć etapy produkcji, które dawniej wymagały całego studia deweloperskiego.
