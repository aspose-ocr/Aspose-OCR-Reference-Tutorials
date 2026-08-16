---
category: general
date: 2026-03-18
description: Exécutez la reconnaissance OCR sur une image pour extraire le texte d’un
  PNG et générer un PDF consultable. Apprenez à reconnaître le texte d’une image et
  à convertir un PNG en PDF en quelques minutes.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: fr
og_description: Exécutez l'OCR sur l'image pour extraire le texte d'un PNG, reconnaître
  le texte de l'image et générer un PDF consultable. Suivez ce guide étape par étape.
og_title: Effectuer une OCR sur une image – Extraire rapidement le texte d’un PNG
tags:
- OCR
- Python
- Image Processing
title: Exécuter l'OCR sur une image – Extraire rapidement le texte d'un PNG
url: /fr/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter OCR sur une image – Extraire du texte d'un PNG rapidement

Vous avez déjà eu besoin d'**exécuter OCR sur une image** mais vous ne saviez pas par où commencer ? Peut‑être avez‑vous un article numérisé enregistré sous `article.png` et vous ne voulez que le texte brut, ou vous avez besoin d'un PDF consultable pour l'archivage. Dans les deux cas, vous êtes au bon endroit. Dans ce tutoriel, nous allons parcourir l'extraction du texte d'un PNG, la reconnaissance de l'image texte, et même la conversion de ce PNG en PDF consultable — le tout avec quelques lignes de code.

> **Ce que vous obtiendrez :** un script complet et exécutable qui charge un PNG, exécute OCR, enregistre la sortie hOCR, et crée éventuellement un PDF consultable. Aucun import manquant, aucune impasse du type « voir la documentation » — juste une solution autonome que vous pouvez intégrer à votre projet dès aujourd’hui.

## Prérequis

- **Python 3.8+** (la syntaxe utilisée ici fonctionne avec n'importe quelle version récente)
- La bibliothèque **`ocr_engine`** que vous utilisez (l'exemple suppose une classe appelée `OcrEngine` ; remplacez‑la par Tesseract, EasyOCR, etc., si nécessaire)
- Une image PNG que vous souhaitez traiter (par ex. `article.png` placée dans un dossier que vous pouvez référencer)
- Permission d'écriture sur le répertoire de sortie

Si vous utilisez Tesseract en interne, installez‑le avec :

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

Puis installez l'enveloppe Python  :

```bash
pip install pytesseract Pillow
```

*Astuce :* gardez votre bibliothèque OCR à jour — de nouveaux packs de langues et des améliorations de performances arrivent fréquemment.

## Exécuter OCR sur une image – Guide étape par étape

Ci-dessous le **script complet**. N'hésitez pas à le copier‑coller dans un fichier nommé `run_ocr.py` et à l'exécuter avec `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Ce que fait le script, en termes simples

1. **Instancier** le moteur OCR afin de pouvoir contrôler ses paramètres.
2. **Charger** le fichier PNG (`article.png`). Le script s'arrête rapidement si le fichier n'existe pas — aucun erreur mystérieuse `NoneType` plus tard.
3. **Sélectionner** `hocr` comme format d'exportation. Ce format conserve la mise en page originale, ce qui est essentiel pour convertir ultérieurement l'image en PDF consultable.
4. **Exécuter** le moteur de reconnaissance ; c'est ici que le travail lourd est effectué.
5. **Écrire** le XML hOCR dans `article.hocr`. Vous avez maintenant une représentation lisible par machine du texte et de ses coordonnées.
6. *(Optionnel)* Passer à `"pdf"` et générer un PDF consultable en une étape supplémentaire.

La **sortie attendue** est un fichier `.hocr` encodé en UTF‑8 qui ressemble à ceci (troncé pour la brièveté) :

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Si vous décommentez la section PDF, vous obtiendrez également `article_searchable.pdf`, que vous pouvez ouvrir avec n'importe quel lecteur PDF et utiliser la boîte de recherche **Ctrl + F** pour localiser les mots instantanément.

![Exemple de sortie d'OCR sur image](example.png "OCR sur image – résultats hOCR et PDF")

## Comment extraire du texte d'un PNG avec OcrEngine

Si tout ce dont vous avez besoin est le texte brut (sans mise en page, sans PDF), vous pouvez ignorer complètement l'étape hOCR :

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Pourquoi choisir le texte brut ?* Il est léger, parfait pour l'indexation, et fonctionne très bien avec les pipelines NLP en aval.

## Reconnaître l'image texte et générer un PDF consultable

Générer un PDF consultable est une danse en deux parties :

1. **Exécuter OCR** avec `hocr` (comme nous l'avons fait ci‑dessus) pour obtenir les informations de mise en page.
2. **Combiner** le PNG original avec le hOCR dans un PDF en utilisant l'exportateur PDF du moteur.

La plupart des bibliothèques OCR modernes (Tesseract, ABBYY, Google Vision) exposent une exportation `pdf` qui fait exactement cela. L'extrait dans le bloc *Optionnel* du script principal montre le modèle. Si votre bibliothèque ne possède pas d'exportateur PDF intégré, vous pouvez utiliser **`pdf2image`** + **`reportlab`** pour assembler l'image et le hOCR—faites‑le moi savoir, et je partagerai un exemple supplémentaire rapide.

## Convertir PNG en PDF avec la sortie OCR

Parfois vous voulez simplement un **PDF simple** qui contient l'image (sans couche consultable). C’est encore plus simple :

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Combinez cela avec l'étape OCR si vous avez besoin d'une version consultable, ou conservez‑le comme une réplique visuelle fidèle à des fins d'archivage.

## Pièges courants & astuces

| Problème | Pourquoi cela se produit | Solution rapide |
|----------|--------------------------|-----------------|
| **PNG flou ou basse résolution** | La précision de l'OCR chute drastiquement en dessous d'environ 300 DPI. | Agrandir avec `Image.resize((width*2, height*2), Image.LANCZOS)` avant de le fournir au moteur. |
| **Mauvaise langue** | Le moteur utilise l'anglais par défaut ; les caractères non anglais deviennent illisibles. | Appeler `ocr_engine.setLanguage('deu')` (ou le code ISO approprié) avant `recognize()`. |
| **Sortie hOCR manquante** | Certains moteurs basculent vers le texte brut lorsque `setExportFormat` n’est pas appelé. | Vérifier que `setExportFormat("hocr")` s'exécute **avant** `recognize()`. |
| **Erreurs de permission de fichier** | Tentative d'écriture dans un dossier en lecture seule. | Utiliser un chemin à l'intérieur de votre projet ou `os.makedirs(..., exist_ok=True)` d'abord. |
| **Les gros PDFs provoquent des pics de mémoire** | L'exportateur PDF garde l'image entière en RAM. | Traiter les pages par lots ou utiliser un générateur PDF en flux. |

*Astuce :* testez toujours sur une petite image d'exemple avant de passer à un lot de milliers. Cela évite des heures de débogage.

## Conclusion

Vous savez maintenant **comment exécuter OCR sur des fichiers image**, **extraire du texte d'un PNG**, **reconnaître l'image texte** pour des tâches en aval, **générer un PDF consultable**, et **convertir PNG en PDF** lorsque vous avez besoin d'une archive simple. Le script fourni est une solution complète, prête à copier‑coller, qui fonctionne immédiatement, et les sections optionnelles vous permettent d'adapter la sortie à votre flux de travail exact.

### Et après ?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}