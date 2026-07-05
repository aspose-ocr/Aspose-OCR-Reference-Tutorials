---
category: general
date: 2026-07-05
description: Créez un PDF consultable avec Python. Apprenez à OCR un PNG numérisé,
  à convertir un PDF d'image numérisée et à obtenir un PDF consultable en quelques
  minutes.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: fr
og_description: Créez rapidement un PDF consultable. Ce guide montre comment OCR un
  PNG, convertir un PDF d’image numérisée et produire un PDF consultable à l’aide
  de Python.
og_title: Créer un PDF consultable à partir d'une image numérisée – Tutoriel OCR Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Créer un PDF consultable à partir d’une image numérisée – Guide complet OCR
  en Python
url: /fr/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir d’une image numérisée – Guide complet OCR Python

Vous êtes-vous déjà demandé comment **créer un PDF consultable** à partir d’une photo numérisée sans payer de logiciels coûteux ? Vous n’êtes pas seul. Dans de nombreux bureaux, les PDF arrivent sous forme d’images plates — difficiles à rechercher, impossibles à copier‑coller, et un cauchemar pour les audits de conformité. La bonne nouvelle ? En quelques lignes de Python, vous pouvez transformer ce PNG statique en un PDF entièrement consultable, et le processus est plus simple que vous ne le pensez.

Dans ce tutoriel, nous parcourrons un **exemple complet de reconnaissance OCR**, en couvrant tout, de l’installation de la bonne bibliothèque à l’écriture du fichier PDF final. À la fin, vous saurez exactement comment **convertir des PDF d’images numérisées**, comment **ocr pdf** programmatique, et vous disposerez d’un script réutilisable que vous pourrez intégrer à n’importe quel projet.

## Ce que vous allez apprendre

- Installer et configurer une bibliothèque OCR Python (nous utiliserons `pytesseract` et `pdf2image`).
- Initialiser le moteur OCR et définir la langue.
- Charger un PNG numérisé (ou toute image) et exécuter l’OCR dessus.
- Convertir le résultat OCR en **PDF consultable** (tableau d’octets) et l’enregistrer.
- Astuces pour gérer les documents multi‑pages, les différentes langues et les pièges courants.

Aucune expérience préalable avec l’OCR n’est requise — juste un environnement Python 3 fonctionnel et un peu de curiosité.

---

## Créer un PDF consultable – Vue d’ensemble

Voici un diagramme de flux de haut niveau des étapes que nous allons implémenter.  

![Diagramme du flux de création d’un PDF consultable](https://example.com/flowchart.png "Diagramme du flux de création d’un PDF consultable")

*Texte alternatif : Diagramme du flux de création d’un PDF consultable montrant l’initialisation du moteur, le chargement de l’image, la reconnaissance OCR, la conversion en PDF et l’écriture du fichier.*

---

## Étape 1 : Initialiser le moteur OCR (how to ocr pdf)

Pourquoi devons‑nous initialiser quoi que ce soit ? Le moteur OCR est le cerveau qui interprète les motifs de pixels comme des caractères. En créant une instance du moteur et en définissant explicitement la langue, nous indiquons à la bibliothèque quel alphabet attendre, ce qui améliore considérablement la précision.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Astuce :** Si vous devez OCRiser des documents en plusieurs langues, installez les packs de langues correspondants pour Tesseract et passez une liste comme `"eng+spa"` à `ocr_language`.

---

## Étape 2 : Charger l’image numérisée (convert scanned image pdf)

La prochaine pièce du puzzle consiste à faire entrer les données d’image dans Python. Que vous ayez un PNG unique ou un TIFF multi‑pages, la classe `PIL.Image` peut l’ouvrir. Si vous partez d’un PDF contenant déjà des images numérisées, `pdf2image` convertira chaque page en image pour nous.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Pourquoi c’est important :** Charger l’image en tant qu’objet Pillow nous donne accès à ses données de pixels brutes, dont le moteur OCR a besoin. Ignorer cette étape et fournir directement des octets bruts provoquerait des erreurs.

---

## Étape 3 : Effectuer la reconnaissance OCR sur l’image (ocr recognition example)

Place maintenant la partie amusante — laisser le moteur lire le texte. `pytesseract.image_to_pdf_or_hocr` renvoie un flux d’octets PDF qui contient déjà une couche de texte invisible, exactement ce qu’il nous faut pour un **PDF consultable**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Cas particulier :** Si votre image a un faible contraste, envisagez d’appliquer un seuil simple avant l’OCR :

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Cette petite étape de prétraitement peut augmenter la précision de façon spectaculaire.

---

## Étape 4 : Écrire les octets PDF dans un fichier (convert png searchable pdf)

La bibliothèque OCR nous remet un tableau d’octets — pensez‑y comme le contenu brut d’un fichier PDF. Tout ce que nous devons faire maintenant, c’est écrire ces octets sur le disque.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**Ce que vous verrez :** Ouvrez le fichier résultant dans n’importe quel lecteur PDF et essayez de rechercher un mot que vous savez présent dans l’image originale. Le surlignage devrait vous amener directement à l’emplacement, prouvant que la couche de texte invisible fonctionne.

---

## Étape 5 : Étendre aux documents multi‑pages (convert scanned image pdf)

Les contrats du monde réel s’étendent souvent sur plusieurs pages. Pour **convertir des PDF d’images numérisées** contenant plusieurs pages, bouclez sur chaque page, OCRisez‑la, puis concaténez les PDF résultants.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Pourquoi fusionner ?** Chaque appel à `image_to_pdf_or_hocr` produit un PDF autonome. Les fusionner garantit que le document final conserve l’ordre original des pages.

---

## Problèmes courants et comment les résoudre

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Aucun texte consultable après ouverture du PDF | Tesseract ne trouve aucun caractère (sortie vide) | Vérifiez la qualité de l’image, augmentez le DPI ou appliquez un prétraitement (contraste, binarisation). |
| Caractères illisibles (ex. �) | Pack de langue incorrect ou polices manquantes | Installez les données de langue correctes (`tesseract‑lang‑eng`) et assurez‑vous que `ocr_language` correspond. |
| Taille du fichier PDF énorme (>10 Mo pour une image d’une page) | Utilisation d’un PNG sans perte comme source ; l’OCR ajoute une image haute résolution | Redimensionnez l’image avant l’OCR (`image.thumbnail((1240, 1754))` pour du A4). |
| Le script plante sous Windows avec « tesseract.exe not found » | Binaire Tesseract absent du PATH | Ajoutez `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (ajustez le chemin). |

---

## Script complet, prêt à l’emploi

En rassemblant tout, voici un fichier unique que vous pouvez copier‑coller et exécuter :

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Enregistrez‑le sous le nom `create_searchable_pdf.py`, remplacez les espaces réservés par de vrais chemins, puis lancez :

```bash
python create_searchable_pdf.py
```

Vous devriez voir un


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}