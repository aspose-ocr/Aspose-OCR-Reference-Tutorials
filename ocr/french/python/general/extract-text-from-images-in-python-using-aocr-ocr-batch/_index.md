---
category: general
date: 2026-06-25
description: Extraire du texte d’images avec la bibliothèque Python aocr – apprendre
  la reconnaissance OCR par lots, définir le mode de reconnaissance imprimé et ajouter
  un post‑processeur IA.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: fr
og_description: Extrayez du texte à partir d'images en utilisant la bibliothèque Python
  aocr. Ce tutoriel montre la reconnaissance OCR par lots, le mode de reconnaissance
  d'imprimé et le post‑processeur IA optionnel.
og_title: Extraire du texte à partir d'images en Python – Guide complet du batch aocr
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Extraire du texte d'images en Python avec aocr OCR Batch
url: /fr/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'images en Python avec aocr OCR Batch

Vous avez déjà eu besoin **d'extraire du texte à partir d'images** mais vous êtes submergé par des dizaines de petites étapes ? Vous n'êtes pas seul. Que vous numérisiez des formulaires scannés, récupériez des données à partir de reçus, ou construisiez une archive consultable, obtenir des résultats OCR fiables à grande échelle peut ressembler à gravir une colline escarpée.

Bonne nouvelle ? Avec la **bibliothèque aocr** vous pouvez lancer un **batch OCR Python** complet en quelques lignes seulement. Dans ce guide, nous allons créer un batch OCR, charger toutes les images prises en charge depuis un dossier, choisir le bon **mode de reconnaissance printed**, et même ajouter un **post‑processus IA** pour un gain supplémentaire de précision. À la fin, vous disposerez d’un script prêt à l’emploi qui extrait le texte des images et indique la quantité capturée par fichier.

## Ce que vous allez apprendre

- Comment installer et importer le package `aocr`.
- Configurer un `OcrBatch` pour gérer des milliers de fichiers automatiquement.
- Choisir le mode de reconnaissance optimal pour les documents imprimés.
- (Optionnel) Brancher un post‑processus IA pour nettoyer les résultats bruyants.
- Afficher chaque chemin de fichier avec la longueur du texte extrait.
- Astuces pour gérer les cas limites comme les formats non pris en charge ou les pages vides.

### Prérequis

- Python 3.8 ou supérieur installé sur votre machine.  
- Familiarité de base avec le scripting Python (boucles, imports, etc.).  
- Accès à un dossier d’images scannées (PNG, JPG, TIFF, etc.).  

Si vous avez tout cela, plongeons‑y—aucun service externe requis.

## Étape 1 : Installer la bibliothèque aocr

Première chose à faire. Le package `aocr` ne fait pas partie de la bibliothèque standard, il faut donc le récupérer sur PyPI.

```bash
pip install aocr
```

> **Astuce :** Utilisez un environnement virtuel (`python -m venv .venv`) pour isoler les dépendances.  

Une fois installé, vous pouvez importer les classes principales.

```python
# core imports
import aocr
```

## Étape 2 : Créer une instance d’OCR Batch

Un `OcrBatch` est le moteur qui parcourra votre répertoire et suivra chaque fichier image. Pensez‑y comme à un tapis roulant qui alimente les images dans le moteur OCR.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

À ce stade le batch est vide, mais nous le remplirons à l’étape suivante.

## Étape 3 : Ajouter toutes les images prises en charge depuis un dossier (récursivement)

Vous avez probablement une structure de dossiers imbriquée—peut‑être un sous‑dossier par client ou par mois. La méthode `add_folder` parcourt l’arbre pour vous, en récupérant chaque image qu’elle sait lire.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Remplacez `"YOUR_DIRECTORY/scanned_forms/"` par le chemin réel sur votre système. Après cet appel, `ocr_batch.file_paths` contient une liste de noms de fichiers absolus, et le batch sait exactement combien d’éléments il devra traiter.

## Étape 4 : Choisir le mode de reconnaissance pour le texte imprimé

Le moteur `aocr` prend en charge plusieurs modes (handwritten, printed, mixed). Comme nous traitons des formulaires imprimés propres, définissez le mode en conséquence. Ce petit drapeau peut améliorer considérablement la précision car le moteur évite les heuristiques lourdes nécessaires aux écritures cursives.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Pourquoi c’est important :** Le texte imprimé possède des lignes de base et des formes de caractères cohérentes, ce qui permet au modèle OCR d’appliquer des dictionnaires de caractères plus stricts. Si vous laissez le mode sur « auto », vous risquez d’obtenir du bruit supplémentaire sur des scans basse résolution.

## Étape 5 : (Optionnel) Attacher un post‑processus IA

Si vos scans souffrent de flou, de faible contraste ou de polices inhabituelles, un post‑processus IA peut nettoyer la sortie brute de l’OCR avant de la transmettre aux systèmes en aval. La méthode `set_ai_postprocessor` attend un objet implémentant une interface `process(text: str) -> str`.

Voici un exemple minimal utilisant une classe fictive `SimpleCleaner`. En pratique, vous pourriez brancher un transformeur HuggingFace, un modèle de langue personnalisé, ou même un correcteur orthographique basé sur des règles.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Si vous sautez cette étape, le batch renverra simplement les chaînes OCR brutes.

## Étape 6 : Exécuter l’OCR sur l’ensemble du batch et collecter les résultats

Le gros du travail commence maintenant. La méthode `run` parcourt chaque fichier, lance le moteur OCR, fait passer la sortie par le post‑processus IA optionnel, et renvoie une liste de chaînes — une par image.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Comme la méthode renvoie une simple liste Python, vous pouvez la manipuler comme n’importe quelle collection — la stocker, l’écrire dans un CSV, ou l’alimenter dans une base de données.

## Étape 7 : Afficher chaque chemin de fichier avec la longueur du texte extrait

Une vérification rapide consiste à imprimer le nombre de caractères extraits de chaque fichier. Si une page est blanche ou que l’OCR a échoué, vous verrez une longueur de `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Un résultat typique ressemble à :

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Voir un drapeau `0` indique immédiatement quels fichiers nécessitent une seconde vérification (peut‑être corrompus ou pas du tout des images).

## Gestion des cas limites courants

### 1. Types de fichiers non pris en charge

`aocr` ignore silencieusement les fichiers qu’il ne peut pas décoder. Si vous suspectez la présence de PDF ou de BMP mélangés, filtrez‑les au préalable :

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Gros batches et consommation de mémoire

Traiter des milliers de scans haute résolution peut gonfler l’utilisation de la mémoire. Atténuez cela en traitant par morceaux :

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Pages vides ou à faible contraste

Si une page produit moins de 10 caractères, vous pouvez la marquer pour une révision manuelle :

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Exemple complet fonctionnel

En rassemblant le tout, voici un script que vous pouvez copier‑coller et exécuter immédiatement. Enregistrez‑le sous le nom `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Sortie attendue** (truncée pour la brièveté) :

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Exécutez‑le avec :

```bash
python batch_ocr.py
```

Si tout est correctement configuré, vous verrez une ligne pour chaque image, chacune indiquant le nombre de caractères du texte extrait.

## Foire aux questions

**Q : Cela fonctionne‑t‑il sur les PDF ?**  
R : Pas directement. `aocr` ne gère que les images raster. Convertissez les PDF en PNG/TIFF d’abord (par ex., avec `pdf2image`).

**Q : Puis‑je changer le mode de reconnaissance en manuscrit ?**  
R : Absolument — remplacez simplement `aocr.RecognitionMode.PRINTED` par `aocr.RecognitionMode.HANDWRITTEN`. Attendez‑vous à un temps d’exécution plus long mais à de meilleurs résultats sur des notes cursives.

**Q : Et si j’ai besoin d’un support multilingue ?**  
R : La bibliothèque fournit des packs de langues. Installez le module de langue souhaité (`pip install aocr-lang-fr` pour le français, etc.) et définissez `ocr_batch.language = "fr"` avant l’exécution.

## Prochaines étapes et sujets associés

- **Traitement parallèle :** Enveloppez l’exécution du batch dans un `concurrent.futures.ThreadPoolExecutor` pour exploiter plusieurs cœurs CPU.  
- **Stockage des résultats :** Écrivez `ocr_results` dans un CSV ou une base SQLite pour des analyses en aval.  
- **Intégration avec le cloud IA :** Remplacez le `SimpleCleaner` par un modèle transformeur de HuggingFace pour une correction orthographique de pointe.  
- **Fine‑tuning de aocr :** Si vous disposez d’un jeu de polices personnalisé, explorez `aocr.Trainer` pour améliorer la précision en mode imprimé.

---

C’est tout—vous avez maintenant une base solide


## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}