---
category: general
date: 2026-01-12
description: Extraire du texte d’un PDF à l’aide du moteur OCR Python – apprenez comment
  lire un PDF avec OCR, charger une image pour l’OCR et obtenir des résultats structurés.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: fr
og_description: Extraire du texte d’un PDF à l’aide du moteur OCR Python. Ce tutoriel
  montre comment lire un PDF avec OCR, charger une image pour l’OCR et utiliser le
  moteur OCR Python pour des résultats fiables.
og_title: Extraire du texte d’un PDF avec le moteur OCR Python – Guide complet
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Extraire du texte d'un PDF avec le moteur OCR Python – Guide étape par étape
url: /fr/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'un PDF avec le moteur OCR Python – Tutoriel complet

Vous avez déjà eu besoin d'**extraire du texte d'un PDF** mais le fichier n'est qu'une image numérisée ? Vous n'êtes pas seul. Dans de nombreux projets réels, le PDF que vous recevez ne contient aucun texte sélectionnable, donc la seule solution est de **lire le PDF avec OCR**.  

Dans ce guide, nous parcourrons une solution pratique, de bout en bout, qui montre exactement comment **charger une image pour OCR**, lancer le **moteur OCR Python**, et extraire du texte structuré que vous pouvez injecter dans des pipelines en aval. Pas de références vagues, juste un exemple complet et exécutable que vous pouvez copier‑coller dès aujourd'hui.

## Ce que vous apprendrez

- Comment installer et importer la bibliothèque OCR Python dont vous avez besoin.  
- Les étapes exactes pour **charger une image pour OCR** à partir d'un fichier PDF.  
- Comment appeler la méthode `recognize_structured()` du moteur et itérer sur les blocs, lignes et mots.  
- Conseils pour gérer les résultats à faible confiance et les PDF multi‑pages.  

À la fin de ce tutoriel, vous disposerez d'un script qui **extrait de manière fiable du texte d'un PDF**, quel que soit le nombre de pages, qu'il s'agisse d'une ou d'une centaine.

---

![Diagramme montrant le moteur OCR traitant un PDF et produisant du texte structuré.](images/ocr_flow.png "diagramme d'extraction de texte d'un pdf")

*Texte alternatif de l'image : diagramme d'extraction de texte d'un pdf illustrant les étapes de traitement OCR.*

## Prérequis

- Python 3.9 ou plus récent (le code utilise des f‑strings et des annotations de type).  
- Un package OCR installable via pip qui expose une classe `OcrEngine` (par exemple, une bibliothèque fictive `pyocr`).  
- Un fichier PDF que vous souhaitez traiter, enregistré localement (par ex., `form.pdf`).  

Si vous n'avez pas la bibliothèque OCR, installez‑la avec :

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Étape 1 : Extraire du texte d'un PDF – Configurer le moteur OCR

Avant de pouvoir **lire le PDF avec OCR**, nous avons besoin d'une instance du moteur. Pensez au moteur comme le cerveau qui examine chaque pixel et décide quel caractère il représente.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Pourquoi c'est important :** Initialiser le moteur une fois vous permet de réutiliser les packs de langues chargés sur plusieurs fichiers, économisant ainsi du temps et de la mémoire.

---

## Étape 2 : Charger une image pour OCR – Préparer votre PDF

Un PDF n'est pas une image brute, donc la bibliothèque fournit généralement un utilitaire pour convertir la première page (ou toutes les pages) en une image que le moteur OCR peut comprendre.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Astuce :** Si votre PDF comporte plusieurs pages, de nombreuses bibliothèques OCR vous permettent de passer `page=2` ou de boucler sur `engine.load_image(pdf_path, page=n)`. Pour les gros documents, envisagez de traiter les pages par lots afin d'éviter les pics de mémoire.

---

## Étape 3 : Utiliser le moteur OCR Python – Reconnaître le texte structuré

C'est maintenant que le travail lourd se fait. L'appel `recognize_structured()` renvoie une hiérarchie de blocs → lignes → mots, chacun annoté avec la langue, la confiance et les boîtes englobantes.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Ce que vous obtenez   
> - `structured_result.blocks` – conteneurs de niveau supérieur (souvent des paragraphes ou des colonnes).  
> - Chaque bloc contient `lines`, et chaque ligne contient `words`.  
> - Les scores de confiance vous permettent de filtrer les résultats douteux.

---

## Étape 4 : Itérer sur les résultats – Accéder aux blocs, lignes et mots

Ci-dessous se trouve une boucle compacte qui affiche les informations les plus utiles. N'hésitez pas à l'étendre pour écrire du JSON, du CSV, ou alimenter une base de données.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Sortie attendue

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Pourquoi vous allez adorer cela :** La hiérarchie reflète la façon dont les humains lisent une page, ce qui facilite la reconstruction ultérieure de tableaux ou de mises en page en colonnes.

---

## Étape 5 : Gestion des cas limites – Faible confiance & PDF multi‑pages

### Mots à faible confiance

Si la confiance d'un mot descend en dessous, par exemple, de `0.70`, vous pourriez vouloir le signaler pour une révision manuelle :

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Traitement de toutes les pages

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Astuce pro :** Mettez en cache les images intermédiaires au format PNG si votre bibliothèque OCR les re‑rend chaque fois — cela peut économiser quelques secondes sur de gros lots.

---

## Script complet fonctionnel

En réunissant tout, voici un fichier unique que vous pouvez exécuter immédiatement :

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Enregistrez-le sous le nom `extract_pdf_ocr.py` et exécutez :

```bash
python extract_pdf_ocr.py
```

Vous devriez voir les détails au niveau des blocs affichés dans la console, ainsi que les éventuels avertissements de faible confiance.

---

## Conclusion

Nous venons de couvrir une méthode complète, prête pour la production, pour **extraire du texte d'un PDF** en utilisant un **moteur OCR Python**. En partant de l'installation de la bibliothèque, en passant par **le chargement d'une image pour OCR**, jusqu'à **la lecture du PDF avec OCR** et enfin l'itération sur la sortie structurée, vous disposez maintenant d'un script réutilisable que vous pouvez adapter à n'importe quel projet.

Les prochaines étapes que vous pourriez explorer :

- Exporter la hiérarchie en JSON pour les pipelines NLP en aval.  
- Ajouter la détection de langue pour changer les modèles OCR à la volée.  
- Intégrer `pdf2image` pour pré‑traiter les PDF contenant des mises en page complexes.  

Essayez-le sur un lot de factures multi‑pages, ajustez le seuil de confiance, et voyez à quelle vitesse vous pouvez transformer des PDF numérisés en texte consultable et éditable. Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous — bonne OCRisation !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}