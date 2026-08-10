---
category: general
date: 2026-05-31
description: Créez un PDF consultable à partir d'images numérisées avec Python OCR.
  Apprenez à convertir un PDF d'images numérisées, à transformer un TIFF en PDF et
  à ajouter une couche de texte OCR en quelques minutes.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: fr
og_description: Créez un PDF consultable instantanément. Ce guide montre comment exécuter
  l’OCR, convertir un PDF d’image numérisée et ajouter une couche de texte OCR à l’aide
  d’un seul script Python.
og_title: Créer un PDF consultable avec Python – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Créer un PDF consultable avec Python – Guide étape par étape
url: /fr/python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF interrogeable avec Python – Guide pas à pas

Vous êtes‑vous déjà demandé comment **créer un PDF interrogeable** à partir d’une page numérisée sans jongler avec des dizaines d’outils ? Vous n’êtes pas seul. Dans de nombreux flux de travail de bureau, un TIFF ou JPEG numérisé atterrit sur un lecteur partagé, et la personne suivante doit copier‑coller le texte manuellement — fastidieux, source d’erreurs et perte de temps.  

Dans ce tutoriel, nous parcourrons une solution propre et programmatique qui vous permet de **convertir un PDF d’image numérisée**, **convertir TIFF en PDF**, et **ajouter une couche de texte OCR** en une seule étape. À la fin, vous disposerez d’un script prêt à l’emploi qui exécute l’OCR, intègre le texte caché et génère un PDF interrogeable que vous pouvez indexer, rechercher ou partager en toute confiance.

## Ce dont vous avez besoin

- Python 3.9+ (toute version récente fonctionne)
- `aspose-ocr` et `aspose-pdf` packages (installés via `pip install aspose-ocr aspose-pdf`)
- Un fichier image numérisé (`.tif`, `.png`, `.jpg`, ou même une page PDF qui n’est qu’une image)
- Une quantité modeste de RAM (le moteur OCR est léger ; même un ordinateur portable le gère)

> **Astuce :** Si vous êtes sous Windows, le moyen le plus simple d’obtenir les paquets est d’exécuter la commande dans une fenêtre PowerShell élevée.

```bash
pip install aspose-ocr aspose-pdf
```

Maintenant que les prérequis sont réglés, plongeons dans le code.

## Étape 1 : Créer une instance du moteur OCR – *create searchable pdf*

La première chose que nous faisons est de lancer le moteur OCR. Considérez-le comme le cerveau qui lira chaque pixel et le transformera en caractères.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Pourquoi c’est important :** Initialiser le moteur une seule fois maintient une faible utilisation de la mémoire. Si vous appeliez `OcrEngine()` dans une boucle pour chaque page, vous manqueriez rapidement de ressources.

## Étape 2 : Charger l’image numérisée – *convert tiff to pdf* & *convert scanned image pdf*

Ensuite, pointez le moteur vers le fichier que vous souhaitez traiter. L’API accepte n’importe quelle image raster, donc un TIFF fonctionne tout aussi bien qu’un JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

Si vous avez un PDF qui ne contient qu’une image numérisée, vous pouvez toujours utiliser `load_image` car Aspose extraira automatiquement la première page.

## Étape 3 : Préparer les options d’enregistrement PDF – *add OCR text layer*

Ici, nous configurons l’apparence du PDF final. Le drapeau crucial est `create_searchable_pdf` ; le définir à `True` indique à la bibliothèque d’intégrer une couche de texte invisible qui reflète le contenu visuel.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **Ce que fait la couche de texte :** Lorsque vous ouvrez le fichier résultant dans Adobe Reader et essayez de sélectionner du texte, vous verrez les caractères cachés. Les moteurs de recherche peuvent également les indexer — idéal pour la conformité ou l’archivage.

## Étape 4 : Exécuter l’OCR et enregistrer – *how to run OCR* in a single call

Maintenant, la magie opère. Un seul appel de méthode exécute le moteur de reconnaissance et écrit le PDF interrogeable sur le disque.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

La méthode `recognize` renvoie un objet d’état que vous pouvez inspecter pour détecter des erreurs, mais pour la plupart des scénarios simples, l’appel simple ci‑dessus suffit.

### Sortie attendue

L’exécution du script affiche :

```
PDF saved as searchable PDF.
```

Si vous ouvrez `scanned_page_searchable.pdf`, vous remarquerez que vous pouvez sélectionner du texte, le copier‑coller, et même lancer une recherche `Ctrl+F`. C’est la marque d’un flux de travail **create searchable pdf**.

## Script complet fonctionnel

Ci‑dessous se trouve le script complet, prêt à être exécuté. Remplacez simplement les chemins factices par vos emplacements de fichiers réels.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Enregistrez-le sous le nom `create_searchable_pdf.py` et exécutez :

```bash
python create_searchable_pdf.py
```

## Questions fréquentes & cas particuliers

### 1️⃣ Puis‑je traiter des PDF multi‑pages ?

Oui. Utilisez `ocr_engine.load_image("file.pdf")` puis bouclez sur chaque page avec `ocr_engine.recognize(pdf_save_options, page_number)`. La bibliothèque générera automatiquement un PDF interrogeable multi‑pages.

### 2️⃣ Que faire si mon fichier source est un TIFF haute résolution (300 dpi+) ?

Une résolution DPI plus élevée donne une meilleure précision OCR mais aussi une utilisation mémoire plus importante. Si vous rencontrez un `MemoryError`, réduisez d’abord la taille de l’image :

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ Comment changer la langue de l’OCR ?

Définissez la propriété `language` sur le moteur avant de charger l’image :

```python
ocr_engine.language = "fra"   # French
```

Une liste complète des codes de langue pris en charge se trouve dans la documentation Aspose.

### 4️⃣ Que faire si je dois conserver la qualité d’image d’origine ?

La classe `PdfSaveOptions` possède une propriété `compression`. Réglez‑la sur `PdfCompression.None` pour préserver les données raster exactement telles qu’elles étaient.

```python
pdf_save_options.compression = "None"
```

## Conseils pour des déploiements prêts pour la production

- **Traitement par lots :** Encapsulez la logique principale dans une fonction qui accepte une liste de chemins de fichiers. Enregistrez chaque succès/échec dans un CSV pour les traces d’audit.
- **Parallélisme :** Utilisez `concurrent.futures.ThreadPoolExecutor` pour exécuter l’OCR sur plusieurs cœurs. N’oubliez pas que chaque thread a besoin de sa propre instance `OcrEngine`.
- **Sécurité :** Si vous traitez des documents sensibles, exécutez le script dans un environnement sandbox et supprimez les fichiers temporaires immédiatement après le traitement.

## Conclusion

Vous savez maintenant comment **créer des PDF interrogeables** à partir d’images numérisées en utilisant un script Python concis. En initialisant un moteur OCR, en chargeant un TIFF (ou tout raster), en configurant `PdfSaveOptions` pour **add OCR text layer**, et enfin en appelant `recognize`, l’ensemble du pipeline **convert scanned image pdf** et **convert TIFF to PDF** devient une commande unique et réutilisable.

Prochaines étapes ? Essayez d’enchaîner ce script avec un observateur de fichiers afin que chaque nouvelle numérisation déposée dans un dossier devienne automatiquement interrogeable. Ou expérimentez différentes langues OCR pour prendre en charge des archives multilingues. Le ciel est la limite lorsque vous combinez OCR et génération de PDF.

Vous avez d’autres questions sur **how to run OCR** dans d’autres langages ou frameworks ? Laissez un commentaire ci‑dessous, et bon codage ! 

![Diagram showing the flow from scanned image → OCR engine → searchable PDF (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")

## Que devriez‑vous apprendre ensuite ?

- [Comment faire de l’OCR d’un PDF en .NET avec Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convertir des images en PDF C# – Enregistrer le résultat OCR multi‑pages](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Comment faire de l’OCR de texte d’image avec la langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}