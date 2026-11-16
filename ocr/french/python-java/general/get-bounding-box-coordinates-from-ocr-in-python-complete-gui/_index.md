---
category: general
date: 2026-06-22
description: Obtenez les coordonnées des boîtes englobantes à partir d’images avec
  Python. Apprenez à extraire du texte d’une image en Python grâce à Aspose OCR et
  au parsing JSON en quelques minutes.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: fr
og_description: Obtenez les coordonnées des boîtes englobantes à partir d'images avec
  Python. Ce guide montre comment extraire du texte d'une image en Python avec Aspose
  OCR et analyser les données de mise en page.
og_title: Obtenez les coordonnées de la boîte englobante à partir de l'OCR en Python
  – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Obtenez les coordonnées de la boîte englobante à partir de l'OCR en Python
  – Guide complet
url: /fr/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir les coordonnées de la boîte englobante à partir de l'OCR en Python – Guide complet

Avez‑vous déjà eu besoin d’**obtenir les coordonnées de la boîte englobante** pour chaque mot d’une facture numérisée, mais vous ne saviez pas par où commencer ? Vous n’êtes pas le seul. Dans de nombreux projets d’automatisation, il faut localiser le texte sur une image pour le mettre en évidence, le masquer ou le transmettre à des analyses en aval. La bonne nouvelle ? En quelques lignes de Python et Aspose.OCR, vous pouvez extraire à la fois le texte **et** sa position exacte en une seule passe.

Dans ce tutoriel, nous parcourrons un exemple pratique qui vous montre comment **extraire du texte d’une image en Python**, puis plonger dans les données de mise en page JSON pour récupérer ces boîtes englobantes. Pas de superflu, juste un script fonctionnel, des explications sur l’importance de chaque étape, et des conseils pour éviter les pièges courants.

---

## Ce que vous allez créer

À la fin de ce guide, vous disposerez d’un script Python prêt à l’emploi qui :

1. Charge une image (par ex., un PNG de facture) dans Aspose OCR.
2. Configure le moteur pour générer des informations de mise en page au format JSON.
3. Analyse le JSON en un dictionnaire Python.
4. Itère sur chaque mot reconnu, affichant son texte **et** ses coordonnées de boîte englobante.

Vous verrez également comment adapter le code pour les PDF multi‑pages, différents formats d’image et des systèmes de coordonnées personnalisés.

### Prérequis

- Python 3.8+ installé sur votre machine.  
- Une licence active d’Aspose.OCR pour Python ou un essai gratuit (la bibliothèque fonctionne sans licence mais ajoute un filigrane).  
- `pip install aspose-ocr` (le nom du paquet sur PyPI).  
- Une image d’exemple nommée `invoice.png` placée dans un dossier que vous pouvez référencer.

C’est tout—pas de frameworks lourds, pas de services externes. Plongeons‑y.

## Étape 1 : Installer et importer les bibliothèques requises

Tout d’abord, assurez‑vous que le paquet Aspose OCR et le module intégré `json` sont disponibles. Le module `json` est fourni avec Python, nous n’avons donc besoin d’installer que Aspose.

```bash
pip install aspose-ocr
```

Importez‑les maintenant dans votre script :

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Pourquoi c’est important :** L’importation de `aspose.ocr` vous donne accès au moteur OCR haute performance, tandis que `json` vous permet de transformer la chaîne de mise en page brute en un dictionnaire Python natif pour une traversée facile.

## Étape 2 : Créer le moteur OCR et charger votre image

Le moteur est le cœur du processus. Vous l’instanciez, puis le pointez vers l’image que vous souhaitez analyser.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Astuce :** Remplacez `"YOUR_DIRECTORY/invoice.png"` par un chemin absolu ou relatif qui pointe vers votre fichier réel. Si le fichier n’est pas trouvé, Aspose lèvera une `FileNotFoundError`, alors vérifiez l’orthographe.

## Étape 3 : Configurer le moteur pour produire des données de mise en page JSON

Aspose OCR peut renvoyer du texte brut, du JSON uniquement OCR, ou un JSON complet de mise en page incluant les coordonnées des mots, lignes et même des caractères individuels. Pour **obtenir les coordonnées de la boîte englobante**, nous avons besoin du JSON de mise en page.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Pourquoi le JSON ?** Le JSON est indépendant du langage, lisible par l’homme, et se mappe proprement aux dictionnaires Python. Le JSON de mise en page contient un tableau `"words"` où chaque entrée possède le texte et un tableau `boundingBox` de huit nombres (les quatre points des coins).

## Étape 4 : Exécuter la reconnaissance et récupérer la chaîne JSON brute

Nous exécutons maintenant réellement l’OCR. La méthode `recognize()` renvoie un objet `OcrResult`, à partir duquel nous pouvons extraire la chaîne JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Si vous affichez `layout_json`, vous verrez quelque chose comme :

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Cas limite :** Certaines images peuvent produire des tableaux `"words"` vides si le moteur OCR ne détecte aucun texte. Dans ce cas, vérifiez la qualité de l’image (contraste, résolution) avant de continuer.

## Étape 5 : Analyser le JSON en un dictionnaire Python

Travailler avec des structures Python natives est bien plus facile que de manipuler des chaînes. Utilisez la fonction `json.loads()` pour convertir la chaîne.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Maintenant, `layout_data["words"]` est une liste de dictionnaires, chacun représentant un mot et sa boîte englobante.

## Étape 6 : Itérer sur les mots et **obtenir les coordonnées de la boîte englobante**

Voici le cœur de notre tutoriel : parcourir chaque mot, extraire le texte et afficher les coordonnées. C’est exactement l’endroit où nous **obtenons les coordonnées de la boîte englobante**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Exemple de sortie** (vos nombres différeront selon l’image) :

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Pourquoi le format à huit points ?** Les quatre coins (haut‑gauche, haut‑droite, bas‑droite, bas‑gauche) vous permettent de dessiner un polygone autour du mot, même si le texte est incliné. Si vous avez seulement besoin d’un rectangle simple, vous pouvez calculer `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, et `height = max(y…) - y_min`.

## Améliorations optionnelles

### 1. Convertir les boîtes englobantes en rectangles simples

Si votre outil en aval attend `(x, y, largeur, hauteur)` au lieu de huit points, ajoutez un helper :

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Gérer les PDF multi‑pages

Aspose OCR peut accepter des flux PDF. Remplacez la ligne de chargement d’image par :

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Itérez `set_page_number` pour chaque page, en collectant les coordonnées par page.

### 3. Visualiser les boîtes englobantes

Si vous voulez voir les boîtes dessinées sur l’image originale, utilisez Pillow :

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

## Questions fréquentes & pièges

- **Et si le JSON est volumineux ?** Pour de gros documents, envisagez de diffuser le JSON ou de le traiter page par page afin de limiter l’utilisation de la mémoire.  
- **Pourquoi certains mots sont‑ils manquants ?** Un faible contraste ou du texte manuscrit fait souvent échouer les moteurs OCR. Pré‑traitez l’image (augmentez le contraste, binarisez) avant de la transmettre à Aspose.  
- **Puis‑je obtenir des coordonnées au niveau des caractères ?** Oui—définissez `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` pour recevoir un tableau `"characters"` avec son propre `boundingBox`.  
- **Le système de coordonnées est‑il basé à zéro ?** Absolument. (0, 0) correspond au coin supérieur gauche de l’image.

## Script complet – Prêt à copier et exécuter

Voici l’exemple complet et exécutable qui combine toutes les étapes. Enregistrez‑le sous le nom `extract_bboxes.py` et exécutez `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extraire du texte d’une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment utiliser Aspose OCR pour obtenir le résultat JSON en reconnaissance d’image](/ocr/english/net/text-recognition/get-result-as-json/)
- [Comment extraire du texte d’une image en préparant des rectangles dans l’OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}