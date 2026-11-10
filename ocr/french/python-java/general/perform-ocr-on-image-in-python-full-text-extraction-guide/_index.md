---
category: general
date: 2026-06-19
description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  en utilisant la bibliothèque OCR de Python. Apprenez comment détecter le texte d’une
  image, reconnaître le texte d’un JPEG et extraire le texte d’une image numérisée
  efficacement.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: fr
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  avec Python et extrayez le texte des fichiers numérisés. Ce guide vous accompagne
  pas à pas dans le chargement des images, la correction de l’inclinaison et la reconnaissance
  du texte.
og_title: Effectuer l’OCR d’une image en Python – Guide complet d’extraction de texte
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Effectuer une OCR sur une image en Python – Guide complet d'extraction de texte
url: /fr/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image en Python – Guide complet d'extraction de texte

Vous avez déjà eu besoin de **perform OCR on image** mais vous êtes tombé sur un mur parce que le code semblait cryptique ? Vous n'êtes pas seul. Que vous transformiez une pile de reçus numérisés en PDF consultables ou que vous extrayiez des légendes d'un JPEG pour un projet de data‑science, la capacité à reconnaître du texte à partir de JPEG et d'autres formats est une compétence indispensable pour tout développeur aujourd'hui.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre comment **detect text from image**, **extract text from scanned image** et même **load image for OCR** en quelques lignes seulement. À la fin, vous disposerez d’un extrait de code solide, prêt pour la production, que vous pourrez intégrer directement dans vos projets — sans importations manquantes, sans raccourcis vagues du type « voir la documentation ».

## Ce que vous allez créer

- Un petit script Python qui crée un moteur OCR, active l’auto‑deskew, charge un JPEG (ou tout autre format supporté) et affiche le texte reconnu.
- Des explications sur **why** chaque paramètre est important, pas seulement **how** le taper.
- Des astuces pour gérer les PDF multi‑pages, les langues non‑anglais et les pièges courants comme les scans flous.

### Prérequis

- Python 3.8+ installé (l’exemple utilise le package `ocr` disponible via `pip install ocr-lib` – remplacez‑le par le nom réel de votre bibliothèque).
- Une connaissance de base des fonctions Python et des environnements virtuels.
- Un fichier image (JPEG, PNG, TIFF) que vous souhaitez traiter ; nous utiliserons `skewed_page.jpg` comme exemple.

> **Pro tip :** Si vous êtes sous Windows, lancez votre terminal en tant qu’administrateur lors de l’installation de la bibliothèque OCR pour éviter les problèmes de permissions.

---

## Perform OCR on Image – Configuration et mise en place

La première chose dont vous avez besoin est une instance propre du moteur OCR. Pensez‑y comme le cerveau de l’opération ; sans une configuration correcte, même l’image la plus nette renverra du charabia.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Why this matters :**  
Définir `engine.language` restreint l’ensemble de caractères attendu par le moteur OCR, ce qui augmente considérablement la précision. Si vous omettez cela, le moteur devinera, souvent en lisant mal des mots simples.

---

## Enable Automatic Deskew – Corriger les scans inclinés

Les pages numérisées ne sont rarement parfaitement plates. Une légère inclinaison peut perturber la segmentation des caractères, transformant « Hello » en « H3llo ». Le drapeau `auto_deskew` fait le gros du travail pour vous.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Edge case :** Si vous savez que vos images sont déjà droites, désactiver le deskew peut économiser quelques millisecondes de temps de traitement — utile lorsqu’on traite des milliers de pages dans un job batch.

---

## Load Image for OCR – Prise en charge de JPEG, PNG, TIFF

Nous allons maintenant réellement **load image for OCR**. La méthode `ocr.Image.load` est flexible ; elle accepte un chemin vers n’importe quel format raster supporté.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Why this step is crucial :** La bibliothèque lit le fichier dans un bitmap interne, appliquant les conversions d’espace couleur nécessaires. Ignorer cette étape et passer un flux d’octets brut déclencherait une `FileNotFoundError` ou, pire, produirait silencieusement des résultats vides.

Si vous devez **recognize text from JPEG** spécifiquement, assurez‑vous simplement que l’extension du fichier est `.jpeg` ou `.jpg`. Le même appel fonctionne pour PNG (`.png`) ou TIFF (`.tif`) sans modification.

---

## Perform OCR on Image – Exécution du moteur

Avec le moteur prêt et l’image en mémoire, il est temps de **perform OCR on image**. Cette ligne unique fait tout le travail : pré‑traitement, segmentation, classification et assemblage du texte.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**What happens under the hood ?**  
- Le moteur applique la transformation de deskew (si activée).  
- Il exécute un réseau neuronal ou le backend Tesseract pour identifier les caractères.  
- Enfin, il assemble les caractères en mots et lignes, renvoyant un objet `result` riche.

---

## Extract Text from Scanned Image – Afficher les résultats

L’étape finale consiste à **extract text from scanned image** et à l’afficher. L’attribut `result.text` contient la représentation en texte brut.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Un résultat typique ressemble à :

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Si le moteur OCR ne trouve aucun caractère, `result.text` sera une chaîne vide. Dans ce cas, revérifiez la qualité de l’image ou envisagez d’ajuster la propriété `engine.confidence_threshold` (si votre bibliothèque le supporte).

---

## Gestion des variations courantes

### Recognize Text from JPEG vs PNG

Les deux formats sont supportés, mais la compression JPEG peut introduire des artefacts qui perturbent le moteur. Si vous remarquez des erreurs fréquentes, essayez de convertir le JPEG en PNG d’abord :

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Detect Text from Image with Multiple Languages

Si votre document mêle anglais et espagnol, activez un mode multilingue :

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

Le moteur prendra alors en compte les deux alphabets lors de la reconnaissance.

### Extract Text from Scanned PDFs

Pour les PDF, il faut d’abord rasteriser chaque page en image. Des bibliothèques comme `pdf2image` rendent cela très simple :

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Exemple complet fonctionnel

Voici le script complet que vous pouvez copier‑coller dans un fichier `ocr_demo.py`. Il inclut la gestion des erreurs et un petit helper pour mesurer le temps d’exécution.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Expected output** (en supposant un scan clair) :

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Questions fréquentes

**Q : Puis‑je exécuter cela sur un serveur sans interface graphique ?**  
R : Absolument. La bibliothèque fonctionne sans GUI ; assurez‑vous simplement que les binaires natifs nécessaires (par ex., Tesseract) sont installés sur le serveur.

**Q : Et si l’image est floue ?**  
R : Envisagez d’ajouter un filtre de netteté avant `engine.recognize`. De nombreuses bibliothèques OCR exposent `image_preprocessing.sharpen = True` ou vous pouvez utiliser `cv2.GaussianBlur` d’OpenCV en sens inverse.

**Q : Le script supporte‑t‑il le traitement par lots ?**  
R : Oui. Enveloppez `perform_ocr` dans une boucle sur une liste de chemins de fichiers,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}