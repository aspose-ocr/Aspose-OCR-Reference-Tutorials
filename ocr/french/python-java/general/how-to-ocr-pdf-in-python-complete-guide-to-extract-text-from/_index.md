---
category: general
date: 2026-06-22
description: Apprenez à OCR des fichiers PDF en Python, à extraire le texte d’un PDF
  et à convertir un PDF en texte en utilisant une approche basée sur les flux. Des
  étapes simples pour traiter les PDF numérisés.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: fr
og_description: Comment faire de l’OCR de fichiers PDF en Python ? Suivez ce guide
  pour extraire le texte d’un PDF, convertir un PDF en texte et traiter les PDF numérisés
  à l’aide d’un flux.
og_title: Comment faire de l’OCR d’un PDF en Python – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Comment faire de l’OCR d’un PDF en Python – Guide complet pour extraire le
  texte des PDF
url: /fr/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR de PDF en Python – Guide complet pour extraire du texte des PDF

Vous vous êtes déjà demandé **comment faire de l'OCR de PDF** sans vous battre avec des outils de bureau lourds ? Vous n'êtes pas le seul. Dans de nombreux projets réels — pensez à l'automatisation des factures ou à la numérisation d'archives — vous avez besoin d'une méthode fiable pour transformer un PDF scanné en texte consultable et modifiable.

Dans ce tutoriel, nous parcourrons un exemple propre, de bout en bout, qui **extrait du texte d'un PDF** en utilisant un moteur OCR Python léger. À la fin, vous saurez exactement comment **convertir un PDF en texte**, comment **charger un PDF depuis un flux**, et comment **traiter un PDF scanné** efficacement. Pas de magie, juste du code Python simple que vous pouvez intégrer à votre projet dès aujourd'hui.

## Ce que vous allez apprendre

- Installer et configurer une bibliothèque OCR Python qui comprend les entrées PDF.  
- Activer le mode de reconnaissance PDF et définir le format de sortie en texte brut.  
- Charger un PDF multi‑pages depuis un flux de fichier (le modèle classique « charger pdf depuis un flux »).  
- Exécuter l'OCR sur toutes les pages et récupérer le contenu textuel.  
- Imprimer ou stocker les résultats pour un traitement en aval.

**Prérequis**  
- Python 3.8+ installé sur votre machine.  
- Familiarité de base avec pip et les environnements virtuels.  
- Un fichier PDF scanné (nommé `multipage.pdf` dans l'exemple) placé dans un répertoire connu.

Si l'un de ces points vous semble inconnu, ne vous inquiétez pas — chaque étape est expliquée en termes simples, et nous fournirons les commandes exactes dont vous avez besoin.

---

## Étape 1 : Installer le moteur OCR (comment faire de l'OCR de PDF)

Tout d'abord, vous avez besoin d'un moteur OCR capable de gérer les entrées PDF. Pour ce guide, nous utiliserons le package hypothétique `ocr` (l'API reflète les SDK commerciaux populaires, mais le même schéma fonctionne avec Tesseract‑OCR, ABBYY ou Google Vision lorsqu'il est correctement encapsulé).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Astuce :** Si vous êtes sous Windows et rencontrez des erreurs de permission, essayez `pip install --user ocr` à la place.

Une fois le package installé, vous pouvez l'importer dans votre script et créer une instance du moteur — c'est le cœur de **comment faire de l'OCR de PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

L'objet `OcrEngine` contient tous les paramètres que nous ajusterons plus tard, comme la langue, le DPI et — surtout — le mode PDF.

## Étape 2 : Activer la reconnaissance PDF et choisir la sortie (extrait du texte d'un PDF)

Par défaut, de nombreux SDK OCR supposent que vous leur fournissez des images. Pour que le moteur traite le flux entrant comme un PDF, nous activons le drapeau de reconnaissance PDF et demandons une sortie en texte brut.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Pourquoi se donner la peine de spécifier le format de sortie ? Parce que certains moteurs peuvent renvoyer un PDF avec des calques de texte cachés, des PDF consultables, ou du JSON avec des boîtes englobantes. Pour la plupart des pipelines d'extraction de données, **extrait du texte d'un PDF** sous forme de chaînes simples est le format en aval le plus propre.

## Étape 3 : Charger le PDF depuis un flux de fichier (charger PDF depuis un flux)

Charger un PDF depuis un flux est un schéma efficace en mémoire — vous évitez de charger le fichier complet en RAM d'un coup. Cela est particulièrement pratique lorsqu'on traite de gros documents multi‑pages.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **Et si le fichier se trouve sur S3 ou un autre bucket cloud ?**  
> Remplacez simplement `from_file` par une méthode qui accepte un tampon d'octets (par ex., `ImageStream.from_bytes(s3_object.read())`). Le reste du pipeline reste identique.

## Étape 4 : Exécuter l'OCR sur toutes les pages (traiter un PDF scanné)

Le travail intensif commence maintenant. Le moteur parcourra chaque page, exécutera le moteur de reconnaissance, et renverra une liste d'objets page — chacun exposant son contenu textuel.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

En coulisses, la bibliothèque OCR décompresse chaque page PDF, la rasterise au DPI configuré, et transmet le bitmap à son modèle de réseau neuronal. Le résultat ? Une collection d'objets `Page` prêts à être extraits.

## Étape 5 : Récupérer et afficher le texte reconnu (convertir PDF en texte)

Enfin, nous parcourons les pages renvoyées et affichons le texte reconnu. C'est le moment où **convertir PDF en texte** se réalise réellement.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Sortie attendue

Si `multipage.pdf` contient trois pages scannées, vous verrez quelque chose comme :

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Remarquez la séparation nette entre les pages — utile si vous devez stocker le texte de chaque page dans une base de données ou le transmettre à un modèle NLP en aval.

## Gestion des cas limites courants

### 1. PDF avec couches d'image et de texte mixtes

Certains PDF contiennent déjà une couche de texte cachée (par ex., exportés depuis Word). Si vous voulez que le moteur OCR **ignore le texte existant** et re‑traite l'image, définissez :

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Fichiers volumineux dépassant les limites de mémoire

Lorsque vous travaillez avec des PDF de plusieurs gigaoctets, envisagez de les traiter par morceaux :

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Prise en charge des langues et des polices

Si vos documents scannés sont en français ou contiennent des caractères spéciaux, indiquez au moteur quel modèle de langue utiliser :

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## Script complet – Prêt à exécuter

Ci-dessous le script complet, exécutable, qui assemble toutes les pièces. Enregistrez-le sous le nom `ocr_pdf.py` et exécutez `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**L'exécution du script** affichera le texte de chaque page dans la console, exactement comme indiqué dans la section « Sortie attendue ». À partir de là, vous pouvez rediriger la sortie vers un fichier :

```bash
python ocr_pdf.py > extracted_text.txt
```

## Conclusion

Nous venons de couvrir **comment faire de l'OCR de PDF** en Python du début à la fin. En configurant le moteur, en chargeant le document via un flux, et en itérant sur chaque page reconnue, vous pouvez **extrait du texte d'un PDF**, **convertir PDF en texte**, et **traiter un PDF scanné** avec seulement quelques lignes. L'approche passe des petites factures de deux pages aux archives massives de plusieurs centaines de pages.

Et ensuite ? Essayez d'alimenter les chaînes extraites dans un index de recherche, un résumeur de modèle de langage, ou un pipeline de validation de données. Vous pouvez également expérimenter avec des formats de sortie comme le JSON pour conserver les métadonnées de position pour une analyse documentaire avancée.

Des questions sur la gestion des PDF chiffrés ou l'intégration avec le stockage cloud ? Laissez un commentaire ci‑dessous — bon codage !

![Diagramme montrant le flux de travail OCR PDF – comment faire de l'OCR PDF, charger PDF depuis un flux, reconnaître les pages et extraire le texte](ocr-pdf-workflow.png "diagramme du flux de travail comment faire de l'OCR PDF")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code fonctionnels complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment faire de l'OCR de PDF en .NET avec Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Comment extraire du texte d'une image avec Aspose.OCR pour .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [Comment extraire du texte d'archives ZIP avec Aspose.OCR pour .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}