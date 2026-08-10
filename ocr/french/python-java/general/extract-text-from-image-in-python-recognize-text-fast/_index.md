---
category: general
date: 2026-07-05
description: Extraire du texte d'une image avec Python OCR. Apprenez à reconnaître
  le texte d'une image, à charger l'image pour l'OCR et à définir la langue de l'OCR
  en quelques lignes seulement.
draft: false
keywords:
- extract text from image
- how to recognize text from image
- load image for ocr
- create ocr engine python
- set ocr language
language: fr
og_description: Extraire du texte d’une image avec Python OCR. Ce guide montre comment
  reconnaître le texte d’une image, charger l’image pour l’OCR, créer un moteur OCR
  à la manière de Python et définir la langue de l’OCR.
og_title: Extraire du texte d’une image en Python – Reconnaître le texte rapidement
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to recognize text
    from image, load image for OCR, and set OCR language in just a few lines.
  headline: Extract Text from Image in Python – Recognize Text Fast
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Extraire du texte d’une image en Python – Reconnaître le texte rapidement
url: /fr/python-java/general/extract-text-from-image-in-python-recognize-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en Python – Reconnaître le texte rapidement

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais vous ne saviez pas quelle bibliothèque choisir ? Si vous vous êtes déjà demandé *comment reconnaître du texte à partir d'une image* sans jongler avec des outils externes, vous êtes au bon endroit. Dans ce tutoriel, nous allons lancer un petit moteur OCR, le pointer vers une image, et extraire le texte — rien de plus, rien de moins.

Nous passerons en revue chaque étape : **create OCR engine python**, **set OCR language**, **load image for OCR**, lancer la reconnaissance de façon asynchrone, et enfin lire le résultat. À la fin, vous disposerez d'un script autonome que vous pourrez intégrer à n'importe quel projet, qu'il s'agisse d'un numériseur de documents ou d'un chatbot qui lit les mèmes.

## Ce dont vous avez besoin

- Python 3.8+ (le code fonctionne également sur 3.10 et versions ultérieures)  
- Le package `ocr` (un léger wrapper autour de Tesseract – installez avec `pip install ocr` ou votre fork préféré)  
- Un fichier image (`.jpg`, `.png`, etc.) contenant du texte lisible  
- Un petit peu de patience pour la partie async (c’est rapide, promis)

C’est tout — aucune dépendance lourde, aucune compilation native. Si vous avez déjà Tesseract installé sur votre système, le wrapper `ocr` le détectera automatiquement.

## Étape 1 : Créer le moteur OCR – le cœur de l'extraction

Première chose à faire : vous avez besoin d'un objet moteur qui sait communiquer avec le moteur OCR sous‑jacent. Considérez‑le comme le « cerveau » qui traitera ensuite l'image.

```python
import ocr

# Step 1: Instantiate the OCR engine
engine = ocr.OcrEngine()
```

*Pourquoi c'est important* : sans moteur, vous n'avez aucun contexte pour les paramètres de langue ou les capacités async. La classe `OcrEngine` abstrait les appels en ligne de commande de bas niveau à Tesseract, vous offrant une API Python propre.

## Étape 2 : Définir la langue OCR – indiquer au moteur ce à quoi s’attendre

Si votre document est en anglais, vous pouvez laisser la valeur par défaut, mais il est recommandé de la définir explicitement. Cela montre également comment **set OCR language** pour d'autres paramètres régionaux.

```python
# Step 2: Explicitly set the language to English
engine.language = ocr.Language.ENGLISH
```

> **Astuce** : Pour les PDF multilingues, vous pouvez passer une liste comme `[ocr.Language.ENGLISH, ocr.Language.FRENCH]`. Le moteur tentera les deux langues automatiquement.

## Étape 3 : Charger l'image pour l'OCR – charger votre image en mémoire

Nous allons maintenant réellement **load image for OCR**. Le wrapper supporte le chargement paresseux, ainsi le fichier n’est lu que lorsque le moteur en a besoin.

```python
# Step 3: Load the image you want to process
image_path = "YOUR_DIRECTORY/large_document.jpg"
image = ocr.Image.load(image_path)
```

*Cas particulier* : Si l'image est très grande (plus de 5 Mo), envisagez de la redimensionner d'abord pour accélérer la reconnaissance. Vous pouvez le faire avec Pillow :

```python
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio, max 2000px
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")
```

## Étape 4 : Lancer la reconnaissance asynchrone – ne bloquez pas votre application

L'exécution de l'OCR peut prendre une seconde ou deux, surtout sur de gros scans. La méthode `recognize_async` renvoie un futur que vous pouvez interroger plus tard, vous permettant de **perform other work while OCR runs in the background**.

```python
# Step 4: Start the recognition asynchronously
future = engine.recognize_async(image)

# While OCR works, we can do something else
print("Processing other tasks while OCR runs...")
# Example placeholder work
for i in range(3):
    print(f"Task {i+1} done.")
```

Pourquoi async ? Dans un serveur web, vous ne voulez pas qu'une seule requête bloque tout le pool de workers. L'objet futur vous donne le contrôle : vous pouvez `await` dans du code async ou bloquer uniquement lorsque vous avez réellement besoin du résultat.

## Étape 5 : Récupérer le résultat – bloquer uniquement si nécessaire

Lorsque vous avez finalement besoin du texte, appelez `future.get()`. Cet appel **blocks only here**, ce qui signifie que le reste de votre programme reste réactif jusqu'à ce que l'OCR se termine.

```python
# Step 5: Get the recognized text (blocks here)
result = future.get()   # blocks only at this point
```

Si vous êtes dans une boucle `asyncio`, vous pouvez plutôt `await future` – le wrapper prend en charge les deux styles.

## Étape 6 : Utiliser le texte reconnu – vos données sont prêtes

Maintenant que vous avez un objet `result`, extraire la chaîne brute est trivial. Imprimons‑le et montrons également comment vous pourriez l'écrire dans un fichier.

```python
# Step 6: Output the OCR result
print("OCR completed:")
print(result.text)

# Optional: save to a .txt file
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Sortie attendue** (troncature pour la brièveté) :

```
OCR completed:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Si l'image ne contient aucun texte, `result.text` sera une chaîne vide — gérez ce cas avec grâce.

## Exemple complet fonctionnel – toutes les étapes dans un seul script

Voici le programme complet, prêt à être exécuté. Copiez‑collez, ajustez le `image_path`, et vous êtes prêt.

```python
import ocr
from PIL import Image as PilImage

# -------------------------------------------------
# 1️⃣ Create OCR engine
engine = ocr.OcrEngine()

# 2️⃣ Set language (English)
engine.language = ocr.Language.ENGLISH

# 3️⃣ Load image (optional resize for large files)
original_path = "YOUR_DIRECTORY/large_document.jpg"
pil_img = PilImage.open(original_path)
pil_img.thumbnail((2000, 2000))          # keep aspect ratio
pil_img.save("resized.jpg")
image = ocr.Image.load("resized.jpg")

# 4️⃣ Start async recognition
future = engine.recognize_async(image)
print("Processing other tasks while OCR runs...")
for i in range(3):
    print(f"Task {i+1} done.")

# 5️⃣ Wait for result
result = future.get()

# 6️⃣ Use the text
print("OCR completed:")
print(result.text)
with open("extracted.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

> **Note** : Remplacez `"YOUR_DIRECTORY/large_document.jpg"` par le chemin réel vers votre image. Le script fonctionne sous Windows, macOS et Linux tant que Tesseract est installé et accessible dans votre `PATH`.

## Pièges courants & comment les éviter

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Caractères indésirables** | Langue incorrecte ou fichiers de données de langue manquants. | Assurez‑vous que `engine.language` correspond à la langue du texte et que le fichier `.traineddata` correspondant existe dans le dossier `tessdata` de Tesseract. |
| **Performance lente sur les grandes images** | L'OCR évolue approximativement avec le nombre de pixels. | Redimensionnez ou sous‑échantillonnez avant de le fournir au moteur (voir l'extrait Pillow). |
| **Le futur ne se résout jamais** | Fichier image corrompu ou illisible. | Enveloppez `future.get()` dans un bloc try/except et validez `image.is_valid()` avant la reconnaissance. |
| **Perte d'Unicode** |  |  |

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convertir une image en texte – Effectuer l'OCR sur une image depuis une URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extraire du texte d'une image – Optimisation OCR avec Aspose OCR pour .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}