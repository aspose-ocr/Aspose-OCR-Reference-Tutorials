---
category: general
date: 2026-06-25
description: Prétraiter l'image pour l'OCR et reconnaître le texte d'un document numérisé
  en utilisant Python. Tutoriel étape par étape avec le code complet.
draft: false
keywords:
- preprocess image for OCR
- recognize text from scanned document
- Python OCR tutorial
- image deskewing Python
- OCR preprocessing tips
language: fr
og_description: Prétraitez l'image pour l'OCR et reconnaissez le texte d'un document
  numérisé avec Python. Suivez ce tutoriel détaillé et exécutable.
og_title: Prétraiter l'image pour l'OCR en Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  headline: Preprocess Image for OCR in Python – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR and recognize text from scanned document using
    Python. Step‑by‑step tutorial with full code.
  name: Preprocess Image for OCR in Python – Complete Guide
  steps:
  - name: Create an OCR Engine Instance
    text: '```python import ocr # <-- make sure the OCR library is installed'
  - name: Enable Automatic Deskewing and Binarization
    text: '```python # Step 2: Enable automatic deskewing and binarization to improve
      recognition engine.image_preprocessing = ocr.ImagePreProcessingOptions( auto_deskew=True,
      auto_binarize=True ) ```'
  - name: Load the Skewed Image You Want to Process
    text: '```python # Step 3: Load the skewed image you want to process image_path
      = "YOUR_DIRECTORY/skewed_document.jpg" image = ocr.Image.load(image_path) ```'
  - name: Perform OCR on the Pre‑processed Image
    text: '```python # Step 4: Perform OCR on the pre‑processed image result = engine.recognize(image)
      ```'
  - name: Output the Recognized Text
    text: '```python # Step 5: Output the recognized text print("Deskewed & binarized
      text:", result.text) ```'
  - name: 1. Handling Multiple Languages
    text: 'If your document contains both English and French, configure the engine
      before step 1:'
  - name: 2. Fine‑Tuning Binarization Thresholds
    text: 'Automatic binarization works for most cases, but some old photocopies need
      a custom threshold:'
  - name: 3. Extracting Layout Information
    text: 'Sometimes you need more than raw text—you want to know where each paragraph
      lives on the page. Many engines expose a `result.blocks` collection:'
  - name: 4. Processing a Batch of Files
    text: 'If you have a folder full of scanned PDFs converted to JPEGs, wrap the
      whole flow in a loop:'
  - name: 5. Dealing with Low‑Resolution Scans
    text: 'Low‑resolution images (< 150 dpi) often produce fuzzy characters. A quick
      remedy is to upscale using a high‑quality algorithm before feeding the image
      to the OCR engine:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Prétraitement d'image pour l'OCR en Python – Guide complet
url: /fr/python-java/general/preprocess-image-for-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prétraiter l'image pour l'OCR en Python – Guide complet

Vous vous êtes déjà demandé comment **preprocess image for OCR** afin que le texte soit propre et fiable ? Vous n'êtes pas seul—la plupart des développeurs rencontrent le même problème lorsque la page numérisée est de travers ou que le contraste est déséquilibré. La bonne nouvelle, c’est que quelques lignes de Python peuvent redresser ce désordre, binariser l’image et vous restituer un texte net et consultable.

Dans ce tutoriel, nous parcourrons les étapes exactes pour **preprocess image for OCR** *et* **recognize text from scanned document** fichiers, en utilisant une bibliothèque OCR populaire. À la fin, vous disposerez d’un script prêt à l’emploi, comprendrez pourquoi chaque paramètre est important et saurez comment l’ajuster pour les cas limites difficiles.

## Ce dont vous avez besoin

- Python 3.8 ou plus récent (le code fonctionne également avec 3.10+)
- Un package OCR qui expose les classes `OcrEngine`, `ImagePreProcessingOptions` et `Image` (par ex., le module fictif `ocr` utilisé dans l’exemple)
- Un document numérisé ou photographié légèrement incliné ou à faible contraste
- Votre IDE préféré ou un simple terminal—aucune interface graphique lourde requise

C’est tout. Aucun binaire supplémentaire, aucune gymnastique Docker. Plongeons‑y.

## Prétraiter l'image pour l'OCR – Étape par étape

Voici le flux de travail principal découpé en cinq étapes claires. Chaque étape comprend **pourquoi** nous le faisons, le **code** exact, et une courte **explication** de ce qui se passe en coulisses.

### Étape 1 : Créer une instance d’OCR Engine

```python
import ocr  # <-- make sure the OCR library is installed

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Pourquoi c’est important :*  
L’objet `OcrEngine` est le cerveau de l’opération. Il contient la configuration comme les packs de langues, les seuils de confiance, et—le plus important pour nous—les drapeaux de prétraitement d’image. L’instancier en premier nous donne une base propre pour activer les astuces qui suivent.

### Étape 2 : Activer le redressement automatique et la binarisation

```python
# Step 2: Enable automatic deskewing and binarization to improve recognition
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
```

*Pourquoi c’est important :*  
- **Deskewing** fait pivoter l’image afin que les lignes de texte deviennent horizontales. Les moteurs OCR peinent lorsque la ligne de base penche de plus de quelques degrés.  
- **Binarization** convertit l’image en noir et blanc pur, éliminant le bruit de fond qui peut perturber les classificateurs de caractères.  
- Les deux options sont *automatiques* dans de nombreuses bibliothèques modernes, mais vous devez encore les activer—d’où l’affectation explicite.

> **Astuce :** Si vos images sources sont déjà parfaitement alignées, vous pouvez définir `auto_deskew=False` pour économiser une milliseconde de temps de traitement.

### Étape 3 : Charger l’image inclinée que vous souhaitez traiter

```python
# Step 3: Load the skewed image you want to process
image_path = "YOUR_DIRECTORY/skewed_document.jpg"
image = ocr.Image.load(image_path)
```

*Pourquoi c’est important :*  
La méthode `Image.load` lit le fichier en mémoire et l’enveloppe dans un objet compris par le moteur OCR. Elle extrait également des métadonnées comme le DPI, qui peuvent influencer le facteur d’échelle par défaut pour le redressement.

> **Cas particulier :** Si l’image est un TIFF multi‑pages, vous devrez itérer sur chaque page ou utiliser un assistant comme `ocr.MultiPageImage.load`. Les mêmes paramètres de prétraitement s’appliquent à chaque page.

### Étape 4 : Effectuer l’OCR sur l’image pré‑traitée

```python
# Step 4: Perform OCR on the pre‑processed image
result = engine.recognize(image)
```

*Pourquoi c’est important :*  
À ce stade, le moteur applique les étapes de redressement et de binarisation que nous avons activées précédemment, puis exécute son réseau de neurones (ou le pipeline classique de type Tesseract) sur le bitmap nettoyé. L’objet `result` retourné contient généralement le texte brut, les scores de confiance, et parfois les données de position pour chaque mot.

> **Et si le texte est encore illisible ?**  
> Vérifiez la résolution de l’image : l’OCR fonctionne mieux à 300 dpi ou plus. Si votre source est inférieure, envisagez de l’upscaler avant de la charger, ou demandez le scan original à la source du document.

### Étape 5 : Exporter le texte reconnu

```python
# Step 5: Output the recognized text
print("Deskewed & binarized text:", result.text)
```

*Pourquoi c’est important :*  
`result.text` est une représentation en chaîne de caractères de tout ce que le moteur a pu lire. L’imprimer est pratique pour un débogage rapide ; dans une application réelle, vous l’écririez probablement dans un fichier `.txt`, une base de données, ou le transmettriez à un pipeline NLP en aval.

---

## Reconnaître le texte à partir d’un document numérisé – Aller au-delà des bases

Maintenant que le pipeline de base fonctionne, explorons quelques variations courantes que vous pourriez rencontrer en essayant de **recognize text from scanned document** images dans des conditions réelles.

### 1. Gestion de plusieurs langues

Si votre document contient à la fois l’anglais et le français, configurez le moteur avant l’étape 1 :

```python
engine = ocr.OcrEngine(languages=["eng", "fra"])
```

La plupart des moteurs OCR acceptent les codes ISO‑639‑2 ; charger des packs de langues supplémentaires ajoute un léger surcoût mais améliore considérablement la précision sur les pages multilingues.

### 2. Ajustement fin des seuils de binarisation

La binarisation automatique fonctionne dans la plupart des cas, mais certaines anciennes photocopies nécessitent un seuil personnalisé :

```python
engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=False,          # turn off auto
    binarization_threshold=180   # manual threshold (0‑255)
)
```

Expérimentez avec des valeurs entre 120 et 220 jusqu’à ce que l’arrière‑plan disparaisse sans effacer les caractères faibles.

### 3. Extraction des informations de mise en page

Parfois vous avez besoin de plus que du texte brut—vous voulez savoir où chaque paragraphe se situe sur la page. De nombreux moteurs exposent une collection `result.blocks` :

```python
for block in result.blocks:
    print(f"Block at ({block.x}, {block.y}) size {block.width}x{block.height}")
    print(block.text)
```

C’est inestimable pour reconstruire des tableaux ou préserver l’ordre des colonnes.

### 4. Traitement d’un lot de fichiers

Si vous avez un dossier rempli de PDF numérisés convertis en JPEG, encapsulez tout le flux dans une boucle :

```python
import pathlib

folder = pathlib.Path("YOUR_DIRECTORY")
for img_file in folder.glob("*.jpg"):
    img = ocr.Image.load(str(img_file))
    txt = engine.recognize(img).text
    (folder / f"{img_file.stem}.txt").write_text(txt, encoding="utf-8")
    print(f"Processed {img_file.name}")
```

La boucle réutilise la même instance `engine`, ce qui est plus efficace que de la recréer pour chaque fichier.

### 5. Gestion des scans à basse résolution

Les images à basse résolution (< 150 dpi) produisent souvent des caractères flous. Un remède rapide consiste à les upscaler avec un algorithme de haute qualité avant de les fournir au moteur OCR :

```python
from PIL import Image as PilImage

pil_img = PilImage.open("low_res.jpg")
upscaled = pil_img.resize((pil_img.width * 2, pil_img.height * 2), PilImage.LANCZOS)
upscaled.save("upscaled.jpg")
image = ocr.Image.load("upscaled.jpg")
```

L’upscaling ne créera pas magiquement de détails, mais l’étape de binarisation peut travailler avec des bords plus nets, offrant un léger gain.

## Résultat attendu

Exécuter le script original en cinq étapes sur un scan modérément incliné à 300 dpi devrait afficher quelque chose comme :

```
Deskewed & binarized text: 
Dear Customer,

Thank you for your recent purchase. Please find your receipt attached.

Best regards,
Acme Corp.
```

Si vous voyez des caractères illisibles, revérifiez les drapeaux de prétraitement, la résolution de l’image et la configuration des langues.

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **preprocess image for OCR** et **recognize text from scanned document** fichiers en utilisant Python. En partant d’une nouvelle instance de moteur, nous avons activé le redressement automatique et la binarisation, chargé une image inclinée, exécuté la reconnaissance et imprimé le texte propre. En cours de route, nous avons exploré le support multilingue, les ajustements manuels de seuil, l’extraction de mise en page, le traitement par lots et les solutions pour les résolutions basses.

Testez le script sur vos propres scans—peut‑être une pile de reçus, un formulaire manuscrit, ou une vieille découpe de journal. Une fois à l’aise, essayez d’ajouter la génération de PDF ou d’alimenter la sortie dans un index de recherche. Les possibilités sont infinies.

**Prêt pour le prochain défi ?** Consultez nos tutoriels sur *« Extract Tables from Scanned PDFs with Python »* et *« Train Custom OCR Models with TensorFlow »* pour continuer à développer votre boîte à outils d’automatisation de documents.

Bon codage, et que votre OCR soit toujours net !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}