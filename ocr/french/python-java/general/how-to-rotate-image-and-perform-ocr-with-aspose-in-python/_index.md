---
category: general
date: 2026-03-26
description: Apprenez à faire pivoter une image et à effectuer la reconnaissance optique
  de caractères (OCR) en Python. Ce guide montre également comment prétraiter l'image
  pour l'OCR et extraire le texte de l'image de manière efficace.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: fr
og_description: Comment faire pivoter correctement une image puis reconnaître le texte
  de l'image à l'aide d'Aspose OCR. Suivez ce tutoriel étape par étape pour prétraiter
  l'image pour l'OCR et extraire le texte de l'image.
og_title: Comment faire pivoter une image et effectuer une OCR – Guide complet Python
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Comment faire pivoter une image et effectuer l’OCR avec Aspose en Python
url: /fr/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire pivoter une image et effectuer une OCR avec Aspose en Python

Vous vous êtes déjà demandé **how to rotate image** afin qu'un moteur OCR puisse réellement lire le texte ? Peut‑être avez‑vous scanné un formulaire qui s'est retrouvé de travers, ou une capture d'appareil photo qui a tourné de 90° dans le sens des aiguilles d'une montre. Dans ce cas le texte semble correct à l'œil humain, mais le moteur OCR voit un désordre. Bonne nouvelle ? C’est un jeu d'enfant de corriger l'orientation, recadrer la région qui vous intéresse, puis extraire le texte — le tout en quelques lignes de Python et des bibliothèques Aspose.

Dans ce tutoriel, nous parcourrons l’ensemble du flux de travail : du chargement d’un TIFF pivoté, à la correction de son orientation, **preprocess image for OCR**, et enfin **recognize text from image**. À la fin, vous saurez **how to perform OCR** sur n’importe quelle image et serez capable d’**extract text from image** avec confiance.

## Ce dont vous avez besoin

- Python 3.8+ (le code fonctionne avec n’importe quelle version récente)
- `asposeocrjava` et `asposeimaging` paquets installés via `pip`
- Une image d’exemple nécessitant une rotation (par ex., `rotated_form.tif`)
- Un peu de curiosité sur le traitement d’image

Aucun framework lourd requis — seulement les deux paquets Aspose et un peu de logique Python.

---

## Étape 1 : Installer les paquets Aspose (How to Perform OCR)

Avant de pouvoir **rotate image** ou **recognize text from image**, nous avons besoin des bibliothèques qui font réellement le travail lourd.

```bash
pip install asposeocrjava asposeimaging
```

> **Astuce :** Si vous êtes derrière un proxy d’entreprise, ajoutez `--proxy http://proxy:port` à la commande. Les paquets sont de simples wrappers Python autour du cœur Aspose .NET/Java, donc l’installation est généralement instantanée.

---

## Étape 2 : Charger le fichier source et le faire pivoter – L’étape centrale “How to Rotate Image”

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Pourquoi pivoter ?** La plupart des moteurs OCR supposent que le texte s’écoule de gauche à droite et de haut en bas. Si le bitmap est de travers, le moteur renverra soit du charabia, soit rien du tout. Faire pivoter aligne la grille de pixels avec l’ordre de lecture attendu, améliorant ainsi considérablement la précision.

> **Cas particulier :** Si vous n’êtes pas sûr que l’image nécessite une rotation de 90°, 180° ou 270°, vous pouvez inspecter `source_image.width` vs `source_image.height` ou utiliser les balises d’orientation `exif`. La méthode `rotate_flip` d’Aspose prend également en charge `ROTATE_180` et `ROTATE_270_CLOCKWISE`.

> **Aperçu de l’image (optionnel) :**  
> ![exemple de rotation d’image](/assets/rotate-demo.png "Comment faire pivoter une image – avant et après rotation")

---

## Étape 3 : Recadrer la région d’intérêt – Preprocess Image for OCR

Souvent, vous n’avez besoin que d’une petite partie de la page — par exemple, un champ de signature ou un bloc de chiffres. Le recadrage élimine le bruit et accélère **how to perform OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Pourquoi recadrer ?** Réduire la taille de l’image limite l’espace de recherche du moteur OCR, ce qui réduit les faux positifs et diminue le temps de traitement. Cela aide également si le fichier source contient des filigranes ou d’autres graphiques pouvant perturber le moteur.

> **Conseil :** Si vous traitez plusieurs champs, répétez l’étape de recadrage avec différents rectangles et exécutez l’OCR sur chaque morceau séparément.

---

## Étape 4 : Initialiser le moteur OCR – Le cœur “How to Perform OCR”

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Dans les coulisses :** Aspose OCR utilise une combinaison de Tesseract et d’une analyse d’image propriétaire. Instancier le moteur une fois et le réutiliser pour plusieurs images est plus efficace que de créer un nouvel objet à chaque fois.

---

## Étape 5 : Fournir l’image recadrée et reconnaître le texte – How to Extract Text from Image

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Expected Output

Si la ROI contient la phrase “Invoice #12345 – Paid”, vous verrez quelque chose comme :

```
Invoice #12345 – Paid
```

Si l’OCR a des difficultés, vous pourriez obtenir des espaces supplémentaires ou des caractères mal lus (par ex., “Invo1ce #I2345 – Pa1d”). C’est là que les astuces **preprocess image for OCR** — comme ajuster le contraste ou appliquer une binarisation — entrent en jeu. Aspose propose des filtres supplémentaires que vous pouvez chaîner avant l’étape 5, mais le flux de base ci‑dessus fonctionne pour la plupart des scans propres.

---

## Étape 6 : Optionnel – Affiner les paramètres OCR (Advanced “How to Perform OCR”)

Si vous avez besoin d’une précision supérieure pour une langue spécifique ou souhaitez ignorer certains caractères, vous pouvez ajuster le moteur :

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Quand l’utiliser :** Utilisez ceci lorsque le document contient de nombreux symboles décoratifs qui ne vous intéressent pas. La mise sur liste noire réduit les détections erronées.

---

## Script complet de bout en bout

En rassemblant tous les éléments, voici un script prêt à l’emploi qui **how to rotate image**, **preprocess image for OCR**, et enfin **recognize text from image** :

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

L’exécution de ce script affiche le texte reconnu dans la console et enregistre une visualisation de la ROI traitée sous le nom `processed_roi.png`. Vous pouvez ouvrir ce PNG pour vérifier que la rotation et le recadrage se sont déroulés comme prévu.

---

## Questions fréquentes & pièges

| Question | Réponse |
|----------|--------|
| **Et si l’image est déjà à l’endroit ?** | L’étape de rotation est idempotente — faire pivoter une image correctement orientée de 90° la déformera évidemment, donc vous devez inspecter `source_image.width` vs `height` ou utiliser les données d’orientation EXIF avant d’appeler `rotate_flip`. |
| **Mon résultat OCR contient des sauts de ligne supplémentaires.** | Utilisez `result.get_text().replace("\n", " ").strip()` pour nettoyer, ou activez `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Puis‑je traiter les PDF directement ?** | Oui — Aspose Imaging peut charger les pages PDF en tant qu’images (`Image.load("file.pdf")`), après quoi vous suivez les mêmes étapes de rotation et d’OCR. |
| **Existe‑t‑il un moyen de traiter en lot de nombreux fichiers ?** | Enveloppez `ocr_rotated_image` dans une boucle sur un répertoire, ou utilisez `concurrent.futures` de Python pour paralléliser. |
| **Comment gérer les langues autres que l’anglais ?** | Définissez la langue de reconnaissance via `ocr_engine.get_recognition_settings().set_recognition_language("fr")` pour le français, etc. |

---

## Conclusion

Nous avons couvert **how to rotate image** correctement, **preprocess image for OCR** en recadrant, et enfin **how to perform OCR** pour **recognize text from image** et **extract text from image** en utilisant les bibliothèques Python d’Aspose. Le script complet montre un flux de travail pratique et prêt pour la production que vous pouvez intégrer à n’importe quel pipeline d’automatisation.

Si vous êtes prêt à aller plus loin, essayez d’expérimenter avec :

- **Amélioration d’image** (contraste, binarisation) avant l’OCR
- **Extraction de plusieurs ROI** pour les formulaires avec plusieurs champs
- **Traitement par lots** de dossiers entiers de documents scannés
- **Intégration** avec des systèmes en aval (par ex., alimenter les données extraites dans une base de données)

N’hésitez pas à adapter le code à votre propre cas d’utilisation, et bon codage ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}