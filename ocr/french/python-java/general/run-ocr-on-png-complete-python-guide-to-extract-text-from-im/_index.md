---
category: general
date: 2026-01-12
description: Exécutez la reconnaissance optique de caractères (OCR) sur des fichiers
  PNG rapidement avec Python. Apprenez comment extraire le texte d’une image et d’une
  facture, et charger l’image pour l’OCR en utilisant Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: fr
og_description: Exécutez l’OCR sur un PNG instantanément. Ce guide montre comment
  extraire le texte d’une image et d’une facture, charger l’image pour l’OCR, et enregistrer
  les résultats au format JSON et CSV.
og_title: Exécuter OCR sur PNG – Tutoriel complet Python
tags:
- OCR
- Python
- Image Processing
title: Exécuter l’OCR sur PNG – Guide complet Python pour extraire le texte des images
url: /fr/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter l'OCR sur PNG – Guide complet Python pour extraire du texte d'images

Vous avez déjà eu besoin de **exécuter l'OCR sur PNG** mais vous n'étiez pas sûr de la bibliothèque qui vous fournirait des résultats propres et structurés ? Vous n'êtes pas seul. Dans de nombreux projets réels—pensez à l'automatisation des factures ou à la numérisation de reçus—la première étape consiste à **extraire du texte d'image**, et le PNG est un format courant car il conserve une qualité sans perte.

Dans ce tutoriel, nous allons parcourir un exemple pratique en utilisant le package Aspose.OCR pour Python. À la fin du guide, vous saurez comment **charger une image pour l'OCR**, extraire chaque ligne de texte, transformer ces données en un objet JSON bien structuré, et même les exporter en CSV pour un traitement en aval. Pas de blabla, juste une solution prête à l'emploi.

## Ce que vous allez apprendre

- Comment installer et importer la bibliothèque Aspose.OCR.  
- Les étapes exactes pour **exécuter l'OCR sur PNG** et gérer l'objet résultat.  
- Des méthodes pour **extraire du texte de facture** et formater la sortie en JSON ou CSV.  
- Des astuces pour traiter les images à faible contraste, les documents multilingues et les scores de confiance.  
- Un exemple complet, copiable‑collable, que vous pouvez exécuter dès aujourd'hui.

> **Prérequis :** Python 3.8+ et une connaissance de base de pip. Si vous n’avez jamais utilisé Aspose auparavant, ne vous inquiétez pas — ce guide couvre tout ce dont vous avez besoin pour démarrer.

---

## Étape 1 – Installer Aspose.OCR et préparer votre environnement

Avant de pouvoir **exécuter l'OCR sur PNG**, la bibliothèque doit être présente sur votre système.

```bash
pip install aspose-ocr
```

> **Astuce :** Utilisez un environnement virtuel (`python -m venv venv`) pour isoler les dépendances. Cela évite les conflits de version si vous jonglez avec plusieurs projets.

Une fois installé, importez les modules dont nous aurons besoin :

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Ici nous chargeons `asposeocr` pour le traitement lourd et la bibliothèque intégrée `json` pour la sérialisation ultérieure.

---

## Étape 2 – Créer le moteur OCR et définir la langue

Le moteur OCR est le composant central qui lit réellement les pixels. Pour la plupart des factures en anglais, vous utiliserez le pack de langue anglais :

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Pourquoi c’est important :** Spécifier la langue restreint l’ensemble de caractères, ce qui augmente la précision et accélère le traitement. Si vous devez gérer des factures multilingues, remplacez simplement `ocr.Language.ENGLISH` par l’énumération appropriée.

---

## Étape 3 – Charger l'image pour l'OCR

Nous allons maintenant **charger l'image pour l'OCR**. La méthode `Image.load` accepte un chemin de fichier et fonctionne avec PNG, JPEG, BMP, et plus encore.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Cas particulier :** Si le PNG est exceptionnellement volumineux (plus de 5 Mo), envisagez de le redimensionner d'abord afin de garder une utilisation mémoire raisonnable. Pillow peut le faire en une seule ligne :

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Étape 4 – Exécuter l'OCR sur PNG et capturer le résultat

Avec le moteur prêt et l'image chargée, il est temps de **exécuter l'OCR sur PNG** et de récupérer le résultat structuré.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

L’objet `ocr_result` contient une collection d’éléments `OcrRegion`, chacun avec le texte reconnu et un score de confiance (0‑100). C’est ici que vous obtenez les données granulaires nécessaires pour **extraire du texte de facture**.

---

## Étape 5 – Convertir le résultat en JSON et l’afficher joliment

La plupart des systèmes en aval préfèrent le JSON, nous allons donc transformer la sortie OCR en une chaîne bien formatée.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Exemple de sortie

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Remarquez que chaque ligne inclut une métrique de confiance — parfait pour filtrer les entrées à faible confiance si vous prévoyez d’**extraire du texte de facture** automatiquement.

---

## Étape 6 – Enregistrer les données OCR en CSV (une ligne par texte + confiance)

Le CSV est idéal pour les feuilles de calcul ou les importations rapides de données. Aspose propose une ligne de code pour tout exporter dans un fichier CSV.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Le CSV généré ressemblera à ceci :

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Vous pouvez maintenant l’ouvrir dans Excel, Google Sheets, ou l’alimenter dans une base de données.

---

## Bonus – Gestion du texte à faible confiance et des PDF multi‑pages

### Filtrage par confiance

Si vous ne voulez que les lignes à haute certitude, filtrez le JSON avant de l’écrire :

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Documents multi‑pages

Aspose.OCR crée automatiquement une nouvelle entrée `page` pour chaque page d’un PNG ou PDF multi‑pages. Parcourez `ocr_data["pages"]` pour les traiter toutes—aucun code supplémentaire n’est nécessaire.

---

## Exemple complet fonctionnel

Voici le **script complet** que vous pouvez copier, coller et exécuter immédiatement. Remplacez `YOUR_DIRECTORY` par le dossier contenant votre fichier PNG.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Exécutez le script avec `python run_ocr.py` et vous verrez le dump JSON dans la console, un fichier CSV sur le disque, et une liste filtrée d’entrées à haute confiance.

---

## Questions fréquentes

**Q : Puis‑je utiliser cela pour extraire du texte d’un reçu numérisé au lieu d’une facture ?**  
R : Absolument. Le même flux de travail s’applique—il suffit de pointer `image_path` vers votre PNG de reçu. Si le reçu utilise une langue différente, changez `engine.language` en conséquence.

**Q : Et si mon PNG contient du texte tourné ?**  
R : Aspose.OCR détecte automatiquement l’orientation, mais pour les cas récalcitrants vous pouvez faire pivoter manuellement l’image avec Pillow avant de la transmettre au moteur.

**Q : Ai‑je besoin d’une licence payante pour Aspose.OCR ?**  
R : La bibliothèque propose un mode d’évaluation gratuit avec un filigrane sur la sortie. Pour une utilisation en production, vous aurez besoin d’une licence, disponible sur le site d’Aspose.

---

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **exécuter l'OCR sur PNG** avec Python : installation du SDK, chargement de l’image, extraction de texte structuré, et sauvegarde du résultat en JSON ou CSV. Que vous souhaitiez **extraire du texte d’image** pour un script simple ou **extraire du texte de facture** pour une chaîne d’automatisation comptable, les étapes ci‑dessus vous offrent une base solide prête pour la production.

Ensuite, vous pourriez explorer :

- L’intégration de la sortie CSV avec une base de données pour le stockage en masse des factures.  
- L’ajout de post‑traitement avec des expressions régulières pour extraire dates, montants ou numéros de TVA.  
- L’utilisation de la fonction `ocr_engine.recognize_barcode` si vos factures contiennent des QR codes.

Essayez, ajustez les seuils de confiance, et voyez votre flux de traitement de documents devenir un jeu d’enfant. Vous avez d’autres questions ou un cas d’usage intéressant à partager ? Laissez un commentaire ci‑dessous—bon OCR !  

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – visual example of OCR result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}