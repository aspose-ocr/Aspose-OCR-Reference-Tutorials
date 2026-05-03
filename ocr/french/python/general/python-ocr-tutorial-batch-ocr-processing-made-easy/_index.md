---
category: general
date: 2026-05-03
description: Tutoriel Python OCR montrant comment charger des fichiers image PNG,
  reconnaître le texte à partir d’une image et des ressources IA gratuites pour le
  traitement OCR par lots.
draft: false
keywords:
- python ocr tutorial
- batch ocr processing
- free ai resources
- load png image
- recognize text from image
language: fr
og_description: Le tutoriel Python OCR vous guide à travers le chargement d’images
  PNG, la reconnaissance de texte à partir d’une image et la gestion des ressources
  IA gratuites pour le traitement OCR par lots.
og_title: Tutoriel OCR Python – OCR par lots rapide avec des ressources IA gratuites
tags:
- OCR
- Python
- AI
title: Tutoriel OCR Python – Traitement par lots d'OCR simplifié
url: /fr/python/general/python-ocr-tutorial-batch-ocr-processing-made-easy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutoriel OCR Python – Traitement par lots simplifié

Vous avez déjà eu besoin d'un **python ocr tutorial** qui vous permette réellement de lancer de l'OCR sur des dizaines de fichiers PNG sans perdre patience ? Vous n'êtes pas seul. Dans de nombreux projets réels, il faut **load png image** des fichiers, les envoyer à un moteur, puis nettoyer les ressources IA une fois terminé.  

Dans ce guide, nous parcourrons un exemple complet, prêt à l’emploi, qui montre exactement comment **recognize text from image** des fichiers, les traiter par lots, et libérer la mémoire IA sous‑jacente. À la fin, vous disposerez d’un script autonome que vous pourrez intégrer à n’importe quel projet—sans fioritures, juste l’essentiel.

## Ce dont vous avez besoin

- Python 3.10 ou plus récent (la syntaxe utilisée repose sur les f‑strings et les annotations de type)  
- Une bibliothèque OCR qui expose une méthode `engine.recognize` — pour la démonstration, nous supposerons un package fictif `aocr`, mais vous pouvez le remplacer par Tesseract, EasyOCR, etc.  
- Le module d’aide `ai` montré dans l’extrait de code (il gère l’initialisation du modèle et le nettoyage des ressources)  
- Un dossier rempli de fichiers PNG que vous souhaitez traiter  

Si vous n’avez pas `aocr` ou `ai` installés, vous pouvez les simuler avec des stubs — voir la section « Optional Stubs » près de la fin.

## Étape 1 : Initialiser le moteur IA (Free AI Resources)

Avant d’alimenter le pipeline OCR avec une image, le modèle sous‑jacent doit être prêt. L’initialiser une seule fois économise de la mémoire et accélère les traitements par lots.

```python
# step_1_initialize.py
import ai                # hypothetical helper that wraps the AI model
import aocr               # OCR library

def init_engine(config_path: str = "config.yaml"):
    """
    Initialize the AI engine if it hasn't been set up yet.
    This uses free AI resources – the engine will be released later.
    """
    if not ai.is_initialized():
        ai.initialize(config_path)   # auto‑initialize with the provided configuration
    else:
        print("Engine already initialized.")
```

**Pourquoi c’est important :**  
Appeler `ai.initialize` à chaque image allouerait de la mémoire GPU à chaque fois, ce qui finirait par faire planter le script. En vérifiant `ai.is_initialized()` nous garantissons une allocation unique — c’est le principe du « free AI resources ».

## Étape 2 : Charger les fichiers PNG pour le traitement OCR par lots

Nous rassemblons maintenant tous les fichiers PNG que nous voulons passer à l’OCR. L’utilisation de `pathlib` rend le code indépendant du système d’exploitation.

```python
# step_2_load_images.py
from pathlib import Path
from typing import List

def collect_png_paths(directory: str) -> List[Path]:
    """
    Scan `directory` and return a list of Path objects pointing to PNG files.
    """
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files
```

**Cas limite :**  
Si le dossier contient des fichiers non‑PNG (par ex. des JPEG), ils seront ignorés, évitant ainsi que `engine.recognize` ne plante sur un format non supporté.

## Étape 3 : Exécuter l’OCR sur chaque image et appliquer le post‑traitement

Avec le moteur prêt et la liste de fichiers préparée, nous pouvons parcourir les images, extraire le texte brut, et le transmettre à un post‑processeur qui nettoie les artefacts OCR courants (comme les sauts de ligne parasites).

```python
# step_3_ocr_batch.py
import aocr
import ai
from pathlib import Path
from typing import List

def ocr_batch(image_paths: List[Path]) -> List[str]:
    """
    Perform OCR on each PNG image and return a list of cleaned strings.
    """
    results = []
    for image_path in image_paths:
        # Load the image – aocr.Image.load abstracts away Pillow/OpenCV details
        img = aocr.Image.load(str(image_path))
        
        # Recognize raw text
        raw_text = engine.recognize(img)
        
        # Refine the raw OCR output using the AI post‑processor
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters extracted.")
    
    return results
```

**Pourquoi séparer le chargement de la reconnaissance :**  
`aocr.Image.load` peut effectuer un décodage paresseux, ce qui est plus rapide pour de gros lots. Garder l’étape de chargement explicite facilite également le remplacement par une autre bibliothèque d’images si vous devez plus tard gérer des JPEG ou TIFF.

## Étape 4 : Nettoyage – Libérer les ressources IA après le lot

Une fois le lot terminé, nous devons libérer le modèle pour éviter les fuites de mémoire, surtout sur les machines équipées de GPU.

```python
# step_4_cleanup.py
import ai

def release_resources():
    """
    Free any allocated AI resources. Safe to call multiple times.
    """
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources have been released.")
    else:
        print("No AI resources were allocated.")
```

## Assemblage complet – Le script entier

Voici un fichier unique qui assemble les quatre étapes en un flux de travail cohérent. Enregistrez‑le sous le nom `batch_ocr.py` et exécutez‑le depuis la ligne de commande.

```python
# batch_ocr.py
"""
Python OCR tutorial – end‑to‑end batch OCR processing.
Loads PNG images, runs OCR, post‑processes results, and frees AI resources.
"""

import sys
from pathlib import Path
import ai
import aocr

# ----------------------------------------------------------------------
# Helper functions (copied from the steps above)
# ----------------------------------------------------------------------
def init_engine(cfg: str = "config.yaml"):
    if not ai.is_initialized():
        ai.initialize(cfg)
    else:
        print("Engine already initialized.")

def collect_png_paths(directory: str):
    base_path = Path(directory)
    if not base_path.is_dir():
        raise NotADirectoryError(f"'{directory}' is not a valid folder.")
    png_files = sorted(base_path.glob("*.png"))
    if not png_files:
        raise FileNotFoundError("No PNG images found in the specified directory.")
    print(f"Found {len(png_files)} PNG image(s) to process.")
    return png_files

def ocr_batch(image_paths):
    results = []
    for image_path in image_paths:
        img = aocr.Image.load(str(image_path))
        raw_text = engine.recognize(img)
        cleaned_text = ai.run_postprocessor(raw_text)
        results.append(cleaned_text)
        print(f"Processed {image_path.name}: {len(cleaned_text)} characters.")
    return results

def release_resources():
    if ai.is_initialized():
        ai.free_resources()
        print("AI resources released.")
    else:
        print("No resources to release.")

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-png>")
        sys.exit(1)

    image_dir = sys.argv[1]

    try:
        init_engine()
        png_paths = collect_png_paths(image_dir)
        texts = ocr_batch(png_paths)

        # Optional: write results to a single text file
        output_file = Path("ocr_results.txt")
        with output_file.open("w", encoding="utf-8") as f:
            for path, txt in zip(png_paths, texts):
                f.write(f"--- {path.name} ---\n")
                f.write(txt + "\n\n")
        print(f"All results saved to {output_file.resolve()}")
    finally:
        release_resources()
```

### Résultat attendu

L’exécution du script sur un dossier contenant trois PNG pourrait afficher :

```
Engine already initialized.
Found 3 PNG image(s) to process.
Processed invoice1.png: 452 characters.
Processed receipt2.png: 317 characters.
Processed flyer3.png: 689 characters.
All results saved to /home/user/ocr_results.txt
AI resources released.
```

Le fichier `ocr_results.txt` contiendra un séparateur clair pour chaque image suivi du texte OCR nettoyé.

## Stubs optionnels pour aocr & ai (si vous n’avez pas les vrais paquets)

Si vous voulez simplement tester le flux sans charger de lourdes bibliothèques OCR, vous pouvez créer des modules factices minimalistes :

```python
# aocr/__init__.py
class Image:
    @staticmethod
    def load(path):
        return f"ImageObject({path})"

def dummy_recognize(image):
    return "Raw OCR output for " + str(image)

engine = type("Engine", (), {"recognize": dummy_recognize})()
```

```python
# ai/__init__.py
_state = {"initialized": False}

def is_initialized():
    return _state["initialized"]

def initialize(cfg):
    print(f"Initializing AI engine with {cfg}")
    _state["initialized"] = True

def run_postprocessor(text):
    # Very naive cleanup: strip extra spaces
    return " ".join(text.split())

def free_resources():
    print("Freeing AI resources")
    _state["initialized"] = False
```

Placez ces dossiers à côté de `batch_ocr.py` et le script s’exécutera, affichant des résultats factices.

## Astuces pro & pièges courants

- **Pics de mémoire :** Si vous traitez des milliers de PNG haute résolution, pensez à les redimensionner avant l’OCR. `aocr.Image.load` accepte souvent un argument `max_size`.
- **Gestion Unicode :** Ouvrez toujours le fichier de sortie avec `encoding="utf-8"` ; les moteurs OCR peuvent produire des caractères non‑ASCII.
- **Parallélisme :** Pour un OCR limité par le CPU, vous pouvez envelopper `ocr_batch` dans un `concurrent.futures.ThreadPoolExecutor`. N’oubliez pas de ne garder qu’une seule instance `ai` — créer de nombreux threads qui appellent chacun `ai.initialize` contredit l’objectif « free AI resources ».
- **Résilience aux erreurs :** Enveloppez la boucle par image dans un bloc `try/except` afin qu’un PNG corrompu n’arrête pas tout le traitement.

## Conclusion

Vous disposez maintenant d’un **python ocr tutorial** qui montre comment **load png image** des fichiers, réaliser un **batch OCR processing**, et gérer de façon responsable les **free AI resources**. L’exemple complet et exécutable montre exactement comment **recognize text from image** et nettoyer après, afin que vous puissiez le copier‑coller dans vos propres projets sans chercher des pièces manquantes.

Prêt pour l’étape suivante ? Essayez de remplacer les modules factices `aocr` et `ai` par de vraies bibliothèques comme `pytesseract` et `torchvision`. Vous pouvez également étendre le script pour produire du JSON, pousser les résultats vers une base de données, ou l’intégrer à un bucket de stockage cloud. Le ciel est la limite—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}