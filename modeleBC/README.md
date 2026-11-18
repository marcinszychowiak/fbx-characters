# Katalog Dedykowanych Modeli 3D BloodChess (`modeleBC/`)

Wszystkie assety w katalogu `modeleBC/` są zoptymalizowanymi plikami binarnymi **glTF 2.0 (`.glb`)**, przygotowanymi bezpośrednio do wczytania przez `GLTFLoader` w Three.js / Babylon.js lub silnikach Unity / Godot / Unreal.

---

## 1. Postacie Frakcyjne (Humanoid Rig + Sockets)

Każda postać posiada **szkielet 19 kości** ze skinningiem oraz wbudowane punkty montażowe (`Empty`):
- `Socket_Crown` – czubek głowy (pod nakrycia ról i koronę),
- `Socket_Hand_R` – prawa dłoń (broń główna),
- `Socket_Hand_L` – lewa dłoń (tarcza / rekwizyt / broń boczna),
- `Socket_Back` – plecy (peleryna / kołczan).

| Plik GLB | Alias dla Studio | Frakcja | Wzrost realny | Uwagi / Skala |
| :--- | :--- | :--- | :---: | :--- |
| `goblin.glb` | `goblins.glb` | Sabat Goblinów | 0.70 m | Najmniejsza jednostka, zwinny zwiadowca |
| `rzeznik.glb` | `butchers.glb` | Rzeźnia | 1.60 m | Krępy, masywny rzeźnik z fartuchem |
| `Syndykat.glb` | `mafia.glb` | Syndykat | 1.70 m | Elegancki garnitur mafijny |
| `klan.glb` | `ninjas.glb` | Klan Krwawego Cienia | 1.75 m / 1.42 m | Wyprostowany 1.75 m; w przysiadzie bojowym 1.42 m |
| `korsarz.glb` | `pirates.glb` | Korsarze | 1.80 m | Awanturnik morski |
| `kowboj.glb` | `cowboys.glb` | Kowboje | 1.80 m | Strzelec z Dzikiego Zachodu |
| `horda.glb` | `undead.glb` | Horda | 1.80 m | Zainfekowany zombie |
| `najemnicy.glb`| `soldiers.glb` | Najemnicy | 1.90 m | Opancerzony żołnierz kontraktowy |
| `zakon.glb` | `crusaders.glb` | Zakon | 1.90 m | Zakonnik w zbroi krzyżowca |
| `wiking.glb` | `vikings.glb` | Wikingowie | 2.15 m | Olbrzym z północy |

---

## 2. Dedykowane Wierzchowce i Baszty

- `kon.glb` – Koń bojowy / Skoczek (posiada punkt siodła `Socket_Rider`).
- `wieza.glb` – Kamienna baszta oblężnicza / Wieża (posiada punkt podestu `Socket_Rider`).

---

## 3. Uzbrojenie Ról Bitewnych (Grip w `0, 0, 0`)

Wszystkie bronie mają punkt chwytu wycentrowany dokładnie w `(0, 0, 0)`, co umożliwia natychmiastowe podpięcie do dłoni:
- `miecz_krola.glb` – Miecz monarszy (prawa dłoń Króla),
- `berlo.glb` – Złote berło władcy (lewa dłoń Króla),
- `sztylet_krolowa.glb` – Paradny sztylet Królowej (lewa dłoń Hetmana),
- `kopia.glb` – Kopia rycerska (prawa dłoń Skoczka na koniu),
- `puklerz.glb` – Tarcza kawaleryjska / puklerz (lewa dłoń Skoczka),
- `kostur_gonca.glb` – Pastorał / kostur święty (prawa dłoń Gońca),
- `kielich_gonca.glb` – Złoty kielich rytualny ze szmaragdami (lewa dłoń Gońca),
- `mlot_wiezy.glb` – Runiczny młot obronny (prawa dłoń Wieży),
- `pawez_wiezy.glb` – Wielka tarcza oblężnicza / pawęż (lewa dłoń Wieży).

---

## 4. Nakrycia Głowy i Atrybuty Ról (`Socket_Crown`)

- `korona.glb` – Korona królewska (dla Króla oraz Hetmana w mniejszej skali),
- `czepiec_wiezy.glb` – Stalowy hełm basztowy z nosalem,
- `czapka_gonca.glb` – Błazeńska czapka z rogami i dzwoneczkami,
- `kita_skoczka.glb` – Hełm rycerski z pióropuszem.

---

## 5. Cokoły i Efekty VFX

- `podstawka.glb` (alias: `cokol.glb`) – Kamienny rzeźbiony cokół (średnica $0.95\text{ m}$, wysokość $0.135\text{ m}$, spód na $Z = 0$), zredukowany do 246 KB.
- `specialpower.glb` – Animowany pionowy słup energii i fal uderzeniowych aktywacji mocy specjalnej (wysokość $2.10\text{ m}$).
- `takedown_horda_syndykat.glb` – Zintegrowana animacja filmowej egzekucji Hetmana przez Zombie (125 klatek, dwie zsynchronizowane postacie).

---

## 6. Lewitujące Symbole Szachowe 3D (Unicode PBR z Czarnym Rantem)

Wysokość `0.40 m`, pivot w środku geometrycznym `(0, 0, 0)`. Modele posiadają **2 sloty materiałowe**:
- **Slot 0 (`Symbol_Faction_Face`):** Awers i rewers symbolu – podmieniany w kodzie na barwę armii gracza.
- **Slot 1 (`Symbol_Black_Rim`):** Krawędź fazowana i boki w głębokiej czerni – tworzą ostry, czytelny kontur na dowolnym tle.
- `symbol_krol.glb` – Symbol Króla (♔ / ♚),
- `symbol_hetman.glb` – Symbol Hetmana / Królowej (♕ / ♛),
- `symbol_wieza.glb` – Symbol Wieży (♖ / ♜),
- `symbol_goniec.glb` – Symbol Gońca (♗ / ♝),
- `symbol_skoczek.glb` – Symbol Skoczka (♘ / ♞),
- `symbol_pion.glb` – Symbol Piona (♙ / ♟),
- `symbole_szachowe_3d.glb` – Paczka zbiorcza ze wszystkimi 6 symbolami.

---

## 7. Scenografia Areny Bitewnej

- `plansza.glb` – Luksusowy stół szachowy z polerowanego onyksu i białego marmuru ($9.20\text{ m} \times 9.20\text{ m}$, platforma $10.40\text{ m} \times 10.40\text{ m}$, siatka pól $1.15\text{ m}$).
- `schody.glb` – Samodzielne kamienne schody (szerokość $5.20\text{ m}$, spadek $3.00\text{ m}$) z pivotem na górnym podeście.
- `sztandar.glb` – Powiewający sztandar z 10-kościowym szkieletem (animacja wiatru 60 klatek).
- `koksownik.glb` – Mosiężno-kamienny koksownik zamkowy (wysokość $1.41\text{ m}$, gniazdo `Socket_Flame`).
- `ogien_do_koksownika.glb` – Animowany ogień płomieni (192 meshe, pętla 30 klatek).
- `koksownik_z_ogniem.glb` – Zintegrowany koksownik z animowanym ogniem.
- `sztandar.glb` – Samodzielny powiewający sztandar heraldyczny z 10-kościowym szkieletem (zorientowany pionowo w dół, długość 7.10 m, szerokość 1.61 m).
- `sceneria_lochy.glb` – **Kompletna arena lochów 3D**:
  - Centralna platforma szachownicy z polerowanego marmuru i onyksu,
  - **Masywna kamienna podmurówka (`Arena_Chess_Podium`)** zamykająca w 100% pustkę pod szachownicą ($10.38	ext{ m} 	imes 10.38	ext{ m} 	imes 2.82	ext{ m}$) wraz z 4 narożnymi bastionami pod koksowniki,
  - Schody wejściowe Białych (południe) i Czarnych (północ),
  - 4 koksowniki narożne na $X, Y = \pm 5.35	ext{ m}$ z animowanym ogniem,
  - Gotyckie mury i bramy łukowe odsunięte na $X = \pm 10.50	ext{ m}$ (zapewniające ponad 4.5 m wolnej przestrzeni wokół planszy),
  - **4 wielkie sztandary heraldyczne wiszące pionowo** wzdłuż ścian tuż za koksownikami.
  - Centralna platforma szachownicy,
  - Schody wejściowe Białych (południe) i Czarnych (północ),
  - 4 koksowniki narożne na $X, Y = \pm 5.35\text{ m}$,
  - Gotyckie mury i bramy łukowe odsunięte na $X = \pm 10.50\text{ m}$ (zapewniające ponad 4.5 m wolnej przestrzeni wokół szachownicy),
  - 4 powiewające sztandary heraldyczne na ścianach.

---

## 8. Plansze Referencyjne (Podglądy PNG)

- `preview_arena_lochy_mecz.png` – Taktyczny rzut zablokowanej kamery meczowej z góry.
- `preview_arena_lochy_biale.png` – Widok od dołu schodów Białych.
- `preview_arena_lochy_detal.png` – Detal ognia i sztandaru na murze.
- `showcase_symbole_szachowe_3d.png` – Zestawienie 6 symboli szachowych.
- `showcase_10_frakcji_kolory.png` – Oficjalna paleta barw 10 frakcji.
- `proponowane_skale_studio.png` – Plansza kalibracji wzrostu postaci ($0.70\text{ m} - 2.15\text{ m}$).
