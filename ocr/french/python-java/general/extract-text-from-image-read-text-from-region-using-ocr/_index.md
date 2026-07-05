---
category: general
date: 2026-07-05
description: Extraire du texte d’une image avec OCR en Python. Apprenez comment charger
  une image pour l’OCR, lire le texte d’une région et extraire le texte d’une facture
  en quelques lignes de code.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: fr
og_description: Extraire du texte d’une image avec Python OCR. Ce guide montre comment
  charger une image pour l’OCR, lire le texte d’une région et extraire rapidement
  le texte d’une facture.
og_title: Extraire le texte d’une image – Lire le texte d’une zone à l’aide de l’OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extraire le texte d’une image – Lire le texte d’une région à l’aide de l’OCR
url: /fr/python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image – Lire du texte d'une région avec l'OCR

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais seule une partie précise compte—comme le montant total sur une facture ? Vous n'êtes pas seul. Dans de nombreux projets réels, vous devrez **lire du texte d'une région** plutôt que d'analyser l'image entière. Heureusement, avec quelques lignes de Python, vous pouvez charger une image pour l'OCR, définir une région d'intérêt (ROI) et récupérer exactement les caractères dont vous avez besoin.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre comment **charger une image pour l'OCR**, configurer un ROI, puis **extraire du texte d'une facture**. À la fin, vous disposerez d'un extrait prêt à l'emploi fonctionnant avec n'importe quelle bibliothèque OCR populaire supportant la reconnaissance par région.

---

## Ce dont vous aurez besoin

- Python 3.8+ (le code fonctionne également avec 3.10)  
- Un paquet OCR qui expose une classe `OcrEngine` (pour la démo, nous utiliserons un module fictif `ocr` ; remplacez‑le par `pytesseract`, `easyocr` ou toute bibliothèque offrant le support ROI)  
- Une image d'exemple—par ex. `invoice.png`—qui contient du texte imprimé clair  
- Une connaissance de base des fonctions et classes Python (pas besoin de connaissances approfondies en deep learning)

Si vous avez déjà tout cela, super—plongeons‑y. Sinon, téléchargez la dernière version de Python depuis python.org et installez le paquet OCR via `pip install your-ocr-lib`.

---

![Exemple d'extraction de texte d'image](extract-text-from-image.png "Extraction de texte d'image – démonstration OCR basée sur la région")

*L'image ci‑dessus illustre la région (rectangle rouge) que nous ciblerons pour **extraire du texte d'une image**.*

---

## Étape 1 : Installer et importer la bibliothèque OCR

Tout d'abord, assurez‑vous que la bibliothèque OCR est disponible dans votre environnement. Le modèle d'importation ci‑dessous fonctionne pour la plupart des paquets qui exposent une classe de haut niveau `OcrEngine`.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Astuce** : Si vous utilisez `pytesseract`, vous devrez installer le binaire Tesseract séparément et définir `pytesseract.pytesseract.tesseract_cmd` vers son chemin.

---

## Étape 2 : Créer le moteur OCR et définir la langue

Créer le moteur est simple, mais spécifier la langue améliore considérablement la précision, surtout pour les factures contenant des chiffres et des mots anglais.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Pourquoi faisons‑nous cela ? Le moteur OCR utilise des modèles linguistiques pour prédire les caractères ; indiquer qu'il doit s'attendre à de l'anglais réduit les faux positifs comme la confusion entre “0” et “O”.

---

## Étape 3 : Charger l'image pour l'OCR

Nous allons maintenant **charger l'image pour l'OCR**. La plupart des bibliothèques acceptent un chemin de fichier ou un objet image Pillow. Ici, nous utilisons le chargeur intégré de la bibliothèque pour plus de simplicité.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Assurez‑vous que le chemin pointe vers le bon répertoire ; une erreur fréquente consiste à oublier le chemin relatif lorsque le script s'exécute depuis un répertoire de travail différent.

---

## Étape 4 : Définir la région d'intérêt (ROI)

Définir le ROI est le cœur de **lire du texte d'une région**. Pensez à cela comme tracer un rectangle autour de la partie de la facture contenant le montant total.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` et `top` représentent les coordonnées X et Y du coin supérieur gauche du rectangle.  
- `width` et `height` définissent la taille de la boîte.  
- Vous pouvez expérimenter avec différentes valeurs à l'aide d'un visualiseur d'image affichant les coordonnées en pixels.

> **Pourquoi le ROI est important :** Exécuter l'OCR sur la page entière gaspille des cycles CPU et introduit souvent du bruit provenant de texte, tableaux ou graphiques non pertinents. En se concentrant sur une région, vous obtenez des résultats plus propres et un traitement plus rapide.

---

## Étape 5 : Effectuer l'OCR sur la région spécifiée

Avec tout configuré, nous **extraitons enfin le texte de l'image**—mais uniquement à l'intérieur du ROI que nous avons défini.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

La méthode `recognize` renvoie un objet contenant généralement la chaîne brute, les scores de confiance et parfois les boîtes englobantes pour chaque mot. Pour notre besoin, nous ne conservons que le texte brut.

---

## Étape 6 : Afficher le texte extrait

Imprimons le résultat et voyons ce que nous obtenons. Cette étape montre **extraire du texte d'une facture** dans un scénario réel.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Sortie attendue

```
Text inside ROI:
Total Amount: $1,245.67
```

Si votre facture utilise une mise en page différente, vous verrez le texte présent dans le rectangle—peut‑être un numéro de facture, une date ou une référence PO.

---

## Étape 7 : Encapsuler le tout dans une fonction réutilisable (optionnel)

Pour rendre la solution réutilisable sur plusieurs factures, encapsulez la logique dans une fonction. Cela illustre également **ocr on region** comme utilitaire générique.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

Vous pouvez maintenant appeler la fonction avec n'importe quelle facture :

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Écueils courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Sortie vide** | Le ROI ne couvre en réalité aucun texte (coordonnées erronées). | Revérifiez les valeurs de pixels avec un éditeur d'image ; ajoutez une superposition de débogage visuelle. |
| **Caractères indésirables** | Résolution d'image basse ou contraste insuffisant. | Pré‑traitez l'image : convertissez en niveaux de gris, appliquez un seuillage (`cv2.threshold`). |
| **Mauvaise langue** | Le moteur utilise par défaut une langue ne contenant pas le jeu de caractères requis. | Définissez explicitement `ocr_engine.language` à `ENGLISH` ou à la locale appropriée. |
| **Ralentissement des performances** | Exécution de l'OCR sur de grandes images de façon répétée. | Redimensionnez l'image avant le chargement, ou ne traitez que le ROI en le découpant d'abord. |

---

## Extension de l'exemple : plusieurs ROI

Parfois, une facture contient plusieurs champs dont vous avez besoin—comme **extraire du texte d'une facture** pour le montant total et la date de la facture. Vous pouvez parcourir une liste de rectangles :

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

Ce schéma garde votre code propre et facilite l'ajout de nouvelles régions ultérieurement.

---

## Conclusion

Nous venons de couvrir un flux de travail complet, de bout en bout, pour **extraire du texte d'une image** à l'aide d'OCR Python, en se concentrant sur une région spécifique. En **chargeant l'image pour l'OCR**, en définissant une **région d'intérêt**, et en invoquant le moteur, vous pouvez de façon fiable **lire du texte d'une région**—idéal pour récupérer les totaux des factures, les dates des reçus ou toute autre donnée localisée.

N'hésitez pas à expérimenter


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants abordent des sujets étroitement liés qui s'appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraire du texte d'image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)
- [Comment extraire du texte d'image en préparant des rectangles dans l'OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}