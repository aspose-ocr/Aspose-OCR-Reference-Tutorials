---
category: general
date: 2026-03-26
description: Comment exécuter l'OCR sur un fichier PNG et extraire le texte d'une
  image avec un dictionnaire personnalisé pour améliorer la précision de l'OCR. Apprenez
  à charger rapidement une image pour l'OCR.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: fr
og_description: Comment exécuter l’OCR sur un fichier PNG et extraire le texte d’une
  image avec un dictionnaire personnalisé pour améliorer la précision de l’OCR. Guide
  étape par étape.
og_title: Comment exécuter l'OCR – Extraire du texte d’une image en Python
tags:
- OCR
- Python
- Image Processing
title: Comment exécuter l'OCR – Extraire du texte d’une image en Python
url: /fr/python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter OCR – Extraire du texte d'une image en Python

Vous vous êtes déjà demandé **comment exécuter OCR** sur une facture numérisée ou une capture d'écran et obtenir un texte propre et interrogeable ? Vous n'êtes pas seul. Dans de nombreux projets, le goulot d'étranglement consiste simplement à charger l'image pour OCR puis à inciter le moteur à comprendre les mots spécifiques à un domaine.  

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l’emploi, qui **extrait du texte d'une image** ; il vous montre comment **reconnaître du texte à partir d'actifs PNG**, et même des astuces pour **améliorer la précision d'OCR** avec des dictionnaires personnalisés et des caractères spéciaux. À la fin, vous disposerez d’un script autonome que vous pourrez intégrer à n’importe quel code Python.

## Ce dont vous aurez besoin

- Python 3.8+ (le code utilise des annotations de type mais fonctionne sur les versions 3.x antérieures)
- La bibliothèque `ocr` fournie avec le moteur OCR que vous ciblez (installez‑la via `pip install ocr‑engine` – remplacez par le nom réel du paquet)
- Un fichier image (`input.png`) que vous souhaitez traiter
- Optionnel : un fichier texte brut (`invoice_terms.txt`) contenant des mots spécifiques au domaine, un par ligne

Aucune dépendance externe lourde, aucune clé d’API cloud, uniquement un moteur OCR local.

---

## Étape 1 : Installer et importer la bibliothèque OCR

Tout d'abord, assurez‑vous que le paquet OCR est installé. Si vous utilisez le paquet hypothétique `ocr-engine`, exécutez :

```bash
pip install ocr-engine
```

Importez maintenant les classes dont vous aurez besoin :

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Astuce :** Si vous utilisez un environnement virtuel, activez‑le avant d’installer afin de garder votre Python global propre.

## Étape 2 : Créer une instance du moteur OCR

Créer un objet moteur est le point d’entrée de chaque tâche OCR. Pensez‑y comme à l’allumage du matériel du scanner dans le logiciel.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Pourquoi c’est important : le moteur conserve la configuration comme les packs de langues, les modes de reconnaissance et toutes les ressources personnalisées que vous ajouterez plus tard. Sans lui, vous ne pouvez pas **load image for OCR** ni exécuter le pipeline de reconnaissance.

## Étape 3 : Charger l'image que vous souhaitez reconnaître

Ici nous **chargeons réellement l'image pour OCR**. La méthode `Imaging.Image.load()` lit le fichier et le convertit au format bitmap interne attendu par le moteur.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

Si vous avez un JPEG ou un TIFF, la même méthode fonctionne — il suffit de changer l’extension. Le moteur détecte automatiquement le format.

> **Cas particulier :** Les très grandes images (plus de 5 MP) peuvent provoquer des pics de mémoire. Envisagez de réduire la taille avec Pillow avant le chargement si vous rencontrez des problèmes de performance.

## Étape 4 : Fournir un dictionnaire personnalisé pour améliorer la précision

La plupart des moteurs OCR sont fournis avec des modèles linguistiques génériques. Pour les factures, reçus ou documents juridiques, vous verrez souvent des mots manquants. Fournir une liste de mots personnalisée indique au moteur « ces termes sont valides, traitez‑les comme corrects ».

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Des entrées typiques pourraient être :

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

L’ajout de ceux‑ci améliore le métrique **improve OCR accuracy** de façon spectaculaire—surtout pour les symboles non‑ASCII.

## Étape 5 : Ajouter des caractères spéciaux non couverts par l’ensemble par défaut

Si votre domaine utilise des symboles comme le signe Euro (€) ou le Ø scandinave, vous pouvez les ajouter explicitement :

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

Le moteur traitera désormais ces glyphes comme valides pendant la phase de reconnaissance, réduisant ainsi le risque de sortie « garbage ».

## Étape 6 : Exécuter le processus OCR et récupérer le texte

Enfin, invoquez le reconnaisseur et récupérez le résultat en texte brut. L’appel `recognize()` renvoie un objet riche ; nous n’avons besoin que de la chaîne brute pour la plupart des cas d’utilisation.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Sortie attendue** (truncée pour la brièveté) :

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

Si la sortie semble brouillée, revérifiez que votre dictionnaire personnalisé et vos caractères spéciaux sont correctement chargés.

---

## Vue d’ensemble visuelle

![how to run OCR diagram](ocr-workflow.png){alt="diagramme comment exécuter OCR"}

Le diagramme ci‑dessus illustre le flux depuis le chargement d’une image jusqu’à l’obtention d’un texte propre, en soulignant les points où vous pouvez injecter des dictionnaires personnalisés et des jeux de caractères.

---

## Questions fréquentes & pièges

### Cela fonctionne‑t‑il avec des PDF multi‑pages ?

Oui—convertissez chaque page en PNG (avec `pdf2image` ou similaire) et alimentez‑les séquentiellement à la même instance `ocr_engine`. Le moteur traite chaque image indépendamment, vous obtiendrez donc une liste de chaînes que vous pourrez concaténer.

### Que faire si l’image est tournée ?

La plupart des moteurs OCR modernes détectent automatiquement l’orientation, mais vous pouvez forcer une rotation avec :

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### Comment gérer des langues autres que l’anglais ?

Changez le modèle de langue avant de charger l’image :

```python
ocr_engine.set_language("de")  # German
```

Assurez‑vous que le pack de langue correspondant est installé.

---

## Script complet – Prêt à copier‑coller

Ci‑dessus se trouve le programme complet, prêt à être exécuté après que vous ayez remplacé les chemins factices.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Exécutez‑le avec :

```bash
python run_ocr.py
```

Vous devriez voir le texte extrait affiché dans la console. À partir de là, vous pouvez l’écrire dans un fichier, le transmettre à une base de données, ou le passer à des pipelines NLP en aval.

---

## Récapitulatif & prochaines étapes

Nous avons couvert **comment exécuter OCR** sur un PNG, comment **extraire du texte d’une image**, et montré des méthodes pratiques pour **reconnaître du texte à partir de PNG** tout en **améliorant la précision d’OCR** avec des dictionnaires et des caractères personnalisés.  

Ensuite, envisagez :

- **Traitement par lots :** Parcourir un répertoire d’images.
- **Post‑traitement :** Utiliser des expressions régulières pour extraire les numéros de facture ou les dates.
- **Intégration :** Connecter le script à une API Flask pour des services OCR à la demande.

Si vous êtes curieux de sujets plus avancés, consultez les tutoriels sur **load image for OCR** avec le pré‑traitement OpenCV, ou plongez dans les modèles OCR basés sur le deep‑learning comme Tesseract 4+ avec des couches LSTM.

---

### Continuez à expérimenter !

Essayez de remplacer le `invoice_terms.txt` par une liste de terminologie médicale, ajoutez des caractères grecs, ou alimentez le moteur avec une photo basse résolution pour voir jusqu’où la précision peut s’étendre. Plus vous bidouillez, mieux vous comprendrez les compromis entre le pré‑traitement, les vocabulaires personnalisés et les paramètres du moteur.

Bon codage, et que vos résultats OCR soient toujours nets !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}