---
category: general
date: 2026-03-26
description: Comment extraire le texte d’un PDF à l’aide de l’OCR. Apprenez à charger
  le PDF comme image, à reconnaître le texte du PDF et à extraire le texte du PDF
  avec un exemple simple en Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: fr
og_description: Comment extraire le texte d’un PDF à l’aide de l’OCR. Ce guide vous
  montre comment charger le PDF en tant qu’image, reconnaître le texte du PDF et extraire
  le texte du PDF en Python.
og_title: Comment extraire le texte d’un PDF avec OCR – Tutoriel complet
tags:
- OCR
- Python
- PDF processing
title: Comment extraire le texte d’un PDF avec OCR – Guide complet étape par étape
url: /fr/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire le texte d'un PDF avec OCR – Guide complet étape par étape

Vous vous êtes déjà demandé **comment extraire le texte d'un PDF** qui n'est en fait qu'une image numérisée ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils ont besoin d'un contenu consultable mais ne disposent que de PDF uniquement image. Bonne nouvelle ? Quelques lignes de code et une bibliothèque OCR solide peuvent transformer ces PDF image en texte brut en un clin d'œil.  

Dans ce tutoriel, nous allons parcourir **comment utiliser l'OCR** pour charger un PDF en tant qu'image, reconnaître le texte du PDF, et enfin **extraire le texte d'un PDF** de n'importe quelle longueur. À la fin, vous disposerez d'un script exécutable, d'une explication claire de chaque étape, et de quelques astuces pour éviter les pièges habituels.

## Ce dont vous avez besoin

- Python 3.9 ou plus récent (le code fonctionne également avec 3.10+)  
- Le package Python `ocr` (ou toute bibliothèque OCR compatible qui expose `OcrEngine`, `OcrEngineMode` et `Imaging.Image`)  
- Un PDF multi‑pages que vous souhaitez traiter (pour la démo, nous l'appellerons `multi_page.pdf`)  
- Une connaissance de base des environnements virtuels (optionnel mais recommandé)

> **Conseil pro** : Si vous êtes sous Windows, envisagez d'utiliser l'Anaconda Prompt ; sous macOS/Linux, une simple commande `python -m venv venv && source venv/bin/activate` fait l'affaire.

## Étape 1 : Installer la bibliothèque OCR

Tout d'abord, récupérez le package OCR depuis PyPI. L'exemple ci‑dessous utilise un package `ocr` fictif qui reflète l'API montrée dans l'extrait de code, mais la plupart des bibliothèques réelles (comme `pytesseract` + `pdf2image`) suivent le même schéma.

```bash
pip install ocr
```

Si vous utilisez un moteur différent, remplacez `ocr` par le nom approprié (par ex., `pip install pytesseract pdf2image`).

## Étape 2 : Initialiser le moteur OCR

Créer une instance du moteur est la base de **comment extraire le texte d'un PDF**. Pensez au moteur comme le cerveau qui interprétera les pixels de chaque page du PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Pourquoi c'est important** : `set_engine_mode` vous permet d'échanger vitesse contre précision. `DEFAULT` est un choix équilibré ; si vous avez besoin d'une précision supérieure, passez à `HIGH_ACCURACY` (si la bibliothèque le supporte).

## Étape 3 : Charger le PDF en tant qu'objet Image

L'OCR fonctionne sur des images, pas sur des conteneurs PDF, nous devons donc d'abord convertir le PDF en une représentation image. La méthode `Imaging.Image.load` gère automatiquement les PDF multi‑pages.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Cas particulier** : Certaines bibliothèques n'acceptent qu'une image à page unique. Dans ce cas, vous parcourriez chaque page avec `pdf2image.convert_from_path`. Notre appel `load` abstrait cela, rendant **load pdf as image** une ligne de code.

## Étape 4 : Reconnaître le texte sur toutes les pages

Vient maintenant le cœur de **recognize PDF text**. Le moteur analyse chaque page, renvoyant une liste d'objets résultat — un par page.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Chaque `page_result` contient des méthodes comme `get_text()` (texte brut) et `get_confidence()` (métrique de qualité optionnelle).  

> **Astuce** : Si vous n'avez besoin que de la première page, appelez `recognize(pdf_image[0])` au lieu de l'aide multi‑pages.

## Étape 5 : Parcourir les résultats et afficher le texte extrait

Enfin, nous parcourons les résultats, affichant le texte de chaque page. Cela complète le flux de travail **extract text from PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Sortie attendue

Si `multi_page.pdf` contient trois pages avec les mots « Hello », « World » et « Python », vous verrez :

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

C’est tout—votre PDF est maintenant entièrement consultable et le texte est prêt pour le traitement en aval (indexation, analyse de sentiment, etc.).

## Étape 6 : Gérer les problèmes courants

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Sortie vide** | Les pages du PDF sont numérisées à faible DPI, rendant les caractères indiscernables. | Agrandir l'image avant l'OCR : `pdf_image = pdf_image.resize(300)` (300 DPI est un bon compromis). |
| **Caractères parasites** | Les alphabets non latins nécessitent des packs de langue. | Charger le modèle de langue approprié : `ocr_engine.load_language('spa')` pour l'espagnol, etc. |
| **Explosion de mémoire sur de gros PDFs** | Charger toutes les pages d'un coup consomme de la RAM. | Traiter les pages par lots : `for img in pdf_image.split(batch=10): …` (pseudo‑code). |
| **Performance lente** | Utiliser `DEFAULT` sur un document massif peut être lent. | Passer en mode `FAST` ou exécuter l'OCR en parallèle avec `concurrent.futures`. |

## Bonus : Enregistrer le texte extrait dans un fichier

La plupart des pipelines réels ont besoin de persister le texte. Voici un petit utilitaire qui écrit tout dans `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Vous pouvez maintenant alimenter `output.txt` dans un moteur de recherche, une base de données, ou tout modèle NLP.

## Assemblage complet – Script complet

Ci‑dessous se trouve le programme complet, prêt à être exécuté. Copiez‑collez, ajustez les chemins de fichiers, et vous êtes prêt.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Exécutez‑le :

```bash
python extract_pdf_ocr.py
```

Vous devriez voir le contenu de chaque page affiché dans la console, suivi d'une confirmation que le fichier `extracted_text.txt` a été créé.

## Conclusion

Nous avons couvert **comment extraire le texte d'un PDF** à partir de documents uniquement image en utilisant un moteur OCR, depuis l'installation de la bibliothèque jusqu'à la gestion des résultats multi‑pages et la sauvegarde de la sortie. Vous savez maintenant **comment utiliser l'OCR**, comment **charger le PDF en tant qu'image**, et comment **reconnaître le texte du PDF** de manière fiable.  

Prochaines étapes ? Essayez de remplacer le mode moteur par défaut par un réglage haute précision, expérimentez les packs de langue pour les PDF multilingues, ou canalisez le texte extrait vers un index de recherche plein texte comme Elasticsearch. Le ciel est la limite une fois que vous avez maîtrisé les bases de l'extraction de texte à partir de fichiers PDF.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="diagramme du flux de travail d'extraction de PDF"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}