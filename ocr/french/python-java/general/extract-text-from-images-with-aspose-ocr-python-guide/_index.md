---
category: general
date: 2026-03-18
description: Apprenez à extraire du texte à partir d’images et à convertir le texte
  d’images numérisées en chaînes éditables en utilisant Aspose OCR en Python. Code
  étape par étape inclus.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: fr
og_description: Extrayez du texte à partir d'images en utilisant Aspose OCR en Python.
  Ce tutoriel montre comment convertir le texte des images numérisées en quelques
  lignes de code.
og_title: Extraire du texte à partir d'images avec Aspose OCR – Guide Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Extraire du texte d'images avec Aspose OCR – Guide Python
url: /fr/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'images avec Aspose OCR – Guide Python

Vous avez déjà eu besoin d'**extraire du texte à partir d'images** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul — les développeurs sont constamment confrontés à la difficulté de transformer des PDF numérisés, des captures d'écran bruyantes ou des reçus photographiés en chaînes recherchables et modifiables.  

Bonne nouvelle ! Avec Aspose OCR pour Python, vous pouvez **convertir le texte d'images numérisées** en masse, sans quitter votre IDE. Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l'exécution, qui montre exactement comment faire, pourquoi chaque étape est importante et quels pièges éviter.

## Ce que vous apprendrez

- Installer la bibliothèque Aspose OCR dans un environnement Python.  
- Préparer une liste de fichiers image (PNG, JPG, TIFF, etc.).  
- Exécuter l'OCR par lots avec un appel de méthode unique.  
- Accéder et afficher le texte extrait pour chaque fichier.  
- Gérer les pièges courants comme les formats non pris en charge et l'utilisation mémoire des gros fichiers.  

À la fin, vous disposerez d'un script réutilisable capable d'**extraire du texte à partir d'images** à la demande — idéal pour automatiser la saisie de données, indexer des documents ou alimenter des pipelines NLP en aval.

---

![Extract text from images example](/images/ocr-extract-text.png "extraire du texte à partir d'images")

*Texte alternatif de l'image : “extraire du texte à partir d'images avec Aspose OCR en Python”*

## Prérequis

- Python 3.8 ou plus récent (le code utilise des f‑strings).  
- Une licence valide d'Aspose OCR pour Python ou une clé d'essai gratuite.  
- Les images que vous souhaitez traiter stockées localement (tout mélange de PNG, JPG ou TIFF).  

Si vous avez déjà un environnement virtuel, tant mieux — sinon, créez‑en un avec :

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Vous êtes maintenant prêt à installer le SDK.

## Étape 1 : Installer le SDK Aspose OCR

Aspose distribue son moteur OCR via PyPI, donc une simple commande `pip` suffit :

```bash
pip install aspose-ocr
```

> **Astuce pro :** Verrouillez la version (par ex., `aspose-ocr==22.12`) pour éviter des changements incompatibles inattendus plus tard.

## Étape 2 : Importer la classe du moteur OCR

La classe principale avec laquelle vous interagirez est `OcrEngine`. Importez‑la en haut de votre script :

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Pourquoi c’est important :* N'importer que ce dont vous avez besoin maintient le temps de démarrage bas, surtout lorsque vous intégrez plus tard le script dans une application plus grande.

## Étape 3 : Définir les fichiers image à traiter

Créez une liste Python contenant les chemins complets vers chaque image que vous voulez analyser. Remplacez `YOUR_DIRECTORY` par le chemin réel du dossier.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Cas limite :** Si vous avez des centaines de fichiers, envisagez de générer cette liste de façon programmatique avec `glob.glob('*.png')` afin d'éviter les modifications manuelles.

## Étape 4 : Exécuter l'OCR sur toutes les images d'un coup

Aspose OCR fournit une méthode pratique `processMultiple` qui renvoie une liste d'objets `OcrResult` — un pour chaque fichier d'entrée.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Pourquoi le traitement par lots ?* Envoyer chaque image individuellement entraîne un surcoût supplémentaire (initialisation du moteur, chargement des bibliothèques natives). L'appel par lot réduit la charge CPU et accélère le travail global.

### Gérer les erreurs de manière élégante

Si une image ne peut pas être lue (fichier corrompu, format non pris en charge), `processMultiple` lèvera une exception. Enveloppez l'appel dans un bloc `try/except` pour que le script reste actif :

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Étape 5 : Afficher le texte extrait pour chaque fichier

Itérez sur les résultats, en associant chaque `OcrResult` à son nom de fichier d'origine. La méthode `getText()` renvoie la chaîne reconnue.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Sortie attendue

Exécuter le script complet sur trois captures d'écran simples peut produire quelque chose comme :

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Si une image ne contient aucun caractère reconnaissable, vous verrez une chaîne vide — rien ne plante, et vous pourrez décider de signaler ce fichier pour une révision manuelle.

## Bonus : Affiner la précision de l'OCR

Aspose OCR propose plusieurs paramètres optionnels que vous pourriez vouloir expérimenter :

| Paramètre | Ce qu'il fait | Quand l'utiliser |
|-----------|----------------|-------------------|
| `ocr_engine.setLanguage('eng')` | Force le modèle de langue anglais (réduit les faux positifs). | Principalement les documents en anglais. |
| `ocr_engine.setResolution(300)` | Améliore la précision sur les scans à faible résolution. | Scans inférieurs à 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | Traite l'image entière comme un seul bloc de texte. | Reçus simples ou cartes d'identité. |

Vous pouvez ajouter ces lignes juste après la création de `ocr_engine` :

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Pièges courants et comment les éviter

1. **Piles TIFF volumineuses** – Un TIFF multi‑pages peut consommer plusieurs gigaoctets de RAM lorsqu'il est chargé en une fois. Divisez le fichier en images mono‑page avant de le transmettre à `processMultiple`.  
2. **Scripts non latins** – Si vous devez **extraire du texte à partir d'images** contenant des caractères cyrilliques, arabes ou chinois, changez le code de langue en conséquence (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Espaces dans les chemins de fichiers** – Les chemins Windows contenant des espaces peuvent provoquer `FileNotFoundError`. Enveloppez chaque chemin dans des chaînes brutes (`r"C:\My Folder\image.png"`) ou utilisez `os.path.abspath`.  

Anticiper ces problèmes vous évite des erreurs d'exécution obscures plus tard.

---

## Exemple complet fonctionnel

Voici le script complet que vous pouvez copier‑coller dans un fichier nommé `batch_ocr.py`. Il inclut toutes les bonnes pratiques évoquées ci‑dessus.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Enregistrez, activez votre environnement virtuel, puis exécutez :

```bash
python batch_ocr.py
```

Vous devriez voir les chaînes extraites affichées dans la console, prêtes pour un traitement ultérieur (par ex., sauvegarde dans une base de données ou alimentation d'un modèle de langage naturel).

---

## Conclusion

Dans ce guide, nous avons montré comment **extraire du texte à partir d'images** en utilisant Aspose OCR pour Python, en couvrant tout, de l'installation au traitement par lots et à la gestion des erreurs. Le script est compact, pleinement fonctionnel et facile à étendre — que vous ayez besoin de **convertir le texte d'images numérisées** en fichiers CSV, d'alimenter un index de recherche ou simplement d'automatiser la saisie de données.

Prêt pour l'étape suivante ? Envisagez d'associer ce pipeline OCR à un fusionneur de PDF pour créer des PDF recherchables, ou de le connecter à un déclencheur de stockage cloud afin que chaque scan téléchargé soit traité instantanément. Le ciel est la limite, et vous disposez maintenant d'une base solide pour construire.

Des questions ou des idées d'amélioration ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}