# 🎲 Lotto Quest

**A roguelike-style browser game about risk, luck and the house edge.**
Climb a branching map, pick your fights, roll the D100, and see how many points you can walk away with — if the odds let you.

Built with [Phaser 3](https://phaser.io/) during **Hackathon Bydgoszcz 2025**.

<!-- Tip: add a screenshot or GIF here, e.g. ![Gameplay](docs/screenshot.png) -->

---

## 🕹️ How to play

1. Click **GRAJ** (Play) and enter your name.
2. You start at the campfire with **100 points** and **3 lives** ❤️.
3. Each level you choose one of up to three paths with the arrow keys:

   | Key | Move |
   |-----|------|
   | `←` | left path |
   | `↑` | middle path |
   | `→` | right path |

4. Entering a monster's territory triggers a **D100 roll**. Every monster shows its target (e.g. `D65+`) — roll that number or higher to win.
5. Reach the **Boss** at the top of the map for a final coin flip: **×2** your points or **×0.5**.
6. Your final score goes to the local **Top 10** leaderboard.

The game ends early if you lose all 3 lives or your points drop to almost zero — in that case your score is 0.

## 👹 Monsters

| Monster | Win chance | On win | On loss |
|---------|-----------|--------|---------|
| 🟢 **Low risk** | 60–90% | small gain | lose 20–35% of points + 1 life |
| 🔴 **High risk** | 20–50% | big gain | lose 50–80% of points + 1 life |
| 💀 **Boss** | 50% | points ×2 | points ×0.5 |

Every monster's odds are randomised, so the target number on each one matters — read the map before you move.

## 📐 The math behind it

Lotto Quest isn't just random — it's built on a real gambling model. Each regular encounter has a **return-to-player (RTP) of 85%**:

```
gain = (1 − winChance) × lossPercent / winChance × RTP
```

That means every regular fight has a **negative expected value**: on average, the more you play, the more you lose — exactly like real games of chance. High-risk monsters pay more, but don't beat the house. The only bet in your favour is the Boss (expected value ×1.25), so the real question is: *can you get there with something left?*

The game also shows "near misses" (*O MAŁY WŁOS!*) — the kind of feedback real gambling products use to keep players going. Notice how it feels.

## 🚀 Running locally

No build step, no dependencies to install — Phaser is loaded from a CDN.

```bash
git clone https://github.com/pilarhz/Lotto-Quest.git
cd Lotto-Quest
python3 -m http.server 8000
```

Then open <http://localhost:8000>.

> Opening `index.html` directly from disk may fail to load images in some browsers, so serve the folder with any local web server (Python, `npx serve`, VS Code Live Server…).

## 📁 Project structure

```
Lotto-Quest/
├── index.html    # page shell + player-name overlay
├── main.js       # game logic: odds model, scenes, leaderboard
├── style.css     # overlay and page styling
└── assets/       # map, monsters, boss, player sprite, campfire
```

Scenes: `PreloadScene` → `MenuScene` → `GameScene` / `RulesScene` / `LeaderboardScene`.
Scores are saved in the browser's `localStorage` (key `lottoScores`), so the leaderboard is per device.

## 🛠️ Tech stack

- [Phaser 3.87](https://phaser.io/) (Arcade Physics, tweens, cameras)
- Vanilla JavaScript, HTML, CSS

## 🌐 Language

The in-game interface is in **Polish**.

---

Made with ☕ and dice at Hackathon Bydgoszcz 2025.
