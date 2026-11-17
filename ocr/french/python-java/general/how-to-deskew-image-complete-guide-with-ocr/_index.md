---
category: general
date: 2026-03-26
description: Apprenez à redresser une image, à reconnaître le texte d’une image et
  à créer un pipeline de prétraitement d’images pour éliminer le bruit d’un scan et
  convertir l’image numérisée en texte.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: fr
og_description: Comment redresser une image et transformer un scan incliné en texte
  recherchable. Suivez ce guide pour reconnaître le texte à partir d’une image, éliminer
  le bruit du scan et convertir l’image numérisée en texte.
og_title: Comment redresser une image – Guide OCR étape par étape
tags:
- OCR
- image-processing
- Python
title: Comment redresser une image – Guide complet avec OCR
url: /fr/python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment deskew une image – Guide complet avec OCR

Vous vous êtes déjà demandé **comment deskew image** qui provient d'un scanner bon marché ? Vous n'êtes pas seul. Une page de travers a l'air non professionnel, et surtout, l'inclinaison peut perturber tout moteur OCR essayant de **reconnaître le texte à partir d'une image**.  

Dans ce tutoriel, nous parcourrons une **pipeline de prétraitement d'image** complète qui deskew, binarise et débruite un scan, puis le transmet à un moteur OCR afin que vous puissiez **convertir une image scannée en texte** avec un minimum de tracas. Pas de magie, juste du Python pur et une petite bibliothèque qui fait le gros du travail.

## Ce dont vous avez besoin

- Python 3.9+ (le code fonctionne sur 3.10 et plus)
- Le package `ocr` (installez via `pip install ocr‑toolkit` – remplacez par le nom réel de votre bibliothèque)
- Un JPEG ou PNG scanné qui est visiblement incliné (par ex., `skewed_scan.jpg`)
- Un peu de curiosité sur la raison pour laquelle chaque étape de prétraitement est importante

C’est tout. Pas de dépendances lourdes comme OpenCV sauf si vous souhaitez aller plus loin plus tard.

## Étape 1 : Charger l'image scannée

La première chose est de charger le fichier en mémoire. Cette étape est simple mais cruciale — si le chemin est incorrect, tout le reste plante.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Pourquoi ?**  
> Charger l'image nous fournit un objet manipulable avec lequel le `ocr.ImagePreprocessor` peut travailler. Sauter cette étape laisserait la pipeline aveugle aux données réelles des pixels.

## Comment deskew une image et la préparer pour l'OCR

Maintenant que nous avons l'image, redressons‑la. La méthode `deskew()` estime l'angle d'inclinaison et fait pivoter l'image pour la remettre à l'horizontale.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Conseil pro :** Si vos scans sont seulement légèrement inclinés (≤ 3°), l'algorithme par défaut est généralement parfait. Pour des angles extrêmes, vous pourriez devoir ajuster les paramètres internes — consultez la documentation de la bibliothèque pour `max_angle`.

## Binariser l'image – La rendre noir et blanc

Les moteurs OCR adorent les entrées à fort contraste. Convertir l'image en une représentation binaire (noir et blanc) élimine les nuances subtiles qui peuvent perturber la reconnaissance de caractères.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **Qu'arrive‑t‑il ?**  
> Les pixels plus clairs que 128 deviennent blancs ; tout le reste devient noir. Ajustez le seuil si votre scan est anormalement sombre ou clair.

## Supprimer le bruit du scan avant l'OCR

Même une image parfaitement deskew peut contenir des taches, de la poussière ou des artefacts de compression. Ces petites taches sont le fléau de tout moteur OCR.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Pourquoi supprimer le bruit ?**  
> Le bruit crée de fausses bordures que le moteur OCR pourrait interpréter comme des caractères. Un petit rayon suffit pour la plupart des scans ; augmentez‑le pour les documents très granuleux.

## Appliquer la pipeline de prétraitement d'image

Toute la configuration est prête — maintenant nous exécutons la pipeline sur l'image originale.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Résultat :** `processed_image` est un bitmap nettoyé, redressé, à fort contraste, prêt pour l'extraction de texte.

## Reconnaître le texte d'une image avec le moteur OCR

Il est temps de réellement lire le texte. Nous initialisons le moteur OCR, lui fournissons notre image polie, et demandons la chaîne brute.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Sortie attendue (exemple) :**  

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Si vous voyez des caractères illisibles, revérifiez l'étape de deskew ou expérimentez avec une valeur de `threshold` différente.

## Construire une pipeline de prétraitement d'image – Script complet

En assemblant tout, voici un script unique et exécutable que vous pouvez placer dans un fichier `.py` et lancer :

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Astuce :** Enveloppez le tout dans une fonction (`def ocr_from_file(path): …`) si vous prévoyez de traiter de nombreux fichiers en lot.

## Questions fréquentes & cas limites

- **Et si l'image est déjà droite ?**  
  La méthode `deskew()` détecte un angle quasi nul et laisse l'image intacte, vous pouvez donc l'exécuter en toute sécurité sur chaque fichier.

- **Mon scan est en couleur—dois‑je le garder ?**  
  La couleur n'apporte aucune valeur pour la plupart des tâches OCR. La binarisation l'élimine, accélérant le traitement et réduisant l'utilisation de mémoire.

- **Puis‑je chaîner plusieurs étapes de prétraitement ?**  
  Absolument. La classe `ImagePreprocessor` est conçue pour les pipelines ; vous pouvez ajouter `sharpen()`, `contrast_enhance()`, ou des filtres personnalisés avant d'appeler `apply()`.

- **La sortie OCR contient des sauts de ligne parasites—comment corriger ?**  
  Post‑traitez la chaîne avec `text.replace("\n", " ").strip()` ou utilisez une bibliothèque d'analyse de mise en page plus avancée comme les modes `--psm` de Tesseract.

## Prochaines étapes

Maintenant que vous savez **comment deskew image** et disposez d'une solide **pipeline de prétraitement d'image**, vous pourriez explorer :

- Intégrer **recognize text from image** dans une API Flask pour des téléchargements de documents en temps réel.
- Utiliser la pipeline pour **remove noise from scan** de documents historiques où la préservation est essentielle.
- Passer à l'échelle pour traiter par lots des milliers de pages et générer un PDF consultable à l'aide de `pdfminer` ou `PyMuPDF`.

N'hésitez pas à expérimenter avec différents seuils, rayons de débruitage, ou même à remplacer le backend OCR par Tesseract si vous avez besoin d'un support multilingue. Les principes restent les mêmes : redressez, nettoyez, puis lisez.

---

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—je serai ravi de vous aider à peaufiner la pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}