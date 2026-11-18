# Case Study: „Po 10 000 godzin vibecodingu jesteś programistą”
## Oficjalny Rejestr Postępów i Decyzji Architektonicznych Projektu BloodChess

> **O dokumencie:**  
> Niniejsze opracowanie stanowi narracyjny i techniczny zapis ewolucji projektu **BloodChess** – od luźnych plików FBX i dźwięków WAV na pulpicie, aż po w pełni funkcjonalną grę bitewną 3D z filmowymi egzekucjami Hetmana, zbalansowaną skalą postaci, dynamicznymi symbolami ról i kompletną areną lochów.  
> 
> Ze względu na optymalizację czasu przetwarzania przez silniki AI i narzędzia deweloperskie (Studio), pełna treść studium przypadku została podzielona na modułowe tomy tematyczne.

---

## Spis Tomów i Rejestr Wpisów

### [Tom 1: Fundamenty, Modele Humanoidów i Headless Rigging (Wpisy 1–5)](study_case/tom_1_fundamenty_i_rigging.md)
*Fundamenty strukturalne projektu, unifikacja assetów GLB, orkiestracja audio i automatyzacja riggingu w Blenderze.*
- **Wpis 1:** Od luźnych plików na pulpicie do ustrukturyzowanego silnika bitewnego gry „BloodChess”.
- **Wpis 2:** Dedykowane modele frakcyjne GLB i detektywistyczna naprawa uszkodzonych assetów (`.tmp` $\to$ `.glb`).
- **Wpis 3:** Dynamiczna orkiestracja bitwy — architektura systemu ścieżki dźwiękowej (`Soundtrack/`).
- **Wpis 4:** Od proceduralnych brył do AAA — zarządzanie długiem wizualnym Three.js i Backlog assetów.
- **Wpis 5:** Headless Blender w służbie vibecodingu — automatyczny Rigging (19 kości), Skinning i gniazda ekwipunku (Sockets).

### [Tom 2: Figury, Uzbrojenie Ról, Animacje Takedownów i Skala (Wpisy 6–10)](study_case/tom_2_figury_animacje_i_skala.md)
*Kompletowanie uzbrojenia, marmurowo-onyksowa plansza, animacje filmowych egzekucji oraz anatomiczna kalibracja wzrostu.*
- **Wpis 6:** Pierwsza partia oręża — wdrożenie dedykowanego uzbrojenia ról specjalnych (miecz, berło, sztylet, lanca, kostur, kielich, młot, pawęż).
- **Wpis 7:** Luksusowa arena z onyksu i marmuru — kalibracja szachownicy (`plansza.glb`) pod siatkę pól $1.15\text{ m}$.
- **Wpis 8:** Armia Ogólna i Wizualny Przełom — wdrożenie zestawu nakryć głowy ról, cokołu pod figury i aury mocy specjalnej (`specialpower.glb`).
- **Wpis 9:** Pierwsza filmowa egzekucja Hetmana — choreografia takedownu Horda vs Syndykat (reżyseria kamer i animacji NLA).
- **Wpis 10:** Anatomiczna kalibracja skal bierek w silniku — proporcje od Sabatu Goblinów ($70\text{ cm}$) po Wikingów ($215\text{ cm}$) oraz rozwiązanie zagadki przysiadu Ninja.

### [Tom 3: Symbole Szachowe 3D, Standard Interakcji i Arena Lochów (Wpisy 11–16)](study_case/tom_3_symbole_interakcja_i_sceneria.md)
*Identyfikacja bierek w 3D, ergonomia Double-Tap na telefonach oraz budowa monumentalnej scenerii lochów.*
- **Wpis 11:** Trójwymiarowe runy rangowe bierek — generowanie lewitujących symboli Unicode (glTF PBR) z dynamicznym barwieniem 10 frakcji.
- **Wpis 12:** Standard interakcji Double-Tap (PC & Mobile), rygor zablokowanej kamery meczowej i warunkowa asysta trudności (Easy).
- **Wpis 13:** Opracowanie oświetlenia scenografii – Koksownik bojowy, animowany ogień (192 meshe płomieni) i kompozycja 4 narożników.
- **Wpis 14:** Budowa modularnej areny lochów (Dungeon Arena) – Dwustronne kamienne schody, koksowniki w rogach i powiewające sztandary heraldyczne.
- **Wpis 15:** Korekta przestrzenna areny lochów – Diagnoza błędu rotacji Quaternion i uwolnienie pola widzenia szachownicy ($X = \pm 10.50\text{ m}$).
- **Wpis 16:** Zabudowa podmurówki szachownicy, pionowanie wielkich sztandarów heraldycznych oraz czarny rant PBR symboli 3D.

---

## Kluczowe Wnioski i Manifest Vibecodingu

> [!TIP]
> **Główna lekcja inżynieryjna:**  
> AI asystent nowej generacji nie zatrzymuje się na pisaniu kodu tekstowego. Gdy pojawia się wąskie gardło budżetowe lub manualne (jak rigging siatek 3D, generowanie geometrii z glifów czy kalibracja pivotów i wymiarów pól), agent przejmuje stery nad profesjonalnymi narzędziami inżynieryjnymi (Headless Blender), wykonując w tle godziny żmudnej pracy 3D artisty w kilkadziesiąt sekund. Zgrany tandem człowiek-AI pozwala w jeden wieczór zamknąć etapy produkcji, które dawniej wymagały całego studia deweloperskiego.
