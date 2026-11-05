---
category: general
date: 2026-06-25
description: Apprenez comment effectuer la reconnaissance optique de caractères (OCR)
  en Python, découvrez la meilleure façon de charger une image pour l’OCR, puis améliorez
  la précision grâce au post‑traitement Aspose AI.
draft: false
keywords:
- how to perform OCR
- load image for OCR
- Aspose OCR Python
- AI post‑processor OCR
- OCR accuracy improvement
- Python image processing OCR
language: fr
og_description: Comment effectuer la reconnaissance optique de caractères (OCR) en
  Python ? Suivez ce guide pour charger une image pour l’OCR, exécuter une reconnaissance
  de base et améliorer les résultats avec le post‑traitement Aspose AI.
og_title: Comment réaliser l'OCR en Python – Tutoriel complet Aspose OCR et IA
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  headline: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  type: TechArticle
- description: Learn how to perform OCR in Python and discover the best way to load
    image for OCR, then boost accuracy with Aspose AI post‑processing.
  name: How to Perform OCR in Python – Complete Aspose OCR & AI Guide
  steps:
  - name: Expected Output
    text: '``` === Raw OCR === Inv0ice #12345 Date: 2023-08-15 Total: $1,23O'
  - name: What if I don’t have a GPU?
    text: Set `model_config.gpu_layers = 0` and optionally increase `model_config.context_size`
      to 2048 for better CPU performance. The model will run slower, but you still
      get the same quality of correction.
  - name: My image is rotated—will `load_image` handle it?
    text: 'Aspose OCR automatically detects orientation, but for extremely skewed
      scans you may want to pre‑rotate using Pillow:'
  - name: How do I process multiple files in a folder?
    text: Wrap the whole pipeline in a `for` loop and store each `enhanced_text` in
      a list or write directly to a CSV. Remember to call `ocr_ai.free_resources()`
      **once** after the loop, not after each file—re‑initialising the model repeatedly
      is wasteful.
  - name: Can I swap the language model?
    text: Absolutely. Just change `model_config.hugging_face_repo_id` to any GGUF‑compatible
      model on Hugging Face (e.g., `Meta/Llama-3.2-1B-Instruct-GGUF`). Keep the quantization
      setting consistent with your hardware.
  type: HowTo
tags:
- OCR
- Python
- Aspose
- AI
title: Comment effectuer l'OCR en Python – Guide complet Aspose OCR & IA
url: /fr/python/general/how-to-perform-ocr-in-python-complete-aspose-ocr-ai-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR en Python – Guide complet Aspose OCR & IA

Vous vous êtes déjà demandé **comment effectuer de l'OCR** en Python sans vous battre avec des astuces d'image bas‑niveau ? Vous n'êtes pas seul. Dans ce tutoriel, nous parcourrons le chargement d'une image pour l'OCR, l'extraction de texte brut, puis le polissage du résultat avec le post‑processeur IA d'Aspose. À la fin, vous disposerez d'un script prêt à l'emploi qui transforme des scans bruyants en texte propre et consultable—sans services supplémentaires requis.

Nous couvrirons tout, de l'installation du SDK à la libération des ressources dans les applications à long terme. Si vous avez déjà essayé de **charger une image pour l'OCR** et obtenu un méli-mélo, ce guide est l'antidote. Vous verrez pourquoi combiner l'OCR traditionnel avec un modèle de langage donne des résultats qui semblent avoir été tapés par un humain.

## Prérequis

- Python 3.9 ou plus récent (le code utilise des annotations de type que les interpréteurs plus anciens n’aiment pas)
- Une licence Aspose OCR active ou un essai gratuit (l'édition communautaire fonctionne pour l'évaluation)
- Un GPU avec au moins 4 Go de VRAM si vous souhaitez accélérer le modèle IA (optionnel mais apprécié)
- Une image d'exemple, par ex. `sample_invoice.png`, placée à un endroit que vous pouvez référencer

Si l'un de ces éléments vous est inconnu, ne paniquez pas—l'installation du SDK se fait en une seule ligne, et les paramètres du GPU peuvent être désactivés plus tard.

## Étape 1 : Installer Aspose OCR et les dépendances

Ouvrez un terminal et exécutez :

```bash
pip install aspose-ocr
pip install aspose-ocr-ai
```

Le premier paquet vous fournit `aspose.ocr`, le second ajoute les utilitaires du post‑processeur IA. Les deux sont des wheels Python purs, vous n’aurez donc rien à compiler vous‑même.

## Étape 2 : Charger l'image pour l'OCR et initialiser le moteur

Nous allons maintenant **charger une image pour l'OCR** en utilisant le `OcrEngine` d'Aspose. Considérez cela comme remettre une feuille de papier à un employé très assidu qui lit chaque caractère.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Initialise the basic OCR engine
ocr_engine = aocr.OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

# Perform a plain OCR scan – this returns a raw string
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)
```

> **Pourquoi c'est important :** L'appel `load_image` est le pont entre votre système de fichiers et le moteur OCR. Si le chemin est incorrect, vous obtiendrez une `FileNotFoundError` avant même que la reconnaissance ne commence. Vérifiez toujours les séparateurs de répertoires, surtout sous Windows vs. macOS/Linux.

## Étape 3 : Configurer le post‑processeur IA d'Aspose

Aspose AI peut télécharger un modèle de langage depuis Hugging Face, le mettre en cache localement, et exécuter l'inférence sur votre GPU (ou CPU). Ci-dessous nous configurons un modèle léger de 3 milliards de paramètres qui tient sur la plupart des ordinateurs portables modernes.

```python
# Initialise the AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()

# Allow the SDK to fetch the model automatically
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"

# Use half of the GPU layers – balances speed and VRAM usage
model_config.gpu_layers = 20
model_config.context_size = 1024

# Load (or download) the model now
ocr_ai.initialize(model_config)
```

> **Astuce :** Si vous êtes sur une machine uniquement CPU, définissez `gpu_layers = 0`. Le modèle fonctionnera toujours, juste un peu plus lent. La quantification `int8` garde l'empreinte mémoire minuscule tout en préservant la plupart de la précision du modèle.

## Étape 4 : Enregistrer un post‑processeur personnalisé

Le modèle IA a besoin d'une invite qui lui indique quoi faire. Ici, nous lui demandons d'agir comme un relecteur OCR, corrigeant les fautes d'orthographe, fusionnant les mots cassés et supprimant les artefacts.

```python
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    # Temperature 0.0 makes the output deterministic
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

# Hook the custom processor into the AI pipeline
ocr_ai.set_post_processor(correction_processor, custom_settings=None)
```

> **Pourquoi un processeur personnalisé ?** Le post‑processeur par défaut pourrait ajouter des explications supplémentaires ou du formatage dont vous n’avez pas besoin. En fournissant notre propre fonction, nous conservons la sortie strictement comme texte nettoyé, ce qui est parfait pour l'indexation en aval ou le stockage en base de données.

## Étape 5 : Exécuter le pipeline OCR amélioré par l'IA

Nous injectons maintenant la sortie OCR brute dans la couche IA. Le moteur appellera notre `correction_processor`, qui à son tour communique avec le modèle de langage.

```python
# Apply the AI post‑processor to the raw OCR result
enhanced_text = ocr_ai.run_postprocessor(raw_text)

print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)
```

Vous devriez constater une amélioration notable : les caractères manquants sont restaurés, les erreurs courantes d'OCR comme “0” vs “O” sont corrigées, et les sauts de ligne deviennent plus logiques.

## Étape 6 : Nettoyage – Libérer les ressources

Si vous prévoyez d'exécuter cela au sein d'un service web ou d'un démon de longue durée, libérer la mémoire GPU est crucial. Oublier d'appeler `free_resources` peut entraîner des plantages « out‑of‑memory » après quelques centaines de requêtes.

```python
ocr_ai.free_resources()
```

C’est tout—votre pipeline OCR complet est maintenant prêt pour la production.

## Récapitulatif du script complet

Ci-dessous le script complet et exécutable. Copiez‑collez‑le dans un fichier nommé `ocr_with_ai.py`, ajustez le chemin de l'image, et exécutez `python ocr_with_ai.py`.

```python
import aspose.ocr as aocr
import aspose.ocr.ai as aocr_ai

# Step 1: Load image for OCR and perform basic recognition
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize()
print("=== Raw OCR ===")
print(raw_text)

# Step 2: Initialise the Aspose AI post‑processor
ocr_ai = aocr_ai.AsposeAI()
model_config = aocr_ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "int8"
model_config.gpu_layers = 20          # half of GPU layers
model_config.context_size = 1024
ocr_ai.initialize(model_config)

# Step 3: Register custom correction processor
def correction_processor(text, settings):
    prompt = (
        "You are an OCR post‑processor. Fix any spelling or OCR errors in the following "
        "text and return ONLY the cleaned version:\n\n"
        f"{text}"
    )
    return ocr_ai.run_inference(prompt, temperature=0.0, max_new_tokens=512)

ocr_ai.set_post_processor(correction_processor, custom_settings=None)

# Step 4: Run AI post‑processor on raw OCR output
enhanced_text = ocr_ai.run_postprocessor(raw_text)
print("\n=== AI‑enhanced OCR ===")
print(enhanced_text)

# Step 5: Release resources (important for long‑running apps)
ocr_ai.free_resources()
```

### Sortie attendue

```
=== Raw OCR ===
Inv0ice #12345
Date: 2023-08-15
Total: $1,23O

=== AI‑enhanced OCR ===
Invoice #12345
Date: 2023-08-15
Total: $1,230
```

Remarquez comment “Inv0ice” devient “Invoice” et le “O” errant après le montant disparaît. C’est l'IA qui fait sa magie.

## Questions fréquentes & cas limites

### Et si je n’ai pas de GPU ?

Définissez `model_config.gpu_layers = 0` et augmentez éventuellement `model_config.context_size` à 2048 pour de meilleures performances CPU. Le modèle fonctionnera plus lentement, mais vous obtenez toujours la même qualité de correction.

### Mon image est tournée—`load_image` la gérera‑t‑elle ?

Aspose OCR détecte automatiquement l'orientation, mais pour des scans extrêmement inclinés vous pouvez vouloir pré‑tourner avec Pillow :

```python
from PIL import Image
img = Image.open("sample.png")
rotated = img.rotate(90, expand=True)
rotated.save("rotated.png")
ocr_engine.load_image("rotated.png")
```

### Comment traiter plusieurs fichiers dans un dossier ?

Enveloppez tout le pipeline dans une boucle `for` et stockez chaque `enhanced_text` dans une liste ou écrivez directement dans un CSV. N'oubliez pas d'appeler `ocr_ai.free_resources()` **une seule fois** après la boucle, pas après chaque fichier—ré‑initialiser le modèle à chaque fois est gaspilleur.

```python
import os

for filename in os.listdir("invoices"):
    if filename.lower().endswith(".png"):
        ocr_engine.load_image(os.path.join("invoices", filename))
        raw = ocr_engine.recognize()
        clean = ocr_ai.run_postprocessor(raw)
        # Save or index `clean`
```

### Puis‑je changer le modèle de langage ?

Absolument. Changez simplement `model_config.hugging_face_repo_id` vers n'importe quel modèle compatible GGUF sur Hugging Face (par ex., `Meta/Llama-3.2-1B-Instruct-GGUF`). Conservez le paramètre de quantification cohérent avec votre matériel.

## Astuces pro & pièges

- **Astuce pro :** Définissez `temperature=0.0` pour des corrections déterministes. Des températures plus élevées peuvent introduire des changements créatifs mais incorrects.
- **Attention à :** Les documents extrêmement longs (> 5000 caractères). La fenêtre de contexte du modèle est limitée à 1024 tokens dans l'exemple ; divisez le texte en paragraphes avant de l'envoyer à l'IA.
- **Note de sécurité :** Si vous exécutez cela dans un environnement réglementé, assurez‑vous que l'URL de téléchargement du modèle est sur liste blanche. Le drapeau `allow_auto_download` peut

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Comment utiliser AspOCR : filtres de prétraitement d'image OCR pour .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}