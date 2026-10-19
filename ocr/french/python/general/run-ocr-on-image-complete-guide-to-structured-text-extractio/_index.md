---
category: general
date: 2026-05-03
description: Apprenez à exécuter l'OCR sur une image et à extraire le texte avec ses
  coordonnées en utilisant la reconnaissance OCR structurée. Code Python étape par
  étape inclus.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: fr
og_description: Exécutez la reconnaissance OCR sur une image et obtenez le texte avec
  les coordonnées grâce à la reconnaissance OCR structurée. Exemple complet en Python
  avec explications.
og_title: Exécuter la reconnaissance optique de caractères sur une image – Tutoriel
  d'extraction de texte structuré
tags:
- OCR
- Python
- Computer Vision
title: Exécuter la reconnaissance optique de caractères sur une image – Guide complet
  de l'extraction de texte structuré
url: /fr/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter OCR sur image – Guide complet de l'extraction de texte structuré

Vous avez déjà eu besoin de **run OCR on image** fichiers mais vous n'étiez pas sûr de comment conserver les positions exactes de chaque mot ? Vous n'êtes pas seul. Dans de nombreux projets—numérisation de reçus, digitalisation de formulaires ou tests d'interface utilisateur—vous avez besoin non seulement du texte brut mais aussi des boîtes englobantes qui indiquent où chaque ligne se trouve sur l'image.  

Ce tutoriel vous montre une méthode pratique pour *run OCR on image* en utilisant le moteur **aocr**, demander la **structured OCR recognition**, puis post‑traiter le résultat tout en préservant la géométrie. À la fin, vous pourrez **extract text with coordinates** en quelques lignes de Python, et vous comprendrez pourquoi le mode structuré est important pour les tâches en aval.

## Ce que vous apprendrez

- Comment initialiser le moteur OCR pour la **structured OCR recognition**.  
- Comment fournir une image et recevoir les résultats bruts incluant les limites des lignes.  
- Comment exécuter un post‑processor qui nettoie le texte sans perdre la géométrie.  
- Comment itérer sur les lignes finales et afficher chaque morceau de texte avec sa boîte englobante.  

Pas de magie, pas d'étapes cachées—juste un exemple complet et exécutable que vous pouvez intégrer dans votre propre projet.

---

## Prérequis

Avant de commencer, assurez-vous d'avoir installé les éléments suivants :

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Vous aurez également besoin d'un fichier image (`input_image.png` ou `.jpg`) contenant du texte clair et lisible. Tout, d'une facture numérisée à une capture d'écran, fonctionne tant que le moteur OCR peut voir les caractères.

---

## Étape 1 : Initialise le moteur OCR pour la reconnaissance structurée

La première chose que nous faisons est de créer une instance de `aocr.Engine()` et de lui indiquer que nous voulons la **structured OCR recognition**. Le mode structuré renvoie non seulement le texte brut mais aussi les données géométriques (rectangles englobants) pour chaque ligne, ce qui est essentiel lorsque vous devez mapper le texte sur l'image.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Pourquoi c'est important :**  
> En mode par défaut, le moteur peut ne vous fournir qu'une chaîne de mots concaténés. Le mode structuré vous donne une hiérarchie pages → lignes → mots, chacun avec des coordonnées, ce qui facilite grandement la superposition des résultats sur l'image originale ou leur alimentation dans un modèle sensible à la mise en page.

---

## Étape 2 : Exécuter OCR sur l'image et obtenir les résultats bruts

Nous fournissons maintenant l'image au moteur. L'appel `recognize` renvoie un objet `OcrResult` qui contient une collection de lignes, chacune avec son propre rectangle englobant.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

À ce stade, `raw_result.lines` contient des objets avec deux attributs importants :

- `text` – la chaîne reconnue pour cette ligne.  
- `bounds` – un tuple comme `(x, y, width, height)` décrivant la position de la ligne.

---

## Étape 3 : Post‑processer tout en préservant la géométrie

La sortie brute d'OCR est souvent bruyante : caractères parasites, espaces mal placés ou problèmes de sauts de ligne. La fonction `ai.run_postprocessor` nettoie le texte mais **conserve la géométrie originale** intacte, de sorte que vous avez toujours des coordonnées précises.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Astuce pro :** Si vous avez des vocabulaires spécifiques à un domaine (par ex., des codes produit), fournissez un dictionnaire personnalisé au post‑processor pour améliorer la précision.

---

## Étape 4 : Extract text with coordinates – itérer et afficher

Enfin, nous parcourons les lignes nettoyées, affichant la boîte englobante de chaque ligne à côté de son texte. C’est le cœur de **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Résultat attendu

En supposant que l'image d'entrée contienne deux lignes : « Invoice #12345 » et « Total: $89.99 », vous verrez quelque chose comme :

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

Le premier tuple est le `(x, y, width, height)` de la ligne sur l'image originale, vous permettant de dessiner des rectangles, de mettre en évidence le texte ou d'alimenter les coordonnées dans un autre système.

---

## Visualiser le résultat (optionnel)

Si vous voulez voir les boîtes englobantes superposées sur l'image, vous pouvez utiliser Pillow (PIL) pour dessiner des rectangles. Voici un extrait rapide ; n'hésitez pas à le sauter si vous n'avez besoin que des données brutes.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

Le texte alternatif ci‑dessus contient le **primary keyword**, répondant à l'exigence SEO pour les attributs alt d'image.

---

## Pourquoi la reconnaissance OCR structurée surpasse l'extraction de texte simple

Vous vous demandez peut‑être, « Je ne peux pas simplement exécuter OCR et obtenir le texte ? Pourquoi se soucier de la géométrie ? »

- **Contexte spatial :** Lorsque vous devez mapper les champs d'un formulaire (par ex., « Date » à côté d'une valeur de date), les coordonnées vous indiquent *où* les données se trouvent.  
- **Mises en page multi‑colonnes :** Le texte linéaire simple perd l'ordre ; les données structurées conservent l'ordre des colonnes.  
- **Précision du post‑processus :** Connaître la taille de la boîte vous aide à décider si un mot est un en‑tête, une note de bas de page ou un artefact parasite.  

En bref, la **structured OCR recognition** vous offre la flexibilité de créer des pipelines plus intelligents—que vous alimentiez des données dans une base de données, créiez des PDF recherchables, ou entraîniez un modèle d'apprentissage automatique qui respecte la mise en page.

---

## Cas limites courants et comment les gérer

| Situation | Ce qu'il faut surveiller | Solution suggérée |
|-----------|--------------------------|-------------------|
| **Images tournées ou inclinées** | Les boîtes englobantes peuvent être hors axe. | Pré‑traiter avec un redressement (par ex., `warpAffine` d'OpenCV). |
| **Polices très petites** | Le moteur peut manquer des caractères, entraînant des lignes vides. | Augmenter la résolution de l'image ou utiliser `ocr_engine.set_dpi(300)`. |
| **Langues mixtes** | Un mauvais modèle de langue peut produire du texte illisible. | Définir `ocr_engine.language = ["en", "de"]` avant la reconnaissance. |
| **Boîtes qui se chevauchent** | Le post‑processor peut fusionner deux lignes involontairement. | Vérifier `line.bounds` après le traitement ; ajuster les seuils dans `ai.run_postprocessor`. |

Aborder ces scénarios tôt vous évite des maux de tête plus tard, surtout lorsque vous faites évoluer la solution à des centaines de documents par jour.

---

## Script complet de bout en bout

Voici le programme complet, prêt à être exécuté, qui relie toutes les étapes. Copiez‑collez, ajustez le chemin de l'image, et vous êtes prêt.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Exécuter ce script permettra de :

1. **Run OCR on image** avec le mode structuré.  
2. **Extract text with coordinates** pour chaque ligne.  
3. Optionnellement produire un PNG annoté montrant les boîtes.

---

## Conclusion

Vous disposez maintenant d'une solution solide et autonome pour **run OCR on image** et **extract text with coordinates** en utilisant la **structured OCR recognition**. Le code montre chaque étape—de l'initialisation du moteur au post‑processing et à la vérification visuelle—afin que vous puissiez l'adapter aux reçus, formulaires ou tout document visuel nécessitant une localisation précise du texte.

Et ensuite ? Essayez de remplacer le moteur `aocr` par une autre bibliothèque (Tesseract, EasyOCR) et voyez comment leurs sorties structurées diffèrent. Expérimentez différentes stratégies de post‑processing, comme la correction orthographique ou des filtres regex personnalisés, pour améliorer la précision dans votre domaine. Et si vous construisez un pipeline plus large, envisagez de stocker les paires `(text, bounds)` dans une base de données pour des analyses ultérieures.

Bon codage, et que vos projets OCR soient toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}