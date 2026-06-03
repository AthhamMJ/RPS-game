# AI Rock Paper Scissors

A browser-based Rock Paper Scissors game that uses your webcam and a [Google Teachable Machine](https://teachablemachine.withgoogle.com) image classification model to detect your hand gesture in real time.

## How it works

- Your webcam feed is continuously analyzed by a TensorFlow.js model trained on Teachable Machine
- Confidence bars show live predictions for Rock, Paper, and Scissors
- Click **Play Round** to lock in your current gesture — the CPU picks randomly
- First to 3 wins (best of 5 rounds)

## Running locally

No install needed. Open `index.html` directly in a browser, or use a local server (required for webcam in some browsers):

```bash
npx serve .
# or
python -m http.server 8080
```

Then visit `http://localhost:8080`.

## Using your own Teachable Machine model

1. Go to [teachablemachine.withgoogle.com](https://teachablemachine.withgoogle.com) and create an **Image Project**
2. Create exactly 3 classes named `Rock`, `Paper`, and `Scissors` — train with your hand gestures
3. Click **Export Model → Upload (shareable link)** and copy the URL
4. In `game.js`, replace the `MODEL_URL` value with your link (keep the trailing slash):

```js
const MODEL_URL = "https://teachablemachine.withgoogle.com/models/YOUR_MODEL_ID/";
```

## Forking this project

1. Click **Fork** on the [GitHub repository](https://github.com/ratheesk/rps-game)
2. Clone your fork:

```bash
git clone https://github.com/YOUR_USERNAME/rps-game.git
cd rps-game
```

3. Train your own Teachable Machine model and update `MODEL_URL` in `game.js` as described above
4. Open `index.html` in a browser — done!

To push changes back to your fork:

```bash
git add .
git commit -m "your message"
git push origin main
```

## Tech stack

- Vanilla HTML / CSS / JavaScript — no framework, no build step
- [TensorFlow.js](https://www.tensorflow.org/js) — runs the model in the browser
- [Teachable Machine Image](https://github.com/googlecreativelab/teachablemachine-community/tree/master/libraries/image) — webcam + model wrapper
- Google Fonts: Syne + DM Sans
