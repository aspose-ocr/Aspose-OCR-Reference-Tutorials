---
category: general
date: 2026-01-12
description: Extraire du texte d’une image avec Python en utilisant Aspose OCR. Apprenez
  à convertir une image numérisée en texte avec du code asynchrone en quelques minutes.
draft: false
keywords:
- extract text from image python
- convert scanned image to text
language: fr
og_description: Extraire du texte d’une image Python avec Aspose OCR. Ce tutoriel
  montre comment convertir une image numérisée en texte en utilisant des fonctions
  asynchrones.
og_title: Extraire du texte d’une image avec Python – Guide OCR asynchrone
tags:
- python
- ocr
- async
title: Extraire du texte d’une image avec Python – Guide OCR asynchrone
url: /fr/python-java/general/extract-text-from-image-python-async-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d’une image avec Python – Guide OCR Asynchrone

Vous avez déjà eu besoin d’**extraire du texte d’une image Python** dans vos scripts mais vous êtes bloqué au niveau de l’OCR ? Vous n’êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu’ils ont un document numérisé et souhaitent le transformer en texte recherchable sans perdre patience.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre comment **convertir une image numérisée en texte** en utilisant l’API asynchrone d’Aspose OCR. À la fin, vous disposerez d’une fonction unique que vous pourrez intégrer dans n’importe quel projet, et vous comprendrez pourquoi le traitement asynchrone permet à votre application de rester réactive même lorsque l’OCR prend quelques secondes.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Python 3.8+ installé (les fonctionnalités async nécessitent au moins la version 3.7)
- Le package `asposeocr` (`pip install asposeocr`) – c’est la bibliothèque que nous utiliserons
- Un fichier image numérisé (TIFF, PNG, JPEG – tout ce qu’Aspose OCR prend en charge)
- Une connaissance de base de `asyncio` (si vous n’en avez pas, pas d’inquiétude – nous expliquerons chaque étape)

Aucune dépendance système supplémentaire n’est requise ; Aspose OCR regroupe tout ce dont vous avez besoin.

![Diagramme montrant le flux OCR asynchrone – extraire du texte d’une image python](https://example.com/async-ocr-diagram.png "flux OCR asynchrone – extraire du texte d’une image python")

## Étape 1 – Configurer la fonction d’assistance asynchrone  

Le cœur de la solution est une fonction `async` qui charge une image, lance l’OCR, puis attend le résultat. Garder la fonction asynchrone signifie que vous pouvez exécuter d’autres coroutines (par ex., télécharger d’autres fichiers) pendant que le moteur OCR travaille en arrière‑plan.

```python
import asposeocr as ocr
import asyncio

async def async_ocr(image_path: str) -> str:
    """
    Extracts text from the given image file using Aspose OCR asynchronously.
    
    Parameters
    ----------
    image_path: str
        Path to the scanned image (e.g., 'input.tif')
    
    Returns
    -------
    str
        Recognized plain‑text string
    """
    # Initialize the OCR engine and set the language to English.
    ocr_engine = ocr.OcrEngine()
    ocr_engine.language = ocr.Language.ENGLISH

    # Start the OCR operation. process_async returns a Future‑like object.
    ocr_future = ocr_engine.process_async(ocr.Image.load(image_path))

    # Here you could perform other async work – we just yield control.
    await asyncio.sleep(0)

    # Await the OCR result and pull out the recognized text.
    ocr_result = await ocr_future
    return ocr_result.text
```

**Pourquoi c’est important :** En renvoyant un `Future`, Aspose OCR effectue le travail lourd dans un pool de threads séparé. `await` libère la boucle d’événements, de sorte que votre application reste fluide. Si vous devez traiter de nombreuses images simultanément, il suffit de planifier plusieurs appels `async_ocr` avec `asyncio.gather`.

## Étape 2 – Exécuter la coroutine dans la boucle d’événements  

Maintenant que nous avons une fonction d’assistance, nous devons l’exécuter. `asyncio.run` crée une nouvelle boucle d’événements, exécute la coroutine et ferme proprement le tout.

```python
if __name__ == "__main__":
    # Replace with the actual path to your scanned file.
    image_file = "YOUR_DIRECTORY/input.tif"

    # Run the async OCR function and capture the output.
    recognized_text = asyncio.run(async_ocr(image_file))

    # Print the extracted text to the console.
    print("=== OCR RESULT ===")
    print(recognized_text)
```

**Astuce :** Si vous intégrez cela dans une application async plus grande (par ex., FastAPI), vous appelleriez directement `await async_ocr(...)` au lieu de `asyncio.run`.

## Étape 3 – Vérifier la sortie  

Lorsque vous lancez le script, vous devriez voir quelque chose comme :

```
=== OCR RESULT ===
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

Si la sortie apparaît illisible, revérifiez que :

1. L’image est nette et pas trop compressée.  
2. Vous avez sélectionné la bonne langue (`ocr.Language.ENGLISH` fonctionne pour la plupart des textes latins).  
3. Le chemin du fichier est correct et le fichier est lisible.

## Étape 4 – Gestion des cas particuliers  

### Plusieurs langues  

Si vous devez **convertir une image numérisée en texte** dans une langue autre que l’anglais, il suffit de modifier la propriété de langue :

```python
ocr_engine.language = ocr.Language.FRENCH   # or ocr.Language.SPANISH, etc.
```

### Fichiers volumineux  

Pour des TIFF très gros, envisagez de redimensionner ou de convertir en PNG à résolution plus basse avant de les envoyer à l’OCR. Cela réduit la pression sur la mémoire et accélère le traitement.

```python
# Example: downscale a huge image (requires Pillow)
from PIL import Image as PilImage

pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000))  # max dimension 2000px
pil_img.save("temp_resized.png")
ocr_future = ocr_engine.process_async(ocr.Image.load("temp_resized.png"))
```

### Gestion des erreurs  

Enveloppez l’appel OCR dans un bloc `try/except` pour intercepter les erreurs liées au réseau ou à la licence.

```python
try:
    ocr_result = await ocr_future
except ocr.OcrException as exc:
    print(f"OCR failed: {exc}")
    return ""
```

## Étape 5 – Mise à l’échelle : traiter de nombreuses images en parallèle  

Comme la fonction est async, vous pouvez lancer des dizaines de jobs OCR simultanément :

```python
async def batch_ocr(image_paths):
    tasks = [async_ocr(p) for p in image_paths]
    return await asyncio.gather(*tasks)

if __name__ == "__main__":
    files = ["doc1.tif", "doc2.tif", "doc3.tif"]
    results = asyncio.run(batch_ocr(files))
    for i, text in enumerate(results):
        print(f"--- Result for {files[i]} ---")
        print(text)
```

Ce modèle maintient le CPU occupé pendant que le moteur OCR travaille en parallèle, réduisant ainsi de façon spectaculaire le temps de traitement total.

## Conclusion  

Vous disposez maintenant d’une solution robuste d’**extraction de texte d’une image Python** qui exploite l’API asynchrone d’Aspose OCR. L’exemple complet montre comment :

1. Initialiser le moteur OCR et sélectionner une langue.  
2. Lancer l’OCR de façon asynchrone avec `process_async`.  
3. Attendre le résultat sans bloquer la boucle d’événements.  
4. Gérer les pièges courants comme les fichiers volumineux et le support multilingue.  

N’hésitez pas à adapter le code à vos propres pipelines — que vous construisiez un système de gestion de documents, un indexeur de recherche ou un simple utilitaire en ligne de commande. Les étapes suivantes pourraient inclure :

- Stocker le texte extrait dans une base de données pour la recherche en texte intégral.  
- Ajouter la génération de PDF (par ex., avec `PyPDF2`) pour créer des PDF recherchables.  
- Intégrer avec un framework web comme FastAPI pour un service OCR RESTful.

Bon codage, et profitez de la transformation de vos images numérisées en texte searchable et éditable !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}