<div align="center">

# 🤖 QuizBot — SmartBook Solver

[![Releases](https://img.shields.io/badge/Releases-Latest-blue?style=flat-square&logo=github)](https://github.com/aerix-official/smartbook-solver/releases)
[![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)](https://github.com/aerix-official/smartbook-solver/blob/main/LICENSE)
[![Downloads](https://img.shields.io/github/downloads/aerix-official/smartbook-solver/total?style=flat-square&label=Downloads&color=orange)](https://github.com/aerix-official/smartbook-solver/releases)

*A powerful Chrome extension that automatically solves **McGraw-Hill SmartBook** assignments using Claude API or free AI tabs.*

[Features](#-features) • [Supported Types](#-supported-question-types) • [Installation](#-installation) • [Setup](#-setup) • [Usage](#-usage) • [Disguise](#-sticky-notes-disguise)

</div>

---

## 🚀 Features

* **⚡ Dual AI Mode** — Use high-speed Anthropic API keys or leverage free ChatGPT, Gemini, and DeepSeek tabs.
* **🤖 Full Automation** — Detects questions, submits answers, selects confidence, and advances automatically.
* **✅ Universal Support** — Handles all SmartBook types: Multiple Choice, T/F, Multi-Select, Fill-in-the-Blank, and Text Selection.
* **🧩 Matching Specialist** — Fully automated matching questions via keyboard-based drag-and-drop simulation.
* **📈 Double Credit Mode** — Unique feature that duplicates the tab to answer questions twice for maximum credit.
* **🧠 Correction Recovery** — Learns from mistakes. If an answer is marked wrong, QuizBot uses that feedback for the next attempt.
* **⚙️ Customizable Workflow** — Randomize confidence levels or use "Pause Before Submit" for manual oversight.
* **🛡 Alt+Z Stealth Toggle** — Instantly hide the in-page QuizBot button on SmartBook; press again to bring it back.
* **🗒 Sticky Notes Disguise** — The popup and settings page open as a working sticky-notes app. Type the unlock code and press **Delete** to reveal the real UI. The extension is also listed as "Sticky Notes" in the manifest.

---

## 🛠 Supported Question Types

| Type | Description |
|---|---|
| **Multiple Choice** | Selects the correct radio button |
| **True / False** | Clicks True or False |
| **Multiple Select** | Checks all correct checkboxes |
| **Fill in the Blank** | Types answer(s) into the input field(s) |
| **Select Text** | Clicks the correct highlighted text segment |
| **Matching** | Keyboard drag-and-drop to align prompts with choices |

---

## 📥 Installation

1. **Download** or clone this repository to your local machine.
2. Open Chrome and navigate to `chrome://extensions/`.
3. Enable **Developer mode** (toggle in the top-right corner).
4. Click **Load unpacked** and select the `QuizBot - Extension` folder.
5. The extension will now appear in your toolbar — it's listed as **Sticky Notes** by default (see [Sticky Notes Disguise](#-sticky-notes-disguise) below).

---

## 🤖 AI Modes & Cost

| Mode | How it works | Cost |
|---|---|---|
| **Claude API** | Direct background calls (Fastest) | Anthropic API Rates |
| **ChatGPT** | Automated typing into ChatGPT tab | **Free** |
| **Gemini** | Automated typing into Gemini tab | **Free** |
| **DeepSeek** | Automated typing into DeepSeek tab | **Free** |

---

## ⚙️ Setup

### 1. Claude API Mode (Recommended)
*Fastest performance, no tab switching required.*
1. Get an API key from [console.anthropic.com](https://console.anthropic.com).
2. Click the **Sticky Notes** toolbar icon, type the [unlock code](#-sticky-notes-disguise) into a note, then press **Delete**.
3. Click **Settings ⚙** (settings page also opens as a notes app — unlock it the same way).
4. Paste your key (starts with `sk-ant-`) and click **Save Key**.
5. Set the mode to **Claude** in the main popup.

### 2. Tab AI Mode (Free)
1. Open [ChatGPT](https://chatgpt.com), [Gemini](https://gemini.google.com), or [chat.deepseek.com](https://chat.deepseek.com) and log in.
2. Click the **QuizBot Icon** and select your active AI provider.
3. The status bar will confirm the tab is detected.

---

## 📖 Usage

1. Open a **McGraw-Hill SmartBook** assignment.
2. Look for the **QuizBot** button in the header bar.
3. Click **QuizBot** to start automation.
4. To stop at any time, click the button again (labeled **Stop QuizBot**).

### ⌨ Keyboard Shortcuts

| Shortcut | Action |
|---|---|
| `Alt + S` | Open the extension popup (Sticky Notes disguise) |
| `Alt + Z` | Hide / show the in-page QuizBot button on SmartBook |

---

## 🗒 Sticky Notes Disguise

The extension hides itself behind a fully-functional sticky-notes app. Anyone glancing at your toolbar, popup, or settings page sees a casual notes app — only the right combo unlocks the real UI.

### What it looks like
* **Manifest name** is `Sticky Notes` with a generic description ("A simple sticky notes app for quick thoughts, reminders, and lists.").
* **Popup** opens as a single-note pad with a yellow paper, color picker (5 colors), Save/Delete buttons, a paginator for switching between notes, and a `+` button to add new ones.
* **Settings page** opens as a full notes app — sidebar with note list and search, large editor with title and "last edited" timestamp, color picker, and Save/Delete in the footer.
* Notes really save (to `localStorage`), so the disguise works even if someone pokes around.
* Real SmartBook Solver UI lives in the DOM but stays hidden until you unlock.

### Unlocking
1. Type **`200606`** as the entire content of the current note.
2. Press **`Delete`**.
3. The notes app slides away and the real UI appears.

The unlock is **session-only** — close the popup or reload the settings tab and the notes app comes back.

### Customising
* **Change the code** — edit `UNLOCK_CODE` at the top of [`disguise/notes.js`](disguise/notes.js).
* **Change the icon** — swap `quizbot_logo.png` (or update the paths in `manifest.json`'s `icons` and `action.default_icon` blocks) for a notes-looking icon.
* **Change the unlock trigger** — by default the code must be the entire content of a note before pressing Delete. You can adjust the check in `deleteCurrent()` inside `notes.js` (e.g. accept partial matches, require Save instead, etc.).
* **Disable the disguise** — in `popup/popup.html` / `options/options.html`, remove the `<div id="notesShell">…</div>` block and remove the `hidden` attribute from `<div id="appShell">`.

> ⚠ The unlock code lives in plain text inside `disguise/notes.js`. Anyone who unzips the extension can read it. The disguise is for casual over-the-shoulder concealment, not security.

---

## 🛡 Disclaimer

This tool is for educational purposes only. Use it responsibly and be aware of your institution's academic integrity policies. QuizBot is an independent project and is not affiliated with or endorsed by McGraw Hill.

---

<div align="center">
  <sub>Built for efficiency. Use responsibly.</sub>
</div>
