---
category: general
date: 2026-07-18
description: Exécutez l’OCR sur une image avec Aspose OCR en Python. Apprenez à extraire
  le texte brut d’une image, à appliquer un post‑traitement IA et à obtenir rapidement
  des résultats propres.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: fr
lastmod: 2026-07-18
og_description: Exécutez la reconnaissance optique de caractères (OCR) sur une image
  avec Aspose OCR et Python. Ce tutoriel montre comment extraire le texte brut d’une
  image et améliorer la précision grâce à un post‑processeur IA.
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: Exécuter l'OCR sur une image – Guide complet Python avec Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: Exécuter l'OCR sur une image avec Aspose AI – Tutoriel complet Python
url: /fr/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter l'OCR sur une image avec Aspose AI – Tutoriel complet Python

Vous vous êtes déjà demandé comment **exécuter l'OCR sur une image** sans vous battre avec des API de bas niveau ? Vous n'êtes pas seul. Dans de nombreux projets—traitement de factures, numérisation de reçus ou digitalisation de documents anciens—obtenir du texte propre et interrogeable à partir d'une image est la première, et souvent la plus difficile, étape.

Dans ce guide, nous parcourrons un exemple pratique qui non seulement **exécute l'OCR sur une image**, mais montre également comment **extraire du texte brut d'une image** à l'aide du moteur OCR d'Aspose, puis peaufiner le résultat avec un petit post‑processeur IA. À la fin, vous disposerez d’un script prêt à l’emploi, d’une compréhension claire de chaque composant et de quelques astuces pour éviter les pièges courants.

![Run OCR on Image example](/images/run-ocr-on-image.png){: .align-center alt="Sortie console de l'exécution de l'OCR sur une image montrant le texte original et le texte amélioré par l'IA"}

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir :

- Python 3.8+ installé (le code fonctionne sous Windows, macOS et Linux).
- Une licence active Aspose OCR for Python ou un essai gratuit (le package est `aspose-ocr` sur PyPI).
- Un fichier image d’exemple (par ex., une facture ou un reçu numérisé) enregistré localement.
- Optionnel : une machine avec GPU activé si vous prévoyez de modifier le paramètre `gpu_layers` plus tard.

C’est tout—pas de moteurs OCR lourds, pas d’appels externes au cloud, juste une installation pip unique et quelques lignes de code.

## Étape 1 : Installer le package Aspose OCR

Ouvrez un terminal et exécutez :

```bash
pip install aspose-ocr
```

Le package récupère le moteur OCR principal ainsi que l’espace de noms léger `aspose.ocr` que nous utiliserons tout au long du tutoriel.

## Étape 2 : Importer les classes requises

Nous commençons par importer les deux classes principales : `AsposeAI` pour le post‑traitement enrichi par l’IA et `OcrEngine` pour l’extraction réelle du texte.

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*Pourquoi c’est important* : `OcrEngine` effectue le travail lourd de reconnaissance des glyphes, tandis que `AsposeAI` nous permet d’ajouter une logique personnalisée—comme la capitalisation de chaque mot—sans réécrire le cœur de l’OCR.

## Étape 3 : Créer une instance AsposeAI (journalisation optionnelle)

Si vous souhaitez une journalisation détaillée, vous pouvez fournir un logger personnalisé, mais la configuration par défaut suffit dans la plupart des cas.

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## Étape 4 : Ajuster le modèle sous‑jacent (optionnel)

Aspose OCR est fourni avec un modèle linguistique par défaut, mais vous pouvez le pointer vers un dépôt HuggingFace ou forcer l’exécution sur CPU. Ci‑dessous, nous activons les téléchargements automatiques et sélectionnons le petit modèle `gpt2`—juste pour illustrer les réglages possibles.

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **Astuce pro** : Si vous disposez d’un GPU compatible CUDA, augmentez `gpu_layers` à `1` ou `2` pour un gain de vitesse notable.

## Étape 5 : Enregistrer un post‑processeur simple

Notre objectif est d’**extraire du texte brut d’une image** puis de le rendre plus lisible. Voici une petite fonction qui capitalise chaque mot. Vous pouvez la remplacer par une correction orthographique, une détection de langue ou même un appel complet à un LLM.

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

Le dictionnaire `custom_settings` vous permet de transmettre des paramètres supplémentaires plus tard—utile lorsque vous faites évoluer le processeur.

## Étape 6 : Charger une image et exécuter l'OCR

Nous allons enfin **exécuter l'OCR sur une image**. Nous récupérerons deux types de sortie :

1. **Texte brut** – une chaîne sans information de mise en page.
2. **Texte structuré** – conscient de la mise en page, conservant colonnes et tableaux.

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **Pourquoi les deux ?** `plain_text` est parfait pour des recherches rapides, tandis que `structured_text` brille lorsque vous devez reconstruire des tableaux ou conserver l’alignement des colonnes.

## Étape 7 : Améliorer les sorties OCR avec le post‑processeur IA

Avec les résultats OCR en main, nous les transmettons à `AsposeAI.run_postprocessor`. C’est ici que la fonction `capitalize_words` définie précédemment s’exécute.

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

Si vous décidez plus tard de remplacer le post‑processeur par quelque chose de plus sophistiqué—par ex., un correcteur grammatical—il suffit de remplacer la fonction à l’étape 5 et le reste du pipeline reste identique.

## Étape 8 : Voir les résultats

Imprimons tout côte à côte afin que vous puissiez comparer le OCR brut avec la version améliorée par l’IA.

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### Sortie attendue

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

Remarquez comment le post‑processeur IA a transformé les mots tout en minuscules en mots capitalisés, rendant le texte beaucoup plus lisible. Vous pouvez appliquer n’importe quelle transformation — c’est simplement une preuve de concept.

## Étape 9 : Nettoyer les ressources

Aspose charge des fichiers de modèle volumineux en mémoire. Lorsque vous avez terminé, libérez‑les pour éviter les fuites de mémoire, surtout dans les services à long terme.

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## Questions fréquentes et cas limites

| Question | Réponse |
|----------|---------|
| **Puis‑je exécuter l'OCR sur plusieurs images dans une boucle ?** | Absolument. Instanciez `OcrEngine` une seule fois, appelez `load_image` dans la boucle, et réutilisez la même instance `AsposeAI` pour le post‑traitement. |
| **Que faire si l'image est de basse résolution ?** | Pré‑traitez avec OpenCV (par ex., `cv2.resize` et `cv2.threshold`) avant de la transmettre à `OcrEngine`. |
| **Ai‑je besoin d’un GPU ?** | Pas obligatoire. Le mode CPU par défaut fonctionne bien pour la plupart des documents. Réglez `ai.config.gpu_layers` > 0 uniquement si vous avez un GPU compatible et avez besoin de vitesse. |
| **Comment extraire du texte brut d’une image dans d’autres langues ?** | Modifiez `ocr_engine.language = "fr"` (ou tout code ISO‑639‑1) avant d’appeler `recognize`. Le même post‑processeur fonctionnera, mais vous pourriez avoir besoin d’une logique spécifique à la langue. |

## Script complet fonctionnel

En rassemblant tous les éléments, voici le programme complet, prêt à être exécuté :

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

Enregistrez‑le sous le nom `run_ocr_on_image.py`, remplacez le chemin factice par le chemin réel de votre image, puis lancez `python run_ocr_on_image.py`. Vous devriez voir la sortie avant/après exactement comme dans l’exemple ci‑dessus.

## Conclusion

Nous avons réussi à **exécuter l'OCR sur une image** à l’aide d’Aspose OCR, démontré comment **extraire du texte brut d’une image**, et présenté une méthode légère pour améliorer la lisibilité avec un post‑processeur IA. Le schéma de base—OCR

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte d’une image avec Aspose OCR – Guide pas à pas](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraire du texte d’une image en C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Optimisation de l'extraction de texte d'image – OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}