---
category: general
date: 2026-03-28
description: Apprenez à faire de l’OCR sur des PDF avec Python rapidement. Ce guide
  vous montre comment extraire du texte d’un PDF, reconnaître le texte d’un PDF et
  convertir un PDF numérisé en texte à l’aide d’Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: fr
og_description: Maîtrisez l'OCR de PDF avec Python. Extrayez le texte d'un PDF, reconnaissez
  le texte d'un PDF et convertissez un PDF numérisé en texte en quelques minutes.
og_title: Comment faire de l'OCR d'un PDF en Python – Guide complet
tags:
- PDF
- OCR
- Python
- Aspose
title: Comment faire de l’OCR d’un PDF en Python – Guide étape par étape
url: /fr/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR de PDF en Python – Guide étape par étape

Vous vous êtes déjà demandé **comment faire de l'OCR de PDF** lorsqu'un fichier n'est qu'une image d'une page ? Vous n'êtes pas seul. Dans ce tutoriel, nous passerons en revue les étapes exactes pour faire de l'OCR de fichiers PDF, extraire du texte d'un PDF et transformer un PDF numérisé en texte recherchable — le tout avec du code Python simple.

Nous couvrirons tout, de l'installation de la bibliothèque Aspose OCR à l'extraction du texte reconnu de chaque page. À la fin, vous pourrez **faire de l'OCR de PDF avec Python**, **extraire du texte d'un PDF**, et **convertir un PDF numérisé en texte** sans devoir fouiller dans une multitude de documents. Pas de blabla, juste un exemple pratique et exécutable que vous pouvez copier‑coller.

## Ce dont vous aurez besoin

Avant de commencer, assurez‑vous d'avoir :

* Python 3.8+ (la dernière version stable fonctionne le mieux)  
* Une licence Aspose OCR for Python ou une clé d'essai gratuite – vous pouvez l'obtenir sur le site d'Aspose.  
* Un PDF numérisé que vous souhaitez traiter (nous l'appellerons `input.pdf`).  

Si vous avez déjà tout cela, super — passons à l'action. Sinon, l'installation du package est un jeu d'enfant et nous vous montrons comment faire.

## Comment faire de l'OCR de PDF – Configuration de l'environnement

La première chose à faire est d'obtenir le module Aspose OCR sur votre machine. Le package s'appelle `aspose-ocr`, et vous pouvez l'installer via pip :

```bash
pip install aspose-ocr
```

> **Astuce :** Utilisez un environnement virtuel (`python -m venv venv`) afin que vos dépendances restent bien organisées.

Une fois le package installé, vous êtes prêt à l'importer et à démarrer le moteur OCR. C’est la base de chaque flux de travail **ocr pdf with python** que vous construirez par la suite.

## OCR de PDF avec Python – Importation d'Aspose OCR

Maintenant que la bibliothèque est disponible, importons‑la dans notre script. Nous définirons également le moteur en *mode PDF direct*, ce qui indique à Aspose de lire les octets du PDF directement depuis le fichier au lieu de convertir chaque page en image d'abord.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Pourquoi utiliser `PdfMode.DIRECT` ? Parce que cela évite une étape supplémentaire de rasterisation, rendant le processus plus rapide et préservant la mise en page originale — très pratique lorsque vous devez **reconnaître du texte à partir d'un PDF** avec précision.

## Reconnaître du texte à partir d'un PDF – Exécution du moteur

Avec le moteur prêt, pointez‑le vers votre fichier numérisé. La méthode `recognize_from_pdf` fait tout le travail lourd : elle analyse chaque page, exécute l'algorithme OCR et renvoie un objet `OcrResult` contenant une collection d'objets `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Si vous vous demandez si cela fonctionne avec des PDF chiffrés — oui, tant que vous fournissez le mot de passe via `ocr_engine.password = "secret"` avant d'appeler `recognize_from_pdf`. C’est un cas de bord que beaucoup de tutoriels négligent, mais qui est utile dans des pipelines réels.

## Extraire du texte d'un PDF – Accéder aux résultats des pages

La liste `ocr_result.pages` contient une entrée par page. Chaque objet `Page` possède un attribut `.text` qui contient la représentation texte brut de la page numérisée. Parcourons‑les et affichons les résultats afin que vous puissiez voir exactement ce qui a été extrait.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

L'exécution du script affichera quelque chose comme :

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Cette sortie prouve que vous avez bien **extrait du texte d'un PDF** et **reconnu du texte à partir d'un PDF** avec Aspose OCR. Vous pouvez maintenant acheminer les chaînes vers une base de données, un index de recherche, ou tout pipeline NLP en aval.

![exemple de OCR de PDF](placeholder-image.png "exemple de OCR de PDF")

*Texte alternatif de l'image :* **exemple de OCR de PDF** – montre la sortie console du texte reconnu page par page.

## Convertir un PDF numérisé en texte – Enregistrement du résultat

La plupart des développeurs ne veulent pas seulement voir le texte dans la console ; ils ont besoin d'un fichier persistant. Voici un petit helper qui écrit le texte de chaque page dans un fichier `.txt` séparé, convertissant ainsi efficacement **un PDF numérisé en texte** dans un dossier nommé `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Après l'exécution du script, vous disposerez d'un répertoire bien organisé :

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Vous avez maintenant complètement **converti un PDF numérisé en texte** et pouvez alimenter ces fichiers dans n'importe quel processus en aval — recherche, analyses, ou même un simple `grep`.

## Questions fréquentes & cas particuliers

**Et si mon PDF contient des images mélangées à du texte réel ?**  
Aspose OCR tentera de tout reconnaître, mais vous pouvez accélérer le traitement en désactivant l'OCR pour les pages qui contiennent déjà du texte sélectionnable. Réglez `ocr_engine.auto_detect_page_orientation = True` puis appelez `ocr_engine.recognize_from_pdf(..., detect_text=False)` pour les pages connues.

**Puis‑je contrôler le modèle de langue ?**  
Absolument. Définissez `ocr_engine.language = aocr.Language.English` (ou toute langue prise en charge) avant d'appeler `recognize_from_pdf`. Cela améliore la précision pour les documents non anglais.

**Comment gérer des PDF très volumineux (100 + pages) ?**  
Traitez‑les par morceaux. La méthode `recognize_from_pdf` accepte un argument `page_range`, par ex. `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Parcourez les intervalles pour garder la consommation mémoire faible.

## Exemple complet fonctionnel

En rassemblant le tout, voici un script unique que vous pouvez placer dans un fichier nommé `ocr_pdf.py` et exécuter :

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Exécutez‑le avec :

```bash
python ocr_pdf.py
```

Vous devriez voir une sortie console confirmant le texte de chaque page ainsi que l'emplacement des fichiers `.txt` enregistrés.

## Conclusion

Nous avons couvert **comment faire de l'OCR de PDF** avec Python, démontré une méthode propre pour **ocr pdf with python**, montré comment **extraire du texte d'un PDF**, expliqué les mécanismes derrière **reconnaître du texte à partir d'un PDF**, et enfin fourni un extrait prêt à l'emploi qui **convertit un PDF numérisé en texte**. L'ensemble du processus est encapsulé

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}