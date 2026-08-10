---
category: general
date: 2026-06-06
description: Extraire du texte d’images PDF à l’aide de Python OCR. Apprenez comment
  convertir rapidement des documents numérisés en texte avec une reconnaissance par
  lots asynchrone.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: fr
og_description: Extraire du texte d'images PDF avec Python. Ce guide étape par étape
  montre comment convertir des documents numérisés en texte en utilisant l'OCR asynchrone.
og_title: Extraire du texte d'images PDF – Tutoriel OCR Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extraire le texte des images PDF – Guide Python pour convertir les documents
  numérisés en texte
url: /fr/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'images PDF – Guide Python pour convertir des documents numérisés en texte

Vous avez déjà eu besoin d'**extraire du texte à partir d'images pdf** sans passer des heures à retaper ? Dans ce guide, nous vous montrerons comment **convertir des documents numérisés en texte** en utilisant un flux de travail OCR asynchrone simple en Python.  

Si vous avez déjà contemplé une pile de PDF numérisés en vous disant « Il doit bien y avoir une façon plus rapide », vous êtes au bon endroit. Nous passerons en revue chaque ligne de code, expliquerons pourquoi chaque élément est important, et couvrirons même quelques cas limites que vous pourriez rencontrer.

## Ce que vous apprendrez

- Comment démarrer un moteur OCR et définir la langue de reconnaissance.  
- Le fonctionnement de l'alimentation d'une liste mixte de PNG et PDF dans un reconnaisseur par lots.  
- Exécuter la tâche OCR de manière asynchrone afin que votre application reste réactive.  
- Récupérer les résultats, les associer à leurs fichiers sources et afficher une sortie propre.  

**Prérequis** : Python 3.8+, une compréhension de base de `asyncio` ou `concurrent.futures`, et une bibliothèque OCR qui expose une classe `OcrEngine` similaire à celle de l'exemple (par ex., Aspose.OCR, wrapper Tesseract, ou un wrapper personnalisé). Aucun réglage lourd requis — installez simplement la bibliothèque et vous êtes prêt à partir.

![extraire du texte à partir d'images pdf](https://example.com/placeholder.png "Capture d'écran de la sortie OCR – extraire du texte à partir d'images pdf")

## Extraire du texte à partir d'images PDF – Configurer le moteur OCR

La première chose dont vous avez besoin est une instance de moteur OCR configurée pour la langue de vos documents. Dans notre cas, nous utiliserons le français, mais vous pouvez le remplacer par n'importe quelle langue prise en charge.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Pourquoi c’est important** : Définir la langue dès le départ améliore considérablement la précision. Le moteur utilise des dictionnaires et des modèles de caractères spécifiques à chaque langue ; le fournir avec la mauvaise langue est une source fréquente de sortie brouillée.

## Préparer la liste de fichiers – Images et PDF ensemble

Notre reconnaisseur par lots peut gérer à la fois les images raster (`.png`, `.jpg`) et les conteneurs PDF. Il suffit de fournir une simple liste Python de chemins de fichiers.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Astuce** : Gardez la liste plate ; le moteur décompressera chaque page PDF en images en interne avant la reconnaissance. Si vous avez des milliers de fichiers, envisagez de découper la liste en lots plus petits afin d'éviter des pics de mémoire.

## Lancer la reconnaissance par lots asynchrone

Au lieu de bloquer le thread principal, nous lançons la tâche OCR en arrière‑plan. La méthode renvoie un `Future` qui contiendra finalement une liste d'objets `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Comment ça fonctionne** : En coulisses, le moteur crée un pool de threads (ou une tâche async, selon l'implémentation). Cela vous permet de continuer d'autres travaux — comme mettre à jour une UI, récupérer davantage de fichiers, ou journaliser la progression — pendant que le traitement lourd s'effectue ailleurs.

## Faire quelque chose d’utile pendant que l’OCR s’exécute

Une erreur courante consiste à rester inactif et à interroger le futur dans une boucle serrée. À la place, vous pouvez effectuer n'importe quel travail non lié. Pour la démonstration, nous nous contenterons d'imprimer une ligne d'état.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Rassembler les résultats une fois le futur terminé

Lorsque vous êtes prêt à collecter la sortie OCR, utilisez `as_completed` de `concurrent.futures`. Ce modèle fonctionne que vous ayez un futur ou plusieurs.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Ce que vous verrez** : Chaque chemin de fichier suivi de la représentation texte brute extraite. Pour les PDF, `result.text` contient le texte concaténé de chaque page.

### Sortie attendue (exemple)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Si vous remarquez des caractères manquants, revérifiez que la langue que vous avez définie correspond à la langue du document, et envisagez de pré‑traiter les images (redressement, augmentation du contraste) avant de les fournir au moteur.

## Gestion des cas limites et des pièges courants

| Situation | Que faire |
|-----------|-----------|
| **Langues mixtes** | Effectuer d'abord une passe de détection de langue, puis instancier des moteurs séparés par langue. |
| **PDF volumineux (> 100 Mo)** | Diviser le PDF en pages individuelles sur le disque (par ex., avec `PyPDF2`) et les fournir comme entrées séparées. |
| **Scripts non latins** | S'assurer que la bibliothèque OCR inclut le pack de langue requis ; certaines bibliothèques exigent le téléchargement de fichiers de données supplémentaires. |
| **Goulot d'étranglement de performance** | Augmenter la taille du pool de threads (`engine.set_thread_pool_size(8)`) ou passer à un backend accéléré GPU si disponible. |
| **Texte manquant dans les images basse résolution** | Pré‑traiter avec OpenCV : `cv2.resize`, `cv2.threshold` et `cv2.medianBlur` pour améliorer la lisibilité. |

## Exemple complet fonctionnel (prêt à copier‑coller)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Enregistrez ceci sous `extract_text_async.py`, remplacez `YOUR_DIRECTORY` par le chemin vers vos fichiers, installez le paquet OCR (`pip install your-ocr-lib`), puis exécutez `python extract_text_async.py`. Vous devriez voir la sortie console illustrée précédemment.

## Prochaines étapes – Aller au‑delà de l’extraction basique

- **Post‑traitement** : Supprimer les espaces superflus, normaliser l'Unicode (`unicodedata.normalize`), ou exécuter un correcteur orthographique pour nettoyer le bruit OCR.  
- **Sortie structurée** : Exporter les résultats vers CSV, JSON, ou directement dans une base de données pour la recherche en aval.  
- **Lots parallèles** : Si vous avez des centaines de fichiers, lancez plusieurs futures et utilisez une file d'attente pour garder le CPU occupé sans saturer la mémoire.  
- **Intégration avec des frameworks web** : Connecter ce script à un endpoint Flask ou FastAPI pour fournir un OCR à la demande en tant que service.

---

### TL;DR

Vous savez maintenant comment **extraire du texte à partir d'images pdf** avec un script Python minimal qui exécute l'OCR de façon asynchrone, vous permettant de **convertir des documents numérisés en texte** tout en gardant votre programme réactif. Expérimentez avec les paramètres de langue, les tailles de lots et les astuces de pré‑traitement pour obtenir la meilleure précision possible.

Vous avez une variante à partager — peut‑être l’OCR sur des notes manuscrites ou un service cloud ? Laissez un commentaire, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte à partir d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraire du texte à partir d'images en utilisant l'opération OCR sur des dossiers](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extraire du texte à partir d'images en utilisant Aspose.OCR – Caractères autorisés](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}