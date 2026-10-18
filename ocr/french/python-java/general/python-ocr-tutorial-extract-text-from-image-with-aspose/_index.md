---
category: general
date: 2026-03-26
description: 'Tutoriel OCR Python : apprenez comment extraire du texte d’une image,
  charger l’image pour l’OCR et reconnaître le texte d’un reçu en utilisant Aspose
  OCR en quelques étapes seulement.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: fr
og_description: 'Tutoriel OCR Python : apprenez rapidement à extraire du texte d’une
  image, charger une image pour l’OCR et reconnaître le texte d’un reçu avec Aspise
  OCR.'
og_title: Tutoriel OCR Python – Extraire du texte d’une image
tags:
- OCR
- Aspose
- Python
title: Tutoriel OCR Python – Extraire du texte d’une image avec Aspose
url: /fr/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutoriel OCR Python – Extraire du texte d'une image avec Aspose

Vous êtes-vous déjà demandé comment extraire le texte d’un reçu flou ou d’un formulaire numérisé sans passer des heures à écrire des expressions régulières personnalisées ? Vous n’êtes pas seul. Dans ce **tutoriel OCR python** nous allons parcourir le chargement d’une image pour l’OCR, l’exécution de l’OCR en Python, puis la reconnaissance du texte à partir de fichiers de reçus en utilisant la bibliothèque Aspose OCR.  

À la fin de ce guide, vous disposerez d’un script prêt à l’emploi qui lit n’importe quel format d’image pris en charge, extrait le contenu textuel et l’affiche dans la console. Aucun service externe, aucune clé d’API — juste du pur Python et un moteur OCR puissant.  

## Ce dont vous avez besoin

- Python 3.8 ou plus récent (le code utilise des annotations de type, donc un interpréteur récent est recommandé)
- Le package `asposeocrjava` installé via `pip install aspose-ocr`
- Une image d’exemple – par exemple `receipt_noisy.jpg` contenant un reçu de magasin typique
- (Facultatif) Un environnement virtuel pour garder les dépendances propres

Si ces points sont cochés, nous pouvons passer directement au code.  

## Étape 1 : Installer et importer les classes Aspose OCR

Tout d’abord, assurez‑vous que le package Aspose OCR est disponible. Puis importez les classes dont nous aurons besoin.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Pourquoi c’est important :** Importer uniquement les symboles nécessaires garde l’espace de noms propre et indique à l’interpréteur quelles parties de la bibliothèque nous utilisons réellement. Cela raccourcit également les lignes de code ultérieures, rendant le tutoriel plus facile à suivre.

> **Astuce :** Si vous utilisez un notebook Jupyter, préfixez la ligne d’installation avec `!` pour l’exécuter dans la cellule.

## Étape 2 : Créer le moteur OCR et activer le mode Deep‑Learning

Aspose propose plusieurs modes de moteur. Pour la plupart des reçus réels, le modèle deep‑learning offre la meilleure précision, surtout sur des scans bruyants.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Pourquoi le deep‑learning ?** L’OCR traditionnel basé sur des règles peut échouer sur des caractères à faible contraste ou déformés. Le modèle deep‑learning, entraîné sur des millions de glyphes, s’adapte mieux aux variations — exactement ce dont vous avez besoin lorsque vous *effectuez de l’OCR en Python* sur des reçus pris avec un smartphone.

## Étape 3 : Charger l’image pour l’OCR

Nous allons maintenant réellement **charger l’image pour l’OCR**. Aspose.Imaging prend en charge PNG, JPEG, BMP, TIFF, et bien d’autres, vous pouvez donc pointer vers pratiquement n’importe quelle photo d’un document.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Erreur fréquente :** Oublier d’associer l’image au moteur entraîne une `NullReferenceException` à l’exécution. Appelez toujours `set_image` après avoir chargé le fichier.

## Étape 4 : Effectuer l’OCR et extraire le texte

Avec le moteur prêt et l’image attachée, nous pouvons enfin **effectuer l’OCR en Python** et récupérer le résultat textuel.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

La méthode `recognize()` renvoie un objet `OcrResult` qui contient non seulement le texte brut mais aussi les scores de confiance, les boîtes englobantes et les informations de langue. Pour un cas d’utilisation rapide **extraire du texte d’une image**, nous n’avons besoin que de `get_text()`.

## Étape 5 : Afficher le texte reconnu

Voyons ce que le moteur a réellement lu sur le reçu.

```python
print("Recognized text:\n", recognized_text)
```

Un résultat typique ressemble à :

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Si la sortie contient des caractères illisibles, envisagez de pré‑traiter l’image (par ex., augmenter le contraste ou appliquer un filtre de redressement) avant de la charger dans le moteur OCR. Aspose.Imaging propose une suite complète d’outils d’amélioration d’image que vous pouvez chaîner.

## Gestion des cas limites & conseils pour une meilleure précision

### 1. Traiter des reçus extrêmement bruyants
Si le reçu est fortement taché, vous pouvez passer en mode `OcrEngineMode.HIGH_SPEED` pour un passage plus rapide, bien que moins précis, puis exécuter une seconde passe en `DEEP_LEARNING` sur l’image nettoyée.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Spécifier la langue
Par défaut, Aspose tente de détecter automatiquement la langue. Pour les reçus en anglais, vous pouvez la verrouiller :

```python
ocr_engine.set_language("eng")
```

### 3. Gestion de la mémoire
Lors du traitement de nombreuses images dans une boucle, libérez explicitement les ressources :

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. Enregistrer les résultats OCR dans un fichier
Parfois, vous avez besoin du texte extrait pour une analyse ultérieure.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Exemple complet fonctionnel

Voici le script complet qui réunit tous les éléments. Copiez‑collez‑le dans un fichier nommé `receipt_ocr.py`, ajustez le chemin de l’image, puis exécutez `python receipt_ocr.py`.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

L’exécution du script doit afficher le contenu du reçu dans votre console et créer également `receipt_output.txt` avec les mêmes données.

![Tutoriel OCR Python – sortie d’exemple de reçu](https://example.com/receipt_output.png "exemple de tutoriel OCR python")

*Texte alternatif de l’image :* **tutoriel OCR python – sortie d’exemple de reçu**

## Récapitulatif & étapes suivantes

Nous venons de parcourir un **tutoriel OCR python** qui montre comment **charger une image pour l’OCR**, **effectuer l’OCR en Python**, et enfin **reconnaître le texte d’un reçu** à l’aide d’Aspose. Les points clés sont :

- Choisir le bon mode de moteur (deep‑learning pour la précision)
- Toujours attacher l’image avant d’appeler `recognize()`
- Utiliser l’objet `OcrResult` pour extraire le texte propre, puis le stocker ou le traiter selon les besoins

Et après ? Envisagez de chaîner les filtres Aspose Imaging pour améliorer les scans à faible contraste, ou d’intégrer le script dans une API Flask afin de pouvoir télécharger des reçus via un formulaire web. Vous pouvez également explorer l’exportation des données OCR vers CSV pour automatiser la comptabilité.

Des questions sur la gestion de PDFs multi‑pages ou de scripts non latins ? Laissez un commentaire — je suis heureux d’aider !  

**Prêt à faire passer votre automatisation de documents au niveau supérieur ?** Prenez le code, expérimentez avec différentes images, et laissez le moteur OCR faire le gros du travail. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}