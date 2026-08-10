---
category: general
date: 2026-06-19
description: Comment extraire un PDF avec OCR en Python – tutoriel étape par étape
  couvrant l'extraction de texte d'un PDF, la reconnaissance de texte à partir d'une
  image et un exemple d'OCR en Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: fr
og_description: Comment extraire un PDF avec OCR en Python. Apprenez à extraire le
  texte d’un PDF, à reconnaître le texte d’une image, et découvrez un exemple complet
  d’OCR en Python.
og_title: Comment extraire le texte d’un PDF avec OCR en Python – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Comment extraire le texte d’un PDF avec OCR en Python – Guide complet
url: /fr/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire du texte PDF avec OCR en Python – Guide complet

Vous vous êtes déjà demandé **comment extraire PDF** lorsque le fichier n’est qu’une image numérisée ? Vous n’êtes pas seul. Dans de nombreux projets réels—contrats, factures ou archives historiques—le PDF que vous recevez ne contient aucun texte sélectionnable. Bonne nouvelle : quelques lignes de Python peuvent transformer ces pages uniquement images en texte consultable et modifiable.

Dans ce tutoriel, nous allons parcourir un **exemple OCR Python** pratique qui lit un PDF, rend sa première page sous forme d’image, puis **extrait le texte du PDF** à l’aide d’un moteur OCR. À la fin, vous saurez exactement comment **lire PDF avec OCR**, pourquoi chaque étape est importante, et comment adapter le code pour des documents multi‑pages ou d’autres langues.

## Ce que vous allez apprendre

- Installer et configurer une bibliothèque OCR fiable pour Python.  
- Convertir les pages PDF en images adaptées à l’OCR.  
- **Reconnaître le texte à partir d’une image** et récupérer des chaînes Unicode propres.  
- Pièges courants (PDF basse résolution, pages tournées) et comment les éviter.  
- Étendre le script pour gérer plusieurs pages ou un traitement par lots.

**Prérequis** : Python 3.8+, pip, et une compréhension de base des environnements virtuels. Aucune expérience préalable en OCR requise—suivez simplement le guide.

---

## ## Comment extraire du texte PDF avec OCR en Python

Ce titre H2 contient notre mot‑clé principal exactement où les moteurs de recherche aiment le voir. Passons directement au code.

### Étape 1 – Installer les paquets requis

Tout d’abord, nous avons besoin d’un moteur OCR. L’exemple ci‑dessous utilise le populaire package **ocr** (un wrapper léger autour de Tesseract). Si vous préférez un autre backend, les concepts restent les mêmes.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Astuce :** Sous Linux, vous aurez également besoin du binaire Tesseract : `sudo apt-get install tesseract-ocr`. Les utilisateurs macOS peuvent l’obtenir via Homebrew : `brew install tesseract`.

### Étape 2 – Initialiser le moteur OCR et définir la langue

Nous lançons maintenant le moteur et lui indiquons de rechercher les caractères anglais. Vous pouvez remplacer `ocr.Language.English` par n’importe quel code de langue supporté.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Pourquoi c’est important :** Spécifier la langue améliore considérablement la précision car le moteur peut appliquer des dictionnaires et modèles de caractères propres à la langue.

### Étape 3 – Charger une page PDF en tant qu’image

L’OCR fonctionne sur des images raster, pas sur des objets PDF. L’aide‑mémoire `ocr.Image.from_pdf` rend la page choisie en bitmap. Ajustez `page_number` pour d’autres pages (indexation à partir de 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Cas particulier :** Si le PDF contient des graphiques vectoriels plutôt que des images numérisées, vous pourriez obtenir un rendu net. Pour des scans basse résolution, envisagez d’augmenter le DPI : `ocr.Image.from_pdf(..., dpi=300)`.

### Étape 4 – Reconnaître le texte à partir de l’image rendue

Voici le cœur de **l’exemple ocr python**. Le moteur traite le bitmap et renvoie un objet contenant la chaîne extraite.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

L’attribut `ocr_result.text` contient la sortie texte brute, en conservant les sauts de ligne lorsque c’est possible.

### Étape 5 – Afficher ou stocker le texte extrait

Enfin, nous affichons le résultat. Dans une vraie application, vous écririez probablement dans un fichier ou une base de données.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

L’exécution du script devrait afficher quelque chose comme :

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

C’est un flux de travail complet **extraction texte depuis pdf** utilisant l’OCR.

---

## ## Reconnaître le texte à partir d’une image – Ajuster la précision

Si vous ne vous intéressez qu’à **reconnaître le texte à partir d’une image** (par ex., un JPEG d’un reçu), vous pouvez ignorer l’étape de conversion PDF :

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Conseils pour de meilleurs résultats :**

- **Pré‑traiter** l’image : convertir en niveaux de gris, appliquer un seuillage, ou redresser. Pillow rend cela simple.  
- **Augmenter le DPI** lors du rendu PDF : une résolution plus élevée fournit plus de détails au moteur OCR.  
- **Activer la configuration du moteur OCR** pour la segmentation de page (`ocr_engine.config = "--psm 6"` pour des blocs uniformes).

---

## ## Lire PDF avec OCR – Gestion de plusieurs pages

La plupart des contrats s’étendent sur plusieurs pages. Boucler sur chaque page est simple :

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Cette fonction **lit PDF avec OCR**, concatène la sortie et insère un marqueur de saut de page clair. Vous pouvez ensuite injecter `full_text` dans un index de recherche ou le stocker comme fichier `.txt`.

---

## ## Problèmes courants et solutions

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Caractères brouillés, beaucoup de `?` | Mauvaise langue ou fichiers de données linguistiques manquants | Installer le bon pack de langue Tesseract (`tesseract-ocr-<lang>`) et définir `ocr_engine.language`. |
| Lignes manquantes ou mots tronqués | DPI trop faible (inférieur à 150) | Rendre le PDF à 300 DPI ou plus (`dpi=300`). |
| Texte tourné ou à l’envers | Page numérisée pas à l’endroit | Utiliser `ocr.Image.deskew(page_image)` avant la reconnaissance. |
| Traitement lent sur de gros PDFs | Traitement séquentiel des pages sur un seul thread | Paralleliser avec `concurrent.futures.ThreadPoolExecutor`. |

---

## ## Étendre l’exemple OCR Python

- **Exporter vers PDF/A** : après extraction, vous pouvez réintégrer le texte dans un PDF consultable à l’aide de `reportlab` ou `pypdf2`.  
- **Détection de langue** : utilisez `langdetect` sur la sortie OCR pour changer dynamiquement `ocr_engine.language`.  
- **Traitement par lots** : parcourez un répertoire avec `os.listdir` et appliquez `extract_all_pages` à chaque fichier.

---

## ## Résultat attendu et vérification

Lorsque vous exécutez le script sur un scan clair en anglais, vous devriez voir un bloc de texte propre avec une ponctuation correcte. Vérifiez en :

1. Comparant quelques lignes avec l’image numérisée d’origine.  
2. Exécutant un simple comptage de mots (`len(ocr_result.text.split())`) pour s’assurer que la sortie n’est pas vide.  
3. Optionnellement, en passant le résultat dans un correcteur orthographique comme `pyspellchecker` pour repérer les erreurs d’OCR.

---

## Conclusion

Nous avons couvert **comment extraire PDF** lorsque l’analyse traditionnelle échoue, démontré un **exemple ocr python** complet, et expliqué comment **reconnaître le texte à partir d’une image** et **lire PDF avec OCR** pour des scénarios mono‑page et multi‑pages. Avec les extraits de code ci‑dessus, vous pouvez désormais transformer n’importe quel PDF numérisé en texte consultable et modifiable—plus besoin de retaper manuellement.

Prochaines étapes ? Essayez de changer la langue en espagnol (`ocr.Language.Spanish`) ou expérimentez les techniques de pré‑traitement d’image pour augmenter la précision. Si vous construisez un système de gestion de documents, pensez à indexer le texte extrait avec Elasticsearch pour une recherche ultra‑rapide.

Des questions ou un PDF capricieux ? Laissez un commentaire, et bon codage !  

![Comment extraire PDF avec OCR en Python](image.png "Comment extraire PDF avec OCR en Python")


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}