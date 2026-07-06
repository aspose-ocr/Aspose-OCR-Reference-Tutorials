---
category: general
date: 2026-04-29
description: Extraire du texte d’un PDF avec Aspose OCR en Python. Apprenez le traitement
  OCR par lots des PDF, convertissez le texte des PDF numérisés et gérez les pages
  à faible confiance.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: fr
og_description: Extrayez du texte d’un PDF avec Aspose OCR en Python. Ce guide montre
  le traitement OCR par lots des PDF, la conversion du texte des PDF numérisés et
  la gestion des résultats à faible confiance.
og_title: Extraire du texte d’un PDF – OCR PDF avec Python
tags:
- OCR
- Python
- PDF processing
title: Extraire le texte d'un PDF – OCR PDF avec Python
url: /fr/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'un PDF – OCR PDF avec Python

Vous avez déjà eu besoin d'**extraire du texte d'un PDF** mais le fichier n'est qu'une image numérisée ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils essaient de transformer des PDF en données recherchables. La bonne nouvelle ? Avec Aspose OCR for Python, vous pouvez convertir le texte d'un PDF numérisé en quelques lignes, et même exécuter le **traitement OCR PDF par lots** lorsque vous avez des dizaines de fichiers à gérer.

Dans ce tutoriel, nous parcourrons l’ensemble du flux de travail : configuration de la bibliothèque, exécution de l'OCR sur un PDF unique, passage à un traitement par lots, et gestion des pages à faible confiance afin de savoir quand une révision manuelle est nécessaire. À la fin, vous disposerez d'un script prêt à l'emploi qui extrait le texte de n'importe quel PDF numérisé, et vous comprendrez les raisons derrière chaque étape.

## Ce dont vous avez besoin

- Python 3.8 ou plus récent (le code utilise des f‑strings, donc 3.6+ fonctionne, mais 3.8+ est recommandé)
- Une licence Aspose OCR for Python ou une clé d'essai gratuite (vous pouvez en obtenir une sur le site web d'Aspose)
- Un dossier contenant un ou plusieurs PDF numérisés que vous souhaitez traiter
- Une quantité modeste d'espace disque pour les rapports *.txt* générés

C’est tout—pas de dépendances externes lourdes, pas de gymnastique OpenCV. Le moteur Aspose OCR fait le travail lourd pour vous.

## Configuration de l'environnement

Tout d'abord, installez le package Aspose OCR depuis PyPI :

```bash
pip install aspose-ocr
```

Si vous avez un fichier de licence (`Aspose.OCR.lic`), placez-le à la racine de votre projet et activez-le comme suit :

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Astuce :** Gardez le fichier de licence hors du contrôle de version ; ajoutez‑le à `.gitignore` pour éviter toute exposition accidentelle.

## Effectuer l'OCR sur un PDF unique

Examinons maintenant comment extraire du texte d'un PDF numérisé unique. Les étapes principales sont :

1. Créez une instance `OcrEngine`.
2. Pointez‑la vers le fichier PDF.
3. Récupérez un `OcrResult` pour chaque page.
4. Écrivez la sortie en texte brut sur le disque.
5. Libérez le moteur pour libérer les ressources natives.

Voici le script complet et exécutable :

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**Ce que vous verrez :** Pour chaque page, le script affiche quelque chose comme `Page 1: confidence 97.45%`. Si une page est en dessous du seuil de 80 %, un avertissement apparaît, vous indiquant que l'OCR a peut‑être manqué des caractères.

### Pourquoi cela fonctionne

- **`OcrEngine`** est la porte d'accès à la bibliothèque native Aspose OCR ; il gère tout, du prétraitement d'image à la reconnaissance de caractères.
- **`extract_from_pdf`** rasterise automatiquement chaque page du PDF, vous n'avez donc pas besoin de convertir le PDF en images vous‑même.
- **Confidence scores** vous permettent d'automatiser les contrôles de qualité—crucial lorsque vous traitez des documents juridiques ou médicaux où la précision est importante.

## Traitement OCR PDF par lots avec Python

La plupart des projets réels impliquent plus d'un fichier. Étendons le script mono‑fichier à un pipeline de **traitement OCR PDF par lots** qui parcourt un répertoire, traite chaque PDF et stocke les résultats dans un sous‑dossier correspondant.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Comment cela aide

- **Scalabilité :** La fonction parcourt le dossier une fois, créant un sous‑dossier de sortie dédié pour chaque PDF. Cela maintient l'ordre lorsque vous avez des dizaines de documents.
- **Réutilisabilité :** `ocr_pdf_file` peut être appelé depuis d'autres scripts (par ex., un service web) car c'est une fonction pure.
- **Gestion des erreurs :** Le script affiche un message convivial si le dossier d'entrée est vide, vous évitant ainsi un échec silencieux.

## Conversion du texte d'un PDF numérisé – Gestion des cas limites

Bien que le code ci‑dessus fonctionne pour la plupart des PDF, vous pourriez rencontrer quelques particularités :

| Situation | Pourquoi cela se produit | Comment atténuer |
|-----------|--------------------------|------------------|
| **PDF chiffrés** | Le PDF est protégé par un mot de passe. | Passez le mot de passe à `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Documents multilingues** | Aspose OCR utilise l'anglais par défaut. | Définissez `ocr_engine.language = "spa"` pour l'espagnol, ou fournissez une liste pour des langues mixtes. |
| **PDF très volumineux (>500 pages)** | L'utilisation de la mémoire augmente car chaque page est chargée en RAM. | Traitez le PDF par morceaux en utilisant `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` et bouclez. |
| **Qualité de numérisation médiocre** | Une faible résolution DPI ou un bruit important réduit la confiance. | Pré‑traitez le PDF avec `engine.image_preprocessing = True` ou augmentez le DPI via `engine.dpi = 300`. |

> **Attention :** Activer le prétraitement d'image peut augmenter sensiblement le temps CPU. Si vous exécutez un lot nocturne, prévoyez suffisamment de temps ou lancez un travailleur séparé.

## Vérification de la sortie

Après l'exécution du script, vous trouverez une structure de dossiers similaire à :

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Ouvrez n'importe quel fichier `.txt` ; vous devriez voir du texte propre, encodé en UTF‑8, qui reflète le contenu numérisé original. Si vous remarquez des caractères illisibles, revérifiez les paramètres de langue du PDF et assurez‑vous que les packs de polices appropriés sont installés sur la machine.

## Nettoyage des ressources

Aspose OCR repose sur des DLL natives, il est donc essentiel d'appeler `engine.dispose()` une fois terminé. Oublier cette étape peut entraîner des fuites de mémoire, surtout dans des traitements par lots de longue durée.

```python
# Always the last line of your script
engine.dispose()
```

## Exemple complet de bout en bout

En réunissant tout, voici un exemple complet

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}