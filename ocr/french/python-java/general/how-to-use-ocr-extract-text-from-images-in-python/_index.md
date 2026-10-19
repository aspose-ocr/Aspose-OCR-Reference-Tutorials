---
category: general
date: 2026-03-18
description: Comment utiliser l’OCR pour extraire du texte à partir d’images – un
  guide rapide pour reconnaître le texte des fichiers PNG et charger les images pour
  l’OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: fr
og_description: Comment utiliser l’OCR pour extraire du texte à partir d’images –
  apprenez à reconnaître le texte d’un PNG, charger l’image pour l’OCR et extraire
  le texte avec un script Python simple.
og_title: 'Comment utiliser l’OCR : extraire du texte à partir d’images en Python'
tags:
- OCR
- Python
- Image Processing
title: 'Comment utiliser l’OCR : extraire du texte d’images en Python'
url: /fr/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR : extraire du texte d'images en Python

Vous vous êtes déjà demandé **comment utiliser l'OCR** lorsque vous avez une capture d'écran désordonnée ou un reçu numérisé ? Vous n'êtes pas seul—les développeurs doivent constamment extraire du texte lisible à partir d'images, en particulier des PNG provenant d'applications mobiles ou de téléchargements Web. Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre comment **extraire du texte d'une image**, **reconnaître du texte à partir d'un PNG**, et même **charger une image pour l'OCR** en quelques lignes de Python.

Nous couvrirons tout, de l'installation de la bonne bibliothèque à la gestion de documents multilingues, de sorte qu'à la fin vous saurez exactement *comment extraire du texte* de n'importe quelle image que vous soumettez au moteur. Pas de références vagues, juste une solution claire, étape par étape, que vous pouvez copier‑coller et exécuter.

## Ce que vous allez apprendre

1. Configurer un moteur OCR léger (sans dépendances lourdes requises).  
2. Charger un fichier image—spécifiquement un PNG—dans le moteur.  
3. Activer la détection automatique de la langue afin que le moteur puisse gérer du contenu multilingue.  
4. Exécuter le processus de reconnaissance et récupérer le résultat en texte brut.  
5. Ajuster le flux de travail pour les cas limites comme les fichiers manquants ou les formats non pris en charge.

Si vous êtes à l'aise avec le Python de base, vous êtes prêt. Aucune expérience préalable en OCR n'est nécessaire, bien qu'un rapide coup d'œil à la documentation de la bibliothèque ne fasse jamais de mal.

---

![Comment utiliser l'OCR sur une image PNG](placeholder.png "Comment utiliser l'OCR sur une image PNG – guide étape par étape")

## Comment utiliser l'OCR – charger l'image et reconnaître le texte {#how-to-use-ocr}

### Étape 1 : installer la bibliothèque OCR

Tout d'abord, vous avez besoin d'un package Python qui fournit une classe `OcrEngine`. Pour les besoins de ce tutoriel, nous utiliserons le package fictif mais illustratif **SimpleOCR**, que vous pouvez installer via pip :

```bash
pip install simple-ocr
```

> **Astuce :** Si vous travaillez dans un environnement virtuel (fortement recommandé), activez‑le avant d'exécuter la commande d'installation. Cela maintient vos dépendances de projet propres.

### Étape 2 : importer le moteur et créer une instance

Créer le moteur est aussi simple que d'appeler son constructeur. Considérez le moteur comme le « cerveau » qui traitera plus tard l'image que vous lui fournissez.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Pourquoi créons‑nous une nouvelle instance à chaque fois ? Isolation. Un moteur neuf garantit qu'aucun état résiduel d'une exécution précédente ne contamine la reconnaissance actuelle, ce qui est crucial lorsque vous traitez de nombreux fichiers en lot.

### Étape 3 : charger l'image que vous souhaitez traiter

Nous allons maintenant réellement **charger l'image pour l'OCR**. La méthode `setImageFromFile` accepte un chemin vers n'importe quelle image raster ; nous la pointerons vers un PNG nommé `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Si le fichier n'est pas trouvé, `SimpleOCR` lève une claire `FileNotFoundError`. Vous pouvez la capturer pour fournir un message d'erreur convivial :

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Étape 4 : activer la détection automatique de la langue

La plupart des moteurs OCR modernes sont fournis avec des packs de langues. En passant `"multilingual"` nous indiquons au moteur de détecter le texte et de choisir automatiquement le bon modèle linguistique. C'est particulièrement pratique lorsque votre PNG contient un mélange d'anglais et d'espagnol, par exemple.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Si vous connaissez la langue à l'avance, vous pouvez remplacer `"multilingual"` par une locale spécifique comme `"eng"` ou `"spa"` pour accélérer le traitement.

### Étape 5 : exécuter le processus de reconnaissance

Le travail intensif se fait ici. `recognize()` analyse l'image, applique la segmentation, exécute le réseau neuronal et construit un tampon de texte en interne.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

En coulisses, le moteur effectue :

- **Pré‑traitement** (redressement, binarisation)  
- **Analyse de mise en page** (détection des colonnes, tableaux)  
- **Classification des caractères** (à l'aide d'un modèle d'apprentissage profond)

Tout cela est abstrait, c'est pourquoi vous n'avez besoin que d'une seule ligne.

### Étape 6 : récupérer et afficher le texte reconnu

Enfin, nous récupérons l'objet résultat et extrayons la chaîne brute. C'est la partie où vous **extrayez réellement du texte d'une image**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Sortie attendue** (troncature pour la brièveté) :

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Si l'image ne contient aucun caractère reconnaissable, `text` sera une chaîne vide. Vous pouvez vous en prémunir :

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Extraire du texte d'une image – gérer les cas limites courants

### Plusieurs langues dans un même fichier

Lorsque un document mélange des langues, le paramètre `"multilingual"` fonctionne généralement correctement. Cependant, si vous remarquez des erreurs de reconnaissance, vous pouvez spécifier manuellement une liste de secours :

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Formats non PNG

Même si notre objectif est **reconnaître du texte à partir d'un PNG**, `SimpleOCR` accepte également JPEG, BMP et TIFF. Il suffit de changer l'extension du fichier dans `setImageFromFile`. Pour les piles TIFF, vous devrez peut‑être sélectionner une page spécifique :

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Fichiers volumineux et utilisation de la mémoire

Si vous traitez des scans gigapixels, envisagez de redimensionner avant l'OCR :

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Le redimensionnement réduit la pression sur la mémoire tout en conservant suffisamment de détails pour une reconnaissance précise.

### Déboguer les chargements échoués

Parfois, une image semble correcte à l'œil mais est corrompue en interne. Activez la journalisation détaillée pour voir ce que le moteur détecte :

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Script complet, prêt à l'exécution

Ci-dessous se trouve le programme complet qui assemble toutes les pièces. Copiez‑le dans un fichier nommé `ocr_demo.py`, ajustez le placeholder `YOUR_DIRECTORY`, et exécutez `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

L'exécution de ce script devrait afficher la version texte brut de tout ce qui se trouve dans `mixed_doc.png`. N'hésitez pas à remplacer le fichier par n'importe quelle autre image—**comment extraire du texte** fonctionne de la même manière.

---

## Conclusion

Nous venons de parcourir **comment utiliser l'OCR** en Python pour **extraire du texte d'images** ; en nous concentrant spécifiquement sur **reconnaître du texte à partir d'un PNG** et les étapes pratiques pour **charger une image pour l'OCR**. Le fragment ci‑dessus est une solution autonome : installer le package, lui fournir un fichier, activer la détection multilingue, exécuter le moteur et récupérer le résultat.

À partir d'ici, vous pourriez :

- Intégrer le script dans un service web qui accepte les téléchargements d'utilisateurs.  
- Traiter par lots un dossier de PDF convertis en PNG.  
- Ajouter un post‑traitement (par ex., nettoyage par expressions régulières, vérification orthographique) pour améliorer la précision.

Rappelez‑vous, la qualité de l'OCR dépend de la clarté de l'image, des packs de langues appropriés, et parfois d'un peu de pré‑traitement—alors expérimentez

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}