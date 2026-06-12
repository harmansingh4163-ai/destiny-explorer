# destiny-explorer

A chess explorer that answers a different question than a chess engine. 
An engine tells you the best move. This tool tries to play out **every 
possible game** from a position, and then colors each move by where it 
can lead — win, loss, or draw. It shows you the future of a position, 
not just the next step.

## How it works (simple version)

- It plays moves one by one, going deeper and deeper, like exploring 
  every branch of a tree.
- When a game ends (checkmate, stalemate, draw), it **undoes moves** 
  step by step to walk back up the tree, then tries the next untried move. 
  This repeats until every branch is explored.
- The whole search is **deterministic** — no randomness. Run it twice on 
  the same position, get the same answer twice.
- Many different move orders lead to the **same board position**. Exploring 
  the same position twice is wasted work, so every position gets a 
  fingerprint number (Zobrist hashing) and is stored in a table 
  (transposition table). If a position was already explored, its result 
  is reused instead of recomputed. This duplicate-removal is what makes 
  the search possible at all.
- Progress **auto-saves**, so long searches can be stopped and resumed.

## How to use

1. Open the project in Godot 4.3 and run it.
2. Set up a position on the board (or start from a built-in one).
3. Start the search. Moves get colored as results come in — the colors 
   show each move's possible outcomes ("destiny").
4. There is also a Rust version of the engine for faster searching, 
   without the GUI.

## Honest note

Full chess from the starting position is far too big to ever finish — 
this is for endgames and small positions, where "every possible game" 
is actually reachable.

Status: working hobby project, rough edges expected.
