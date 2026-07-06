---
category: general
date: 2026-06-16
description: Comment utiliser l'OCR en Python pour extraire du texte à partir de fichiers
  image tels que PNG. Apprenez la conversion étape par étape d’une image en texte
  avec Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- read text from png
- convert image to text
- ocr image to text python
language: fr
og_description: Comment utiliser l'OCR en Python pour extraire du texte à partir d'images.
  Ce guide vous guide à travers la conversion de fichiers PNG en texte consultable
  avec Aspose OCR.
og_title: Comment utiliser l'OCR en Python – Extraire du texte d'images
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  headline: How to Use OCR in Python – Extract Text from Images
  type: TechArticle
- description: How to use OCR in Python to extract text from image files like PNG.
    Learn step‑by‑step conversion of image to text with Aspose OCR.
  name: How to Use OCR in Python – Extract Text from Images
  steps:
  - name: Expected Output
    text: '``` Detected language: English Recognized text: Hello, world! This is a
      multi‑language test. こんにちは世界 ```'
  - name: 1. License Not Found
    text: If you see an error like `License file not found`, double‑check the path
      you passed to `set_license`. Using a raw string (`r"..."`) helps avoid escape‑character
      mishaps on Windows.
  - name: 2. Blank Output
    text: 'A blank `ocr_result.text` usually means the image is too noisy or the text
      is too faint. Try increasing the image contrast:'
  - name: 3. Wrong Language Detection
    text: 'If the auto‑detect picks the wrong language, you can force a specific one:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Aspose
title: Comment utiliser l'OCR en Python – Extraire du texte à partir d'images
url: /fr/python-java/general/how-to-use-ocr-in-python-extract-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en Python – Extraire du texte à partir d'images

Vous vous êtes déjà demandé **comment utiliser l'OCR** dans un projet Python ? Vous n'êtes pas le seul. Que vous construisiez un scanner de reçus, un archiviste de documents, ou que vous soyez simplement curieux de transformer une capture d'écran en texte éditable, la capacité à **extraire du texte à partir d'images** est un véritable changement de jeu.

Dans ce tutoriel, nous parcourrons l'ensemble du processus — de l'installation de la bibliothèque Aspose OCR à la lecture du texte d'un fichier PNG — afin que vous puissiez **convertir une image en texte** en quelques lignes de code seulement. À la fin, vous saurez exactement comment **lire du texte à partir d'un PNG** et même gérer automatiquement du contenu multilingue.

> **Astuce :** La détection automatique de la langue d'Aspose OCR signifie que vous n'avez pas besoin de deviner la langue à l'avance — parfait pour les applications qui voyagent à travers le monde.

## Ce dont vous aurez besoin

- Python 3.8+ (la dernière version stable convient)
- Un fichier de licence Aspose OCR valide (`Aspose.OCR.lic`). L'essai gratuit fonctionne pour les tests, mais une licence appropriée supprime les limites d'évaluation.
- Le package Aspose OCR installé via `pip` :

```bash
pip install aspose-ocr
```

- Un fichier image que vous souhaitez traiter — utilisons `sample-multi-lang.png` comme démonstration.

Avoir ces prérequis prêts garantira un flux fluide et évitera les surprises du type « module not found » plus tard.

![Flux de travail d'utilisation de l'OCR en Python](https://example.com/ocr-workflow.png "Comment utiliser l'OCR en Python – illustration étape par étape")

*Texte alternatif de l'image : Diagramme montrant comment utiliser l'OCR en Python pour extraire du texte d'une image.*

## Étape 1 : Appliquer votre licence Aspose OCR (Nécessaire une fois par application)

La toute première chose qu'un projet OCR sérieux fait est de charger une licence. Sans celle‑ci, Aspose affichera un avertissement et limitera le nombre de pages que vous pouvez traiter.

```python
# Import the license class
from aspose.ocr import License

# Create a License object and point it to your .lic file
ocr_license = License()
ocr_license.set_license(r"C:\Path\To\Your\Aspose.OCR.lic")
```

> **Pourquoi c'est important :** Charger la licence dès le départ garantit que le moteur **ocr image to text python** fonctionne à pleine vitesse et sans filigranes. Considérez cela comme le déverrouillage des fonctionnalités premium avant de commencer la conversion.

## Étape 2 : Créer un moteur OCR et activer la détection automatique de la langue

Nous allons maintenant instancier le moteur principal. Activer `language_auto_detect` est crucial lorsque vous ne savez pas si l'image contient de l'anglais, de l'espagnol, du chinois ou un mélange de langues.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine
ocr_engine = OcrEngine()

# Turn on auto‑language detection – it works for over 60 languages
ocr_engine.language_auto_detect = True
```

Si vous *connaissez* la langue à l'avance, vous pouvez définir `ocr_engine.language = "English"` (ou tout code ISO supporté) pour accélérer légèrement le processus. Mais pour un utilitaire générique de « lecture de texte à partir d'un PNG », l'auto‑détection est le choix le plus sûr.

## Étape 3 : Charger l'image que vous souhaitez traiter

Aspose OCR fonctionne avec une variété de formats — PNG, JPEG, BMP, TIFF, etc. Chargeons un fichier PNG contenant plusieurs langues.

```python
from aspose.ocr import Image

# Load the image from disk (replace with your actual path)
ocr_image = Image.load_from_file(r"C:\Path\To\sample-multi-lang.png")

# Assign the image to the engine
ocr_engine.image = ocr_image
```

> **Cas particulier :** Si l'image est très grande (plus de quelques mégaoctets), vous pourriez vouloir la réduire d'abord pour améliorer les performances. Aspose fournit `ocr_image.resize(width, height)` à cet effet.

## Étape 4 : Effectuer la reconnaissance OCR

Une fois tout configuré, l'extraction réelle du texte se fait en un seul appel de méthode. L'objet résultat vous fournit à la fois le texte reconnu et la langue détectée.

```python
# Run the recognition process
ocr_result = ocr_engine.recognize()
```

En coulisses, Aspose exécute des réseaux neuronaux sophistiqués et des algorithmes de correspondance de motifs pour transformer chaque groupe de pixels en caractères. Le travail intensif est entièrement réalisé en code natif, vous obtenez ainsi une **OCR rapide et précise** même sur du matériel modeste.

## Étape 5 : Afficher la langue détectée et le texte reconnu

Enfin, affichons ce que nous avons obtenu. La propriété `detected_language` indique la langue que Aspose a devinée, et `text` contient la transcription complète.

```python
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

### Résultat attendu

```
Detected language: English
Recognized text:
 Hello, world!
 This is a multi‑language test.
 こんにちは世界
```

Si vous exécutez le script sur une image contenant à la fois de l'anglais et du japonais, vous verrez la langue changer automatiquement — grâce à la fonction d'auto‑détection que nous avons activée précédemment.

## Gestion des problèmes courants

### 1. Licence introuvable

Si vous voyez une erreur comme `License file not found`, vérifiez à nouveau le chemin que vous avez passé à `set_license`. Utiliser une chaîne brute (`r"..."`) aide à éviter les problèmes de caractères d'échappement sous Windows.

### 2. Sortie vide

Une sortie `ocr_result.text` vide signifie généralement que l'image est trop bruitée ou que le texte est trop pâle. Essayez d'augmenter le contraste de l'image :

```python
ocr_image = Image.load_from_file("sample.png")
ocr_image = ocr_image.adjust_contrast(1.5)  # Boost contrast by 50%
ocr_engine.image = ocr_image
```

### 3. Détection de langue incorrecte

Si l'auto‑détection choisit la mauvaise langue, vous pouvez forcer une langue spécifique :

```python
ocr_engine.language = "Japanese"  # ISO code or language name
```

## Extension de l'exemple : traitement par lots de plusieurs fichiers PNG

Souvent, vous voudrez **convertir une image en texte** pour un dossier complet, pas seulement un fichier unique. Voici une boucle rapide qui traite chaque PNG d'un répertoire :

```python
import os
from pathlib import Path

input_folder = Path(r"C:\Images")
output_folder = Path(r"C:\OCR_Output")
output_folder.mkdir(exist_ok=True)

for png_path in input_folder.glob("*.png"):
    # Load and assign image
    ocr_image = Image.load_from_file(str(png_path))
    ocr_engine.image = ocr_image

    # Recognize
    result = ocr_engine.recognize()

    # Write result to a .txt file with the same base name
    txt_path = output_folder / (png_path.stem + ".txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(f"Detected language: {result.detected_language}\n")
        f.write(result.text)

    print(f"Processed {png_path.name} → {txt_path.name}")
```

Cet extrait montre une façon pratique d'**extraire du texte à partir d'images** en masse, une exigence courante pour les pipelines de numérisation de documents.

## Script complet fonctionnel

En rassemblant le tout, voici un fichier unique que vous pouvez exécuter de bout en bout :

```python
# ocr_demo.py
import os
from aspose.ocr import License, OcrEngine, Image

# -------------------------------------------------
# 1️⃣ Apply license (replace with your own path)
# -------------------------------------------------
license_path = r"C:\Path\To\Aspose.OCR.lic"
ocr_license = License()
ocr_license.set_license(license_path)

# -------------------------------------------------
# 2️⃣ Create engine and enable auto‑detect
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.language_auto_detect = True

# -------------------------------------------------
# 3️⃣ Load image (change to your PNG file)
# -------------------------------------------------
image_path = r"C:\Path\To\sample-multi-lang.png"
ocr_image = Image.load_from_file(image_path)
ocr_engine.image = ocr_image

# -------------------------------------------------
# 4️⃣ Recognize and output results
# -------------------------------------------------
ocr_result = ocr_engine.recognize()
print("Detected language:", ocr_result.detected_language)
print("Recognized text:\n", ocr_result.text)
```

Enregistrez-le sous le nom `ocr_demo.py`, exécutez `python ocr_demo.py`, et vous verrez la langue et le texte affichés dans la console.

## Conclusion

Nous avons couvert **comment utiliser l'OCR** en Python du début à la fin, vous montrant comment **extraire du texte à partir d'images**, **lire du texte à partir d'un PNG**, et généralement **convertir une image en texte** en utilisant le puissant moteur d'Aspose. En chargeant une licence, en activant la détection automatique de la langue et en alimentant une image dans le `OcrEngine`, vous obtenez du texte propre et consultable en quelques secondes.

Et ensuite ? Essayez de remplacer Aspose par une alternative open‑source comme Tesseract pour comparer la précision, expérimentez avec des entrées PDF, ou intégrez l'étape OCR dans une API Flask pour un traitement d'image en temps réel. Le ciel est la limite une fois que vous maîtrisez les bases de **ocr image to text python**.

Des questions sur la gestion de polices complexes, l'optimisation des performances ou la licence ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}