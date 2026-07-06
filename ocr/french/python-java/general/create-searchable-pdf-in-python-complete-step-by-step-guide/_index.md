---
category: general
date: 2026-06-19
description: Créer un PDF consultable à partir d’une image en utilisant l’OCR Python.
  Apprenez à convertir l’OCR en PDF, extraire le texte d’une image et effectuer rapidement
  l’OCR sur une image.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: fr
og_description: Créez un PDF consultable à partir d’une image avec Python OCR. Ce
  guide montre comment convertir l’OCR en PDF, extraire le texte d’une image et effectuer
  l’OCR sur une image.
og_title: Créer un PDF recherchable en Python – Guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Créer un PDF interrogeable en Python – Guide complet étape par étape
url: /fr/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF interrogeable en Python – Guide complet étape par étape

Vous avez déjà eu besoin de **créer un PDF interrogeable** à partir d'un reçu numérisé mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul — de nombreux développeurs rencontrent le même obstacle lorsqu'ils essaient pour la première fois de transformer une image de texte en un PDF réellement recherchable.  

Dans ce tutoriel, nous allons parcourir une solution pratique qui vous permet de **perform OCR on image**, de transformer ce résultat OCR en **searchable PDF**, et même d'extraire le texte brut si vous en avez besoin pour un traitement ultérieur. Pas de superflu, juste un exemple fonctionnel que vous pouvez copier‑coller dans votre projet dès aujourd'hui.

## Ce que vous allez apprendre

- Comment configurer un moteur OCR léger en Python  
- Les étapes exactes pour **convert OCR to PDF** et l'enregistrer comme document interrogeable  
- Moyens d'**extract text from image** pour une analyse en aval  
- Conseils pour gérer les pièges courants comme l'orientation de l'image et les gros fichiers  
- Un script complet et exécutable que vous pouvez adapter à votre propre cas d'utilisation

### Prérequis

- Python 3.8+ installé sur votre machine  
- Familiarité de base avec pip et les environnements virtuels (optionnel mais recommandé)  
- Un fichier image (PNG, JPEG, etc.) contenant du texte clair et lisible par machine  

Si vous avez tout cela, plongeons‑nous dedans.

## Étape 1 : Installer la bibliothèque requise

Le fragment de code que vous avez vu plus tôt utilise un paquet fictif `ocr`, mais les mêmes idées s’appliquent aux bibliothèques réelles telles que **EasyOCR**, **pytesseract**, ou **pdfminer.six**. Pour ce guide, nous utiliserons **EasyOCR** car il est purement Python, prend en charge de nombreuses langues, et renvoie une méthode pratique de conversion PDF via un assistant auxiliaire.

```bash
pip install easyocr pillow
```

> **Astuce :** Installez dans un environnement virtuel (`python -m venv venv && source venv/bin/activate`) pour garder vos dépendances propres.

## Étape 2 : Initialiser le moteur OCR – Effectuer l'OCR sur l'image

Maintenant que la bibliothèque est prête, nous créons un moteur OCR et lui indiquons de travailler avec du texte anglais. C’est le premier endroit où nous **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Pourquoi avons‑nous besoin d’un objet lecteur dédié ? EasyOCR pré‑charge les modèles de langue, donc réutiliser le même `reader` pour plusieurs images est bien plus efficace que de le réinitialiser à chaque fois.

## Étape 3 : Charger l'image – Extraire le texte de l'image

Apportons l'image en mémoire. Cette étape est celle où nous **extract text from image** plus tard, mais pour l’instant nous nous contentons de la charger.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Si votre image est à l’envers ou inclinée, envisagez d’utiliser les méthodes `rotate` ou `transpose` de Pillow avant de la transmettre au moteur OCR. Une vérification visuelle rapide peut vous faire gagner des heures de débogage plus tard.

## Étape 4 : Exécuter le moteur OCR et capturer les résultats

Voici le cœur du processus — envoyer l'image au moteur OCR et récupérer des données structurées.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Le drapeau `detail=1` nous fournit des boîtes englobantes, dont nous aurons besoin lorsque nous **convert OCR to PDF** plus tard. Si vous ne vous intéressez qu'aux chaînes brutes, définissez `detail=0`.

## Étape 5 : Convertir le résultat OCR en PDF interrogeable – Convertir l'OCR en PDF

EasyOCR ne fournit pas de générateur PDF direct, mais nous pouvons assembler le PDF nous‑mêmes en utilisant Pillow et la bibliothèque `reportlab`. Pour garder le tutoriel léger, nous utiliserons `fpdf2`, qui nous permet d’intégrer l’image originale et de superposer du texte invisible.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Qu’est‑ce qui vient de se passer ? Nous avons placé l’image numérisée comme couche visible, puis écrit les mots reconnus au-dessus en texte blanc qui se fond dans le fond blanc. Les outils de recherche lisent toujours la couche cachée, de sorte que le PDF devient **searchable** sans modifier l’apparence visuelle.

## Étape 6 : Enregistrer les octets du PDF – Convertir l'image en PDF

Si vous préférez manipuler le PDF en mémoire (par ex., l’envoyer via une API), vous pouvez capturer les octets au lieu d’écrire directement sur le disque.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Cette ligne illustre le flux de travail classique **convert image to PDF** : vous partez d’une image, exécutez l’OCR, superposez le texte, puis émettez finalement un flux PDF.

## Étape 7 : Vérifier le résultat – Vérifications rapides

Après avoir exécuté le script, ouvrez `receipt_searchable.pdf` dans n'importe quel lecteur PDF et essayez la boîte de recherche (Ctrl + F). Tapez un mot que vous savez présent dans le reçu — s’il saute à l’endroit correct, vous avez réussi à **create searchable pdf** !  

Si la recherche échoue, revérifiez :

1. Les scores de confiance de l'OCR (valeurs `conf`). Une faible confiance peut indiquer que l'image est floue.  
2. Les coordonnées des boîtes englobantes — parfois EasyOCR les rapporte dans une orientation différente.  
3. Que le lecteur PDF n'est pas réglé en mode « image‑only » (rare, mais certains lecteurs ont cette option).

## Script complet fonctionnel

En réunissant tous les éléments, voici le fichier Python complet, prêt à être exécuté :

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Enregistrez‑le sous le nom `searchable_pdf.py`, remplacez les espaces réservés `YOUR_DIRECTORY` par de vrais chemins, puis lancez :

```bash
python searchable_pdf.py
```

Vous devriez voir un message de confirmation et un tout nouveau PDF interrogeable apparaître dans votre dossier.

## Questions fréquentes & cas particuliers

**Et si l'image est en couleur ?**  
EasyOCR fonctionne avec les images en niveaux de gris et en couleur, mais convertir en niveaux de gris (`pil_image.convert("L")`) peut parfois améliorer la précision sur des scans bruyants.

**Puis‑je gérer des PDF multipages ?**  
Oui — bouclez sur chaque image de page, exécutez les étapes OCR, et ajoutez chaque page au même objet `FPDF`. N’oubliez pas de réinitialiser le curseur (`self.add_page()`) pour chaque nouvelle image.

**Existe‑t‑il un moyen de garder la couche texte originale au lieu du texte blanc invisible ?**  
Si vous avez besoin d’un vrai PDF « texte‑sous‑image » (par ex., pour l’accessibilité), envisagez d’utiliser `pdfminer` ou `pikepdf` pour intégrer une couche texte cachée avec les balises PDF appropriées. C’est plus avancé, mais le principe reste le même : image de fond + texte superposé.

**Et si la confiance OCR est basse ?**  
Vous pouvez filtrer les mots à faible confiance :

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Conclusion – Ce que nous avons accompli

Nous avons commencé avec une simple image de reçu, **performed OCR on image**, extrait les chaînes reconnues, et enfin **create searchable pdf** qui se comporte comme tout document numérisé professionnellement. Le processus a couvert chaque mot‑clé secondaire—**convert OCR to PDF**, **extract text from image**, **convert image to PDF**, et **perform OCR on image**—vous offrant ainsi une boîte à outils réutilisable pour tout projet similaire.

### Prochaines étapes

- Expérimentez d'autres langues en passant leurs codes ISO à `easyocr.Reader(['en', 'es'])`.  
- Remplacez EasyOCR par Tesseract si vous avez besoin d'une solution entièrement hors ligne ; le reste du pipeline reste identique.  
- Ajoutez une visualisation de la confiance OCR (dessinez les boîtes englobantes sur l'image) pour déboguer les scans problématiques.  

Vous avez une variante à partager ? Laissez un commentaire, fork

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convertir des images en PDF C# – Enregistrer le résultat OCR multipage](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Comment OCR une image – Effectuer l'OCR sur une image dans la reconnaissance d'images OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}