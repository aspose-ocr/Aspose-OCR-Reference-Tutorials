---
category: general
date: 2026-07-05
description: Comment redresser rapidement une image. Apprenez à prétraiter une image
  pour l'OCR, corriger la rotation de l'image et convertir une numérisation en texte
  avec Python.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: fr
og_description: Comment redresser une image et prétraiter une image pour l'OCR. Ce
  guide montre comment corriger la rotation d'une image et extraire le texte d'une
  image à l'aide de Python.
og_title: Comment redresser une image – Prétraitement OCR étape par étape
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: Comment redresser une image – Guide complet pour le prétraitement OCR
url: /fr/python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image – Guide complet pour le prétraitement OCR

Vous êtes‑vous déjà demandé **comment redresser une image** qui ressemble à une photo prise avec un scanner de travers ? Vous n'êtes pas le seul. Dans de nombreux projets réels, la première chose à faire avant de pouvoir **extraire du texte d'une image** est de redresser ce désalignement.  

Dans ce tutoriel, nous allons parcourir un exemple pratique, de bout en bout, qui **prétraite l'image pour l'OCR**, corrige la rotation, et enfin **convertit la numérisation en texte** à l'aide d'une bibliothèque OCR Python. Pas de références vagues, juste un script fonctionnel que vous pouvez copier‑coller, plus des astuces sur les pièges courants.  

## Ce que vous allez accomplir

* Charger n'importe quel JPEG ou PNG numérisé légèrement incliné.  
* Appliquer un filtre de redressement et une étape de binarisation pour améliorer la précision de l'OCR.  
* Exécuter le moteur OCR et **extraire du texte d'une image** de façon fiable.  
* Comprendre pourquoi **une rotation correcte de l'image** est importante pour l'extraction de texte en aval.  

### Prérequis

* Python 3.9+ installé sur votre machine.  
* Un package OCR installable via pip qui imite l'espace de noms `ocr` utilisé dans l'exemple (par exemple, un wrapper léger autour de Tesseract).  
* Une connaissance de base des fonctions Python et des concepts de traitement d'image.  

Si vous avez tout cela, plongeons‑y.

![how to deskew image example](deskew_before_after.png){alt="comment redresser une image – avant et après correction"}

## Étape 1 : Configurer le moteur OCR – Comment redresser une image avec Python

First things first: you need an OCR engine that can understand the language of your document.  The snippet below shows the minimal boilerplate to create the engine and tell it you’re working with English text.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Pourquoi c’est important :*  Le paramètre de langue du moteur influence le jeu de caractères et le dictionnaire qu’il utilise. Ignorer cette étape peut amener l'OCR à mal interpréter des mots courants, surtout après que vous ayez **corrigé la rotation de l'image**.

## Étape 2 : Charger l'image numérisée que vous souhaitez redresser

Now we bring the file into memory.  Replace `"YOUR_DIRECTORY/skewed_scan.jpg"` with the path to your own image.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

If the image is already in a NumPy array or an OpenCV `Mat`, you can adapt the loader accordingly – the key is that the object must expose the `apply_filter` method used later.

## Étape 3 : Prétraiter l'image pour l'OCR – Redresser et binariser

Here’s where the magic happens.  We chain two filters:

1. **Deskew** – automatically detects the dominant text baseline and rotates the image back to horizontal.  
2. **Binarize (Otsu)** – converts the picture to pure black‑and‑white, which dramatically improves recognition rates.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Astuce :*  Si vous remarquez que le texte reste flou après la binarisation, essayez d'ajuster le contraste ou d'utiliser une méthode de seuillage différente. Le module `ocr.Filter` inclut souvent `adaptive_threshold()` pour les cas plus difficiles.

## Étape 4 : Exécuter l'OCR – Extraire le texte d'une image

With a clean, straightened canvas, we hand the image to the engine.  The result object contains the recognized string, confidence scores, and even bounding boxes if you need them later.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Typical output looks like:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Notice how the line breaks line up perfectly?  That’s the benefit of **correct image rotation** – the OCR no longer has to guess line orientation.

## Étape 5 : Tout rassembler – Un script monofichier pour convertir une numérisation en texte

Below is the full, runnable script that combines every piece we’ve discussed.  Save it as `deskew_ocr.py` and execute `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Pourquoi cela fonctionne

* **Deskew first** – rotating the image before binarization ensures the threshold algorithm works on a level horizon.  
* **Binarize after deskew** – Otsu’s method assumes a bimodal histogram; a tilted page would ruin that assumption.  
* **English language model** – tells the OCR what characters to expect, reducing false positives.  

If you need to handle other languages, just swap `ocr.Language.ENGLISH` for the appropriate enum.

## Questions fréquentes et cas particuliers

| Question | Réponse |
|----------|--------|
| *Et si la numérisation est à l’envers ?* | Le filtre `deskew()` détecte généralement aussi une rotation de 180°. Si cela échoue, appelez `apply_filter(ocr.Filter.rotate(180))` avant le redressement. |
| *Mon document contient des graphiques en couleur – la binarisation les effacera‑t‑elle ?* | Oui. Pour du contenu mixte, envisagez d’utiliser uniquement `ocr.Filter.deskew()`, puis exécutez l'OCR sur l'image couleur. Vous pouvez toujours extraire le texte tout en conservant les graphiques. |
| *Puis‑je traiter un lot de fichiers ?* | Enveloppez la logique dans une boucle, lisez chaque chemin de fichier depuis une liste, et stockez chaque `result.text` dans un fichier `.txt` séparé. |
| *Comment améliorer la précision sur des numérisations basse résolution ?* | Agrandissez l'image avec un filtre bicubique **avant** le redressement, puis appliquez un filtre de netteté. Plus de pixels donnent au moteur OCR de meilleurs indices. |

## Bonus : Vérification visuelle du redressement

If you want to see the before‑and‑after side by side, add a quick Matplotlib snippet:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

## Conclusion

We’ve covered **how to deskew image** files, why **preprocess image for OCR** is essential, and how to **extract text from image** to finally **convert scan to text**.  The workflow—load → deskew → binarize → recognize—ensures the OCR sees a clean, straight page, which translates into higher accuracy and fewer manual corrections.

What’s next on your OCR journey?  Try experimenting with:

* Different language packs (`ocr.Language.FRENCH`, etc.).  
* Adding a layout analysis step to detect columns or tables.  
* Exporting the OCR results to searchable PDFs using a PDF library.

Feel free to drop a comment if you hit a snag, or share your own tweaks for handling especially stubborn scans.  Happy coding, and may your images always stay perfectly level!

## Que devriez‑vous apprendre ensuite ?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step‑by‑step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Comment utiliser AspOCR : filtres de prétraitement d'image OCR pour .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Comment faire de l'OCR sur une image – Effectuer l'OCR sur une image dans la reconnaissance d'images OCR](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}