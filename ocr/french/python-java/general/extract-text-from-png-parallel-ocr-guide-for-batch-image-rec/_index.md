---
category: general
date: 2026-03-18
description: Extraire du texte d’un PNG avec Python et Aspose OCR. Apprenez comment
  charger une image pour l’OCR, exécuter l’OCR sur plusieurs fichiers et réaliser
  une reconnaissance d’images en lot avec traitement parallèle.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: fr
og_description: Extraire du texte d’un PNG avec Aspose OCR en Python. Ce tutoriel
  montre comment charger une image pour l’OCR, traiter plusieurs fichiers OCR et exécuter
  un traitement par lots d’images OCR en utilisant la reconnaissance d’images parallèle.
og_title: Extraire du texte d’un PNG – Guide OCR parallèle
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Extraire le texte d’un PNG – Guide OCR parallèle pour la reconnaissance d’images
  par lots
url: /fr/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'un PNG – Guide OCR parallèle pour la reconnaissance d'images par lots

Vous avez déjà eu besoin d'**extraire du texte d'un PNG** mais vous êtes resté bloqué au moment où une seule image prend une éternité à être traitée ? Vous n'êtes pas seul. Dans de nombreux projets réels — pensez aux scanners de factures, aux numériseurs de reçus ou aux outils d'archivage — la vitesse compte, et traiter chaque PNG un par un ne suffit pas.  

Dans ce guide, nous parcourrons une solution complète, prête à l'emploi, qui **charge l'image pour l'OCR**, exécute **ocr multiple files** en mode **batch OCR images**, et exploite la **reconnaissance d'images parallèle** avec le module `threading` de Python. À la fin, vous disposerez d'un script qui extrait le texte d'un nombre quelconque de PNG en quelques secondes, pas en minutes.

## Ce dont vous avez besoin

- Python 3.8 ou plus récent (la syntaxe présentée fonctionne également sur 3.10+).  
- Le package Aspose OCR pour Java/​Python (`aspose-ocr`). Vous pouvez l'installer via `pip`.  
- Un dossier contenant quelques fichiers PNG que vous souhaitez traiter.  
- Une quantité modeste de RAM — chaque thread possède une petite instance du moteur OCR, de sorte même un ordinateur portable peut lancer des dizaines de travailleurs.

Pas de services externes, pas de clés cloud, et pas de fichiers de configuration mystérieux. Juste du code Python pur que vous pouvez copier‑coller et exécuter.

## Pourquoi extraire du texte d'un PNG en parallèle ?

Le traitement d'un PNG est limité par le CPU : le moteur OCR exécute une série d'algorithmes d'analyse d'image qui parcourent les données de pixels. Lorsque vous avez dix, vingt ou une centaine d'images, le temps d'exécution total est essentiellement la somme de chaque exécution individuelle.  

En créant un thread pour chaque fichier, nous laissons le système d'exploitation planifier ces tâches lourdes en CPU de manière concurrente. Sur une machine multi‑cœur, cela réduit souvent de moitié — voire de quatre fois — le temps réel. Le compromis est une empreinte mémoire légèrement plus élevée, mais pour la plupart des traitements par lots, le gain de vitesse en vaut largement la peine.

> **Astuce :** Si vous traitez des centaines de mégaoctets d'images, envisagez d'utiliser `concurrent.futures.ProcessPoolExecutor` au lieu de `threading`. Les processus offrent un vrai parallélisme sur l'interpréteur CPython limité par le GIL, au prix d'un peu plus de surcharge.

## Étape 1 : Installer Aspose OCR pour Python

Première chose à faire — installons la bibliothèque OCR sur votre système.

```bash
pip install aspose-ocr
```

Cette seule ligne récupère les dernières binaires Aspose OCR ainsi que ses liaisons Python. Si vous rencontrez une erreur de permission, essayez d'ajouter `--user` ou d'utiliser un environnement virtuel.

## Étape 2 : Charger l'image pour l'OCR – la fonction worker

Nous définissons maintenant la routine principale qui sera exécutée dans chaque thread. Elle **charge l'image pour l'OCR**, exécute la reconnaissance et affiche un aperçu du texte extrait.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Quelques points à noter :

- **Pourquoi un nouveau `OcrEngine` par thread ?** Le moteur possède des tampons internes ; partager une seule instance provoquerait des conditions de concurrence et un rendu illisible.  
- **Pourquoi supprimer les sauts de ligne ?** Lorsqu'on journalise dans la console, cela garde la ligne propre.  
- **Gestion des erreurs ?** En production, vous envelopperiez le corps dans un `try/except` et éventuellement enregistreriez dans un fichier — quelque chose que nous aborderons plus tard.

## Étape 3 : Lister les fichiers PNG à traiter

Vous pourriez coder en dur la liste, mais une approche plus flexible consiste à parcourir un répertoire. Ci-dessous, nous listons manuellement trois fichiers pour plus de clarté ; remplacez les chemins par votre propre dossier.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Si vous préférez une découverte automatique :

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Cette petite modification vous permet d'**extraire du texte d'un PNG** en masse sans toucher au code source à chaque fois.

## Étape 4 : Configurer ocr multiple files avec batch OCR images

Nous créons maintenant un thread pour chaque image. C'est le cœur du modèle **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

La compréhension de liste maintient le code concis, et chaque objet `Thread` stocke la fonction cible et son argument (`image_path`).  

> **Note :** Le module `threading` de Python utilise les threads natifs du système d'exploitation, ainsi sur un ordinateur portable à 4 cœurs vous verrez généralement jusqu'à quatre threads réellement exécutés simultanément ; les autres seront planifiés lorsque des cœurs seront libres.

## Étape 5 : Exécuter la reconnaissance d'images parallèle

Lancer les workers est simple : itérer sur la liste et appeler `start()`. Ensuite, nous attendons que chaque thread se termine en utilisant `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Lorsque le script se termine, vous verrez une série de lignes comme :

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Cette sortie confirme que chaque PNG a été traité et que le texte extrait est disponible pour un traitement ultérieur (par ex., sauvegarde dans une base de données ou alimentation d'un pipeline NLP).

## Étape 6 : Vérifier les résultats et gérer les cas limites

### Vérification des résultats vides

Parfois, une image est trop bruitée, ou le moteur OCR ne détecte aucun caractère. Un contrôle rapide peut vous éviter des erreurs en aval.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Limiter le nombre de threads concurrents

Si vous exécutez cela sur une VM modeste, créer des centaines de threads peut submerger le planificateur. Vous pouvez limiter la concurrence avec un sémaphore :

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Enregistrer les résultats dans un fichier

Au lieu d'imprimer, vous pourriez vouloir un CSV contenant le nom de fichier et le texte extrait :

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Assurez‑vous d'ouvrir le CSV **une seule fois** en dehors de la fonction thread afin d'éviter les conditions de concurrence ; l'écrivain du module `csv` est sûr pour les écritures simples.

## Exemple complet fonctionnel

En rassemblant le tout, voici un script unique que vous pouvez placer dans un fichier nommé `batch_ocr.py` et exécuter :

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}