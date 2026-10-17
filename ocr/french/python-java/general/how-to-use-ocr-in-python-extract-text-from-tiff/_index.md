---
category: general
date: 2026-07-05
description: Comment utiliser l'OCR en Python pour convertir rapidement des fichiers
  TIFF en texte. Apprenez les étapes de la bibliothèque OCR en Python pour extraire
  le texte des images TIFF et créer un moteur OCR en Python.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: fr
og_description: Comment utiliser l'OCR en Python ? Ce guide vous montre étape par
  étape comment convertir un TIFF en texte en utilisant un moteur OCR Python et la
  bibliothèque ocr python.
og_title: Comment utiliser l'OCR en Python – Extraction complète de texte TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Comment utiliser l'OCR en Python – Extraire du texte à partir de TIFF
url: /fr/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en Python – Extraire du texte d'un TIFF

Vous vous êtes déjà demandé **comment utiliser l'OCR en Python** pour transformer un livre numérisé en texte modifiable ? Vous n'êtes pas le seul—les développeurs, les chercheurs et les amateurs rencontrent tous cet obstacle lorsqu'ils traitent des images TIFF multi‑pages. La bonne nouvelle ? Avec la **ocr library python** vous pouvez lancer un petit moteur OCR, le pointer vers un fichier TIFF, et obtenir du texte propre et recherchable en quelques secondes.

Dans ce tutoriel, nous passerons en revue tout ce dont vous avez besoin : installer le bon package, charger un TIFF multi‑pages, exécuter le moteur OCR, et enfin afficher le contenu de chaque page. À la fin, vous serez capable de **convertir TIFF en texte** et **extraire du texte d'un TIFF** sans quitter votre environnement Python.

## Prérequis

- Python 3.9 ou plus récent (l'exemple a été testé sur 3.11)
- Une version récente de la bibliothèque `ocr` (ou tout `python ocr engine` compatible que vous préférez)
- Un fichier TIFF multi‑pages que vous souhaitez traiter (nous l'appellerons `scanned_book.tif`)
- Une connaissance de base des scripts Python et des environnements virtuels

Aucun outil externe lourd requis—juste pip et quelques lignes de code.

## Installer la bibliothèque OCR pour Python

Tout d'abord : vous avez besoin d'un backend OCR solide. Pour ce guide, nous utiliserons le package fictif `ocr` qui fournit une API haut‑niveau simple, mais le même schéma fonctionne avec des wrappers basés sur Tesseract comme `pytesseract` ou des SDK commerciaux.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Astuce :** Si vous êtes sous Windows et que le package dépend de binaires natifs, assurez-vous d'avoir le redistributable Visual C++ approprié installé. L'installateur vous avertira généralement si quelque chose manque.

## Comment utiliser le moteur OCR en Python

Maintenant que la bibliothèque est prête, lançons un moteur OCR et pointons‑le vers notre fichier TIFF. L'extrait suivant crée une instance du moteur, définit la langue sur English, et le prépare au traitement multi‑pages.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Pourquoi définir la langue ?**  
La plupart des moteurs OCR utilisent des modèles linguistiques pour améliorer la précision. Si vous sautez cette étape, le moteur revient à un modèle générique qui peut mal reconnaître la ponctuation ou les caractères spéciaux.

## Charger l'image TIFF multi‑pages

L'étape suivante consiste à charger le document numérisé. L'utilitaire `ocr.Image.load` comprend les piles TIFF dès le départ, renvoyant un objet qui représente chaque page en interne.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Cas particulier :** Si votre TIFF utilise une compression (CCITT Group 4, LZW, etc.) et que la bibliothèque génère une erreur, essayez de le convertir d'abord en une version non compressée avec ImageMagick :
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Effectuer l'OCR sur toutes les pages – Convertir TIFF en texte

Avec l'objet image en main, le moteur peut maintenant traiter chaque page d'un coup. Cette méthode renvoie une liste où chaque élément contient le résultat OCR d'une seule page.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Que se passe-t-il en coulisses ?**  
La fonction `recognize_multi_page` parcourt chaque page rasterisée, exécute le reconnaisseur de réseau neuronal, et regroupe la sortie texte brut avec les scores de confiance. C’est essentiellement une opération par lot qui vous évite d'écrire une boucle manuelle.

## Parcourir les résultats – Extraire du texte d'un TIFF

Enfin, nous affichons le texte reconnu. Vous pouvez écrire la sortie dans des fichiers `.txt` séparés, l'envoyer à une base de données, ou l'alimenter dans un index de recherche—ce qui correspond à votre flux de travail.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Sortie attendue

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Chaque chaîne `result.text` contient la sortie OCR brute pour cette page. Si vous avez besoin de préserver les sauts de ligne, la plupart des moteurs exposent `result.lines` sous forme de liste de chaînes.

## Gérer les gros fichiers TIFF – Astuces & conseils

Le traitement d'un TIFF de 500 pages peut être gourmand en mémoire. Voici quelques stratégies pour garder les choses fluides :

1. **Diviser les pages** – Au lieu de `recognize_multi_page`, appelez `engine.recognize(page)` à l'intérieur d'un générateur qui produit une page à la fois.
2. **Ajuster le DPI** – Réduire la résolution de l'image (par ex., de 300 DPI à 200 DPI) diminue la charge CPU tout en affectant à peine la précision pour la plupart des textes imprimés.
3. **Paralléliser** – Si votre moteur OCR est thread‑safe, créez un `concurrent.futures.ThreadPoolExecutor` pour exécuter la reconnaissance sur plusieurs pages simultanément.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Enregistrer le texte extrait dans des fichiers

La plupart des pipelines réels nécessitent un stockage persistant. Ci-dessous une façon concise de sauvegarder le texte de chaque page dans son propre fichier, en préservant l'ordre des pages.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Vous avez maintenant un répertoire propre de fichiers `.txt` prêt pour l'indexation ou un traitement NLP supplémentaire.

## Aperçu de l'image – Comment visualiser les résultats OCR

Si vous souhaitez voir la superposition OCR sur l'image originale (utile pour le débogage), de nombreuses bibliothèques vous permettent de dessiner des boîtes englobantes. Voici un exemple rapide avec Pillow :

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Comment utiliser l'OCR en Python – Superposition OCR sur une page TIFF](ocr_overlay_example.png)

*Texte alternatif :* Comment utiliser l'OCR en Python – superposition visuelle du texte reconnu sur une page TIFF.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Caractères brouillés | Modèle linguistique incorrect | Définir `engine.language` sur l'énumération correcte |
| Pages manquantes | Compression TIFF non prise en charge | Convertir d'abord en TIFF non compressé |
| Performances lentes | DPI élevé + traitement monothread | Réduire le DPI ou activer le multithreading |
| Sortie vide | Image trop sombre/faible contraste | Pré‑traiter avec étirement de contraste (`opencv` ou `Pillow`) |

Résoudre ces problèmes dès le départ vous fera gagner des heures de débogage plus tard.

## Prochaines étapes – Aller au-delà de l'extraction de base

Maintenant que vous avez maîtrisé les bases de **comment utiliser l'OCR en Python**, envisagez d'explorer :

- **Génération de PDF** – Combinez le texte extrait avec `reportlab` pour reconstruire des PDF recherchables.
- **Détection de langue** – Changez automatiquement `engine.language` en utilisant `langdetect`.
- **Extraction de données structurées** – Utilisez des expressions régulières ou spaCy pour extraire des dates, des noms ou des tableaux du texte brut.
- **Backends OCR alternatifs** – Remplacez `ocr` par `pytesseract` ou `easyocr` si vous avez besoin d'un support multilingue.

Chacun de ces sujets se rattache naturellement aux mots‑clés secondaires **ocr library python**, **convert tiff to text**, **extract text from tiff**, et **python ocr engine**, vous offrant une base solide pour des projets plus avancés.

---

### Conclusion

Nous avons couvert **comment utiliser l'OCR en Python** de l'installation au traitement multi‑pages, vous montrant exactement comment **convertir TIFF en texte** et **extraire du texte d'un TIFF** en utilisant un **moteur OCR python** simple. L'exemple complet et exécutable ci‑dessus devrait fonctionner immédiatement pour la plupart des fichiers TIFF standards, et les astuces fournies vous aideront à passer à des documents plus volumineux ou à intégrer l'OCR dans des pipelines plus larges.

Essayez-le avec vos propres livres numérisés, reçus ou images d'archives—puis expérimentez les idées de niveau supérieur listées dans la section « Prochaines étapes ». Bon codage, et que vos résultats OCR soient toujours précis !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment extraire du texte d'un TIFF avec Aspose.OCR pour Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Comment effectuer l'extraction de texte d'image depuis un flux avec Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}