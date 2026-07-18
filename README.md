# Crystal Caverns - A Phaser Platformer

A retro-style platformer game built with Phaser 3, deployable on GitHub Pages.

## Features

- Character selection: play as Max the Dragon, Riley the Axolotl, Mommy the Bear, or Daddy the Turtle
- 3 levels of increasing difficulty
- Player movement with double-jump ability
- Collectible coins (10 pts) and crystals (50 pts)
- Patrolling enemies you can stomp or avoid
- Spike hazards and gaps to jump over
- Score tracking and 3-life system
- Pause functionality (P key)
- Background music with on/off toggle (M key or menu buttons)
- Procedural sound effects (jump, coins, crystals, stomps, damage, and more) with on/off toggle
- Jellyfish background artwork
- Main menu, game over, and victory screens
- All character and level graphics generated procedurally

## Controls

| Key | Action |
|-----|--------|
| A / Left Arrow | Move Left |
| D / Right Arrow | Move Right |
| W / Up Arrow / Space | Jump (press twice for double jump) |
| P | Pause / Resume |
| M | Music On/Off |
| 1-4 | Select character (on character select screen) |

## Play Locally

You need a local web server because the game loads JavaScript modules.

### Option 1: Python (already installed on Raspberry Pi)

```bash
cd phaser-platformer
python3 -m http.server 8080
```

Open your browser to `http://localhost:8080`

### Option 2: Node.js

```bash
cd phaser-platformer
npx serve -p 8080
```

Open your browser to `http://localhost:8080`

### Option 3: VS Code

Install the "Live Server" extension, right-click `index.html`, and select "Open with Live Server".

## Deploy to GitHub Pages

1. Create a new repository on GitHub (e.g., `crystal-caverns`)

2. Initialize git and push the code:

```bash
cd phaser-platformer
git init
git add .
git commit -m "Initial commit - Crystal Caverns platformer"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/crystal-caverns.git
git push -u origin main
```

3. Enable GitHub Pages:
   - Go to your repository on GitHub
   - Click **Settings** > **Pages**
   - Under "Source", select **Deploy from a branch**
   - Select **main** branch and **/ (root)** folder
   - Click **Save**

4. Wait 1-2 minutes, then visit:
   ```
   https://YOUR_USERNAME.github.io/crystal-caverns/
   ```

## Project Structure

```
phaser-platformer/
├── index.html          # Main HTML file
├── style.css           # Page styling
├── README.md           # This file
├── assets/
│   ├── bg_jellies.jpeg     # Background artwork
│   └── music_jellyfish.mp3 # Background music
└── js/
    ├── config.js       # Phaser game configuration + character roster
    ├── sfx.js          # Sound effects (procedural) + music/toggle helpers
    ├── scene_boot.js   # Boot scene - loads assets, generates all textures
    ├── scene_menu.js   # Main menu scene
    ├── scene_charselect.js # Character selection scene
    ├── scene_play.js   # Main gameplay scene (levels, player, enemies)
    ├── scene_gameover.js  # Game over screen
    └── scene_victory.js   # Victory screen
```

## Customization

### Add a new level

Add a new level object to the `levels` array in `js/scene_play.js` inside `getLevelData()`:

```javascript
{
    width: 1920,
    platforms: [
        { x: 160, y: 440 },
        { x: 320, y: 360 },
    ],
    coins: [
        { x: 224, y: 400 },
    ],
    crystals: [
        { x: 784, y: 250 },
    ],
    enemies: [
        { x: 540, y: 370, minX: 500, maxX: 620, speed: 50 },
    ],
    spikes: [
        { x: 640, y: GAME_HEIGHT - TILE_SIZE - 20 },
    ],
    gaps: [
        { x: 640, width: TILE_SIZE * 2 },
    ],
    door: { x: 1840, y: GAME_HEIGHT - TILE_SIZE - 56 }
}
```

Update `this.maxLevel` in the `init()` method of `ScenePlay`.

### Change player speed

In `js/scene_play.js`, look for `setVelocityX(-180)` (left) and `setVelocityX(180)` (right).

### Change jump height

In `js/scene_play.js`, look for `setVelocityY(-400)` (first jump) and `setVelocityY(-380)` (double jump).

### Change gravity

In `js/config.js`, modify `gravity: { y: 600 }`.

## Tech Stack

- [Phaser 3.80.1](https://phaser.io/) - HTML5 game framework
- Vanilla JavaScript (no build step required)
- All graphics generated with Phaser's Graphics API

## License

MIT - feel free to use, modify, and share!
