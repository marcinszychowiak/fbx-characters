# Study Case: Po 10 000 godzin vibecodingu jesteś programistą
## Tom 3: Symbole Szachowe 3D, Standard Interakcji i Arena Lochów (Wpisy 11–15)

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
