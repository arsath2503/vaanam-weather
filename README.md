# Vaanam (வானம்) — Weather Website

A weather website with an animated sky that reflects real conditions —
sun/moon position, clouds, and rain react to live weather data from OpenWeatherMap.

---

## Part 1 — One-time setup on your computer

### 1. Install Git
- Windows: download from https://git-scm.com/download/win and run the installer (defaults are fine)
- Check it worked by opening a terminal (Command Prompt / PowerShell) and running:
  ```
  git --version
  ```

### 2. Create a GitHub account
- Go to https://github.com/join and sign up (free)

### 3. Configure Git with your identity (one time only)
```
git config --global user.name "Mohamed Arsath Ali"
git config --global user.email "your-email@example.com"
```

---

## Part 2 — Get a free OpenWeatherMap API key

1. Go to https://openweathermap.org/api and click **Sign Up** (free)
2. After signing up, go to https://home.openweathermap.org/api_keys
3. Copy your API key (it may take 10–60 minutes to activate after signup — this is normal)

---

## Part 3 — Create the GitHub repository

1. Go to https://github.com/new
2. Repository name: `vaanam-weather`
3. Set it to **Public** (required for free GitHub Pages)
4. Do NOT initialize with a README (we already have one) — leave all checkboxes unticked
5. Click **Create repository**
6. GitHub will show you a page with commands — ignore those, use the ones below instead

---

## Part 4 — Push this project to GitHub

Open a terminal in this project folder (the one containing this README) and run:

```bash
git init
git add .
git commit -m "Initial commit: Vaanam weather app"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/vaanam-weather.git
git push -u origin main
```

Replace `YOUR-USERNAME` with your actual GitHub username.
When prompted for a password, GitHub no longer accepts your account password —
you'll need a **Personal Access Token** instead:
1. Go to https://github.com/settings/tokens → **Generate new token (classic)**
2. Tick the `repo` scope, generate it, and copy the token
3. Paste that token as your password when Git asks

---

## Part 5 — Add your API key as a GitHub secret (keeps it out of your public code)

1. In your new repo on GitHub, go to **Settings → Secrets and variables → Actions**
2. Click **New repository secret**
3. Name: `OPENWEATHER_API_KEY`
4. Value: paste the API key from Part 2
5. Click **Add secret**

---

## Part 6 — Turn on GitHub Pages

1. In your repo, go to **Settings → Pages**
2. Under "Build and deployment", set **Source** to **GitHub Actions**
3. That's it — the workflow in `.github/workflows/deploy.yml` will now run automatically

---

## Part 7 — Trigger the first deploy

Since you already pushed in Part 4, the deploy should already be running:
1. Go to the **Actions** tab in your repo
2. You should see a "Deploy Vaanam to GitHub Pages" run in progress
3. Once it finishes (green checkmark), go to **Settings → Pages** — your live URL will be shown at the top, something like:
   ```
   https://YOUR-USERNAME.github.io/vaanam-weather/
   ```

---

## Testing locally before you push (optional)

1. Copy `config.example.js` to `config.js`
2. Open `config.js` and paste your real API key in place of `PASTE_YOUR_KEY_HERE`
3. Open `index.html` directly in your browser
   (`config.js` is git-ignored, so this local key never gets committed)

---

## Making changes later

Any time you edit `index.html` (or anything else) and want the live site updated:
```bash
git add .
git commit -m "Describe what you changed"
git push
```
The GitHub Actions workflow re-deploys automatically within about a minute.

---

## Notes on the API key

OpenWeatherMap's free tier is generous for a personal project (1,000 calls/day),
but keep in mind: because this is a static site, the key is visible to anyone who
opens their browser's developer tools while visiting the live page — it is not
truly "secret" from an end user, only kept out of your public GitHub source code.
For a portfolio/personal project this is the standard, accepted approach. If you
ever want the key fully hidden even from network requests, that requires a small
server-side proxy (e.g. a Cloudflare Worker) — happy to help set that up later
if you want to go further.
