---
category: general
date: 2026-01-02
description: Apprenez à redresser les images et à augmenter le contraste pour obtenir
  rapidement du texte brut. Comprend du code Python étape par étape et des conseils
  pour extraire le texte.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: fr
og_description: Comment redresser une image et augmenter le contraste pour obtenir
  du texte brut. Exemple complet en Python avec extraction de tableau et accélération
  GPU.
og_title: Comment redresser une image – Tutoriel complet OCR GPU
tags:
- OCR
- Python
- Image Processing
title: Comment redresser une image – Guide OCR accéléré par GPU
url: /fr/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image – Guide OCR accéléré par GPU

Vous vous êtes déjà demandé **comment redresser une image** lorsque vos reçus arrivent avec un angle étrange ? Vous n'êtes pas seul ; une photo inclinée peut transformer un reçu parfaitement lisible en un désordre incompréhensible. La bonne nouvelle, c’est qu’avec quelques lignes de Python, vous pouvez auto‑redresser, augmenter le contraste et extraire du texte brut propre—sans Photoshop manuel.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui non seulement montre **comment redresser une image**, mais aussi **comment augmenter le contraste**, **comment obtenir du texte brut**, et même **comment extraire du texte** des tableaux que le moteur OCR détecte. À la fin, vous disposerez d’un script autonome que vous pourrez intégrer à n’importe quel projet.

## Ce dont vous avez besoin

- Python 3.9+ installé (le code utilise des annotations de type, donc un interpréteur récent est recommandé)
- La bibliothèque `ocr` qui fournit `OcrEngine`, `EngineMode`, `ImageProcessingOptions` et `OcrResult` (installez‑la via `pip install ocr‑sdk` – remplacez par le nom réel du paquet que vous utilisez)
- Un GPU avec pilotes compatibles si vous voulez le gain de vitesse (optionnel mais recommandé)
- Un fichier image légèrement tourné ou à faible contraste, par ex. `receipt_skewed.jpg`

> **Astuce pro :** Si vous n’avez pas de GPU, changez simplement `EngineMode.GPU` en `EngineMode.CPU` et le script fonctionnera toujours—un peu plus lent.

## Implémentation pas à pas

Nous découpons la solution en blocs logiques. Chaque bloc possède un **H2** descriptif contenant le mot‑clé principal *comment redresser une image* ou l’un des mots‑clés secondaires. Le code est complet, commenté et prêt à être exécuté.

### Comment redresser une image avec OCR accéléré par GPU

La première chose que nous faisons est d’indiquer au moteur OCR de s’exécuter sur le GPU et d’activer la fonction d’auto‑redressement. L’auto‑redressement analyse la géométrie de l’image et la fait pivoter pour la remettre à l’endroit.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Pourquoi c’est important :** L’accélération GPU peut réduire le temps de traitement de secondes à millisecondes, ce qui est crucial lorsque vous traitez des dizaines de reçus par minute.

### Augmenter le contraste de l’image pour une meilleure reconnaissance

Un reçu à faible contraste est un cauchemar pour tout système OCR. En augmentant le contraste, nous offrons au moteur des bords plus nets avec lesquels travailler.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Comment augmenter le contraste :** La méthode `set_contrast_boost` accepte un pourcentage ; 30 % est une valeur sûre qui fonctionne pour la plupart des reçus numérisés. Si vos images sont très sombres, montez à 50 % ou expérimentez.

### Obtenir du texte brut à partir de l’image traitée

Maintenant que l’image est droite et lumineuse, nous la transmettons au moteur et demandons le résultat en texte brut.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Sortie attendue** (troncature pour la brièveté) :

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Comment obtenir du texte brut :** La méthode `get_text()` supprime toute information de mise en page et renvoie une chaîne propre, que vous pouvez ensuite stocker dans une base de données, envoyer à une API ou alimenter des analyses en aval.

### Comment extraire du texte des tableaux détectés

Souvent, les reçus contiennent des données tabulaires (articles, quantités, prix). Le SDK OCR peut détecter les tableaux et vous permettre d’itérer sur les lignes et les cellules.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Exemple de sortie de tableau** :

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Pourquoi extraire les tableaux :** Les données structurées facilitent le calcul des totaux, la génération de rapports ou l’alimentation d’un logiciel de comptabilité.

### Script complet fonctionnel

En rassemblant tous les morceaux, voici le script que vous pouvez copier‑coller dans `deskew_and_ocr.py` :

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Exécutez‑le avec :

```bash
python deskew_and_ocr.py
```

Vous devriez voir le texte nettoyé et les tableaux détectés affichés dans la console.

## Cas limites courants & comment les gérer

| Situation | Que faire |
|-----------|-----------|
| **L’image est à l’envers** | Augmentez la confiance de `set_auto_deskew(True)` en appelant également `set_rotation_correction(True)` si le SDK le propose. |
| **L’augmentation du contraste rend l’image trop claire** | Réduisez le pourcentage passé à `set_contrast_boost` (par ex. 15 %). |
| **GPU non disponible** | Remplacez `EngineMode.GPU` par `EngineMode.CPU` ; le reste du pipeline reste inchangé. |
| **Les tableaux sont manqués** | Essayez une numérisation à plus haute résolution ou activez `set_table_detection(True)` si la bibliothèque le permet. |

## Prochaines étapes : du texte brut aux données structurées

Maintenant que vous savez **comment redresser une image**, **comment augmenter le contraste** et **comment obtenir du texte brut**, vous pourriez :

- Analyser le texte brut avec des expressions régulières pour extraire des paires clé‑valeur (par ex. `total`, `date`).
- Stocker les résultats dans une base SQLite ou PostgreSQL pour des rapports ultérieurs.
- Intégrer le script dans une fonction serverless (AWS Lambda, Azure Functions) pour traiter automatiquement les téléchargements.

Toutes ces extensions s’appuient sur la même base que nous avons couverte ici.

## Conclusion

Nous avons parcouru **comment redresser une image** à l’aide d’un moteur OCR accéléré par GPU, démontré **comment augmenter le contraste** pour une reconnaissance plus nette, montré exactement **comment obtenir du texte brut**, et même expliqué **comment extraire du texte** des tableaux. Le script complet et exécutable lie le tout, vous permettant de l’ajouter à n’importe quel projet Python et de commencer à extraire des données propres à partir de photos inclinées et à faible contraste immédiatement.

Essayez avec quelques-uns de vos propres reçus, ajustez le niveau de contraste, et laissez l’OCR faire le gros du travail. Si vous rencontrez des particularités, revenez au tableau des cas limites ci‑dessus — la plupart des problèmes se résolvent avec un petit ajustement.

Bon codage, et que vos images soient toujours droites et lumineuses !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}