---
category: general
date: 2026-06-28
description: Apprenez à reconnaître le texte à partir d’une image et à effectuer une
  OCR sur l’image en utilisant Aspose OCR pour Python. Comprend les étapes pour définir
  la langue OCR et extraire les scores de confiance.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: fr
og_description: Reconnaître le texte d'une image en utilisant Aspose OCR en Python.
  Ce guide montre comment définir la langue OCR, effectuer l'OCR sur une image et
  lire les niveaux de confiance.
og_title: Reconnaître le texte à partir d'une image – Tutoriel complet OCR Python
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Reconnaître le texte d’une image avec Aspose OCR – Guide complet Python
url: /fr/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Reconnaître du texte à partir d'une image avec Aspose OCR – Guide complet Python

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** mais vous n'étiez pas sûr de la bibliothèque qui vous offrirait à la fois rapidité et précision ? Vous n'êtes pas seul. Dans le monde de l'automatisation des documents, pouvoir **effectuer de l'OCR sur une image** est une exigence quotidienne—que vous numérisiez des reçus, scanniez des passeports ou extrayiez des données de panneaux multilingues.

Dans ce tutoriel, nous parcourrons un exemple pratique qui montre exactement comment **reconnaître du texte à partir d'une image** en utilisant Aspose OCR pour Python, et nous aborderons également **comment définir la langue OCR** afin que le moteur sache s'il s'agit de latin, de cyrillique ou de tout autre script. À la fin, vous disposerez d'un script prêt à l'emploi qui affiche le texte complet, la confiance ligne par ligne, et même les boîtes englobantes pour chaque mot.

## Ce dont vous avez besoin

- **Python 3.8+** (le code fonctionne avec n'importe quelle version récente)
- **Aspose.OCR for Python via Java** package – installez‑le avec `pip install aspose-ocr`
- Un fichier image (par ex., `mixed_script.png`) contenant le texte que vous souhaitez extraire
- Un IDE ou éditeur de base—VS Code, PyCharm, ou même un éditeur de texte simple fera l'affaire

Aucune dépendance lourde, aucun binaire natif à compiler. Juste une installation pip et vous êtes prêt.

## Étape 1 : Installer et importer le moteur OCR

Tout d'abord, installons la bibliothèque sur votre machine et importons les classes dont vous aurez besoin.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **Astuce :** Si vous êtes derrière un proxy d'entreprise, ajoutez le drapeau `--proxy` à la commande pip. Cela vous évite bien des maux de tête plus tard.

## Étape 2 : Créer le moteur et **comment définir la langue OCR**

Créer une instance `OcrEngine` est aussi simple que d'appeler son constructeur, mais la vraie puissance apparaît lorsque vous indiquez au moteur la langue attendue. C'est la partie qui répond à la question « **comment définir la langue OCR** ».

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

Pourquoi est‑ce important ? Les algorithmes d'OCR utilisent des modèles de caractères spécifiques à chaque langue ; définir la bonne langue augmente considérablement la précision, surtout pour les scripts avec des glyphes similaires (pensez à « 0 » vs « O » en latin versus « О » en cyrillique).

## Étape 3 : **effectuer de l'OCR sur une image** – Reconnaître le texte

Nous transmettons maintenant au moteur le chemin de l'image et le laissons faire sa magie. La méthode renvoie un objet `RecognitionResult` qui contient tout ce dont vous pourriez avoir besoin.

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

Si le fichier n'est pas trouvé, Aspose lèvera une `FileNotFoundError`. Enveloppez l'appel dans un bloc `try/except` pour le code de production—rien de pire qu'une exception non gérée qui fait planter votre service.

## Étape 4 : Afficher le texte complet reconnu

La demande la plus courante est simplement « donnez‑moi le texte ». La méthode `getText()` concatène toutes les lignes détectées en une seule chaîne.

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

Vous verrez quelque chose comme :

```
Full text: Hello World!
This is a sample mixed‑script image.
```

C’est le cœur de **reconnaître du texte à partir d'une image**—une ligne de code qui renvoie tout ce que le moteur a pu déchiffrer.

## Étape 5 : (Optionnel) Afficher la confiance pour chaque ligne détectée

Les scores de confiance vous permettent d'évaluer la fiabilité. Les lignes avec un score inférieur, par exemple, à 0,70 peuvent nécessiter une révision humaine.

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

Sortie typique :

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## Étape 6 : (Optionnel) Récupérer les boîtes englobantes pour chaque mot – Idéal pour la mise en évidence UI

Si vous créez un visualiseur qui permet aux utilisateurs de cliquer sur un mot pour voir ses données OCR, les coordonnées des boîtes englobantes sont précieuses.

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

Exemple de sortie :

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

Ces coordonnées sont en pixels par rapport à l'image originale, vous pouvez donc les superposer directement sur un canevas.

## Script complet fonctionnel

En rassemblant le tout, voici un script prêt à l'exécution que vous pouvez intégrer à n'importe quel projet. Remplacez simplement `YOUR_DIRECTORY/mixed_script.png` par le chemin réel de votre image.

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

Exécutez‑le avec :

```bash
python ocr_demo.py
```

Vous devriez voir le texte complet extrait, les scores de confiance et les boîtes englobantes affichés dans la console.

## Questions fréquentes & cas limites

### Et si mon image contient plusieurs langues ?

Aspose OCR prend en charge la détection multilingue, mais vous devez fournir un **drapeau de langue combiné**. Par exemple, pour gérer à la fois le latin et le cyrillique :

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

L'opérateur pipe (`|`) fusionne les énumérations. Cela répond à l'exigence « **effectuer de l'OCR sur une image** » pour les scénarios multilingues.

### Comment améliorer la précision sur des images basse résolution ?

- **Pré‑traiter** l'image : augmenter le contraste, appliquer une binarisation, ou agrandir avec une bibliothèque comme Pillow.
- **Définir le DPI correct** si vous le connaissez ; Aspose respecte les métadonnées de l'image.
- **Choisir la bonne langue**—plus vous êtes précis, meilleure sera la performance du modèle.

### Puis‑je extraire uniquement certaines régions de l'image ?

Oui. Utilisez la méthode `recognizeRegion` (non montrée dans l'exemple de base) et passez un objet rectangle définissant la zone d'intérêt. Cela est pratique lorsque vous avez besoin uniquement d'un tableau ou d'un bloc de texte spécifique.

## Conclusion

Nous venons de parcourir un exemple complet, de bout en bout, de comment **reconnaître du texte à partir d'une image** avec Aspose OCR pour Python. Vous savez maintenant comment **effectuer de l'OCR sur une image**, définir correctement la **langue OCR**, et récupérer à la fois les scores de confiance et les boîtes englobantes au niveau des mots pour les travaux UI en aval.

À partir de là, vous pourriez :

- Expérimenter d'autres langues (`Language.Arabic`, `Language.Japanese`, etc.)
- Intégrer le script dans un service web (Flask/Django) pour fournir l'OCR en tant qu'API
- Combiner les données de boîtes englobantes avec un canvas front‑end pour permettre aux utilisateurs de mettre en évidence le texte

Les possibilités sont aussi vastes que les documents que vous devez numériser. Vous avez une image difficile qui refuse de coopérer ? Laissez un commentaire, et nous résoudrons le problème ensemble. Bon codage !

![exemple de reconnaissance de texte à partir d'une image](/images/ocr_example.png "reconnaissance de texte à partir d'une image – sortie Aspose OCR")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte à partir d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Reconnaître du texte d'image avec Aspose OCR pour plusieurs langues](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Comment définir la valeur de seuil dans la reconnaissance d'image OCR](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}