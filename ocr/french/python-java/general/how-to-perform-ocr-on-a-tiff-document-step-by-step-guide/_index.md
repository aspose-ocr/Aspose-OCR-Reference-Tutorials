---
category: general
date: 2026-01-12
description: Comment effectuer une OCR rapidement et avec précision. Apprenez à exécuter
  l'OCR sur un document, extraire le texte d'un TIFF, charger une image pour l'OCR
  et définir la langue de l'OCR en Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: fr
og_description: Comment effectuer l’OCR en Python. Ce tutoriel vous montre comment
  exécuter l’OCR sur un document, extraire le texte d’un TIFF, charger une image pour
  l’OCR et définir la langue de l’OCR.
og_title: Comment effectuer une OCR sur un document TIFF – Guide complet
tags:
- OCR
- Python
- Image Processing
title: Comment effectuer la reconnaissance optique de caractères (OCR) sur un document
  TIFF – Guide étape par étape
url: /fr/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR sur un document TIFF – Guide complet

Vous vous êtes déjà demandé **comment effectuer une OCR** sur un fichier TIFF numérisé sans passer des heures à chercher la bonne bibliothèque ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent extraire du texte d'images TIFF, surtout lorsque les performances et les paramètres de langue sont importants.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : de l'installation du package OCR, le chargement de l'image pour l'OCR, la configuration de la langue OCR, jusqu'à **exécuter l'OCR sur le document** et extraire du texte propre. À la fin, vous disposerez d'un script prêt à l'emploi que vous pourrez intégrer à n'importe quel projet.

> **Astuce pro :** Bien que l'exemple utilise un module générique `ocr`, les mêmes concepts s'appliquent à Tesseract, EasyOCR ou tout moteur OCR moderne qui expose une API Python.

---

## Ce dont vous aurez besoin

- Python 3.8+ (toute version récente fonctionne)
- Une bibliothèque OCR qui fournit une classe `OcrEngine` (l'exemple utilise un package fictif `ocr` ; remplacez-le par celui que vous utilisez réellement)
- Un fichier TIFF multi‑pages que vous souhaitez traiter (nous l'appellerons `big_document.tif`)
- Une machine avec au moins 4 cœurs CPU si vous prévoyez de définir le nombre de threads

Pas de services externes, pas de clés cloud—juste du code local qui s'exécute en quelques secondes.

![exemple d'exécution d'OCR](/images/ocr-example.png "Comment effectuer une OCR sur un document TIFF")

*Texte alternatif de l'image : comment effectuer une OCR sur un document TIFF – aperçu du texte extrait.*

---

## Étape 1 : Installer et importer la bibliothèque OCR

Première chose à faire : installer la bibliothèque sur votre machine. La plupart des packages OCR sont sur PyPI, donc un simple `pip install` suffit.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Ensuite, importez les classes dont vous avez besoin. Si vous utilisez Tesseract, la ligne d'importation sera différente, mais le reste du code reste identique.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Pourquoi c'est important :* Importer les bons symboles dès le départ évite les conflits de noms plus tard et rend le script plus lisible.

---

## Étape 2 : Créer et configurer le moteur OCR (définir la langue OCR)

Configurer le moteur, c’est là que vous **définissez la langue OCR** pour une reconnaissance précise. L'anglais est la langue par défaut, mais vous pouvez passer au français, à l'allemand, ou même à un mode multilingue avec une seule ligne.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Pourquoi 4 threads ?** La plupart des ordinateurs portables modernes ont au moins quatre cœurs, et limiter le nombre de threads empêche le processus OCR d’occuper toute la machine—particulièrement utile lorsque le script s'exécute sur un serveur partagé.

Si vous avez besoin d’une autre langue, remplacez simplement `ocr.Language.ENGLISH` par `ocr.Language.FRENCH`, `ocr.Language.SPANISH`, etc.

---

## Étape 3 : Charger l'image pour l'OCR (Load Image for OCR)

Nous **chargeons maintenant l'image pour l'OCR**. La méthode `Image.load` lit le fichier TIFF en mémoire, en gérant automatiquement les documents multi‑pages.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Cas limite :* Si le fichier est très volumineux, vous pourriez manquer de RAM. Dans ce cas, envisagez de charger une page à la fois avec `Image.load_page(page_number)` (si la bibliothèque le supporte).

---

## Étape 4 : Exécuter l'OCR sur le document

Avec le moteur prêt et l'image chargée, il est temps de **exécuter l'OCR sur le document**. La méthode `process` effectue le travail lourd et renvoie un objet résultat.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

En coulisses, le moteur divise l'image en blocs de texte, exécute le modèle de reconnaissance et assemble les résultats. L'appel est bloquant, ce qui signifie que le script attend que le TIFF complet soit traité—idéal pour les traitements par lots.

---

## Étape 5 : Extraire le texte du TIFF et vérifier la sortie

Enfin, nous **extrayons le texte du TIFF** en accédant à l'attribut `text` du résultat. Imprimons les 200 premiers caractères comme vérification rapide.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Sortie attendue (exemple) :**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Si vous avez besoin du texte complet, utilisez simplement `ocr_result.text`. Pour un traitement en aval, vous pourriez vouloir l'écrire dans un fichier `.txt` :

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

---

## Exemple complet fonctionnel

En réunissant le tout, voici un script prêt à l'exécution. Remplacez le nom de package fictif par celui que vous avez réellement installé.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Exécutez le script avec :

```bash
python ocr_tiff_example.py
```

Vous devriez voir un aperçu affiché dans la console et un fichier nommé `extracted_text.txt` contenant la transcription complète.

---

## Questions fréquentes & cas limites

- **Et si le TIFF contient plusieurs pages ?**  
  La plupart des moteurs OCR traitent chaque page comme une image distincte en interne. `ocr_result.text` contiendra un saut de ligne entre les pages. Si vous avez besoin d'un traitement page par page, itérez avec `Image.load_page(page_number)`.

- **Puis-je traiter un PNG ou JPEG à la place d'un TIFF ?**  
  Bien sûr. La méthode `Image.load` accepte généralement tout format supporté par Pillow ou la bibliothèque sous‑jacente. Changez simplement l'extension du fichier.

- **Mon texte est illisible—devrais-je changer la langue ?**  
  Oui. L'étape **définir la langue OCR** est cruciale pour les documents non‑anglais. Assurez‑vous que le pack de langue est installé (par ex., `tesseract‑lang‑fra` pour le français).

- **Manque de mémoire ?**  
  Réduisez le `set_memory_limit` ou traitez les pages une par une. Certains moteurs permettent également de réduire la résolution de l'image avant la reconnaissance.

---

## Conclusion

Voilà—un guide concis et entièrement fonctionnel sur **comment effectuer une OCR** sur un fichier TIFF avec Python. Nous avons couvert tout, de l'installation de la bibliothèque, la configuration du moteur (y compris **définir la langue OCR**), **charger l'image pour l'OCR**, **exécuter l'OCR sur le document**, et enfin **extraire le texte du TIFF**.  

N'hésitez pas à expérimenter : ajustez le nombre de threads, changez de langue, ou alimentez la sortie OCR dans un pipeline de traitement du langage naturel. Le ciel est la limite une fois que vous avez maîtrisé les bases.

Vous avez d'autres questions ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}