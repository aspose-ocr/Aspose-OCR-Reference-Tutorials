---
category: general
date: 2026-04-26
description: Comment extraire l’OCR d’images avec Python – un exemple d’OCR en Python
  qui montre comment charger une image pour l’OCR et extraire le texte d’un reçu.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: fr
og_description: Comment extraire l’OCR d’images avec Python. Découvrez un exemple
  d’OCR en Python, chargez une image pour l’OCR et extrayez le texte d’un reçu en
  quelques minutes.
og_title: Comment extraire l'OCR en Python – Guide complet
tags:
- OCR
- Python
- Image Processing
title: Comment extraire l'OCR en Python – Tutoriel étape par étape
url: /fr/python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment extraire l'ocr en Python – Guide complet

Vous vous êtes déjà demandé **comment extraire l'ocr** d'un reçu flou ou d'une facture numérisée ? Vous n'êtes pas le seul—les développeurs se heurtent constamment à un mur lorsqu'ils ont besoin d'un texte propre, lisible par machine à partir d'images. La bonne nouvelle ? En quelques lignes de Python, vous pouvez transformer une photo de reçu en texte à haute confiance, consultable.

Dans ce tutoriel, nous parcourrons un **exemple d'ocr python** qui montre **comment charger une image pour l'ocr**, exécuter le moteur, et ne conserver que les caractères qui atteignent un seuil de confiance de 85 %. À la fin, vous serez capable d'**extraire du texte d'un reçu** sans fouiller la documentation ou deviner les paramètres de l'API.

## Ce dont vous avez besoin

- Python 3.9 ou plus récent (la syntaxe que nous utilisons fonctionne sur 3.8+)
- Le package `aocr` (ou toute bibliothèque OCR qui fournit une classe `OcrEngine`). Installez-le avec :

```bash
pip install aocr
```

- Une image d'exemple de reçu (`receipt.png`) placée dans un dossier que vous pouvez référencer.
- Un éditeur de texte ou un IDE—VS Code, PyCharm, ou même un simple notebook fera l'affaire.

C'est tout. Aucun framework lourd, aucun service externe, juste du Python pur.

![Résultat OCR à haute confiance – comment extraire l'ocr d'un reçu](/images/ocr-high-confidence.png)

*Texte alternatif de l'image : comment extraire l'ocr d'un reçu en utilisant Python OCR*

## Étape 1 – Créer l'instance du moteur OCR (comment extraire l'ocr)

La première chose que nous faisons est de lancer un moteur OCR. Pensez‑y comme le cerveau qui lira les pixels pour nous.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Pourquoi ?** Instancier `OcrEngine` vous fournit un nouvel objet de configuration. Vous pouvez ensuite ajuster les modèles de langue, les paramètres DPI ou les étapes de prétraitement—tout cela sans toucher à la boucle de traitement principale.

## Étape 2 – Charger l'image pour l'OCR

Ensuite, nous pointons le moteur vers l'image que nous voulons analyser. C'est ici que le mot‑clé **charger l'image pour l'ocr** entre en jeu.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Astuce :** Si votre image se trouve dans un répertoire différent, utilisez `os.path.join` pour construire un chemin indépendant de la plateforme.

**Pourquoi charger l'image de cette façon ?** L'utilitaire `Image.load` lit le fichier dans un format que le moteur comprend, gérant automatiquement les formats courants (PNG, JPEG, TIFF). Sauter cette étape ou fournir des octets bruts déclencherait une `ValueError`.

## Étape 3 – Exécuter le processus OCR

Nous exécutons maintenant réellement l'OCR. La méthode `process` renvoie un objet résultat riche contenant les symboles reconnus, les scores de confiance et les boîtes englobantes.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**Que contient `ocr_result` ?** Dans la plupart des bibliothèques, il inclut :

- `text` : la chaîne brute concaténée.
- `symbol_confidences` : une liste de tuples `(char, confidence)`.
- `boxes` : les coordonnées de chaque caractère (utile pour le débogage visuel).

Avoir accès à la confiance par caractère est essentiel pour l'étape suivante.

## Étape 4 – Conserver uniquement les symboles à haute confiance (≥ 85 %)

Un reçu comporte souvent des bavures, une impression pâle ou du bruit de fond. En filtrant les symboles à faible confiance, nous améliorons considérablement l'analyse en aval.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Pourquoi 85 % ?** Empiriquement, un seuil autour de 0,85 équilibre rappel et précision pour la plupart des reçus imprimés. Si vous remarquez des chiffres manquants, abaissez le seuil ; si vous obtenez du charabia, augmentez‑le.

## Étape 5 – Produire le texte extrait à haute confiance

Enfin, nous affichons (ou stockons) la chaîne nettoyée. C'est le cœur de notre flux de travail **extraire du texte d'un reçu**.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

Un exemple de sortie ressemble à :

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

Vous pouvez maintenant injecter cette chaîne dans un générateur CSV, une base de données, ou tout pipeline analytique en aval.

## Script complet, prêt à l'exécution

Ci-dessous le fragment de code complet que vous pouvez copier‑coller dans `ocr_receipt.py` et exécuter immédiatement.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Enregistrez le fichier, assurez‑vous que `receipt.png` existe, puis exécutez :

```bash
python ocr_receipt.py
```

Vous devriez voir le texte du reçu nettoyé affiché dans la console.

## Cas limites & scénarios « What‑If »

| Situation | Solution proposée |
|-----------|-------------------|
| **Très faible confiance partout** | Pré‑traitez l'image : augmentez le contraste, convertissez en niveaux de gris, ou appliquez un filtre de débruitage (`cv2.GaussianBlur`). |
| **Caractères non latins** | Passez un modèle de langue à `OcrEngine` (par ex., `ocr_engine.language = "spa"` pour l'espagnol). |
| **Plusieurs reçus dans une même image** | Exécutez l'OCR sur l'image entière, puis divisez le résultat à l'aide d'expressions régulières qui détectent `\n\n+` (sauts de ligne doubles). |
| **Besoin du texte OCR brut également** | Conservez `ocr_result.text` en plus de la version filtrée pour le débogage. |

Ces variantes garantissent que votre connaissance **comment utiliser l'OCR** s'étend au-delà du cas le plus simple.

## Pièges courants (et comment les éviter)

- **Oublier d'installer la bibliothèque** – `pip install aocr` doit réussir avant l'importation.
- **Utiliser le mauvais séparateur de chemin** sous Windows (`\` vs `/`). Utilisez `os.path.join`.
- **Coder en dur le seuil de confiance** sans test – effectuez toujours une vérification visuelle rapide sur quelques reçus d'abord.
- **Ignorer la normalisation Unicode** – certains reçus contiennent des caractères de tiret spéciaux ; exécutez `unicodedata.normalize('NFKC', text)` si vous prévoyez de stocker la sortie.

## Prochaines étapes – Aller au-delà des bases

Maintenant que vous savez **comment extraire l'ocr** d'un seul reçu, vous pourriez vouloir :

1. **Traiter par lots un dossier de reçus** – parcourir tous les fichiers PNG/JPG et écrire chaque résultat dans un CSV.
2. **Intégrer avec une base de données** – stocker `high_confidence_text` dans SQLite pour des recherches rapides.
3. **Appliquer une analyse en langage naturel** – utilisez des regex ou `dateutil` pour extraire dates, totaux et montants de taxe.
4. **Expérimenter d'autres bibliothèques** – `pytesseract`, `easyocr`, ou des services cloud (Google Vision, Azure OCR) si vous avez besoin d'un support multilingue ou d'une plus grande précision.

Chacun de ces sujets intègre naturellement nos mots‑clés secondaires : *python ocr example*, *extract text from receipt*, *load image for ocr*, et *how to use OCR*.

## Conclusion

Nous venons de parcourir un **exemple d'ocr python** complet qui montre **comment extraire l'ocr** à partir d'une image de reçu, filtrer les symboles à faible confiance, et produire des résultats propres. Les étapes sont simples, le code est autonome, et l'approche est suffisamment flexible pour s'adapter à des projets plus importants.

Essayez-le avec vos propres reçus, ajustez le seuil de confiance, puis passez à un traitement par lots. Si vous rencontrez des particularités—comme un logo pâle ou une police inhabituelle—rappelez‑vous les astuces pour les cas limites ci‑dessus. Bon codage, et que vos pipelines OCR soient toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}