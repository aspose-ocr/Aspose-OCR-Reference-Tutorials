---
category: general
date: 2026-06-19
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) sur
  une image en utilisant Aspose OCR et le post‑processeur IA en Python. Comprend un
  modèle téléchargé automatiquement, la correction orthographique et l'accélération
  GPU.
draft: false
keywords:
- perform OCR on image
- Aspose OCR Python
- AI post‑processor
- auto‑downloaded model
- spellcheck post‑processor
- GPU acceleration
language: fr
og_description: Effectuer la reconnaissance optique de caractères sur une image en
  utilisant Aspose OCR et le post‑processeur IA. Guide étape par étape avec modèle
  téléchargé automatiquement, correction orthographique et accélération GPU.
og_title: Effectuer l'OCR sur une image – Tutoriel complet Python
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  headline: perform OCR on image with Aspose AI – Full Python Guide
  type: TechArticle
- description: Learn how to perform OCR on image using Aspose OCR and AI post‑processor
    in Python. Includes auto‑downloaded model, spellcheck, and GPU acceleration.
  name: perform OCR on image with Aspose AI – Full Python Guide
  steps:
  - name: Initializes the Aspose OCR engine and loads a sample invoice image.
    text: Initializes the Aspose OCR engine and loads a sample invoice image.
  - name: Runs a basic OCR pass and prints the raw text.
    text: Runs a basic OCR pass and prints the raw text.
  - name: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
    text: Configures **Aspose AI** with an **auto‑downloaded model** from Hugging Face.
  - name: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
    text: Executes the **AI post‑processor** (including a **spellcheck post‑processor**)
      to clean up the OCR output.
  - name: Releases all resources cleanly.
    text: Releases all resources cleanly.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Effectuer l'OCR sur une image avec Aspose AI – Guide complet Python
url: /fr/python/general/perform-ocr-on-image-with-aspose-ai-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur image – Tutoriel complet Python

Vous êtes‑vous déjà demandé comment **effectuer une OCR sur image** sans vous battre avec des dizaines de bibliothèques ? D’après mon expérience, le problème réside souvent dans la gestion d’un moteur OCR brut, puis dans le nettoyage de la sortie bruitée. Heureusement, Aspose OCR pour Python associé à son post‑processeur IA rend toute la chaîne très simple.

Dans ce guide, nous parcourrons un exemple pratique, de bout en bout, qui montre exactement comment **effectuer une OCR sur image**, améliorer la précision avec un modèle auto‑téléchargé, activer la correction orthographique, et même exploiter l’accélération GPU lorsqu’elle est disponible. À la fin, vous disposerez d’un script réutilisable que vous pourrez intégrer à tout projet de facturation, de numérisation de reçus ou de digitalisation de documents.

## Ce que vous allez créer

Nous créerons un petit programme Python qui :

1. Initialise le moteur Aspose OCR et charge une image de facture d’exemple.  
2. Effectue une passe OCR de base et affiche le texte brut.  
3. Configure **Aspose AI** avec un **modèle auto‑téléchargé** depuis Hugging Face.  
4. Exécute le **post‑processeur IA** (incluant un **post‑processeur de correction orthographique**) pour nettoyer la sortie OCR.  
5. Libère toutes les ressources proprement.

Aucun service externe, aucune clé API — juste quelques lignes de Python et la puissance d’Aspose.

> **Astuce :** Si vous disposez d’une machine avec un GPU décemment puissant, définir `gpu_layers` peut économiser quelques secondes sur l’étape de post‑traitement.

## Prérequis

- Python 3.8 ou supérieur (le code utilise des annotations de type mais elles sont optionnelles).  
- Packages `aspose-ocr` et `aspose-ai` installés via `pip`.  
  ```bash
  pip install aspose-ocr aspose-ai
  ```  
- Une image d’exemple (PNG, JPG ou TIFF) placée quelque part que vous pouvez référencer, par ex. `sample_invoice.png`.  
- (Optionnel) Un GPU compatible CUDA et les pilotes appropriés si vous souhaitez **l’accélération GPU**.

Maintenant que le terrain est préparé, plongeons dans le code.

![perform OCR on image example](image.png)

## Effectuer une OCR sur image – Étape 1 : Initialise le moteur OCR et charge l’image

La première chose dont nous avons besoin est une instance du moteur OCR. Aspose OCR propose une API propre, orientée objet, qui abstrait le pré‑traitement d’image de bas niveau.

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()
ocr_engine.Language = "en"                     # English; change as needed

# Load the image you want to analyse
ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")
```

**Pourquoi c’est important :**  
Définir la langue dès le départ indique au moteur quel jeu de caractères attendre, ce qui peut améliorer la vitesse et la précision de reconnaissance. Si vous traitez des documents multilingues, remplacez simplement `"en"` par `"fr"` ou `"de"` selon le besoin.

## Étape 2 : Effectuer une OCR de base et visualiser le texte brut

Nous exécutons maintenant la reconnaissance. L’objet résultat contient le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

```python
# Run OCR
ocr_result = ocr_engine.Recognize()

# Show the unprocessed output
print("Raw OCR output:")
print(ocr_result.Text)
```

Un résultat typique peut ressembler à ceci (notez les caractères parfois mal lus) :

```
Raw OCR output:
Inv0ice N0: 12345
Date: 2023/09/15
Total Am0unt: $1,2O0.00
```

Vous pouvez voir les zéros (`0`) là où le moteur a pensé avoir vu un « O ». C’est là que le **post‑processeur IA** brille.

## Configurer Aspose AI – modèle auto‑téléchargé et correction orthographique

Avant de transmettre le résultat OCR brut à la couche IA, nous devons indiquer à Aspose AI quel modèle utiliser. La bibliothèque peut télécharger automatiquement un modèle depuis Hugging Face, vous évitant ainsi de gérer de gros fichiers `.bin`.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

# Create a model configuration that auto‑downloads the Qwen2.5‑3B‑Instruct model
model_config = AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"   # reduces RAM usage
model_config.gpu_layers = 20                      # use GPU if available

# Initialise the AI engine with the config
ai_engine = AsposeAI(model_config)

# Enable the built‑in spellcheck post‑processor
ai_engine.set_post_processor("spellcheck", None)
```

**Explication des paramètres**

| Paramètre | Ce qu’il fait | Quand ajuster |
|-----------|----------------|----------------|
| `allow_auto_download` | Permet à Aspose de récupérer le modèle automatiquement lors du premier lancement. | Gardez `true` sauf si vous avez pré‑téléchargé pour une utilisation hors ligne. |
| `hugging_face_repo_id` | Identifiant du modèle sur Hugging Face. | Changez-le pour un modèle différent si vous avez besoin d’un modèle spécialisé. |
| `hugging_face_quantization` | Choisit le niveau de quantification (`int8`, `float16`, etc.). | Utilisez `int8` pour les environnements à faible mémoire ; `float16` pour une précision supérieure. |
| `gpu_layers` | Nombre de couches du transformeur exécutées sur le GPU. | Mettez `0` pour CPU uniquement, ou une valeur jusqu’au nombre total de couches du modèle (20 pour Qwen2.5‑3B). |

## Exécuter le post‑processeur IA sur le résultat OCR

Avec le moteur prêt, il suffit d’alimenter la sortie OCR brute dans le pipeline IA. Le **post‑processeur de correction orthographique** intégré corrigera les fautes évidentes, tandis que le modèle de langage pourra reformuler ou compléter les informations manquantes si vous activez d’autres processeurs plus tard.

```python
# Enhance the OCR result using the AI post‑processor
enhanced_result = ai_engine.run_postprocessor(ocr_result)

# Display the cleaned‑up text
print("\nAI‑enhanced OCR output:")
print(enhanced_result.Text)
```

Sortie attendue après l’étape de correction orthographique :

```
AI‑enhanced OCR output:
Invoice No: 12345
Date: 2023/09/15
Total Amount: $1,200.00
```

Remarquez comment les zéros ont été corrigés en lettres correctes, et le mot mal orthographié « Am0unt » est devenu « Amount ». Le **post‑processeur IA** fonctionne en envoyant le texte brut au modèle sélectionné, qui renvoie ensuite une version raffinée basée sur son entraînement.

### Cas limites & astuces

- **Images basse résolution** : Si le moteur OCR a du mal, envisagez d’up‑scaler d’abord l’image (`Pillow` peut aider) ou d’augmenter `ocr_engine.ImagePreprocessingOptions`.  
- **Scripts non latins** : Changez `ocr_engine.Language` vers le code ISO approprié (`"zh"` pour le chinois, `"ar"` pour l’arabe).  
- **GPU non détecté** : Le paramètre `gpu_layers` revient silencieusement à CPU si aucun GPU compatible n’est trouvé, vous n’avez donc pas besoin de gestion d’erreur supplémentaire.  
- **Limites de taille du modèle** : Le modèle Qwen2.5‑3B fait environ 4 Go compressés ; assurez‑vous d’avoir suffisamment d’espace disque pour le téléchargement automatique.

## Libérer les ressources – arrêt propre

Les objets Aspose détiennent des handles natifs, il est donc recommandé de les libérer une fois le travail terminé. Cela évite les fuites de mémoire, surtout dans les services à longue durée d’exécution.

```python
# Free AI resources
ai_engine.free_resources()

# Dispose of the OCR engine
ocr_engine.Dispose()
```

Vous pouvez envelopper tout le script dans un bloc `try…finally` si vous préférez un nettoyage explicite.

## Script complet – prêt à copier‑coller

Ci‑dessous se trouve le programme complet, prêt à être exécuté après avoir remplacé `YOUR_DIRECTORY` par le chemin vers votre image.

```python
# -*- coding: utf-8 -*-
"""
Full example: perform OCR on image using Aspose OCR + AI post‑processor.
Author: Your Name
Date: 2026‑06‑19
"""

from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = OcrEngine()
    ocr_engine.Language = "en"
    ocr_engine.SetImageFromFile("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Basic OCR
    ocr_result = ocr_engine.Recognize()
    print("Raw OCR output:")
    print(ocr_result.Text)

    # 3️⃣ Configure Aspose AI with auto‑downloaded model
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "int8"
    model_cfg.gpu_layers = 20   # GPU acceleration if available

    ai_engine = AsposeAI(model_cfg)
    ai_engine.set_post_processor("spellcheck", None)   # enable spellcheck

    # 4️⃣ AI post‑processing
    enhanced = ai_engine.run_postprocessor(ocr_result)
    print("\nAI‑enhanced OCR output:")
    print(enhanced.Text)

    # 5️⃣ Clean up
    ai_engine.free_resources()
    ocr_engine.Dispose()

if __name__ == "__main__":
    main()
```

Exécutez‑le avec :

```bash
python perform_ocr_on_image.py
```

Vous devriez voir les sorties brutes et nettoyées affichées dans la console.

## Conclusion

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convertir une image en texte – Effectuer une OCR sur image depuis une URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}