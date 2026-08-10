---
category: general
date: 2026-06-19
description: Extrayez du texte à partir d'images en Python avec un moteur OCR simple.
  Apprenez à convertir des images numérisées en texte, à reconnaître le texte à partir
  de photos et à répertorier efficacement les fichiers image en Python.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: fr
og_description: Extraire du texte d'images en Python à l'aide d'un moteur OCR léger.
  Ce guide vous montre comment convertir des images numérisées en texte, reconnaître
  le texte à partir de photos et lister les fichiers image en Python en quelques étapes.
og_title: Extraire du texte d'images avec Python – Guide complet d'OCR par lots
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Extraire du texte d'images en Python – Guide complet d'OCR en lot
url: /fr/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'images en Python – Guide complet d'OCR par lots

Vous avez déjà eu besoin d'**extraire du texte à partir d'images** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul—les développeurs sont constamment confrontés au défi de transformer des PDF numérisés, des reçus photographiés ou des captures d'écran en texte consultable. Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l'exécution, qui montre comment **convertir des images numérisées en texte**, reconnaître le texte à partir d'images, et même **list image files python**‑style. À la fin, vous disposerez d'un script réutilisable qui traite un dossier entier en une seule fois.

Nous couvrirons tout ce dont vous avez besoin : les bibliothèques requises, pourquoi chaque étape est importante, la gestion des cas limites, et un peu de dépannage. Pas besoin de courir après la documentation externe ; le code ci‑dessous est autonome, et les explications répondent au « comment » *et* au « pourquoi ». Prenez votre IDE préféré, et c'est parti.

---

## Ce que vous allez construire

- Initialiser un moteur OCR (nous utiliserons le package `ocr` à titre d'illustration).
- Parcourir un répertoire et **list image files python**‑style, en filtrant PNG, JPG et TIFF.
- Exécuter une opération **batch OCR** sur toutes les images trouvées.
- Imprimer le texte extrait pour chaque fichier, clairement étiqueté.

> **Astuce pro :** Si vous n'avez pas la bibliothèque `ocr` installée, vous pouvez la remplacer par `pytesseract` avec quelques modifications mineures — la logique principale reste la même.

## Prérequis

- Python 3.8+ (le script utilise les f‑strings et les annotations de type).
- Une bibliothèque OCR qui expose un `OcrEngine` avec `recognize_batch`. Pour ce guide, nous supposons un package fictif `ocr`, mais le modèle fonctionne avec de vraies bibliothèques.
- Un dossier contenant les fichiers image que vous souhaitez traiter (`.png`, `.jpg`, `.tif`).

## Étape 1 – Installer & importer les modules requis

Tout d'abord, assurez-vous que le package OCR est disponible. Si vous utilisez une vraie bibliothèque comme `pytesseract`, remplacez l'import en conséquence.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Pourquoi c'est important :** L'import de `os` nous fournit une gestion des chemins multiplateforme, tandis que `typing.List` aide à l'autocomplétion dans l'IDE et à la pérennité du code.

## Étape 2 – **Extract Text from Images** : Initialiser le moteur OCR

Créer le moteur est la première étape de tout travail OCR. Nous définissons également la langue en auto‑détection afin que le moteur puisse gérer des documents multilingues.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Explication :** En encapsulant la création du moteur dans une fonction, nous gardons le code modulaire. Si vous devez plus tard ajuster le DPI ou le mode OCR, vous n'avez qu'à modifier cet unique endroit.

## Étape 3 – **List Image Files Python** : Rassembler les fichiers d'un répertoire

Nous devons maintenant localiser chaque image que nous voulons traiter. La compréhension de liste ci‑dessous reflète un modèle courant de “list image files python”.

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Gestion des cas limites :** La fonction ignore les sous‑dossiers (vous pouvez ajouter la récursion plus tard) et filtre automatiquement les fichiers cachés car ils ne se terminent généralement pas par les extensions prises en charge.

## Étape 4 – **Convert Scanned Images to Text** : Exécuter le batch OCR

La plupart des bibliothèques OCR offrent une méthode batch qui est bien plus rapide que le traitement image par image. Voici comment nous l'appelons.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Pourquoi le batch ?** Envoyer toutes les images d'un coup réduit la surcharge (par ex., charger le modèle OCR à plusieurs reprises) et permet souvent une meilleure utilisation du CPU/GPU.

## Étape 5 – **Recognize Text from Pictures** : Afficher les résultats

Enfin, nous parcourons les noms de fichiers associés et les résultats OCR, en imprimant un en‑tête propre pour chaque image.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Astuce :** `strip()` supprime les espaces blancs en début et fin de chaîne que l'OCR ajoute souvent.

## Script complet – Assemblez le tout

Voici le programme complet et exécutable. Enregistrez‑le sous le nom `batch_ocr.py` et lancez `python batch_ocr.py <your_folder>`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Sortie attendue

En supposant que le dossier contienne `invoice1.png` et `receipt.jpg`, vous pourriez voir :

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Chaque bloc est clairement étiqueté, ce qui rend le traitement en aval (par ex., l'enregistrement dans une base de données) simple.

## Gérer les problèmes courants

| Problème | Pourquoi cela se produit | Solution rapide |
|----------|--------------------------|-----------------|
| **Aucun texte n'apparaît** | Langue OCR non détectée ou image à faible contraste. | Forcer une langue (`engine.language = ocr.Language.English`) ou prétraiter les images (augmenter le contraste). |
| **Erreur de mémoire sur de gros lots** | Le moteur tente de charger toutes les images d'un coup. | Diviser `image_files` en morceaux (`batch_size = 20`) et appeler `recognize_batch` de façon répétée. |
| **Format de fichier non pris en charge** | Vous avez ajouté un `.gif` ou `.bmp`. | Étendre le tuple `supported_exts` ou convertir les images en PNG/JPG au préalable. |
| **Corruption Unicode** | L'OCR renvoie des octets au lieu de chaînes. | S'assurer que la bibliothèque OCR renvoie du Unicode (`result.text.decode('utf‑8')` si nécessaire). |

## Étendre le flux de travail

Maintenant que vous pouvez **extraire du texte à partir d'images**, envisagez les étapes suivantes :

- **Exportation vers CSV** – Écrire chaque nom de fichier et son texte extrait dans une feuille de calcul pour l'analyse.
- **Traitement parallèle** – Utiliser `concurrent.futures.ThreadPoolExecutor` pour gérer plusieurs lots simultanément.
- **Intégration avec un OCR cloud** – Remplacer le moteur local par Google Vision ou Azure OCR pour une meilleure précision sur des mises en page complexes.
- **Ajout de prétraitement d'image** – Des bibliothèques comme Pillow ou OpenCV peuvent redresser, débruiter ou binariser les images avant l'OCR, améliorant les résultats.

Toutes ces idées utilisent naturellement les mêmes fonctions de base que nous avons créées, vous n'aurez donc pas besoin de repartir de zéro.

## Conclusion

Nous venons de parcourir une solution complète pour **extraire du texte à partir d'images** en Python, couvrant tout, de **list image files python** à **recognize text from pictures** et enfin **convert scanned images to text** dans un batch propre. Le script est délibérément simple tout en étant suffisamment flexible pour servir de base à des projets plus importants — que vous numérisiez des reçus, construisiez une archive consultable ou alimentiez un pipeline d'extraction de données.

Essayez-le, ajustez les étapes de prétraitement, et voyez votre précision OCR s'améliorer. Si vous rencontrez des problèmes, consultez à nouveau le tableau « Gérer les problèmes courants » ; la plupart des soucis se résolvent avec un petit changement de configuration.

Prêt pour le prochain défi ? Essayez d'ajouter une étape de conversion PDF‑vers‑image avec `pdf2image`, puis alimentez ces images directement dans le même pipeline. Le ciel est la limite lorsque vous combinez l'OCR avec le riche écosystème de Python.

Bon codage, et que votre texte soit toujours lisible !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}