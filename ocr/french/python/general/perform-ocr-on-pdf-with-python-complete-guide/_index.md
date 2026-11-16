---
category: general
date: 2026-06-25
description: Effectuez l’OCR sur un PDF avec Python — apprenez à charger le PDF pour
  l’OCR, extraire le texte des pages du PDF et prévisualiser le texte reconnu efficacement.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: fr
og_description: Effectuer une OCR sur un PDF en Python. Ce guide montre comment charger
  un PDF pour l’OCR, extraire le texte des pages du PDF et prévisualiser rapidement
  le texte reconnu.
og_title: Effectuer une OCR sur PDF avec Python – Tutoriel étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Effectuer l'OCR sur un PDF avec Python – Guide complet
url: /fr/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur un PDF avec Python – Guide complet

Vous avez déjà eu besoin d'**effectuer une OCR sur des fichiers PDF** mais vous ne saviez pas par où commencer ? Peut‑être avez‑vous une montagne de contrats numérisés, ou un seul manuel volumineux qui refuse de coopérer avec votre extracteur de texte habituel. En bref, vous voulez **charger le PDF pour l'OCR**, extraire le texte, et obtenir un aperçu rapide—le tout sans épuiser la mémoire de votre machine.

Eh bien, vous êtes au bon endroit. Dans ce tutoriel, nous passerons en revue un script Python entièrement fonctionnel qui **extrait le texte des pages PDF**, vous montre comment **prévisualiser le texte reconnu**, et résout même le problème classique de **comment faire de l'OCR sur de gros PDF** de manière efficace.

À la fin, vous disposerez d’un programme prêt à l’emploi, d’une compréhension claire de chaque paramètre de configuration, et de plusieurs astuces pour éviter les pièges courants qui font trébucher les débutants.

---

## Ce que vous allez apprendre

- Comment **charger le PDF pour l'OCR** à l'aide de la bibliothèque `aocr`.
- Les étapes exactes pour **effectuer une OCR sur les pages PDF** une par une.
- Des méthodes pour **extraire le texte des pages PDF** tout en maîtrisant l’utilisation de la mémoire.
- Comment **prévisualiser le texte reconnu** pour vérifier la pertinence des résultats.
- Des stratégies pour gérer les **gros PDF** sans épuiser la RAM.

> **Astuce :** Ce guide suppose que vous avez Python 3.9+ installé et une connaissance de base des environnements virtuels. Si vous débutez avec Python, créez d’abord un virtualenv—croyez‑moi, cela évite bien des maux de tête plus tard.

---

## Prérequis

| Prérequis | Pourquoi c’est important |
|-----------|---------------------------|
| Package Python `aocr` (ou tout moteur OCR compatible) | Fournit la classe `OcrEngine` utilisée tout au long du script. |
| `pip` et un environnement virtuel | Garde les dépendances isolées de votre Python système. |
| Espace disque suffisant pour les extractions d’images temporaires | Certains moteurs OCR écrivent les images de page sur le disque avant le traitement. |
| Facultatif : `tqdm` pour les barres de progression | Améliore l’expérience utilisateur lors du traitement de **comment faire de l'OCR sur de gros PDF**. |

Installez les essentiels avec :

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Si votre PDF est protégé par un mot de passe, vous devrez fournir le mot de passe plus tard—voir la section « Cas particuliers ».

---

## Étape 1 : Effectuer l'OCR sur le PDF – Configuration du moteur

Première chose, nous avons besoin d’une instance du moteur OCR. Pensez‑y comme le cerveau qui lira l’image de chaque page et produira du texte brut.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Pourquoi définir `max_memory_mb` ?**  
> Les moteurs OCR mettent souvent en cache les images de page en RAM. En limitant la mémoire, vous évitez que votre script ne plante sur un contrat de 500 pages.

---

## Étape 2 : Charger le PDF pour l'OCR et configurer les paramètres

Nous allons maintenant réellement **charger le PDF pour l'OCR**. Le chemin peut être absolu ou relatif ; assurez‑vous simplement que le fichier existe.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Si le PDF est chiffré, `engine.load_pdf` lèvera généralement une exception. Dans ce cas, vous pouvez appeler `engine.load_pdf(pdf_path, password="secret")`—plus de détails plus loin.

---

## Étape 3 : Extraire le texte des pages PDF – Boucle principale

C’est ici que nous **effectuons l'OCR sur le PDF** page par page. Nous **prévisualiserons également le texte reconnu** pour les premiers quelques centaines de caractères afin que vous puissiez vérifier que tout fonctionne.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Astuce pro :** La barre de progression `tqdm` vous donne un repère visuel, particulièrement utile lorsqu’on traite des **comment faire de l'OCR sur de gros PDF** qui prennent plusieurs minutes.

---

## Étape 4 : Tout assembler – Un script prêt à l’exécution

Voici l’exemple complet et exécutable. Enregistrez‑le sous le nom `pdf_ocr.py` et lancez‑le avec `python pdf_ocr.py path/to/your/file.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Sortie attendue (extrait)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Vous verrez un court aperçu pour chaque page, suivi d’une confirmation finale indiquant que le fichier texte concaténé a bien été écrit.

---

## Cas particuliers & conseils pratiques

| Situation | Que faire |
|-----------|-----------|
| **PDF chiffré** | Fournissez le mot de passe : `engine.load_pdf(pdf_path, password="mySecret")`. |
| **PDF très volumineux (> 1000 pages)** | Augmentez prudemment `max_memory_mb`, ou traitez par blocs (par ex. 200 pages à la fois). |
| **Contenu mixte (imprimé + manuscrit)** | Changez `engine.recognition_mode` en `aocr.RecognitionMode.MIXED` si la bibliothèque le supporte. |
| **Polices manquantes ou mauvaise qualité de numérisation** | Pré‑traitez les pages avec une bibliothèque d’amélioration d’image (ex. Pillow) avant d’appeler `recognize()`. |
| **Plantages hors‑mémoire** | Réduisez `preview_len` ou écrivez le texte de chaque page directement sur le disque au lieu de tout garder dans une liste. |

---

## Comment faire de l'OCR sur de gros PDF efficacement – Stratégies avancées

Lorsque vous abordez **comment faire de l'OCR sur de gros PDF**, la vitesse et la stabilité deviennent cruciales. Voici quelques astuces à intégrer dans le script :

1. **Paralléliser par page** – Utilisez `concurrent.futures.ThreadPoolExecutor` si le moteur OCR est thread‑safe.  
2. **Mettre en cache les images intermédiaires** – Certains moteurs permettent de stocker les pages rasterisées sur SSD, ce qui réduit considérablement la charge CPU lors des ré‑exécutions.  
3. **Écriture batch du résultat** – Au lieu d’ajouter à une liste Python, ouvrez le fichier de sortie une fois et écrivez le texte de chaque page dès qu’il est prêt.  
4. **Ajuster le DPI** – Baisser le DPI lors de la rasterisation diminue la mémoire mais peut affecter la précision ; trouvez le compromis idéal (généralement 200‑300 DPI).

Voici un petit extrait montrant comment vous pourriez paralléliser l’étape OCR (optionnel, décommentez pour l’utiliser) :

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Rappelez‑vous : le parallélisme peut augmenter l’utilisation du CPU, surveillez donc la température de votre système lors de longues exécutions.

---

## Questions fréquentes

**Q : Puis‑je utiliser ce script avec d’autres bibliothèques OCR comme Tesseract ?**  
**R :** Absolument. Remplacez les appels `aocr` par `pytesseract.image_to

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}