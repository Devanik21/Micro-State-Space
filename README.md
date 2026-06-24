# micro-state-space

A collection of three minimalist, abstract strategy games designed to exist within ultra-low, micro-sized mathematical state spaces. This repository explores the balance between minimal physical configurations and deep tactical complexity.

## 🎮 The Games

### 1. Hex-Line
A minimalist connection game played on a small hexagonal grid that completely eliminates ties.
*   **The Board:** A cluster of 7 hexagons (1 center hex surrounded by 6 outer hexes).
*   **How to Play:** Two players alternate placing tokens on empty hexagons.
*   **Winning Condition:** Create a straight line of 3 tokens passing through the center, OR occupy any 4 of the 6 outer hexagons.
*   **State Space:** Max 2,187 physical states (~700 legal states).

### 2. Quantum Match
A hidden-information deduction game using a tiny grid and a shared pool of pieces.
*   **The Board:** A simple 2 × 2 grid (4 squares total).
*   **The Pieces:** A shared pool of 4 identical double-sided tokens (White/Black).
*   **How to Play:** On your turn, either flip exactly one token on the board to your color, OR place a new token from the pool onto an empty square with your color facing up.
*   **Winning Condition:** Control all 4 squares on the board with your color at the end of any turn.
*   **State Space:** 81 physical states.

### 3. Shift-3
A dynamic, moving-board game that fits into a tiny mathematical space.
*   **The Board:** A single row of 5 squares.
*   **How to Play:** Players start with 2 pieces each and alternate turns. Move by either placing a piece on an empty square, OR sliding an already-placed piece one square left or right into an adjacent empty space.
*   **Winning Condition:** Get your 2 pieces to completely surround any single opponent piece (e.g., P1, P2, P1), OR occupy 3 adjacent squares.
*   **State Space:** 243 physical states.

---

## 🛠️ Project Structure

```text
├── games/
│   ├── hex_line.py         # Hex-Line game logic
│   ├── quantum_match.py    # Quantum Match game logic
│   └── shift_3.py          # Shift-3 game logic
├── main.py                 # Game entry point / CLI launcher
├── README.md               # Project documentation
└── .gitignore              # Git ignore file
```

---

## 🚀 Getting Started

### Prerequisites
*   Python 3.8 or higher

### Installation & Run
1. Clone the repository:
   ```bash
   git clone https://github.com
   cd micro-state-space
   ```
2. Run the games:
   ```bash
   python main.py
   ```

---

## 📄 License
This project is licensed under the MIT License - see the LICENSE file for details.
