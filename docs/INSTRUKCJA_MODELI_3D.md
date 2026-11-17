# Instrukcja przygotowania i dopasowania modeli 3D (`.glb`) — Krwawe Szachy 3D

Dokument definiuje standardy inżynieryjne przygotowywania modeli 3D dla silnika **BloodChess**, wyjaśnia przyczyny problemów z dopasowaniem elementów oraz określa procedury pracy w środowiskach **Blender** oraz generatorach AI (**Tripo.AI**).

---

## 1. Dlaczego obecne elementy nie zawsze idealnie pasują?

Wczesne pliki `.glb` (generowane jako surowe, scalone bryły AI) posiadają trzy ograniczenia geometryczne, których silnik Three.js nie jest w stanie automatycznie skorygować bez metadanych przestrzennych:

1. **Brak szkieletu (kościec / rigg):**  
   Pojedyncza sztywna siatka (`nodes: 1, skins: 0`) uniemożliwia zginanie kolan i bioder. Z tego powodu Skoczek stoi na grzbiecie konia, zamiast siedzieć w siodle z nogami po bokach.
2. **Brak punktów montażowych („Socketów”):**  
   Brak oznaczonych węzłów dłoni czy czaszki wymusza na silniku szacowanie pozycji korony z obwiedni całego modelu (`bounding box max.y`). Przy rogach hełmu (Wiking), uniesionym toporze lub pióropuszu korona unosi się w powietrzu nad najwyższym punktem zamiast na głowie.
3. **Wypalone bronie w jednej bryle:**  
   Część modeli posiada broń wtopioną w siatkę bazową, co powoduje kolizję przy próbie dodania broni proceduralnej lub dedykowanej.

---

## 2. Standard Przestrzeni i Skali w Silniku Gry

Niezależnie od narzędzia (Blender, Tripo.AI, skrypt automatyzacji), model musi spełniać poniższe reguły:

- **Format eksportu:** `glTF Binary (.glb)` (układ współrzędnych: **+Y Up**).
- **Punkt zerowy (Origin `0, 0, 0`):**
  - **Postać piesza, koń, wieża, podstawka:** środek podstawy `(X = 0, Z = 0)`, spód stóp / kopyt / cokołu dokładnie na ziemi `(Y = 0)`.
  - **Korona (`korona.glb`):** środek dolnej krawędzi obręczy dokładnie na `(0, 0, 0)`, wierzchołki ząbków skierowane w `+Y`.
  - **Broń (miecz, topór, pistolet, kosa):** punkt `(0, 0, 0)` dokładnie w **miejscu chwytu rękojeści (środek dłoni)**, głownia/lufa skierowana w `+Y`.
  - **Tarcza:** punkt `(0, 0, 0)` na wewnętrznym uchwycie/paskach, lico skierowane na zewnątrz.
- **Kierunek „Przód” (Front Facing):**  
  Twarz postaci, klatka piersiowa i przód konia muszą być skierowane w stronę **osi `+Z`** (w Three.js) / widok na wprost.
- **Wymiary referencyjne na polu szachownicy (pole = `1.15 m`):**
  - **Pion (`p`):** wys. ~`1.08 m`, szer. maks. `0.70 m`
  - **Skoczek (`n`):** wierzchowiec wys. ~`0.84 m` × dł. `0.94 m`
  - **Goniec (`b`):** wys. ~`1.20 m`
  - **Wieża (`r`):** baszta wys. ~`0.72 m` × śr. `0.78 m` (+ strzelec `0.90 m`)
  - **Hetman / Królowa (`q`):** wys. ~`1.38 m` (+ korona `0.88x`)
  - **Król (`k`):** wys. ~`1.54 m` (+ korona `1.18x`)

---

## 3. Standard Nazewnictwa Socketów (Węzły Empty w glTF)

Obiekty typu **Empty (`Plain Axes`)** eksportują się do formatu `.glb` jako puste węzły `THREE.Object3D`, do których silnik gry automatycznie kotwiczy komponenty potomne:

| Nazwa Węzła (Socket) | Zastosowanie | Precyzyjna Lokalizacja |
| :--- | :--- | :--- |
| `Socket_Crown` | Punkt osadzenia `korona.glb` oraz czapek/mitr | Na szczycie czaszki/hełmu (styk z dolną krawędzią korony) |
| `Socket_Hand_R` | Punkt uchwytu prawej dłoni (broń główna) | Środek prawej pięści; oś `+Y` wzdłuż rękojeści w górę |
| `Socket_Hand_L` | Punkt uchwytu lewej dłoni (tarcza / berło) | Środek lewej dłoni lub przedramienia |
| `Socket_Back` | Mocowanie peleryny / kołczanu | Środek górnej części pleców między łopatkami |
| `Socket_Rider` *(na `kon.glb` / `wieza.glb`)* | Punkt posadzenia jeźdźca / strzelca | Najniższy punkt siodła na koniu / podest wieży |
| `Socket_Piece` *(na `podstawka.glb`)* | Punkt posadzenia pionka | Środek górnej płaszczyzny cokołu |

---

## 4. Praca w Tripo.AI vs Blender — Wytyczne Operacyjne

Generator AI **Tripo.AI** znacząco przyspiesza kreację, ale posiada specyficzne ograniczenia w porównaniu z DCC (Blender). Poniżej zestawiono optymalne strategie radzenia sobie z tymi ograniczeniami:

### 4.1. Co Tripo.AI robi doskonale:
1. **Generowanie zoptymalizowanych siatek (Retopologia):** W opcjach eksportu Tripo wybieraj format **GLB** oraz docelowy budżet siatki **10 000 – 15 000 trójkątów** (zamiast surowych 100k).
2. **Generowanie scalonych wariantów (Rider + Mount):** Zamiast generować konia i jeźdźca osobno, a potem walczyć ze składaniem ich w kodzie, Tripo potrafi wygenerować zintegrowany model:
   > *Prompt:* `"Medieval Viking knight fully armored, mounted and sitting firmly in saddle on an armored war horse, hands holding reins, dynamic battle pose, complete single piece"` (`viking_cavalry.glb`).
3. **Generowanie postaci z wbudowanymi regaliami:** Zamiast montować koronę w locie przez bounding-box, możesz wygenerować dedykowanych władców:
   > *Prompt Król:* `"Viking King wearing an ornate golden crown firmly set on his brow, royal furs, standing proud, empty hands"` (`viking_king.glb`).
4. **Wymuszanie czystych dłoni (Unarmed Base):** Aby model nie miał wtopionej broni kolidującej z systemem uzbrojenia, w promptach zawsze dodawaj:  
   `"unarmed, empty open hands, relaxed fists, no weapons in hands"`.

### 4.2. Czego Tripo.AI NIE potrafi (Wymaga interwencji Blendera / Agenta):
- **Brak obsługi Socketów:** Tripo nie potrafi dodać węzła `Socket_Crown` ani `Socket_Hand_R`.
- **Brak kontroli punktu Pivot:** Tripo centruje oś obrotu w środku geometrii, uniemożliwiając ustawienie pivota na rękojeści miecza czy obręczy korony.

---

## 5. Rola Agenta (Antigravity): Automatyczna Pipeline Blendera

Użytkownik nie musi ręcznie instalować Blendera ani klikać wierzchołków. Architekt posiada możliwość uruchomienia **headless Blendera (CLI / skrypty Python)** w środowisku roboczym.

### Automatyczny potok przetwarzania surowych modeli z Tripo.AI:
1. Użytkownik pobiera model z Tripo.AI i załącza plik `.glb`.
2. Agent uruchamia skrypt Python w Blenderze (`blender.exe -b -P process_asset.py`):
   - Weryfikuje wymiary i centrowanie na osiach `X, Y, Z`.
   - Analizuje siatkę i automatycznie wstawia `Socket_Crown` na czaszce oraz `Socket_Hand_R` w dłoni.
   - Przeprowadza optymalizację Decimate (jeśli polycount > 15 000).
   - Przesuwa Pivot na dno obręczy (dla koron) lub rękojeść (dla broni).
   - Zapisuje gotowy, produkcyjny plik `.glb` do `modeleBC/` i wypycha na GitHub.
