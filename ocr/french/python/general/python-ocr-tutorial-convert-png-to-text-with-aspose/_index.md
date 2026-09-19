---
category: general
date: 2026-09-19
description: Le tutoriel OCR Python montre comment convertir un PNG en texte à l'aide
  d'Aspose OCR. Apprenez l'extraction de texte OCR en Python et extrayez le texte
  d'images numérisées.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: fr
lastmod: 2026-09-19
og_description: Le tutoriel OCR Python vous guide dans la conversion de PNG en texte
  à l'aide d'Aspose OCR. Maîtrisez l'extraction de texte OCR en Python et extrayez
  le texte d'images numérisées.
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: Tutoriel OCR Python – convertir PNG en texte avec Aspose
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: 'Tutoriel OCR Python : convertir un PNG en texte avec Aspose'
url: /fr/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutoriel OCR Python : convertir PNG en texte avec Aspose

Si vous avez besoin d’un **tutoriel OCR python** qui transforme une image PNG en texte modifiable, ce guide vous fournit une solution complète, prête à l’emploi. Vous verrez comment installer la bibliothèque Aspose OCR, charger une image, exécuter le moteur de reconnaissance et afficher les résultats — le tout en quelques étapes concises.

Numériser un document et extraire le texte peut sembler fastidieux, surtout lorsque vous devez gérer différents formats d’image et paramètres de langue. Ce tutoriel élimine les approximations en vous montrant exactement quelles méthodes appeler et pourquoi elles sont importantes, afin que vous puissiez vous concentrer sur l’intégration de l’OCR dans vos propres applications.

Vous apprendrez également à **convertir PNG en texte**, à gérer les pièges courants et à adapter le code pour d’autres types d’image tels que JPEG ou TIFF. À la fin, vous serez capable d’extraire du texte de n’importe quelle image numérisée avec confiance.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Python 3.8 ou une version plus récente installé.
* Une connexion Internet pour télécharger le package Aspose OCR.
* Une image PNG (ou tout format pris en charge) contenant du texte lisible.

Vous **n’avez pas** besoin d’un moteur OCR séparé ou de binaires externes — Aspose OCR regroupe tout ce dont vous avez besoin.

## Étape 1 : Installer le package Aspose OCR

La première étape consiste à ajouter la bibliothèque à votre environnement. Aspose fournit un package pure‑Python qui peut être installé via pip.

```bash
pip install aspose-ocr
```

> **Astuce :** Utilisez un environnement virtuel (`python -m venv venv`) pour isoler les dépendances des autres projets.

L’installation du package rend le module `aspose.ocr` disponible, contenant la classe `OcrEngine` utilisée tout au long de ce tutoriel.

## Étape 2 : Importer la classe du moteur OCR

Maintenant que le package est présent, importez la classe qui pilote le processus de reconnaissance.

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

`OcrEngine` encapsule toute la logique de chargement d’images, de configuration de la langue et d’extraction du texte. L’importer en haut du script suit les bonnes pratiques Python et garde le code propre.

## Étape 3 : Créer une instance du moteur OCR

Créer une instance vous donne un moteur vierge avec les paramètres par défaut. Vous pourrez ensuite personnaliser des propriétés comme la langue ou le pré‑traitement d’image.

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

Un nouvel objet `engine` représente une session OCR unique. Réutiliser la même instance pour plusieurs images peut améliorer les performances grâce à la mise en cache des ressources internes.

## Étape 4 : Charger l’image à traiter

Indiquez le chemin du fichier PNG que vous souhaitez convertir. La méthode `load_image` accepte tout format supporté par Aspose OCR, vous pouvez donc également fournir des fichiers JPEG, BMP ou TIFF.

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

Si le fichier est introuvable, `load_image` lève une `FileNotFoundError`. En production, encapsulez l’appel dans un bloc try/except pour afficher un message d’erreur convivial.

## Étape 5 : Effectuer l’OCR pour extraire le texte de l’image

Appeler `recognize` lance le pipeline de reconnaissance et renvoie la chaîne extraite. La méthode gère automatiquement l’analyse de mise en page, la segmentation des caractères et la détection de la langue (l’anglais par défaut).

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

Vous pouvez changer la langue avant d’appeler `recognize` :

```python
engine.language = "fr"   # for French text
```

Cette flexibilité est utile lorsque vous avez besoin d’**extraction de texte OCR python** pour des documents multilingues.

## Étape 6 : Afficher le texte reconnu

Enfin, imprimez ou stockez le résultat. Pour une vérification rapide, `print` affiche la chaîne brute dans la console.

```python
# Step 6: Output the recognized text
print(text)
```

### Résultat attendu

Si `sample.png` contient la phrase « Hello, world! », la console affichera :

```
Hello, world!
```

La sortie peut inclure des sauts de ligne ou des espaces supplémentaires selon la mise en page d’origine. Vous pouvez post‑traiter la chaîne avec `str.strip()` ou des expressions régulières pour la nettoyer.

## Gestion des cas limites courants

### 1. Formats non‑PNG

Même si ce tutoriel se concentre sur la **conversion PNG en texte**, vous pouvez recevoir des fichiers JPEG ou TIFF. Le même code fonctionne ; il suffit de changer l’extension du fichier dans `load_image`.

```python
engine.load_image("scanned_page.tiff")
```

### 2. Images à basse résolution

La précision de l’OCR chute en dessous de 150 dpi. Si vous obtenez de mauvais résultats, agrandissez d’abord l’image avec Pillow :

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. Extraction de texte d’une image numérisée contenant plusieurs langues

Définissez une liste de codes de langue séparés par des virgules :

```python
engine.language = "en,es,de"
```

Aspose OCR tentera de reconnaître les caractères de toutes les langues listées.

### 4. Documents volumineux

Traiter de nombreuses pages en une seule exécution peut épuiser la mémoire. Traitez chaque page individuellement :

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## Script complet, exécutable

Assembler toutes les étapes donne un programme autonome que vous pouvez copier, coller et exécuter.

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

Exécutez le script avec :

```bash
python python_ocr_tutorial.py
```

Vous devriez voir le texte extrait affiché dans la console.

## Conclusion

Ce **tutoriel OCR python** a montré comment **convertir PNG en texte** avec Aspose OCR, en couvrant l’installation, le chargement d’image, la reconnaissance et la gestion de la sortie. Vous disposez maintenant d’un modèle fiable pour **l’extraction de texte OCR python**, et vous pouvez l’adapter pour **extraire du texte d’une image python** à partir de n’importe quel document numérisé.

À partir d’ici, envisagez :

* D’intégrer le script dans un service web (par ex., Flask) afin de proposer l’OCR via une API.
* De stocker le texte extrait dans une base de données pour des archives consultables.
* D’expérimenter avec différents paramètres de langue pour gérer des scans multilingues.

Bon codage, et profitez de la transformation d’images en texte recherché et éditable !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Python OCR Tutorial: Extract Table Text from Images](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}