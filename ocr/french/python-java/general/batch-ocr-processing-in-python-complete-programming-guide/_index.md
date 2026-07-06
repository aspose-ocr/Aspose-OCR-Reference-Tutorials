---
category: general
date: 2026-06-25
description: Traitement OCR par lots en Python simplifié. Apprenez comment extraire
  du texte d'un lot d'images et maîtrisez l'extraction de texte de lots d'images avec
  des threads parallèles.
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: fr
og_description: Le traitement OCR par lots en Python vous permet d'extraire rapidement
  le texte d'un lot d'images. Ce tutoriel vous guide à travers l'OCR parallèle avec
  des exemples de code clairs.
og_title: Traitement OCR par lots en Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Traitement OCR par lots en Python – Guide complet de programmation
url: /fr/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Traitement OCR par lots en Python – Guide complet de programmation

Vous avez déjà eu besoin d’un **traitement OCR par lots** mais vous ne saviez pas comment l’exécuter efficacement sur des dizaines de pages numérisées ? Vous n’êtes pas seul — les développeurs se heurtent souvent à un mur lorsqu’ils essaient d’extraire du texte d’un lot d’images sans saturer leur CPU.  

Dans ce guide, nous vous montrons une méthode simple pour **extraire du texte d’un lot d’images** en utilisant le moteur OCR de Python, exécuter le travail sur jusqu’à huit threads, puis afficher combien de caractères chaque image a fourni. À la fin, vous disposerez d’un script réutilisable qui gère **l’extraction de texte d’images par lots** comme un pro.

## Ce que couvre ce tutoriel

Nous parcourrons trois étapes pratiques :

1. Construire une liste de fichiers image que vous souhaitez reconnaître.  
2. Lancer le moteur OCR en parallèle avec `max_threads=8`.  
3. Parcourir les résultats et imprimer un résumé concis.

Pas de services externes, pas de bibliothèques obscures — juste du Python pur et un wrapper OCR typique (par exemple, `ocr` provenant de `easyocr` ou d’un wrapper personnalisé). Si vous avez Python 3.8+ et un paquet OCR installé, vous êtes prêt à copier‑coller et à exécuter.

---

## Étape 1 : Préparer une liste de fichiers image pour le traitement OCR par lots

La première chose dont vous avez besoin est une collection de chemins d’image. Considérez‑la comme une liste de courses pour le moteur OCR ; chaque entrée pointe vers un fichier PNG, JPEG ou TIFF contenant le texte que vous voulez lire.

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**Pourquoi c’est important :**  
Créer la liste à l’avance permet au moteur OCR de fonctionner en véritable mode lot. Cela vous donne également un endroit unique pour ajouter ou retirer des fichiers sans toucher à la logique de traitement plus tard. La vérification de validité évite le crash « file not found » redouté à mi‑parcours d’une exécution longue.

---

## Étape 2 : Exécuter l’OCR sur le lot avec des threads parallèles (Extract Text from Image Batch)

Nous transmettons maintenant la liste au moteur OCR. La plupart des wrappers OCR modernes exposent une méthode `recognize_batch` qui accepte un argument `max_threads`. En le réglant sur `8`, nous demandons à la bibliothèque de créer huit threads de travail, ce qui, sur un CPU quad‑core avec hyper‑threading, peut réduire considérablement le temps de traitement.

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**Pourquoi le parallélisme aide :**  
L’OCR est gourmand en CPU ; chaque image est passée à travers un réseau de neurones ou un moteur hérité. Les exécuter les unes après les autres peut être très lent, surtout pour des scans haute résolution. Les threads parallèles maintiennent tous les cœurs occupés, transformant une tâche de 5 minutes en une minute sur du matériel typique.

**Astuce :** Si vous utilisez `easyocr`, l’appel ressemble à `reader.readtext(image_path, detail=0)` dans une boucle. Notre abstraction `recognize_batch` masque cette complexité, mais vous pouvez toujours la remplacer par votre propre `ThreadPoolExecutor` si la bibliothèque ne propose pas de support de lot.

---

## Étape 3 : Parcourir les résultats et résumer l’extraction de texte d’images par lots

Une fois l’OCR terminé, vous disposerez d’une liste d’objets résultat. Faisons le zip des chemins de fichiers originaux avec leurs sorties OCR correspondantes et imprimons une ligne claire pour chaque image indiquant le nombre de caractères reconnus.

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Ce que vous verrez :**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**Pourquoi cette étape est utile :**  
Un comptage rapide des caractères vous indique en un clin d’œil si une image a été traitée correctement. Un nombre anormalement bas peut suggérer un scan flou, un mauvais réglage de langue ou un fichier corrompu — des problèmes que vous pouvez corriger avant de passer à l’analyse en aval.

---

## Bonus : Gestion des cas limites et des pièges courants

### Images manquantes ou corrompues  
Si une image ne peut pas être ouverte, la plupart des bibliothèques OCR lèvent une exception qui interrompt tout le lot. Enveloppez l’appel dans un `try/except` à l’intérieur de la fonction de lot ou filtrez les fichiers problématiques au préalable (voir la vérification de validité à l’Étape 1).

### Paramètres de langue et de DPI  
Pour les documents multilingues, passez un paramètre `langs` (par ex., `langs=['en', 'de']`). Si vos scans sont de faible résolution, envisagez un pré‑traitement avec `Pillow` pour les upscaler à 300 DPI avant l’OCR — cela améliore souvent la précision.

### Contraintes de mémoire  
Huit threads peuvent consommer beaucoup de RAM, surtout avec de grandes images. Si vous rencontrez des erreurs de mémoire, réduisez `max_threads` ou traitez la liste par petits morceaux :

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## Script complet fonctionnel

En réunissant tous les éléments, voici un exemple complet, prêt à être exécuté. Remplacez `"YOUR_DIRECTORY"` par le chemin contenant vos fichiers PNG et assurez‑vous que le module `ocr` est installé.

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Sortie attendue** (vos nombres varieront) :

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

Exécutez le script avec `python batch_ocr.py` et observez le terminal se remplir de statistiques concises.

---

## Vue d’ensemble visuelle

![Diagramme du traitement OCR par lots](image-placeholder.png "Diagramme illustrant les étapes du traitement OCR par lots")

*Texte alternatif de l’image :* *Diagramme du traitement OCR par lots montrant la création de la liste de fichiers, l’exécution OCR parallèle et la synthèse des résultats.*

---

## Conclusion

Vous disposez maintenant d’une base solide pour le **traitement OCR par lots** en Python. En préparant une liste propre d’images, en exploitant des threads parallèles pour **extract text from image batch**, et en résumant les résultats, vous transformez une tâche manuelle fastidieuse en un pipeline rapide et reproductible.  

À partir d’ici, vous pouvez :

- Enregistrer chaque `result.text` dans un fichier `.txt` pour un traitement NLP en aval.  
- Combiner les comptes de caractères avec les scores de confiance pour filtrer les pages de mauvaise qualité.  
- Intégrer le script dans un workflow d’ingestion de documents plus large, éventuellement pour alimenter un index de recherche.

Que vous numérisiez des archives, développiez une application de numérisation de reçus, ou prépariez des données d’entraînement pour un modèle linguistique, les concepts présentés ici s’étendent à des centaines voire des milliers de fichiers avec peu d’ajustements.

Des questions sur les réglages de langue, le pré‑traitement d’image, ou le déploiement dans le cloud ? Laissez un commentaire ou consultez les tutoriels associés sur *Python image preprocessing* et *asynchronous OCR with asyncio*. Bon codage !

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}