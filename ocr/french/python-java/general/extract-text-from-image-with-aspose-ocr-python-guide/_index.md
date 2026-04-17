---
category: general
date: 2026-03-28
description: Extraire du texte d’une image avec Aspose OCR en Python – apprenez à
  reconnaître le texte d’un PNG, convertir une image en texte avec Python, et charger
  rapidement une image pour l’OCR.
draft: false
keywords:
- extract text from image
- recognize text from png
- convert image to text python
- load image for ocr
- read text from scanned image
language: fr
og_description: Extraire du texte d’une image avec Aspose OCR en Python. Ce tutoriel
  montre comment reconnaître le texte à partir d’un PNG, convertir une image en texte
  avec Python et charger une image pour l’OCR.
og_title: extraire du texte d'une image avec Aspose OCR – guide Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Extraire du texte d’une image avec Aspose OCR – guide Python
url: /fr/python-java/general/extract-text-from-image-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extraire du texte d'une image avec Aspose OCR – guide Python

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais vous n'étiez pas sûr de la bibliothèque qui vous donnerait des résultats fiables sur un scan PNG ? Vous n'êtes pas seul—beaucoup de développeurs rencontrent ce problème lorsqu'ils traitent des PDF numérisés ou des photos de reçus. La bonne nouvelle ? Avec Aspose OCR pour Python, vous pouvez reconnaître du texte à partir de fichiers PNG, convertir une image en texte de style python, et charger l'image pour l'OCR en quelques lignes seulement.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre exactement comment **extraire du texte d'une image** à l'aide d'Aspose OCR. Vous verrez comment charger l'image, activer la détection automatique de la langue, exécuter le moteur OCR, et enfin lire la langue détectée ainsi que le texte extrait. À la fin, vous pourrez intégrer ce code dans n'importe quel projet qui doit lire du texte à partir de fichiers d'images numérisées.

## Ce que vous apprendrez

- Comment **charger l'image pour l'OCR** avec Aspose Storage.
- Comment **reconnaître le texte à partir de PNG** et détecter automatiquement sa langue.
- Comment **convertir une image en texte python** sans manipuler des tampons d'octets de bas niveau.
- Conseils pour gérer les PDF multi‑pages, les pièges courants et les scénarios limites.
- Sortie attendue et méthodes rapides pour vérifier que l'extraction a réussi.

### Prérequis

- Python 3.8 + installé sur votre machine.
- Une licence Aspose OCR pour Python (ou une clé d'essai gratuite) – vous pouvez l'obtenir sur le site web d'Aspose.
- Les packages `aspose-ocr` et `aspose-storage` installés via `pip install aspose-ocr aspose-storage`.
- Un fichier PNG ou tout autre image prise en charge que vous souhaitez traiter.

Maintenant, plongeons‑y.

## Étape 1 : Charger l'image pour l'OCR

Avant que le moteur OCR ne puisse faire quoi que ce soit, il a besoin d'un objet image. Aspose Storage rend cela simple.

```python
# Step 1: Import required Aspose modules
import aspose.ocr as aocr
import aspose.storage as storage

# Step 1.1: Define the path to your image file
input_image_path = "YOUR_DIRECTORY/input_image.png"

# Step 1.2: Load the image – Aspose supports PNG, JPEG, BMP, TIFF, etc.
# The Image class abstracts away file‑system handling.
image = storage.Image.load(input_image_path)
```

*Pourquoi c'est important :* L'utilisation de `storage.Image.load` abstrait les particularités propres aux formats, vous permettant de **reconnaître le texte à partir de png** ou JPEG sans écrire de chargeurs personnalisés. Si le fichier n'est pas trouvé, Aspose lève une `FileNotFoundError` claire, que vous pouvez intercepter pour un repli élégant.

> **Astuce :** Gardez vos images en dessous de 5 Mo pour de meilleures performances. Les fichiers plus volumineux peuvent être réduits avec `image.resize()` avant l'OCR.

## Étape 2 : Initialiser le moteur OCR et activer la détection de langue

Aspose OCR est fourni avec un puissant `OcrEngine` capable de détecter automatiquement la langue du texte qu'il voit. L'activer augmente souvent la précision pour les documents multilingues.

```python
# Step 2: Initialise the OCR engine
ocr_engine = aocr.OcrEngine()

# Step 2.1: Enable automatic language detection (AUTO mode)
ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO
```

*Pourquoi c'est important :* Lorsque vous **convertissez une image en texte python** de style, vous vous souciez généralement de la langue car elle influence le jeu de caractères et le dictionnaire utilisés pendant la reconnaissance. Le mode AUTO permet au moteur de choisir la meilleure correspondance, qu'il s'agisse d'anglais, d'espagnol ou de chinois.

## Étape 3 : Reconnaître le texte à partir de PNG et extraire le résultat

Maintenant, le travail intensif commence. La méthode `recognize` exécute le pipeline OCR et renvoie un objet résultat riche.

```python
# Step 3: Run OCR on the loaded image
ocr_result = ocr_engine.recognize(image)

# Step 3.1: Pull out the detected language and the plain text
detected_lang = ocr_result.detected_language
extracted_text = ocr_result.text
```

Si vous avez seulement besoin de la chaîne brute, `ocr_result.text` est prête à l'emploi. La propriété `detected_language` vous fournit un code ISO‑639‑1 (par ex., `"en"` pour l'anglais).

> **Cas limite :** Pour des scans fortement corrompus, le moteur peut renvoyer une chaîne vide. Dans ce cas, envisagez de prétraiter l'image (augmenter le contraste, redresser) en utilisant des bibliothèques comme Pillow avant de la fournir à Aspose.

## Étape 4 : Afficher le résultat – à quoi s'attendre

Imprimons les résultats afin que vous puissiez vérifier que tout a fonctionné.

```python
# Step 4: Show the detection results
print(f"Detected language: {detected_lang}")
print("Extracted text:")
print(extracted_text)
```

### Exemple de sortie

```
Detected language: en
Extracted text:
Invoice #12345
Date: 2026‑03‑01
Total: $1,250.00
Thank you for your business!
```

Si vous voyez quelque chose de similaire, félicitations—vous avez réussi à **extraire du texte d'une image** avec Aspose OCR ! Si la sortie est illisible, revérifiez que la qualité de l'image est suffisante (au moins 300 dpi pour du texte imprimé).

## Étape 5 : Astuces avancées – gestion des PDF multi‑pages et des documents numérisés

Bien que le flux de base fonctionne pour un seul PNG, les scénarios réels impliquent souvent des PDF multi‑pages ou des piles TIFF.

1. **Convertir les pages PDF en images** – Aspose PDF peut rendre chaque page en PNG, que vous injectez ensuite dans la boucle OCR.
2. **Traitement par lots** – Parcourez un répertoire d'images numérisées, accumulant les résultats dans une liste ou les écrivant dans un CSV.
3. **Sélection de langue personnalisée** – Si vous savez que le document est toujours en français, définissez `ocr_engine.language_detection = aocr.LanguageDetectionMode.FRENCH` pour un gain de vitesse.

```python
# Example: Batch processing a folder of PNGs
import os

folder = "scans/"
texts = []
for file_name in os.listdir(folder):
    if file_name.lower().endswith(".png"):
        img = storage.Image.load(os.path.join(folder, file_name))
        result = ocr_engine.recognize(img)
        texts.append({"file": file_name,
                      "lang": result.detected_language,
                      "text": result.text})
```

Vous avez maintenant une collection pratique que vous pouvez exporter avec `json` ou `pandas`.

## Étape 6 : Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Sortie vide | Image trop basse résolution ou fortement compressée | Augmenter la résolution à ≥300 dpi, utiliser Pillow pour affiner |
| Détection de langue incorrecte | Pages multilingues | Définir manuellement `language_detection` sur une langue spécifique ou traiter chaque page séparément |
| Erreur de mémoire sur de gros lots | Chargement de nombreuses images haute résolution en même temps | Traiter les images une par une, ou utiliser `gc.collect()` après chaque itération |
| Caractères inattendus | Police non prise en charge par le dictionnaire OCR | Activer `ocr_engine.enable_complex_script` si vous traitez de l'arabe ou du hindi |

## Script complet exécutable

Voici le script complet que vous pouvez copier‑coller dans un fichier nommé `extract_text.py`. Remplacez `YOUR_DIRECTORY/input_image.png` par le chemin réel vers votre image.

```python
# extract_text.py
# Complete example: extract text from image with Aspose OCR (Python)

import aspose.ocr as aocr
import aspose.storage as storage

def main():
    # 1️⃣ Load the image
    input_image_path = "YOUR_DIRECTORY/input_image.png"
    try:
        image = storage.Image.load(input_image_path)
    except Exception as e:
        print(f"❗ Unable to load image: {e}")
        return

    # 2️⃣ Initialise OCR engine and enable auto language detection
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language_detection = aocr.LanguageDetectionMode.AUTO

    # 3️⃣ Run OCR
    try:
        ocr_result = ocr_engine.recognize(image)
    except Exception as e:
        print(f"❗ OCR failed: {e}")
        return

    # 4️⃣ Output results
    print(f"Detected language: {ocr_result.detected_language}")
    print("Extracted text:")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Exécutez-le avec :

```bash
python extract_text.py
```

Vous devriez voir la langue détectée suivie du texte extrait affiché dans la console.

## Conclusion

Vous savez maintenant comment **extraire du texte d'une image** à l'aide d'Aspose OCR en Python, depuis le chargement du fichier jusqu'à l'affichage du texte reconnu. Cette solution de bout en bout vous permet de **reconnaître le texte à partir de png**, **convertir une image en texte python** de style, et de **charger l'image pour l'OCR** confortablement dans n'importe quel pipeline d'automatisation.

Prochaines étapes ? Essayez d'alimenter le script avec un lot de reçus numérisés, exportez les résultats vers un CSV, ou intégrez l'étape OCR dans un flux de traitement de documents plus large (par ex., remplissage automatique d'une base de données). Vous pouvez également explorer la bibliothèque Aspose PDF pour transformer des PDF numérisés en documents recherchables—une extension évidente si vous traitez des PDF **lire le texte à partir d'une image numérisée**.

Bon codage, et n'hésitez pas à expérimenter avec différents paramètres de langue, astuces de pré‑traitement d'image, ou même à combiner Aspose OCR avec Tesseract pour une approche hybride. Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—résolvons-les ensemble !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}