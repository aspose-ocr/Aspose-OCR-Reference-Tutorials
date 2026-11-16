---
category: general
date: 2026-06-25
description: Extraire le texte d’un PDF avec OCR en Python. Apprenez à convertir un
  PDF en texte grâce à un exemple clair d’OCR en Python et obtenez des résultats fiables
  rapidement.
draft: false
keywords:
- extract pdf text OCR
- convert pdf to text
- python ocr example
- Aspose OCR Python
- multi‑page PDF OCR
language: fr
og_description: Extraire le texte d’un PDF avec OCR en Python. Ce guide présente un
  exemple d’OCR en Python qui convertit les PDF en texte, en gérant sans effort les
  documents multi‑pages.
og_title: Extraction de texte PDF OCR en Python – Tutoriel complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract PDF text OCR using Python. Learn how to convert PDF to text
    with a clear python OCR example and get reliable results fast.
  headline: Extract PDF Text OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Extraction de texte PDF OCR en Python – Guide complet étape par étape
url: /fr/python-java/general/extract-pdf-text-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraction de texte PDF OCR en Python – Guide complet étape par étape

Vous avez déjà eu besoin d'**extraire du texte PDF OCR** sans savoir quelle bibliothèque pouvait gérer des PDF multi‑pages sans prise de tête ? Vous n'êtes pas seul. Dans de nombreux projets réels—contrats juridiques, factures numérisées ou rapports archivés—obtenir un texte propre et consultable à partir d'un PDF est une compétence indispensable.

Dans ce tutoriel, nous allons parcourir un **exemple python ocr** qui **convertit un pdf en texte** à l'aide d'Aspose.OCR. À la fin, vous disposerez d'un script prêt à l'emploi qui extrait le texte de chaque page, affiche un aperçu et même enregistre l'ensemble du document dans un fichier `.txt` unique. Pas de blabla, juste une solution pratique que vous pouvez intégrer dès aujourd'hui à votre code.

## Ce que vous allez apprendre

- Comment installer et importer le module Aspose OCR pour Python.  
- Comment créer une instance du moteur OCR et exécuter **l'extraction de texte PDF OCR** sur un PDF multi‑pages.  
- Comment parcourir le résultat de chaque page, afficher un aperçu et écrire la sortie complète sur le disque.  
- Astuces pour gérer les pièges courants comme les pages blanches ou les caractères Unicode.  

> **Prérequis :** Python 3.8+ installé, connaissance de base de pip, et un fichier PDF que vous souhaitez traiter. Aucune expérience préalable en OCR n'est requise.

---

![Extract PDF Text OCR workflow diagram](extract-pdf-text-ocr.png "Diagram of extract pdf text OCR process")

*Texte alternatif : Diagramme illustrant le flux de travail de l'extraction de texte PDF OCR en Python.*

## Étape 1 : Installer Aspose OCR pour Python

Avant que le code ne s'exécute, vous devez disposer du package Aspose.OCR. Il est distribué via PyPI, donc une seule commande pip suffit.

```bash
pip install aspose-ocr
```

> **Astuce pro :** Si vous travaillez dans un environnement virtuel (fortement recommandé), activez‑le d'abord pour garder les dépendances isolées.

## Étape 2 : Importer le module et créer le moteur OCR

Maintenant que la bibliothèque est disponible, importez‑la et créez un `OcrEngine`. Pensez au moteur comme le cerveau qui effectue tout le travail lourd — reconnaissance des caractères, gestion des mises en page, et renvoi de chaînes Unicode propres.

```python
# Step 2: Import the Aspose OCR module and create an engine
import aspose.ocr as ocr

engine = ocr.OcrEngine()
```

> **Pourquoi c’est important :** Instancier le moteur une seule fois et le réutiliser pour toutes les pages est beaucoup plus efficace que de créer un nouveau moteur par page. Cela garantit également des paramètres cohérents tout au long du document.

## Étape 3 : Reconnaître toutes les pages d'un PDF (OCR multi‑pages)

La méthode `recognize_multi_page` d'Aspose.OCR accepte un chemin de fichier et renvoie une liste d'objets `OcrResult`—un par page. C’est le cœur de notre opération **convertir pdf en texte**.

```python
# Step 3: Run OCR on every page of the PDF
pdf_path = "YOUR_DIRECTORY/contract.pdf"   # replace with your actual file
pdf_pages = engine.recognize_multi_page(pdf_path)  # returns List[OcrResult]
```

> **Cas limite :** Si le PDF est protégé par mot de passe, vous devrez fournir le mot de passe via `engine.set_password("your_password")` avant d’appeler `recognize_multi_page`.

## Étape 4 : Parcourir les résultats et afficher un aperçu

Un aperçu rapide vous aide à vérifier que l'OCR capte bien le texte. Nous afficherons les 200 premiers caractères de chaque page, mais vous pouvez ajuster la tranche selon vos besoins.

```python
# Step 4: Display a short preview of each page’s extracted text
for page_number, page_result in enumerate(pdf_pages, start=1):
    print(f"--- Page {page_number} ---")
    # Show the first 200 characters of the page's OCR text
    print(page_result.text[:200])
    print()  # blank line for readability
```

**Exemple de sortie**

```
--- Page 1 ---
This Agreement is made on the 1st day of January 2025 between ...

--- Page 2 ---
WHEREAS, the Parties desire to enter into a collaborative ...

--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed this Agreement ...
```

Ce qui précède ne montre qu'un extrait, mais le texte complet se trouve dans `page_result.text`.

## Étape 5 : Combiner toutes les pages en un seul fichier texte (optionnel)

La plupart des flux de travail en aval—indexation de recherche, analyse de données ou archivage simple—préfèrent un fichier `.txt` unique. Concatenons les pages et écrivons le résultat.

```python
# Step 5: Save the complete OCR output to a .txt file
output_path = "YOUR_DIRECTORY/contract_extracted.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    for page_result in pdf_pages:
        out_file.write(page_result.text)
        out_file.write("\n\n")  # separate pages with a blank line
print(f"All pages saved to {output_path}")
```

> **Pourquoi cela fonctionne :** Utiliser UTF‑8 garantit que vous ne perdez pas les caractères spéciaux comme les lettres accentuées ou les symboles qui apparaissent souvent dans les documents juridiques.

## Étape 6 : Gestion des pièges courants

| Problème | Symptom | Solution |
|----------|---------|----------|
| Pages blanches dans la sortie | `page_result.text` est vide | Vérifiez que le PDF source contient bien des images numérisées ; certains PDF sont déjà basés sur du texte et nécessitent une approche différente (par ex. bibliothèques d'extraction de texte PDF). |
| Caractères illisibles | Symboles étranges au lieu de lettres | Assurez‑vous que la langue du moteur OCR est correctement définie : `engine.language = ocr.Language.English` (ou une autre langue). |
| PDF volumineux très lent | Le script semble bloqué sur une page | Activez le multithreading : `engine.recognize_multi_page(pdf_path, ocr.RecognizeOptions(parallel=True))`. |
| Erreurs de mémoire sur de gros fichiers | `MemoryError` levée | Traitez le PDF par blocs (par ex. 50 pages à la fois) ou augmentez la limite de mémoire de Python. |

## Script complet – Prêt à l'exécution

En réunissant tous les éléments, voici le script complet et autonome que vous pouvez copier‑coller dans un fichier nommé `extract_pdf_text_ocr.py`.

```python
# extract_pdf_text_ocr.py
# Complete python ocr example that extracts PDF text using Aspose OCR.

import aspose.ocr as ocr

def main():
    # 1️⃣ Install the library via `pip install aspose-ocr` before running.
    # 2️⃣ Set the path to your PDF.
    pdf_path = "YOUR_DIRECTORY/contract.pdf"
    output_path = "YOUR_DIRECTORY/contract_extracted.txt"

    # 3️⃣ Create the OCR engine.
    engine = ocr.OcrEngine()
    # Optional: set language for better accuracy.
    # engine.language = ocr.Language.English

    # 4️⃣ Perform multi‑page OCR.
    pdf_pages = engine.recognize_multi_page(pdf_path)

    # 5️⃣ Show a preview of each page.
    for page_number, page_result in enumerate(pdf_pages, start=1):
        print(f"--- Page {page_number} ---")
        print(page_result.text[:200])
        print()

    # 6️⃣ Write the full text to a file.
    with open(output_path, "w", encoding="utf-8") as out_file:
        for page_result in pdf_pages:
            out_file.write(page_result.text)
            out_file.write("\n\n")
    print(f"✅ All pages saved to {output_path}")

if __name__ == "__main__":
    main()
```

Exécutez‑le depuis votre terminal :

```bash
python extract_pdf_text_ocr.py
```

Vous devriez voir les aperçus de pages affichés dans la console, suivis d’une confirmation indiquant que le texte complet a été enregistré.

## Récapitulatif & étapes suivantes

Nous venons de démontrer comment **extraire du texte PDF OCR** à l'aide d'un **exemple python ocr** qui **convertit un pdf en texte** de manière efficace. Les étapes clés—installation, importation, création du moteur, appel à `recognize_multi_page`, aperçu et sauvegarde—couvrent le flux de travail le plus courant pour les PDF numérisés.

**Et après ?**  

- **Affiner la précision** : jouez avec `engine.recognize_multi_page(..., RecognizeOptions(...))` pour ajuster le DPI ou utiliser des packs de langues.  
- **Post‑traitement** : supprimez les espaces superflus, lancez une vérification orthographique, ou alimentez le texte dans un pipeline de traitement du langage naturel.  
- **Traitement par lots** : bouclez sur un dossier de PDF pour créer une archive consultable.  

Si vous rencontrez des difficultés, vérifiez que le PDF contient réellement des images raster (l'OCR agit sur des images, pas sur du texte intégré). Pour les PDF déjà textuels, envisagez des bibliothèques comme `pdfminer.six` ou `PyMuPDF`.

---

**Bon codage !** Si ce guide vous a aidé à **extraire du texte PDF OCR** pour votre projet, n'hésitez pas à partager vos résultats dans les commentaires, ou à ouvrir une issue sur la page GitHub d'Aspose OCR pour des demandes de fonctionnalités. Continuez d'expérimenter, et vous disposerez bientôt d'un pipeline robuste qui transforme n'importe quel PDF numérisé en texte consultable et modifiable.


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code fonctionnels complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}