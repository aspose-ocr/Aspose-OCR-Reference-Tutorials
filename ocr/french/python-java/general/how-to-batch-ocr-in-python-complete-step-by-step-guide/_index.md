---
category: general
date: 2026-06-28
description: Comment réaliser de l'OCR par lots avec Python. Apprenez à OCR plusieurs
  images, extraire du texte à partir de PNG et convertir une image en texte grâce
  à un tutoriel complet d'OCR en Python.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: fr
og_description: Comment faire de l'OCR par lots en Python, expliqué dans la première
  phrase. Suivez ce tutoriel OCR Python pour extraire efficacement le texte des fichiers
  PNG.
og_title: Comment réaliser une OCR par lots en Python – Guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Comment faire de l’OCR par lots en Python – Guide complet étape par étape
url: /fr/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots en Python – Guide complet étape par étape

Vous vous êtes déjà demandé **comment faire de l'OCR par lots** sur une pile de pages numérisées sans écrire une boucle qui bloque votre interface ? Vous n'êtes pas le seul. Traiter des dizaines de fichiers PNG un par un peut donner l'impression de regarder la peinture sécher, surtout lorsque chaque image met une seconde ou deux à être décodée.  

Dans ce tutoriel, nous vous montrerons une méthode propre et non bloquante pour **OCR plusieurs images** à la fois, **extraire du texte d'un PNG** et **convertir une image en texte** en utilisant un moteur OCR moderne pour Python. À la fin, vous disposerez d'un script prêt à l'emploi que vous pourrez intégrer à n'importe quel projet – parfait pour un *tutoriel python ocr* rapide ou un travail par lots de niveau production.

## Ce que vous allez créer

- Initialiser un moteur OCR et définir sa langue sur Latin (ou toute langue dont vous avez besoin).  
- Fournir une liste de chemins d'images (PNG dans notre exemple) au moteur.  
- Lancer une opération par lots qui renvoie un objet de type Future.  
- Récupérer tous les résultats de façon concurrente avec un pool de threads, en gardant votre thread principal libre.  
- Afficher le texte reconnu pour chaque page, séparé de façon lisible.

Pas de magie cachée, juste du Python pur et une bibliothèque OCR tierce (nous utiliserons le package fictif `pyocr` à titre d'illustration).  

**Prérequis**  
- Python 3.8+ installé.  
- Familiarité de base avec les fonctions Python et `concurrent.futures`.  
- Accès à une bibliothèque OCR qui expose une classe `OcrEngine` (par ex., `pip install pyocr`).  

Si l'un de ces éléments vous manque, procurez‑vous‑le dès maintenant – c’est plus simple que vous ne le pensez.

---

## Comment faire de l'OCR par lots en Python – Concepts de base

Avant de plonger dans le code, répondons au « pourquoi » de chaque étape.

1. **Pourquoi définir la langue ?**  
   La précision de l'OCR monte en flèche lorsque le moteur sait quels caractères attendre. Le latin fonctionne pour l'anglais, le français, l'espagnol, etc. Passez à `Language.Japanese` ou `Language.Arabic` si besoin.

2. **Pourquoi utiliser une opération par lots ?**  
   Un appel par lots permet au moteur de planifier le travail en interne, souvent en exploitant des threads natifs ou l'accélération GPU. Il renvoie un handle que vous pouvez interroger plus tard, ce qui évite de bloquer pendant le traitement de chaque image.

3. **Pourquoi un ThreadPoolExecutor ?**  
   L'objet Future que nous recevons est *lazy* – il ne commence à récupérer les résultats que lorsque nous le demandons. En passant un pool de threads à `getAll`, nous laissons Python récupérer le texte de chaque page en parallèle, réduisant considérablement le temps d'exécution global.

4. **Pourquoi énumérer les résultats ?**  
   L'ordre des résultats correspond à l'ordre des chemins d'entrée, ce qui nous permet d'étiqueter en toute sécurité chaque numéro de page.

Comprendre ces « pourquoi » vous aide à adapter le modèle à d'autres bibliothèques ou à des ensembles de données plus volumineux.

---

## Étape 1 : Installer et importer les packages requis

Tout d'abord, assurez‑vous que la bibliothèque OCR est installée. L'exemple utilise un package générique `pyocr` ; remplacez‑le par la bibliothèque réelle que vous préférez (par ex., `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Ensuite, importez tout ce dont nous avons besoin.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Astuce :** Utiliser `Path` de `pathlib` rend votre script indépendant du système d'exploitation et plus lisible.

---

## Étape 2 : Créer le moteur OCR et définir la langue

Créer le moteur est simple. Nous le verrouillerons sur le latin pour cette démonstration.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

L'appel `setLanguage` est optionnel pour certains moteurs, mais c’est une bonne habitude. Il indique au modèle OCR de se concentrer sur le jeu de caractères qui vous intéresse, améliorant à la fois la vitesse et la précision.

---

## Étape 3 : Lister les fichiers image à traiter (Extraire du texte d'un PNG)

Rassemblez tous les fichiers PNG que vous souhaitez convertir. Utiliser `Path.glob` vous permet de déposer un dossier complet sans modifier le script.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Pourquoi c’est important :** En triant la liste, nous garantissons un ordre déterministe, ce qui aligne chaque résultat avec le numéro de page correct.

---

## Étape 4 : Lancer une opération OCR par lots (Convertir une image en texte)

Nous transmettons maintenant la liste au moteur. La méthode renvoie un conteneur de type Future que nous interrogerons plus tard.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

En interne, le moteur peut lancer ses propres threads de travail ou même un pipeline GPU. Tout ce qui nous importe, c’est que nous disposons d’un handle (`batch_future`) qui sait comment récupérer les résultats individuels.

---

## Étape 5 : Récupérer tous les résultats de façon concurrente (OCR plusieurs images)

C’est ici que nous *batchons* réellement le travail. En passant un `ThreadPoolExecutor` à `getAll`, le texte de chaque page est récupéré dans son propre thread.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Vous pouvez ajuster `max_workers` en fonction du nombre de cœurs CPU ou des recommandations de la bibliothèque OCR. Plus de workers ≠ toujours plus rapide – surveillez votre utilisation CPU.

---

## Étape 6 : Afficher le texte reconnu (Finale du tutoriel Python OCR)

Enfin, affichez le texte de chaque page. L'objet `Result` expose `getText()` – adaptez si votre bibliothèque utilise un nom de méthode différent.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Sortie attendue (exemple)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Si une image échoue, la plupart des moteurs renvoient une chaîne vide ou lèvent une exception – vous pouvez envelopper la boucle dans un bloc `try/except` pour gérer les cas limites de façon élégante.

---

## Script complet – Prêt à exécuter

Voici le script complet et autonome. Copiez‑collez‑le dans un fichier nommé `batch_ocr.py`, ajustez `YOUR_DIRECTORY`, puis exécutez `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Enregistrez, exécutez, et observez la console se remplir du texte extrait. Simple, rapide et entièrement asynchrone.

---

## Pièges courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Pas de sortie** – chaînes vides | Le moteur OCR n’a trouvé aucun texte (image trop bruitée) | Pré‑traiter les images : binariser, redresser, ou augmenter le DPI |
| **`FileNotFoundError`** | Chemin du répertoire incorrect ou fichiers PNG manquants | Vérifiez `YOUR_DIRECTORY` et assurez‑vous que les fichiers se terminent par `.png` |
| **Utilisation CPU élevée** | `max_workers` trop élevé pour votre machine | Réduisez `max_workers` ou activez l’accélération GPU si supportée |
| **Brouillage Unicode** | Le moteur a utilisé une langue différente par défaut | Appelez `engine.setLanguage(Language.Latin)` (ou la langue appropriée) avant le batch OCR |

---

## Étendre le tutoriel – Prochaines étapes

- **OCR multiple images** dans d'autres formats (JPEG, TIFF) – il suffit de changer le motif glob.  
- **Extract text from PNG** et l’alimenter dans un index de recherche (par ex., Elasticsearch).  
- **Convert image to text** pour la génération de PDF en utilisant `reportlab` ou `PyPDF2`.  
- **Parallelize across machines** avec `multiprocessing` ou une file de tâches comme Celery pour des ensembles de données massifs.  

Chacun de ces sujets s’appuie naturellement sur le **python ocr tutorial** que vous venez de terminer.

---

## Conclusion

Nous avons parcouru **comment faire de l'OCR par lots** sur une collection de fichiers PNG, démontré la puissance d’une API orientée batch, et montré comment **extraire du texte d'un PNG** avec une approche à pool de threads. Le script complet ci‑dessus est prêt pour la production, et vous disposez maintenant d’une base solide pour tout projet Python intensif en OCR.

Essayez‑le, ajustez les paramètres de langue, et pourquoi pas remplacer `pyocr` par `pytesseract` – le schéma reste le même. Vous avez des questions ou souhaitez partager un cas d’utilisation intéressant ? Laissez un commentaire, et continuons la discussion.

*Bon codage !*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraire du texte d'images en utilisant l'opération OCR sur des dossiers](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Comment faire de l'OCR par lots d'images avec une liste dans Aspose.OCR pour .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}