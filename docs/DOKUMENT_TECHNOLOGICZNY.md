# Dokument Technologiczny Projektu — BloodChess

## 1. Wstęp i cel dokumentu
Niniejszy dokument przedstawia w przystępny i zrozumiały sposób stos technologiczny oraz architekturę zasobów wykorzystanych w projekcie **BloodChess** (Krwawe Szachy). Wyjaśnia, dlaczego wybrano konkretne technologie, jakie były alternatywy oraz jakie kryteria zadecydowały o ich wdrożeniu.

---

## 2. Zestawienie Technologii i Uzasadnienia Wyborów

### 2.1. Format Modeli 3D Ogólnych: Autodesk FBX (.fbx)
- **Rola w projekcie:** Główny format dystrybucji 52 trójwymiarowych modeli postaci bazowych, pancerzy i rekwizytów (`FBX/`).
- **Dlaczego FBX?** Format FBX to uniwersalny standard branżowy w tworzeniu gier komputerowych. Zawiera w jednym pliku siatkę 3D (geometrię), szkielet deformacyjny (rigging), wagi wierzchołków (skin weights) oraz koordynaty mapowania tekstur (UVs).
- **Alternatywy:** OBJ (brak obsługi szkieletów i animacji), DAE/Collada (przestarzały).
- **Kryteria decyzyjne:** Stuprocentowa kompatybilność "out of the box" z wiodącymi silnikami gier (Unity, Unreal Engine 5, Godot) oraz programami do animacji (Blender, Maya).

### 2.2. Format Dedykowanych Modeli Frakcyjnych: Binary glTF 2.0 (.glb)
- **Rola w projekcie:** Dystrybucja 10 unikalnych, dedykowanych modeli postaci dla każdej z frakcji (`modeleBC/`).
- **Dlaczego glTF / GLB?** Nazywany "JPEG-iem dla grafiki 3D" przez konsorcjum Khronos Group. Format binarny `.glb` pakuje geometrię, materiały PBR (Physically Based Rendering), tekstury oraz szkielet w jeden zoptymalizowany plik bez konieczności linkowania zewnętrznych plików PNG/JPG.
- **Alternatywy:** Klasyczny FBX z osobnymi folderami tekstur (podatny na gubienie ścieżek bezwzględnych do materiałów), USDZ (format głównie ekosystemu Apple).
- **Kryteria decyzyjne:** Zerowe ryzyko brakujących tekstur (self-contained asset), szybkie ładowanie w runtime silników nowej generacji i narzędzi webowych/silników gier, natywna obsługa materiałów PBR.

### 2.3. Format Dźwięków Krótkich (Głosy i SFX): Nieskompresowany PCM WAV (48 kHz / 16-bit)
- **Rola w projekcie:** Przechowywanie kwestii głosowych frakcji (`BloodChess/`) oraz próbek efektów dźwiękowych (SFX).
- **Dlaczego WAV 48 kHz?** Częstotliwość 48 kHz jest standardem produkcyjnym w branży filmowej i w nowoczesnych grach wideo. Format nieskompresowany zapobiega degradacji jakości i artefaktom kompresji podczas wielokrotnego nakładania filtrów dźwiękowych i miksowania w silniku audio.
- **Alternatywy:** MP3 (niezalecany dla krótkich sampli ze względu na opóźnienia dekompresji i obcięte pasmo wysokich tonów), OGG Vorbis.
- **Kryteria decyzyjne:** Zachowanie studyjnej czystości głosu, brak opóźnień (zero-latency) przy odpalaniu zsynchronizowanych zdarzeń animacji.

### 2.4. Format Muzyki Tła (Soundtrack / BGM): MP3 (Streaming Audio)
- **Rola w projekcie:** Przechowywanie pełnowymiarowych, wielominutowych utworów muzycznych w katalogu `Soundtrack/`.
- **Dlaczego MP3 dla muzyki?** Utwory trwające 4–5 minut w nieskompresowanym formacie WAV zajmowałyby po 50–70 MB każdy, drastycznie obciążając pamięć RAM silnika gry. Skompresowany format MP3 (5–6 MB) pozwala na bezpośredni streaming z nośnika (audio streaming) bez alokacji całego utworu w pamięci operacyjnej.
- **Alternatywy:** WAV (zbyt duży rozmiar pliku), FLAC (zbędny narzut pamięciowy w grach czasu rzeczywistego).
- **Kryteria decyzyjne:** Optymalny stosunek wierności brzmienia orkiestry do rozmiaru pliku, wsparcie streamingu dyskowego w Unity, Unreal i Godot.

### 2.5. Scenariusze i Specyfikacja Techniczna: Markdown (.md) oraz Notacje JSON
- **Rola w projekcie:** Definicja 10 scenariuszy egzekucji frakcyjnych w katalogu `Scenarios/`.
- **Dlaczego Markdown + JSON?** Format Markdown jest czytelny zarówno dla człowieka (reżysera, animatora, osoby nietechnicznej), jak i maszynowo interpretowalny. Wbudowane bloki schematów JSON umożliwiają automatycznym parserom i generatorom kodu w silniku natychmiastowe zbudowanie tablicy zdarzeń (`Animation Event Track`).
- **Alternatywy:** Dokumenty Word / PDF (nieprzejrzyste dla systemów kontroli wersji Git, brak automatycznego parsowania), bazy SQL (zbędna złożoność na etapie prototypowania).
- **Kryteria decyzyjne:** Pełna integracja z GitHubem, łatwa edycja w dowolnym edytorze, czytelne diffy w historii wersji.

### 2.6. Kontrola Wersji: Git & GitHub
- **Rola w projekcie:** Śledzenie zmian, tworzenie bezpiecznych kopii zapasowych, wersjonowanie i integracja pracy agentów AI z repozytorium zdalnym.
- **Dlaczego Git?** Niezawodny, rozproszony system kontroli wersji, standard światowej inżynierii oprogramowania.

---

## 3. Podsumowanie
Dobór technologii w projekcie **BloodChess** kładzie nacisk na interoperacyjność, bezstratną jakość materiałów źródłowych oraz prostotę integracji dla zewnętrznych programów i kreatorów tworzących logikę gry.
