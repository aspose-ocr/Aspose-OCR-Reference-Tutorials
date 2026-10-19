---
category: general
date: 2026-06-25
description: Extraire du texte d’une image avec OCR Python. Apprenez comment charger
  une image pour l’OCR, effectuer l’OCR en Python et convertir le reçu en JSON en
  quelques étapes simples.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: fr
og_description: Extraire du texte d’une image à l’aide de l’OCR Python. Ce tutoriel
  vous guide à travers le chargement d’une image pour l’OCR, l’exécution de l’OCR
  en Python et la conversion d’un reçu en JSON.
og_title: Extraire du texte d'une image en Python – Guide complet d'OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Extraire du texte d'une image en Python – Guide complet d'OCR
url: /fr/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en Python – Guide complet d'OCR

Vous avez déjà eu besoin d'**extraire du texte d'une image** sans savoir par où commencer ? Dans ce tutoriel, nous vous guiderons à travers **le chargement d'une image pour l'OCR**, **l'exécution de l'OCR en Python**, et **la conversion d'un reçu en JSON** — le tout avec seulement quelques lignes de code.

Si vous avez déjà créé une application de numérisation de reçus, un suivi de dépenses, ou si vous souhaitez simplement automatiser la saisie de données, vous verrez pourquoi maîtriser ce flux est un véritable atout. À la fin, vous disposerez d'un script fonctionnel qui lit une photo de reçu et génère un payload JSON propre, prêt pour les services en aval.

## Ce que vous allez apprendre

Nous couvrirons chaque étape, de l'installation de la bibliothèque `aocr` à la gestion du résultat brut. Plus précisément, vous apprendrez à :

1. **Créer une instance du moteur OCR** – le point d'entrée pour tout le travail de reconnaissance.  
2. **Charger une image pour l'OCR** – indiquer au moteur quel fichier lire.  
3. **Choisir le format d'exportation** – JSON ou XML, nous opterons pour JSON car il est plus facile à consommer.  
4. **Lancer la reconnaissance** – exécuter réellement l'OCR en Python.  
5. **Afficher ou stocker le résultat** – convertir le reçu en JSON et voir la sortie.

Aucune expérience préalable avec l'OCR n'est requise ; il vous suffit d'une configuration Python de base et d'un fichier image (un reçu, un flyer, ce dont vous avez besoin).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="extraction de texte d'une image avec OCR Python"}

## Extraire du texte d'une image – OCR Python étape par étape

Voici le script complet, prêt à être exécuté. Copiez‑collez‑le simplement dans un fichier nommé `receipt_ocr.py` et lancez `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Pourquoi cela fonctionne

- **Instance du moteur** – `aocr.OcrEngine()` encapsule tout le travail lourd (chargement du modèle, prétraitement, etc.).  
- **Chargement de l'image** – `engine.load_image()` indique à la bibliothèque exactement quel bitmap analyser ; vous pouvez fournir JPEG, PNG ou même des PDF multi‑pages.  
- **Format d'exportation** – définir `engine.export_format` sur `aocr.ExportFormat.JSON` rend le résultat sous forme de chaîne structurée, parfait pour les API qui attendent du JSON.  
- **Appel de reconnaissance** – `engine.recognize()` exécute l'inférence du réseau neuronal en arrière‑plan ; il renvoie une chaîne JSON contenant les blocs de texte détectés, les scores de confiance et les informations de mise en page.  

---

## Charger une image pour l'OCR avec aocr

Si vous vous demandez si l'image nécessite un prétraitement spécial, la réponse courte est **non** — `aocr` gère la plupart des cas courants (ajustement du contraste, redressement) automatiquement. Cependant, vous pouvez améliorer la précision en :

- Vous assurant que l'image a au moins 300 dpi.  
- Découpant les bordures inutiles.  
- Convertissant en niveaux de gris avant de la fournir (optionnel, `engine.load_image()` le fera pour vous).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Astuce :* Si le reçu contient beaucoup de bruit, l'étape supplémentaire ci‑dessus peut augmenter la **précision de l'OCR en Python** de façon notable.

---

## Choisir le format d'exportation et convertir le reçu en JSON

Vous vous demandez peut‑être « Pourquoi pas simplement du texte brut ? » Parce que le JSON préserve la structure hiérarchique (lignes, mots, boîtes englobantes). Cela facilite grandement le mappage de champs comme *montant total* ou *date* plus tard.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Lorsque vous exécuterez le script, `json_result` ressemblera à ceci (troncé pour la concision) :

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Vous avez maintenant un payload **convert receipt to JSON** que vous pouvez injecter directement dans une base de données, un endpoint REST ou un modèle d'apprentissage automatique.

---

## Exécuter la reconnaissance et récupérer les résultats

L'étape finale — exécuter réellement l'OCR — est aussi simple que d'appeler `recognize()`. En coulisses, la bibliothèque :

1. Envoie l'image à travers un réseau de neurones convolutionnel pré‑entraîné.  
2. Décodage la sortie du réseau en caractères lisibles.  
3. Emballe le tout dans le format sélectionné (JSON dans notre cas).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Si vous devez stocker la sortie au lieu de l'afficher, écrivez‑la simplement dans un fichier :

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Cas particulier :* Certains reçus contiennent des caractères non ASCII (par ex., « € »). Assurez‑vous d'ouvrir le fichier avec l'encodage UTF‑8, comme indiqué ci‑dessus, pour éviter les textes corrompus.

---

## Exemple complet fonctionnel (toutes les étapes dans un seul script)

En rassemblant tout, voici le script final que vous pouvez exécuter de bout en bout :

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Exécutez‑le avec :

```bash
python receipt_ocr.py
```

Vous devriez voir une ligne de confirmation et, dans le même répertoire, un fichier `receipt_output.json` contenant les données structurées.

---

## Conclusion

Vous savez maintenant **comment extraire du texte d'une image** avec Python, **comment charger une image pour l'OCR**, **comment exécuter l'OCR en Python**, et **comment convertir un reçu en JSON** pour une consommation en aval. Ce flux de bout en bout est léger, ne nécessite que le paquet `aocr`, et peut être intégré à n'importe quel pipeline d'automatisation.

Et après ? Essayez de changer le format d'exportation en XML, expérimentez différentes techniques de prétraitement d'image, ou créez une petite API Flask qui accepte un reçu téléchargé et renvoie instantanément le payload JSON. Le ciel est la limite une fois les bases maîtrisées.

Des questions ou un problème ? Laissez un commentaire ci‑dessous, et bon codage !


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}