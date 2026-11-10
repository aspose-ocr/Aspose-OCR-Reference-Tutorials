---
category: general
date: 2026-06-06
description: OCR d'image PNG avec Python – apprenez comment extraire du texte d'une
  image, exécuter un exemple d'OCR en Python et même lire facilement du texte grec
  ancien.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: fr
og_description: OCR d'image PNG en Python expliqué. Ce guide montre comment extraire
  du texte d’une image, exécuter un exemple d’OCR en Python et lire le grec ancien
  facilement.
og_title: OCR d'image PNG en Python – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR d'image PNG en Python – Guide complet étape par étape
url: /fr/python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR d'image PNG en Python – Guide complet étape par étape

Vous êtes‑vous déjà demandé comment **OCR PNG image** des fichiers directement depuis un script Python ? Peut‑être avez‑vous un dossier rempli de manuscrits anciens numérisés et vous devez **extract text from image** sans taper tout manuellement. La bonne nouvelle, c’est que vous n’avez pas besoin d’un doctorat en vision par ordinateur—juste quelques lignes de code et la bonne bibliothèque, et vous lirez du grec ancien en quelques secondes.

Dans ce tutoriel, nous parcourrons un **python OCR example** qui reconnaît le texte d’un PNG, définit la langue en grec polytonique, et affiche le résultat. À la fin, vous saurez exactement comment **recognize image text**, gérer les pièges courants, et adapter le script à d’autres langues ou formats d’image.

## Ce que vous apprendrez

- Installer et configurer une bibliothèque OCR Python (pytesseract + Tesseract OCR)
- Créer une instance du moteur OCR et charger un fichier PNG
- Définir la langue de reconnaissance en grec polytonique afin de pouvoir **read ancient greek**
- Produire le texte reconnu et dépanner les problèmes typiques
- Étendre le script pour traiter par lots plusieurs PNG ou passer à une autre langue

### Prérequis

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| Python 3.8+ | Syntaxe moderne et annotations de type |
| `pytesseract` package | Petit wrapper autour du moteur Tesseract |
| Tesseract OCR binaries (≥ 5.0) | Le moteur réel qui effectue le travail lourd |
| Greek language data (`grc.traineddata`) | Nécessaire pour **read ancient greek** correctement |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Notre cible pour la démonstration **ocr png image** |

Vous pouvez installer la partie Python avec :

```bash
pip install pytesseract Pillow
```

Et sur Ubuntu/macOS, vous ajouteriez le moteur lui‑même :

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

N’oubliez pas de télécharger les données d’entraînement grec polytonique :

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Le chemin peut différer ; ajustez `TESSDATA_PREFIX` si nécessaire.)*

## OCR PNG Image : Créer l’instance du moteur

La première chose dont nous avons besoin est un objet qui communique avec Tesseract. Dans `pytesseract`, le moteur est accessible via des fonctions au niveau du module, mais pour plus de clarté nous l’envelopperons dans une petite classe. Cela reflète le concept de « engine » que vous avez vu dans l’extrait original.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Pourquoi l’envelopper ?**  
- Conserve l’API publique identique à l’extrait avec lequel vous avez commencé, rendant la migration indolore.  
- Nous permet d’ajouter de la journalisation ou de la gestion d’erreurs plus tard sans toucher au flux principal.  
- Démonstre une bonne pratique OOP—quelque chose que les développeurs seniors apprécient.

## Extraire le texte d’une image : définir la langue en grec polytonique

Maintenant que nous avons un moteur, nous devons lui indiquer quelle langue attendre. Le grec polytonique utilise des diacritiques qui ne sont pas couverts par les données « greek » standard, nous pointons donc Tesseract vers le fichier d’entraînement `grc`.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

Si vous souhaitez un jour **extract text from image** dans une autre langue, remplacez simplement `"grc"` par `"eng"` pour l’anglais, `"fra"` pour le français, etc. La même ligne fonctionne pour toute langue que vous avez installée.

## Reconnaître le texte d’une image : exécuter l’OCR sur un PNG

Avec la langue définie, nous injectons le PNG dans le moteur. L’exemple original utilisait un chemin codé en dur ; nous le rendrons un peu plus flexible en utilisant des objets `Path`.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Conseils & cas limites**

- **File not found** – encapsulez l’appel dans un `try/except FileNotFoundError` pour fournir un message convivial.
- **Low‑resolution PNG** – envisagez un pré‑traitement (par ex., redimensionnement, binarisation) avec Pillow avant l’OCR.  
- **Non‑Greek text** – Tesseract essaiera toujours de décoder, mais la précision chute fortement. Assurez‑vous toujours que la langue correspond.

## Sortir le texte reconnu

Enfin, nous affichons le résultat. Dans un projet réel, vous pourriez écrire dans une base de données, un CSV, ou même l’alimenter dans un pipeline de traduction.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

Lorsque vous exécutez le script sur une numérisation claire d’une inscription grecque ancienne, vous devriez voir quelque chose comme :

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

Si la sortie apparaît brouillée, vérifiez que le fichier **greek.traineddata** se trouve dans le bon dossier et que le PNG n’est pas trop bruyant.

## Exemple complet fonctionnel (Toutes les étapes dans un seul script)

Ci‑dessous se trouve le programme complet, prêt à être exécuté. Enregistrez‑le sous le nom `ocr_greek.py` et lancez `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Sortie attendue** (troncature pour la brièveté) :

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

Si vous voyez les caractères grecs corrects, félicitations — vous avez réussi à effectuer une opération **ocr png image** en Python !

## Questions fréquentes & astuces pro

### Comment améliorer la précision sur un PNG bruyant ?

- Convertir l’image en niveaux de gris : `img = img.convert('L')`
- Appliquer un seuil binaire : `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Agrandir avec `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

Ces étapes transforment souvent un cauchemar de **recognize image text** en un résultat propre.

### Puis‑je traiter un dossier complet de PNG ?

Absolument. Enveloppez l’appel `recognize_image` dans une boucle `for` sur `Path.glob("*.png")`. Stockez chaque résultat dans un dictionnaire ou écrivez‑le dans un CSV pour une analyse ultérieure.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### Et si je dois extraire uniquement les nombres ?

Passez une chaîne **config** personnalisée à `image_to_string` :

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

De cette façon vous pouvez **extract text from image** des fichiers contenant des tableaux, numéros de série ou horodatages.

### Existe‑t‑il un moyen d’obtenir des scores de confiance ?

Oui—utilisez `pytesseract.image_to_data` qui renvoie un TSV avec la confiance par mot. Vous pouvez filtrer les tokens à faible confiance avant d’assembler la chaîne finale.

## Étendre le tutoriel

Maintenant que vous avez maîtrisé les bases, envisagez d’explorer ces sujets connexes :

- **Batch OCR with multiprocessing** – accélérer le traitement de grands corpus de PNG.
- **Hybrid OCR + NLP pipelines** – traduire automatiquement le grec ancien extrait en anglais moderne.
- **Alternative engines** – essayer `easyocr` ou des méthodes basées sur `opencv` pour des cas d’utilisation spécifiques.
- **Cloud OCR services** – Google Vision, Azure Computer Vision, ou AWS Textract pour une mise à l’échelle sans serveur.

Chacun de ces éléments s’appuie sur le **python ocr example** de base que nous venons de couvrir, vous permettant de plonger plus profondément en toute confiance.

## Conclusion

Nous avons pris un extrait simple et l’avons transformé en un flux de travail robuste **ocr png image** en Python. En créant un `OcrEngine`, en définissant la langue en grec polytonique, en injectant un PNG et en affichant le résultat, vous savez maintenant comment **extract text from image** des fichiers, **recognize image text**, et même **read ancient greek**.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte d’une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment définir la valeur du seuil dans la reconnaissance d’image OCR](/ocr/english/net/ocr-settings/set-threshold-value/)
- [reconnaître le texte d’une image avec Aspose OCR pour plusieurs langues](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}