# ⚡ Crypto Volatility Tracker Terminal

![Dashboard Preview](./preview.gif)

## About

**Crypto Volatility Tracker Terminal** is an advanced, interactive dashboard for spotting abnormal volatility in cryptocurrency markets, wrapped in a dark cyberpunk / fintech interface inspired by modern trading terminals.

Instead of relying on a fixed percentage threshold, the dashboard compares each coin's latest move against *its own* recent behavior. A 1.5% jump is routine for one asset and a red flag for another, and the terminal tells the difference in real time.

The entire project is a single `index.html` file. There is no backend, no build step and no API keys.

> **Note:** this version runs on a built-in market simulator, so all prices on screen are generated locally for demonstration purposes and are not real quotes.

## Key Features

- **Live charts (Chart.js):** 24-hour sparklines on every coin card, a multi-asset price history chart (30 min / 1 h / 3 h), a Z-score bar chart with threshold lines, and a per-coin detail view that plots price together with minute-by-minute volatility.
- **Smart volatility alerts:** compares the current price with the price *X* minutes ago (3, 5, 10 or 15 min) and scores the move with a Z-score against the coin's own baseline. Anomalies trigger a pulsing green/red card glow, a banner, a toast notification, an entry in the alert log and an optional sound. A minimum-move filter and per-coin cooldown keep the signal clean.
- **Adjustable sensitivity:** change the comparison window and the anomaly threshold on the fly and see the table and charts recalculate instantly.
- **Autonomous live engine:** a self-contained market engine runs entirely in the browser, with no external API calls. It is therefore immune to CORS blocks, rate limits and API outages, and it works the same on `file://`, localhost and GitHub Pages.
- **Responsive design (Tailwind CSS):** a glass-style dark UI that adapts from mobile to wide desktop screens, with an animated countdown ring, price flash effects and reduced-motion support.

## Tech Stack

| Layer | Technology |
|---|---|
| Markup | HTML5 |
| Styling | Tailwind CSS (via CDN) |
| Logic | JavaScript (ES6+), no frameworks |
| Charts | Chart.js 4 |
| Audio alerts | Web Audio API |

## Quick Start

No servers, no package managers and no dependencies to install.

1. Download or clone this repository.
2. Open `index.html` in any modern browser.

```bash
git clone https://github.com/<Urbanexxx>/<crypto-volatility-tracker>.git
cd <crypto-volatility-tracker>
# then simply open index.html in your browser
```

An internet connection is only needed to load the Tailwind CSS, Chart.js and font files from their CDNs. To publish the dashboard, enable **GitHub Pages** for the repository and point it at the root folder.

## How the Volatility Score Works

1. Take the log return between the current price and the price *X* minutes ago.
2. Measure the coin's normal one-minute movement over the preceding hour, using a robust estimator (median absolute deviation) so earlier spikes do not dull the detector.
3. Scale that baseline to the chosen window and compute `Z = R / (σ · √X)`.
4. Flag an **anomaly** when `|Z|` passes the chosen threshold and the move exceeds 0.25%, and an **elevated** state one step below it.

## Disclaimer

This is a portfolio and educational project. It does not provide financial advice, and the data shown is simulated.
