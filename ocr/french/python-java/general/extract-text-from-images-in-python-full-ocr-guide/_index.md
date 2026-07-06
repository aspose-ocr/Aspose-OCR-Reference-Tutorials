---
category: general
date: 2026-06-19
description: extraire du texte d'images en utilisant Python OCR. Apprenez la détection
  automatique de la langue, le traitement parallèle et la reconnaissance par lots
  dans un tutoriel concis.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: fr
og_description: extraire du texte à partir d'images avec Python OCR. Ce guide montre
  la détection automatique de la langue, le traitement parallèle et la reconnaissance
  par lots dans un seul tutoriel.
og_title: extraire du texte d'images en Python – Guide complet d'OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Extraire du texte des images en Python – Guide complet d'OCR
url: /fr/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'images en Python – Guide complet OCR

Vous vous êtes déjà demandé comment **extraire du texte à partir d'images** sans taper manuellement chaque mot ? Vous n'êtes pas le seul. Que vous numérisiez d'anciens reçus, que vous construisiez une archive de documents consultable, ou que vous vous amusiez simplement avec des astuces d'IA sympas, la capacité d'extraire du texte à partir d'images est une compétence indispensable pour tout développeur Python aujourd'hui.

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l’emploi, qui **extrait du texte à partir d'images** en utilisant un moteur OCR populaire. Nous aborderons la détection automatique de la langue, le traitement parallèle pour la vitesse, et la reconnaissance d'images en lot afin que vous puissiez gérer des dizaines de fichiers en quelques secondes. Ça ressemble à ce dont vous avez besoin ? Plongeons‑y.

## Ce que vous apprendrez

- Comment instancier le moteur OCR avec `ocr.OcrEngine`.
- Activer la **détection automatique de la langue** afin que le moteur choisisse la bonne langue tout seul.
- Configurer le **OCR en traitement parallèle** avec un pool de threads personnalisé.
- Exécuter la **reconnaissance d'images en lot** sur une liste de fichiers.
- Imprimer le texte reconnu pour chaque image, prêt à être sauvegardé ou indexé.

Aucune documentation externe requise — tout ce dont vous avez besoin se trouve ici, et le code fonctionne immédiatement avec le package `ocr` (installez‑le via `pip install ocr`).

## Prérequis

1. Python 3.8 ou plus récent installé.
2. Le package `ocr` (`pip install ocr`).
3. Un dossier d'images PNG (ou JPG) que vous souhaitez traiter.
4. Une familiarité de base avec les fonctions et boucles Python.

C’est tout — aucune dépendance lourde, aucune magie GPU, juste du Python pur.

![exemple d'extraction de texte à partir d'images](https://example.com/ocr-demo.png "Capture d'écran montrant la sortie d'extraction de texte à partir d'images")

*Texte alternatif : capture d'écran de démonstration d'extraction de texte à partir d'images*

## Étape 1 – Configurer le moteur OCR (Mot‑clé principal en action)

First thing’s first: create an OCR engine instance. Think of `ocr.OcrEngine()` as the brain behind the operation; it knows how to read characters, lines, and paragraphs.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Pourquoi avons‑nous besoin d’un moteur explicite ? Parce que l’**utilisation de ocr.OcrEngine** vous donne un contrôle fin sur les paramètres de langue, le threading, et plus encore. C’est la façon la plus flexible d’**extraire du texte à partir d'images** comparée aux aides en une ligne.

## Étape 2 – Laisser le moteur détecter les langues automatiquement

Most OCR libraries require you to tell them which language to look for. That’s fine for a single‑language project, but cumbersome for a mixed‑language batch. Luckily, the `ocr` package supports **automatic language detection**.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

Définir `engine.language` à `ocr.Language.Auto` indique au moteur de sentir chaque image et de choisir le modèle de langue approprié. Cette petite ligne vous fait gagner des heures de configuration manuelle lorsque vous traitez des documents internationaux.

## Étape 3 – Accélérer le traitement avec le OCR en parallélisation

If you have four or more CPU cores, why not use them? The engine can spin up a thread pool, letting multiple images be processed at the same time. This is where **parallel processing OCR** shines.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

N’hésitez pas à ajuster le nombre `4` en fonction de votre machine. Plus de threads → des exécutions de lot plus rapides, mais rappelez‑vous que chaque thread consomme de la mémoire, alors trouvez le juste milieu pour votre environnement.

## Étape 4 – Rassembler les images que vous souhaitez traiter

Now we need a list of file paths. You can build this list manually, read it from a CSV, or use `glob`. For clarity, we’ll hard‑code a short list:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre système. Si vous avez des dizaines de fichiers, un simple `glob.glob("*.png")` fera le gros du travail.

## Étape 5 – Exécuter la reconnaissance d'images en lot

Here’s the heart of the tutorial: a single call that processes every image in `files` and returns a list of result objects. This is the **batch image recognition** feature that makes large‑scale OCR practical.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

En coulisses, le moteur répartit chaque fichier sur les quatre threads de travail que nous avons configurés précédemment, tout en détectant automatiquement la langue pour chaque image. La méthode renvoie une liste où chaque élément contient le texte reconnu et les métadonnées.

## Étape 6 – Imprimer (ou stocker) le texte extrait

Finally, we loop over the results and print the text. In a real project you’d probably write this to a database or a CSV file, but printing keeps the example simple.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**Sortie attendue** (troncature pour la brièveté) :

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

Chaque bloc montre le nom de fichier suivi de la chaîne dérivée de l’OCR. Si une image contient plusieurs langues, vous verrez apparaître les caractères appropriés grâce à l’étape précédente de **détection automatique de la langue**.

## Astuces professionnelles & pièges courants

- **La qualité de l'image compte** – les photos floues ou à faible contraste produiront du bruit. Pré‑traitez avec OpenCV (`cv2.threshold`, `cv2.resize`) si nécessaire.
- **Nombre de threads vs. I/O** – si vos images résident sur un lecteur réseau lent, plus de threads ne vous aidera pas. Surveillez l’utilisation du CPU avec `top` ou le **Gestionnaire des tâches**.
- **Gestion de l'Unicode** – `result.text` est une chaîne Unicode. Lors de l’écriture dans des fichiers, ouvrez‑les avec `encoding="utf‑8"` pour éviter les `UnicodeEncodeError`.
- **Utilisation de la mémoire** – les gros PDF peuvent consommer beaucoup de RAM. Si vous rencontrez un `MemoryError`, réduisez la taille du pool de threads ou traitez les images par petits lots.

## Script complet fonctionnel

Below is the complete, copy‑and‑paste‑ready script that incorporates every step we discussed. Save it as `batch_ocr.py` and run `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

Exécutez‑le ainsi :

```bash
python batch_ocr.py ./my_images 4
```

Vous verrez un bloc de texte joliment formaté pour chaque image, prouvant que vous pouvez **extraire du texte à partir d'images** à grande échelle.

## Et après ?

Now that you’ve mastered the basics of **extract text from images** with Python, consider exploring:

- **Post‑processing** : nettoyez la sortie OCR avec des expressions régulières ou des bibliothèques de traitement du langage naturel.
- **Conversion PDF** : alimentez les chaînes extraites dans un générateur de PDF pour des PDF consultables.
- **Services OCR cloud** : comparez les résultats `ocr` on‑prem avec Google Vision ou Azure OCR pour des cas limites de précision.
- **Interface GUI** : créez une petite application Flask ou FastAPI qui permet aux utilisateurs de télécharger des images et de voir instantanément le texte extrait.

Each of these topics builds on the **Python OCR library** foundation you just set up, and they all benefit from the same **parallel processing OCR** tricks we used here.

---

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous — je suis toujours disponible pour dépanner les bizarreries du OCR.*

## Que devriez‑vous apprendre ensuite ?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraire du texte d'images en utilisant l'opération OCR sur des dossiers](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extraire du texte d'une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}