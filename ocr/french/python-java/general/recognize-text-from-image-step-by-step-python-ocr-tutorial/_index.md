---
category: general
date: 2026-03-26
description: Reconnaître le texte d’une image rapidement en apprenant comment charger
  l’image pour l’OCR et extraire les données d’une région spécifique. Suivez ce guide
  pratique.
draft: false
keywords:
- recognize text from image
- load image for ocr
- OCR region of interest
- extract text from ROI
- Python OCR library
- image preprocessing for OCR
language: fr
og_description: Reconnaître le texte d’une image en Python en chargeant une image
  pour l’OCR, en définissant une zone d’intérêt et en extrayant du texte propre. Découvrez
  le flux de travail complet.
og_title: Reconnaître du texte à partir d'une image – Guide complet d'OCR en Python
tags:
- OCR
- Python
- Image Processing
title: Reconnaître le texte à partir d'une image – Tutoriel OCR Python étape par étape
url: /fr/python-java/general/recognize-text-from-image-step-by-step-python-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image – Guide complet Python OCR

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** sans savoir par où commencer ? Peut‑être que vous avez un formulaire numérisé, un reçu ou une capture d’écran et que vous voulez simplement récupérer les mots contenus dans une zone précise. Bonne nouvelle : avec quelques lignes de Python, vous pouvez charger l’image pour l’OCR, vous concentrer sur une région unique et extraire le texte exact dont vous avez besoin—sans copier manuellement.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : chargement de l’image, définition d’une région d’intérêt (ROI), exécution du moteur OCR et affichage du résultat. À la fin, vous pourrez intégrer ce fragment dans n’importe quel projet qui doit extraire du texte d’une partie spécifique d’une image. Pas de pipelines de traitement d’image lourds, juste du code clair, lisible et fonctionnel dès aujourd’hui.

## Prérequis

- Python 3.8+ installé  
- Le package `ocr` (ou toute bibliothèque OCR compatible) – installez‑le avec `pip install ocr-lib` (remplacez par le nom réel du package que vous utilisez)  
- Une image PNG/JPEG contenant le formulaire que vous souhaitez lire  
- Une connaissance de base des fonctions et classes Python  

Si vous êtes déjà à l’aise avec tout cela, tant mieux — vous pouvez passer à la suite. Sinon, prenez un café rapide et assurez‑vous que les éléments ci‑dessus sont prêts ; les étapes suivantes supposent qu’ils sont en place.

## Étape 1 : Créer une instance du moteur OCR – Noyau « reconnaître du texte à partir d'une image »

La première chose dont nous avons besoin est un objet capable de communiquer avec le moteur OCR. Considérez‑le comme le cerveau qui, plus tard, **reconnaîtra du texte à partir d'une image**.

```python
import ocr  # Import the OCR library

# Initialize the engine
ocr_engine = ocr.OcrEngine()
```

> **Pourquoi c’est important :** Initialiser le moteur une seule fois vous permet de réutiliser les paramètres (comme les packs de langues) sur plusieurs images, ce qui améliore les performances et garde le code propre.

## Étape 2 : Charger l’image pour l’OCR – Mettre l’image en mémoire

Nous allons maintenant **charger l’image pour l’OCR**. La bibliothèque fournit une méthode statique pratique qui lit le fichier et renvoie un objet compréhensible par le moteur.

```python
# Load the source image (replace the path with your own)
image_path = "YOUR_DIRECTORY/form.png"
ocr_engine.set_image(ocr.Imaging.Image.load(image_path))
```

> **Astuce pro :** Si votre image est volumineuse, pensez à la redimensionner avant le chargement. Des images plus petites accélèrent l’OCR sans sacrifier la précision pour la plupart des textes imprimés.

## Étape 3 : Définir la région d’intérêt OCR (ROI)

Souvent, vous n’avez pas besoin de toute la page—seulement d’une boîte précise où l’utilisateur a saisi des données. Définir une **région d’intérêt OCR** indique au moteur d’ignorer le reste, ce qui réduit le bruit et accélère le traitement.

```python
# Define ROI: (left, top, width, height) in pixels
region_of_interest = ocr.Rectangle(120, 340, 560, 90)

# Register the ROI with the engine
ocr_engine.add_region_of_interest(region_of_interest)
```

> **Pourquoi se concentrer sur la ROI ?**  
> - **Vitesse :** Le moteur analyse moins de pixels.  
> - **Précision :** Les graphiques d’arrière‑plan hors de la ROI peuvent perturber la reconnaissance des caractères.  
> - **Simplicité :** Vous obtenez une chaîne propre qui correspond exactement au champ qui vous intéresse.

## Étape 4 : Exécuter le processus OCR – Le moment de vérité

Une fois tout configuré, nous **reconnaissons du texte à partir d'une image** à l’intérieur de la ROI définie.

```python
# Execute OCR on the specified region
ocr_result = ocr_engine.recognize()
```

Si le moteur supporte plusieurs régions, `ocr_result` contiendra une liste ; dans notre cas à ROI unique, c’est un simple objet avec une méthode `get_text()`.

## Étape 5 : Extraire et afficher le texte – Obtenir le résultat final

Nous extrayons maintenant la chaîne brute de l’objet résultat et l’affichons. C’est ici que vous pouvez brancher la sortie vers une base de données, un fichier CSV ou toute autre logique en aval.

```python
# Retrieve the recognized text
extracted_text = ocr_result.get_text()

# Show the result
print("Text inside ROI:\n", extracted_text)
```

**Sortie attendue** (exemple pour un champ de nom rempli) :

```
Text inside ROI:
 John Doe
```

Si le moteur OCR renvoie des espaces ou des sauts de ligne superflus, vous pouvez les nettoyer avec `.strip()` ou une expression régulière.

## Gestion des cas limites courants

| Situation                              | Que faire                                                               |
|----------------------------------------|--------------------------------------------------------------------------|
| **Image basse résolution**            | Agrandir avec `Pillow` (`Image.resize`) avant le chargement.            |
| **Texte incliné ou pivoté**           | Appliquer une correction de rotation (`ocr.Imaging.Image.rotate`).     |
| **Multiples langues**                 | Définir le pack de langues sur le moteur : `ocr_engine.set_language('eng+spa')`. |
| **Aucune ROI définie**                | Omettre `add_region_of_interest` ; le moteur traitera l’image entière. |
| **Caractères inattendus (ex. : virgules)** | Post‑traiter la chaîne : `extracted_text.replace(',', '')`.            |

Ces astuces maintiennent votre pipeline **load image for OCR** robuste même lorsque le matériel source n’est pas parfait.

## Exemple complet fonctionnel – Copier, coller, exécuter

Voici le script complet que vous pouvez placer dans un fichier `.py` et lancer. Il inclut tous les imports, la gestion des erreurs et un petit helper qui vérifie l’existence de l’image.

```python
import os
import ocr

def recognize_text_from_image(image_path: str,
                              roi: tuple = (120, 340, 560, 90)):
    """
    Recognize text from a specific region of an image.

    Parameters
    ----------
    image_path : str
        Full path to the image file.
    roi : tuple
        (left, top, width, height) defining the region of interest.

    Returns
    -------
    str
        The extracted text, stripped of surrounding whitespace.
    """
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")

    # Step 1 – create engine
    engine = ocr.OcrEngine()

    # Step 2 – load image for OCR
    engine.set_image(ocr.Imaging.Image.load(image_path))

    # Step 3 – define ROI
    left, top, width, height = roi
    engine.add_region_of_interest(ocr.Rectangle(left, top, width, height))

    # Step 4 – run OCR
    result = engine.recognize()

    # Step 5 – extract text
    text = result.get_text().strip()
    return text


if __name__ == "__main__":
    # Adjust the path to point at your form image
    img_path = "YOUR_DIRECTORY/form.png"

    try:
        roi_text = recognize_text_from_image(img_path)
        print("Text inside ROI:\n", roi_text)
    except Exception as e:
        print("OCR failed:", e)
```

Exécuter ce script affiche la chaîne nettoyée provenant de la ROI, vous fournissant ainsi une donnée prête à l’emploi.

## Conclusion

Vous disposez maintenant d’une méthode claire, de bout en bout, pour **reconnaître du texte à partir d'une image** en commençant par **load image for OCR**, en définissant une **OCR region of interest** précise, puis en extrayant du texte propre. L’approche fonctionne avec n’importe quelle bibliothèque OCR Python suivant le modèle présenté, et vous pouvez facilement l’étendre pour gérer plusieurs ROI, différentes langues ou des étapes de pré‑traitement.

Ensuite, vous pourriez explorer :

- **prétraitement d’image pour l’OCR** (seuillage, débruitage) afin d’améliorer la précision sur des scans bruyants.  
- Utiliser le résultat **extract text from ROI** pour alimenter un `pandas.DataFrame` et analyser des données en masse.  
- Passer à un service OCR cloud (Google Vision, Azure Computer Vision) lorsque vous avez besoin d’une fiabilité supérieure à grande échelle.

Essayez, ajustez les coordonnées du rectangle selon vos propres formulaires, et laissez l’automatisation prendre le relais. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}