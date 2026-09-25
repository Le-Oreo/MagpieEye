<div align="center">

```
███╗   ███╗ █████╗  ██████╗ ██████╗ ██╗███████╗
████╗ ████║██╔══██╗██╔════╝ ██╔══██╗██║██╔════╝
 ██╔████╔██║███████║██║  ███╗██████╔╝██║█████╗
 ██║╚██╔╝██║██╔══██║██║   ██║██╔═══╝ ██║██╔══╝
██║ ╚═╝ ██║██║  ██║╚██████╔╝██║     ██║███████╗
╚═╝     ╚═╝╚═╝  ╚═╝ ╚═════╝ ╚═╝     ╚═╝╚══════╝
           ███████╗██╗   ██╗███████╗
           ██╔════╝╚██╗ ██╔╝██╔════╝
            █████╗   ╚████╔╝ █████╗
            ██╔══╝    ╚██╔╝  ██╔══╝
           ███████╗   ██║   ███████╗
           ╚══════╝   ╚═╝   ╚══════╝
```

**The correlation engine for OSINT.** Point it at a folder of recon-tool output and it works out which scattered findings - an email here, a username there, a reused handle - all point to the **same person**, then draws it as an interactive graph.

![stage](https://img.shields.io/badge/stage-v0.1-D97706?style=for-the-badge) ![engine](https://img.shields.io/badge/engine-Python-1f6feb?style=for-the-badge) ![platform](https://img.shields.io/badge/platform-Windows-3a3a3a?style=for-the-badge) ![license](https://img.shields.io/badge/license-MIT-2ea043?style=for-the-badge)

<sub>companion to <b>BLACKHOUND</b> · crafted by <b>Oreo</b></sub>

</div>

---

## What it does

BLACKHOUND *gathers* intelligence by running tools. MAGPIEEYE *connects* what those tools found. One hunts, the other ties the threads together.

Recon tools each dump their results separately - one finds an email, another a username, another an IP. Nothing joins them up. MAGPIEEYE does that joining automatically:

1. **Reads** the output of many recon tools (JSON, CSV, plaintext - whatever they produce).
2. **Normalizes** every result into one common shape: a *finding*.
3. **Extracts** the typed identifiers (email, username, phone, domain, ip, name, handle, crypto address).
4. **Correlates** them - exact matches, fuzzy matches (`jsmith` ≈ `j.smith`), and cross-type inferences (`john@x.com` implies the username `john`).
5. **Scores** every link with a confidence value and a plain-English reason, so you can see *why* two things were connected.
6. **Outputs** an interactive graph (dots = identifiers, lines = links), plus a plaintext report and a JSON export.

> **The one hard rule:** never link two findings that belong to *different* people. A missed connection is a minor annoyance; a wrong one silently corrupts an investigation. When confidence is low, MAGPIEEYE leaves things unlinked rather than guess.

---

## Quick start

1. Double-click **`magpieeye.bat`**.
2. Press **`S`** to run the bundled sample, or **`A`** and point it at your own folder of recon output.
3. A graph opens in your browser. Dots are identifiers; solid lines are strong links, dashed lines are weaker ones. Tap any link to see why it was drawn.

No setup. On first run MAGPIEEYE finds your Python (or fetches a portable one) and installs its own libraries silently. Everything hides behind the one `.bat` - exactly like BLACKHOUND.

## Console

| key | does |
|-----|------|
| `A` | analyze a folder of recon output |
| `S` | run the bundled sample |
| `D` | doctor - what's installed here |
| `C` | settings - theme + options (saved to `magpieeye.cfg`) |
| `Q` | quit |

## Feeding it BLACKHOUND

Any text/JSON/CSV a tool writes works. Save a tool's output into a folder and point MAGPIEEYE at it. It reads the folder recursively, so a whole run's worth of dumps can go in together and come out as one combined graph.

---

## Requirements

| you need | for |
|----------|-----|
| **Windows** + a terminal | the launcher (best in **Windows Terminal**) |
| **Python 3.12** *(recommended)* | the engine - MAGPIEEYE fetches a portable one if you have none |

The engine runs on the standard library alone if it must; the optional libraries (`pydantic`, `rapidfuzz`, `networkx`, `jinja2`) just make matching sharper and are installed automatically on first run.

---

## Responsible use

MAGPIEEYE correlates data about real people. Only feed it output you gathered from **authorized** investigations, and handle what it links with the same care as the source data. It runs entirely offline and executes no third-party code - it only reads the files you give it.

<div align="center"><sub><b>MAGPIEEYE</b> - gathers every scattered thread and shows you the one who dropped them. · by Oreo</sub></div>
