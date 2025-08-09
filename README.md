# Popeyes IS — Tkinter Click & Collect + Prize Wheel (FR)

Projet universitaire (Sorbonne, S2 S2IE) : mini-application **Tkinter** simulant un parcours client "Click & Collect" et une roue des récompenses pour un fast-food.  
L’application permet de sélectionner un restaurant pour récupérer une commande, de lancer une roue animée et d’attribuer un lot avec des probabilités configurables.

---

## Objectifs pédagogiques

- Modéliser un parcours utilisateur simple (Accueil → Click & Collect → Roue).
- Illustrer une gamification basique (récompenses probabilisées).
- Manipuler Tkinter (frames, navigation, images, événements) et Pillow (rotation/redimensionnement d’image).

---

## Fonctionnalités

- Accueil : navigation vers Click & Collect ou la Roue.
- Click & Collect : liste de restaurants et message de retrait.
- Roue des récompenses :
  - Animation fluide (rotation via `after`).
  - Arrêt manuel et tirage probabiliste.
  - Affichage du gain (Raté, Points de fidélité, Burger, Menu).
- Interface en français.

---

## Stack et dépendances

- Python ≥ 3.9
- tkinter (inclus avec CPython)
- Pillow pour la manipulation d’images

Installation rapide :

```bash
# (optionnel) environnement virtuel
python -m venv .venv

# Windows
.venv\Scriptsctivate
# macOS/Linux
source .venv/bin/activate

pip install pillow
```

Note de compatibilité : `Image.ANTIALIAS` est déprécié à partir de Pillow ≥ 10. Utiliser `Image.Resampling.LANCZOS`.

---

## Organisation des fichiers

```
Projet_Popeyes/
├─ README.md
├─ Information System Wheel 3 FR.ipynb
├─ app.py                      # (optionnel) version script autonome
├─ assets/
│  └─ roue.png                 # image de la roue
└─ requirements.txt            # pillow
```

Si l’image est manquante, créer `assets/roue.png` ou adapter le chemin de l’image dans le code.

---

## Lancement

### Option A — Jupyter Notebook
Ouvrir `Information System Wheel 3 FR.ipynb` et exécuter les cellules.

### Option B — Script Python
Copier le code dans `app.py` et utiliser un chemin **relatif** pour l’image :

```python
image_path = "assets/roue.png"  # adapter si nécessaire
```

Exécuter :

```bash
python app.py
```

---

## Configuration de l’image

- Format recommandé : PNG, carré (ex. 800×800).
- L’image est pivotée et redimensionnée (~300 px).
- Les images trop grandes sont automatiquement réduites via `thumbnail`.

Exemple de remplacement de l’API dépréciée :

```python
from PIL import Image

# Ancien (déprécié) :
# image.thumbnail((300, 300), Image.ANTIALIAS)

# Nouveau (Pillow ≥ 10) :
image.thumbnail((300, 300), Image.Resampling.LANCZOS)
```

---

## Paramétrage des récompenses

Le tirage utilise un entier aléatoire [1–100] et mappe sur une plage :

```python
prizes = [
    ("Raté", 0, 30),
    ("10 Points de fidélité", 31, 65),
    ("Burger", 66, 90),
    ("Menu", 91, 100)
]
```

Pour ajuster les probabilités, modifier les bornes tout en couvrant 1–100 sans chevauchement.

---

## Navigation et événements (résumé)

- `show_home()` / `show_click_and_collect()` / `show_prize_wheel()` : gestion des écrans.
- `pick_up_order()` : affiche le restaurant sélectionné.
- `pick_prize()` → `update_image()` : démarre/maintient la rotation.
- `stop_spin()` : stoppe l’animation et déclenche `show_prize()`.

Flux :

```
[Accueil]
   ├── Click & Collect  → Sélection → Message de retrait
   └── Roue             → Rotation → Stop → Tirage → Résultat
```

---

## Améliorations possibles

- Externaliser la configuration (JSON/YAML) : probabilités, restaurants, libellés.
- Utiliser des chemins relatifs et embarquer les assets dans le repo.
- Amélioration UI (mise en page `grid`, styles, icônes).
- Effet d’inertie (décélération progressive) avant l’arrêt de la roue.
- Tests unitaires du tirage avec graines pseudo-aléatoires.
- Internationalisation (FR/EN).

---

## Points connus

- Chemin d’image parfois codé en dur dans des exemples antérieurs.
- `Image.ANTIALIAS` obsolète avec Pillow ≥ 10.
- L’animation utilise `after` : éviter les opérations bloquantes dans le thread UI.

---

## Licence

Projet académique. Utilisation libre à des fins éducatives et démonstratives.  
(Ajouter une licence explicite si nécessaire, ex. MIT.)

---

## English Summary

Small Tkinter demo app for a fast-food Click & Collect flow and an animated Prize Wheel.  
Features: screen navigation, list selection, image rotation with Pillow, and probabilistic reward assignment.  
Run via notebook or `python app.py`; ensure `assets/roue.png` exists and install `pillow`. Replace `ANTIALIAS` with `Image.Resampling.LANCZOS` for Pillow ≥ 10.
