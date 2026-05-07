# HalluciCheck – AI Hallucination Detector

A lightweight, single-file web tool that detects hallucinations, unsupported claims, and factual inconsistencies in AI-generated text using the Claude API. Simply paste any AI-generated content and HalluciCheck will analyze it in seconds — returning a hallucination risk score, flagged issues with severity levels, and an overall summary. No backend, no frameworks, no install required; it runs entirely in the browser.

## Features
- Paste any AI-generated text (ChatGPT, Gemini, Claude, etc.)
- Get a hallucination risk score (0–100)
- See flagged issues with severity levels (High / Medium / Low)
- Overall summary analysis
- No backend required — runs entirely in the browser

## Tech Stack
- Plain HTML + CSS + JavaScript
- Anthropic Claude API (`claude-sonnet-4-20250514`)
- No frameworks, no dependencies

## Live Demo
> https://yourusername.github.io/hallucicheck

---

## Deployment (GitHub Pages via Terminal)

### Prerequisites
- Git installed (`git --version`)
- A GitHub account
- Your Anthropic API key from https://console.anthropic.com

### Step 1 — Add your API key to index.html
Open `index.html` and find this line (around line 130):
```javascript
body: JSON.stringify({
```
Just above the `fetch` call, the headers object currently has no auth. Add your key:
```javascript
headers: {
  'Content-Type': 'application/json',
  'x-api-key': 'YOUR_ANTHROPIC_API_KEY_HERE',
  'anthropic-version': '2023-06-01',
  'anthropic-dangerous-direct-browser-access': 'true'
},
```

### Step 2 — Initialize Git and push to GitHub

```bash
# Navigate to your project folder
cd /path/to/your/project

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial commit - HalluciCheck"

# Create repo on GitHub (install gh CLI first if needed: https://cli.github.com)
gh repo create hallucicheck --public --source=. --push

# OR if you already created the repo manually on GitHub:
git remote add origin https://github.com/YOURUSERNAME/hallucicheck.git
git branch -M main
git push -u origin main
```

### Step 3 — Enable GitHub Pages

```bash
# Using GitHub CLI (easiest)
gh api repos/YOURUSERNAME/hallucicheck/pages \
  --method POST \
  --field source='{"branch":"main","path":"/"}'
```

Or do it manually:
1. Go to your repo on GitHub
2. Settings → Pages → Source → main branch → Save

### Step 4 — Your site is live!
```
https://YOURUSERNAME.github.io/hallucicheck
```
(Takes ~1–2 minutes to go live after enabling Pages)

---

## Project Structure
```
hallucicheck/
└── index.html    # entire app in one file
└── README.md
```

## How It Works
1. User pastes AI-generated text into the textarea
2. App sends text to Claude API with a structured prompt
3. Claude returns a JSON object with risk score, flags, and summary
4. UI renders results with color-coded severity indicators


