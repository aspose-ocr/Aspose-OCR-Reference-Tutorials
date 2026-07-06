---
category: general
date: 2026-03-26
description: Apprenez à réaliser de l’OCR en Python et à extraire facilement du texte
  d’une image, à lire le texte d’un scan ou à extraire le texte d’une facture à l’aide
  d’un simple OcrEngine.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: fr
og_description: Comment effectuer la reconnaissance optique de caractères (OCR) en
  Python ? Ce guide vous montre comment extraire du texte d’une image, lire le texte
  d’un scan et extraire le texte d’une facture en quelques minutes.
og_title: Comment réaliser l'OCR en Python – Extraire rapidement du texte
tags:
- OCR
- Python
- Image Processing
title: Comment effectuer une OCR en Python – Extraire rapidement le texte
url: /fr/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR en Python – Extraire du texte rapidement

Vous vous êtes déjà demandé **comment effectuer de l'OCR** sur un reçu numérisé ou un PDF flou ? Vous n'êtes pas seul. Dans de nombreux projets, le besoin de **extraire du texte d'une image** apparaît tôt ou tard, et l'approche habituelle « taper tout à la main » n'est tout simplement pas évolutive.  

Dans ce tutoriel, vous verrez un exemple complet, prêt à l'exécution, qui montre **comment utiliser l'OCR** pour lire du texte à partir d'une numérisation, extraire des données d'une facture, et même gérer la correction automatique de l'inclinaison — le tout avec seulement quelques lignes de Python.

## Ce que vous allez apprendre

* Les dépendances exactes et les imports requis.
* Comment créer et configurer une instance `OcrEngine`.
* Méthodes pour **extraire du texte d'une image**, **lire du texte à partir d'une numérisation**, et **extraire du texte d'une facture** en utilisant le même moteur.
* Pièges courants (mauvaise langue, fichiers manquants, images volumineuses) et comment les éviter.
* Sortie attendue afin que vous puissiez vérifier que l'OCR a réussi.

Aucun lien vers une documentation externe n'est nécessaire — tout est autonome, vous pouvez copier‑coller le code et voir les résultats immédiatement.

## Prérequis

Avant de plonger, assurez‑vous d'avoir :

* Python 3.8+ installé (le package `ocr` fonctionne avec n'importe quelle version récente).
* La bibliothèque `ocr` disponible (`pip install ocr‑engine` – remplacez par le nom réel du package si différent).
* Un fichier image que vous souhaitez traiter – pour la démonstration nous utiliserons `invoice.png` situé dans un dossier appelé `YOUR_DIRECTORY`.

C’est tout. Si vous avez déjà tout cela, vous êtes prêt à commencer.

## Étape 1 : Installer et importer le module OCR

Première chose à faire : nous avons besoin de la bibliothèque OCR. Si vous ne l'avez pas encore installée, exécutez la commande suivante dans votre terminal :

```bash
pip install ocr-engine
```

Ensuite, importez le module dans votre script.

```python
# Step 1: Import the OCR module
import ocr
```

> **Astuce :** Gardez votre environnement virtuel propre ; cela évite les conflits de version lorsque vous ajoutez plus tard d'autres packages de traitement d'image.

## Étape 2 : Créer et configurer le moteur OCR

Créer le moteur est aussi simple que d'appeler son constructeur, mais la vraie puissance réside dans une configuration correcte. Nous définirons la langue sur English et activerons la correction automatique de l'inclinaison, ce qui est essentiel lorsqu'on traite des factures numérisées qui ne sont pas parfaitement alignées.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Pourquoi activer `auto_skew` ? De nombreux scanners produisent des images légèrement inclinées. Sans correction, le moteur peut manquer des caractères, transformant une facture parfaitement lisible en charabia.

## Étape 3 : Effectuer l'OCR sur votre image cible

Nous injectons maintenant le fichier image dans le moteur. La méthode `recognize_image` renvoie un objet contenant le texte brut ainsi que les scores de confiance (si la bibliothèque les fournit).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Si vous travaillez dans un scénario **read text from scan**, remplacez simplement le chemin par le PDF numérisé converti en PNG ou JPEG. Le même appel fonctionne pour tout format d'image supporté par la bibliothèque sous‑jacent.

## Étape 4 : Inspecter et utiliser le texte extrait

Affichons la sortie brute de l'OCR. Dans un pipeline de traitement de factures réel, vous analyseriez probablement cette chaîne, extrairiez les lignes d'articles, les totaux et les dates, mais pour l'instant un rapide coup d'œil confirmera que l'OCR a réussi.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Sortie attendue (troncature pour la brièveté) :**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Si la sortie semble brouillée, vérifiez que l'image est nette et que `engine.language` correspond à la langue du document.

## Étape 5 : Gérer les cas limites courants

### Images volumineuses

Traiter une numérisation de 5000 × 5000 pixels peut consommer beaucoup de mémoire. Une façon rapide d'atténuer cela est de réduire l'échelle de l'image avant de l'envoyer au moteur :

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Plusieurs langues

Si vous devez **extraire du texte d'une image** contenant à la fois de l'English et de l'Spanish, vous pouvez définir une liste de langues :

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Le moteur tentera de reconnaître les caractères des deux ensembles.

### Gestion des erreurs

Ne supposez jamais que le fichier existe. Enveloppez l'appel dans un bloc try‑except pour afficher un message convivial :

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Référence visuelle

Ci-dessous se trouve une capture d'écran de la facture d'exemple utilisée dans la démonstration. Notez la légère inclinaison — exactement ce que `auto_skew` corrige.

![comment effectuer de l'OCR sur une facture](/images/ocr-example.png)

*Alt text:* comment effectuer de l'OCR sur une image de facture montrant la correction automatique de l'inclinaison.

## Exemple complet et exécutable

En rassemblant tout, voici un script unique que vous pouvez exécuter depuis la ligne de commande. Il couvre l'installation, la configuration, la gestion des erreurs, et une étape de post‑traitement simple qui écrit le texte extrait dans un fichier nommé `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

L'exécution de `python full_ocr_demo.py` affichera le texte extrait dans la console et le stockera dans `output.txt`. À partir de là, vous pouvez appliquer des expressions régulières, des écrivains CSV, ou toute autre logique nécessaire pour l'automatisation de **extract text from invoice**.

## Conclusion

Vous disposez maintenant d'une solution solide, de bout en bout, à **how to perform OCR** en Python. En créant un `OcrEngine`, en configurant la langue et la correction d'inclinaison, et en gérant quelques cas limites pratiques, vous pouvez de manière fiable **extraire du texte d'une image**, **lire du texte à partir d'une numérisation**, et **extraire du texte d'une facture** sans fouiller dans une documentation éparpillée.  
Et ensuite ? Essayez de traiter un lot de fichiers dans une boucle, expérimentez avec différentes langues, ou branchez la sortie dans une bibliothèque de génération de PDF pour créer des PDF recherchables. Le ciel est la limite, et le code que vous venez de voir est une base solide.  

Des questions sur un format de fichier spécifique ou besoin d'aide pour ajuster les seuils de confiance ? Laissez un commentaire ci‑dessous — heureux de vous aider à affiner votre pipeline OCR !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}