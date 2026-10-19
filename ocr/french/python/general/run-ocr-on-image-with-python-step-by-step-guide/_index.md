---
category: general
date: 2026-08-12
description: Exécuter la reconnaissance optique de caractères (OCR) sur une image
  en utilisant Python et Aspose AI pour extraire le texte de l'image et améliorer
  la précision de l'OCR avec un post‑processeur de correction orthographique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: fr
lastmod: 2026-08-12
og_description: Exécutez l’OCR sur une image en Python et extrayez instantanément
  le texte de l’image tout en améliorant la précision de l’OCR grâce au post‑traitement
  IA d’Aspose.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Exécuter l'OCR sur une image avec Python – tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Effectuer l'OCR sur une image avec Python – guide étape par étape
url: /fr/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter l'OCR sur une image avec Python – guide étape par étape

Si vous devez **run OCR on image** des fichiers en Python, ce guide vous accompagne tout au long du flux de travail. Vous apprendrez comment **extract text from image**, appliquer **OCR text correction**, et **improve OCR accuracy** avec seulement quelques lignes de code.

Le traitement de documents numérisés, de reçus ou de captures d’écran produit souvent du texte bruité. En ajoutant un post‑processeur de vérification orthographique, vous pouvez transformer la sortie brute d’OCR en un contenu propre et interrogeable sans passer à un outil séparé. Ce tutoriel couvre tout ce dont vous avez besoin — du chargement de l’image à l’affichage du résultat corrigé.

## Prérequis

* Python 3.9 ou version plus récente installé.
* Accès aux packages Python Aspose.OCR et Aspose.AI (ou leurs équivalents open‑source).
* Une image d’exemple (par ex., `sample.png`) placée dans un répertoire connu.
* Familiarité de base avec les fonctions Python et le code orienté objet.

Vous pouvez installer les bibliothèques requises avec pip :

```bash
pip install aspose-ocr aspose-ai
```

> **Astuce :** Utilisez un environnement virtuel (`python -m venv .venv`) pour isoler les dépendances.

## Étape 1 : Run OCR on image – créer l’instance du moteur

La première étape consiste à créer un objet `OcrEngine`. Cet objet encapsule la configuration du moteur OCR et fournit des méthodes pour la gestion et la reconnaissance d’images.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Créer le moteur une fois et le réutiliser pour plusieurs images réduit le temps de démarrage et garantit des paramètres cohérents tout au long de la session.

## Étape 2 : Charger l’image pour l’OCR

Avant que la reconnaissance puisse s’effectuer, le moteur doit connaître l’image à analyser. La méthode `load_image` accepte un chemin de fichier ou un flux binaire.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Pourquoi c’est important :** Charger correctement l’image est la base d’un OCR précis. Fournir une image haute résolution (300 dpi ou plus) **improves OCR accuracy** car le moteur peut distinguer les caractères plus clairement.

## Étape 3 : Extract text from image – effectuer une reconnaissance de base

Une fois l’image chargée, vous pouvez appeler `recognize()` pour obtenir un objet résultat. Le résultat contient le texte brut, les scores de confiance et, éventuellement, les boîtes englobantes pour chaque mot.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

À ce stade, vous avez réussi à **run OCR on image** et extrait les caractères bruts. Cependant, le texte peut contenir des fautes d’orthographe, surtout pour des numérisations de mauvaise qualité.

## Étape 4 : OCR text correction – ajouter un correcteur orthographique en post‑traitement

Aspose AI fournit un pipeline de post‑traitement flexible. En branchant un correcteur orthographique personnalisé, vous pouvez corriger les erreurs OCR typiques (par ex., « l » vs. « 1 », « O » vs. « 0 »).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Comment fonctionne le correcteur orthographique :** `MySpellChecker` doit implémenter une méthode `process(text: str) -> str`. À l’intérieur, vous pouvez utiliser des bibliothèques comme `pyspellchecker` ou `symspellpy` pour remplacer les séquences de mots improbables par des alternatives validées par le dictionnaire.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Étape 5 : Afficher le texte OCR original et corrigé

Enfin, comparez les sorties brutes et corrigées. Cela vous aide à vérifier que **OCR text correction** a réellement **improved OCR accuracy** pour votre cas d’utilisation.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Résultat attendu

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

La ligne corrigée montre que le correcteur orthographique a remplacé les erreurs de reconnaissance OCR courantes (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## Étape 6 : Improve OCR accuracy – liste de contrôle des meilleures pratiques

Même avec le post‑traitement, vous pouvez augmenter la qualité de base du moteur OCR :

| Élément de la liste de contrôle | Pourquoi cela aide |
|---------------------------------|---------------------|
| **Use high‑resolution images (≥300 dpi)** | Plus de données de pixels réduit l’ambiguïté des caractères. |
| **Convert colored images to grayscale** | Supprime le bruit chromatique qui peut perturber le moteur. |
| **Apply image deskewing** | Redresse le texte incliné, évitant les erreurs de coupure de ligne. |
| **Set language/locale explicitly** | Guide le reconnaisseur vers le jeu de caractères correct. |
| **Enable language model** (if the library supports it) | Fournit des prédictions contextuelles, améliorant davantage **improving OCR accuracy**. |

Vous pouvez implémenter ces étapes de prétraitement avec Pillow ou OpenCV avant de transmettre l’image à `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Script complet exécutable

En réunissant tous les éléments, le script suivant est prêt à être copié‑collé dans un fichier nommé `run_ocr.py` et exécuté.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

L’exécution du script affiche le texte original et corrigé, confirmant que vous avez réussi à **run OCR on image**, **extracted text from image**, et **improved OCR accuracy** grâce à **OCR text correction**.

## Conclusion

Vous savez maintenant comment **run OCR on image** des fichiers en Python, extraire le texte brut et appliquer un correcteur orthographique en post‑traitement pour obtenir des résultats plus propres. En suivant la liste de contrôle pour **improve OCR accuracy**, vous pouvez adapter ce flux de travail aux reçus, factures, cartes d’identité ou tout document numérisé.

### Et après ?

* Explorez **language‑specific dictionaries** pour l’OCR multilingue.
* Intégrez le pipeline à une base de données ou à un index de recherche (par ex., Elasticsearch) pour rendre le texte extrait interrogeable.
* Remplacez le correcteur orthographique simple par un modèle de langage neuronal (par ex., correction basée sur GPT) pour une précision encore plus élevée.

N’hésitez pas à expérimenter différentes techniques de prétraitement d’image, différents post‑processeurs ou moteurs OCR alternatifs. Le schéma de base — **run OCR on image → extract text from image → OCR text correction → improve OCR accuracy** — reste le même, vous offrant une base solide pour tout projet de numérisation de documents.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}