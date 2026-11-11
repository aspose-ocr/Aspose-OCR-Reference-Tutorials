---
category: general
date: 2026-09-25
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) sur
  une image avec Aspose OCR, à charger l'image pour l'OCR et à reconnaître le texte
  d’un reçu dans un exemple complet en Python.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- load image for OCR
- recognize text from receipt
- Aspose OCR Python
- AI post‑processor OCR
language: fr
lastmod: 2026-09-25
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  avec Aspose OCR en Python. Ce guide montre comment charger une image pour l’OCR
  et reconnaître le texte d’un reçu grâce à l’amélioration par IA.
og_image_alt: Screenshot of Python code performing OCR on an image and showing original
  vs AI‑enhanced text
og_title: Effectuer la reconnaissance optique de caractères sur une image avec Aspose
  OCR et le post‑processeur IA – Guide Python
schemas:
- author: Aspose
  dateModified: '2026-09-25'
  description: Learn how to perform OCR on image with Aspose OCR, load image for OCR,
    and recognize text from receipt in a complete Python example.
  headline: How to perform OCR on image using Aspose OCR and AI post‑processor in
    Python
  type: TechArticle
tags:
- OCR
- Python
- Aspose
title: Comment effectuer la reconnaissance optique de caractères (OCR) sur une image
  en utilisant Aspose OCR et le post‑processeur IA en Python
url: /fr/python/general/how-to-perform-ocr-on-image-using-aspose-ocr-and-ai-post-pro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR sur une image avec Aspose OCR et le post‑processeur IA en Python

Si vous devez **effectuer une OCR sur des fichiers image** en Python, ce tutoriel vous montre une solution complète, prête à l’emploi. Vous apprendrez comment **charger une image pour l’OCR**, exécuter le moteur Aspose OCR, et **reconnaître le texte à partir de documents de reçu** avec un post‑traitement optionnel piloté par l’IA.

Nous parcourrons chaque étape, de l’installation du SDK à la libération des ressources, afin que vous puissiez intégrer une extraction de texte fiable dans vos propres applications sans rien laisser au hasard.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Python 3.8+ installé  
- Aspose OCR pour Python via pip (`pip install aspose-ocr`)  
- Un accès Internet pour le téléchargement optionnel du modèle IA  
- Une image de reçu d’exemple (`receipt.png`) placée dans un répertoire connu  

Aucun service externe supplémentaire n’est requis ; le code s’exécute localement et utilise le modèle gratuit Qwen2‑3B‑Instruct lorsque des couches GPU sont disponibles.

## Étape 1 : Installer les packages requis

```bash
pip install aspose-ocr
```

Le package `aspose-ocr` contient à la fois la classe `OcrEngine` et le post‑processeur `AsposeAI` que nous utiliserons pour **effectuer une OCR sur des fichiers image**.

## Étape 2 : Créer et configurer le moteur OCR – charger l’image pour l’OCR

```python
from aspose.ocr import OcrEngine

# Initialise the OCR engine
ocr_engine = OcrEngine()

# Load the image you want to process
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # <-- load image for OCR
```

Appeler `load_image` indique au moteur quel fichier analyser. Vous pouvez remplacer le chemin par n’importe quel fichier PNG, JPG ou TIFF que vous devez **effectuer une OCR sur image**.

## Étape 3 : Configurer le post‑processeur AsposeAI optionnel

Le post‑processeur IA peut corriger l’orthographe, améliorer le formatage ou appliquer une logique personnalisée après que le résultat brut de l’OCR soit retourné.

```python
from aspose.ocr import AsposeAI, AsposeAIModelConfig

# Initialise the AI processor (logging is optional)
ai_processor = AsposeAI()   # AsposeAI(logging=my_logger)

# Define which model to use – it will auto‑download if missing
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20                     # use GPU layers when available
)

# Load the model configuration into the processor
ai_processor.initialize(model_config)   # implicit in many examples
```

La configuration indique au processeur de télécharger le modèle Qwen2 par défaut, vous permettant de **effectuer une OCR sur image** avec une compréhension linguistique de haut niveau.

## Étape 4 : Attacher une fonction de post‑traitement simple

Vous pouvez brancher n’importe quel callable qui reçoit le texte brut et renvoie une version corrigée. Voici un exemple minimal qui corrige une faute de frappe courante :

```python
def simple_spell_check(text, **kwargs):
    """Correct a frequent misspelling in receipt OCR results."""
    return text.replace("reciept", "receipt")

# Register the function with the AI processor
ai_processor.set_post_processor(simple_spell_check, {})
```

Comme la fonction est enregistrée, chaque fois que vous appelez `run_postprocessor`, la sortie de l’OCR passera par cette étape.

## Étape 5 : Exécuter l’OCR et améliorer le résultat – reconnaître le texte du reçu

```python
# Perform the core OCR operation
raw_result = ocr_engine.recognize()          # <-- recognize text from receipt

# Let the AI processor improve the raw output
enhanced_result = ai_processor.run_postprocessor(raw_result)

# Display both versions
print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)
```

L’appel `recognize` renvoie un objet dont l’attribut `text` contient les caractères bruts extraits de l’image du reçu. L’appel suivant `run_postprocessor` renvoie un nouveau résultat où notre correcteur orthographique (et toute amélioration basée sur le modèle) a été appliqué.

### Résultat attendu

```
Original OCR : Total: $23.45\nSubtotl: $20.00\nTax: $3.45\nThank you for your reciept
AI‑enhanced  : Total: $23.45
Subtotal: $20.00
Tax: $3.45
Thank you for your receipt
```

Remarquez comment le texte amélioré par l’IA corrige la faute de frappe et insère des sauts de ligne pour une meilleure lisibilité — exactement ce que vous souhaitez lorsque vous **reconnaissez le texte à partir de reçus**.

## Étape 6 : Nettoyer les ressources

```python
# Release memory held by the AI processor
ai_processor.free_resources()

# Dispose of the OCR engine
ocr_engine.dispose()
```

Libérer les ressources est particulièrement important lorsqu’on traite de nombreuses images dans un service à long terme.

## Script complet exécutable

Assembler toutes les pièces vous donne un script unique que vous pouvez copier, coller et exécuter :

```python
# ocr_receipt.py
from aspose.ocr import AsposeAI, AsposeAIModelConfig, OcrEngine

# 1️⃣ Initialise OCR engine and load the image
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/receipt.png")   # load image for OCR

# 2️⃣ Set up optional AI post‑processor
ai_processor = AsposeAI()
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20
)
ai_processor.initialize(model_config)

# 3️⃣ Register a simple spell‑check function
def simple_spell_check(text, **kwargs):
    return text.replace("reciept", "receipt")
ai_processor.set_post_processor(simple_spell_check, {})

# 4️⃣ Perform OCR and enhance the result
raw_result = ocr_engine.recognize()                # recognize text from receipt
enhanced_result = ai_processor.run_postprocessor(raw_result)

print("Original OCR :", raw_result.text)
print("AI‑enhanced  :", enhanced_result.text)

# 5️⃣ Release resources
ai_processor.free_resources()
ocr_engine.dispose()
```

Exécutez le script avec :

```bash
python ocr_receipt.py
```

Vous devriez voir les sorties originales et améliorées par l’IA affichées dans la console.

## Astuces professionnelles et pièges courants

- **La qualité de l’image compte** — assurez‑vous que le reçu soit bien éclairé et pas trop compressé ; sinon le moteur OCR risque de manquer des caractères, réduisant l’avantage du post‑traitement.  
- **Disponibilité du GPU** — si votre machine ne possède pas de GPU compatible, définissez `gpu_layers=0` pour forcer l’inférence CPU ; le modèle fonctionnera toujours, bien que plus lentement.  
- **Post‑processeurs personnalisés** — vous pouvez chaîner plusieurs fonctions ou utiliser un modèle de langage plus sophistiqué pour reformater les dates, montants ou noms de fournisseurs.  
- **Traitement par lots** — créez une seule instance `AsposeAI` et réutilisez‑la à travers de nombreuses instances `OcrEngine` afin d’éviter des téléchargements répétés du modèle.  

## Conclusion

Vous savez maintenant comment **effectuer une OCR sur des fichiers image** avec Aspose OCR, comment **charger une image pour l’OCR**, et comment **reconnaître le texte à partir de reçus** avec des améliorations pilotées par l’IA. En suivant les étapes ci‑dessus, vous pouvez intégrer un traitement de reçus précis et à haut débit dans n’importe quelle application Python.

**Prochaines étapes** : explorez des techniques de post‑traitement supplémentaires comme la normalisation des devises, intégrez le résultat dans une base de données, ou passez à un modèle plus grand pour des reçus multilingues. Pour une personnalisation plus poussée, consultez la documentation Aspose OCR sur les packs de langues personnalisés et le pré‑traitement avancé d’image.

Bon codage !

## Que devez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Perform OCR in C# – Extract Text from Image Using Aspose OCR](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image-using-aspose/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}