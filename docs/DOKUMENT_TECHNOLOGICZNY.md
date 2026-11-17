# Dokument Technologiczny Projektu — BloodChess

## 1. Wstęp i cel dokumentu
Niniejszy dokument przedstawia w przystępny i zrozumiały sposób stos technologiczny oraz architekturę zasobów wykorzystanych w projekcie **BloodChess** (Krwawe Szachy). Wyjaśnia, dlaczego wybrano konkretne technologie, jakie były alternatywy oraz jakie kryteria zadecydowały o ich wdrożeniu.

---

## 2. Zestawienie Technologii i Uzasadnienia Wyborów

### 2.1. Format Modeli 3D: Autodesk FBX (.fbx)
- **Rola w projekcie:** Główny format dystrybucji 52 trójwymiarowych modeli postaci, pancerzy i rekwizytów (`FBX/`).
- **Dlaczego FBX?** Format FBX to uniwersalny standard branżowy w tworzeniu gier komputerowych. Zawiera w jednym pliku nie tylko siatkę 3D (geometrię), ale również szkielet deformacyjny (rigging), wagi wierzchołków (skin weights) oraz koordynaty mapowania tekstur (UVs).
- **Alternatywy:** OBJ (brak obsługi szkieletów i animacji), glTF/GLB (nowoczesny, świetny do webu, ale wciąż wymagający konwersji w części starszych narzędzi DCC), DAE/Collada (przestarzały).
- **Kryteria decyzyjne:** Stuprocentowa kompatybilność "out of the box" z wiodącymi silnikami gier (Unity, Unreal Engine 5, Godot) oraz programami do animacji (Blender, Maya).

### 2.2. Format Dźwięków: Nieskompresowany PCM WAV (48 kHz / 16-bit)
- **Rola w projekcie:** Przechowywanie kwestii głosowych frakcji (`BloodChess/`) oraz próbek efektów dźwiękowych (SFX).
- **Dlaczego WAV 48 kHz?** Częstotliwość 48 kHz jest standardem produkcyjnym w branży filmowej i w nowoczesnych grach wideo. Format nieskompresowany zapobiega degradacji jakości i artefaktom kompresji podczas wielokrotnego nakładania filtrów dźwiękowych i miksowania w silniku audio.
- **Alternatywy:** MP3 (niezalecany w silnikach ze względu na opóźnienia dekompresji i obcięte pasmo wysokich tonów), OGG Vorbis (dobry format runtime, ale kompresję do OGG wykonuje bezpośrednio silnik gry przy budowaniu projektu).
- **Kryteria decyzyjne:** Zachowanie studyjnej czystości głosu, brak opóźnień przy odpalaniu zsynchronizowanych zdarzeń animacji.

### 2.3. Scenariusze i Specyfikacja Techniczna: Markdown (.md) oraz Notacje JSON
- **Rola w projekcie:** Definicja 10 scenariuszy egzekucji frakcyjnych w katalogu `Scenarios/`.
- **Dlaczego Markdown + JSON?** Format Markdown jest czytelny zarówno dla człowieka (reżysera, animatora, osoby nietechnicznej), jak i maszynowo interpretowalny. Wbudowane bloki schematów JSON umożliwiają automatycznym parserom i generatorom kodu w silniku natychmiastowe zbudowanie tablicy zdarzeń (`Animation Event Track`).
- **Alternatywy:** Dokumenty Word / PDF (nieprzejrzyste dla systemów kontroli wersji Git, brak automatycznego parsowania), bazy SQL (zbędna złożoność na etapie prototypowania).
- **Kryteria decyzyjne:** Pełna integracja z GitHubem, łatwa edycja w dowolnym edytorze, czytelne diffy w historii wersji.

### 2.4. Kontrola Wersji: Git & GitHub
- **Rola w projekcie:** Śledzenie zmian, tworzenie bezpiecznych kopii zapasowych, wersjonowanie i integracja pracy agentów AI z repozytorium zdalnym.
- **Dlaczego Git?** Niezawodny, rozproszony system kontroli wersji, standard światowej inżynierii oprogramowania.

---

## 3. Podsumowanie
Dobór technologii w projekcie **BloodChess** kładzie nacisk na interoperacyjność, bezstratną jakość materiałów źródłowych oraz prostotę integracji dla zewnętrznych programów i kreatorów tworzących logikę gry.
