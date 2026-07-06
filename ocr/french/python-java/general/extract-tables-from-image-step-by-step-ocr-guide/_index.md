---
category: general
date: 2026-03-26
description: Extraire des tableaux d’une image et convertir l’image en feuille de
  calcul à l’aide de l’OCR Python. Apprenez comment charger une image pour l’OCR,
  lire les tableaux et extraire les données du tableau.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: fr
og_description: Extraire des tableaux d’une image avec OCR Python. Ce guide montre
  comment charger l’image pour l’OCR, lire les tableaux et les convertir en feuille
  de calcul.
og_title: Extraire des tableaux d’une image – Tutoriel complet d’OCR
tags:
- OCR
- Python
- Data Extraction
title: Extraire des tableaux d’une image – Guide OCR étape par étape
url: /fr/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire des tableaux à partir d’une image – Tutoriel OCR complet

Vous avez déjà eu besoin d'**extraire des tableaux d’une image** sans savoir par où commencer ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu’un PDF ou une capture d’écran contient des données tabulaires qui doivent devenir des lignes et colonnes éditables. La bonne nouvelle ? Quelques lignes de code Python, associées à un moteur OCR performant, peuvent transformer cette image en une feuille de calcul exploitable en quelques secondes.

Dans ce tutoriel, nous allons parcourir le chargement d’une image pour l’OCR, l’exécution du moteur de reconnaissance, et l’extraction de chaque tableau ligne par ligne. À la fin, vous pourrez **convertir une image en feuille de calcul**, et vous verrez aussi comment **ocr read tables** et **ocr extract table data** pour un traitement en aval. Aucun tour de magie caché, juste du code clair et exécutable que vous pouvez intégrer dès aujourd’hui à votre projet.

---

## Ce dont vous avez besoin

Avant de plonger, assurez‑vous d’avoir les éléments suivants à portée de main :

- **Python 3.9+** – la dernière version stable fonctionne le mieux.  
- La bibliothèque **`ocr`** (ou tout SDK OCR compatible exposant `OcrEngine`, `Image` et les méthodes liées aux tableaux). Installez‑la avec `pip install ocr‑sdk` (remplacez par le nom réel du paquet).  
- Un fichier image (`.png`, `.jpg`, etc.) contenant un tableau clairement imprimé.  
- Optionnel : **pandas** si vous souhaitez écrire les données extraites directement dans un fichier CSV ou Excel (`pip install pandas`).

Tout est‑t‑il prêt ? Super—c’est parti.

---

## Étape 1 : Importer le SDK OCR et préparer votre environnement

Première chose à faire : importer les classes OCR dans notre script et mettre en place un petit utilitaire qui transformera plus tard les données brutes du tableau en DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Pourquoi c’est important :** L’import de `ocr` nous donne accès à `OcrEngine`, `Imaging.Image` et aux objets tableau que nous parcourrons. `pandas` n’est pas obligatoire pour l’extraction, mais il rend la partie **convertir image en feuille de calcul** très simple.

---

## Étape 2 : Charger l’image à traiter

Nous allons maintenant **charger l’image pour l’OCR**. Le SDK attend un objet `Image`, nous allons donc envelopper le chemin du fichier avec la méthode d’aide `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Astuce :** Conservez vos fichiers image dans un dossier dédié (`assets/` ou `data/`) et utilisez des chemins relatifs. Ainsi le script reste portable d’une machine à l’autre.

---

## Étape 3 : Exécuter le processus de reconnaissance

Une fois l’image attachée, nous pouvons enfin demander au moteur d'**ocr read tables**. L’appel `recognize()` renvoie un objet résultat contenant tout ce que le moteur a découvert — blocs de texte, lignes et, surtout pour nous, les tableaux.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Pourquoi vérifier :** Certaines images peuvent être bruyantes ou les bordures du tableau trop faibles, ce qui empêche le moteur de les détecter. Journaliser un avertissement vous donne un retour rapide sans interrompre le script.

---

## Étape 4 : Extraire les lignes et les cellules de chaque tableau

C’est ici que la vraie magie opère. Nous allons parcourir chaque tableau détecté, extraire chaque ligne, puis le texte de chaque cellule. La compréhension de liste interne rend le code concis, mais nous expliquerons tout de même le flux.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Que se passe‑t‑il ?**  

- `enumerate(..., start=1)` nous fournit un numéro de tableau lisible pour les logs.  
- `row_obj.get_cells()` renvoie chaque objet cellule ; `cell.get_text()` récupère la chaîne décodée par l’OCR.  
- Nous stockons les lignes dans `rows_data`, puis les transmettons à `pandas.DataFrame` qui aligne automatiquement les colonnes.  
- Le bloc `print` reproduit la **sortie essentielle** montrée dans l’extrait original, afin que vous puissiez vérifier les résultats immédiatement.

**Gestion des cas limites :** Si une ligne possède un nombre de cellules différent des autres, `pandas` remplira les cases manquantes avec `NaN`. Vous pourrez ensuite nettoyer le DataFrame avec `df.fillna('')` si vous préférez des chaînes vides.

---

## Étape 5 : Enregistrer les tableaux extraits dans une feuille de calcul

Maintenant que nous disposons d’une liste de DataFrames, les transformer en classeur Excel (ou fichiers CSV) devient un jeu d’enfant. Cela répond à l’objectif **convertir image en feuille de calcul**.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Pourquoi Excel ?** La plupart des utilisateurs métier préfèrent le format `.xlsx`. Si vous préférez le CSV, remplacez la boucle par `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Script complet, prêt à l’emploi

En rassemblant le tout, voici le programme complet que vous pouvez copier‑coller et exécuter.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Sortie console attendue** (pour un tableau simple 2×3) :

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Et vous trouverez `extracted_tables.xlsx` dans le répertoire du script, chaque tableau étant placé sur une feuille distincte.

---

## Questions fréquentes & Astuces

| Question | Réponse |
|----------|---------|
| **Puis‑je utiliser une autre bibliothèque OCR ?** | Absolument. Le principe reste le même : charger l’image → reconnaître → parcourir `get_tables()`. Il suffit de remplacer les importations et les noms d’objets. |
| **Que faire si mon image est bruitée ?** | Pré‑traitez avec OpenCV (seuillage, redressement) avant de la transmettre au moteur OCR. La réduction du bruit améliore souvent la précision de **ocr extract table data**. |
| **Dois‑je installer `openpyxl` ?** | Oui, `pandas` s’en sert en interne pour l’export Excel. Installez‑le avec `pip install openpyxl`. |
| **Comment gérer les cellules fusionnées ?** | Certains SDK exposent `cell.is_merged()` ; vous pouvez détecter et propager la valeur sur la plage fusionnée manuellement. |
| **Existe‑t‑il un moyen d’extraire uniquement certains tableaux ?** | Filtrez avec `table_obj.get_confidence()` ou en vérifiant des mots‑clés d’en‑tête avant le traitement. |

---

## Conclusion

Vous disposez maintenant d’une solution complète, de bout en bout, pour **extraire des tableaux d’une image**, convertir le résultat en une feuille de calcul propre, et même gérer plusieurs tableaux dans une même image. Le script montre comment **load image for OCR**, **ocr read tables**, et **ocr extract table data** tout en restant suffisamment flexible pour les variations du monde réel.

Et après ? Essayez de fournir au moteur OCR une page PDF rendue en image, ou expérimentez avec différentes langues et polices. Vous pouvez également acheminer les DataFrames directement vers une base de données ou un outil de reporting—votre imagination est la seule limite.

Si ce guide vous a été utile, n’hésitez pas à le partager, à étoiler le dépôt qui héberge le SDK, ou à laisser un commentaire avec vos propres astuces. Bon codage, et que vos tableaux soient toujours parfaitement analysés !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}