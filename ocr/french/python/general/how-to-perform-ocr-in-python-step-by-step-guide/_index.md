---
category: general
date: 2026-01-12
description: Comment effectuer la reconnaissance optique de caractères (OCR) et convertir
  rapidement une image en texte. Apprenez à reconnaître les caractères spéciaux, extraire
  le texte d’une image et charger l’image pour l’OCR avec un exemple complet en Python.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: fr
og_description: Comment effectuer la reconnaissance optique de caractères (OCR) en
  Python, convertir une image en texte et reconnaître les caractères spéciaux. Suivez
  ce guide pratique pour extraire du texte à partir d’images.
og_title: Comment effectuer de l'OCR en Python – Tutoriel complet
tags:
- OCR
- Python
- Image Processing
title: Comment effectuer l'OCR en Python – Guide étape par étape
url: /fr/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer la reconnaissance optique de caractères (OCR) en Python – Guide étape par étape

Vous avez déjà eu besoin d'**effectuer de l'OCR** sur une capture d'écran contenant à la fois des caractères latins et cyrilliques ? Vous n'êtes pas seul. Dans de nombreux projets—qu'il s'agisse de numériser des reçus, d'indexer des documents multilingues ou de créer une archive consultable—**comment effectuer l'OCR** devient rapidement une question cruciale.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre comment **convertir une image en texte**, **reconnaître des caractères spéciaux**, et **extraire du texte d'une image** à l'aide d'une bibliothèque Python simple. À la fin, vous disposerez d'un script prêt à l'emploi qui charge une image pour l'OCR, gère le contenu multilingue et affiche le résultat.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir les prérequis suivants :

- Python 3.8+ installé sur votre machine.  
- Le package `ocr` (ou toute bibliothèque OCR compatible) installé via `pip install ocr`.  
- Un fichier image (`multilingual.png`) contenant à la fois des glyphes latins et cyrilliques.  
- Un éditeur de texte ou un IDE de base—VS Code, PyCharm, ou même un simple Bloc‑notes feront l'affaire.  

Si vous n’avez pas le package `ocr`, vous pouvez le remplacer par `pytesseract` avec quelques modifications mineures ; les concepts de base restent les mêmes.

## Étape 1 : Installer et importer la bibliothèque OCR

Tout d’abord, préparons le moteur OCR. Nous allons importer la bibliothèque, créer une instance du moteur et le configurer pour la prise en charge multilingue.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Pourquoi c’est important :**  
Créer le moteur est la base—sans cela vous ne pouvez pas **charger une image pour l'OCR** plus tard. L’activation des packs de langues garantit que le moteur peut identifier correctement des caractères comme « Ŀ », « Ҕ » et « Ǣ ». Si vous sautez cette étape, vous obtiendrez une sortie illisible pour les scripts non latins.

## Étape 2 : Charger l'image contenant du texte multilingue

Nous pointons maintenant le moteur vers le fichier que nous voulons traiter. Le chemin peut être absolu ou relatif ; assurez‑vous simplement qu’il pointe vers une image lisible.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![exemple de comment effectuer OCR](/images/ocr-example.png "comment effectuer OCR sur une image multilingue")

**Pourquoi c’est important :**  
L’appel `load_image` lit les données de pixels en mémoire, les préparant pour l’algorithme OCR. Si l’image est volumineuse, le moteur peut automatiquement la réduire ; vous pourrez affiner cela plus tard avec `engine.set_max_resolution(3000)` pour des scans haute résolution.

## Étape 3 : Exécuter le processus de reconnaissance

Avec le moteur prêt et l’image chargée, nous pouvons enfin extraire le contenu textuel.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Pourquoi c’est important :**  
`recognize()` effectue le travail lourd du réseau neuronal en arrière‑plan. Il renvoie un objet contenant le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin pour le débogage visuel.

## Étape 4 : Afficher le texte reconnu

Voyons ce que le moteur a trouvé. Nous afficherons le texte dans la console, mais vous pourriez également l’écrire dans un fichier ou une base de données.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Résultat attendu

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Si vous voyez quelque chose de similaire, félicitations—vous avez réussi à **convertir une image en texte** et à **reconnaître des caractères spéciaux**.

## Gestion des problèmes courants

Même avec un script simple, vous pouvez rencontrer quelques obstacles. Voici quelques astuces pratiques tirées de mon expérience.

### 1. Packs de langues manquants

Si vous obtenez des points d’interrogation (`?`) à la place des lettres cyrilliques, vérifiez que les packs de langues sont installés. Pour de nombreux moteurs OCR, vous devez télécharger les fichiers `.traineddata` correspondants et les placer dans le dossier `tessdata` du moteur.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Qualité d’image faible

Les images floues ou à faible contraste produisent des scores de confiance bas. Pré‑traitez l’image avec OpenCV :

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Fichiers volumineux et utilisation de la mémoire

Traiter une photo de 10 Mo peut faire exploser la mémoire. Utilisez `engine.set_max_image_size(2000)` pour limiter la résolution, ou découpez l’image en tuiles et appliquez l’OCR à chaque tuile séparément.

### 4. Capture des boîtes englobantes

Si vous devez mettre en évidence où chaque mot apparaît (utile pour des superpositions UI), accédez à `result.boxes` :

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Script complet – Exécution en un clic

En rassemblant le tout, voici un fichier unique que vous pouvez exécuter avec `python ocr_demo.py`. Il inclut la gestion des erreurs, le pré‑traitement optionnel, et des commentaires pour plus de clarté.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Exécutez‑le avec :

```bash
python ocr_demo.py path/to/multilingual.png
```

Vous devriez voir le même résultat affiché précédemment, confirmant que vous avez **extrait du texte d’une image** avec succès.

## Conclusion

Nous avons couvert **comment effectuer l'OCR** en Python du début à la fin : installation de la bibliothèque, chargement d’une image, reconnaissance de contenu multilingue, et gestion des cas limites les plus courants. En suivant ce guide, vous pouvez maintenant **convertir une image en texte**, **reconnaître des caractères spéciaux**, et **extraire du texte d’une image** dans vos propres projets—plus besoin de transcription manuelle.

Et après ? Essayez d’expérimenter avec :

- Ajouter davantage de packs de langues (par ex., `spa` pour l’espagnol).  
- Exporter les résultats au format JSON pour un traitement en aval.  
- Intégrer l’étape OCR dans une API Flask afin que d’autres services puissent l’appeler.  

Si vous rencontrez des problèmes, la communauté autour de la plupart des bibliothèques OCR est active—recherchez « ocr library language pack installation » ou laissez un commentaire ci‑dessous. Bon codage, et profitez de la transformation des images en texte consultable !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}