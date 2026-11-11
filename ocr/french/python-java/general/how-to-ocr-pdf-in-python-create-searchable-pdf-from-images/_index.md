---
category: general
date: 2026-06-06
description: Comment faire de l’OCR sur un PDF et créer des fichiers PDF recherchables
  à partir d’images avec Python. Apprenez à ajouter du texte recherchable et à convertir
  une image en PDF/A en quelques minutes.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: fr
og_description: Comment faire de l’OCR sur un PDF étape par étape. Apprenez à ajouter
  du texte recherchable et à convertir une image en PDF/A à l’aide d’un script Python
  simple.
og_title: Comment faire de l'OCR d'un PDF – Guide rapide pour créer des PDF recherchables
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Comment faire de l'OCR d'un PDF en Python – Créer un PDF consultable à partir
  d'images
url: /fr/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment OCR un PDF – Transformer des images numérisées en PDF recherchables

Vous vous êtes déjà demandé **comment OCR un PDF** lorsqu’il ne vous reste qu’une image numérisée d’une facture ou d’un reçu ? Vous n’êtes pas le seul. Dans de nombreux bureaux, les documents entrants arrivent sous forme de PNG ou JPEG plats, et l’étape suivante—rendre ce contenu interrogeable—semble être une boîte noire.  

La bonne nouvelle ? En quelques lignes de Python, vous pouvez **créer des PDF recherchables**, **ajouter du texte interrogeable**, et même **convertir une image en PDF/A** pour l’archivage à long terme. Dans ce tutoriel, nous parcourrons chaque étape, expliquerons pourquoi elle est importante, et vous fournirons un script prêt à l’emploi que vous pourrez intégrer à n’importe quel projet.

> **Astuce :** La même approche fonctionne pour les numérisations multi‑pages ; il suffit de boucler sur les fichiers et le moteur se charge du travail lourd.

---

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir les éléments suivants sur votre machine :

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| Python 3.9 ou plus récent | Syntaxe moderne et meilleure prise en charge des bibliothèques |
| Moteur OCR basé sur `pdfium` (par ex., `pdfocr` ou un SDK commercial) | Gère à la fois la reconnaissance d’image et la génération de PDF/A |
| Un fichier image (PNG, JPEG, TIFF) que vous souhaitez transformer en PDF recherché | La source du texte |
| Permission d’écriture sur le dossier de sortie | Pour que le script puisse enregistrer le nouveau PDF |

Si vous n’avez pas encore installé le SDK OCR, exécutez :

```bash
pip install pdfocr   # replace with your vendor's package name
```

C’est tout — aucune dépendance système complexe, juste un `pip install`.

---

## Comment OCR un PDF – Vue d’ensemble

À haut niveau, le processus se compose de trois actions simples :

1. **Reconnaître** le texte présent dans l’image tout en conservant les graphiques d’origine.  
2. **Exporter** le résultat OCR avec l’image originale sous forme de **PDF/A recherché** (la variante PDF adaptée à l’archivage).  
3. **Valider** que le fichier résultant contient du texte sélectionnable, superposé à l’image d’origine.

Vous verrez ci‑dessous chaque étape en code, avec les explications du *pourquoi* derrière les commandes.

---

## Étape 1 : Reconnaître le texte à partir de l’image

Dans un premier temps, nous demandons au moteur OCR de lire les pixels et de renvoyer un objet résultat contenant à la fois l’image brute et le texte extrait. Pensez‑y comme le moteur « lisant » la facture pour vous.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Pourquoi c’est important

- **Conserver les graphiques** signifie que la mise en page visuelle (tableaux, logos, tampons) reste exactement telle que le scanner l’a capturée.  
- L’objet `result` contient généralement une couche de texte cachée que nous intégrerons plus tard dans le PDF.  
- Utiliser `recognize_image` au lieu de `recognize_pdf` évite une étape de conversion supplémentaire, ce qui accélère le traitement des images mono‑page.

#### Variantes courantes

- Si vous avez un **TIFF multi‑pages**, passez le chemin du fichier directement ; la plupart des moteurs traiteront chaque page comme une image séparée.  
- Pour les PDF contenant déjà des images, vous pouvez appeler `engine.recognize_pdf("file.pdf")` et ignorer complètement cette étape.

---

## Étape 2 : Exporter le résultat OCR en PDF/A recherché

Nous prenons maintenant le `result` de l’étape 1 et demandons au moteur d’écrire un nouveau fichier. Le drapeau clé ici est *PDF/A* — la version normalisée ISO du PDF conçue pour la préservation à long terme.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Pourquoi c’est important

- **PDF recherché** : Le fichier de sortie contient une couche de texte cachée et sélectionnable. Vous pouvez maintenant faire Ctrl + F dans le document.  
- **Conformité PDF/A** : Certaines organisations (juridiques, financières) exigent le PDF/A pour les archives ; cette étape satisfait automatiquement cette contrainte.  
- La méthode **ajoute du texte recherché** sans aplatir l’image, de sorte que la fidélité visuelle reste parfaite.

#### Cas particulier : besoin d’un PDF standard ?

Si le PDF/A ne vous intéresse pas, remplacez `save_as_pdfa` par `save_as_pdf`. Le reste du flux de travail reste identique.

---

## Étape 3 : Vérifier le PDF recherché

Une vérification rapide vous évite des bugs mystérieux plus tard. Ouvrez le fichier généré dans n’importe quel lecteur PDF, essayez de sélectionner un mot, et utilisez la fonction de recherche.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Résultat attendu

Lorsque vous exécutez le script, la console affiche :

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

En ouvrant le fichier, vous devez voir l’image originale de la facture avec une fine couche de texte invisible. Sélectionnez n’importe quel mot ; il sera sélectionnable—**c’est le texte recherché** que vous venez d’ajouter.

---

## Ajouter du texte recherché à des PDF existants (Bonus)

Parfois, vous avez déjà un PDF mais devez **ajouter du texte recherché**. Le même moteur peut superposer les résultats OCR sur un PDF existant :

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Ici, `apply_to` fusionne la couche cachée avec les pages originales, vous permettant de **créer un PDF recherché** sans rescanner.

---

## Pièges courants et astuces

| Piège | Comment l’éviter |
|-------|-------------------|
| **Images sources à basse résolution** (< 150 dpi) | Agrandir ou demander un scan à plus haute résolution ; la précision de l’OCR chute fortement en dessous de 150 dpi. |
| **Données linguistiques manquantes** | Installez les packs de langues appropriés pour votre moteur OCR (`pip install pdfocr[eng,spa]`). |
| **Dossier de sortie non inscriptible** | Exécutez le script avec les permissions suffisantes ou choisissez un autre répertoire. |
| **Échec de validation PDF/A** | Assurez‑vous de ne pas incorporer de polices ou de JavaScript non supportés ; la plupart des SDK gèrent cela automatiquement avec `save_as_pdfa`. |

---

## Script complet – Solution en un seul fichier

Voici un script autonome qui réunit tous les éléments. Copiez‑collez‑le, remplacez les chemins factices, et vous êtes prêt à **convertir une image en PDF/A** en quelques secondes.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Ce que fait ce script :**  
1. Charge le moteur OCR.  
2. Lit l’image choisie et extrait le texte.  
3. Écrit un **PDF/A recherché** que vous pouvez immédiatement distribuer ou archiver.  

N’hésitez pas à encapsuler la logique `main` dans une fonction qui traite un dossier complet — il suffit d’itérer sur `os.listdir()` et de répéter les trois étapes pour chaque fichier.

---

## Prochaines étapes & sujets connexes

Maintenant que vous avez maîtrisé **comment OCR un PDF**, explorez ces idées complémentaires :

- **Traitement par lots** : utilisez `concurrent.futures` pour OCRiser des dizaines de factures en parallèle.  
- **Injection de métadonnées** : ajoutez des dates de création ou des numéros de facture aux métadonnées du PDF pour faciliter l’indexation.  
- **PDF hybrides** : combinez texte recherché et images intégrées pour créer un « jumeau numérique » du document papier.  
- **Sorties alternatives** : exportez vers **DOCX** ou **HTML** si les systèmes en aval nécessitent des formats éditables.

Chacune de ces options s’appuie sur les concepts de base que vous venez d’apprendre — reconnaître, exporter, vérifier.

---

## Conclusion

En résumé, vous savez maintenant **comment OCR un PDF** en transformant une simple image en **PDF/A recherché** avec seulement trois lignes de Python. Le script se charge du travail lourd, préserve les graphiques d’origine, et vous fournit un document conforme aux normes que vous pouvez rechercher, archiver ou partager.  

Testez-le avec vos propres factures, reçus ou contrats numérisés. Si vous rencontrez des difficultés, laissez un commentaire ci‑dessous ou consultez la documentation officielle du SDK — elle regorge généralement d’exemples supplémentaires. Bon codage, et profitez de votre nouvelle capacité à rendre n’importe quelle image instantanément interrogeable ! 

![Exemple de comment OCR un PDF montrant l’image originale et la superposition du PDF recherché](placeholder.png "Exemple de comment OCR un PDF montrant l’image originale et la superposition du PDF recherché")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment OCR un PDF en .NET avec Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Reconnaître le texte d’un PDF – Opérations OCR avec Aspose.OCR pour Java](/ocr/english/java/ocr-operations/)
- [Convertir des images en PDF C# – Enregistrer le résultat OCR multi‑pages](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}