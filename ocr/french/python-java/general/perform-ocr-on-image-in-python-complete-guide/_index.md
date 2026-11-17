---
category: general
date: 2026-06-22
description: Effectuez la reconnaissance OCR d’une image avec Python en quelques lignes
  seulement. Apprenez à charger une image pour l’OCR, à reconnaître le texte d’un
  PNG et à utiliser le moteur OCR efficacement.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- load image for OCR
- use OCR engine
language: fr
og_description: Effectuez rapidement une OCR sur une image avec Python. Ce tutoriel
  montre comment charger une image pour l'OCR, reconnaître le texte d’un PNG et utiliser
  le moteur OCR avec confiance.
og_title: Effectuer la reconnaissance optique de caractères (OCR) sur une image en
  Python – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Perform OCR on image using Python in just a few lines. Learn how to
    load image for OCR, recognize text from PNG, and use OCR engine efficiently.
  headline: Perform OCR on Image in Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Effectuer l'OCR sur une image en Python – Guide complet
url: /fr/python-java/general/perform-ocr-on-image-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image en Python – Guide complet

Vous avez déjà eu besoin d'**effectuer une OCR sur une image** mais vous êtes resté bloqué dès la première ligne de code ? Vous n'êtes pas seul. Dans ce guide pas à pas, nous vous montrerons exactement comment **charger l'image pour l'OCR**, configurer un **moteur OCR** léger, et enfin **reconnaître le texte d'un PNG** avec seulement quelques commandes.

Nous couvrirons tout, de l'installation de la bibliothèque à l'ajustement de la liste blanche afin que seuls les chiffres et les lettres majuscules passent le scan. À la fin, vous disposerez d'un script prêt à l'emploi que vous pourrez intégrer à n'importe quel projet — sans mystère, sans fioritures.

## Ce que vous apprendrez

- Comment **utiliser le moteur OCR** de façon programmatique en Python.  
- Les étapes exactes pour **charger l'image pour l'OCR** depuis un dossier local.  
- Pourquoi et comment restreindre la reconnaissance à un jeu de caractères personnalisé.  
- Comment **reconnaître le texte d'un PNG** et gérer le résultat en toute sécurité.  

**Prérequis :** Python 3.7+ installé, un terminal avec lequel vous êtes à l'aise, et une image (par ex. `serial-number.png`) que vous souhaitez lire. Aucune expérience préalable en OCR n'est requise.

---

## Effectuer une OCR sur une image – Initialiser le moteur OCR

La première chose à faire est de créer une instance du moteur OCR. Considérez le moteur comme le cerveau qui analysera les pixels et les transformera en caractères.

```python
import ocr  # Assuming the OCR library is named `ocr`

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Pourquoi c'est important :* Sans moteur, il n'y a rien pour traiter l'image. La classe `OcrEngine` regroupe tout le travail lourd — pré‑traitement, segmentation et classification des caractères — dans un seul objet réutilisable.

---

## Charger l'image pour l'OCR – Fournir le fichier PNG

Maintenant que le moteur existe, vous devez lui fournir l'image que vous souhaitez lire. La bibliothèque attend un objet `ImageStream`, que vous pouvez créer directement à partir d'un chemin de fichier.

```python
# Step 2: Load the image to be processed
image_path = "YOUR_DIRECTORY/serial-number.png"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

*Astuce :* Conservez l'image dans un format à fort contraste (texte noir sur fond blanc) et évitez les artefacts de compression ; ils peuvent perturber l'algorithme OCR.

---

## Restreindre les caractères – Liste blanche des chiffres et lettres majuscules

Souvent, vous ne vous intéressez qu'à un sous‑ensemble de caractères — par exemple, un numéro de série ne contenant que A‑Z et 0‑9. En définissant une liste blanche, vous indiquez au moteur d'ignorer tout le reste, ce qui améliore considérablement la précision.

```python
# Step 3: Restrict recognition to digits and uppercase letters
whitelist = "ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789"
engine.get_settings().set_whitelist(whitelist)
```

*Que se passe-t-il en coulisses ?* Le moteur construit un filtre qui élimine tout glyphe absent de la liste blanche avant l'étape finale de classification. Cela est particulièrement utile lorsque l'image contient du bruit ou du texte décoratif dont vous n'avez pas besoin.

---

## Reconnaître le texte d'un PNG – Exécuter le processus OCR

Avec le moteur prêt et l'image chargée, vous pouvez enfin **effectuer une OCR sur une image**. L'appel `recognize()` exécute la chaîne complète et renvoie un objet résultat.

```python
# Step 4: Perform OCR on the image
result = engine.recognize()
```

Si vous êtes curieux concernant les performances, la méthode se termine généralement en quelques centaines de millisecondes pour un PNG de 300 × 200 px sur un ordinateur portable moderne.

---

## Sortie et vérification – Obtenir le texte reconnu

La dernière étape consiste à extraire le texte brut de l'objet résultat. Tout ce qui ne correspond pas à la liste blanche est automatiquement éliminé, vous obtenez ainsi une chaîne propre prête pour un traitement ultérieur.

```python
# Step 5: Output the recognized text (characters outside the whitelist are ignored)
recognized_text = result.get_text()
print(recognized_text)
```

*Sortie typique :* `AB12C3D4E5` (en supposant que l'image contenait exactement ce numéro de série).  

Si la sortie est vide ou illisible, revérifiez la qualité de l'image et la liste blanche ; un piège fréquent est d'ommettre accidentellement des caractères nécessaires.

---

## Cas limites et pièges courants

| Situation | À vérifier | Correction suggérée |
|-----------|------------|---------------------|
| **Fichier non trouvé** | Faute de frappe dans le chemin ou fichier manquant | Utilisez `os.path.abspath` pour vérifier le chemin complet avant d'appeler `set_image`. |
| **Image à faible contraste** | Le texte se fond avec l'arrière-plan | Appliquez un seuil simple (`Pillow` ou `OpenCV`) avant de fournir l'image au moteur. |
| **Caractères inattendus** | Liste blanche trop restrictive | Ajoutez les caractères manquants à la chaîne de la liste blanche. |
| **Images volumineuses** | Reconnaissance lente | Redimensionnez l'image à une largeur maximale de 1024 px ; la qualité OCR reste généralement élevée. |

---

## Script complet – Prêt à exécuter

Ci-dessous le script complet et autonome qui assemble toutes les pièces. Enregistrez-le sous le nom `ocr_demo.py`, remplacez `YOUR_DIRECTORY` par le dossier réel, et exécutez `python ocr_demo.py`.

```python
import ocr
import os

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a PNG image and return the recognized text.
    Only uppercase letters and digits are allowed.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()

    # Load the PNG image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # Whitelist: A-Z and 0-9
    engine.get_settings().set_whitelist("ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789")

    # Run recognition
    result = engine.recognize()

    # Return clean text
    return result.get_text()

if __name__ == "__main__":
    # Adjust the path to point to your PNG file
    png_path = "YOUR_DIRECTORY/serial-number.png"
    try:
        text = perform_ocr(png_path)
        print("Recognized text:", text)
    except Exception as e:
        print("Error during OCR:", e)
```

*Sortie console attendue* (lorsque le PNG contient `SN12345`) :

```
Recognized text: SN12345
```

---

## Conclusion

Vous savez maintenant exactement comment **effectuer une OCR sur une image** en Python, depuis **charger l'image pour l'OCR** jusqu'à **reconnaître le texte d'un PNG** et enfin extraire un résultat propre à l'aide d'un **moteur OCR** personnalisable. L'approche est simple, extensible et fonctionne immédiatement pour la plupart des scans de type numéro de série.

Et après ? Essayez de remplacer la liste blanche par des lettres minuscules, expérimentez différents formats d'image (JPEG, BMP), ou intégrez le script dans un pipeline de traitement par lots. Le même schéma — moteur → image → paramètres → reconnaissance → sortie — s'applique à pratiquement toute tâche OCR que vous rencontrerez.

Des questions ou une image capricieuse qui refuse de coopérer ? Laissez un commentaire ci‑dessous, et bon codage ! 

![Diagramme illustrant les étapes pour effectuer une OCR sur une image avec Python](https://example.com/ocr-flow.png "Diagramme montrant comment effectuer une OCR sur une image avec un moteur OCR Python")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Convertir l'image en texte – Effectuer une OCR sur une image depuis une URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Comment utiliser AspOCR : filtres de prétraitement d'image OCR pour .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Comment extraire du texte d'une image en préparant des rectangles dans l'OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}