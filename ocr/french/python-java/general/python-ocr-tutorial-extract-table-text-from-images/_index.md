---
category: general
date: 2026-01-12
description: Tutoriel OCR Python montrant comment extraire le texte d’un tableau à
  partir d’une image. Apprenez à lire un tableau depuis une image et à extraire le
  texte sélectionné avec Aspose OCR.
draft: false
keywords:
- python ocr tutorial
- extract table text
- read table from image
- extract selected text
- how to extract table
language: fr
og_description: Tutoriel Python OCR qui vous apprend à extraire le texte d'un tableau
  à partir d'une image, lire le tableau depuis l'image et extraire le texte sélectionné
  à l'aide d'Aspose OCR.
og_title: 'Tutoriel OCR Python : Extraire le texte des tableaux à partir d''images'
tags:
- OCR
- Python
- AsposeOCR
title: 'Tutoriel OCR Python : Extraire le texte des tableaux à partir d''images'
url: /fr/python-java/general/python-ocr-tutorial-extract-table-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutoriel OCR Python : Extraire le texte d’un tableau à partir d’images

Vous avez déjà eu besoin d’un **python ocr tutorial** qui montre réellement comment extraire un tableau d’un formulaire numérisé ? Vous n’êtes pas le seul. La plupart des tutoriels s’arrêtent à l’extraction de texte générique, vous laissant deviner comment isoler cette grille de données qui vous intéresse.  

Dans ce guide, nous parcourrons un scénario réel : lire un tableau à partir d’une image, extraire uniquement le texte sélectionné dont vous avez besoin, puis afficher les résultats. En cours de route, nous ajouterons des astuces sur **how to extract table** de façon fiable, afin que vous n'ayez pas à réinventer la roue à chaque fois.

## Ce que vous apprendrez

- Comment configurer Aspose OCR pour Python.
- Comment définir une région rectangulaire contenant un tableau.
- Les étapes exactes pour **extract table text** et **read table from image**.
- Astuces pour gérer plusieurs langues ou des mises en page de tableau irrégulières.
- Un script complet et exécutable que vous pouvez intégrer immédiatement à votre projet.

**Pré-requis**  
- Python 3.8 ou version supérieure.  
- Familiarité de base avec les concepts d’OCR (pas besoin d’expertise approfondie).  
- Une image PNG ou JPEG contenant un tableau clair (nous l’appellerons `form_with_table.png`).  

Si vous avez tout cela, plongeons‑y—pas de blabla, juste du code concret.

![exemple de tutoriel OCR python de la région du tableau](table_region_example.png){alt="exemple de tutoriel OCR python montrant la région du tableau"}

## Étape 1 : Installer et importer Aspose OCR

Première chose à faire : vous avez besoin de la bibliothèque Aspose OCR. Le paquet se trouve sur PyPI, donc une simple commande `pip` suffit.

```bash
pip install aspose-ocr
```

Importez maintenant le module ainsi que les assistants dont vous aurez besoin.

```python
# Step 1: Import the Aspose OCR package
import asposeocr as ocr
```

*Astuce :* Conservez vos dépendances dans un fichier `requirements.txt`. Cela facilite la reproduction de l’environnement.

## Étape 2 : Initialiser le moteur OCR (Noyau du tutoriel OCR Python)

Créer le moteur est le cœur de tout **python ocr tutorial**. Ici, nous définissons également la langue par défaut sur l’anglais—n’hésitez pas à la changer plus tard.

```python
# Step 2: Create an OCR engine and set the default language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

Pourquoi définir la langue ? La précision de l’OCR peut augmenter considérablement lorsque le moteur sait quels caractères attendre. Si vous traitez des formulaires multilingues, vous pouvez soit définir une liste de langues, soit surcharger par région (voir plus loin).

## Étape 3 : Charger votre image

Aspose OCR fonctionne avec la plupart des formats d’image courants. Il suffit de pointer vers le chemin du fichier, et vous obtiendrez un objet `Image` prêt à être traité.

```python
# Step 3: Load the image that contains the form with the table
image_page = ocr.Image.load("YOUR_DIRECTORY/form_with_table.png")
```

*Cas particulier :* Les images volumineuses (plus de 5 Mo) peuvent ralentir le traitement. Envisagez de les redimensionner ou de les compresser avant l’OCR si les performances deviennent un problème.

## Étape 4 : Définir la région du tableau (Read Table from Image)

Voici la partie amusante : indiquer au moteur *où* se trouve le tableau. Vous fournissez un `OcrRegion` avec un `Rectangle` (x, y, largeur, hauteur). Les coordonnées sont basées sur les pixels, vous devrez donc peut‑être expérimenter un peu.

```python
# Step 4: Define the rectangular area where the table is located
# (x, y, width, height) – adjust these values for your image
table_region = ocr.OcrRegion(
    image_page,
    ocr.Rectangle(120, 340, 800, 450)
)

# Optional: override language for this specific region
table_region.language = ocr.Language.ENGLISH
```

Pourquoi utiliser une région ? En limitant l’OCR à la zone du tableau, nous **extract selected text** plus rapidement et évitons le bruit provenant des étiquettes ou graphiques environnants. Cela améliore également la précision car le moteur peut se concentrer sur une mise en page uniforme.

## Étape 5 : Exécuter l’OCR sur la région définie

Une fois la région définie, nous appelons `process_region`. La méthode renvoie un objet `OcrResult` contenant le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

```python
# Step 5: Run OCR only on the defined region
region_result = ocr_engine.process_region(table_region)
```

Si vous devez extraire plusieurs tableaux, répétez simplement les Étapes 4‑5 avec des rectangles différents.

## Étape 6 : Afficher le texte du tableau extrait

Enfin, imprimez—ou stockez—la représentation textuelle du tableau. Aspose OCR renvoie du texte brut avec des sauts de ligne qui correspondent généralement aux lignes, ce qui rend le post‑traitement simple.

```python
# Step 6: Output the extracted table text
print("Table text:\n", region_result.text)
```

**Sortie attendue** (exemple) :

```
Table text:
 Item        Qty   Price
 Apple       10    $1.20
 Banana      5     $0.80
 Orange      8     $1.00
```

Vous pouvez maintenant transmettre cette chaîne aux analyseurs `csv`, aux DataFrames pandas, ou à tout pipeline d’analyse en aval.

## Exemple complet fonctionnel

En rassemblant le tout, voici le script complet que vous pouvez exécuter immédiatement. Remplacez `YOUR_DIRECTORY/form_with_table.png` par le chemin réel de votre image.

```python
# -*- coding: utf-8 -*-
"""
Python OCR Tutorial: Extract Table Text from Images
---------------------------------------------------
A self‑contained example that demonstrates how to read a table from an image
using Aspose OCR for Python.
"""

# Install the library first:
# pip install aspose-ocr

import asposeocr as ocr

def extract_table(image_path, rect):
    """
    Extracts text from a rectangular region that contains a table.

    :param image_path: Path to the PNG/JPEG image.
    :param rect: Tuple (x, y, width, height) defining the table region.
    :return: Plain‑text representation of the table.
    """
    # Initialise OCR engine with English language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Load the image
    img = ocr.Image.load(image_path)

    # Define the region (override language if needed)
    region = ocr.OcrRegion(img, ocr.Rectangle(*rect))
    region.language = ocr.Language.ENGLISH  # optional per‑region override

    # Process only this region
    result = engine.process_region(region)

    return result.text

if __name__ == "__main__":
    # Adjust these coordinates to match your table location
    table_rect = (120, 340, 800, 450)   # x, y, width, height

    # Path to your image file
    img_file = "YOUR_DIRECTORY/form_with_table.png"

    extracted_text = extract_table(img_file, table_rect)
    print("=== Extracted Table Text ===")
    print(extracted_text)
```

Exécutez le script avec `python extract_table.py`. Si tout s’aligne, vous verrez le tableau affiché dans votre console.

## Questions fréquentes & gestion des cas particuliers

**Que faire si le tableau n’est pas parfaitement rectangulaire ?**  
Vous pouvez diviser le tableau en plusieurs régions qui se chevauchent ou utiliser un rectangle plus grand couvrant toute la zone, puis post‑traiter le texte (par ex., en le découpant aux sauts de ligne).

**Puis‑je extraire uniquement des colonnes spécifiques ?**  
Une fois que vous avez le texte complet du tableau, utilisez `csv` ou `pandas` de Python pour extraire les colonnes qui vous intéressent. L’étape OCR elle‑même renvoie tout ce qui se trouve dans le rectangle.

**Comment travailler avec des tableaux non anglais ?**  
Définissez `ocr_engine.language` (ou `region.language`) sur l’énumération appropriée, comme `ocr.Language.FRENCH` ou combinez plusieurs langues avec `ocr.Language.ENGLISH | ocr.Language.SPANISH`.

**Existe‑t‑il un moyen d’obtenir les boîtes englobantes de chaque cellule ?**  
Aspose OCR peut renvoyer `region_result.words` où chaque mot comprend une boîte englobante. Vous devrez mapper ces boîtes sur une grille—utile pour une analyse de mise en page avancée.

## Conseils pour une meilleure précision

- **Nettoyez l’image** : binarisez ou augmentez le contraste avant de la soumettre à l’OCR. Des bibliothèques comme Pillow peuvent aider.
- **Évitez les artefacts de compression** : enregistrez les numérisations au format PNG lorsque c’est possible.
- **Attention au DPI** : 300 dpi est un bon compromis ; des valeurs plus faibles peuvent entraîner des caractères manquants.
- **Testez différentes tailles de rectangle** : des rectangles légèrement plus grands capturent souvent des caractères errants appartenant au tableau.

## Prochaines étapes

Maintenant que vous avez maîtrisé **how to extract table** avec Aspose OCR, vous pourriez explorer :

- Convertir le texte extrait en fichier CSV avec le module `csv` de Python.
- Injecter les données dans un DataFrame **pandas** pour l’analyse.
- Utiliser l’OCR pour lire des formulaires manuscrits (nécessite un moteur différent ou un entraînement supplémentaire).
- Automatiser le traitement par lots de dizaines de formulaires numérisés à l’aide d’une simple boucle `for`.

Chacune de ces extensions s’appuie sur les concepts de base abordés dans ce **python ocr tutorial**, vous plaçant ainsi en bonne position pour passer à l’échelle.

---

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—je serai ravi de vous aider à affiner l’extraction.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}