# Thermo3D: 3D Temperature Converter

A fast, free, no-signup temperature converter with a live 3D thermometer.
Converts **Celsius, Fahrenheit, Kelvin and Rankine** in real time.
Pure static site: no build step, no backend, no dependencies to install.

## Why it is useful
| Who | How they use it |
|---|---|
| Students & teachers | See how units relate; the thermometer and water-state label make physics visual |
| Cooks & bakers | Oven presets and instant °C ↔ °F |
| Travellers | Understand weather forecasts in another country |
| Engineers, lab & HVAC staff | Kelvin/Rankine support and absolute-zero validation (below −273.15 °C is rejected) |
| Developers / portfolio | Example of Three.js + vanilla JS, deployable in minutes |

## What is in this folder
```
index.html     the whole app (HTML + CSS + JS, 3D via Three.js from cdnjs)
404.html       friendly not-found page
vercel.json    clean URLs + security headers for Vercel
robots.txt     allow search engines
.gitignore
```

## User guide (end to end)
1. **Type a number** in any box (Celsius, Fahrenheit, Kelvin or Rankine). The other three update instantly.
2. **Drag the slider** (−50 to 150 °C) to watch the 3D thermometer, particles and background colour change.
3. **Tap a preset** (Absolute zero, Freezing, Fridge, Room, Body, Boiling, Oven) for common values.
4. **Choose decimals** (0–4) to control rounding.
5. **Copy** a value with the Copy button above each field.
6. **Save** a conversion; it appears under *History* (kept in your browser only). Click a saved row to restore it.
7. **Clear all** empties every field. **◐** toggles light/dark theme.
8. If you see *"Below absolute zero"*, the value is physically impossible. Enter a higher number.

Formulas: F = C×9/5 + 32 · K = C + 273.15 · R = (C + 273.15)×9/5

## Run locally
Just double-click `index.html`, or serve it:
```bash
npx serve .          # or: python3 -m http.server 8000
```

## Deploy option A: GitHub Pages (free)
1. Create a new GitHub repo (e.g. `thermo3d`) and upload every file in this folder (or `git push`).
   ```bash
   git init && git add . && git commit -m "Thermo3D"
   git branch -M main
   git remote add origin https://github.com/<you>/thermo3d.git
   git push -u origin main
   ```
2. Repo → **Settings → Pages**.
3. *Source*: **Deploy from a branch** → branch **main**, folder **/ (root)** → **Save**.
4. After ~1 minute your site is live at `https://<you>.github.io/thermo3d/`.

## Deploy option B: Vercel (free Hobby plan)
**Dashboard way**
1. Push the folder to GitHub (steps above).
2. Go to vercel.com → **Add New → Project** → import the repo.
3. Framework preset: **Other**. Leave build command and output directory empty. Click **Deploy**.
4. You get `https://thermo3d-<hash>.vercel.app`. Every `git push` redeploys automatically.

**CLI way**
```bash
npm i -g vercel
vercel          # preview deploy
vercel --prod   # production deploy
```

**Custom domain:** Vercel project → **Settings → Domains** (or GitHub Pages → Custom domain) and follow the DNS instructions.

## Monitoring traffic, logs and errors

### On Vercel
| Need | Where |
|---|---|
| **Visitors, page views, countries, devices, referrers** | Project → **Analytics** tab → click *Enable* (the tracking script is already in `index.html`). Data appears after the first visits on the *deployed* site |
| **Request and bandwidth usage** | Project → **Observability** (or **Usage**) |
| **Deployment & build logs** | Project → **Deployments** → open a deployment → **Build Logs** |
| **Request logs** | Project → **Logs**. Note: this is a static site with no server code, so logs mostly show deployment events and requests, not application logs |
| **Alerts** | Project → **Settings → Notifications** for failed deployments |

Plan limits change; check Vercel's current pricing page for Hobby-plan analytics limits.

### On GitHub Pages
- **Repo → Insights → Traffic** shows views/clones of the *repository*, not visitors to the website.
- GitHub Pages gives no visitor analytics or server logs. Add a free privacy-friendly tool such as **Cloudflare Web Analytics**, **Plausible** or **GoatCounter** by pasting their one-line script into `index.html` just before `</head>`.
- Deployment status/logs: repo → **Actions** tab.

### Browser errors (any host)
Open the site → press **F12** → **Console**. If the 3D scene is blank, check that your network allows `cdnjs.cloudflare.com`; the converter still works without 3D.

## Updating the site
Edit `index.html` → commit → push. Both GitHub Pages and Vercel redeploy automatically.

## Troubleshooting
| Problem | Fix |
|---|---|
| Blank page on GitHub Pages | Confirm Pages source is `main` / root and the file is named exactly `index.html` |
| 3D thermometer missing | WebGL disabled or CDN blocked; converter still works |
| `/_vercel/insights/script.js` 404 in console | Normal on GitHub Pages or local; the script exists only on Vercel with Analytics enabled |
| History disappeared | It is stored per browser; clearing site data removes it |

## Tech
Vanilla JavaScript, CSS, Three.js r128 (cdnjs). No cookies, no accounts; history stays in your browser's localStorage.
