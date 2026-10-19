---
category: general
date: 2026-06-28
description: Apprenez à reconnaître les images de texte avec l'OCR Python, à extraire
  le texte des fichiers PNG et à afficher le texte reconnu avec une gestion d’erreurs
  robuste.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: fr
og_description: Tutoriel étape par étape pour reconnaître une image de texte en Python,
  extraire le texte PNG et afficher le texte reconnu en toute sécurité.
og_title: Reconnaître le texte d’une image avec Python OCR – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Reconnaître le texte d’une image avec Python OCR – Guide complet
url: /fr/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Reconnaître le texte d'image avec Python OCR – Guide complet

Vous vous êtes déjà demandé comment **reconnaître le texte d'image** dans un script Python sans charger un framework lourd ? Vous n'êtes pas seul. De nombreux développeurs ont besoin d'une méthode rapide pour *load image OCR* une capture d'écran, un reçu numérisé ou un simple PNG et récupérer le texte.

Dans ce tutoriel, nous allons configurer un moteur OCR minimal, ajouter un logger personnalisé, **load image OCR**, exécuter le **process image OCR**, et enfin **print recognized text**. À la fin, vous disposerez d'un script autonome qui peut également **extract text png** sur demande.

## Ce que vous en retirerez

- Un extrait de code Python pleinement fonctionnel qui crée un moteur OCR, journalise chaque étape et gère les échecs de manière élégante.  
- Des explications claires du *pourquoi* de chaque ligne — afin que vous puissiez adapter le code à Tesseract, EasyOCR ou tout autre backend.  
- Des astuces pour les pièges courants (polices manquantes, PNG corrompus) et comment les déboguer.  

### Prérequis

- Python 3.8+ installé  
- Une bibliothèque OCR qui expose une classe `OcrEngine` (l'exemple utilise une API fictive mais typique ; remplacez‑la par `pytesseract`, `easyocr`, etc.).  
- Une image PNG que vous souhaitez analyser, enregistrée sous `input.png` dans un dossier que vous contrôlez.  

> **Conseil pro** : Si vous utilisez `pytesseract`, installez d'abord le binaire système Tesseract (`sudo apt install tesseract-ocr` sur Linux) puis `pip install pytesseract pillow`.

---

## ## Reconnaître le texte d'image : Configuration du logger

Un bon logger est le héros méconnu de toute pipeline OCR. Il vous indique *quand* le moteur a démarré, *quel* fichier il a ouvert, et *pourquoi* il a pu échouer.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Pourquoi c'est important :*  
Le logger découple la sortie diagnostique du cœur OCR, ce qui facilite la redirection des journaux vers un fichier, un service de surveillance ou même une interface utilisateur plus tard.  

---

## ## Charger l'image OCR : Alimenter le moteur avec un PNG

Avant que le moteur puisse **process image OCR**, il a besoin d'un objet image approprié. La plupart des bibliothèques acceptent une instance Pillow `Image`.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Points clés :*  

- **load image ocr** – `Image.from_file` abstrait les détails du décodage PNG.  
- Gardez le chemin configurable ; le coder en dur rend le script fragile.  
- L'appel au logger confirme que l'image a été lue avec succès, ce qui est utile lorsque le fichier est manquant ou corrompu.

---

## ## Processus d'image OCR : Reconnaissance du texte

Le gros du travail commence maintenant. Le moteur analyse le bitmap, applique ses réseaux neuronaux ou heuristiques, et renvoie une chaîne Unicode.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Pourquoi nous l'entourons d'un `try/except` :*  
L'OCR peut exploser sur des PNG à basse résolution, des espaces colorimétriques non pris en charge ou des données linguistiques manquantes. Attraper `OcrException` vous permet de **print recognized text** uniquement lorsqu'il existe réellement, évitant ainsi des traces de pile cryptiques pour les utilisateurs finaux.

---

## ## Imprimer le texte reconnu & extraire le texte PNG

Si la reconnaissance a réussi, nous affichons le résultat et, éventuellement, nous l'écrivons dans un fichier `.txt` qui porte le même nom que le PNG d'origine.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*Ce que vous obtenez :*  

- **print recognized text** – retour visuel immédiat dans le terminal.  
- Un fichier `.txt` parallèle qui **extract text png** efficacement pour les traitements en aval (indexation de recherche, saisie de données, etc.).

---

## ## Cas limites courants & comment les gérer

| Situation | Symptôme | Solution |
|-----------|----------|----------|
| PNG uniquement en niveaux de gris | OCR renvoie une chaîne vide | Convertir en RGB (`Image.convert("RGB")`) avant d'alimenter le moteur. |
| Langue non prise en charge | `OcrException` avec le code `LANG_NOT_FOUND` | Installer le pack de langue (par ex., `tesseract‑lang‑fra` pour le français) et définir `ocr_engine.language = "fra"`. |
| Image très grande ( > 5 MB ) | Reconnaissance lente ou erreur de mémoire | Réduire la taille avec `image.thumbnail((2000, 2000))` avant `set_image`. |
| Caractères inattendus | Sortie brouillée | Vérifier que le fichier est réellement un PNG ; certains fichiers se font passer pour du PNG alors qu'ils sont en fait des JPEG. Utiliser `Image.verify()` pour valider. |

---

## ## Exemple complet fonctionnel (prêt à copier‑coller)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Sortie console attendue (cas idéal) :**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

En cas de problème, vous verrez une ligne claire `[ERROR]` avec la raison, grâce au logger personnalisé.

---

## ## Prochaines étapes & sujets associés

- **extract text png** à partir de lots : enveloppez le script dans une boucle `for` qui parcourt un arbre de répertoires.  
- **process image ocr** avec prétraitement (redressement, amélioration du contraste) en utilisant OpenCV avant d'alimenter le moteur.  
- Passer à un service OCR cloud (Google Vision, Azure Read) en échangeant l'implémentation `OcrEngine` — votre code environnant reste identique.  
- Apprendre comment **print recognized text** dans des PDF en utilisant `reportlab` pour la génération de rapports automatisée.  

---

## Conclusion

Nous venons de parcourir une méthode compacte, prête pour la production, afin de **reconnaître le texte d'image** en Python, depuis le chargement du PNG jusqu'à **print recognized text** et la sauvegarde du résultat. En injectant un petit logger, en gérant les exceptions et en persistant éventuellement la sortie, le script est prêt tant pour des expériences rapides que pour une intégration dans des pipelines plus vastes.

Essayez-le avec vos propres captures d'écran, jouez avec le prétraitement d'image, et vous extrairez bientôt du texte de n'importe quel PNG que vous lui présenterez. Des questions ? Laissez un commentaire — bon OCR !  

![exemple de reconnaissance de texte d'image](placeholder.png)


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment effectuer l'extraction de texte d'image depuis un flux avec Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Convertir une image en texte – Effectuer l'OCR sur une image depuis une URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}