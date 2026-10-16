---
category: general
date: 2026-06-06
description: Comment faire de l'OCR sur un PDF avec Python, extraire le texte d'un
  PDF, convertir le texte d'un PDF numérisé et changer la langue de l'OCR en quelques
  lignes de code seulement.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert scanned pdf text
- perform ocr on pdf
- change ocr language
language: fr
og_description: 'Comment faire de l''OCR sur un PDF avec Python : un guide pratique
  qui vous montre comment extraire du texte d’un PDF, convertir le texte d’un PDF
  scanné et changer la langue de l’OCR sans effort.'
og_title: Comment faire de l'OCR d'un PDF en Python – Tutoriel complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Python, extract text from PDF, convert scanned
    PDF text, and change OCR language in just a few lines of code.
  headline: How to OCR PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Comment faire de l’OCR d’un PDF en Python – Guide complet étape par étape
url: /fr/python-java/general/how-to-ocr-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR sur un PDF en Python – Guide complet étape par étape

Vous vous êtes déjà demandé **comment faire de l'OCR sur un PDF** sans payer pour des outils SaaS coûteux ? Vous n'êtes pas le seul. Que vous numérisiez de vieux livres, extrayiez des données de factures, ou que vous ayez simplement besoin d'un texte consultable à partir d'un rapport numérisé, maîtriser l'OCR de PDF en Python peut vous faire gagner des heures de copie manuelle.

Dans ce tutoriel, nous parcourrons un exemple concis et fonctionnel qui **extrait du texte d'un PDF**, vous montre comment **convertir le texte d'un PDF numérisé** en chaînes éditables, et même comment **changer la langue de l'OCR** si votre document n’est pas en anglais. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet.

## Prérequis et configuration

Avant de plonger, assurez‑vous d’avoir :

- Python 3.8+ installé (le code fonctionne sur 3.9, 3.10 et versions ultérieures)
- Le package `ocr` qui fournit la classe `OcrEngine` (vous pouvez l’installer via `pip install ocr-lib` – remplacez par le vrai nom du package que vous utilisez)
- Un fichier PDF que vous souhaitez traiter ; pour la démonstration nous utiliserons `high_res_book.pdf` placé dans un dossier appelé `YOUR_DIRECTORY`

If you’re using a virtual environment (highly recommended), activate it first:

```bash
python -m venv .venv
source .venv/bin/activate   # on Windows: .venv\Scripts\activate
pip install ocr-lib
```

> **Astuce :** Conservez vos fichiers PDF dans un répertoire dédié `data/` afin d’éviter des problèmes de chemins plus tard.

## Étape 1 : Créer une instance du moteur OCR (Comment faire de l'OCR sur un PDF – Initialisation)

La toute première chose à faire lorsque vous souhaitez **effectuer de l'OCR sur des PDF** est d’instancier le moteur. Pensez au moteur comme le cerveau qui lira chaque page, interprétera les glyphes et vous rendra du texte brut.

```python
# Step 1: Create an OCR engine instance
engine = OcrEngine()
```

Pourquoi c’est important : sans moteur, vous n’avez aucun contexte pour les paramètres de langue, les options de rendu ou la gestion du PDF. L’objet `OcrEngine` contient toutes ces valeurs par défaut et vous permet de les ajuster ultérieurement.

## Étape 2 : Définir la langue de reconnaissance (Changer la langue de l'OCR)

La plupart des bibliothèques OCR utilisent l'anglais par défaut, mais que faire si votre document est en français, allemand ou même japonais ? Changer la langue est aussi simple que d’appeler `set_recognition_language`. Cela répond à l’exigence de **changer la langue de l'OCR** et garantit une meilleure précision.

```python
# Step 2: Set the recognition language to English (or any supported language)
engine.set_recognition_language(ocr.Language.ENGLISH)   # swap ENGLISH for FRANCAIS, etc.
```

> **Pourquoi vous pourriez en avoir besoin :** Une archive multilingue contient souvent des pages à langues mixtes. Changer de langue à la volée évite la mauvaise reconnaissance de caractères comme “ß” ou “ñ”.

## Étape 3 : Configurer les options de rendu du PDF (Convertir efficacement le texte d’un PDF numérisé)

Lorsqu’on travaille avec des PDF numérisés, la résolution et le mode couleur influencent fortement la qualité de l’OCR. Un rendu à 300 DPI en niveaux de gris est un bon compromis pour la plupart des documents — assez élevé pour capturer les détails, mais suffisamment bas pour garder une utilisation de mémoire raisonnable.

```python
# Step 3: Configure PDF rendering options (300 DPI, grayscale)
engine.pdf_render_options() \
      .set_dpi(300) \
      .set_color_mode("grayscale")
```

Les appels en chaîne peuvent sembler sophistiqués, mais ils ne sont qu’une API fluide qui renvoie le même objet d’options à chaque fois. Si vous avez besoin de couleur (par ex., pour des diagrammes en couleur), remplacez `"grayscale"` par `"color"`.

## Étape 4 : Reconnaître le PDF et récupérer le texte de la première page (Extraire du texte d’un PDF)

Voici le cœur du **comment faire de l'OCR sur un PDF** : fournir au moteur le chemin du fichier et extraire le texte reconnu. La méthode renvoie une liste de résultats de pages ; chaque résultat possède un attribut `text`.

```python
# Step 4: Recognize the PDF and print the text of the first page
results = engine.recognize_pdf("YOUR_DIRECTORY/high_res_book.pdf")
print(results[0].text)   # Text from the first page
```

Si vous avez besoin du document complet, itérez sur `results` :

```python
for i, page in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(page.text)
```

### Et si le PDF est chiffré ?

Certains PDF sont protégés par mot de passe. Dans ce cas, vous pouvez transmettre le mot de passe à `recognize_pdf` :

```python
results = engine.recognize_pdf(
    "YOUR_DIRECTORY/secure_doc.pdf",
    password="mySecret123"
)
```

Le moteur déchiffrera à la volée avant d’effectuer l’OCR—aucune étape supplémentaire n’est nécessaire.

## Étape 5 : Post‑traitement du texte extrait (Affiner l’extraction du texte d’un PDF)

La sortie brute de l’OCR contient souvent des sauts de ligne, des espaces superflus ou des caractères mal reconnus. Une routine de nettoyage rapide rend la chaîne extraite prête pour le traitement en aval (indexation de recherche, stockage en base de données, etc.).

```python
import re

def clean_ocr_text(raw: str) -> str:
    # Remove multiple spaces and line breaks
    text = re.sub(r'\s+', ' ', raw)
    # Strip leading/trailing whitespace
    return text.strip()

clean_text = clean_ocr_text(results[0].text)
print(clean_text)
```

Vous pouvez maintenant **extraire du texte d’un PDF** en toute sécurité et l’alimenter dans n’importe quel pipeline NLP, moteur de recherche ou opération simple `open(...).write()`.

## Bonus : Traitement par lots de plusieurs PDF (Faire de l'OCR sur des PDF à grande échelle)

Si vous avez un dossier rempli de PDF numérisés, encapsulez la logique dans une boucle :

```python
import pathlib

pdf_folder = pathlib.Path("YOUR_DIRECTORY")
for pdf_path in pdf_folder.glob("*.pdf"):
    print(f"Processing {pdf_path.name} …")
    pages = engine.recognize_pdf(str(pdf_path))
    full_text = "\n".join(page.text for page in pages)
    cleaned = clean_ocr_text(full_text)

    # Save the extracted text alongside the PDF
    txt_path = pdf_path.with_suffix(".txt")
    txt_path.write_text(cleaned, encoding="utf-8")
    print(f"Saved extracted text to {txt_path.name}")
```

Cet extrait montre comment **effectuer de l'OCR sur des PDF** en masse, un besoin fréquent pour les projets de numérisation.

## Résultat attendu

L’exécution de l’exemple d’une seule page (Étape 4) devrait afficher quelque chose comme :

```
In the beginning God created the heavens and the earth. Now the earth was formless …
```

Si vous avez traité un livre multi‑pages, la console affichera le texte nettoyé de chaque page, et le script de traitement par lots laissera un fichier `.txt` à côté de chaque PDF.

## Problèmes courants et comment les éviter

| Problème | Symptômes | Solution |
|----------|-----------|----------|
| PDF source à basse résolution | Caractères brouillés, mots manquants | Augmenter le DPI (`set_dpi(400)` ou plus) |
| Mauvaise langue définie | De nombreux symboles inconnus, surtout les caractères accentués | Utiliser `engine.set_recognition_language(ocr.Language.FRENCH)` ou l’énumération appropriée |
| Grand PDF provoquant une erreur de mémoire | `MemoryError` ou plantage après quelques pages | Traiter les pages par lots (`engine.recognize_pdf(..., max_pages=10)`) |
| Polices manquantes dans le PDF | Sortie vide pour certaines pages | Vérifier que le PDF contient réellement des images raster ; certains PDF sont uniquement vectoriels et nécessitent une prise en charge différente |

## Illustration d’image

Voici une illustration rapide du flux de travail. Le texte alternatif est délibérément optimisé pour le SEO.

![diagramme du flux de travail de comment faire de l'ocr pdf montrant l'initialisation du moteur, le réglage de la langue, les options de rendu, la reconnaissance et l'extraction du texte](/images/ocr-workflow.png)

*Le diagramme n’est pas requis pour que le code fonctionne, mais il aide les apprenants visuels à voir où chaque étape s’insère.*

## Conclusion

Nous avons couvert **comment faire de l'OCR sur des PDF** en Python du début à la fin : création d’un moteur OCR, **changement de la langue de l'OCR**, configuration du rendu pour **convertir le texte d’un PDF numérisé**, et enfin **extraction du texte d’un PDF** pour une utilisation ultérieure. L’exemple complet et exécutable est prêt à être intégré à n’importe quel projet, et le script de traitement par lots optionnel vous montre comment mettre l’application à l’échelle.

Ensuite, vous pourriez explorer :

- Ajouter **perform OCR on PDF** pour les archives multilingues en parcourant une liste de langues.
- Intégrer le texte extrait avec Elasticsearch pour la recherche en texte intégral.
- Utiliser l’OCR pour créer des PDF consultables en incorporant la couche de texte dans le fichier original (de nombreuses bibliothèques exposent une méthode `save_as_searchable_pdf`).

N’hésitez pas à expérimenter, ajuster les paramètres DPI, ou passer à un autre moteur OCR. Les principes restent les mêmes, et vous disposez désormais d’une base solide sur laquelle construire.

Bon codage, et que vos documents numérisés deviennent enfin consultables !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}