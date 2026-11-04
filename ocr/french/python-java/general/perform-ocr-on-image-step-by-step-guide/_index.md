---
category: general
date: 2026-03-18
description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  pour extraire rapidement le texte de l'image. Apprenez comment charger une image
  pour l'OCR, créer un moteur OCR et améliorer la précision de l'OCR grâce aux options
  de langue.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: fr
og_description: Effectuez l'OCR sur une image grâce à ce guide détaillé. Apprenez
  à charger une image pour l'OCR, à créer un moteur OCR et à améliorer la précision
  de l'OCR pour une extraction fiable du texte.
og_title: Effectuer une reconnaissance optique de caractères sur une image – Tutoriel
  complet de programmation
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Effectuer la reconnaissance optique de caractères sur une image – Guide étape
  par étape
url: /fr/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image – Tutoriel complet de programmation

Vous avez déjà eu besoin de **perform OCR on image** mais vous ne saviez pas quelle bibliothèque choisir ou comment obtenir des résultats fiables ? Vous n'êtes pas seul. Dans ce guide, nous passerons en revue tout ce dont vous avez besoin pour **extract text from image**, depuis le chargement de l'image jusqu'à l'ajustement des options de langue afin de **improve OCR accuracy** à chaque étape.

Nous couvrirons comment **load image for OCR**, comment **create OCR engine**, et pourquoi chaque paramètre est important. À la fin, vous disposerez d’un script prêt à l’emploi qui affiche le texte reconnu, et vous comprendrez le « pourquoi » derrière chaque ligne—pas de raccourcis vagues du type « voir la documentation ». Plongeons‑y.

## Ce dont vous avez besoin

- Python 3.8+ (le code utilise des f‑strings et des annotations de type)
- Le paquet hypothétique `ocr_lib` – installez‑le avec `pip install ocr_lib`
- Un fichier image contenant du texte imprimé clair (par ex., `lab_report.png`)
- Un éditeur de texte basique ou un IDE (VS Code, PyCharm, ce que vous préférez)

Si vous avez déjà tout cela, super—vous êtes prêt. Sinon, téléchargez Python depuis python.org et exécutez la commande pip ; cela ne prend qu’une minute.

![exemple d'OCR sur image](/images/ocr-example.png)

*Texte alternatif : perform OCR on image – exemple de sortie montrant le texte extrait.*

## Étape 1 : Créer le moteur OCR – How to **create OCR engine** in Python

Avant que toute reconnaissance puisse s’effectuer, la bibliothèque a besoin d’un objet moteur qui contient la configuration et l’état d’exécution. Considérez le moteur comme le cerveau de l’opération.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Pourquoi c’est important :** Instancier le moteur dès le départ vous permet d’attacher les options de langue plus tard, et cela met également en cache les modèles internes pour des appels ultérieurs plus rapides.

## Étape 2 : Charger l'image pour l'OCR – The correct way to **load image for OCR**

Maintenant que nous disposons d’un moteur, nous devons lui fournir quelque chose à lire. La méthode `setImageFromFile` accepte un chemin de fichier ; le chemin peut être absolu ou relatif au répertoire de travail du script.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Astuce :** Utilisez un chemin absolu ou `os.path.join` pour éviter les surprises « fichier introuvable » lorsque le script s’exécute depuis un autre dossier.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Étape 3 : Améliorer la précision de l'OCR – Tweaking **language options** to **improve OCR accuracy**

L’OCR fonctionne dès le départ, mais les vocabulaires spécifiques à un domaine (comme le jargon de laboratoire) le perturbent souvent. En fournissant un dictionnaire personnalisé et une liste noire, vous réduisez les mauvaises reconnaissances telles que confondre « 0 » avec « O ».

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Pourquoi cela aide :** Le dictionnaire indique au modèle OCR que « HPLC » est un jeton valide, l’empêchant de décomposer le mot en absurdités. La liste noire indique au modèle de traiter les symboles ambigus comme du bruit, ce qui **improve OCR accuracy** directement.

## Étape 4 : Effectuer l'OCR sur l'image – The core **perform OCR on image** call

Avec le moteur prêt et l'image attachée, il est temps de réellement reconnaître le texte. Cette étape renvoie un objet `OcrResult` que vous pouvez interroger pour obtenir le texte brut, les scores de confiance ou les boîtes englobantes.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Si l’image est floue, vous verrez des scores de confiance plus bas dans le résultat. C’est un indice pour pré‑traiter l’image (par ex., augmenter le contraste) avant de la transmettre au moteur.

## Étape 5 : Extraire le texte de l'image – Pulling the final string out

Enfin, nous demandons au `OcrResult` sa représentation textuelle. La méthode `getText()` renvoie une chaîne en texte brut prête pour le traitement en aval (enregistrement dans un fichier, insertion dans une base de données, etc.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Sortie attendue :** En supposant que `lab_report.png` contienne un tableau simple, vous pourriez voir quelque chose comme :

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

C’est la partie **extract text from image** terminée.

## Exemple complet fonctionnel – Put It All Together

Ci-dessous se trouve un script unique qui assemble les morceaux des sections précédentes. Vous pouvez le copier‑coller dans `run_ocr.py` et exécuter `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Checklist de vérification rapide

| ✅ | Élément |
|---|------|
| ✔️ | Le moteur est créé (`create OCR engine`) |
| ✔️ | L'image est chargée (`load image for OCR`) |
| ✔️ | Les options de langue sont définies (`improve OCR accuracy`) |
| ✔️ | L'OCR est exécutée (`perform OCR on image`) |
| ✔️ | Le texte est extrait (`extract text from image`) |

Exécutez le script et observez la console. Si vous voyez le bloc « OCR Output » avec le contenu de votre rapport, vous avez réussi à **perform OCR on image**.

## Problèmes courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Entrée floue** | Le modèle OCR ne peut pas distinguer les caractères | Pré‑traiter avec OpenCV : `cv2.GaussianBlur` ou augmenter le DPI |
| **Langue incorrecte** | La langue par défaut peut être définie sur autre chose que l'anglais | Appelez `engine.setLanguage("eng")` avant `recognize()` |
| **Termes du dictionnaire manquants** | Les mots spécifiques au domaine deviennent illisibles | Ajoutez‑les via `setDictionary` comme indiqué à l’Étape 3 |
| **Blacklisted characters cause |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}