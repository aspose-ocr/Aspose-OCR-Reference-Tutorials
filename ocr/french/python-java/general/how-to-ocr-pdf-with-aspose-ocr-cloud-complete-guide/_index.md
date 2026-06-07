---
category: general
date: 2026-06-06
description: Comment effectuer la reconnaissance OCR d’un PDF avec Aspose OCR Cloud.
  Apprenez à extraire le texte d’un PDF, convertir une page PDF en PNG et enregistrer
  les images des pages PDF en Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: fr
og_description: Comment OCR un PDF avec Aspose OCR Cloud. Ce guide montre comment
  extraire le texte brut d’un PDF, convertir une page PDF en PNG et enregistrer les
  images des pages du PDF.
og_title: Comment faire de l'OCR d'un PDF avec Aspose OCR Cloud – Étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Comment OCR un PDF avec Aspose OCR Cloud – Guide complet
url: /fr/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR de PDF avec Aspose OCR Cloud – Guide complet

Vous vous êtes déjà demandé **comment faire de l'OCR de PDF** sans vous battre avec des outils de bureau lourds ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils ont besoin d'une méthode rapide et programmatique pour extraire le texte de documents numérisés. La bonne nouvelle ? Avec Aspose OCR Cloud, vous pouvez **extraire du texte d'un PDF**, transformer chaque page en PNG, et même **enregistrer les images des pages PDF** pour une utilisation ultérieure, le tout depuis un script Python propre.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : de l'installation du SDK, à la licence du moteur, en passant par la reconnaissance de PDF multi‑pages, jusqu'à l'extraction de texte brut, la conversion des pages en PNG et la persistance de ces images sur le disque. À la fin, vous disposerez d'un extrait réutilisable que vous pourrez intégrer à n'importe quel projet nécessitant des capacités **comment faire de l'OCR de PDF**.

## Ce dont vous avez besoin

- **Python 3.8+** (le code fonctionne également sur 3.10 et versions ultérieures)  
- Un compte Aspose OCR Cloud – vous recevrez un fichier de licence d'essai gratuit (`Aspose.OCR.lic`)  
- Le package `asposeocrcloud` (`pip install asposeocrcloud`)  
- Un PDF numérisé, multi‑pages que vous souhaitez traiter  

C’est tout. Aucun binaire supplémentaire, aucune dépendance native, juste du Python pur.

## Comment faire de l'OCR de PDF – Configuration et licence

Avant de pouvoir appeler des méthodes OCR, vous devez indiquer au SDK qui vous êtes. Aspose utilise un fichier de licence léger que vous placez à un endroit accessible à votre script.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Astuce :* Si vous sautez l'étape de licence, le SDK fonctionnera toujours mais ajoutera un petit filigrane aux images de sortie. Ce n’est pas idéal pour la production.

## Étape 2 : Installer le SDK Python Aspose OCR Cloud

Ouvrez un terminal et exécutez :

```bash
pip install asposeocrcloud
```

Le package récupère toutes les dépendances requises (requests, pillow, etc.) afin que vous n'ayez rien d'autre à chercher.

## Étape 3 : Créer un moteur OCR et choisir une langue

Le moteur est le cœur de l'opération. Vous pouvez spécifier n'importe quelle langue prise en charge par Aspose ; l'anglais fonctionne dans la plupart des cas.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Pourquoi définir la langue ? Parce que le moteur OCR utilise des dictionnaires spécifiques à chaque langue pour améliorer la précision. Si vous traitez des PDF en français, remplacez simplement `ENGLISH` par `FRENCH`.

## Étape 4 : Pointer vers votre PDF multi‑pages

Fournissez au moteur le chemin complet du fichier que vous souhaitez traiter. Les chemins relatifs sont acceptables tant qu'ils se résolvent depuis le répertoire de travail du script.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Assurez‑vous que le fichier est lisible ; sinon vous verrez une `FileNotFoundError`.

## Étape 5 : Exécuter l'OCR – Vous obtenez une liste de résultats

Appeler `recognize_pdf` renvoie une liste où chaque élément correspond à une page du PDF source.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Chaque `OcrResult` contient deux propriétés pratiques :

* `text` – la représentation en texte brut de la page (idéal pour **extract plain text pdf**)  
* `image` – un objet `Image` de Pillow de la page rendue (parfait pour **convert pdf page png**)

## Étape 6 : Extraire le texte du PDF et convertir les pages en PNG

Nous parcourons maintenant les résultats, affichons le texte extrait et enregistrons une version PNG de chaque page.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Sortie console attendue

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Vous trouverez également `page_1.png`, `page_2.png`, … dans `YOUR_DIRECTORY`. Ce sont les images rasterisées des pages que vous pouvez injecter dans des pipelines de traitement d'image en aval.

## Étape 7 : Enregistrer les images des pages PDF (post‑traitement optionnel)

Si vous n’avez besoin que des images et pas du texte, vous pouvez ignorer la ligne `print(res.text)`. Inversement, si vous souhaitez stocker le texte dans des fichiers `.txt` séparés, ajoutez simplement une petite écriture :

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

Cette petite addition montre à quel point il est facile de **save PDF page images** tout en conservant le contenu extrait.

## Exemple complet fonctionnel

En rassemblant tous les éléments, voici le script complet que vous pouvez copier‑coller dans `ocr_pdf.py` :

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Exécutez‑le avec :

```bash
python ocr_pdf.py
```

Vous devriez voir l’affichage console du texte de chaque page ainsi qu’une série de fichiers PNG

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment faire de l'OCR de PDF en .NET avec Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Reconnaître le texte PDF – Opérations OCR avec Aspose.OCR pour Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convertir des images en PDF C# – Enregistrer le résultat OCR multi‑pages](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}