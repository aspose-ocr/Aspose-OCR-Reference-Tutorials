---
category: general
date: 2026-05-31
description: Apprenez à utiliser la région d'intérêt OCR pour charger une image, effectuer
  l'OCR et extraire le texte d'un rectangle, idéal pour reconnaître le montant sur
  une facture.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: fr
og_description: Maîtrisez la région d'intérêt OCR pour charger l'image pour l'OCR,
  extraire le texte du rectangle et reconnaître le texte d'une facture dans un seul
  tutoriel.
og_title: OCR Région d'intérêt – Guide Python étape par étape
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Région d'intérêt – Extraire le texte d'un rectangle en Python
url: /fr/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Région d'intérêt OCR – Extraire du texte d'un rectangle en Python

Vous vous êtes déjà demandé comment **ocr region of interest** une partie spécifique d'une facture numérisée sans alimenter toute la page dans le moteur ? Vous n'êtes pas le premier à fixer un reçu flou en pensant « Comment extraire le montant qui se trouve quelque part en bas à droite ? » La bonne nouvelle, c'est que vous pouvez indiquer à la bibliothèque OCR exactement où regarder, ce qui augmente considérablement la vitesse et la précision.

Dans ce guide, nous parcourrons un exemple complet et exécutable qui montre comment **load image for OCR**, définir une **region of interest**, puis **extract text from rectangle** pour finalement **recognize text from invoice** et répondre à la question classique « how to extract amount ». Pas de références vagues – seulement du code concret, des explications claires et quelques astuces professionnelles que vous auriez aimé connaître plus tôt.

---

## Ce que vous allez construire

À la fin de ce tutoriel, vous disposerez d’un petit script Python qui :

1. Charge une image de facture depuis le disque.  
2. Marque une ROI rectangulaire où se trouve le montant total.  
3. Exécute l'OCR uniquement à l'intérieur de cette ROI.  
4. Affiche la chaîne du montant nettoyée.  

Tout cela fonctionne avec n'importe quelle bibliothèque OCR qui prend en charge les ROI – ici nous utiliserons un package fictif mais représentatif `SimpleOCR` qui imite des outils populaires comme Tesseract ou EasyOCR. N'hésitez pas à le remplacer ; les concepts restent les mêmes.

---

## Prérequis

- Python 3.8+ installé (`python --version` doit afficher ≥3.8).  
- Un package OCR installable via pip (par ex., `pip install simpleocr`).  
- Une image de facture (PNG ou JPEG) placée dans un dossier que vous pouvez référencer.  
- Une connaissance de base des fonctions et classes Python (rien de compliqué).

Si vous avez déjà tout cela, super—plongeons‑nous dedans. Sinon, récupérez d'abord l'image ; le reste des étapes est indépendant du contenu réel du fichier.

---

## Étape 1 : Charger l'image pour l'OCR

La première chose dont tout flux de travail OCR a besoin est un bitmap à lire. La plupart des bibliothèques exposent une méthode simple `load_image` qui accepte un chemin de fichier. Voici comment le faire avec notre moteur `SimpleOCR` :

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Astuce :** Utilisez des chemins absolus ou `os.path.join` pour éviter les surprises « file not found » lors de l'exécution du script depuis un répertoire de travail différent.

---

## Étape 2 : Définir la région d'intérêt OCR

Au lieu de laisser le moteur scanner toute la page, nous lui indiquons *exactement* où se trouve le montant. C’est l’étape **ocr region of interest**, et c’est la clé d’une extraction fiable, surtout lorsque le document contient des en‑têtes ou pieds‑de‑page bruyants.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Pourquoi ces nombres ? `x` et `y` sont des décalages en pixels depuis le coin supérieur gauche, tandis que `width` et `height` décrivent la taille du rectangle. Si vous n'êtes pas sûr, ouvrez l'image dans n'importe quel éditeur, activez une règle et notez les coordonnées. De nombreux IDE permettent même d'afficher la position du curseur au survol.

---

## Étape 3 : Extraire du texte du rectangle

Maintenant que la ROI est définie, nous demandons au moteur de **recognize text from invoice** mais limité au rectangle que nous venons d'ajouter. L'appel renvoie un objet résultat qui contient généralement la chaîne brute, les scores de confiance et parfois les boîtes englobantes.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

En coulisses, `recognize()` parcourt chaque ROI, découpe cette portion, exécute le modèle OCR et assemble les résultats. C’est pourquoi définir une région **extract text from rectangle** précise peut économiser des secondes de temps de traitement pour les travaux par lots.

---

## Étape 4 : Comment extraire le montant – Nettoyer la sortie

L'OCR n'est pas parfait ; vous obtiendrez souvent des espaces superflus, des sauts de ligne ou même des caractères mal lus (pensez « S » vs « 5 »). Un rapide `strip()` et une petite expression régulière suffisent généralement pour les valeurs monétaires.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Pourquoi c’est important :** Si vous prévoyez d’alimenter le montant dans une base de données ou une passerelle de paiement, vous avez besoin d’un format prévisible. Supprimer les espaces et filtrer les caractères non numériques évite les erreurs en aval.

---

## Étape 5 : Reconnaître le texte de la facture – Script complet

En combinant le tout, voici le script complet, prêt à être exécuté. Enregistrez‑le sous `extract_amount.py` et lancez `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Sortie attendue

```
Amount: 1,245.67
```

Si la ROI est mal alignée, vous pourriez voir quelque chose comme `Amount: 1245.6S`—remarquez le « S » errant. Ajustez les coordonnées du rectangle et relancez jusqu'à ce que la sortie soit propre.

---

## Pièges courants & cas limites

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI trop petite** | Le texte du montant est tronqué, entraînant une reconnaissance partielle. | Agrandissez `width`/`height` d’environ 10‑20 % et retestez. |
| **DPI incorrect** | Les scans à basse résolution (≤150 dpi) réduisent la précision de l'OCR. | Rééchantillonnez l'image à 300 dpi avant le chargement, ou demandez au scanner une résolution plus élevée. |
| **Multiples devises** | L'expression régulière prend le premier groupe numérique, qui peut être le numéro de facture. | Affinez l'expression régulière pour rechercher les symboles monétaires (`$`, `€`, `£`) avant les chiffres. |
| **Factures tournées** | Les moteurs OCR supposent du texte droit ; les pages tournées perturbent la reconnaissance. | Appliquez une correction de rotation (`ocr_engine.rotate(90)`) avant d'ajouter la ROI. |
| **Bruit en arrière‑plan** | Les ombres ou tampons confondent le modèle. | Pré‑traitez avec un simple seuil (`cv2.threshold`) ou utilisez un filtre de débruitage. |

---

## Astuces pro pour les projets réels

- **Traitement par lots :** Parcourez un dossier de factures, calculez la ROI dynamiquement (par ex., basé sur la détection de modèle), et stockez les résultats dans un CSV.  
- **Correspondance de modèles :** Si vous gérez plusieurs mises en page de factures, conservez une carte JSON de `template_id → ROI coordinates`. Changez la ROI en fonction d'un classificateur de mise en page rapide.  
- **Exécution parallèle :** Utilisez `concurrent.futures.ThreadPoolExecutor` pour exécuter plusieurs instances OCR en parallèle—idéal pour les pipelines back‑office à haut volume.  
- **Filtrage par confiance :** La plupart des résultats OCR incluent un score de confiance. Écartez les résultats en dessous d’un seuil (par ex., 85 %) et signalez‑les pour une révision manuelle.

---

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, et enfin **recognize text from invoice** afin de répondre à la question classique **how to extract amount**. Le script est compact, tout en étant suffisamment flexible pour s'adapter à différents formats de documents, langues et back‑ends OCR.

Maintenant que vous avez maîtrisé les bases, envisagez d'étendre le flux de travail : ajouter la lecture de codes‑barres, intégrer un analyseur PDF, ou envoyer le montant extrait à une API comptable. Le ciel est la limite, et avec une ROI bien définie vous obtiendrez toujours des résultats plus rapides et plus propres.

Si vous rencontrez un problème, laissez un commentaire ci‑dessous—bon OCR !

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## Que devriez‑vous apprendre ensuite ?

- [Comment extraire du texte d'une image en préparant des rectangles dans l'OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extraire du texte d'une image Java avec Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extraire du texte d'une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}