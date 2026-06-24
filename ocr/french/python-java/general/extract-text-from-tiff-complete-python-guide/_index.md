---
category: general
date: 2026-06-16
description: Extraire du texte à partir de fichiers TIFF avec l'OCR Python. Apprenez
  à convertir les TIFF en texte pas à pas, en gérant facilement les documents multi‑pages.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: fr
og_description: Extrayez du texte à partir de fichiers TIFF avec OCR en Python. Suivez
  ce guide pour convertir les TIFF en texte, gérer les numérisations multipages et
  obtenir des résultats propres.
og_title: Extraire du texte d’un TIFF – Guide complet Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Extraire du texte d’un TIFF – Guide complet Python
url: /fr/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d’un TIFF – Guide complet Python

Vous avez déjà eu besoin d’**extraire du texte d’un TIFF** mais vous ne saviez pas par où commencer ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils traitent des archives numérisées ou des documents anciens. La bonne nouvelle ? En quelques lignes de Python, vous pouvez **convertir un TIFF en texte** en un clin d’œil, même si le fichier contient des dizaines de pages.

Dans ce tutoriel, nous allons parcourir un exemple réel : charger un TIFF multi‑pages, définir la langue OCR sur le français, et extraire le texte reconnu de chaque page. À la fin, vous disposerez d’un script prêt à l’emploi, comprendrez pourquoi chaque étape est importante, et saurez comment l’adapter à d’autres langues ou formats d’image.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Python 3.8 ou une version plus récente installé.
- Le package `ocr` (ou toute bibliothèque OCR compatible offrant une classe `OcrEngine`). Vous pouvez l’installer avec `pip install ocr-lib` — remplacez‑le par le nom réel du package que vous utilisez.
- Un fichier TIFF multi‑pages (par ex. `french-scans.tif`) que vous souhaitez traiter.
- Une connaissance de base du scripting Python.

Pas de dépendances lourdes, pas de services externes — juste du Python pur et un moteur OCR.

---

## Étape 1 : Configurer le moteur OCR pour **extraire du texte d’un TIFF**

Tout d’abord, nous avons besoin d’une instance du moteur OCR et il faut indiquer la langue à utiliser. Dans notre cas, le matériel source est en français, nous allons donc définir la langue en conséquence.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Pourquoi c’est important :**  
Le réglage de la langue améliore considérablement la précision. Les caractères français comme « é » ou « ç » seraient mal interprétés comme des symboles génériques si le moteur restait sur l’anglais par défaut. En sélectionnant explicitement le français, nous fournissons au moteur la bonne table de caractères.

> **Astuce :** Si vous traitez des documents dans plusieurs langues, vous pouvez modifier `engine.language` à la volée avant chaque appel à `recognize()`.

---

## Étape 2 : Charger le TIFF multi‑pages que vous voulez **convertir en texte**

Un TIFF peut contenir plusieurs cadres — considérez chaque cadre comme une page distincte. La bibliothèque OCR abstrait cela pour nous, il suffit donc de pointer vers le fichier.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Avertissement sur les cas limites :**  
Si le chemin du fichier est incorrect ou si le TIFF est corrompu, la méthode `load_from_file` lèvera une exception. Enveloppez‑le dans un bloc `try/except` pour le code de production :

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Étape 3 : Exécuter l’OCR sur le document complet – Le cœur de **l’extraction de texte d’un TIFF**

Nous laissons maintenant le moteur faire sa magie. L’appel `recognize()` traite chaque page en une seule fois et renvoie un objet résultat riche.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Que se passe‑t‑il en coulisses ?**  
Le moteur parcourt chaque cadre, applique un pré‑traitement (redressement, binarisation), exécute le réseau neuronal, puis agrège le résultat. Parce que nous n’appelons `recognize()` qu’une seule fois, la bibliothèque peut partager les ressources entre les pages, ce qui est plus rapide qu’une boucle manuelle.

---

## Étape 4 : Extraire le texte reconnu du résultat JSON – **convertir le TIFF en texte** page par page

L’objet résultat peut être sérialisé en JSON. Dans ce JSON, vous trouverez un tableau `pages`, chaque élément contenant un champ `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Nous obtenons ainsi une liste Python propre où chaque élément correspond à la sortie OCR d’une page.

---

## Étape 5 : Afficher ou enregistrer le texte de chaque page – La pièce finale de **l’extraction de texte d’un TIFF**

Parcourons les pages et affichons le texte extrait. Vous pouvez également écrire chaque page dans un fichier `.txt` séparé si vous le préférez.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Résultat attendu (exemple)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Si l’OCR a réussi, vous verrez un bloc propre de phrases françaises pour chaque page. Si vous remarquez des caractères illisibles, revérifiez le réglage de la langue ou envisagez d’augmenter la résolution de l’image avant l’OCR.

---

## Gestion des problèmes courants lors de la **conversion d’un TIFF en texte**

| Problème | Pourquoi cela se produit | Solution rapide |
|----------|--------------------------|-----------------|
| **Tableau `pages` vide** | Le TIFF n’a pas été chargé correctement ou ne contient aucun cadre. | Vérifiez le chemin du fichier et assurez‑vous que le TIFF n’est pas un PNG mono‑page déguisé en TIFF. |
| **Caractères corrompus** | Incohérence de langue ou mauvaise qualité d’image. | Définissez la bonne `engine.language` et pré‑traitez l’image (par ex. augmentez le DPI). |
| **Consommation mémoire excessive sur de gros TIFF** | Charger toutes les pages d’un coup consomme beaucoup de RAM. | Traitez par lots : chargez un cadre, reconnaissez‑le, puis libérez‑le avant de passer au suivant. |
| **Erreurs Unicode lors de l’affichage** | Le codage du terminal ne supporte pas les caractères accentués. | Utilisez `print(page["text"].encode('utf-8').decode('utf-8'))` ou configurez votre console en UTF‑8. |

---

## Étendre le script : de **l’extraction de texte d’un TIFF** au traitement par lots

Maintenant que vous avez une base solide, pensez aux étapes suivantes :

1. **Conversion par lots** – Encapsulez le flux complet dans une fonction `def ocr_tiff(path):` et itérez sur un répertoire de fichiers TIFF.  
2. **Exportation vers des fichiers** – Au lieu d’afficher, écrivez le texte de chaque page dans `page_{i}.txt` ou concaténez‑le tout dans un seul document.  
3. **Moteurs OCR alternatifs** – Si vous avez besoin d’une précision supérieure, remplacez `ocr.OcrEngine()` par Tesseract (`pytesseract`) ou Azure Cognitive Services — tout en conservant la même logique « extraire du texte d’un TIFF ».  
4. **Post‑traitement** – Appliquez une correction orthographique, une détection de langue ou un nettoyage regex pour affiner la sortie brute de l’OCR.

---

## Script complet, prêt à l’exécution

Voici le code complet, prêt à être copié‑collé. Il inclut une gestion d’erreurs basique et la sauvegarde optionnelle du texte de chaque page dans des fichiers séparés.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Exécutez ce script, pointez `tiff_file` vers votre document, et observez la console se remplir de phrases françaises propres. Si vous avez indiqué `out_folder`, vous trouverez également une série de fichiers `page_#.txt` prêts pour les traitements en aval.

---

## Conclusion

Nous venons d’**extraire du texte d’un TIFF** à l’aide d’un flux OCR Python simple, et vous savez maintenant comment **convertir un TIFF en texte** de façon fiable. De l’initialisation du moteur avec la bonne langue à la boucle sur le résultat JSON de chaque page, chaque étape a été expliquée avec le « pourquoi », afin que vous puissiez adapter le modèle à d’autres langues, formats d’image ou traitements par lots plus importants.

Et après ? Essayez de remplacer le backend OCR par Tesseract, testez différents packs de langues, ou intégrez la sortie dans une base de données consultable. Le ciel est la limite quand vous pouvez transformer des images numérisées en texte recherchable.

N’hésitez pas à laisser un commentaire si vous rencontrez des difficultés ou avez des idées d’améliorations supplémentaires. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code fonctionnels complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités d’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}