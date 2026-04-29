# QuizBot — SmartBook Solver

A Chrome extension that automatically solves **McGraw-Hill SmartBook** assignments. Supports two AI modes: call Claude directly in the background (no tab switching), or route questions through a free ChatGPT, Gemini, or DeepSeek tab.

---

## Features

- **Dual AI mode** — use your own Anthropic API key for instant background answers, or use a free ChatGPT/Gemini/DeepSeek tab
- **Full automation** — detects questions, submits answers, clicks confidence, and advances to the next question automatically
- **All SmartBook question types** supported (see table below)
- **Matching questions** — fully automated with keyboard-based drag-and-drop simulation
- **Confidence button fix** — multi-strategy detection with proper Angular click events (the original auto-mcgraw extension was broken here)
- **Double Credit Mode** — duplicates the SmartBook tab and answers each question twice for double completion credit
- **Correction recovery** — learns when an answer is marked wrong and uses that feedback on the next attempt
- **Random Confidence** — randomizes High/Medium/Low confidence selection
- **Pause Before Submit** — fills the answer but waits for you to manually click confidence

---

## Supported Question Types

| Type | Description |
|---|---|
| Multiple Choice | Selects the correct radio button |
| True / False | Clicks True or False |
| Multiple Select | Checks all correct checkboxes |
| Fill in the Blank | Types answer(s) into the input field(s) |
| Select Text | Clicks the correct highlighted text segment |
| Matching | Keyboard drag-and-drop to align prompts with choices |

---

## AI Modes

| Mode | How it works | Cost |
|---|---|---|
| **Claude API** | Calls Anthropic directly in the background — fastest, no tab switching | API usage (see below) |
| **ChatGPT** | Types into an open ChatGPT tab and reads the response | Free |
| **Gemini** | Types into an open Gemini tab and reads the response | Free |
| **DeepSeek** | Types into an open DeepSeek tab and reads the response | Free |

---

## Installation

1. Download or clone this folder to your computer
2. Open Chrome and go to `chrome://extensions`
3. Enable **Developer mode** (toggle in the top-right)
4. Click **Load unpacked** and select the `QuizBot - Extension` folder
5. The QuizBot icon will appear in your toolbar

---

## Setup

### Claude API Mode (recommended)

1. Go to [console.anthropic.com](https://console.anthropic.com) and create an account
2. Generate an API key (starts with `sk-ant-`)
3. Click the QuizBot icon → **⚙ Settings**
4. Paste your key in the **API Key** field and click **Save Key**
5. Click **Test Key** to confirm it works
6. In the popup, make sure **Claude** is the selected AI mode

### Tab AI Mode (free)

1. Open [chatgpt.com](https://chatgpt.com), [gemini.google.com](https://gemini.google.com), or [chat.deepseek.com](https://chat.deepseek.com) in a browser tab and log in
2. Click the QuizBot icon and select the matching AI mode button
3. The status bar will confirm the tab is detected

---

## Usage

1. Navigate to a SmartBook assignment in Chrome
2. A **QuizBot** button will appear in the SmartBook header bar
3. Click **QuizBot** to start automation — it will work through every question automatically
4. Click it again (it shows "Stop QuizBot") to stop at any time

The extension also adds a **⚙ settings** button next to the QuizBot button for quick access.

---

## Popup Reference

| Control | Description |
|---|---|
| Mode buttons (Claude / ChatGPT / Gemini / DeepSeek) | Select which AI to use |
| Status bar | Shows whether the API key is set or the AI tab is open |
| **High / Medium / Low** pills | Default confidence level to click |
| **Randomize confidence** | Randomly picks a confidence level each question |
| **Double Credit Mode** | Answer each question twice using a duplicated tab |
| **Pause Before Submit** | Fill answer but wait for manual confidence click |
| **⚙** (gear icon) | Opens the full Settings page |

---

## Settings Page

### API Configuration
| Setting | Description |
|---|---|
| **API Key** | Your Anthropic API key |
| **Model** | Claude Sonnet 4.6 (fast, recommended) or Claude Opus 4.7 (highest accuracy) |
| **Max Output Tokens** | Token limit per answer (1024 recommended) |

### Behavior
| Setting | Description |
|---|---|
| **Double Credit Mode** | Duplicates the tab and submits each question twice |
| **Random Confidence** | Randomly selects High, Medium, or Low each time |
| **Pause Before Submit** | Fills answer but pauses before clicking confidence |
| **Default Confidence Level** | Which button to click when not randomizing |

---

## API Cost (Claude mode only)

| Model | Input | Output | Cache reads |
|---|---|---|---|
| Claude Sonnet 4.6 | $3 / MTok | $15 / MTok | $0.30 / MTok |
| Claude Opus 4.7 | $15 / MTok | $75 / MTok | $1.50 / MTok |

Most SmartBook questions use well under 1,000 tokens. The Settings page shows a running usage estimate. Real billing is shown in your [Anthropic console](https://console.anthropic.com).

---

## How It Works

1. The extension detects a SmartBook question in `.probe-container`
2. Parses the question type, text, and all answer options
3. Sends the question to the selected AI (directly via API or via an open tab)
4. Receives a JSON response `{ "answer": "...", "explanation": "..." }`
5. Fills in the answer using native browser click/input events compatible with Angular's change detection
6. Polls until the confidence buttons become enabled (they're disabled until an answer is selected)
7. Clicks the correct confidence button using a full Angular-compatible mouse event sequence
8. Waits for the Next button to appear and clicks it
9. Repeats for the next question

---

## Notes

- Works on `learning.mheducation.com` (SmartBook)
- Matching questions use keyboard simulation (Space to lift, Arrow keys to move, Space to drop) — this mirrors how a user would drag items with a keyboard
- If a matching question can't be automated, it shows you the suggested matches and resumes once you advance manually
- The extension has no backend — all data stays between your browser and the selected AI service
