# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Running the project

No build step — open `index.html` directly in a browser, or serve it with any static file server to satisfy webcam HTTPS requirements in some browsers:

```
npx serve .
# or
python -m http.server 8080
```

There are no dependencies to install, no lint scripts, and no test suite. All libraries load from CDN at runtime.

## Architecture

Pure vanilla HTML/CSS/JS single-page app. Three files:

- `index.html` — markup and CDN script tags (TensorFlow.js + Teachable Machine Image)
- `style.css` — all styles; dark theme driven by CSS custom properties in `:root`
- `game.js` — all game logic, state, and DOM wiring

### AI / webcam flow

`game.js` loads a **Google Teachable Machine** image classification model at the URL set in `MODEL_URL`. The model must expose exactly three classes whose names match the constants `CLASS_ROCK`, `CLASS_PAPER`, `CLASS_SCISSORS` (default: `"Rock"`, `"Paper"`, `"Scissors"`).

On camera start, `predictionLoop()` runs every animation frame via `requestAnimationFrame`, calling `model.predict(webcam.canvas)` and piping probabilities to the confidence bars. When the player clicks **Play Round**, a snapshot prediction is taken, the highest-probability class becomes the player's move, and `decideWinner()` resolves the outcome.

### Game state

All state is module-level variables in `game.js`: `scorePlayer`, `scoreCpu`, `round`, `cameraReady`, `loopRunning`. Game ends when either side reaches 3 wins or `MAX_ROUNDS` (5) is reached. `resetGame()` zeroes state and restarts the prediction loop without reloading the model.

### Teachable Machine model setup

To use the game, train a model at [teachablemachine.withgoogle.com](https://teachablemachine.withgoogle.com), export it as a shareable link, and replace `YOUR_MODEL_ID` in `game.js:7` with the uploaded model URL (trailing slash required).
