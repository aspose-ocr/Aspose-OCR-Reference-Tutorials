---
category: general
date: 2026-03-28
description: Extrayez rapidement du texte à partir de PNG en utilisant Aspose OCR
  en Python. Apprenez à convertir le texte des pages numérisées avec la reconnaissance
  d'image parallèle en Python pour des résultats haute performance.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: fr
og_description: Extrayez rapidement du texte à partir de PNG en utilisant Aspose OCR
  en Python. Ce guide montre comment convertir le texte des pages numérisées avec
  la reconnaissance d’image parallèle en Python, offrant des résultats à grande vitesse.
og_title: Extraire du texte d'un PNG – OCR parallèle rapide avec Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Extraire le texte d’un PNG – OCR parallèle rapide avec Python et Aspose
url: /fr/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'un PNG – OCR parallèle rapide avec Python

Vous avez déjà eu besoin d'**extraire du texte d'un PNG** mais trouvé l'OCR monothread très lent ? Vous n'êtes pas seul. Que vous numérisiez une pile de reçus scannés ou que vous transformiez des diapositives de cours en PDF recherchables, le goulot d'étranglement est généralement l'étape OCR elle‑même.  

Dans ce tutoriel, nous vous présenterons une solution complète, prête à l'emploi, qui **convertit le texte des pages scannées** en parallèle, en utilisant le mode batch asynchrone d'Aspose OCR avec le `ThreadPoolExecutor` de Python. À la fin, vous pourrez **reconnaître du texte d'image en style python**, en traitant des dizaines d'images en une fraction du temps qu'une boucle naïve prendrait.

> **Ce que vous en retirerez**  
> * Un script entièrement fonctionnel qui extrait le texte des images PNG de façon concurrente.  
> * Une compréhension des raisons pour lesquelles le mode batch asynchrone accélère les choses.  
> * Des astuces pour faire évoluer la solution vers des charges de travail plus importantes.

## Ce dont vous avez besoin

| Prérequis | Raison |
|--------------|--------|
| Python 3.9+ | Syntaxe moderne et annotations de type. |
| `aspose-ocr` and `aspose-storage` packages | Fournissent le moteur OCR et le chargeur d'images. |
| A folder of PNG files (e.g., scanned pages) | Le matériel source que vous souhaitez traiter. |
| Basic knowledge of Python concurrency | Utile mais pas obligatoire ; nous expliquerons tout. |

You can install the Aspose libraries with:

```bash
pip install aspose-ocr aspose-storage
```

> **Astuce :** Gardez vos paquets à jour (`pip list --outdated`) pour profiter des dernières améliorations de performance.

## Étape 1 : Initialiser le moteur Aspose OCR en mode batch asynchrone

La première chose que nous faisons est de créer une instance `OcrEngine` et de la passer en **mode batch asynchrone**. Ce mode met en file d'attente les requêtes de reconnaissance en interne, permettant au moteur de traiter plusieurs images sans bloquer votre thread Python.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Pourquoi asynchrone ?*  
Lorsque vous appelez `recognize` en mode synchrone, l'appel bloque jusqu'à ce que l'image soit entièrement traitée. En mode asynchrone, le moteur peut commencer à travailler sur l'image suivante pendant que la courante est encore en cours de décodage, chevauchant ainsi les opérations d'E/S et le travail du CPU.

## Étape 2 : Lister les fichiers PNG à traiter

Ici nous définissons la collection d'images. Dans un projet réel, vous pourriez générer cette liste dynamiquement (par ex., `glob.glob("*.png")`), mais la garder explicite rend l'exemple facile à suivre.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Note :** Remplacez `YOUR_DIRECTORY` par le chemin réel où se trouvent vos scans PNG. Si vous avez des centaines de fichiers, envisagez d'utiliser `os.listdir` et de filtrer pour les `.png`.

## Étape 3 : Écrire une fonction d'aide qui charge une image et renvoie son texte

L'aide abstrait le processus en deux étapes de chargement d'un fichier via **Aspose Storage** puis de le transmettre au moteur OCR. Ajouter une petite docstring rend la fonction auto‑documentée—utile pour la maintenance future.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Pourquoi une fonction séparée ?*  
Cela garde le code du thread‑pool propre et nous permet de réutiliser la logique ailleurs (par ex., dans un endpoint Flask). De plus, isoler les I/O facilite le débogage — si un fichier particulier échoue, vous verrez le nom du fichier dans la trace d'exception.

## Étape 4 : Exécuter la reconnaissance d'image en parallèle avec Python et un pool de threads

Nous introduisons maintenant `ThreadPoolExecutor`. Par défaut, nous lançons quatre workers, mais vous pouvez ajuster `max_workers` en fonction du nombre de cœurs CPU et de la taille du jeu d'images.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Comment cela vous donne une reconnaissance d'image parallèle en Python

* **ThreadPoolExecutor** crée un pool de threads workers qui appellent chacun `recognize_image`.  
* Comme le moteur OCR est en mode batch asynchrone, chaque thread peut transmettre le travail au moteur tout en restant réactif.  
* `as_completed` renvoie les futures dans l'ordre de leur achèvement, vous obtenez ainsi les résultats dès qu'ils sont prêts—parfait pour le streaming de gros lots.

> **Piège courant :** Utiliser `max_workers=1` annule l'intérêt du parallélisme. Sur une machine à 8 cœurs, `max_workers=8` donne souvent le meilleur débit, mais testez plusieurs valeurs pour trouver le point optimal pour votre matériel.

## Étape 5 : Vérifier la sortie et gérer les cas limites

Lorsque vous exécutez le script, vous devriez voir un bloc de texte pour chaque PNG, précédé de son nom de fichier :

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Si une image échoue (fichier corrompu, format non supporté), le bloc `except` affiche un message d'erreur utile au lieu de faire planter tout le lot.

### Étendre la solution

| Scénario | Ajustement suggéré |
|----------|--------------------|
| **Thousands de pages** | Passer à `ProcessPoolExecutor` pour exploiter plusieurs processus CPU, ou découper la liste et traiter les lots séquentiellement. |
| **Différents formats d'image (JPG, TIFF)** | La méthode `storage.Image.load` détecte automatiquement le format, il suffit donc d'ajouter les fichiers à `input_images`. |
| **Besoin de stocker les résultats** | Écrire `text` dans un fichier `.txt` ou l'insérer dans une base de données dans le bloc `else`. |
| **Surveillance des performances** | Envelopper `recognize_image` avec un chronomètre (`time.perf_counter`) et consigner la durée par fichier. |

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le script complet, prêt à être placé dans un fichier nommé `parallel_ocr.py`. Aucun élément ne manque — tout ce dont vous avez besoin se trouve ici.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Enregistrez le fichier, ajustez le placeholder `YOUR_DIRECTORY`, puis exécutez :

```bash
python parallel_ocr.py
```

Vous devriez voir le texte extrait pour chaque PNG apparaître dans la console, comme montré précédemment.

## Conclusion

Nous venons de démontrer comment **extraire du texte d'un PNG** efficacement en combinant le mode batch asynchrone d'Aspose OCR avec le `ThreadPoolExecutor` de Python. Le script convertit le texte des pages scannées en parallèle, vous offrant une méthode évolutive pour **reconnaître du texte d'image en style python** sans écrire un pool de threads personnalisé à partir de zéro.  

Si vous êtes prêt à pousser cela plus loin, essayez :

* Stocker les résultats dans une base de données SQLite recherchable.  
* Ajouter un pré‑traitement d'image (redressement, débruitage) avec OpenCV avant l'OCR.  
* Déployer le script comme microservice derrière un endpoint Flask ou FastAPI.  

Rappelez‑vous, la clé d'un OCR haute performance n'est pas seulement un moteur plus rapide — il s'agit aussi d'alimenter ce moteur de travail d'une manière qui maximise la concurrence. Avec le modèle présenté ici, vous pouvez gérer des dizaines voire des centaines de scans PNG avec peu de modifications de code.

Bon codage, et que vos PDF soient toujours recherchables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}