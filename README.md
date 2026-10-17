<h1 align="center">🦊 Cute Foxes GIF Counter</h1>

<p align="center">
  <i>A self-hosted, animated, config-driven visitor counter for your GitHub profile.</i><br/>
  Wholesome foxgirls hold up your visit count, one fluffy digit at a time.
</p>

<p align="center">
  <img src="https://cutefoxesgifcounter.vercel.app/api/counter" width="425" alt="Cute Foxes GIF Counter" />
</p>
<p align="center">
  <sub>Live counter powered by Vercel + Upstash Redis</sub>
</p>

<p align="center">
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/0.gif" width="68" alt="0" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/1.gif" width="68" alt="1" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/2.gif" width="68" alt="2" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/3.gif" width="68" alt="3" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/4.gif" width="68" alt="4" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/5.gif" width="68" alt="5" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/6.gif" width="68" alt="6" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/7.gif" width="68" alt="7" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/8.gif" width="68" alt="8" />
  <img src="https://raw.githubusercontent.com/Olexify/CuteFoxesGIFCounter/main/FoxgirlsPack/9.gif" width="68" alt="9" />
</p>
<p align="center">
  <sub>The ten animated digits, each with its own little animation</sub>
</p>

---

## 🍂 What is this?

Static counters are fine, but a foxgirl waving a tail at every visitor is better.
You host it on Vercel, keep the count in Upstash Redis, and change everything from one config file.

```txt
🦊 Booting CuteFoxes.exe...

[OK] Asking Redis how many friends visited
[OK] Lining up foxgirls, one per digit
[OK] Wrapping everything in a cozy SVG
[INFO] Tails are wagging (working as intended)
```

---

## 🧩 Features

* 🦊 Ten pixel-art digit GIFs (0–9) stored right in the repo, in `FoxgirlsPack/`, each with its own animation
* 🕰️ Four timing variants per digit (`3.gif`, `3_1.gif`, `3_2.gif`, `3_3.gif`: different loop start and speed), so neighbouring digits, like a row of zeros, never blink in unison
* 🧸 Placeholder fox digits are drawn if a sprite is missing, so it works from the first deploy
* ⚙️ Everything configurable in `counter.config.json`
* 🎨 Opacity, brightness, contrast, saturation, shadow, scale, spacing
* 📈 Counting modes: `strict`, `unique`, `aggressive`
* ☁️ Runs on the Vercel and Upstash free tiers
* 🔒 No third-party tracking

---

## 🎞️ The animations

| Digit | What she does |
|---|---|
| 0 | blinks, flicks her ears, sways her tail |
| 1 | light glint across the sign, ear perk, happy tail wag |
| 2 | the number glows, stars twinkle, hair swish |
| 3 | hearts float up, petals drift, ears relax, long happy blink |
| 4 | fireflies, hair shine, sign sparkles, ears twitch in turn, tail-tip flick |
| 5 | a gust: petals blow across, hair/tail/ears sway, the number drifts to pink |
| 6 | humming: music notes, beat-synced ears and tail, the number hops |
| 7 | confetti pop, the number flashes gold, ears perk |
| 8 | a sparkle traces an infinity sign, bubbles float up |
| 9 | nine fox-fire flames orbit her, a crescent moon glows |

---

## 🛠️ How it works

```txt
GitHub README loads the image
        ↓
Vercel runs api/counter.js
        ↓
Redis increments the count
        ↓
Number gets padded → each digit mapped to FoxgirlsPack/<digit>.gif
        ↓
GIFs embedded into one SVG → foxgirls appear
```

## 📦 Project structure

```txt
CuteFoxesGIFCounter/
├── api/counter.js        ← serverless function
├── FoxgirlsPack/         ← 0.gif … 9.gif (also accepts .webp / .png)
├── counter.config.json   ← settings
├── package.json
└── vercel.json           ← bundles FoxgirlsPack into the function
```

---

## 🚀 Setup

### 1) Add your digit art 🎨
Put 10 files named `0.gif` … `9.gif` into `FoxgirlsPack/`. The aspect ratio must be **45:100** (the bundled set is **68×151**), with a transparent background. Optionally add timing variants named `<digit>_1.gif` … `<digit>_3.gif` and set `"variants"` in `counter.config.json`; position *i* then uses variant *i* mod *variants*. Keep each under about 65 KB: the counter embeds every digit into one SVG, so 7 digits is roughly 0.5 MB.

### 2) Upstash Redis 🗄️
Open your database in the [Upstash console](https://console.upstash.com). Under **REST API**, copy these two values:
`UPSTASH_REDIS_REST_URL` and `UPSTASH_REDIS_REST_TOKEN`.

### 3) Deploy to Vercel ▲
1. Go to [vercel.com/new](https://vercel.com/new) and import this repo.
2. Set **Framework Preset → Other**.
3. Add the two environment variables from step 2, then deploy.

### 4) Test it
Open `https://<your-project>.vercel.app/api/counter`. The site root `/` returning 404 is expected.

### 5) Embed it 🎀
```html
<p align="center">
  <img src="https://<your-project>.vercel.app/api/counter" width="425" />
</p>
```

---

## ⚙️ Configuration

```json
{
  "counterKey": "counter:Olexify",
  "digits": 7,
  "assetsDir": "FoxgirlsPack",
  "style": {
    "opacity": 0.8, "brightness": 0.9, "contrast": 1.25, "saturate": 1,
    "scale": 1, "spacing": 0, "offsetY": 0,
    "shadowOpacity": 0.58, "shadowBlur": 0.7, "shadowOffsetX": 2.5, "shadowOffsetY": 3.5,
    "bgOpacity": 0, "rounded": 0, "bgColor": "#000000"
  },
  "counting": { "mode": "strict", "cooldownSeconds": 0, "bump": 1 }
}
```

| Mode | Behavior |
|---|---|
| `strict` | +1 on every request (GitHub's image cache still limits how often this fires) |
| `unique` | +1 per IP per `cooldownSeconds` window |
| `aggressive` | +`bump` per request, handy for carrying over a count from another counter |

`counterKey` is the Redis key that stores the count. To keep an existing count, point it at the old key.

---

## 🩹 Troubleshooting

| Symptom | Fix |
|---|---|
| "No entrypoint found" | Set the preset to **Other**. The function must be at `api/counter.js` |
| 500 error | Env vars are missing or wrong, or the config JSON is invalid. Check the Vercel logs |
| Orange placeholder digits | That digit's file is missing from `FoxgirlsPack/` |
| Count updates slowly on GitHub | GitHub caches images through its camo proxy. Open the endpoint directly to test |

---

<p align="center">
  <i>"Every visitor gets a tail wag. That's the rule." 🦊✨</i>
</p>
