---
category: general
date: 2026-06-06
description: Exécutez la reconnaissance optique de caractères (OCR) sur une image
  avec Python et consultez les scores de confiance. Apprenez à filtrer les mots à
  faible confiance, à définir des seuils et à gérer les cas limites.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: fr
og_description: Exécutez la reconnaissance optique de caractères (OCR) sur une image
  en Python, inspectez les niveaux de confiance et filtrez les mots à faible confiance.
  Ce tutoriel vous guide à travers un exemple complet et exécutable.
og_title: Exécuter l'OCR sur une image avec Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Exécuter l'OCR sur une image avec Python – Guide complet étape par étape
url: /fr/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter l'OCR sur une image avec Python – Guide complet étape par étape

Vous avez déjà eu besoin d'**exécuter l'OCR sur une image** mais vous ne saviez pas comment obtenir un texte fiable à partir de celle‑ci ? Vous n'êtes pas seul·e — de nombreux développeurs rencontrent le même problème lorsque les mots extraits semblent incertains et que le score de confiance reste un mystère.  

Dans ce guide, nous plongerons directement dans une solution fonctionnelle : vous verrez comment exécuter l'OCR sur image, lire la confiance globale, et extraire les mots à faible confiance qui pourraient nécessiter une révision manuelle. À la fin, vous disposerez d’un script réutilisable, comprendrez pourquoi chaque ligne compte, et saurez comment ajuster le seuil de confiance pour vos propres projets.

## Ce que couvre ce tutoriel

Nous parcourrons l’ensemble du flux de travail — du chargement d’une image à l’impression d’un rapport propre des mots dont la confiance est inférieure à 80 % . En chemin, nous aborderons :

* Le choix d’un moteur OCR solide (nous utiliserons **EasyOCR**, une bibliothèque OCR Python populaire)  
* L’interprétation de l’attribut `confidence` que chaque résultat OCR renvoie  
* Le filtrage des mots avec un **seuil de confiance OCR** personnalisé  
* L’extension du script pour le traitement par lots ou des moteurs alternatifs comme **pytesseract**  

Aucune expérience préalable en OCR n’est requise, juste une familiarité de base avec Python et un environnement de travail (Python 3.9+ recommandé).  

Prêt·e à transformer des captures d’écran floues en texte propre et interrogeable ? C’est parti.

---

## ## Comment exécuter l'OCR sur une image avec Python

Le cœur du tutoriel est un extrait en trois étapes qui reflète le code que vous avez déjà vu. Ci‑dessous, nous décortiquons chaque ligne, expliquons le pourquoi, puis vous fournissons un script complet, prêt à copier‑coller.

### Étape 1 : Installer et importer le moteur OCR

Tout d’abord, assurez‑vous que la bibliothèque OCR est disponible. **EasyOCR** fonctionne immédiatement pour de nombreuses langues et vous fournit un score de confiance par mot.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Why EasyOCR?* It bundles a deep‑learning model that’s been trained on diverse datasets, so you typically get higher confidence values than the older Tesseract engine, especially on mixed‑quality images.

> **Astuce pro :** Si vous êtes dans un environnement contraint (par ex. un petit conteneur Docker), `pytesseract` peut être plus léger, mais vous perdrez une partie de la précision moderne offerte par EasyOCR.

### Étape 2 : Exécuter l'OCR sur l'image

Nous allons maintenant **exécuter l'OCR sur image**. La méthode `recognize_image` de l’exemple original est remplacée par l’appel `readtext` d’EasyOCR, qui renvoie une liste de tuples `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Chaque entrée de `ocr_results` ressemble à :

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Le troisième élément (`0.92` dans l’exemple) est le score de confiance, compris entre 0 et 1.

### Étape 3 : Résumer la confiance globale

Contrairement à l’extrait précédent qui affichait un seul attribut `confidence`, EasyOCR fournit une confiance par mot. Pour obtenir une idée globale, nous allons les moyenner :

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Why average?* It gives you a quick health check—if the overall confidence is below, say, 70 %, you probably need to improve the image (better lighting, preprocessing, etc.).

### Étape 4 : Lister les mots à faible confiance

Voici la partie qui répond directement à la demande « lister les mots dont la confiance est inférieure au seuil souhaité ». Nous fixons par défaut un **seuil de confiance OCR** de 0,80 (80 %), mais vous pouvez l’ajuster.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

La boucle imprime chaque mot qui n’a pas atteint le seuil, accompagné de son pourcentage de confiance. C’est l’analogue exact de la boucle originale `for recognized_word in recognition_result.words`, mais adaptée au format de sortie d’EasyOCR.

---

## ## Comprendre les scores de confiance OCR

La confiance n’est pas un nombre magique ; c’est l’estimation du modèle quant à la certitude de chaque transcription. Gardez à l’esprit les points suivants :

| Situation | Confiance typique | À faire |
|-----------|-------------------|----------|
| Numérisation claire et haute résolution | 0,95 – 1,00 | Aucun travail supplémentaire nécessaire |
| Légère flou ou éclairage inégal | 0,80 – 0,94 | Envisager un pré‑traitement léger (augmentation du contraste) |
| Bruit important, texte tourné | < 0,70 | Appliquer un pré‑traitement (deskew, débruitage) ou changer de moteur OCR |

> **Attention :** Certaines langues (par ex. l’écriture cursive) produisent naturellement des scores plus bas. Ajustez le seuil en conséquence.

### Cas limites et variations

1. **Traitement par lots** – Si vous devez **exécuter l'OCR sur image** en masse, encapsulez la logique ci‑dessus dans une boucle qui parcourt un répertoire.  
2. **Multiples langues** – Passez une liste comme `['en', 'fr']` à `easyocr.Reader` et le moteur détectera les deux.  
3. **Moteurs alternatifs** – Vous voulez essayer **pytesseract** ? Remplacez le bloc lecteur par :

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Vous devrez alors agréger les confiances caractère par caractère en confiances par mot — un peu plus de travail mais faisable.

4. **Astuces de pré‑traitement** – L’application de filtres OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) peut augmenter la confiance pour les scans bruyants.  

---

## ## Script complet, prêt à l'emploi

Voici le fichier Python complet que vous pouvez déposer dans votre projet. Enregistrez‑le sous le nom `ocr_report.py` et lancez `python ocr_report.py`. Assurez‑vous que le chemin de l’image pointe vers un fichier réel.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Résultat attendu** (vos chiffres varieront) :

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Si chaque mot dépasse la barre des 80 %, vous verrez le message amical « Tous les mots respectent le seuil de confiance. » à la place.

---

## ## Questions fréquentes (FAQ)

**Q : Cette méthode fonctionne‑t‑elle avec les PDF ?**  
R : Pas directement. Convertissez chaque page PDF en image d’abord (par ex. avec `pdf2image`) puis alimentez le script avec le PNG/JPEG.

**Q : Mes scores de confiance sont tous bas—que puis‑je faire ?**  
R : Essayez le pré‑traitement : augmentez le contraste, éliminez le bruit de fond, ou pivotez l’image pour la mettre à l’horizontale. EasyOCR accepte également un paramètre `contrast_ths` que vous pouvez ajuster.

**Q : Puis‑je exporter les résultats en CSV ?**  
R : Absolument. Après la boucle des mots à faible confiance, écrivez `ocr_results` dans un `csv.DictWriter` où chaque ligne contient `text`, `confidence` et les coordonnées de la boîte englobante.

**Q : Existe‑t‑il une version accélérée par GPU ?**  
R : EasyOCR utilise automatiquement CUDA si un GPU compatible et PyTorch sont installés. Vérifiez avec `torch.cuda.is_available()` avant d’exécuter le script.

---

## Conclusion

Nous venons d’**exécuter l'OCR sur image** avec Python, d’inspecter la confiance globale, et d’isoler les mots à faible confiance qui nécessitent une révision manuelle.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment définir la valeur du seuil dans la reconnaissance d'image OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Comment utiliser Aspose OCR pour obtenir un résultat JSON dans la reconnaissance d'image](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extraire du texte d'une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}