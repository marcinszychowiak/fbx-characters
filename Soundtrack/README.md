# System Ścieżki Dźwiękowej (Soundtrack / BGM) — BloodChess

Katalog `Soundtrack/` przechowuje pełnowymiarowe podkłady muzyczne (BGM – Background Music) odtwarzane w trakcie partii szachowych, w menu oraz podczas starć bitewnych w grze **BloodChess**.

---

## 1. Logika Wyboru Muzyki w Grze (Match Audio Selector)

W silniku gry mechanizm zarządzania muzyką tła (`BattleMusicManager`) działa w oparciu o selekcję kontekstową według następującej reguły:

```
[Inicjalizacja Partii: Frakcja A vs Frakcja B]
                      │
                      ▼
       [Budowanie Puli Utworów Meczu]
       ├── Ścieżka dedykowana Frakcji A (np. Faction_Wikingowie_Theme.mp3)
       ├── Ścieżka dedykowana Frakcji B (np. Faction_Zakon_Theme.mp3)
       ├── Uniwersalna ścieżka bitewna #1 (Universal_Battle_Theme_01.mp3)
       └── Uniwersalna ścieżka bitewna #2 (Universal_Battle_Theme_02.mp3)
                      │
                      ▼
        [Losowy Wybór Ścieżki (RNG)]
   Silnik losuje jeden utwór z puli na czas meczu
          (lub odtwarza w pętli w trybie shuffle)
```

### Zasady algorytmu:
1. **Losowanie:** Ścieżka dźwiękowa meczu wybierana jest losowo spośród:
   - utworów przypisanych do **dwóch armii (frakcji)** aktualnie biorących udział w pojedynku,
   - **jednej z dwóch ścieżek uniwersalnych** (ogólnych bitewnych).
2. **Fallback:** Jeżeli dla danej frakcji nie zaimplementowano jeszcze dedykowanej ścieżki, silnik korzysta wyłącznie z puli ścieżek uniwersalnych.
3. **Pętla i przejścia:** Utwory są zapętlane z płynnym wyciszaniem (Crossfade 2.5s) lub dynamicznie przygaszane w momencie aktywacji sekwencji takedownu (cutscenki egzekucyjnej), aby wyeksponować kwestie dialogowe i efekty dźwiękowe ciosów.

---

## 2. Aktualna Zawartość Katalogu

| Nazwa Pliku | Czas Trwania | Rozmiar | Kategoria | Opis |
| :--- | :---: | :---: | :--- | :--- |
| `Universal_Battle_Theme_01.mp3` | **4:04** | **5.74 MB** | Uniwersalna (Bitewna #1) | Epicki, orkiestrowo-symfoniczny motyw bitewny z ciężkimi bębnami wojennymi, sekcją smyczkową i chórem. |

---

## 3. Konwencja Nazewnictwa dla Nowych Ścieżek

W miarę rozwoju gry do katalogu będą sukcesywnie dodawane kolejne utwory. Należy stosować ustandaryzowane nazewnictwo:

### A. Ścieżki Uniwersalne:
- `Universal_Battle_Theme_01.mp3` *(aktualnie w repozytorium)*
- `Universal_Battle_Theme_02.mp3` *(druga planowana ścieżka uniwersalna)*
- `Universal_Menu_Theme.mp3` *(ścieżka do menu głównego / wyboru armii)*

### B. Ścieżki Frakcyjne:
- `Faction_Kowboj_Theme.mp3`
- `Faction_Gobliny_Theme.mp3`
- `Faction_Horda_Theme.mp3`
- `Faction_Klan_Theme.mp3`
- `Faction_Najemnicy_Theme.mp3`
- `Faction_Korsarze_Theme.mp3`
- `Faction_Rzeznia_Theme.mp3`
- `Faction_Syndykat_Theme.mp3`
- `Faction_Wikingowie_Theme.mp3`
- `Faction_Zakon_Theme.mp3`

---

## 4. Wytyczne Techniczne dla Audio Engine (Unity / Unreal / Godot)

1. **Format:** MP3 (CBR/VBR 192-320 kbps) lub OGG Vorbis – zoptymalizowany pod kątem streamingu z dysku (`Streaming from storage`), co zapobiega zajmowaniu pamięci RAM przez długie pliki muzyczne.
2. **Normalizacja Głośności:** Ścieżki powinny być zmasterowane do poziomu `-14 LUFS` (zintegrowany), aby utrzymać stałą dynamikę pomiędzy utworami frakcyjnymi a uniwersalnymi.
3. **Kaczka Audio (Audio Ducking):** W trakcie odtwarzania cutscenki takedownu (`Scenarios/`), poziom głośności muzyki tła powinien zostać automatycznie obniżony o `-9 dB` na szynie miksera, aby zapewnić czytelność głosów z folderu `BloodChess/`.
