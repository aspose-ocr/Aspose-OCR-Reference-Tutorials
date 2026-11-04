---
category: general
date: 2026-06-25
description: Tutoriel OCR Python qui vous montre comment extraire du texte de fichiers
  PNG, lire une image de texte et reconnaître le texte d’une image à l’aide d’un moteur
  simple et gratuit.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: fr
og_description: Le tutoriel Python OCR vous apprend à charger une image pour l'OCR,
  extraire le texte des fichiers PNG et reconnaître le texte d’une image en quelques
  lignes de code seulement.
og_title: Tutoriel OCR Python – Extraire du texte d'un PNG
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Tutoriel OCR Python : Extraire du texte à partir d''images PNG'
url: /fr/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutoriel OCR Python – Extraire du texte d'images PNG

Vous vous êtes déjà demandé comment **python ocr tutorial** peut transformer une capture d'écran d'un reçu en texte modifiable ? Vous n'êtes pas seul. Dans de nombreux projets réels, nous devons *read text image* rapidement, et le faire soi‑même vaut mieux que de copier‑coller depuis une interface graphique à chaque fois.  

Dans ce guide, nous parcourrons un exemple pratique qui **extracts text PNG** des fichiers, vous montre comment *load image for OCR*, et enfin affiche le résultat de *recognize image text* — le tout avec un moteur OCR gratuit, uniquement en mode évaluation. Pas de clés de licence, pas de dépendances lourdes — juste du Python pur et quelques petits paquets.

## Ce que vous allez apprendre

- Comment installer et importer la bibliothèque OCR légère.
- Les étapes exactes pour **load image for OCR** et gérer les pièges courants.
- Méthodes pour **read text image** des fichiers de qualité variable.
- Conseils pour améliorer la précision lorsque vous **extract text png** des fichiers.
- Comment afficher la chaîne reconnue et éventuellement l'écrire sur le disque.

### Prérequis

- Python 3.8 ou plus récent (la bibliothèque fonctionne avec 3.7+ mais 3.8+ est recommandé).
- Familiarité de base avec pip et les environnements virtuels.
- Un fichier image nommé `sample.png` (ou tout PNG que vous souhaitez tester) enregistré dans un dossier que vous pouvez référencer.

Si l'un de ces points vous est inconnu, faites une pause d'une minute et configurez‑les — croyez‑moi, le résultat en vaut la peine.

---

## Tutoriel OCR Python – Configurer le moteur

Première chose à faire : nous avons besoin d’un objet moteur OCR. La bibliothèque que nous allons utiliser est un petit wrapper autour d’un moteur OCR natif qui fonctionne immédiatement en mode évaluation. Elle ne nécessite aucune clé de licence, ce qui rend le *python ocr tutorial* parfait pour les prototypes rapides.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Pourquoi c’est important :** Créer le moteur isole le runtime OCR du reste de votre code, vous permettant de le réutiliser pour plusieurs images sans ré‑initialiser les ressources lourdes à chaque fois.

---

## Charger une image pour OCR – Lire un fichier PNG

Maintenant que le moteur existe, nous devons *load image for OCR*. La méthode `Image.load` de la bibliothèque accepte un chemin et décode automatiquement les formats PNG, JPEG, BMP, et quelques autres.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Astuce :** Si votre PNG contient un canal alpha, la bibliothèque le supprimera automatiquement. Cependant, pour de meilleurs résultats sur les tâches *read text image*, conservez l'image en niveaux de gris — cela réduit le bruit et accélère la reconnaissance.

---

## Reconnaître le texte d'une image – Exécuter le moteur OCR

Avec l'objet image prêt, nous pouvons enfin **recognize image text**. C’est le cœur du *python ocr tutorial* et cela ne nécessite qu’une seule ligne de code.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**Que se passe-t-il en coulisses ?** Le moteur exécute une série de filtres de prétraitement (redressement, binarisation) avant d’alimenter le bitmap dans un réseau neuronal entraîné sur des millions de caractères. C’est pourquoi vous obtenez souvent une sortie étonnamment précise même sur des PNG de basse résolution.

---

## Afficher et enregistrer le texte extrait

Obtenir le résultat est super, mais vous voudrez probablement le voir ou le stocker quelque part. L’objet `result` expose un attribut `text` qui contient la sortie sous forme de chaîne brute.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Sortie attendue** (en supposant que `sample.png` contienne « Hello, OCR! » ):

```
Eval-mode result: Hello, OCR!
```

Si vous obtenez du texte illisible au lieu de caractères lisibles, consultez la section suivante pour les correctifs courants.

---

## Gérer les problèmes courants lors de l'extraction de texte PNG

Même les meilleurs moteurs OCR rencontrent des difficultés avec certaines images. Voici les obstacles typiques et comment les surmonter.

### 1. Faible contraste ou arrière‑plan sombre

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Lignes de texte inclinées

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Caractères non anglais

Si votre PNG contient des lettres accentuées ou des scripts non latins, initialisez le moteur avec le pack de langue approprié :

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Images très grandes

Le traitement d’un PNG 4000×3000 peut être lent. Réduisez‑le tout en préservant la lisibilité :

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Ces ajustements font partie d’un *python ocr tutorial* robuste qui fonctionne au‑delà du scénario idéal.

---

## Script complet – Solution en un seul fichier

Voici le script complet, prêt à l’exécution, qui intègre toutes les étapes et améliorations optionnelles discutées. Copiez‑collez‑le dans `ocr_extract.py` et exécutez `python ocr_extract.py`.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Exécutez‑le :**  
```bash
python ocr_extract.py ./sample.png
```

Vous devriez voir la chaîne reconnue affichée et un fichier `sample_extracted.txt` créé à côté de l’image.

---

## Vue d’ensemble visuelle

![Tutoriel OCR Python – charger une image pour OCR et extraire du texte d'un PNG](/images/python-ocr-flow.png)

*Texte alternatif :* *Diagramme du tutoriel OCR Python montrant le flux depuis le chargement d’une image pour OCR jusqu’à l’extraction du texte PNG.*

---

## Conclusion

Nous venons de terminer un **python ocr tutorial** qui montre comment *load image for OCR*, *recognize image text*, et enfin **extract text png** des fichiers avec seulement quelques commandes Python. Le script est entièrement fonctionnel, gère les cas limites courants, et peut être étendu pour le traitement par lots ou le support multilingue.

Prêt pour le prochain défi ? Essayez d’alimenter le moteur avec des PDF convertis en images, expérimentez différents packs de langue, ou intégrez l’étape OCR dans une API Flask afin que votre application web puisse lire les captures d’écran téléchargées à la volée. Les possibilités d’automatisation *read text image* sont pratiquement infinies.

Des questions ou une image difficile à décoder ? Laissez un commentaire ci‑dessous, et résolvons le problème ensemble. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}