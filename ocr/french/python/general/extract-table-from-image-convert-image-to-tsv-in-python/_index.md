---
category: general
date: 2026-07-05
description: Extraire un tableau d’une image avec OCR en Python. Apprenez à extraire
  le tableau, convertir l’image en TSV et maîtriser les techniques OCR de tableau
  en Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: fr
og_description: Extraire un tableau à partir d'une image avec Python OCR. Ce guide
  montre comment extraire le tableau, convertir l'image en TSV et utiliser les outils
  Python d'OCR pour les tableaux d'images.
og_title: Extraire un tableau à partir d'une image – Convertir une image en TSV avec
  Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Extraire un tableau à partir d'une image – Convertir une image en TSV avec
  Python
url: /fr/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire un tableau à partir d'une image – Convertir une image en TSV avec Python

Vous vous êtes déjà demandé comment extraire un tableau d'une image sans perdre patience ? Dans ce tutoriel, nous allons parcourir **comment extraire les données d'un tableau** à partir d'une image en utilisant la bibliothèque `aocr`, puis transformer ces données en un fichier TSV propre. Pas de magie, juste quelques lignes de Python et un peu de post‑traitement alimenté par l'IA.

Si vous avez déjà essayé de copier‑coller un tableau à partir d'une facture numérisée ou d'une capture d'écran et que vous vous êtes retrouvé avec un méli‑mélange, vous comprendrez pourquoi une approche basée sur l'OCR vaut la peine d'être maîtrisée. À la fin, vous pourrez fournir n'importe quelle image de tableau à Python et obtenir des valeurs séparées par des tabulations propres, prêtes pour les feuilles de calcul ou les bases de données.

---

## Ce dont vous aurez besoin

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Python 3.9+ | Le package `aocr` cible les environnements Python modernes. |
| `aocr` library (`pip install aocr`) | Fournit le moteur OCR et le post‑processeur IA que nous utiliserons. |
| An image file containing a table (PNG, JPG, etc.) | Les données source que nous allons extraire. |
| Optional: a virtual environment | Garde les dépendances isolées — fortement recommandé. |

Avoir cela prêt vous évite des interruptions à mi‑parcours du guide.

---

## Installer les dépendances

First, let’s get the OCR tooling installed. Open a terminal and run:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Astuce :** Si vous rencontrez des erreurs de permission, ajoutez `--user` à la commande `pip install` ou utilisez `pipx` pour une installation globale.

---

## Étape 1 – Initialiser le moteur OCR

Le moteur est le cœur du processus. Pensez‑y comme le « cerveau » qui examine chaque pixel et décide à quel caractère il correspond.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Pourquoi instancier un moteur au lieu d'appeler une fonction unique ? L'objet moteur nous permet d'attacher des post‑processeurs personnalisés plus tard, nous offrant un contrôle fin sur la sortie — essentiel lorsque vous avez besoin d'une précision **ocr table image python**.

---

## Étape 2 – Attacher le post‑processeur IA

`aocr` est fourni avec un post‑processeur IA léger qui nettoie les résultats bruts de l'OCR tout en préservant les bordures des cellules. Aucun argument supplémentaire n'est requis, ce qui garde le code propre.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Si vous sautez cette étape, vous obtiendrez toujours du texte brut, mais la structure du tableau sera bruyante — imaginez une feuille de calcul où chaque cellule est un mystère. Le post‑processeur effectue le travail lourd d'alignement du texte sur sa grille d'origine.

---

## Étape 3 – Charger votre image de tableau

Vous pouvez charger une image depuis n'importe quel chemin, mais pour plus de clarté nous ferons référence à un répertoire factice. Remplacez `"YOUR_DIRECTORY/invoice_table.png"` par le chemin réel de votre fichier.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Note :** `aocr.Image` détecte automatiquement le format de l'image et normalise les canaux de couleur, vous n'avez donc pas besoin de pré‑traiter le fichier sauf s'il est gravement détérioré.

---

## Étape 4 – Effectuer un OCR structuré

Le moteur scanne maintenant l'image et renvoie un objet tableau brut. Cet objet contient les lignes, les colonnes et le texte brut de chaque cellule.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Pourquoi utiliser `recognize_structured` au lieu d'un appel générique `recognize` ? La variante structurée tente d'inférer les limites des lignes/colonnes, vous offrant un résultat de type matrice beaucoup plus facile à convertir en TSV plus tard.

---

## Étape 5 – Nettoyer les données avec le post‑processeur IA

L'exécution du post‑processeur affine la sortie brute : il supprime les caractères parasites, fusionne les fragments séparés et garantit que le texte de chaque cellule est correctement aligné.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Si vous inspectez `processed_table.table`, vous verrez une liste de lignes, chaque ligne étant une liste d'objets `Cell`. Chaque `Cell` possède un attribut `.text` qui contient la chaîne nettoyée.

---

## Étape 6 – Exporter le tableau au format TSV

L'étape finale consiste à transformer les données traitées en un fichier de valeurs séparées par des tabulations (TSV) — exactement ce dont vous avez besoin lorsque vous voulez **convertir une image en TSV** pour Excel ou Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

L'exécution du script affiche chaque ligne dans la console (si vous le souhaitez) et écrit un fichier TSV propre que vous pouvez ouvrir dans n'importe quel programme de feuille de calcul.

### Vérification rapide

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Vous devriez voir des colonnes nettement alignées, comme :

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Si la sortie semble brouillée, revérifiez la qualité de l'image (netteté, contraste) et envisagez d'ajuster les paramètres du moteur OCR — `engine.set_config(...)` vous permet de régler les modèles de langue et les seuils de confiance.

---

## Gestion des cas limites courants

| Situation | Solution suggérée |
|-----------|-------------------|
| **Image inclinée** | Pré‑tourner avec `Pillow` (`Image.rotate`) avant de la fournir à `aocr`. |
| **Faible contraste** | Appliquer une égalisation d'histogramme (`cv2.equalizeHist`) pour améliorer la lisibilité. |
| **Cellules fusionnées** | Post‑traiter le TSV pour séparer les cellules selon des délimiteurs connus ou utiliser le drapeau `merge_cells=False` si disponible. |
| **PDF multi‑pages** | Convertir chaque page en image d'abord (`pdf2image`) et exécuter le pipeline dans une boucle. |

Ces ajustements maintiennent votre flux de travail **ocr table image python** robuste face à des sources variées.

---

## Script complet – Solution tout‑en‑un

Voici le script complet, prêt à l'exécution, qui regroupe chaque étape abordée. Enregistrez‑le sous le nom `extract_table.py` et exécutez `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code fonctionnels complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment extraire un tableau d'une image en utilisant Aspose.OCR pour .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Comment extraire du texte d'une image en préparant des rectangles dans l'OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}