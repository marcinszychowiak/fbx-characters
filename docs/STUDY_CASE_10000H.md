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

## Wpis 11: Trójwymiarowe runy rangowe bierek — generowanie lewitujących symboli Unicode (glTF PBR) z dynamicznym barwieniem frakcyjnym

### 1. Geneza potrzeby UX: Natychmiastowa czytelność na polu bitwy
W grze z 10 unikalnymi armiami i 60 zróżnicowanymi modelami wojowników natychmiastowa identyfikacja roli szachowej (Król, Hetman, Wieża, Goniec, Skoczek, Pion) w ferworze walki jest kluczowa dla komfortu gracza.
Twórca zaproponował genialny w swej prostocie mechanizm: **po kliknięciu danej bierki, nad jej głową pojawia się trójwymiarowy, obracający się i lewitujący symbol szachowy w barwach przynależnej armii**.

### 2. Realizacja w Headless Blenderze (Vector Font to 3D PBR Mesh):
Agent natychmiast przekształcił wektorowe glify Unicode z systemowej biblioteki krojów pisma (`Segoe UI Symbol` U+265A do U+265F) w pełnoprawne, zoptymalizowane bryły 3D:
1. **Modelowanie i Bevel:** Każdemu symbolowi nadano grubość 4 cm oraz 3-stopniowe fazowanie krawędzi (Bevel), dzięki czemu symbole chwytają refleksy światła i prezentują się jak szlachetne insygnia królewskie.
2. **Kalibracja pivotu i skali:**
   - Wysokość każdego znaku znormalizowano precyzyjnie do **0.40 m** (40 cm) – idealnej proporcji nad głowę figury.
   - Środek ciężkości (Origin) wycentrowano idealnie w geometrycznym środku `(0, 0, 0)`, umożliwiając bezproblemową rotację wokół własnej osi bez efektu bicia czy mimośrodu.
3. **Materiały PBR zoptymalizowane pod Three.js:** Nadano materiał metaliczny z emisyjnym blaskiem, który w silniku gry może być dynamicznie barwiony jednym poleceniem (`material.color.setHex(armyColor)` / `material.emissive.setHex(armyColor)`).

### 3. Wdrożenie i Artefakty
Wyeksportowano zestaw modeli do `modeleBC/`:
- `symbol_krol.glb` (Król), `symbol_hetman.glb` (Hetman), `symbol_wieza.glb` (Wieża), `symbol_goniec.glb` (Goniec), `symbol_skoczek.glb` (Skoczek), `symbol_pion.glb` (Pion) oraz paczkę zbiorczą `symbole_szachowe_3d.glb`.
- Wyrenderowano planszę poglądową `modeleBC/showcase_symbole_szachowe_3d.png` prezentującą symbole w pełnej palecie frakcyjnej (złoto, karmazyn, szmaragd, szafir, ametyst, bursztyn).
- Opracowano gotowy moduł TypeScript do obsługi kliknięcia, lewitacji i rotacji w Three.js.

---

## Wpis 12: Standard interakcji Double-Tap (PC & Mobile), rygor kamery meczowej i warunkowa asysta trudności (Easy)

### 1. Przełom w ergonomii: Unifikacja PC i Mobile (Double-Tap)
Twórca podjął kluczową decyzję projektową dotyczącą interfejsu: **zarówno na komputerze (myszka), jak i na telefonie (ekran dotykowy) obowiązuje identyczny, dwuetapowy model interakcji (*Double-Tap / Two-Click*)**:
- **Pierwszy tap:** Czysta inspekcja i przygotowanie – dotknięcie własnej bierki podnosi nad nią lewitujący symbol 3D w kolorze armii i podświetla legalne ruchy. Dotknięcie wrogiej bierki podnosi jej symbol 3D w barwach wroga i **nigdy nie powoduje przypadkowego ruchu ani straty figury**.
- **Drugi tap:** Potwierdzenie intencji – dotknięcie podświetlonego kafelka / wrogiej figury w zasięgu aktywuje ruch lub animację takedownu.

### 2. Balans rozgrywki: Zasięg rażenia wroga (Threat Range) wyłącznie w Easy Mode
Częstym problemem w grach szachowych jest przeciążenie wzrokowe gracza zbyt dużą liczbą podpowiedzi. Zgodnie z wytyczną Twórcy:
- **Tryb Łatwy (Easy vs SI):** Po kliknięciu wrogiej bierki plansza podświetla na czerwono pola, które ta jednostka aktualnie kontroluje (świetna asysta dla początkujących).
- **Tryb Normalny, Trudny i PvP:** Podświetlenie zagrożeń wroga jest zablokowane. Gracz widzi symbol 3D roli (rozwiewający wątpliwość np. Goniec vs Pion), lecz pełną kalkulację taktyczną musi przeprowadzić samodzielnie.

### 3. Sztywna blokada kamery meczowej (Locked Camera Rig)
Na urządzeniach mobilnych obracanie kamery gestem dotykowym w trakcie partii prowadzi do frustrujących pomyłek (obrót sceny zamiast kliknięcia pionka).
Wprowadzono dedykowany rig kamery:
- Po rozpoczęciu meczu kontrolery orbitalne (*OrbitControls*) zostają wyłączone na czas partii.
- Kamera przyjmuje stały, panoramiczny kąt taktyczny ($FOV = 42^\circ$, `position: (0, 7.8, 8.2)`, `lookAt: (0, 0, -0.4)` dla Białych; obrót $180^\circ$ dla Czarnych), obejmujący w pełni całą planszę $9.20\text{ m} \times 9.20\text{ m}$ z idealnym zachowaniem czytelności figur.

Wszystkie te wytyczne wraz z gotową klasą `BloodChessInputController` zostały skompilowane w dedykowany dokument produkcyjny: `docs/INSTRUKCJA_STUDIO_INTERAKCJA_KAMERA.md`.

---

## Wpis 13: Opracowanie oświetlenia scenografii – Koksownik bojowy, animowany ogień (192 meshe) i kompozycja 4 narożników

### 1. Cel: Bitewna atmosfera areny szachowej
Szachownica BloodChess ($9.20\text{ m} \times 9.20\text{ m}$) potrzebowała klimatycznego oświetlenia otoczenia nawiązującego do mrocznej sali zamkowej / cytadeli. Twórca dostarczył surowe modele koksownika oraz wieloczęściowego ognia (`c:\Users\sbard\Downloads\bronie2`).

### 2. Wyzwania inżynieryjne i kalibracja geometrii
- **Koksownik (`koksownik.glb`):**
  - Model składa się z solidnego kamiennego cokołu z pęknięciami (`Object_5`) oraz kutej, mosiężnej misy ze zwieńczeniem (`Object_4`).
  - Surowy plik ze Sketchfab posiadał nadrzędny węzeł z niezerową skalą ($0.2326$). Po uwolnieniu relacji rodzic-dziecko (`CLEAR_KEEP_TRANSFORM`) i wypieczeniu transformacji siatki osadzono spód podstawy idealnie na $Z = 0.00\text{ m}$.
  - Wymiary: podstawa o szerokości $0.79\text{ m}$, wysokość cokołu $1.145\text{ m}$, całkowita wysokość misy $1.413\text{ m}$.
  - W centrum misy osadzono punkt pomocniczy `Socket_Flame` na wysokości $Z = 1.22\text{ m}$.
- **Animowany ogień (`ogien_do_koksownika.glb`):**
  - Ogień składa się ze 192 niezależnych, animowanych siatek płomieni i iskier w zapętlonej akcji 30 klatek.
  - W skali 1:1 ogień miał aż $2.08\text{ m}$ średnicy i $2.73\text{ m}$ wysokości (zbyt potężny do koksownika).
  - Skalibrowano skalę do `0.235` (średnica płomienia $\approx 0.49\text{ m}$, idealnie wpasowana w misę $0.50\text{ m}$).
  - Skonfigurowano węzeł `Flame_Root` z przesunięciem $Z$, dzięki czemu punkt zaczepienia ognia znajduje się dokładnie na jego dolnej krawędzi $(0, 0, 0)$.
  - Materiał `fire` otrzymał wzmocnioną emisję PBR (Emission Strength: 5.0, barwa soczystego pomarańczu/złota).
- **Zintegrowany asset (`koksownik_z_ogniem.glb`):**
  - Gotowy do natychmiastowego wstawienia do Three.js model 2w1 o całkowitej wysokości $1.86\text{ m}$, z płomieniem tańczącym $0.45\text{ m}$ ponad krawędzią misy.

### 3. Zastosowanie w grze (Three.js / Studio):
W 4 rogach planszy poza krawędzią pól ($X, Z = \pm 5.20\text{ m}$):
- `Corner_TopLeft`: `(-5.20, 0, -5.20)`
- `Corner_TopRight`: `(5.20, 0, -5.20)`
- `Corner_BottomLeft`: `(-5.20, 0, 5.20)`
- `Corner_BottomRight`: `(5.20, 0, 5.20)`
W każdym koksowniku na wysokości $Z = 1.38\text{ m}$ silnik Three.js umieszcza `PointLight` o ciepłej barwie `0xff7722`, tworząc dynamiczne cienie figur na marmurowo-onyksowej planszy.

---

## Wpis 14: Budowa modularnej areny lochów (Dungeon Arena) – Dwustronne kamienne schody, koksowniki w rogach i powiewające sztandary heraldyczne

### 1. Cel: Monumentalna sala bitewna w klimacie lochów
Zgodnie z wizją Twórcy szachownica BloodChess ($9.20\text{ m} \times 9.20\text{ m}$, platforma $10.40\text{ m} \times 10.40\text{ m}$) stanowi centralne, wyniesione podium bitewne. Zadaniem Architekta było stworzenie kompletnego, zintegrowanego środowiska 3D w oparciu o surowe assety z folderu oczekujących (`schody.glb`, `sztandar.glb`, `lochy_set.glb`):
1. **Dwustronne kamienne schody** prowadzące na szachownicę z obu stron:
   - Dla Białych (Rank 1 / Południe): opadające ku południowemu wejściu do lochów,
   - Dla Czarnych (Rank 8 / Północ): opadające ku północnemu wejściu do lochów.
2. **Koksowniki bojowe z animowanym ogniem** w 4 rogach platformy planszy.
3. **Mroczne otoczenie lochów** z modułowych murów kamiennych (części pełne oraz z gotyckimi oknami), monumentalnymi portalami łukowymi i filarami wsporczymi.
4. **Powiewające sztandary na ścianach (tuż za koksownikami)** – 4 sztandary z animacją kości, o neutralnej strukturze czystego płótna, przygotowane pod dynamiczne kolorowanie PBR barwami 10 frakcji oraz projekcję symboli bierek w Three.js.

### 2. Wyzwania inżynieryjne i kalibracja przestrzenna
- **Matematyczne dokowanie schodów (`schody.glb`):**
  - Model kamiennych schodów z balustradami i łańcuchami ma szerokość $5.20\text{ m}$, długość biegu $7.135\text{ m}$ i spadek wysokości $3.00\text{ m}$.
  - Wycentrowano oś poprzeczną $X$ do przedziału $[-2.60\text{ m}, +2.60\text{ m}]$, a górny podest wyrównano idealnie do poziomu planszy ($Z = 0.00\text{ m}$).
  - Schody Białych osadzono przy $Y = -5.20\text{ m}$ z zejściem na południe ku $Y = -12.34\text{ m}$ ($Z = -3.00\text{ m}$).
  - Schody Czarnych obrócono o $180^\circ$ i osadzono przy $Y = +5.20\text{ m}$ z zejściem na północ ku $Y = +12.34\text{ m}$ ($Z = -3.00\text{ m}$).
  - Przestrzeń samej szachownicy pozostała w $100\%$ wolna i niezasłonięta.
- **Modułowa architektura lochów (`lochy_set.glb`):**
  - Wyizolowano poszczególne elementy modułowego zestawu: mur pełny ($13.18\text{ m}$), mur z oknem gotyckim ($13.18\text{ m}$), monumentalną bramę z łukiem ($13.18\text{ m}$), filary narożne ($1.52\text{ m} \times 11.02\text{ m}$) oraz płyty posadzkowe ($12.3\text{ m} \times 12.3\text{ m}$).
  - Ściany boczne (wschodnia i zachodnia) odsunięto na bezpieczny dystans $X = \pm 8.50\text{ m}$, tworząc przestronną galerię wokół planszy.
  - Na krańcach schodów ($Y = \pm 13.50\text{ m}$) postawiono potężne bramy łukowe, tworząc bramy wejściowe dla obu armii.
  - Posadzka dolna sali została ułożona na poziomie $Z = -3.25\text{ m}$ (powierzchnia na $-3.00\text{ m}$), idealnie stykając się z najniższym stopniem schodów.
- **Sztandary heraldyczne z animacją kości (`sztandar.glb`):**
  - Surowy asset zawierał 10-kościowy szkielet animowany w pętli 60 klatek (`Banner_BonesAction_Object_6`) oraz zbędną siatkę `Icosphere`, która została usunięta.
  - Wykalibrowano skalę do `0.0035` (szerokość $0.94\text{ m}$, długość zwisu $4.14\text{ m}$).
  - Obrócono szkielet o $90^\circ$ w osi X, aby płótno wisiało pionowo wzdłuż muru.
  - 4 sztandary zawieszono na wysokości $Z = 4.80\text{ m}$ bezpośrednio za koksownikami na ścianach bocznych ($X = \pm 8.35\text{ m}$, $Y = \pm 5.20\text{ m}$).
  - Płótno zwisa do $Z \approx 0.73\text{ m}$, kąpiąc się w blasku ognia z koksowników ($Z = 1.45\text{ m}$).

### 3. Nowe assety produkcyjne w `modeleBC/`
1. `modeleBC/sceneria_lochy.glb` – Zintegrowana, zoptymalizowana arena lochów 3D gotowa do wczytania jednym wywołaniem `GLTFLoader` w Three.js (szachownica, 2x schody, 4x koksowniki, mury, bramy, filary, posadzka, 4x sztandary).
2. `modeleBC/schody.glb` – Samodzielny, wycentrowany model kamiennych schodów ze zoptymalizowanym pivotem na krawędzi górnego podestu.
3. `modeleBC/sztandar.glb` – Samodzielny model powiewającego sztandaru ze szkieletem i zapętloną animacją wiatru.
4. Prezentacje wizualne:
   - `modeleBC/preview_arena_lochy_mecz.png` – Kadr zablokowanej kamery meczowej (panoramiczny rzut taktyczny z góry).
   - `modeleBC/preview_arena_lochy_biale.png` – Widok od dołu południowych schodów Białych patrząc w górę na arenę.
   - `modeleBC/preview_arena_lochy_detal.png` – Cinematic zbliżenie: ogień koksownika, kamienny mur i powiewający sztandar.

---

## Wpis 15: Korekta przestrzenna areny lochów – Diagnoza trybu obrotu Quaternion i uwolnienie pola widzenia szachownicy

### 1. Problem zgłoszony przez Twórcę
Po wstępnym wygenerowaniu scenerii lochów Twórca słusznie zauważył:
> *"Ogólnie super, ale te ścianki tuż przy szachownicy zasłaniają planszę."*

Podczas inspekcji rzutu kamery meczowej okazało się, że boczne fragmenty kamiennego muru faktycznie wchodziły w pole widzenia narożnych pól planszy, przeszkadzając w komfortowej obserwacji rozgrywki i potencjalnie myląc graczy.

### 2. Śledztwo techniczne: Dlaczego mury weszły na planszę?
Analiza skryptowa w headless Blenderze ujawniła podwójną przyczynę:
1. **Ukryty tryb rotacji `QUATERNION` w zaimportowanym glTF:**
   Wszystkie siatki wyodrębnione z surowego `lochy_set.glb` miały ustawiony `rotation_mode = 'QUATERNION'`. Kiedy skrypt przypisywał `new_obj.rotation_euler = (0, 0, rot_z)`, Blender po cichu ignorował wartości Eulera, ponieważ obiekt był sterowany kwaternionem!
2. **Skutek w geometrii:**
   Mury boczne, które miały biec wzdłuż osi Y (długość $13.18\text{ m}$), pozostały zorientowane wzdłuż osi X ($dX = 13.18\text{ m}$, $dY = 1.54\text{ m}$). Z powodu umieszczenia ich na $X = \pm 8.50\text{ m}$, ich wierzchołki rozciągały się w przedziale $X \in [-15.09, -1.91]$ oraz $X \in [1.91, 15.09]$ – dosłownie tnąc planszę (która ma krawędź na $X = \pm 5.20\text{ m}$) aż do $X = \pm 1.91\text{ m}$!

### 3. Wprowadzone rozwiązanie inżynieryjne
Zastosowano bezkompromisową, pewną metodę rektyfikacji geometrii:
1. **Permanentna rotacja wierzchołków na poziomie siatki (Mesh Vertex Baking):**
   Zamiast polegać na rotacji kontenera obiektu, stworzono zrotowaną kopię siatki `make_rotated_copy()`, bezpośrednio obracając współrzędne wierzchołków ($x' = x \cos \alpha - y \sin \alpha$, $y' = x \sin \alpha + y \cos \alpha$). W ten sposób mur ma długość $13.18\text{ m}$ permanentnie wzdłuż osi Y bez potrzeby rotacji obiektu.
2. **Wymuszenie `rotation_mode = 'XYZ'`:**
   Wszystkim obiektom w scenie narzucono explicite kartezjański tryb Eulera.
3. **Odsunięcie ścian bocznych na $X = \pm 10.50\text{ m}$:**
   Mury zachodnie ($X = -10.50\text{ m}$) i wschodnie ($X = +10.50\text{ m}$) zostały odsunięte o dodatkowe $2.0\text{ m}$ na zewnątrz.
   - Pomiędzy krawędzią szachownicy ($X = \pm 5.20\text{ m}$) a wewnętrznym licem murów ($X = \pm 9.73\text{ m}$) powstał szeroki, monumentalny korytarz o szerokości ponad **$4.5\text{ m}$**.
   - Sztandary heraldyczne powieszono na ścianach na $X = \pm 9.70\text{ m}$, obrócone przodem do środka sali.
   - Koksowniki w 4 rogach ($X = \pm 5.35\text{ m}$, $Y = \pm 5.35\text{ m}$) płoną swobodnie na krawędzi podestu, nie dotykając żadnych ścian.
4. **Kalibracja kamery meczowej (`Cam_Match`):**
   Kamerę taktyczną ustawiono na $(0.0, -10.5, 11.2)$, z ogniskową $30\text{ mm}$ i śledzeniem środka planszy $(0, 0, 0.2)$.
   - Wszystkie 64 pola szachownicy (A1–H8) są w 100% widoczne, bez ani jednego cienia czy fragmentu muru w kadrze.
   - Gotyckie ściany i filary tworzą majestatyczne tło po bokach ekranu, budując głębię lochów bez naruszania czytelności gameplayu.

---

### Podsumowanie lekcji z vibecodingu
> **Wniosek:** AI asystent nowej generacji nie zatrzymuje się na pisaniu kodu tekstowego. Gdy pojawia się wąskie gardło budżetowe lub manualne (jak rigging siatek 3D czy kalibracja pivotów i wymiarów pól), agent przejmuje stery nad profesjonalnymi narzędziami inżynieryjnymi (Headless Blender), wykonując w tle godziny żmudnej pracy 3D artisty w kilkadziesiąt sekund. Zgrany tandem człowiek-AI pozwala w jeden wieczór zamknąć etapy produkcji, które dawniej wymagały całego studia deweloperskiego.
