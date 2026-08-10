---
category: general
date: 2026-06-28
description: Comment effectuer une OCR par lots en Python — extraire du texte d'images
  et convertir des pages numérisées en texte grâce au traitement OCR par lots.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: fr
og_description: Apprenez à effectuer la reconnaissance optique de caractères en lot
  avec Python, à extraire du texte à partir d’images et à convertir des pages numérisées
  en texte grâce à un traitement OCR par lots efficace.
og_title: Comment réaliser une OCR par lots en Python – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Comment faire de l'OCR par lots en Python – Guide complet pour extraire du
  texte à partir d'images
url: /fr/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire du OCR par lots en Python – Guide complet pour extraire du texte d'images

Si vous vous demandez **comment faire du OCR par lots en Python**, vous êtes au bon endroit. Ce tutoriel vous montre une méthode rapide pour **extraire du texte d'images** et **convertir des pages numérisées en texte** en utilisant une seule instance du moteur OCR. Fini le copier‑coller d'un fichier après l'autre—laissez le code faire le travail lourd.

Nous passerons en revue tout ce dont vous avez besoin : installer la bibliothèque, charger un dossier complet de scans, exécuter le traitement OCR par lots et gérer les résultats avec élégance. À la fin, vous disposerez d'un script réutilisable qui transforme une pile de PNG ou JPEG en fichiers texte consultables en quelques secondes.

## Ce dont vous avez besoin

* Python 3.9+ installé (le code fonctionne également avec la 3.8, mais 3.9+ vous donne les dernières fonctionnalités de typage).
* Une bibliothèque OCR moderne—ici nous utilisons **Aspose.OCR for Python via .NET**, qui expose la classe `OcrEngine` présentée dans l'extrait original.  
  ```bash
  pip install aspose-ocr
  ```
* Un dossier contenant des pages numérisées (`page1.png`, `page2.png`, …). Tout ce que Pillow peut ouvrir fonctionnera, donc les PDF, TIFF ou BMP sont également acceptés.
* Un petit brin de curiosité—si vous n'avez jamais automatisé la conversion image‑vers‑texte auparavant, vous allez découvrir pourquoi le OCR par lots est une révolution.

> **Astuce :** Si vous préférez une bibliothèque pure‑Python, remplacez `OcrEngine` par `pytesseract.image_to_string`. La logique environnante reste identique.

## Comment faire du OCR par lots en Python – Guide étape par étape

Voici le script complet et exécutable. Chaque ligne est commentée afin que vous puissiez voir *pourquoi* chaque élément est important, pas seulement *ce que* cela fait.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Résultat attendu

Exécuter le script sur un dossier contenant trois scans PNG produit quelque chose comme :

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

L'aperçu montre les 200 premiers caractères de chaque page, et le texte complet se trouve dans le répertoire `ocr_output`.

## Extraire du texte d'images en utilisant un seul moteur

Pourquoi créons‑nous **un** `OcrEngine` et le réutilisons‑nous ? Instancier le moteur peut être coûteux car il charge des packs de langues et des DLL natives. En partageant la même instance pour le lot, vous :

* **Économiser de la mémoire** – un seul ensemble de ressources réside en RAM.
* **Accélérer la vitesse** – le moteur reste chaud, évitant les ré‑initialisations répétées.
* **Maintenir la cohérence** – les mêmes paramètres de reconnaissance s'appliquent à chaque page, ce qui est essentiel lorsque vous souhaitez **extraire du texte d'images** partageant la même mise en page.

Si vous devez ajuster la reconnaissance (par ex., activer la vérification orthographique ou changer la langue), faites‑le *avant* d'appeler `recognize_batch`. Toutes les pages suivantes hériteront automatiquement de ces paramètres.

## Convertir efficacement des pages numérisées en texte

Le cœur du problème—**convertir des pages numérisées en texte**—est résolu par `engine.recognize_batch(images)`. En interne, la bibliothèque traite chaque image dans un pool de threads en arrière‑plan, ce qui vous donne une mise à l'échelle quasi‑linéaire sur les machines multi‑cœurs. Quelques points à garder à l'esprit :

* **La qualité de l'image compte** – 300 dpi ou plus donne les meilleurs résultats. Si vos scans sont de basse résolution, envisagez un sur‑échantillonnage avec Pillow avant de les fournir au moteur.
* **Couleur vs. niveaux de gris** – les moteurs OCR fonctionnent généralement plus rapidement sur du gris 8 bits. Vous pouvez ajouter une étape de prétraitement :
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Support des langues** – Aspose.OCR prend en charge plus de 40 langues. Définissez `engine.language = "eng"` ou ` "fra"` avant l'appel du lot si vous ne travaillez pas en anglais.

## Bonnes pratiques pour le traitement OCR par lots

Même si le code ci‑dessus est déjà concis, le OCR par lots de niveau production nécessite souvent quelques mesures de sécurité supplémentaires :

| Problème | Approche recommandée |
|----------|----------------------|
| **Lots de fichiers volumineux ( > 500 fichiers )** | Divisez en lots de 100–200 images pour garder une empreinte mémoire modeste. |
| **Fichiers corrompus ou non pris en charge** | L'utilitaire `load_images` capture déjà les exceptions et consigne un avertissement ; vous pouvez également écrire un secours pour ignorer ou déplacer les fichiers défectueux. |
| **Suivi de progression** | Enveloppez `recognize_batch` dans une boucle qui rend après chaque image si la bibliothèque expose des callbacks par image. |
| **Post‑traitement** | Exécutez une vérification orthographique ou un nettoyage regex sur les chaînes résultantes pour améliorer la recherchabilité en aval. |
| **Parallélisme** | Si vous avez une configuration multi‑nœuds, répartissez les dossiers entre les travailleurs et fusionnez les sorties `.txt` à la fin. |

Ces conseils vous aident à faire évoluer le **traitement OCR par lots** d'une poignée de pages à des milliers sans faire planter votre script.

## Questions fréquentes

**Q : Puis‑je utiliser cela directement avec des PDF ?**  
R : Absolument. Convertissez chaque page PDF en image d'abord (par ex., avec `pdf2image`) et transmettez la liste résultante à `recognize_batch`. Le reste du pipeline reste inchangé

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraire du texte d'images en utilisant l'opération OCR sur des dossiers](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Comment extraire du texte d'archives ZIP en utilisant Aspose.OCR pour .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}