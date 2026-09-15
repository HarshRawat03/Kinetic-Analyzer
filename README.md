# Reaction Kinetics Analyzer

An interactive, client-side kinetics tool for undergraduate Chemical Reaction Engineering — built with a futuristic, neon HUD-style interface: enter or import concentration–time data, analyze it with the **integrated** or **differential** rate-law method (or let **auto-detect** estimate the order for you), run an **Arrhenius analysis** across multiple temperatures, and export a complete lab report — all running entirely in the browser, no backend required.

**Live demo:** https://harshrawat03.github.io/Kinetics_Analyzer/

---

## Features

**Data input**
- Manual entry in an editable table, CSV import, or one-click example datasets (zero/first/second order, plus a noisy "unknown order" dataset)
- Configurable time and concentration units, experiment name and temperature metadata

**Analysis methods**
- **Integrated rate law** — fits `[A]` vs `t` directly, for orders 0, 1, 2, 3, or any custom (including fractional) order `n`
- **Differential rate law** — estimates instantaneous rate by finite differences and fits `rate = k·Cⁿ`
- **Auto-detect** — regresses `ln(rate)` vs `ln(C)` to estimate the reaction order without assuming one, then cross-checks it against the best integrated fit
- 95% confidence intervals on every fitted rate constant, and color-coded R² so fit quality is visible at a glance

**Arrhenius analysis**
- Combine rate constants from experiments at different temperatures to estimate activation energy `Eₐ` and the pre-exponential factor `A`, with a live `ln k` vs `1/T` plot

**Visualization & reporting**
- Hand-rolled SVG charts (observed vs. predicted, linearized fit, residuals, all-orders comparison, rate profiles)
- A generated text report covering method, parameters, conclusion, and (when available) the Arrhenius results — exportable as `.txt` or printable directly from the browser

**Interface**
- A guided six-step, single-page flow (Data → Method → Results → Charts → Report → Arrhenius) with a sticky step navigator, back/continue controls, and left/right arrow-key navigation

## Tech stack

Plain HTML, CSS and JavaScript — no frameworks, no build step, no dependencies. All math (regression, finite differences, statistics) is implemented from scratch in `index.html`.

## Running it locally

This is a single static file — no server or install step needed.

```bash
git clone https://github.com/HarshRawat03/Reaction_Kinetics_Analyzer1.git
cd Reaction_Kinetics_Analyzer1
open index.html   # or just double-click the file
```

## Deploying to GitHub Pages

1. Push `index.html` (and this `README.md`) to the `main` branch of your repository.
2. On GitHub, go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source** to `Deploy from a branch`, branch `main`, folder `/ (root)`, then **Save**.
4. GitHub will publish the site at `https://<your-username>.github.io/<repo-name>/` within a minute or two — re-push any time you edit `index.html` to redeploy.

## Project structure

```
.
├── index.html   # the entire application (markup, styles, and logic)
├── README.md
└── LICENSE
```

## Scientific method summary

For an order-`n` reaction, `rate = -d[A]/dt = k[A]ⁿ`:

| Order | Integrated form | Differential form |
|---|---|---|
| 0 | `[A] = [A]₀ − kt` | `rate = k` |
| 1 | `ln[A] = ln[A]₀ − kt` | `rate = k[A]` |
| 2 | `1/[A] = 1/[A]₀ + kt` | `rate = k[A]²` |
| 3 | `1/[A]² = 1/[A]₀² + 2kt` | `rate = k[A]³` |
| n (general) | `[A]^(1−n) = [A]₀^(1−n) + (n−1)kt` | `rate = k[A]ⁿ` |

Auto-detect estimates `n` from the slope of `ln(rate)` vs `ln[A]` — no order is assumed. The Arrhenius page fits `ln k = ln A − (Eₐ/R)(1/T)` across rate constants measured at different temperatures.

R² (or fit quality) supports comparing candidate models but does not, on its own, prove a reaction mechanism — residual patterns, replicate runs and chemical context should also be considered.

## Author

**Harsh Rawat** · B.Tech Chemical Engineering, IIT Jammu · Chemical Reaction Engineering

## License

MIT — see [LICENSE](./LICENSE).
