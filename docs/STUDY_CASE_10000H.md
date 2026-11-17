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

### 3. Lekcja z vibecodingu
> **Wniosek:** Dojrzały asystent vibecodingu nie jest biernym wykonawcą poleceń typu „kopiuj-wklej”. Prawdziwa wartość pojawia się wtedy, gdy agent potrafi przeprowadzić inspekcję heksadecymalną nagłówków binarnych, wykryć anomalie w plikach i zabezpieczyć integralność projektu zanim jakikolwiek błąd trafi na produkcję.
