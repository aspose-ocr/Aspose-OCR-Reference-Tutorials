---
category: general
date: 2026-11-20
description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  avec Aspose OCR, puis extrayez le texte de l'image à l'aide du post‑processeur IA
  intégré. Apprenez un flux de travail Python complet en quelques minutes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from image
language: fr
lastmod: 2026-11-20
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur l'image
  avec Aspose OCR, puis extrayez le texte de l'image via un post‑traitement IA. Suivez
  ce guide Python étape par étape.
og_image_alt: Diagram showing how to perform OCR on image and extract text from image
  using Aspose
og_title: Effectuer une OCR sur une image et extraire le texte de l'image à l'aide
  d'Aspose
schemas:
- author: Aspose
  dateModified: '2026-11-20'
  description: Perform OCR on image with Aspose OCR and then extract text from image
    using the built‑in AI post‑processor. Learn a complete Python workflow in minutes.
  headline: Perform OCR on image and extract text from image with Aspose
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI post‑processing
title: Effectuer l'OCR sur une image et extraire le texte de l'image avec Aspose
url: /fr/python/general/perform-ocr-on-image-and-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image et extraire le texte d’une image avec Aspose

Si vous devez **effectuer une OCR sur des fichiers image** en Python, ce guide vous montre une solution complète de bout en bout. En utilisant Aspose OCR conjointement avec le post‑processeur AI d’Aspose, vous pouvez **extraire le texte d’une image** de façon fiable et améliorer la sortie brute de l’OCR grâce à un modèle de langage léger.

Dans ce tutoriel vous allez :

* Configurer le moteur Aspose OCR.
* Exécuter l’OCR pour **extraire le texte d’une image**.
* Optionnellement configurer un modèle AI pour le post‑traitement.
* Enregistrer une fonction de post‑traitement personnalisée.
* Produire du texte enrichi et libérer les ressources.

Les étapes fonctionnent avec n’importe quelle image raster (PNG, JPEG, BMP) et ne nécessitent que le package `aspose-ocr`.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

| Prérequis | Pourquoi c’est important |
|-----------|---------------------------|
| Python 3.8+ | Requis par le SDK Aspose. |
| Package pip `aspose-ocr` | Fournit `AsposeOCR`, `AsposeAI` et les classes de configuration de modèle. |
| Un fichier image (par ex., `sample_image.png`) | La source sur laquelle vous **effectuerez une OCR sur l’image**. |
| Optionnel : support GPU | Si vous prévoyez d’exécuter un modèle plus grand sur un GPU, définissez `gpu_layers` en conséquence. |

Installez le SDK avec :

```bash
pip install aspose-ocr
```

## Étape 1 : Effectuer une OCR sur l’image

La première opération consiste à lire l’image et à obtenir le texte brut. C’est l’étape centrale **effectuer une OCR sur l’image**.

```python
from aspose.ocr import AsposeOCR

# Initialise the OCR engine
ocr_engine = AsposeOCR()

# Path to the image you want to process
image_path = "YOUR_DIRECTORY/sample_image.png"

# Execute OCR – this returns the plain text extracted from the image
raw_text = ocr_engine.recognize_image(image_path)

print("Raw OCR result:")
print(raw_text)
```

**Pourquoi cela fonctionne :** `AsposeOCR.recognize_image` exécute un modèle de reconnaissance optique de caractères pré‑entraîné, optimisé pour la vitesse et la précision sur les polices courantes. La méthode renvoie une chaîne Unicode simple, qui constitue la base pour tout traitement ultérieur.

> **Astuce :** Si l’image contient plusieurs langues, définissez `ocr_engine.language = "eng+spa"` (ou tout code ISO‑639‑2 supporté) avant d’appeler `recognize_image`.

## Étape 2 : Initialiser le post‑processeur AI

Aspose AI fournit une couche de post‑traitement légère qui peut nettoyer les erreurs d’OCR, corriger la ponctuation ou appliquer une logique métier personnalisée.

```python
from aspose.ocr import AsposeAI

# Initialise the AI post‑processor with default logging
ai_processor = AsposeAI()
```

**Pourquoi vous en avez besoin :** L’OCR brut confond souvent des caractères (ex. : “0” vs “O”). L’étape AI affine la sortie, rendant le résultat **extraire le texte d’une image** plus fiable pour les tâches en aval comme l’indexation ou l’analyse.

## Étape 3 : (Optionnel) Configurer le modèle AI

Vous pouvez pointer le processeur vers un modèle Hugging Face spécifique, activer les téléchargements automatiques ou forcer l’exécution sur CPU. Cette étape est optionnelle mais utile lorsque vous souhaitez un comportement déterministe.

```python
from aspose.ocr import AsposeAIModelConfig

# Create a configuration object
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"          # Download model if missing
model_config.hugging_face_repo_id = "openai/gpt2"   # Small, fast model
model_config.gpu_layers = 0                        # Use CPU; set >0 for GPU

# Apply the configuration to the AI processor
ai_processor.configure(model_config)
```

**Explication :**  
* `allow_auto_download` vous évite la gestion manuelle des modèles.  
* `hugging_face_repo_id` sélectionne un modèle ; `gpt2` offre un bon compromis entre taille et qualité pour la correction de courts textes.  
* `gpu_layers` contrôle le nombre de couches du transformeur exécutées sur le GPU ; `0` force une exécution pure CPU, sûre sur toutes les machines.

## Étape 4 : Enregistrer une fonction de post‑traitement personnalisée

Aspose AI vous permet de brancher n’importe quel callable qui reçoit la chaîne OCR brute et renvoie une version transformée. Voici un exemple simple qui convertit tout en majuscules.

```python
def my_post_processor(text):
    """
    Custom post‑processor that transforms the OCR result.
    Replace this logic with your own business rules.
    """
    return text.upper()

# Register the function with the AI processor
ai_processor.set_post_processor(my_post_processor, custom_settings=None)
```

**Quand personnaliser :** Utilisez une fonction personnalisée lorsque vous avez besoin d’un nettoyage spécifique au domaine, comme la suppression d’identifiants confidentiels, la normalisation des dates ou des corrections basées sur des expressions régulières. Le modèle AI s’exécutera *après* cette fonction, vous permettant de combiner des règles déterministes avec des améliorations probabilistes.

## Étape 5 : Améliorer le résultat OCR avec le post‑processeur AI

Exécutez maintenant le pipeline complet : le texte OCR brut est d’abord passé à votre fonction personnalisée, puis au modèle AI, et enfin vous recevez la sortie raffinée.

```python
# Run the AI post‑processor on the raw OCR text
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("\nOriginal OCR :")
print(raw_text)
print("\nAI‑enhanced   :")
print(enhanced_text)
```

**Ce que vous devriez voir :**  
Si l’image originale contenait “Hello world”, la console pourrait afficher :

```
Original OCR :
Hello world

AI‑enhanced   :
HELLO WORLD
```

Dans un scénario réel, le modèle AI corrigerait les fautes d’orthographe, ajouterait la ponctuation manquante ou reformaterait les sauts de ligne, vous offrant un résultat **extraire le texte d’une image** plus propre, prêt à être stocké ou analysé.

## Étape 6 : Libérer les ressources à la fin

Le moteur OCR et le post‑processeur AI allouent des ressources natives. Les libérer explicitement évite les fuites de mémoire, surtout dans des services de longue durée.

```python
# Clean up native resources
ai_processor.free_resources()
```

Si vous avez également instancié `ocr_engine` avec un backend lourd, vous pourriez appeler `ocr_engine.dispose()` (si disponible) de la même manière.

## Variations courantes et cas limites

| Situation | Ajustement recommandé |
|-----------|-----------------------|
| **Grands PDF avec de nombreuses pages** | Boucler sur chaque page, appeler `recognize_image` pour chaque page rasterisée, et agréger les résultats. |
| **Environnement avec GPU** | Définir `model_config.gpu_layers` au nombre de couches que vous souhaitez sur le GPU (ex. : `4`). Assurez‑vous que les pilotes CUDA sont installés. |
| **Texte non anglais** | Modifier `ocr_engine.language` avec le code langue approprié et, si besoin, sélectionner un modèle Hugging Face spécifique à la langue. |
| **Scans très bruyants** | Pré‑traiter l’image avec OpenCV (débruitage, seuillage) avant d’appeler `recognize_image`. |
| **Conserver la casse d’origine** | Remplacer la fonction `my_post_processor` par une fonction neutre ou une règle plus nuancée au lieu de `text.upper()`. |

## Exemple complet fonctionnel

En rassemblant le tout, voici un script unique que vous pouvez exécuter tel quel (remplacez `YOUR_DIRECTORY/sample_image.png` par le chemin réel de votre fichier) :

```python
from aspose.ocr import AsposeOCR, AsposeAI, AsposeAIModelConfig

# 1️⃣ Perform OCR on image
ocr_engine = AsposeOCR()
image_path = "YOUR_DIRECTORY/sample_image.png"
raw_text = ocr_engine.recognize_image(image_path)

# 2️⃣ Initialise the AI post‑processor
ai_processor = AsposeAI()

# 3️⃣ (Optional) Configure the AI model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "openai/gpt2"
model_config.gpu_layers = 0            # CPU execution
ai_processor.configure(model_config)

# 4️⃣ Register a custom post‑processor (example: uppercase)
def my_post_processor(text):
    return text.upper()

ai_processor.set_post_processor(my_post_processor, custom_settings=None)

# 5️⃣ Enhance the OCR result
enhanced_text = ai_processor.run_postprocessor(raw_text)

print("Original OCR :", raw_text)
print("AI‑enhanced   :", enhanced_text)

# 6️⃣ Release resources
ai_processor.free_resources()
```

L’exécution de ce script affiche à la fois la sortie OCR brute et la version améliorée par l’AI, démontrant comment vous pouvez **effectuer une OCR sur des fichiers image** et **extraire le texte d’une image** de façon fiable dans un workflow reproductible.

## Conclusion

Vous savez maintenant comment **effectuer une OCR sur des fichiers image** avec Aspose OCR, puis **extraire le texte d’une image** en utilisant le post‑processeur AI intégré. Le tutoriel a couvert :

* L’initialisation du moteur OCR.
* L’exécution de l’OCR pour obtenir le texte brut.
* (Optionnellement) la configuration d’un modèle Hugging Face léger.
* L’ajout d’une fonction de post‑traitement personnalisée.

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos projets.

- [Extract Text Image with Aspose OCR & AI – Full Step‑by‑Step Guide](/ocr/english/python/general/extract-text-image-with-aspose-ocr-ai-full-step-by-step-guid/)
- [How to Correct OCR Errors – Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image Python – Complete Aspose OCR Guide](/ocr/english/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}