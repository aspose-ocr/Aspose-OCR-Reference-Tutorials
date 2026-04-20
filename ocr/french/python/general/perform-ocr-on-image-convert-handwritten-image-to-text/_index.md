---
category: general
date: 2026-03-18
description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  et extrayez le texte manuscrit d’une photo. Apprenez comment convertir une image
  manuscrite, extraire le texte d’un JPG et reconnaître le texte d’une photo.
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: fr
og_description: Effectuez une OCR sur une image pour extraire le texte manuscrit d’une
  photo. Ce tutoriel montre comment convertir une image manuscrite et reconnaître
  le texte à partir de fichiers JPG.
og_title: Effectuer une reconnaissance optique de caractères sur une image – Guide
  complet du texte manuscrit
tags:
- OCR
- Python
- Handwriting Recognition
title: Effectuer la reconnaissance optique de caractères sur une image – Convertir
  une image manuscrite en texte
url: /fr/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image – Extraction de texte manuscrit Full‑Stack

Vous avez déjà eu besoin d'**effectuer une OCR sur une image** mais vous n'étiez pas sûr que le moteur puisse lire une écriture manuscrite désordonnée ? Vous n'êtes pas seul. Dans de nombreuses applications réelles — pensez aux scanners de reçus de dépenses ou aux utilitaires de prise de notes — vous rencontrerez des photos de gribouillis qui doivent être transformées en texte brut.  

Dans ce guide, nous vous montrerons comment **convertir des images manuscrites**, **extraire du texte d'un jpg**, et même **reconnaître du texte à partir de flux photo** en utilisant une petite bibliothèque de style Python appelée `ocr`. À la fin, vous disposerez d'un script prêt à l'emploi qui extrait chaque mot d'une note manuscrite, quel que soit le tremblement du stylo.

## Ce dont vous avez besoin

- Python 3.8+ (le code fonctionne avec n'importe quel interpréteur récent)
- Le package hypothétique `ocr` – installez-le avec `pip install ocr-lib` (remplacez par le vrai nom du package que vous utilisez)
- Une photographie claire d'une note manuscrite enregistrée sous le nom `note.jpg` (ou tout autre format d'image)
- Une petite dose de curiosité — aucune connaissance avancée en ML n'est requise

C'est tout. Aucun service externe, aucune clé API, juste un moteur local capable d'**effectuer une OCR sur une image**.

![capture d'écran d'effectuer OCR sur une image montrant l'éditeur de code avec le script OCR](example.png)

*Texte alternatif : capture d'écran d'effectuer OCR sur une image montrant l'éditeur de code avec le script OCR.*

## Implémentation étape par étape

Ci-dessous, nous découpons le processus en morceaux faciles à digérer. Chaque en-tête inclut un mot‑clé pour vous permettre de parcourir rapidement, et chaque bloc explique **pourquoi** nous faisons ce que nous faisons — pas seulement **quoi**.

### Étape 1 : Installer et vérifier la bibliothèque OCR

Avant de pouvoir **effectuer une OCR sur une image**, la bibliothèque doit être présente dans votre environnement. Ouvrez un terminal et exécutez :

```bash
pip install ocr-lib
```

> **Astuce :** Si vous travaillez dans un environnement virtuel (fortement recommandé), activez‑le d'abord. Cela garde vos dépendances propres et évite les conflits de version.

Après l'installation, assurons‑nous que Python peut importer le package :

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

Si vous voyez le message de succès, vous êtes prêt à **convertir des images manuscrites**.

### Étape 2 : Créer une instance du moteur et choisir le mode manuscrit

La plupart des moteurs OCR reconnaissent par défaut le texte imprimé. Puisque nous voulons **extraire du texte manuscrit**, nous devons changer le mode explicitement. Cette étape est cruciale car l'écriture manuscrite nécessite souvent un prétraitement différent (comme le lissage des traits).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Pourquoi c'est important :* Les caractères manuscrits peuvent varier énormément en taille et en inclinaison. En définissant `RecognitionMode.HANDWRITTEN`, le moteur applique un modèle entraîné sur des échantillons cursifs, augmentant considérablement la précision.

### Étape 3 : Charger la photo que vous souhaitez analyser

Nous allons maintenant réellement **effectuer une OCR sur une image**. La méthode `load_image` accepte un chemin ou un objet de type fichier. Pour la démonstration, nous chargerons un JPEG, mais le même appel fonctionne pour PNG, BMP ou même des pages PDF.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

Si votre image se trouve dans un bucket cloud, téléchargez‑la d'abord ou passez un flux `BytesIO` — `ocr` est suffisamment flexible pour gérer les deux.

### Étape 4 : Exécuter le processus de reconnaissance

Avec le moteur prêt et l'image en mémoire, nous **effectuons enfin une OCR sur l'image** et récupérons le texte brut.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

L'appel `recognize()` renvoie une chaîne Unicode simple. Pour la plupart des cas d'utilisation, vous pouvez l'écrire directement dans un fichier `.txt`, le transmettre à un pipeline de traitement du langage naturel, ou l'afficher dans une interface graphique.

### Étape 5 : Optionnel – Nettoyer ou post‑traiter la sortie

L'OCR manuscrite n'est pas parfaite ; vous verrez souvent des sauts de ligne parasites ou des caractères mal reconnus. Une étape de nettoyage rapide peut améliorer les résultats en aval.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

N'hésitez pas à brancher des correcteurs orthographiques, des modèles de langue, ou des expressions régulières personnalisées selon votre domaine.

### Script complet – Prêt à copier‑coller

En rassemblant tout, voici le programme complet et exécutable qui **extrait du texte manuscrit** d'un JPEG et affiche un résultat propre.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Sortie attendue** (votre texte réel différera, bien sûr) :

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

Si vous voyez du charabia, revérifiez la qualité de l'image (bonne illumination, flou minimal) et assurez‑vous d'être en mode `HANDWRITTEN`. Ces deux facteurs expliquent la plupart des erreurs de reconnaissance.

## Questions fréquentes (FAQ)

| Question | Réponse |
|----------|--------|
| **Puis-je l'utiliser pour extraire du texte d'un PNG ?** | Absolument. `engine.load_image("scan.png")` fonctionne de la même manière. |
| **Et si mon image est une page PDF ?** | Convertissez d'abord la page en image (par ex., avec `pdf2image`) puis transmettez‑la au moteur. |
| **La bibliothèque est‑elle thread‑safe ?** | Oui, vous pouvez instancier des objets `OcrEngine` séparés par thread. |
| **En quoi cela diffère‑t‑il de `pytesseract` ?** | `ocr` masque le binaire Tesseract et inclut un modèle manuscrit intégré, vous n'avez donc pas besoin d'installer des exécutables externes. |
| **Que faire si je dois **extraire du texte d'un JPG** en masse ?** | Enveloppez le script dans une boucle, ou utilisez `engine.load_image` sur chaque fichier et collectez les résultats dans une liste ou un CSV. |

## Cas limites & meilleures pratiques

1. **Photos à faible contraste** – Augmentez le contraste par programme avant le chargement, ou utilisez `engine.apply_preprocessing('contrast', level=2)`.
2. **Mélange imprimé & manuscrit** – Effectuez deux passes : d'abord avec `HANDWRITTEN`, puis avec `PRINTED`, et fusionnez les sorties.
3. **Images volumineuses** – Redimensionnez à environ 1500 px de largeur ; les moteurs OCR sont généralement plus rapides avec des tampons plus petits sans perdre en précision.
4. **Caractères Unicode** – La bibliothèque renvoie des chaînes UTF‑8, vous pouvez donc gérer les emojis, les lettres accentuées ou les symboles mathématiques immédiatement.

## Conclusion

Nous venons de parcourir un exemple concret de comment **effectuer une OCR sur une image**, en ciblant spécifiquement les notes manuscrites. En installant le package `ocr`, en configurant le moteur en mode `HANDWRITTEN`, en chargeant une photo et en appelant `recognize()`, vous pouvez **convertir des images manuscrites** en texte propre et interrogeable.  

À partir d'ici, vous pourriez **extraire du texte de fichiers jpg** en masse, alimenter la sortie dans une application de prise de notes, ou la combiner avec la synthèse vocale pour l'accessibilité. Le ciel est la limite, et le code ci‑dessus vous fournit une base solide pour expérimenter.

Vous avez une variante à partager — peut‑être un format de fichier différent ou une astuce de prétraitement originale ? Laissez un commentaire, et continuons la discussion. Bon codage, et profitez de transformer ces griffonnages en or numérique !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}