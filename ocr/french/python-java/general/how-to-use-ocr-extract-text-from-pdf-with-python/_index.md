---
category: general
date: 2026-04-26
description: Comment utiliser l’OCR sur des PDF numérisés, extraire le texte d’un
  PDF, exécuter l’OCR sur un PDF et convertir un PDF numérisé en fichiers consultables
  en quelques étapes.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: fr
og_description: 'Comment utiliser l''OCR en Python : apprenez à extraire du texte
  d’un PDF, à exécuter l’OCR sur un PDF et à convertir un PDF numérisé en documents
  consultables.'
og_title: Comment utiliser l'OCR – Guide rapide pour extraire du texte d'un PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Comment utiliser l'OCR – Extraire du texte d'un PDF avec Python
url: /fr/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment utiliser l'OCR – Extraire du texte d'un PDF avec Python

Vous vous êtes déjà demandé **comment utiliser l'OCR** pour extraire du texte d'un contrat, d'un reçu ou d'un ebook numérisé ? Vous n'êtes pas seul. Dans de nombreux projets réels, le PDF que vous recevez n'est qu'une image, et sans OCR vous ne pouvez pas rechercher, indexer ou analyser son contenu.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre **comment utiliser l'OCR**, comment **extraire du texte d'un PDF**, et pourquoi vous pourriez vouloir **convertir un PDF numérisé** en documents recherchables. Nous aborderons également l'art subtil de **charger un PDF en image** afin que le moteur OCR puisse voir chaque page clairement.

> **Aperçu rapide :** À la fin, vous disposerez d'un script qui charge un PDF multi‑pages, exécute l'OCR sur chaque page et affiche le texte reconnu – aucun service externe requis.

## Ce dont vous avez besoin

- Python 3.9+ (toute version récente fonctionne)
- `aocr` package (ou toute bibliothèque OCR compatible qui fournit `OcrEngine` et `Image.load`)
- Un fichier PDF numérisé que vous souhaitez traiter (par ex., `contract.pdf`)
- Une quantité modeste de RAM (≈ 200 Mo par PDF de 100 pages, généralement suffisant)

Si vous n'avez pas encore installé la bibliothèque OCR, exécutez :

```bash
pip install aocr
```

> **Astuce pro :** Utilisez un environnement virtuel pour garder vos dépendances propres.

## Étape 1 : Charger le PDF en image – La première pièce du puzzle

Avant que l'OCR puisse s'exécuter, le PDF doit être représenté sous forme d'image. C'est ici que le mot‑clé secondaire **load pdf as image** entre en jeu.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Pourquoi c'est important :* `aocr.Image.load` rasterise en interne chaque page du PDF en un bitmap que le moteur OCR peut comprendre. Si vous sautez cette étape et fournissez le PDF brut, le moteur lèvera une erreur car il attend des données de pixels, pas des données vectorielles.

> **Note :** Le chemin peut être absolu ou relatif. Assurez‑vous que le fichier est lisible ; sinon vous rencontrerez une `FileNotFoundError`.

## Étape 2 : Exécuter l'OCR sur le PDF – Transformer les pixels en caractères

Maintenant que le PDF est sous forme d'image, nous pouvons enfin **exécuter l'OCR sur le PDF**. Le fragment suivant traite chaque page d'un seul coup :

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Que se passe-t-il en coulisses ?* `process_all_pages` parcourt les pages rasterisées, applique le modèle OCR et renvoie une liste d'objets résultat—un par page. Chaque résultat contient le texte reconnu, les scores de confiance et les boîtes englobantes (si vous en avez besoin plus tard).

## Étape 3 : Extraire le texte du PDF – Tirer les chaînes

Avec les résultats OCR en main, extraire le texte brut devient trivial. Nous parcourrons les pages et afficherons la sortie, démontrant le mot‑clé secondaire **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Sortie attendue** (troncée pour plus de concision) :

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Si vous avez besoin du texte dans une seule chaîne, concaténez simplement :

```python
full_text = "\n".join(r.text for r in page_results)
```

Vous avez maintenant réussi à **extraire le texte d'un PDF** en utilisant l'OCR.

## Étape 4 : Convertir le PDF numérisé – Le rendre recherchable

De nombreux outils en aval (comme Elasticsearch ou SharePoint) attendent un PDF recherchable plutôt qu'un simple dump de texte. Vous pouvez intégrer la sortie OCR dans le PDF original, convertissant ainsi efficacement le **PDF numérisé** en une version recherchable.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Pourquoi s'en soucier ?* Un PDF recherchable conserve la mise en page et les images originales tout en permettant la sélection et l'indexation du texte — une situation gagnant‑gagnant pour les humains et les machines.

## Pièges courants & cas limites

### PDFs multi‑pages trop volumineux pour la mémoire

Si votre PDF comporte des centaines de pages, le charger en une fois peut épuiser la RAM. La bibliothèque `aocr` prend en charge le chargement paresseux :

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Puis traitez les pages une par une :

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Scans de mauvaise qualité

La précision de l'OCR chute drastiquement sur des scans flous ou à faible contraste. Avant d'alimenter l'image dans le moteur, envisagez un prétraitement :

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Support linguistique

Par défaut, le moteur suppose l'anglais. Pour **exécuter l'OCR sur le PDF** dans une autre langue, définissez le code de langue :

```python
ocr_engine.language = "spa"  # Spanish
```

Assurez‑vous que le modèle linguistique correspondant est installé.

## Exemple complet fonctionnel

En rassemblant tout, voici un script autonome que vous pouvez placer dans un fichier nommé `ocr_pdf.py` et exécuter immédiatement :

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Exécutez‑le ainsi :

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Vous verrez le texte affiché dans la console, et si vous avez fourni `-o`, un PDF recherchable apparaîtra à côté du fichier original.

## Astuces pro & bonnes pratiques

- **Traitement par lots :** Lors du traitement de dizaines de PDFs, encapsulez la logique ci‑dessus dans une boucle et consignez le succès/échec de chaque fichier.
- **Filtrage par confiance :** Chaque `page_result` inclut une métrique de confiance. Écartez ou signalez les pages avec une faible confiance pour une révision manuelle.
- **Parallélisme :** Si votre CPU possède plusieurs cœurs, envisagez d'utiliser `concurrent.futures` pour traiter les pages en parallèle — en restant attentif à l'utilisation de la mémoire.
- **Verrouillage de version :** L'API `aocr` peut évoluer. Fixez la version dans `requirements.txt` (par ex., `aocr==2.3.1`) pour éviter les changements incompatibles.

## Conclusion

Nous avons parcouru **comment utiliser l'OCR** pour **extraire du texte d'un PDF**, **exécuter l'OCR sur le PDF**, **charger le PDF en image**, et même **convertir un PDF numérisé** en un format recherchable. Le code est complet, les explications couvrent à la fois le *quoi* et le *pourquoi*, et vous disposez désormais d'un modèle réutilisable pour tout projet traitant des PDFs basés sur des images.

Et ensuite ? Essayez d'alimenter le texte extrait dans un pipeline de traitement du langage naturel, indexez les PDFs recherchables avec Elasticsearch, ou expérimentez différents back‑ends OCR comme Tesserent ou Azure Computer Vision. Le ciel est la limite, et les outils sont à portée de main.

Bon codage, et que vos PDFs soient toujours recherchables ! 

![exemple d'utilisation de l'OCR](/images/ocr_workflow.png "comment utiliser l'OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}