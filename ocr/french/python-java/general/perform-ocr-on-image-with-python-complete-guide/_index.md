---
category: general
date: 2026-07-05
description: Effectuez rapidement la reconnaissance optique de caractères (OCR) sur
  une image en Python. Apprenez à charger une image pour l'OCR, extraire le texte
  d'un formulaire numérisé et à utiliser l'OCR pour reconnaître une image en Python.
draft: false
keywords:
- perform OCR on image
- load image for OCR
- how to use OCR Python
- extract text from scanned form
- OCR recognize image Python
language: fr
og_description: Effectuer la reconnaissance optique de caractères (OCR) sur une image
  en Python. Ce tutoriel montre comment charger une image pour l'OCR, extraire le
  texte d'un formulaire numérisé et utiliser l'OCR pour reconnaître une image en Python.
og_title: Effectuer l'OCR sur une image avec Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image in Python quickly. Learn how to load image for
    OCR, extract text from scanned form, and use OCR recognize image Python.
  headline: Perform OCR on Image with Python – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Effectuer l'OCR sur une image avec Python – Guide complet
url: /fr/python-java/general/perform-ocr-on-image-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image avec Python – Guide complet

Vous avez déjà eu besoin de **perform OCR on image** mais vous ne saviez pas par où commencer en Python ? Vous n'êtes pas seul. Que vous numérisiez des reçus, extrayiez des données d’un formulaire d’enquête bruyant, ou simplement transformiez un PDF scanné en texte recherchable, la capacité d’extraire du texte d’un formulaire scanné est un point de douleur quotidien pour de nombreux développeurs.

Dans ce tutoriel, nous parcourrons **how to use OCR Python** bibliothèque étape par étape, depuis le chargement de l’image jusqu’à l’affichage d’un résultat filtré. À la fin, vous saurez exactement comment **load image for OCR**, configurer les seuils de confiance, et appeler la méthode **OCR recognize image Python** qui fait réellement le gros du travail.

> **Ce que vous obtiendrez :** un script prêt à l’emploi qui charge une image, exécute l’OCR et imprime du texte propre, filtré par la confiance. Pas de références vagues, pas d’imports manquants — juste une solution complète à copier‑coller.

---

## Ce dont vous aurez besoin

Avant de plonger, assurez‑vous d’avoir :

* Python 3.9 ou plus récent installé (le code fonctionne également avec 3.10+).  
* Un paquet OCR qui suit l’API `ocr` utilisée ci‑dessous — par exemple, la bibliothèque fictive `simple-ocr` ou tout wrapper exposant `OcrEngine`, `Language` et `Image`.  
* Un fichier image (`.png`, `.jpg`, etc.) contenant le texte que vous souhaitez extraire.  
* Un terminal ou un IDE où vous pouvez exécuter un script Python unique.

Si vous avez déjà tout cela, super — passons à l’action.

---

## Effectuer une OCR sur une image – Configuration du moteur

La première chose à faire est de créer une instance du moteur OCR. Pensez au moteur comme le cerveau derrière l’opération ; il sait comment interpréter les pixels et les transformer en caractères.

```python
# Import the OCR library – replace `ocr` with your actual package name
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Pourquoi c’est important :* sans moteur, il n’y a rien à traiter. L’objet `OcrEngine` contient toute la configuration que vous ajusterez plus tard, comme la langue et le seuil de confiance.

---

## Charger l’image pour l’OCR – Préparer votre formulaire scanné

Maintenant que le moteur existe, nous devons **load image for OCR**. La méthode `Image.load()` de la bibliothèque lit le fichier depuis le disque et le convertit en une représentation interne que le moteur peut comprendre.

```python
# Step 2: Load the image you want to process
# Replace the path with the actual location of your noisy form
image_path = "YOUR_DIRECTORY/noisy_form.png"
image = ocr.Image.load(image_path)
```

> **Astuce :** si vous travaillez avec des PDF, convertissez chaque page en image d’abord (par ex., avec `pdf2image`). Le moteur OCR n’accepte que des images raster.

---

## Comment utiliser OCR Python – Configuration de la langue et de la confiance

La plupart des moteurs OCR supportent plusieurs langues et vous permettent de filtrer les caractères à faible confiance. Définir ces paramètres dès le départ garantit que vous n’obtiendrez que du texte fiable.

```python
# Step 3: Choose language and set a confidence threshold
engine.language = ocr.Language.ENGLISH          # you can switch to FR, DE, etc.
engine.min_confidence = 85                     # accept only characters >85 % confidence
```

*Pourquoi 85 % ?* En pratique, un seuil autour de 80‑90 % élimine la plupart des bavardages tout en conservant les bonnes données. N’hésitez pas à ajuster selon la qualité de vos scans.

---

## Extraire le texte d’un formulaire scanné – Reconnaître l’image

Avec le moteur prêt et l’image chargée, il est temps d’**perform OCR on image**. La méthode `recognize()` renvoie un objet résultat contenant le texte extrait et, éventuellement, les données de boîte englobante.

```python
# Step 4: Perform OCR recognition on the image
result = engine.recognize(image)
```

Si la bibliothèque le supporte, `result` peut aussi exposer `result.confidences` (une liste de scores de confiance par caractère) et `result.words` (objets mot structurés). Pour ce guide, nous nous concentrerons sur la sortie texte brute.

---

## OCR Recognize Image Python – Affichage des résultats filtrés

Enfin, affichons le texte filtré. Les symboles à faible confiance apparaissent sous forme de point d’interrogation (`?`) parce que nous avons fixé `min_confidence` à 85 %.

```python
# Step 5: Show the filtered text
print("Filtered text:")
print(result.text)
```

### Résultat attendu

```
Filtered text:
Name: John Doe
Date: 2023‑04‑15
Amount: $123.45
Signature: ?
```

Remarquez comment la signature illisible s’est transformée en `?`. C’est exactement le rôle du filtre de confiance — garder la sortie propre pour les traitements en aval.

---

## Pièges courants et astuces professionnelles

| Problème | Pourquoi cela se produit | Solution rapide |
|----------|--------------------------|-----------------|
| **Sortie vide** | L’image est trop sombre ou de faible résolution. | Pré‑traiter avec OpenCV : augmenter le contraste, redimensionner à ≥300 dpi. |
| **Caractères parasites** | Mauvaise langue sélectionnée. | Définir `engine.language` pour correspondre au document (ex. `ocr.Language.FRENCH`). |
| **Trop de symboles `?`** | Seuil de confiance trop élevé. | Baisser `engine.min_confidence` à 70‑80 % pour les scans bruyants. |
| **Erreurs Unicode** | La sortie contient des caractères non‑ASCII mais l’encodage du terminal est incorrect. | Exécuter `python -X utf8` ou définir `PYTHONIOENCODING=utf-8`. |

**Astuce pro :** si vous devez extraire des tableaux, effectuez un second passage avec un moteur OCR sensible à la mise en page (comme le `--psm 6` de Tesseract) après avoir filtré le texte brut.

---

## Script complet – Prêt à être exécuté

Voici le script complet, autonome, qui intègre chaque étape abordée. Enregistrez‑le sous le nom `perform_ocr.py`, ajustez le chemin de l’image, puis lancez `python perform_ocr.py`.

```python
# perform_ocr.py
# -------------------------------------------------
# Complete Python script to perform OCR on image,
# load image for OCR, configure engine, and display
# filtered results. Works with any OCR library that
# follows the simple `ocr` API shown here.
# -------------------------------------------------

import ocr  # Replace with your actual OCR package name

def main():
    # 1️⃣ Create the engine
    engine = ocr.OcrEngine()

    # 2️⃣ Configure language and confidence
    engine.language = ocr.Language.ENGLISH
    engine.min_confidence = 85  # Only keep chars >85 % confidence

    # 3️⃣ Load the image (adjust the path)
    image_path = "YOUR_DIRECTORY/noisy_form.png"
    image = ocr.Image.load(image_path)

    # 4️⃣ Recognize the text
    result = engine.recognize(image)

    # 5️⃣ Print the filtered output
    print("Filtered text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

Exécutez‑le, et vous verrez le texte filtré affiché dans la console — exactement ce que promet l’étape **extract text from scanned form**.

---

## Et après ?

Maintenant que vous savez **perform OCR on image** et **extract text from scanned form**, vous pourriez explorer :

* **Traitement par lots** – parcourir un répertoire d’images pour générer un CSV de résultats.  
* **Post‑traitement** – utiliser des expressions régulières ou spaCy pour extraire des champs comme des dates, montants ou identifiants.  
* **Intégrations** – injecter la sortie OCR dans une base de données, Google Sheets ou une API REST.  

Toutes ces idées utilisent les mêmes fonctions de base que nous avons couvertes : charger l’image, configurer le moteur, et appeler la méthode **OCR recognize image Python**.

---

## Conclusion

Nous avons parcouru un exemple complet, prêt pour la production, montrant comment **perform OCR on image** avec Python. De **load image for OCR** à la configuration de la langue, du réglage du seuil de confiance, jusqu’à **extract text from scanned form**, chaque étape a été détaillée avec du code clair et des explications. Vous disposez maintenant d’une base solide pour aborder des scénarios plus complexes — qu’il s’agisse de traitements par lots, de support multilingue ou d’extraction de tableaux.

Lancez le script, ajustez les seuils, et voyez vos documents devenir recherchables en quelques minutes. Des questions ou un formulaire récalcitrant ? Laissez un commentaire ci‑dessous, et résolvons le problème ensemble. Bon codage !

![Exemple de OCR sur image](example.png "Exemple de OCR sur image")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte d’une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment utiliser AspOCR : filtres de pré‑traitement d’image OCR pour .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extraire le texte d’une image en C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}