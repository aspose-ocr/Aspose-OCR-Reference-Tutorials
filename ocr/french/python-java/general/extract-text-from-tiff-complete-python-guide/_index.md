---
category: general
date: 2026-03-28
description: Extrayez le texte des fichiers TIFF à l'aide d'Aspose OCR en Python.
  Apprenez comment convertir les TIFF en texte rapidement et de manière fiable.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
language: fr
og_description: Extrayez du texte à partir de fichiers TIFF en utilisant Aspose OCR
  en Python. Ce guide montre comment convertir un TIFF en texte étape par étape.
og_title: Extraire du texte d’un TIFF – Guide complet Python
tags:
- OCR
- Python
- Aspose
title: Extraire le texte d’un TIFF – Guide complet Python
url: /fr/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir de TIFF – Guide complet Python

Besoin d'**extraire du texte à partir de TIFF** dans votre projet Python ? Ce guide vous montre comment **convertir TIFF en texte** en utilisant la bibliothèque Aspose OCR, et il le fait d'une manière accessible même aux débutants.  

Si vous avez déjà contemplé un TIFF multi‑pages en vous demandant comment obtenir les mots sans les taper manuellement, vous êtes au bon endroit. Nous parcourrons l’ensemble du processus — de l’installation du package à la gestion des cas particuliers comme les fichiers chiffrés — pour que vous puissiez vous concentrer sur les fonctionnalités qui comptent.

## Ce que vous apprendrez

Dans ce tutoriel vous découvrirez :

* Comment configurer Aspose OCR pour Python.
* Le code exact nécessaire pour lire chaque page d’un TIFF multi‑pages.
* Des méthodes pour gérer les pièges courants tels que les polices manquantes ou les pages corrompues.
* Des astuces pour améliorer la précision et les performances lorsque vous **extrayez du texte à partir de fichiers TIFF** à grande échelle.

À la fin, vous disposerez d’un script prêt à l’emploi qui transforme n’importe quel TIFF en texte brut, prêt à être indexé, recherché ou intégré à des pipelines NLP en aval.

### Prérequis

* Python 3.8 ou plus récent (la bibliothèque supporte 3.7+).
* Une licence Aspose OCR valide — ou vous pouvez commencer avec l’essai gratuit (le code fonctionne en mode évaluation, avec simplement un filigrane sur la sortie).
* Une connaissance de base des environnements virtuels Python (optionnel mais recommandé).

---

## Étape 1 – Installer le package Aspose OCR

Tout d’abord : vous avez besoin du package `aspose-ocr`. Il est hébergé sur PyPI, donc une simple installation avec `pip` suffit.

```bash
pip install aspose-ocr
```

> **Astuce pro :** Utilisez un environnement virtuel (`python -m venv venv`) pour isoler les dépendances. Cela évite les conflits de versions avec d’autres projets que vous pourriez gérer.

> **Pourquoi c’est important :** L’installation du package récupère les binaires natifs du moteur OCR qui effectuent réellement le travail lourd. Sans eux, la méthode `recognize_from_tiff` n’existera pas et vous obtiendrez une `ImportError`.

---

## Étape 2 – Importer la bibliothèque et créer un moteur OCR

Maintenant que la bibliothèque est sur votre machine, importez‑la et créez un `OcrEngine`. Cet objet est le cheval de bataille qui traitera les données d’image.

```python
# Step 2: Import the Aspose OCR library and create an engine instance
import aspose.ocr as aocr

# Initialize the OCR engine – you can optionally pass a license file here
ocr_engine = aocr.OcrEngine()
```

*La classe `OcrEngine` regroupe tous les paramètres OCR, comme la langue, la résolution et les options de prétraitement. Nous ajusterons quelques‑unes de ces options plus tard pour améliorer la précision.*

---

## Étape 3 – Pointer vers votre fichier TIFF multi‑pages

Vous avez besoin du chemin vers le TIFF que vous souhaitez lire. La bibliothèque accepte les chemins absolus ou relatifs, mais les chemins absolus évitent les surprises lorsque le script s’exécute depuis un répertoire de travail différent.

```python
# Step 3: Define the path to the TIFF file
tiff_file_path = "YOUR_DIRECTORY/input.tif"
```

> **Erreur fréquente :** Oublier d’échapper les barres obliques inverses sous Windows (`C:\\Images\\file.tif`). Utiliser des chaînes brutes (`r"C:\Images\file.tif"`) ou des barres obliques normales évite ce problème.

---

## Étape 4 – Reconnaître le texte de toutes les pages

Voici le cœur du tutoriel : appeler `recognize_from_tiff`. La méthode renvoie une liste d’objets `OcrResult` — un pour chaque page — vous permettant de les parcourir individuellement.

```python
# Step 4: Extract text from every page of the TIFF
ocr_pages = ocr_engine.recognize_from_tiff(tiff_file_path)

# Verify we got results
if not ocr_pages:
    raise RuntimeError("No pages were recognized. Check the file path and format.")
```

**Pourquoi cela fonctionne :** Aspose OCR découpe en interne le TIFF en ses cadres constituants, exécute le moteur OCR sur chacun, puis regroupe les résultats. C’est bien plus fiable que d’essayer de séparer manuellement les pages avec Pillow ou ImageMagick.

---

## Étape 5 – Parcourir les résultats et afficher le texte

Enfin, bouclez sur la liste `OcrResult` et imprimez (ou sauvegardez) le texte extrait. Vous pouvez également écrire chaque page dans son propre fichier `.txt` si cela correspond à votre flux de travail.

```python
# Step 5: Print or save the extracted text
for page_index, page_result in enumerate(ocr_pages):
    print(f"--- TIFF Page {page_index + 1} ---")
    print(page_result.text)
    # Optional: write each page to a separate file
    with open(f"page_{page_index + 1}.txt", "w", encoding="utf-8") as f:
        f.write(page_result.text)
```

**Sortie attendue** (troncature pour la brièveté) :

```
--- TIFF Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- TIFF Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
```

> **Gestion des cas limites :** Si une page ne contient aucun texte reconnaissable, `page_result.text` sera une chaîne vide. Vous voudrez peut‑être consigner ces pages pour une révision manuelle ultérieure.

---

## Bonus – Ajuster les paramètres OCR pour une meilleure précision

Parfois la configuration par défaut ne suffit pas, surtout avec des scans basse résolution ou des polices inhabituelles. Voici quelques paramètres que vous pouvez modifier :

```python
# Set language (default is English)
ocr_engine.language = aocr.Language.English

# Increase image resolution before OCR (helps with blurry scans)
ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
    sharpen=True,
    contrast=1.2
)

# Enable deskew to straighten rotated pages
ocr_engine.deskew = True
```

*Ces options sont facultatives, mais elles font souvent la différence entre une sortie illisible et une transcription propre et recherchable.*

---

## Pièges courants & comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Sortie vide pour toutes les pages | Chemin de fichier incorrect ou compression TIFF non prise en charge | Vérifiez le chemin, assurez‑vous que le TIFF utilise une compression prise en charge (par ex., LZW, PackBits). |
| Caractères corrompus (p. ex., �) | Paramètre de langue incorrect ou fichiers de polices manquants | Définissez `ocr_engine.language` sur la locale correcte ; installez les polices requises sur le système hôte. |
| Traitement lent sur de gros TIFF | Mode mono‑thread par défaut | Utilisez `ocr_engine.recognize_from_tiff(..., parallel=True)` si la version de la bibliothèque le supporte. |
| Avertissement de licence | Utilisation de l'essai sans fichier de licence | Fournissez une clé de licence via `aocr.License().set_license("Aspose.OCR.lic")`. |

---

## Script complet – Prêt à l'exécution

Voici le script complet, autonome, qui intègre toutes les étapes et les ajustements optionnels évoqués ci‑dessus. Copiez‑collez‑le dans un fichier nommé `extract_tiff_text.py` et lancez `python extract_tiff_text.py`.

```python
#!/usr/bin/env python3
"""
extract_tiff_text.py

A complete example that extracts text from a multi‑page TIFF using Aspose OCR.
It demonstrates how to:
- Install and import the library
- Initialize the OCR engine
- Configure optional preprocessing
- Iterate over each page and save the results

Author: Your Name
Date: 2026‑03‑28
"""

import aspose.ocr as aocr
import os
import sys

def main(tiff_path: str, output_dir: str = "output"):
    # Ensure output directory exists
    os.makedirs(output_dir, exist_ok=True)

    # Initialize the OCR engine
    ocr_engine = aocr.OcrEngine()

    # Optional: fine‑tune OCR settings for better accuracy
    ocr_engine.language = aocr.Language.English
    ocr_engine.image_preprocessing = aocr.ImagePreprocessingOptions(
        sharpen=True,
        contrast=1.2
    )
    ocr_engine.deskew = True

    # Perform OCR on the TIFF
    try:
        ocr_pages = ocr_engine.recognize_from_tiff(tiff_path)
    except Exception as e:
        sys.exit(f"Failed to process {tiff_path}: {e}")

    if not ocr_pages:
        sys.exit("No pages were recognized. Check the file path and format.")

    # Iterate over results
    for idx, result in enumerate(ocr_pages, start=1):
        page_text = result.text or "[No recognizable text]"
        print(f"--- TIFF Page {idx} ---")
        print(page_text[:200] + ("..." if len(page_text) > 200 else ""))  # preview

        # Save each page's text
        out_file = os.path.join(output_dir, f"page_{idx}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

    print(f"\nAll pages processed. Text files saved in '{output_dir}'.")

if __name__ == "__main__":
    if len(sys.argv) < 2:
        sys.exit("Usage: python extract_tiff_text.py <path_to_tiff>")
    tiff_file = sys.argv[1]
    main(tiff_file)
```

**Exécution du script**

```bash
python extract_tiff_text.py /path/to/your/input.tif
```

Vous verrez un aperçu console de chaque page et un dossier `output` contenant `page_1.txt`, `page_2.txt`, etc.

---

## Conclusion

Nous venons de couvrir tout ce dont vous avez besoin pour **extraire du texte à partir de fichiers TIFF** avec Python et Aspose OCR. De l’installation du package à la gestion des documents multi‑pages, en passant par l’ajustement des paramètres pour la précision et la sauvegarde des résultats, l’ensemble du flux de travail est désormais à votre portée.  

Si vous envisagez de **convertir TIFF en texte** dans une chaîne de production, pensez à regrouper les fichiers, paralléliser les appels OCR et stocker la sortie dans un index searchable comme Elasticsearch. Pour les curieux, expérimentez d’autres langues (`aocr.Language.Spanish`) ou alimentez les résultats bruts d’OCR dans une bibliothèque de correction orthographique pour nettoyer le bruit OCR.

Des questions sur la mise à l’échelle, la licence ou l’intégration avec le stockage cloud ? Laissez un commentaire ci‑dessous, et bon codage ! 

---

![Diagramme montrant le flux OCR du fichier TIFF au texte extrait](https://example.com/placeholder-image.png "Extraire du texte à partir de TIFF avec Python")

*Texte alternatif de l’image : Diagramme montrant le flux OCR du fichier TIFF au texte extrait*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}