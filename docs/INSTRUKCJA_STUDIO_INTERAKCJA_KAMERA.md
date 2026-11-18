# Instrukcja Wdrożeniowa dla Studio: System Interakcji Double-Tap, Blokada Kamery Meczowej i Symbole 3D

> **Dla Studia / Asystenta Kodowania:**  
> Poniższy dokument zawiera kompletne, gotowe wytyczne architektoniczne oraz kod implementacyjny w TypeScript / Three.js dla gry **BloodChess**. Wprowadza ujednolicony system selekcji (PC + Mobile), sztywną blokadę kamery podczas partii, dynamiczne symbole 3D nad głowami bierek oraz warunkowe wyświetlanie zasięgu wroga (tylko w poziomie Łatwym przeciwko SI).

---

## 1. Kamera Meczowa (Locked Gameplay Camera)

### 1.1. Założenie i cel:
Podczas rozgrywki na telefonie dotknięcie ekranu nie może obracać ani przesuwać sceny (*OrbitControls* muszą zostać zablokowane na czas partii). Kamera musi stać sztywno pod optymalnym kątem taktycznym, ukazującym całą szachownicę ($8 \times 8$ pól = $9.20\text{ m} \times 9.20\text{ m}$) w wygodnej perspektywie gracza.

### 1.2. Parametry kamery w Three.js:
- **FOV (Pole widzenia):** `42°` - `45°` (minimalizuje zniekształcenia perspektywiczne na krawędziach).
- **Pozycja dla Gracza Białego (Widok od dołu planszy):**
  - `position: (0, 7.8, 8.2)`
  - `lookAt: (0, 0, -0.4)` (lekki offset ku środkowi planszy)
- **Pozycja dla Gracza Czarnego (Odwrócenie o 180°):**
  - `position: (0, 7.8, -8.2)`
  - `lookAt: (0, 0, 0.4)`
- **Blokada sterowania:**
  - `controls.enabled = false` (lub `controls.enableRotate = false; controls.enablePan = false; controls.enableZoom = false;`).

---

## 2. Mechanika Interakcji: System Double-Tap / Two-Step (PC + Mobile)

To samo, intuicyjne i bezpieczne zachowanie na myszce i ekranie dotykowym:

```
[KLIKNIĘCIE 1 / TAP 1]  --->  INSPEKCJA I WYBÓR (Symbol 3D + podświetlenie pól)
[KLIKNIĘCIE 2 / TAP 2]  --->  POTWIERDZENIE AKCJI (Wykonanie ruchu lub ataku)
```

### 2.1. Scenariusz A: Kliknięcie własnej bierki
1. **Tap 1:** Bierka zostaje zaznaczona (`selectedPiece`).
2. Nad jej głową pojawia się **obracający się lewitujący symbol 3D roli** w kolorze jej armii.
3. Na planszy podświetlają się zielone/złote kropki dozwolonych ruchów oraz czerwone kropki pól bicia.
4. **Tap 2:** Gracz klika podświetlone pole docelowe $\rightarrow$ bierka wykonuje ruch / bicie.

### 2.2. Scenariusz B: Kliknięcie bierki wroga (Czysta Inspekcja)
1. **Zawsze bezpieczne:** Kliknięcie wroga „na sucho” (gdy gracz nie ma zaznaczonej własnej bierki) **NIGDY nie powoduje ruchu ani błędu**.
2. Nad głową wrogiej bierki pojawia się jej **symbol 3D w kolorze armii wroga** (np. Goniec w szafirze Syndykatu).
3. **Zasada poziomu trudności (Threat Range):**
   - **Tylko w trybie `vs_ai` na poziomie `easy`:** Plansza podświetla na czerwono kafelki, które ta wroga bierka obecnie kontroluje / zagraża.
   - **W trybach `normal`, `hard` oraz `PvP`:** Podświetlenie zasięgu wroga jest **ukryte** (gracz widzi tylko symbol rangi nad głową, a kalkulację przeprowadza sam).

### 2.3. Scenariusz C: Wykonanie bicia wroga
1. **Tap 1:** Gracz zaznacza swojego wojownika.
2. **Tap 2:** Gracz klika wrogą figurę stojącą na podświetlonym czerwonym polu bicia $\rightarrow$ aktywuje się sekwencja ataku i filmowy takedown.

---

## 3. Zestaw Modeli Symboli 3D (`modeleBC/`)

Wszystkie symbole są przygotowane w formacie glTF 2.0 (`.glb`), mają wysokość `0.40 m` i wycentrowany pivot `(0, 0, 0)`:
- `modeleBC/symbol_krol.glb` – Król (♔ / ♚)
- `modeleBC/symbol_hetman.glb` – Hetman / Królowa (♕ / ♛)
- `modeleBC/symbol_wieza.glb` – Wieża (♖ / ♜)
- `modeleBC/symbol_goniec.glb` – Goniec (♗ / ♝)
- `modeleBC/symbol_skoczek.glb` – Skoczek (♘ / ♞)
- `modeleBC/symbol_pion.glb` – Pion (♙ / ♟)

### Paleta Kolorów Frakcji (`FACTION_COLORS`):
```typescript
export const FACTION_COLORS: Record<string, number> = {
  crusaders: 0xFFD233, // Zakon (Święte Złoto)
  ninjas:    0xF20D26, // Klan Krwawego Cienia (Karmazynowa Krew)
  mafia:     0x0D73FF, // Syndykat (Królewski Szafir)
  vikings:   0x00F2FF, // Wikingowie (Mroźny Cyjan)
  undead:    0x59FF1A, // Horda (Trupia Ektoplazma)
  goblins:   0x00BF59, // Sabat Goblinów (Żrący Szmaragd)
  cowboys:   0xFF8C0D, // Kowboje (Pustynny Bursztyn)
  butchers:  0xB326F2, // Rzeźnia (Mroczny Ametyst)
  pirates:   0x00A6A6, // Korsarze (Głęboki Turkus)
  soldiers:  0xD9E6F2, // Najemnicy (Stalowy Tytan)
};
```

---

## 4. Gotowa Implementacja w TypeScript / Three.js

Poniższy kontroler zarządza pełną logiką kamery, dwuetapowej selekcji, symboli 3D oraz weryfikacji trudności:

```typescript
import * as THREE from 'three';
import { GLTFLoader } from 'three/examples/jsm/loaders/GLTFLoader.js';

export type PieceRole = 'krol' | 'hetman' | 'wieza' | 'goniec' | 'skoczek' | 'pion';
export type GameDifficulty = 'easy' | 'normal' | 'hard';
export type GameMode = 'vs_ai' | 'pvp_local' | 'pvp_online';

export interface ChessPiece {
  id: string;
  role: PieceRole;
  faction: string;
  isWhite: boolean;
  mesh: THREE.Object3D;
  tileX: number;
  tileZ: number;
  getLegalMoves: () => { x: number; z: number; isCapture: boolean }[];
  getThreatTiles: () => { x: number; z: number }[];
}

export class BloodChessInputController {
  private scene: THREE.Scene;
  private camera: THREE.PerspectiveCamera;
  private symbols: Map<PieceRole, THREE.Object3D> = new Map();
  private activeSymbol: THREE.Object3D | null = null;
  private symbolBaseY: number = 0;

  public selectedPiece: ChessPiece | null = null;
  public inspectedEnemy: ChessPiece | null = null;
  public currentTurnIsWhite: boolean = true;
  public gameMode: GameMode = 'vs_ai';
  public difficulty: GameDifficulty = 'easy';

  constructor(scene: THREE.Scene, camera: THREE.PerspectiveCamera) {
    this.scene = scene;
    this.camera = camera;
    this.preloadSymbols();
  }

  // 1. BLOKADA KAMERY MECZOWEJ
  public lockGameplayCamera(playerIsWhite: boolean) {
    this.camera.fov = 42;
    if (playerIsWhite) {
      this.camera.position.set(0, 7.8, 8.2);
      this.camera.lookAt(0, 0, -0.4);
    } else {
      this.camera.position.set(0, 7.8, -8.2);
      this.camera.lookAt(0, 0, 0.4);
    }
    this.camera.updateProjectionMatrix();
  }

  // 2. ŁADOWANIE MODELI SYMBOLI 3D
  private preloadSymbols() {
    const loader = new GLTFLoader();
    const roles: PieceRole[] = ['krol', 'hetman', 'wieza', 'goniec', 'skoczek', 'pion'];

    roles.forEach(role => {
      loader.load(`modeleBC/symbol_${role}.glb`, (gltf) => {
        const model = gltf.scene;
        model.traverse(child => {
          if ((child as THREE.Mesh).isMesh) {
            const mesh = child as THREE.Mesh;
            mesh.castShadow = true;
            mesh.receiveShadow = false;
          }
        });
        this.symbols.set(role, model);
      });
    });
  }

  // 3. POKAZYWANIE LEWITUJĄCEGO SYMBOLU 3D
  public showSymbolForPiece(piece: ChessPiece) {
    this.hideSymbol();

    const template = this.symbols.get(piece.role);
    if (!template) return;

    const symbol = template.clone();
    const factionColor = FACTION_COLORS[piece.faction] || 0xFFFFFF;

    symbol.traverse(child => {
      if ((child as THREE.Mesh).isMesh) {
        const mesh = child as THREE.Mesh;
        const mat = (mesh.material as THREE.MeshStandardMaterial).clone();
        mat.color.setHex(factionColor);
        mat.emissive.setHex(factionColor);
        mat.emissiveIntensity = 0.35;
        mesh.material = mat;
      }
    });

    // Oblicz wysokość nad głową (wykorzystaj Socket_Crown lub bounding box)
    const crownSocket = piece.mesh.getObjectByName('Socket_Crown');
    if (crownSocket) {
      crownSocket.getWorldPosition(symbol.position);
      this.symbolBaseY = symbol.position.y + 0.30;
    } else {
      const box = new THREE.Box3().setFromObject(piece.mesh);
      this.symbolBaseY = box.max.y + 0.25;
      symbol.position.set(piece.mesh.position.x, this.symbolBaseY, piece.mesh.position.z);
    }

    this.scene.add(symbol);
    this.activeSymbol = symbol;
  }

  public hideSymbol() {
    if (this.activeSymbol) {
      this.scene.remove(this.activeSymbol);
      this.activeSymbol = null;
    }
  }

  // 4. LOGIKA DOUBLE-TAP / TWO-STEP INTERACTION (PC + MOBILE)
  public handlePieceClick(clickedPiece: ChessPiece, boardVisuals: any) {
    const isFriendly = clickedPiece.isWhite === this.currentTurnIsWhite;

    if (isFriendly) {
      // KROK 1: Kliknięcie własnej bierki -> Wybór do ruchu
      this.selectedPiece = clickedPiece;
      this.inspectedEnemy = null;
      boardVisuals.clearAllHighlights();

      // Pokaż symbol 3D w barwach własnej armii
      this.showSymbolForPiece(clickedPiece);

      // Podświetl dozwolone ruchy i cele ataku
      const legalMoves = clickedPiece.getLegalMoves();
      boardVisuals.highlightLegalMoves(legalMoves);
    } 
    else {
      // Kliknięcie bierki wroga:
      if (this.selectedPiece) {
        // Sprawdź, czy kliknięty wróg jest celem ataku dla zaznaczonej bierki:
        const moves = this.selectedPiece.getLegalMoves();
        const canCapture = moves.some(m => m.isCapture && m.x === clickedPiece.tileX && m.z === clickedPiece.tileZ);

        if (canCapture) {
          // KROK 2: POTWIERDZENIE BICIA (Double-Tap zakończony atakiem)
          this.executeMove(this.selectedPiece, clickedPiece.tileX, clickedPiece.tileZ, clickedPiece);
          return;
        }
      }

      // KROK 1B: CZYSTA INSPEKCJA WROGA (Nie powoduje ruchu!)
      this.selectedPiece = null;
      this.inspectedEnemy = clickedPiece;
      boardVisuals.clearAllHighlights();

      // Wyświetl symbol 3D w barwach armii wroga
      this.showSymbolForPiece(clickedPiece);

      // WARUNEK: Zasięg rażenia wroga TYLKO w poziomie EASY przeciwko komputerowi:
      if (this.gameMode === 'vs_ai' && this.difficulty === 'easy') {
        const threatTiles = clickedPiece.getThreatTiles();
        boardVisuals.highlightThreatRange(threatTiles); // Czerwone obwódki pól zagrożonych
      }
    }
  }

  public handleTileClick(tileX: number, tileZ: number, boardVisuals: any) {
    if (this.selectedPiece) {
      const moves = this.selectedPiece.getLegalMoves();
      const isValidMove = moves.some(m => m.x === tileX && m.z === tileZ);

      if (isValidMove) {
        // KROK 2: POTWIERDZENIE RUCHU NA PUSTE POLE
        this.executeMove(this.selectedPiece, tileX, tileZ, null);
        return;
      }
    }

    // Kliknięcie w puste nieaktywne pole -> Reset zaznaczenia
    this.selectedPiece = null;
    this.inspectedEnemy = null;
    this.hideSymbol();
    boardVisuals.clearAllHighlights();
  }

  private executeMove(piece: ChessPiece, targetX: number, targetZ: number, targetEnemy: ChessPiece | null) {
    this.hideSymbol();
    // Odpalenie animacji ruchu / cutscenki takedownu w silniku gry
    console.log(`Executing move for ${piece.id} to (${targetX}, ${targetZ})`);
  }

  // 5. UPDATE PĘTLI ANIMACJI (LEWITACJA I OBRÓT SYMBOLU 3D)
  public update(time: number, delta: number) {
    if (this.activeSymbol) {
      // Płynne unoszenie góra-dół (sinusoida)
      this.activeSymbol.position.y = this.symbolBaseY + Math.sin(time * 3.5) * 0.05;
      // Ciągły obrót wokół osi pionowej Y
      this.activeSymbol.rotation.y += delta * 1.8;
    }
  }
}
```

---

## 5. Podsumowanie Korzyści dla Gracza i Gry:
1. **100% ergonomia na telefonach:** Brak przypadkowych obrotów kamery podczas stukania palcem w małe pola szachownicy.
2. **Koniec z pomyłkami pion vs goniec:** Każdy tap natychmiast rozwiewa wątpliwości lewitującym symbolem 3D.
3. **Czyste szachy na wyższych poziomach:** Podpowiedź zasięgu wroga pomaga nowicjuszom na poziomie Easy, ale nie psuje wyzwania taktycznego na poziomach Normal, Hard i w rozgrywkach sieciowych.
