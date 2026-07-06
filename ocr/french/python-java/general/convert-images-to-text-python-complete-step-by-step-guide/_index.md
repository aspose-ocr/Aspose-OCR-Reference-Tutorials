---
category: general
date: 2026-05-31
description: Apprenez à convertir des images en texte avec Python grâce à un script
  de conversion d’images en texte en masse. Reconnaissez le texte des images numérisées
  avec Aspose.OCR en quelques minutes.
draft: false
keywords:
- convert images to text python
- bulk image to text conversion
- recognize text from scanned images
language: fr
og_description: Convertir des images en texte avec Python instantanément. Ce guide
  montre la conversion d’images en texte en masse et comment reconnaître le texte
  à partir d’images numérisées avec Aspose.OCR.
og_title: Convertir des images en texte Python – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  headline: Convert Images to Text Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to convert images to text python with a bulk image to text
    conversion script. Recognize text from scanned images using Aspose.OCR in minutes.
  name: Convert Images to Text Python – Complete Step‑by‑Step Guide
  steps:
  - name: Imports the OCR engine classes.
    text: Imports the OCR engine classes.
  - name: Instantiates a `BatchOcrEngine`.
    text: Instantiates a `BatchOcrEngine`.
  - name: Points the engine at an input folder of images.
    text: Points the engine at an input folder of images.
  - name: Directs the engine to write each extracted text file into an output folder.
    text: Directs the engine to write each extracted text file into an output folder.
  - name: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
    text: Fires the `recognize()` method, which **recognize text from scanned images**
      one by one.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Convertir des images en texte Python – Guide complet étape par étape
url: /fr/python-java/general/convert-images-to-text-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir des images en texte Python – Guide complet étape par étape

Vous vous êtes déjà demandé comment **convertir des images en texte python** sans devoir fouiller des dizaines de bibliothèques ? Vous n'êtes pas seul. Que vous numérisiez d'anciens reçus, extrayiez des données de factures scannées, ou construisiez une archive PDF consultable, transformer des images en fichiers texte brut est une tâche quotidienne pour de nombreux développeurs.

Dans ce tutoriel, nous allons parcourir un pipeline de **conversion d’images en texte en masse** qui reconnaît le texte à partir d’images scannées, enregistre chaque résultat dans un fichier `.txt` individuel, et le fait le tout en quelques lignes de Python. Pas de recherche d’API obscures — Aspose.OCR fait le gros du travail, et nous vous montrons exactement comment le configurer.

## Ce que vous allez apprendre

- Comment installer et configurer le package Aspose.OCR pour Python.  
- Le code exact nécessaire pour **convertir des images en texte python** à l’aide du `BatchOcrEngine`.  
- Des astuces pour gérer les pièges courants comme les formats non pris en charge ou les fichiers corrompus.  
- Des méthodes pour vérifier que l’étape **reconnaître le texte à partir d’images scannées** a réellement réussi.  

À la fin de ce guide, vous disposerez d’un script prêt à l’emploi capable de traiter des milliers d’images en une seule fois—parfait pour tout scénario de traitement par lots.

## Prérequis

- Python 3.8+ installé sur votre machine.  
- Un dossier contenant les fichiers image (PNG, JPEG, TIFF, etc.) que vous souhaitez transformer en texte.  
- Un compte Aspose Cloud actif ou une licence d’essai gratuite (le niveau gratuit suffit pour les tests).  

Si vous avez tout cela, plongeons‑y.

---

## Étape 1 – Configurer votre environnement Python

Avant d’écrire du code OCR, assurez‑vous de travailler dans un environnement virtuel propre. Cela isole les dépendances et évite les conflits de versions.

```bash
# Create a new virtual environment named venv
python -m venv venv

# Activate the environment (Windows)
venv\Scripts\activate

# Activate the environment (macOS / Linux)
source venv/bin/activate
```

> **Astuce :** Gardez votre répertoire de projet bien organisé—créez un sous‑dossier nommé `ocr_project` et placez le script à l’intérieur. Cela simplifie la gestion des chemins plus tard.

## Étape 2 – Installer Aspose.OCR pour Python

Aspose.OCR est une bibliothèque commerciale, mais elle est distribuée avec une roue de type NuGet gratuite que vous pouvez récupérer depuis PyPI. Exécutez la commande suivante dans l’environnement virtuel activé :

```bash
pip install aspose-ocr
```

Si vous obtenez une erreur de permission, ajoutez le drapeau `--user` ou lancez la commande avec `sudo` (Linux/macOS uniquement). Après l’installation, vous devriez voir quelque chose comme :

```
Successfully installed aspose-ocr-23.9.0
```

> **Pourquoi Aspose ?** Contrairement à de nombreux outils OCR open‑source, Aspose.OCR prend en charge la **conversion d’images en texte en masse** dès le départ et gère une large gamme de formats d’image sans configuration supplémentaire. Il propose également la classe `BatchOcrEngine` qui transforme la tâche **convertir des images en texte python** en une opération d’une seule ligne.

## Étape 3 – Convertir des images en texte Python avec le Batch OCR

Passons maintenant au cœur du tutoriel. Le script ci‑dessous est entièrement exécutable et :

1. Importe les classes du moteur OCR.  
2. Instancie un `BatchOcrEngine`.  
3. Pointe le moteur vers un dossier d’entrée contenant les images.  
4. Indique au moteur d’écrire chaque fichier texte extrait dans un dossier de sortie.  
5. Lance la méthode `recognize()`, qui **reconnaît le texte à partir d’images scannées** une par une.  

Enregistrez le fichier suivant sous le nom `batch_ocr.py` dans votre dossier de projet :

```python
# batch_ocr.py
# -------------------------------------------------
# Bulk Image to Text Conversion using Aspose.OCR
# -------------------------------------------------

# Step 1: Import the OCR engine classes
from asposeocr import BatchOcrEngine, OcrEngine

# Step 2: Create a batch OCR engine instance
batch_engine = BatchOcrEngine()

# Step 3: Set the folder that contains the images to be processed
# Replace 'YOUR_DIRECTORY' with the absolute path to your images folder
batch_engine.input_folder = "YOUR_DIRECTORY/input_images"

# Step 4: Set the folder where the extracted text files will be saved
# Make sure this folder exists or Aspose will raise an error
batch_engine.output_folder = "YOUR_DIRECTORY/output_texts"

# Optional: Adjust OCR settings if you need higher accuracy
# For example, enable language detection for multilingual documents
# batch_engine.ocr_engine.language = "eng+spa"  # English + Spanish

# Step 5: Run the batch recognition – each supported image in the input folder is processed
batch_engine.recognize()

# Step 6: Notify that the batch operation has finished
print("Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.")
```

### Comment ça fonctionne

- **`BatchOcrEngine`** enveloppe le `OcrEngine` classique mais ajoute une orchestration au niveau du dossier, exactement ce qu’il faut lorsque vous voulez **convertir des images en texte python** en lot.  
- La propriété `input_folder` indique au moteur où chercher les images sources. Il parcourt automatiquement le répertoire et met en file d’attente chaque type de fichier pris en charge.  
- La propriété `output_folder` détermine où chaque fichier `.txt` sera placé. Le moteur reproduit le nom de fichier d’origine, ainsi `receipt1.png` devient `receipt1.txt`.  
- L’appel à `recognize()` déclenche la boucle interne qui charge chaque image, exécute l’OCR et écrit le résultat. La méthode bloque jusqu’à ce que tous les fichiers soient traités, ce qui facilite le chaînage d’actions supplémentaires (par ex., compresser le dossier de sortie).

#### Résultat attendu

Lorsque vous exécutez le script :

```bash
python batch_ocr.py
```

Vous devriez voir :

```
Batch processing complete. Text files saved to YOUR_DIRECTORY/output_texts.
```

Dans le dossier `output_texts`, vous trouverez un fichier texte pour chaque image. Ouvrez‑en un avec un éditeur de texte et vous verrez le résultat brut de l’OCR — généralement une approximation proche du texte imprimé d’origine.

## Étape 4 – Vérifier les résultats et gérer les erreurs

Même les meilleurs moteurs OCR peuvent rencontrer des difficultés avec des scans basse résolution ou des pages fortement inclinées. Voici une méthode rapide pour vérifier la cohérence de la sortie et consigner les échecs.

```python
import os

def verify_output(output_dir):
    txt_files = [f for f in os.listdir(output_dir) if f.lower().endswith('.txt')]
    empty_files = [f for f in txt_files if os.path.getsize(os.path.join(output_dir, f)) == 0]

    if empty_files:
        print("Warning: The following files are empty – OCR may have failed:")
        for f in empty_files:
            print(f"  • {f}")
    else:
        print("All text files contain data. OCR succeeded for every image.")

# Run verification after batch processing
verify_output(batch_engine.output_folder)
```

**Pourquoi ajouter cela ?**  
- Cela capture les cas où le moteur produit silencieusement une chaîne vide (courant avec les images illisibles).  
- Cela vous fournit une liste de fichiers problématiques afin que vous puissiez les inspecter manuellement ou relancer le processus avec d’autres paramètres (par ex., augmenter les options `OcrEngine.preprocess`).  

### Cas particuliers & ajustements

| Situation | Solution suggérée |
|-----------|-------------------|
| Les images sont pivotées de 90° | Définissez `batch_engine.ocr_engine.rotation_correction = True`. |
| Langues mixtes (anglais + français) | Utilisez `batch_engine.ocr_engine.language = "eng+fra"` avant `recognize()`. |
| Gros PDFs convertis d’abord en images | Découpez les PDFs en images page par page, puis alimentez le dossier du batch engine. |
| Erreurs de mémoire sur des lots très volumineux | Traitez des sous‑dossiers plus petits séquentiellement, ou augmentez `batch_engine.max_memory_usage`. |

## Étape 5 – Automatiser le workflow complet (optionnel)

Si vous devez exécuter cette conversion chaque nuit, encapsulez le script dans un simple script shell ou un fichier batch Windows, puis planifiez‑le avec `cron` (Linux/macOS) ou le Planificateur de tâches (Windows). Voici un `run_ocr.sh` minimal pour les systèmes de type Unix :

```bash
#!/usr/bin/env bash
# run_ocr.sh – Automate bulk image to text conversion

# Activate virtual environment
source /path/to/venv/bin/activate

# Execute the OCR script
python /path/to/ocr_project/batch_ocr.py

# Deactivate after completion
deactivate
```

Rendez‑le exécutable (`chmod +x run_ocr.sh`) et ajoutez une entrée cron :

```cron
0 2 * * * /path/to/run_ocr.sh >> /var/log/ocr_batch.log 2>&1
```

Cela exécutera la conversion chaque jour à 2 h du matin et consignera toute sortie pour une révision ultérieure.

---

## Conclusion

Vous disposez maintenant d’une méthode éprouvée, prête pour la production, afin de **convertir des images en texte python** en utilisant le `BatchOcrEngine` d’Aspose.OCR. Le script gère la **conversion d’images en texte en masse**, écrit chaque résultat dans un fichier dédié, et inclut des étapes de vérification pour s’assurer que vous **reconnaissez le texte à partir d’images scannées** correctement.

À partir d’ici, vous pouvez :

- Expérimenter avec différents paramètres OCR (packs de langues, correction d’inclinaison, réduction du bruit).  
- Alimenter le texte généré dans un index de recherche comme Elasticsearch pour une recherche plein texte instantanée.  
- Combiner ce pipeline avec des outils de conversion PDF afin de traiter des PDFs scannés en une seule passe.  

Des questions ou un problème avec un type de fichier particulier ? Laissez un commentaire ci‑dessous, et résolvons‑le ensemble. Bon codage, et que vos exécutions OCR soient rapides et sans erreur !

## Ce que vous devriez apprendre ensuite

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}