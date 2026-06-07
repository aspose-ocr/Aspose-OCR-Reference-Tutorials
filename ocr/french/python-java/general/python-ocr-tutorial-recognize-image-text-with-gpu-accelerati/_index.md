---
category: general
date: 2026-06-06
description: Tutoriel OCR en Python montrant comment reconnaître le texte d’une image,
  réaliser une OCR haute résolution et extraire du texte espagnol à l’aide d’une OCR
  accélérée par GPU.
draft: false
keywords:
- python ocr tutorial
- recognize image text
- high resolution ocr
- gpu accelerated ocr
- extract spanish text
language: fr
og_description: Tutoriel Python OCR qui vous guide à travers la reconnaissance de
  texte d'image, l'OCR haute résolution et l'extraction de texte espagnol avec accélération
  GPU.
og_title: Tutoriel OCR Python – Reconnaissance de texte accélérée par GPU
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  headline: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  type: TechArticle
- description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  name: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  steps:
  - name: Prerequisites
    text: '- Python 3.9+ (the code works on 3.10 and newer as well). - A CUDA‑compatible
      GPU (optional but highly recommended). - Basic familiarity with pip and virtual
      environments.'
  - name: 6.1 Fallback When No GPU Is Present
    text: "```python if not torch.cuda.is_available(): # Re‑initialize the reader
      without GPU to avoid hidden errors reader = Reader(lang_list=[\"es\"], gpu=False)
      print(\"\U0001F504 Re‑initialized reader for CPU execution.\") ```"
  - name: 6.2 Down‑sampling Very Large Images
    text: 'If your image is larger than 4000 × 4000 px, you might run out of GPU memory.
      Down‑sample proportionally while preserving DPI:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- GPU
- Spanish
title: Tutoriel OCR Python – Reconnaître le texte d'image avec accélération GPU
url: /fr/python-java/general/python-ocr-tutorial-recognize-image-text-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutoriel OCR Python – Reconnaître le texte d’une image avec accélération GPU

Vous êtes-vous déjà demandé comment **reconnaître le texte d’une image** dans un script Python sans passer des heures à ajuster les paramètres ? Vous n’êtes pas seul. Dans ce **tutoriel OCR python** nous allons vous montrer une méthode propre, de bout en bout, pour extraire du texte espagnol d’une image haute résolution, et nous y ajouterons l’accélération GPU afin que le processus soit ultra‑rapide.

Considérez cela comme une petite démonstration à la pause café que vous pourrez développer plus tard en un pipeline de production. À la fin de ce guide, vous disposerez d’un programme exécutable qui effectue de **l’OCR haute résolution**, exploite un GPU compatible CUDA, et renvoie exactement les caractères espagnols dont vous avez besoin.

## Ce que vous allez apprendre

- Comment installer et importer une bibliothèque OCR moderne qui supporte l’accélération GPU.  
- Comment créer une instance du moteur OCR et la configurer pour **reconnaître le texte d’une image** en espagnol.  
- Comment activer **l’OCR accéléré par GPU** pour obtenir des gains de vitesse massifs sur des fichiers haute résolution.  
- Comment gérer les cas limites tels que l’absence de pilotes CUDA ou le basculement vers le CPU.  
- Astuces pour améliorer la précision lorsque vous devez **extraire du texte espagnol** à partir de scans bruyants.

### Prérequis

- Python 3.9+ (le code fonctionne également sur 3.10 et versions supérieures).  
- Un GPU compatible CUDA (optionnel mais fortement recommandé).  
- Familiarité de base avec pip et les environnements virtuels.  

Si l’un de ces éléments vous manque, le tutoriel fonctionne toujours — il suffit de sauter l’étape GPU et la bibliothèque reviendra automatiquement au CPU.

---

## Tutoriel OCR Python : Installation des paquets requis

Tout d’abord, il nous faut un moteur OCR fiable. Pour ce tutoriel, nous utiliserons le package open‑source **`easyocr`**, qui intègre le support GPU dès qu’un dispositif compatible est détecté.

```bash
# Create a fresh virtual environment (optional but tidy)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows use `ocr-env\Scripts\activate`

# Install EasyOCR and its optional torch dependencies
pip install easyocr[torch]   # Installs both CPU and GPU builds of PyTorch
```

> **Astuce :** Si vous avez déjà installé PyTorch, assurez‑vous qu’il correspond à votre version CUDA (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`). Des versions incompatibles sont une cause fréquente d’erreurs « GPU non trouvé ».

---

## Étape 1 : Créer une instance du moteur OCR

Nous lançons maintenant le moteur. EasyOCR appelle sa classe principale `Reader`. Le constructeur accepte une liste de codes de langue ; nous passerons `"es"` pour l’espagnol.

```python
# Step 1: Initialize the OCR reader for Spanish
from easyocr import Reader

# The `gpu` flag tells EasyOCR to try using CUDA if it’s available.
reader = Reader(lang_list=["es"], gpu=True)
```

*Pourquoi c’est important :* En déclarant la langue dès le départ, le moteur ne charge que les poids de réseau neuronal nécessaires, ce qui économise de la mémoire et accélère l’inférence — particulièrement utile lorsque vous traitez de **l’OCR haute résolution** plus tard.

---

## Étape 2 : Préparer une image haute résolution

Les images haute résolution offrent au modèle davantage de pixels, ce qui se traduit généralement par une meilleure reconnaissance des caractères. Supposons que vous disposiez d’un fichier nommé `high_res_spanish.png` placé dans un dossier appelé `samples`.

```python
import os

# Construct an absolute path – keeps the script portable
image_path = os.path.join("samples", "high_res_spanish.png")

# Quick sanity check – raise a clear error if the file is missing
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")
```

Si vous n’avez pas d’échantillon haute résolution sous la main, vous pouvez en télécharger un gratuitement sur Unsplash ou générer une image synthétique avec Pillow. L’important est de garder le DPI au‑dessus de 300 pour obtenir les meilleurs résultats.

---

## Étape 3 : Activer l’accélération GPU (Optionnel mais recommandé)

EasyOCR tente déjà d’utiliser le GPU dès que vous définissez `gpu=True`. Cependant, il est judicieux de vérifier que le dispositif est réellement utilisé, surtout sur des stations à plusieurs GPU.

```python
import torch

# Verify CUDA availability – helpful for debugging
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device found – falling back to CPU. Performance will be slower.")
```

*Pourquoi vérifier ?* Si le script bascule silencieusement vers le CPU, vous vous demanderez pourquoi une opération de 5 secondes prend soudainement 30 secondes. Cette petite vérification rend le comportement transparent et maintient votre pipeline **OCR accéléré par GPU** prévisible.

---

## Étape 4 : Effectuer l’OCR haute résolution et reconnaître le texte d’image

Place maintenant la partie amusante — la lecture du texte. La méthode `readtext` d’EasyOCR renvoie une liste de tuples contenant la boîte englobante, la chaîne reconnue et un score de confiance.

```python
# Step 4: Run OCR on the high‑resolution image
results = reader.readtext(image_path, detail=1, paragraph=False)

# `results` looks like:
# [
#   ([(x1, y1), (x2, y2), (x3, y3), (x4, y4)], 'Texto reconocido', 0.98),
#   ...
# ]
```

Si vous avez besoin de la chaîne brute sans coordonnées, définissez `detail=0`. Pour la plupart des cas d’utilisation de **reconnaître le texte d’image**, la valeur par défaut (`detail=1`) vous fournit suffisamment de contexte pour un post‑traitement ultérieur.

---

## Étape 5 : Extraire le texte espagnol et nettoyer la sortie

Comme nous avons demandé à EasyOCR de travailler en espagnol, les chaînes retournées le sont déjà. Vous pouvez néanmoins les concaténer, supprimer les espaces superflus ou filtrer les détections à faible confiance.

```python
# Step 5: Consolidate high‑confidence Spanish strings
extracted_text = []
for bbox, text, conf in results:
    if conf > 0.85:                # Drop anything below 85 % confidence
        extracted_text.append(text)

# Join everything into a single block – perfect for further NLP tasks
final_text = "\n".join(extracted_text)

print("📝 Extracted Spanish text:")
print(final_text)
```

**Et si la confiance est basse ?** Vous pouvez soit abaisser le seuil (au risque d’introduire du bruit) soit pré‑traiter l’image (augmenter le contraste, binariser ou redresser). Ces astuces sont courantes lorsqu’on traite de **l’OCR haute résolution** sur des documents numérisés.

---

## Étape 6 : Gestion des cas limites et ajustements de performance

Même les modèles les mieux entraînés rencontrent quelques scénarios difficiles. Voici deux correctifs rapides que vous pouvez coller dans votre script.

### 6.1 Basculement lorsqu’aucun GPU n’est présent

```python
if not torch.cuda.is_available():
    # Re‑initialize the reader without GPU to avoid hidden errors
    reader = Reader(lang_list=["es"], gpu=False)
    print("🔄 Re‑initialized reader for CPU execution.")
```

### 6.2 Réduction d’échantillonnage d’images très grandes

Si votre image dépasse 4000 × 4000 px, vous risquez d’épuiser la mémoire du GPU. Réduisez‑la proportionnellement tout en conservant le DPI :

```python
from PIL import Image

def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path

image_path = resize_if_needed(image_path)
```

Ces extraits rendent le script robuste, que vous l’exécutiez sur une station de travail ou sur un ordinateur portable modeste.

---

## Exemple complet fonctionnel

En rassemblant tous les morceaux, voici le script complet que vous pouvez copier‑coller et exécuter immédiatement :

```python
# python_ocr_tutorial.py
import os
import torch
from PIL import Image
from easyocr import Reader

# ----------------------------------------------------------------------
# Helper: Resize very large images to avoid GPU OOM errors
def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path
# ----------------------------------------------------------------------

# 1️⃣ Verify CUDA availability (optional)
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device – using CPU (expect slower performance).")

# 2️⃣ Initialize the OCR engine for Spanish (GPU if possible)
reader = Reader(lang_list=["es"], gpu=torch.cuda.is_available())

# 3️⃣ Path to the high‑resolution image
image_path = os.path.join("samples", "high_res_spanish.png")
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")

# 4️⃣ Resize if the image is gigantic
image_path = resize_if_needed(image_path)

# 5️⃣ Run OCR – this is the core **recognize image text** step
results = reader.readtext(image_path, detail=1, paragraph=False)

# 6️⃣ Filter and concatenate high‑confidence Spanish strings
extracted = []
for bbox, txt, conf in results:
    if conf > 0.85:
        extracted.append(txt)

final_text = "\n".join(extracted)

# 7️⃣ Output the result – **extract spanish text** ready for downstream processing
print("\n📝 Extracted Spanish text:")
print(final_text)
```

**Sortie attendue (exemple) :**



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte d’une image avec Aspose OCR – Guide pas à pas](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment faire de l’OCR de texte d’image avec langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Comment reconnaître les rectangles de page pour la reconnaissance de texte OCR dans Aspose.OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}