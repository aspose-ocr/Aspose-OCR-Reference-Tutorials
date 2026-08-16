---
category: general
date: 2026-04-26
description: 'Comment faire de l''OCR en Python : apprenez à extraire du texte d’une
  image et à lire un fichier TIFF en Python à l’aide d’un exemple d’OCR basique. Code
  rapide et exécutable inclus.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: fr
og_description: 'comment faire de l''OCR en Python : un guide étape par étape qui
  montre comment extraire du texte d’une image, lire un fichier TIFF avec Python et
  convertir le texte d’une image numérisée avec un script simple et exécutable.'
og_title: Comment faire de l'OCR avec Python – Exemple basique d'OCR pour extraire
  du texte
tags:
- OCR
- Python
- Image Processing
title: Comment faire de l'OCR en Python – Exemple de base d'OCR pour extraire du texte
url: /fr/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment faire de l'ocr python – Exemple basique d'OCR pour extraire du texte

Vous êtes-vous déjà demandé **how to ocr python** lorsque vous avez un fichier TIFF numérisé sur votre bureau ? Vous n'êtes pas le seul à fixer une pile de fichiers image en vous demandant « Comment extraire les mots de ceci ? ». La bonne nouvelle, c’est que transformer une image en texte brut est un jeu d’enfant avec la bonne bibliothèque et quelques étapes claires.

Dans ce tutoriel, nous allons parcourir un **basic OCR example** qui lit un fichier TIFF, extrait le texte et l’affiche dans la console. À la fin, vous saurez exactement comment **extract text from image** des fichiers, comment gérer les particularités des formats TIFF, et quoi ajuster si vous devez **convert scanned image text** en quelque chose de plus utile. Pas de magie cachée — juste du Python simple que vous pouvez copier‑coller et exécuter dès aujourd’hui.

## Ce dont vous avez besoin

- Python 3.9+ installé (la dernière version stable est recommandée).
- Une bibliothèque OCR installable via pip. Pour ce guide, nous utiliserons le package fictif `aocr` qui imite des outils populaires comme Tesseract ; vous pourrez le remplacer par `pytesseract` ou `easyocr` plus tard.
- Une image TIFF que vous souhaitez traiter – nommez‑la `input.tiff` et placez‑la dans un dossier que vous référencerez dans le code.
- Une connaissance de base de la ligne de commande (juste pour installer le package).

C’est tout. Pas de dépendances lourdes, pas de conteneurs Docker, juste quelques lignes de code.

## Étape 1 – Installer et importer les dépendances (how to ocr python)

Tout d’abord, obtenez le package OCR. Ouvrez un terminal et exécutez :

```bash
pip install aocr
```

Si vous préférez une bibliothèque du monde réel, remplacez `aocr` par `pytesseract` et installez séparément le moteur Tesseract.

Ensuite, importez ce dont nous avons besoin. La classe `Path` de `pathlib` nous offre une façon propre de travailler avec les chemins de fichiers sur tous les systèmes d’exploitation.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Pourquoi utiliser `Path` ?* Parce qu’elle abstrait les séparateurs (`/` vs `\`) et vous permet de joindre des répertoires sans vous soucier du système sous‑jacent. Ce petit détail évite souvent bien des maux de tête lorsqu’on déplace le script vers un serveur CI.

## Étape 2 – Créer l'instance du moteur OCR (basic ocr example)

Ensuite, lancez le moteur OCR. Pensez à `OcrEngine` comme le cerveau qui lira l’image et produira des caractères.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

La plupart des bibliothèques OCR vous permettent d’ajuster la langue, le DPI ou les seuils de confiance ici. Pour ce **basic OCR example**, nous resterons sur les valeurs par défaut, mais vous pourrez explorer `ocr_engine.config` plus tard si vous devez gérer des documents multilingues.

## Étape 3 – Charger votre image TIFF (read tiff file python)

Voici où intervient la partie **read tiff file python**. Les TIFF peuvent être multi‑pages, mais `Image.load` récupère la première page par défaut — parfait pour un scan d’une seule page.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Remplacez `"YOUR_DIRECTORY"` par le dossier réel contenant `input.tiff`. Si vous ne savez pas où le script s’exécute, `Path.cwd()` affiche le répertoire de travail actuel — utile pour déboguer les problèmes de chemin.

## Étape 4 – Exécuter le processus OCR (extract text from image)

Maintenant, la magie opère. Appeler `process()` envoie l’image à travers le pipeline OCR et renvoie un objet résultat.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

En coulisses, le moteur peut convertir l’image en niveaux de gris, appliquer un seuillage, puis la transmettre à un réseau de neurones. Vous n’avez pas besoin de gérer ces étapes ; la bibliothèque les abstrait.

## Étape 5 – Afficher le texte reconnu (convert scanned image text)

Enfin, affichez le texte. Dans des projets réels, vous écririez probablement dans un fichier ou une base de données, mais l’impression garde l’exemple simple.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Lorsque vous exécuterez le script, vous devriez voir quelque chose comme :

```
Hello, world!
This is a sample scanned document.
```

Si la sortie apparaît brouillée, revérifiez que l’image source est nette et que la langue OCR correspond au texte.

## Script complet fonctionnel

En rassemblant le tout, voici le programme complet, prêt à être exécuté :

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Sortie attendue

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Si vous avez besoin de **convert scanned image text** en PDF recherchable, vous pouvez acheminer `ocr_result.text` vers un générateur de PDF comme `reportlab` — mais cela constitue un tutoriel à part entière.

## Pièges courants & astuces pro

- **Low‑resolution scans** : l’OCR a du mal en dessous de 150 DPI. Si votre TIFF est flou, rééchantillonnez‑le d’abord avec Pillow (`Image.open(...).resize(...)`).
- **Multiple pages** : pour les TIFF multi‑pages, itérez sur `Image.load_multi_page()` (si votre bibliothèque le supporte) et concaténez les résultats.
- **Language support** : de nombreux moteurs utilisent l’anglais par défaut. Définissez `ocr_engine.language = "spa"` pour le espagnol, par exemple.
- **Whitespace handling** : l’OCR ajoute souvent des sauts de ligne parasites. Utilisez `str.splitlines()` ou des expressions régulières pour nettoyer la sortie.
- **Performance** : pour un traitement en masse, réutilisez une seule instance de `OcrEngine` au lieu d’en créer une nouvelle pour chaque fichier.

## Étendre l'exemple

Maintenant que vous avez maîtrisé **how to ocr python** pour une image unique, envisagez les étapes suivantes :

1. **Batch processing** – Parcourez un répertoire de TIFF et écrivez chaque résultat dans un fichier `.txt`.
2. **Integration with Pandas** – Stockez le texte extrait avec les métadonnées pour une analyse rapide.
3. **Hybrid approach** – Combinez l’OCR avec des bibliothèques NLP comme `spaCy` pour extraire des entités (noms, dates, montants) à partir de factures numérisées.
4. **Alternative file formats** – Remplacez `Image.load` par `Image.from_bytes` pour gérer des images provenant d’une API ou d’une base de données.

Tous ces points s’appuient sur l’idée centrale d’**extract text from image** et de **convert scanned image text** en quelque chose que les machines peuvent comprendre.

## Conclusion

Nous avons parcouru un **basic OCR example** clair, de bout en bout, qui montre **how to ocr python**, comment **read tiff file python**, et comment **extract text from image** avec seulement quelques lignes. Le script est autonome, inclut la gestion des erreurs, et imprime directement le résultat, ce qui en fait une base solide pour tout projet nécessitant de transformer des documents numérisés en texte éditable.

N’hésitez pas à expérimenter — remplacez le backend OCR, ajustez le pré‑traitement, ou intégrez la sortie dans un flux de travail en aval. Le ciel est la limite quand vous pouvez convertir de façon fiable **convert scanned image text** en données recherchables.

Des questions sur les cas limites, les packs de langues ou l’optimisation des performances ? Laissez un commentaire ci‑dessous, et bon codage ! 

![exemple de how to ocr python](/images/ocr-python-example.png "Capture d'écran de la sortie du script how to ocr python")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}