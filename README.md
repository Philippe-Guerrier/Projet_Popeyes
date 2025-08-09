# Popeyes IS — Tkinter Click & Collect + Prize Wheel

Academic project (Sorbonne, S2 S2IE): a small **Tkinter** application that simulates a fast‑food **Click & Collect** flow and an animated **Prize Wheel**.  
Users select a pickup restaurant, spin a wheel, and receive a reward based on configurable probabilities.

---

## Learning Objectives

- Model a simple user journey (Home → Click & Collect → Prize Wheel).
- Demonstrate basic **gamification** with probability‑based rewards.
- Practice **Tkinter** (frames, navigation, images, events) and **Pillow** (image rotation/resizing).

---

## Features

- **Home**: navigate to Click & Collect or the Prize Wheel.
- **Click & Collect**: choose a restaurant; show pickup message.
- **Prize Wheel**:
  - Smooth animation using `after` and image rotation.
  - Manual stop and probability‑based draw.
  - Result display: Miss, Loyalty Points, Burger, Menu.
- French labels in the original notebook (code comments and strings can be localized).

---

## Tech Stack and Dependencies

- **Python** ≥ 3.9
- **tkinter** (bundled with CPython)
- **Pillow** for image handling

Installation:

```bash
# (optional) virtual environment
python -m venv .venv

# Windows
.venv\Scripts\activate
# macOS/Linux
source .venv/bin/activate

pip install pillow
```

Compatibility note: `Image.ANTIALIAS` is deprecated in Pillow ≥ 10. Use `Image.Resampling.LANCZOS` instead.

---

## Project Structure

```
Projet_Popeyes/
├─ README.md
├─ Information System Wheel 3 FR.ipynb
├─ app.py                      # (optional) standalone script version
├─ assets/
│  └─ roue.png                 # wheel image
└─ requirements.txt            # pillow
```

If the image is missing, add `assets/roue.png` or update the image path in code.

---

## Run

### Option A — Jupyter Notebook
Open `Information System Wheel 3 FR.ipynb` and run all cells.

### Option B — Python Script
Copy the notebook logic into `app.py` and use a **relative** image path:

```python
image_path = "assets/roue.png"  # adjust if needed
```

Run:

```bash
python app.py
```

---

## Image Configuration

- Recommended format: PNG, square (e.g., 800×800).
- The image is rotated and resized (~300 px).
- Large images are automatically downscaled with `thumbnail`.

Replacing the deprecated API:

```python
from PIL import Image

# Old (deprecated):
# image.thumbnail((300, 300), Image.ANTIALIAS)

# New (Pillow ≥ 10):
image.thumbnail((300, 300), Image.Resampling.LANCZOS)
```

---

## Prize Configuration

The wheel draws a random integer in [1–100] and maps it to a prize:

```python
prizes = [
    ("Miss", 0, 30),
    ("10 Loyalty Points", 31, 65),
    ("Burger", 66, 90),
    ("Menu", 91, 100)
]
```

To rebalance probabilities, adjust the ranges so they cover 1–100 without gaps or overlaps.

---

## Navigation and Event Flow

- `show_home()` / `show_click_and_collect()` / `show_prize_wheel()` manage screens.
- `pick_up_order()` displays the selected restaurant.
- `pick_prize()` → `update_image()` starts/maintains rotation.
- `stop_spin()` stops animation and triggers `show_prize()`.

Flow:

```
[Home]
   ├── Click & Collect  → Selection → Pickup message
   └── Prize Wheel      → Rotation → Stop → Draw → Result
```

---

## Known Issues

- Some examples hard‑code an absolute image path; prefer a relative path (e.g., `assets/roue.png`).
- `Image.ANTIALIAS` is obsolete with Pillow ≥ 10; use `Image.Resampling.LANCZOS`.
- The animation uses `after`; avoid blocking operations on the UI thread.

---

## English‑Only Note

This repository’s README is intentionally in English. Future READMEs will be provided in English as requested.
