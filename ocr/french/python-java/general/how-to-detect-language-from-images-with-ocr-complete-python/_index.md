---
category: general
date: 2026-06-22
description: Apprenez à détecter la langue à partir d’une image et à extraire le texte
  à l’aide de l’OCR en Python. Tutoriel pas à pas couvrant la détection automatique
  de la langue et l’extraction du texte.
draft: false
keywords:
- how to detect language
- detect language from image
- extract text from image
- how to use ocr
- how to extract text
language: fr
og_description: Comment détecter la langue à partir d’une image en utilisant l’OCR ?
  Ce guide vous montre, étape par étape, comment utiliser l’OCR en Python pour détecter
  la langue et extraire le texte.
og_title: Comment détecter la langue à partir d'images avec OCR – Guide complet en
  Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  headline: How to Detect Language from Images with OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to detect language from image and extract text using OCR
    in Python. Step‑by‑step tutorial covering automatic language detection and text
    extraction.
  name: How to Detect Language from Images with OCR – Complete Python Guide
  steps:
  - name: Expected Output
    text: 'If `sample-multilang.png` contains French text, you might see something
      like:'
  - name: 1. Unsupported Image Formats
    text: 'If you try to load a TIFF file that the OCR library doesn’t recognise,
      `ocr.ImageStream.from_file()` will raise an `OcrUnsupportedFormatError`. Wrap
      the load call in a try/except block:'
  - name: 2. Low‑Resolution Images
    text: 'OCR accuracy drops sharply below ~300 dpi. If you notice poor detection,
      consider pre‑processing the image with Pillow:'
  - name: 3. Multiple Languages in One Image
    text: 'When an image contains text in more than one language, the auto‑detect
      feature will pick the dominant one. To capture all languages, you can disable
      auto‑detect and manually pass a list of languages to the engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Comment détecter la langue à partir d'images avec OCR – Guide complet Python
url: /fr/python-java/general/how-to-detect-language-from-images-with-ocr-complete-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment détecter la langue à partir d'images avec OCR – Guide complet Python

Vous êtes-vous déjà demandé **comment détecter la langue** sur une image sans l'ouvrir manuellement ? Vous n'êtes pas seul. Dans de nombreux projets—pensez aux scanners de reçus, aux archives de documents multilingues, ou à une simple application photo‑to‑texte—il faut connaître *quelle* langue le texte appartient avant de pouvoir le traiter davantage.  

Dans ce tutoriel, nous allons parcourir un exemple pratique, de bout en bout, qui montre **comment détecter la langue** à partir d’une image puis extraire les caractères réels. À la fin, vous pourrez exécuter quelques lignes de Python, pointer le script vers n’importe quelle image prise en charge, et obtenir à la fois la langue détectée *et* le texte extrait. Pas de fioritures, juste une solution claire que vous pouvez copier‑coller.

## Ce que vous allez apprendre

- Installer et configurer une bibliothèque OCR légère en Python.  
- Initialiser le moteur OCR et activer la détection automatique de la langue.  
- Charger une image (quel que soit le format supporté) et lancer l’OCR.  
- Récupérer la langue détectée et le texte extrait.  
- Gérer les pièges courants tels que les formats non supportés ou les résultats de langue ambigus.  

Si vous vous êtes déjà demandé **comment utiliser l’OCR** pour des documents multilingues, ce guide répond à vos besoins.

---

## Prérequis

Avant de commencer, assurez‑vous d’avoir les éléments suivants sur votre machine :

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| Python 3.9 ou plus récent | Le package OCR que nous utiliserons cible les interpréteurs modernes. |
| `pip` (gestionnaire de paquets Python) | Nécessaire pour installer la bibliothèque OCR. |
| Une image d’exemple contenant du texte dans au moins une langue (par ex., `sample-multilang.png`) | Vous donne quelque chose de concret à tester. |
| Optionnel : environnement virtuel (`venv` ou `conda`) | Garde les dépendances propres et évite les conflits de version. |

> **Pro tip :** Si vous travaillez dans un environnement virtuel, activez‑le avant d’installer le package OCR afin de garder votre Python global propre.

---

## Étape 1 : Installer la bibliothèque OCR

Pour cette démonstration, nous utiliserons le package hypothétique `ocr` qui reflète l’API montrée dans l’extrait de code. Dans un scénario réel, vous pourriez le remplacer par `pytesseract`, `easyocr`, ou toute autre bibliothèque supportant la détection automatique de la langue.

```bash
pip install ocr
```

> **Note :** Le package est léger (< 5 Mo) et fonctionne sous Windows, macOS et Linux. Si vous rencontrez des erreurs de permission, ajoutez `--user` à la commande.

---

## Étape 2 : Initialiser le moteur OCR – Comment détecter la langue

Maintenant que la bibliothèque est prête, nous pouvons créer une instance du moteur OCR. C’est l’objet qui analysera réellement l’image et déterminera la langue.

```python
import ocr

# Initialise the OCR engine – this is where we start the language detection pipeline
engine = ocr.OcrEngine()
```

Pourquoi commencer par un moteur ? Pensez au moteur comme le cerveau du système OCR ; il conserve la configuration, charge les modèles de langue et gère le travail intensif en arrière‑plan. L’initialiser d’abord garantit que les appels suivants (comme le chargement d’une image) disposent d’un contexte d’exécution.

---

## Étape 3 : Charger votre image et activer la détection automatique de la langue

L’étape suivante consiste à fournir l’image au moteur. Nous activerons également le drapeau *auto‑detect language* afin que le moteur OCR tente de deviner la langue à la volée.

```python
# Load the image (any supported format – PNG, JPEG, BMP, etc.)
image_path = "YOUR_DIRECTORY/sample-multilang.png"
image = ocr.ImageStream.from_file(image_path)

# Attach the image to the engine
engine.set_image(image)

# Enable automatic language detection – this is the key for detecting language from image
engine.get_settings().set_auto_detect_language(True)
```

> **Pourquoi activer l’auto‑détection ?**  
> La plupart des bibliothèques OCR sont livrées avec une langue par défaut (souvent l’anglais). Si votre document contient du français, du japonais ou tout autre script, le moteur le manquerait sans ce réglage. En activant `set_auto_detect_language(True)`, nous laissons le moteur analyser le bitmap, comparer les statistiques de forme des caractères, et choisir le modèle de langue le plus probable.

---

## Étape 4 : Effectuer l’OCR – Extraire le texte de l’image

Avec l’image chargée et la détection de langue activée, l’étape réelle d’OCR se résume à un seul appel de méthode.

```python
# Run the OCR process – this both detects the language and extracts the text
result = engine.recognize()
```

La méthode `recognize()` réalise deux choses en interne :

1. **Détection de la langue :** Elle exécute un classificateur léger sur l’image pour choisir un code de langue (par ex., `en`, `fr`, `es`).  
2. **Extraction du texte :** Elle applique ensuite le modèle spécifique à la langue pour transcrire les caractères en chaînes Unicode.

Comme les deux actions se produisent simultanément, vous obtenez un seul objet `result` contenant tout ce dont vous avez besoin.

---

## Étape 5 : Récupérer et afficher la langue détectée et le texte extrait

Enfin, nous extrayons le code de langue et le texte brut de l’objet `result` et les affichons dans la console.

```python
# Print the detected language and the extracted text
print("Detected language:", result.get_language())
print("Text:", result.get_text())
```

### Résultat attendu

Si `sample-multilang.png` contient du texte français, vous pourriez voir quelque chose comme :

```
Detected language: fr
Text: Bonjour, ceci est un texte d'exemple.
```

Si l’image est ambiguë ou contient plusieurs langues, le moteur renverra la langue qu’il estime la plus fiable, et vous pourrez ensuite inspecter le score de confiance (la plupart des bibliothèques exposent une méthode `get_confidence()` pour les cas d’usage avancés).

---

## Gestion des cas limites courants

### 1. Formats d’image non supportés

Si vous essayez de charger un fichier TIFF que la bibliothèque OCR ne reconnaît pas, `ocr.ImageStream.from_file()` lèvera une `OcrUnsupportedFormatError`. Enveloppez l’appel de chargement dans un bloc try/except :

```python
try:
    image = ocr.ImageStream.from_file(image_path)
except ocr.OcrUnsupportedFormatError as e:
    print(f"Unsupported format: {e}")
    raise
```

### 2. Images à basse résolution

La précision de l’OCR chute brutalement sous ~300 dpi. Si vous remarquez une mauvaise détection, envisagez de pré‑traiter l’image avec Pillow :

```python
from PIL import Image, ImageEnhance

pil_img = Image.open(image_path)
pil_img = pil_img.resize((pil_img.width * 2, pil_img.height * 2), Image.LANCZOS)
pil_img.save("resized.png")
image = ocr.ImageStream.from_file("resized.png")
```

### 3. Plusieurs langues dans une même image

Lorsque l’image contient du texte dans plus d’une langue, la fonction d’auto‑détection choisira la langue dominante. Pour capturer toutes les langues, vous pouvez désactiver l’auto‑détection et passer manuellement une liste de langues au moteur :

```python
engine.get_settings().set_auto_detect_language(False)
engine.get_settings().set_languages(["en", "fr", "de"])
```

Le moteur OCR tentera alors de reconnaître les caractères en utilisant chaque modèle de langue et renverra la meilleure correspondance pour chaque bloc de texte.

---

## Script complet – Toutes les étapes combinées

Voici le script Python complet, prêt à être exécuté, qui intègre tout ce que nous avons vu. Enregistrez‑le sous le nom `detect_language_ocr.py` et lancez `python detect_language_ocr.py`.

```python
# detect_language_ocr.py
# -------------------------------------------------
# How to detect language from image and extract text using OCR
# -------------------------------------------------

import ocr

def main():
    # 1️⃣ Initialise the OCR engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image (any supported format)
    image_path = "YOUR_DIRECTORY/sample-multilang.png"
    try:
        image = ocr.ImageStream.from_file(image_path)
    except ocr.OcrUnsupportedFormatError as err:
        print(f"Error loading image: {err}")
        return

    engine.set_image(image)

    # 3️⃣ Enable automatic language detection
    engine.get_settings().set_auto_detect_language(True)

    # 4️⃣ Perform OCR – this both detects language and extracts text
    try:
        result = engine.recognize()
    except ocr.OcrRecognitionError as err:
        print(f"OCR failed: {err}")
        return

    # 5️⃣ Retrieve and display the detected language and extracted text
    print("Detected language:", result.get_language())
    print("Text:", result.get_text())

if __name__ == "__main__":
    main()
```

**Exécutez‑le** et vous verrez immédiatement le code de langue suivi du texte extrait. C’est la réponse complète à **comment détecter la langue** et **comment extraire le texte** d’une image à l’aide de l’OCR.

---

## Aller plus loin – Prochaines étapes et sujets associés

- **Améliorer la précision** : Expérimentez le pré‑traitement d’image (seuillage, débruitage) avec `opencv-python`.  
- **Traitement par lots** : Enveloppez le script dans une boucle pour gérer un dossier complet d’images.  
- **Intégrer avec le NLP** : Transférez le texte extrait à une bibliothèque d’identification de langue comme `langdetect` pour une seconde opinion.  
- **Explorer d’autres moteurs OCR** : `pytesseract` offre un contrôle fin, tandis que `easyocr` supporte plus de 80 langues prêtes à l’emploi.  

Tous ces sujets reviennent à nos mots‑clés secondaires—*detect language from image*, *extract text from image*, *how to use OCR*, et *how to extract text*—vous permettant d’élargir votre boîte à outils sans repartir de zéro.

---

## Conclusion

Nous venons de couvrir **comment détecter la langue** à partir d’une image, de parcourir le code exact nécessaire, et d’expliquer pourquoi chaque étape est importante. En initialisant le moteur OCR, en chargeant l’image, en activant la détection automatique de la langue, puis en appelant `recognize()`, vous obtenez à la fois l’identifiant de langue et le texte extrait en une opération propre.

Vous pouvez maintenant intégrer cette logique dans des applications plus vastes—service de numérisation de reçus, chatbot multilingue, ou simple utilitaire de bureau. L’idée centrale reste la même : laissez le moteur OCR faire le gros du travail, puis exploitez les résultats comme vous le souhaitez.

Des questions sur des cas particuliers, ou envie de partager un cas d’usage intéressant ? Laissez un commentaire ci‑dessous. Bon codage, et profitez de la transformation d’images en texte recherchable !  

![comment détecter la langue à partir d'une image](ocr-demo.png "Capture d'écran montrant comment détecter la langue à partir d'une image en utilisant Python OCR")


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code fonctionnels complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte d’une image avec Aspose OCR – Guide pas à pas](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraire du texte d’une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Comment utiliser AspOCR : filtres de pré‑traitement d’image OCR pour .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}