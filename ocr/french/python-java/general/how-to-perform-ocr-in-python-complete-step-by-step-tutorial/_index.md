---
category: general
date: 2026-03-26
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) en
  Python et à reconnaître le texte à partir de fichiers image. Ce guide montre comment
  extraire le texte d’un PNG et convertir rapidement une image en texte.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: fr
og_description: Comment effectuer de l'OCR en Python ? Suivez ce guide pour reconnaître
  le texte d’une image, extraire le texte d’un PNG et convertir une image en texte
  avec une licence d’essai.
og_title: Comment réaliser une OCR en Python – Tutoriel complet
tags:
- OCR
- Python
- Image Processing
title: Comment effectuer la reconnaissance optique de caractères (OCR) en Python –
  Tutoriel complet étape par étape
url: /fr/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR en Python – Tutoriel complet étape par étape  

Vous vous êtes déjà demandé **comment effectuer de l'OCR** sur une photo que vous venez de prendre avec votre téléphone ? Vous n'êtes pas seul·e — les développeurs du monde entier ont besoin d’une méthode fiable pour reconnaître du texte à partir de fichiers image sans se battre avec des bibliothèques natives complexes.  

Dans ce tutoriel, nous allons parcourir un exemple pratique qui montre **comment effectuer de l'OCR**, **reconnaître du texte à partir d’une image**, et **extraire du texte d’un PNG** à l’aide d’un wrapper Python léger. À la fin, vous pourrez **convertir une image en texte** en quelques lignes de code, et vous n’aurez pas à vous soucier des problèmes de licence car nous utiliserons le mode d’essai intégré.

## Ce que vous allez apprendre  

* Comment configurer une licence d’essai pour le moteur OCR (aucun chemin de fichier nécessaire).  
* La séquence exacte d’appels pour **reconnaître du texte à partir d’une image**.  
* Les méthodes pour **extraire du texte d’un PNG** et gérer les pièges courants comme les polices manquantes.  
* Des astuces pour faire évoluer la solution lorsque vous passez d’une licence d’essai à une licence de production.  

**Prérequis** – vous avez besoin de Python 3.8+ et du package `ocr` (installable via `pip install ocr`). Aucun autre outil externe n’est requis.

---  

![how to perform OCR example](https://example.com/ocr-demo.png "how to perform OCR in Python – recognized text displayed")  

*Texte alternatif de l’image : comment effectuer de l'OCR en Python – exemple de sortie*  

## Étape 1 – Activer une licence d’essai (pas de chemin de fichier nécessaire)  

Avant que le moteur puisse lire quoi que ce soit, il a besoin d’une licence valide. Le mode d’essai est parfait pour les expériences et les petits projets.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Pourquoi c’est important :* L’objet licence indique à la bibliothèque OCR que vous opérez dans un bac à sable. Si vous sautez cette étape, le moteur lèvera une `LicenseError` dès que vous appellerez `recognize()`.  

**Astuce :** Lorsque vous passez à une licence payante, remplacez les deux lignes ci‑dessus par `ocr.License("path/to/your/license.key").apply()`.

## Étape 2 – Créer l’instance du moteur OCR  

Maintenant que l’essai est actif, nous instancions le moteur principal. Pensez‑y comme le « cerveau » qui regardera l’image et décidera quels caractères se trouvent où.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Pourquoi c’est important :* Le `OcrEngine` conserve la configuration comme les packs de langues et les réglages DPI. Vous pourrez les ajuster plus tard, mais les valeurs par défaut fonctionnent pour la plupart des PNG uniquement en anglais.

## Étape 3 – Charger le PNG que vous souhaitez traiter  

Voici où nous **reconnaissons du texte à partir d’une image**. La méthode `ocr.Imaging.Image.load()` prend en charge PNG, JPEG, BMP et quelques autres formats.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Cas particulier :* Si votre PNG utilise une palette indexée (courant pour les captures d’écran), le chargeur le convertira automatiquement en un tampon RGB 24 bits. Cette conversion peut entraîner un léger impact de performance, mais elle garantit des résultats OCR précis.

## Étape 4 – Exécuter l’OCR et récupérer le texte  

Enfin, nous demandons au moteur d’effectuer son travail puis nous extrayons le résultat en texte brut.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Sortie attendue** (exemple pour une image simple contenant « Hello World » ):

```
Hello World
```

Si l’image contient plusieurs lignes, la sortie conservera les sauts de ligne, ce qui facilite l’alimentation de processus en aval comme les analyseurs CSV ou les pipelines NLP.

## Optionnel : Affinage pour une meilleure précision  

* **Packs de langues :** `ocr_engine.set_language("eng")` (par défaut) ou `"fra"` pour le français.  
* **Mise à l’échelle DPI :** `ocr_engine.set_dpi(300)` peut améliorer les résultats sur des scans basse résolution.  
* **Pré‑traitement :** Appliquer un seuillage binaire (`ocr.Imaging.Image.threshold()`) avant `set_image` donne souvent un texte plus propre sur des arrière‑plans bruyants.

Ces ajustements sont utiles lorsque vous passez d’une démonstration rapide à un **ocr tutorial python** de niveau production qui traite des centaines de fichiers par jour.

## Script complet – Prêt à copier‑coller  

Voici le script complet, exécutable, qui combine toutes les étapes ci‑dessus. Enregistrez‑le sous le nom `run_ocr.py` et remplacez `YOUR_DIRECTORY/sample1.png` par le chemin vers votre propre PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Exécutez‑le depuis la ligne de commande :

```bash
python run_ocr.py
```

Vous devriez voir le texte extrait affiché dans la console. Si vous obtenez une chaîne vide, vérifiez que l’image contient bien du texte clair, à fort contraste, et que la licence d’essai a été appliquée sans erreur.

## Questions fréquentes & pièges courants  

* **« Cela fonctionne‑t‑il avec JPEG ? »** – Absolument. La méthode `load()` détecte automatiquement le format, vous pouvez donc remplacer le PNG par un JPEG sans modifier le code.  
* **« Et si l’image est tournée ? »** – Le moteur peut détecter automatiquement l’orientation, mais pour de meilleurs résultats vous pouvez pré‑tourner avec `input_image.rotate(90)` avant `set_image`.  
* **« Puis‑je traiter plusieurs images dans une boucle ? »** – Oui. Déplacez simplement les appels de chargement et de `recognize()` à l’intérieur d’une boucle `for` ; la même instance `ocr_engine` peut être réutilisée, ce qui économise un petit peu de surcharge.  

## Prochaines étapes – De la démo à la production  

Maintenant que vous savez **comment effectuer de l'OCR**, envisagez ces sujets complémentaires :

* **Traitement par lots** – Combinez ce script avec `os.listdir()` pour **extraire du texte d’un PNG** en masse.  
* **Intégration avec PDF** – Utilisez `pdf2image` pour convertir les pages PDF en PNG, puis alimentez‑les dans le même pipeline.  
* **Post‑traitement** – Appliquez des expressions régulières ou du fuzzy matching pour nettoyer les erreurs courantes d’OCR (par ex., « 0 » vs « O »).  

Chacune de ces extensions repose sur l’idée centrale de **convertir une image en texte** et augmente l’utilité de votre flux de travail OCR.

---  

### TL;DR  

Nous avons couvert tout ce qu’il faut savoir pour **comment effectuer de l'OCR** en Python : activer une licence d’essai, créer un moteur, charger un PNG, lancer la reconnaissance et afficher le résultat. En quelques lignes seulement, vous pouvez **reconnaître du texte à partir d’une image**, **extraire du texte d’un PNG**, et **convertir une image en texte** pour n’importe quelle application en aval.  

Essayez, ajustez le DPI ou les paramètres de langue, et laissez le moteur faire le gros du travail. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}