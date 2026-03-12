# Research Gym 🏋️

A single-file web app for training your research brain. Designed for ML/AI researchers who want to read more actively, think more sharply, and actually remember what they learn.

---

## What it is

**12 training machines**, each targeting a different research skill:

| Machine | What it trains |
|---|---|
| 📄 Paper Speed-Run | Fast comprehension — key claims in 5 min |
| 🥊 Claim Fighter | Critical reading — what's actually supported |
| 🔬 Method Auditor | Experimental design and confound spotting |
| 🧠 Explain It | Understanding depth — explain to a non-expert |
| 💡 Hypothesis Engine | Generative thinking from existing results |
| 🔁 Reverse Engineer | Working backward from results to methods |
| 🔥 Kill Your Idea | Steel-manning — find the holes in your own work |
| 🔮 Future Scenarios | Extrapolation and implication reasoning |
| 💻 Code Architect | PyTorch fluency — daily rotating code concepts |
| 📖 Vocab Builder | Flashcard deck with math-heavy definitions |
| 🔭 Deep Dive | Slow reading and synthesis practice |
| ✍️ Sharp Writer | Technical writing and clarity |

**Locker Room** — your personal space:
- **Focus** — weekly research question + end-of-session reflection, with collapsible history
- **Scratch Pad** — freeform ideas notepad, auto-saves as you type
- **Library** — papers you want to read, add manually or star from the lobby
- **Progress Wall** — machine usage stats and streaks
- **Full Log** — every session entry, exportable as JSON

---

## Setup

### Option 1 — Just open the file
Download `index.html` and open it in any browser. Done.

### Option 2 — Host on GitHub Pages
1. Fork this repo (or create a new one and upload `index.html`)
2. Go to **Settings → Pages → Source** → `main` branch, `/root`
3. Your site will be live at `https://yourusername.github.io/research-gym`

---

## API key

The app uses the [Anthropic API](https://console.anthropic.com) to generate exercise prompts and feedback. You'll need your own key.

1. Get a key at [console.anthropic.com](https://console.anthropic.com)
2. Paste it into the app on first launch
3. It's saved to your browser's localStorage — never sent anywhere else

The app calls the API directly from your browser using the `anthropic-dangerous-direct-browser-access` header. Your key stays local.

Typical usage is light — a few hundred tokens per exercise. A $5 credit goes a long way.

---

## Vocab cards

The built-in deck has ~24 terms with full math definitions (KL divergence, GRPO, LoRA, Flash Attention, etc.).

To add your own terms:
1. Go to **Vocab Builder → ↓ Export** to download the current deck as JSON
2. Edit the file — each entry is just `{ "term": "...", "def": "...", "related": "..." }`
3. Hit **↑ Import** to load it back

Custom terms persist in localStorage and survive page reloads.

Example format:
```json
[
  {
    "term": "GRPO",
    "def": "Group Relative Policy Optimization. Replaces PPO's value network with group-normalized advantage...",
    "related": "PPO · RLHF · DeepSeek-R1"
  }
]
```

---

## Data & privacy

Everything is stored in your browser's `localStorage`. Nothing is sent to any server except:
- Anthropic API calls when you submit an exercise (your text + the paper abstract)

To export your data: **Locker Room → Full Log → ⬇ Export JSON**

To wipe everything: **Locker Room → Full Log → (scroll to bottom) → Clear all data**

---

## Things to know

- **ArXiv fetch** — the lobby auto-fetches papers on load via a CORS proxy. If it fails, paste any abstract directly into a machine using the "Paste your own paper" toggle, or add papers manually in the Library tab.
- **Single file** — the entire app is one HTML file with no external dependencies except Google Fonts and the Anthropic API. It will work offline except for AI feedback and ArXiv fetching.
- **No account needed** — your data is yours, in your browser.

---

## Stack

- Vanilla JS + HTML + CSS
- [Anthropic Messages API](https://docs.anthropic.com/en/api/messages) (`claude-sonnet-4-20250514`)
- [ArXiv API](https://arxiv.org/help/api) for paper fetching
- [allorigins.win](https://allorigins.win) as CORS proxy for ArXiv
- Google Fonts: Figtree + IBM Plex Mono
