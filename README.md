# Setlist

*From a natural-language request to a live-style setlist of instrumental metal and rock, with an intensity arc — built one step at a time to learn music AI hands-on.*

> **Status:** early design · first experiments on data and genre recognition.

## What it is

You write something like *"40 minutes of heavy instrumental music: slow opening, peak in the middle, long ending"* and get back an ordered setlist, the way a band builds one for a concert: openers, peaks and breathers, a closing arc.

It is also a learning path. Each capability is built as a short experiment that touches one layer of music AI:

| Step | Capability | Music AI layer |
|---|---|---|
| 0 | Corpus — how much instrumental metal/rock is in open datasets | data |
| 1 | Look & listen — spectrograms, tempo, tuning | audio representation, MIR |
| 2 | Genre and subgenre | MIR, pretrained models |
| 3 | Structure and intensity (with source separation) | MIR, evaluation |
| 4 | Search by sound | audio–text retrieval |
| 5 | Ordering with constraints | sequencing |
| 6 | Natural-language request | LLM |

## Repository layout

| Folder | Content |
|---|---|
| `requisiti.md` · `soluzione.md` · `decisioni.md` | the design: what, how, why (in Italian) |
| `raw/input/` · `raw/output/` | sources and experiment results (one folder per experiment) |
| `code/` | Python package, one script per experiment, tests |
| `data/` · `models/` | audio, datasets, pretrained models — **not versioned**, see their READMEs |
| `assets/` | diagrams (Excalidraw) |

## Running the code

Linux or WSL (Essentia has no native Windows wheels):

```bash
python -m venv .venv && source .venv/bin/activate
pip install -r code/requirements.txt
```

Download the models listed in `models/README.md`.

## Method

The repo is also an Obsidian vault run with an LLM-maintained wiki (after [Karpathy's LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f)): design, decisions and experiments live next to the code. Working rules are in `CLAUDE.md`.

## Data and licenses

Experiments use open datasets (MTG-Jamendo, DEAM) and Essentia pretrained models (CC BY-NC-SA 4.0). No audio or model files are included in this repository.
