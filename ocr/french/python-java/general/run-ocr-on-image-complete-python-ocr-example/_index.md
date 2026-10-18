---
category: general
date: 2026-03-18
description: Effectuez rapidement de l'OCR sur une image avec Python. Apprenez à reconnaître
  le texte d'un PNG, à charger l'image pour l'OCR et à extraire les mots de l'image
  grâce à un guide pas à pas.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: fr
og_description: Exécutez la reconnaissance OCR sur une image avec Python. Ce tutoriel
  montre comment reconnaître le texte d’un fichier PNG, charger l’image pour l’OCR
  et extraire les mots de l’image avec un exemple complet de code.
og_title: Exécuter l'OCR sur une image – Guide Python
tags:
- OCR
- Python
- Image Processing
title: Exécuter l'OCR sur une image – Exemple complet d'OCR en Python
url: /fr/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter OCR sur une image – Exemple complet d’OCR en Python

Vous avez déjà eu besoin d'**exécuter OCR sur une image** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul ; de nombreux développeurs rencontrent ce blocage lorsqu'ils abordent pour la première fois l'extraction de texte à partir de documents numérisés. Dans ce tutoriel, nous allons parcourir un **exemple d’OCR en Python** qui vous permet d'**extraire du texte depuis des fichiers PNG**, de **charger une image pour l’OCR**, et d'**extraire les mots d’une image** avec leurs scores de confiance—le tout en quelques lignes de code.

Nous couvrirons tout ce dont vous avez besoin : la bibliothèque requise, comment configurer le moteur, pourquoi chaque étape est importante, et à quoi ressemble la sortie. À la fin, vous pourrez insérer ce fragment dans votre propre projet et commencer à extraire du texte de n'importe quelle image instantanément. Pas de blabla, juste une solution pratique et exécutable.

## Ce qu’il vous faut

Avant de commencer, assurez‑vous d’avoir :

- Python 3.8 ou une version plus récente installé  
- Le package `ocrengine` (ou toute bibliothèque qui fournit une classe `OcrEngine`). Vous pouvez l’installer via `pip install ocrengine` – adaptez le nom si vous utilisez une autre bibliothèque OCR comme `pytesseract`.  
- Un fichier image (PNG, JPG, etc.) que vous souhaitez traiter – pour ce guide, nous utiliserons `invoice.png`.  

C’est tout. Pas de dépendances lourdes, pas de services externes, juste du Python pur.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Texte alternatif : exemple d’exécution d’OCR sur une image – facture numérisée en cours de traitement*

## Étape 1 – Installer et importer la bibliothèque OCR

Première chose, installons le moteur OCR dans notre environnement et importons‑le. Si vous utilisez le package hypothétique `ocrengine`, l’import ressemble à ceci :

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Pourquoi c’est important :** Importer la bonne classe vous donne accès aux méthodes que nous appellerons plus tard, comme `setImageFromFile` et `recognize`. Si vous sautez cette étape, Python lèvera une `ModuleNotFoundError`, et vous serez bloqué avant même de charger une image.

## Étape 2 – Créer une instance du moteur OCR

Maintenant que la bibliothèque est prête, nous avons besoin d’un objet moteur qui contiendra la configuration et l’état du processus de reconnaissance.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Astuce :* Certains moteurs OCR vous permettent d’ajuster les modèles de langue ou les paramètres DPI à ce stade. Pour un **exemple d’OCR python** basique, les valeurs par défaut fonctionnent bien, mais si vous traitez des scans à basse résolution, pensez à les modifier ici.

## Étape 3 – Charger l’image à traiter

L’étape logique suivante est de **charger l’image pour l’OCR**. Vous indiquez au moteur le chemin du fichier PNG (ou de tout format supporté) que vous souhaitez analyser.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Que se passe‑t‑il en coulisses ?** Le moteur lit les données de pixels, les convertit dans un format que l’algorithme de reconnaissance peut comprendre, et les stocke en interne. Si le chemin du fichier est incorrect, vous obtiendrez une `FileNotFoundError`, alors vérifiez que l’image existe bien.

## Étape 4 – Exécuter l’algorithme de reconnaissance

Une fois l’image chargée, nous **exécutons enfin l’OCR sur l’image** pour extraire le contenu textuel.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

À ce stade, le moteur parcourt le bitmap, applique le rapprochement de motifs, et renvoie un objet contenant chaque mot détecté, chaque ligne, ainsi que les métriques de confiance.

## Étape 5 – Parcourir les mots reconnus et afficher la confiance

La partie la plus utile de tout flux de travail OCR est de voir **la confiance** pour chaque jeton extrait. Elle indique à quel point le moteur est sûr de chaque mot, vous permettant de filtrer les résultats à faible confiance si nécessaire.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Sortie attendue** (exemple) :

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Vous pouvez maintenant voir exactement **les mots extraits de l’image** et la fiabilité de chaque détection. C’est le cœur de toute pipeline **d’extraction de mots depuis une image**.

## Gestion des cas limites courants

### Et si l’image est en niveaux de gris ?

Certains moteurs OCR fonctionnent mieux avec des images en couleur. Si vous remarquez une faible confiance généralisée, essayez de convertir le PNG en une version noir‑et‑blanc à contraste élevé avant de le transmettre au moteur. Pillow peut aider :

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Gestion de plusieurs langues

Si votre document contient à la fois de l’anglais et de l’espagnol, vous voudrez **reconnaître du texte depuis un PNG** en utilisant un modèle multilingue. La plupart des moteurs vous permettent de définir la liste des langues lors de l’initialisation :

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtrer les mots à faible confiance

Parfois, vous ne voulez que les mots dont la confiance dépasse, par exemple, 90 %. Un filtre rapide ressemble à ceci :

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Script complet, prêt à l’emploi

En rassemblant le tout, voici un script unique que vous pouvez copier‑coller et exécuter immédiatement (remplacez simplement le chemin vers votre PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Exécutez‑le avec :

```bash
python run_ocr_on_image.py
```

Vous devriez voir la liste des mots et les pourcentages de confiance affichés dans la console, exactement comme montré précédemment.

## Questions fréquentes

**Cela fonctionne‑t‑il avec des fichiers JPG ou TIFF ?**  
Absolument. La méthode `setImageFromFile` accepte tout format que la bibliothèque sous‑jacent peut décoder, vous pouvez donc **exécuter OCR sur des fichiers image** de type JPG, TIFF, BMP, etc.

**Puis‑je traiter plusieurs images dans une boucle ?**  
Oui. Enveloppez les étapes de chargement et de reconnaissance dans une boucle `for` sur une liste de chemins de fichiers. N’oubliez pas de ré‑initialiser le moteur si la bibliothèque nécessite une nouvelle instance par image.

**Et si j’ai besoin du texte sous forme d’une chaîne unique plutôt que mot par mot ?**  
La plupart des objets de résultat OCR exposent une méthode `getText()` qui renvoie le document complet. Exemple :

```python
full_text = ocr_result.getText()
print(full_text)
```

## Prochaines étapes et sujets associés

Maintenant que vous savez **exécuter OCR sur une image**, pensez à explorer :

- **Post‑traitement** : utilisez des expressions régulières pour nettoyer les dates, montants ou identifiants extraits des factures.  
- **Traitement par lots** : combinez le script avec `os.listdir()` pour gérer des dossiers entiers de documents numérisés.  
- **Bibliothèques alternatives** : `pytesseract` est une option open‑source populaire ; le flux de travail est similaire—il suffit de remplacer les appels du moteur.  
- **Exportation des résultats** : écrivez les mots extraits et leurs scores de confiance dans un CSV pour des analyses en aval.

Chacune de ces extensions s’appuie directement sur les bases posées ici, vous permettant de transformer les données OCR brutes en informations exploitables.

---

### TL;DR

Nous avons présenté un **exemple d’OCR python** concis qui montre comment **charger une image pour l’OCR**, **exécuter OCR sur une image**, et **extraire des mots depuis une image** tout en rapportant la confiance. Le script complet est prêt à être exécuté, et vous disposez maintenant du savoir‑faire pour l’adapter à tout projet nécessitant de **reconnaître du texte depuis un PNG** (ou d’autres formats). Essayez‑le, ajustez les seuils de confiance, et voyez vos applications devenir conscientes du texte en quelques minutes. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}