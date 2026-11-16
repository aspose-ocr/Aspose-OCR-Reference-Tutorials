---
category: general
date: 2026-03-26
description: Comment réaliser une OCR par lots efficacement avec Python — apprenez
  à extraire du texte d’images et de PDF grâce à la conversion OCR en traitement parallèle.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: fr
og_description: Comment faire de l'OCR par lots efficacement — guide étape par étape
  pour extraire du texte d'images, conversion OCR de PDF et traitement OCR par lots
  avec Python.
og_title: 'comment faire du OCR par lots : extraction de texte rapide et parallèle'
tags:
- OCR
- Python
- Parallel Computing
title: 'Comment réaliser un OCR par lots : extraction rapide de texte en parallèle'
url: /fr/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment effectuer un OCR en lot : extraction de texte parallèle rapide

Vous vous êtes déjà demandé **how to batch ocr** lorsque vous avez des dizaines de pages numérisées, captures d'écran et PDF qui traînent ? Vous n'êtes pas le seul—la plupart des développeurs rencontrent le même problème : traiter chaque fichier un par un devient un goulet d'étranglement pénible.  

La bonne nouvelle, c'est que vous pouvez lancer une poignée de threads de travail, leur fournir tous vos fichiers, et regarder le moteur OCR parcourir le lot en parallèle. Dans ce tutoriel, nous passerons en revue un exemple complet, prêt à l'emploi, qui montre **extract text from images**, effectue **pdf ocr conversion**, et exploite **parallel ocr processing** pour la rapidité.

> **Ce que vous retirerez**  
> * Un script Python entièrement fonctionnel qui traite une liste mixte de fichiers PNG, TIFF, PDF et JPG en une seule fois.  
> * Compréhension des raisons pour lesquelles un pool de threads accélère les tâches OCR liées aux I/O.  
> * Astuces pour gérer les erreurs, les gros PDF et les nombres de threads personnalisés.  

## Prérequis

| Exigence | Raison |
|----------|--------|
| Python 3.8+ | Modern syntax & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Provides `OcrBatchProcessor` and result objects |
| Une poignée de fichiers d'exemple (PNG, TIFF, PDF, JPG) | Pour voir **extract text from images** en action |
| Familiarité de base avec les threads (optionnel) | Utile mais pas obligatoire |

Si vous n'avez pas encore installé le package `ocr`, exécutez :

```bash
pip install ocr-lib   # replace with the actual package name
```

Maintenant que l'environnement est prêt, décomposons le problème.

## Étape 1 : Importer les aides et instancier le processeur de lot

La première chose dont nous avons besoin est un endroit pour rassembler tous les travaux OCR. La classe `OcrBatchProcessor` fait exactement cela —elle met en file d'attente les éléments de travail et vous renvoie une liste d'objets `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Pourquoi c'est important* : L'importation de `as_completed` nous permet de réagir instantanément à chaque travail terminé, au lieu d'attendre le fichier le plus lent. C'est le cœur du **batch ocr processing**.

## Étape 2 : Ajuster le pool de workers pour l'exécution parallèle

Par défaut, le processeur peut utiliser un seul thread, ce qui annule l'intérêt du traitement par lots. Nous demandons explicitement quatre workers—n'hésitez pas à augmenter ce nombre jusqu'au nombre de cœurs CPU dont vous disposez.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Astuce* : Pour les tâches I/O‑bound comme l'OCR, vous obtenez souvent des rendements décroissants après `CPU cores * 2`. Testez quelques valeurs et choisissez le point optimal.

## Étape 3 : Mettre en file d'attente chaque fichier que vous souhaitez OCRer

Ici, nous ajoutons un mélange de fichiers image et PDF. La méthode `add` enregistre simplement le chemin ; le travail réel ne commencera pas avant que nous soumettions le lot.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Si vous devez traiter un dossier complet, une boucle `glob` rapide fait l'affaire :

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Étape 4 : Lancer les jobs et collecter les futures

Appeler `submit_all` donne le feu vert au processeur. Il renvoie une liste d'objets `Future`—considérez‑les comme des espaces réservés pour des résultats qui apparaîtront plus tard.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

À ce stade, le moteur OCR travaille en arrière‑plan, chaque thread se chargeant d'un fichier.

## Étape 5 : Récupérer les résultats dès qu'ils sont terminés

En utilisant `as_completed`, nous parcourons les futures dans l'ordre de leur achèvement, pas dans l'ordre de leur soumission. Cela maintient notre script réactif, surtout lorsque certains PDF prennent plus de temps que de simples PNG.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Sortie attendue** (troncée pour plus de concision) :

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Chaque bloc correspond à la représentation texte brut du fichier original. Si vous effectuez une **pdf ocr conversion**, le texte inclura tout ce que le moteur OCR a pu déchiffrer de chaque page.

## Gestion des cas limites et des pièges courants

| Situation | À surveiller | Solution rapide |
|-----------|--------------|-----------------|
| Une image corrompue | `future.result()` raises `OSError` | Enveloppez dans `try/except` (voir le code ci‑dessus) |
| PDF très volumineux ( > 100 Mo ) | Pression mémoire, threads plus lents | Augmentez modestement `thread_count` ou divisez le PDF en chapitres d'abord |
| Documents multilingues | Le modèle OCR par défaut peut mal détecter | Passez des indices de langue à `OcrBatchProcessor` si la bibliothèque le supporte |
| Besoin de préserver la mise en page | `get_text()` simple perd les colonnes | Utilisez `ocr_result.get_hocr()` ou une méthode similaire consciente de la mise en page |

### Astuce : Nombre de threads personnalisé selon le type de fichier

Si vous savez que la majeure partie de votre charge de travail est constituée de PDF, vous pouvez allouer plus de threads pour ceux‑ci et moins pour les petits PNG. Certaines bibliothèques vous permettent de passer une `priority` par job ; sinon, vous pouvez créer deux lots séparés—un pour les images, un pour les PDF—et les exécuter simultanément.

## Vue d'ensemble visuelle (optionnel)

![diagramme du flux de batch ocr](https://example.com/ocr-workflow.png "flux de batch ocr")

*Le diagramme illustre le flux depuis la découverte des fichiers → création du lot → exécution parallèle → agrégation des résultats.*

## Script complet à copier‑coller

Ci-dessous se trouve le programme complet, prêt à être placé dans un fichier `.py`. Il inclut tous les extraits ci‑dessus, ainsi qu'un petit assistant qui découvre automatiquement les fichiers pris en charge dans un répertoire.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Enregistrez-le sous le nom `batch_ocr.py`, pointez-le vers un dossier contenant vos scans, et observez la console se remplir de texte extrait.  

### Pourquoi cela fonctionne

* **Thread pool** – L'OCR attend principalement les I/O disque et les appels au moteur externe, donc plusieurs threads maintiennent le CPU occupé.  
* **`as_completed`** – Vous obtenez les résultats dès qu'ils sont prêts, ce qui est idéal pour le retour d'interface utilisateur ou les pipelines de streaming.  
* **Error isolation** – Un fichier défectueux ne fera pas tomber tout le lot ; le bloc `try/except` isole les échecs.

## Conclusion

En résumé, vous savez maintenant **how to batch ocr** en utilisant `concurrent.futures` de Python avec une bibliothèque OCR qui prend en charge le traitement par lots. En configurant un pool de threads modeste, en mettant en file d'attente chaque fichier pris en charge et en récupérant les résultats dès qu'ils sont terminés, vous obtenez un **parallel ocr processing** rapide sans sacrifier la fiabilité.  

À partir d'ici, vous pourriez :

* Connecter la sortie à un index de recherche pour une récupération rapide des documents.  
* Étendre le script pour écrire chaque résultat dans un fichier `.txt` à côté de l'original.  
* Remplacer le pool de threads intégré par `asyncio` si votre bibliothèque OCR propose des API asynchrones.  

Continuez à expérimenter—remplacez par Tesseract, Azure Cognitive Services ou Google Vision, et vous verrez le même schéma s'appliquer. Bon OCR !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}