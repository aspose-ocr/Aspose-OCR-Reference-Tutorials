---
category: general
date: 2026-05-03
description: extraire du texte d’une image à l’aide d’Aspose OCR et de la correction
  orthographique IA. Apprenez comment OCRiser une image, charger une image pour l’OCR,
  reconnaître le texte d’une facture et libérer les ressources GPU.
draft: false
keywords:
- extract text from image
- how to ocr image
- load image for ocr
- release gpu resources
- recognize text from invoice
language: fr
og_description: extraire du texte d’une image avec Aspose OCR et la correction orthographique
  IA. Guide étape par étape couvrant comment OCRiser une image, charger l’image pour
  l’OCR et libérer les ressources GPU.
og_title: extraire du texte d’une image – Guide complet d’OCR et de vérification orthographique
tags:
- OCR
- Aspose
- AI
- Python
title: extraire du texte d’une image – OCR avec le correcteur orthographique Aspose
  AI
url: /fr/python/general/extract-text-from-image-ocr-with-aspose-ai-spell-check/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extraire du texte d'image – Guide complet OCR & Spell‑Check

Vous avez déjà eu besoin d'**extraire du texte d'image** sans savoir quelle bibliothèque offrirait à la fois rapidité et précision ? Vous n'êtes pas seul. Dans de nombreux projets réels—pensons au traitement de factures, à la numérisation de reçus ou à la lecture de contrats—obtenir du texte propre et interrogeable à partir d’une photo est le premier obstacle.

Bonne nouvelle : Aspose OCR associé à un modèle léger Aspose AI peut accomplir cette tâche en quelques lignes de Python. Dans ce tutoriel, nous verrons **comment OCR une image**, charger correctement l’image, exécuter un post‑processeur de vérification orthographique intégré, puis **libérer les ressources GPU** afin que votre application reste économe en mémoire.

À la fin de ce guide, vous serez capable de **reconnaître le texte d'images de factures**, corriger automatiquement les erreurs courantes d’OCR et garder votre GPU propre pour le lot suivant.

---

## Ce dont vous avez besoin

- Python 3.9 ou plus récent (le code utilise des annotations de type mais fonctionne sur les versions 3.x antérieures)
- Packages `aspose-ocr` et `aspose-ai` (installez avec `pip install aspose-ocr aspose-ai`)
- Un GPU compatible CUDA est optionnel ; le script reviendra au CPU si aucun n’est détecté.
- Une image d’exemple, par ex. `sample_invoice.png`, placée dans un dossier accessible.

Pas de frameworks ML lourds, pas de téléchargements de modèles massifs—juste un petit modèle quantisé Q4‑K‑M qui tient confortablement sur la plupart des GPU.

---

## Étape 1 : Initialiser le moteur OCR – extraire du texte d'image

La première chose à faire est de créer une instance `OcrEngine` et d’indiquer la langue attendue. Ici nous choisissons l’anglais et demandons une sortie en texte brut, idéale pour le traitement en aval.

```python
import aocr  # Aspose OCR package
import aspose.ai as ai  # Aspose AI package

# Initialise the OCR engine
ocr_engine = aocr.OcrEngine()
ocr_engine.language = aocr.Language.English            # Choose any supported language
ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Plain text makes post‑processing easier
```

**Pourquoi c'est important :** définir la langue restreint l’ensemble de caractères, améliorant ainsi la précision. Le mode texte brut supprime les informations de mise en page dont vous n’avez généralement pas besoin lorsque vous ne faites qu’extraire du texte d'image.

---

## Étape 2 : Charger l'image pour l'OCR – comment OCR une image

Nous transmettons maintenant une vraie image au moteur. L’assistant `Image.load` comprend les formats courants (PNG, JPEG, TIFF) et masque les particularités d’E/S de fichiers.

```python
# Load the input image – this is the "load image for OCR" step
input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
raw_text = ocr_engine.recognize(input_image)  # Returns the recognised text as a string
```

**Astuce :** si vos images sources sont volumineuses, pensez à les redimensionner avant de les envoyer au moteur ; des dimensions plus petites peuvent réduire l’utilisation de la mémoire GPU sans nuire à la qualité de reconnaissance.

---

## Étape 3 : Configurer le modèle Aspose AI – reconnaître le texte d'une facture

Aspose AI fournit un petit modèle GGUF que vous pouvez télécharger automatiquement. L’exemple utilise le dépôt `Qwen2.5‑3B‑Instruct‑GGUF`, quantisé en `q4_k_m`. Nous indiquons également au runtime d’allouer 20 couches sur le GPU, ce qui équilibre vitesse et consommation de VRAM.

```python
# Model configuration – auto‑download a small Q4‑K‑M quantised model
model_config = ai.AsposeAIModelConfig()
model_config.allow_auto_download = "true"
model_config.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
model_config.hugging_face_quantization = "q4_k_m"
model_config.gpu_layers = 20  # Use 20 GPU layers when a GPU is available
```

**Dans les coulisses :** le modèle quantisé occupe environ 1,5 Go sur le disque, une fraction d’un modèle en pleine précision, tout en conservant suffisamment de nuances linguistiques pour repérer les fautes d’OCR typiques.

---

## Étape 4 : Initialiser AsposeAI et attacher le post‑processeur de vérification orthographique

Aspose AI inclut un post‑processeur de vérification orthographique prêt à l’emploi. En l’attachez, chaque résultat d’OCR sera automatiquement nettoyé.

```python
# Initialise AsposeAI and attach the built‑in spell‑check post‑processor
ocr_ai = ai.AsposeAI(model_config)  # Pass the config we just built
ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})  # Empty dict → default settings
```

**Pourquoi utiliser le post‑processeur ?** Les moteurs OCR confondent souvent « Invoice » avec « Invo1ce » ou « Total » avec « T0tal ». La vérification orthographique exécute un modèle linguistique léger sur la chaîne brute et corrige ces erreurs sans que vous ayez à créer un dictionnaire personnalisé.

---

## Étape 5 : Exécuter le post‑processeur de vérification orthographique sur le résultat OCR

Une fois tout branché, un seul appel renvoie le texte corrigé. Nous affichons également les versions originale et nettoyée afin que vous puissiez constater l’amélioration.

```python
# Run the spell‑check post‑processor on the OCR result
corrected_text = ocr_ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Corrected:", corrected_text)
```

Un résultat typique pour une facture pourrait ressembler à ceci :

```
Original : Invo1ce #12345
Date: 2023/07/15
Total: $1,250.00
...
Corrected: Invoice #12345
Date: 2023/07/15
Total: $1,250.00
...
```

Remarquez comment « Invo1ce » est devenu le mot correct « Invoice ». C’est la puissance du correcteur orthographique intégré basé sur l’IA.

---

## Étape 6 : Libérer les ressources GPU – libérer les ressources GPU en toute sécurité

Si vous exécutez cela dans un service de longue durée (par ex. une API web qui traite des dizaines de factures par minute), vous devez libérer le contexte GPU après chaque lot. Sinon vous verrez des fuites de mémoire et, finalement, des erreurs « CUDA out of memory ».

```python
# Release GPU resources – crucial to avoid memory leaks
ocr_ai.free_resources()
```

**Astuce pro :** appelez `free_resources()` dans un bloc `finally` ou un gestionnaire de contexte afin qu’il s’exécute toujours, même en cas d’exception.

---

## Exemple complet fonctionnel

Assembler toutes les pièces donne un script autonome que vous pouvez intégrer à n’importe quel projet.

```python
# extract_text_from_image.py
import aocr
import aspose.ai as ai

def main():
    # Step 1: Initialise OCR engine
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain

    # Step 2: Load image for OCR
    input_image = aocr.Image.load("YOUR_DIRECTORY/sample_invoice.png")
    raw_text = ocr_engine.recognize(input_image)

    # Step 3: Configure Aspose AI model
    model_cfg = ai.AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 20

    # Step 4: Initialise AI and attach spell‑check
    ocr_ai = ai.AsposeAI(model_cfg)
    ocr_ai.set_post_processor(ocr_ai.postprocessor_spell_check, {})

    # Step 5: Run spell‑check
    corrected_text = ocr_ai.run_postprocessor(raw_text)

    print("Original :", raw_text)
    print("Corrected:", corrected_text)

    # Step 6: Release GPU resources
    ocr_ai.free_resources()

if __name__ == "__main__":
    main()
```

Enregistrez le fichier, ajustez le chemin vers votre image, puis lancez `python extract_text_from_image.py`. Vous devriez voir le texte de la facture nettoyé s’afficher dans la console.

---

## Questions fréquentes (FAQ)

**Q : Cela fonctionne-t-il sur des machines uniquement CPU ?**  
R : Absolument. Si aucun GPU n’est détecté, Aspose AI revient à l’exécution CPU, bien que plus lente. Vous pouvez forcer le CPU en réglant `model_cfg.gpu_layers = 0`.

**Q : Et si mes factures sont dans une langue autre que l’anglais ?**  
R : Modifiez `ocr_engine.language` avec la valeur d’énumération appropriée (par ex. `aocr.Language.Spanish`). Le modèle de vérification orthographique est multilingue, mais vous obtiendrez de meilleurs résultats avec un modèle spécifique à la langue.

**Q : Puis‑je traiter plusieurs images dans une boucle ?**  
R : Oui. Placez simplement les étapes de chargement, de reconnaissance et de post‑traitement à l’intérieur d’une boucle `for`. N’oubliez pas d’appeler `ocr_ai.free_resources()` après la boucle ou après chaque lot si vous réutilisez la même instance AI.

**Q : Quelle est la taille du téléchargement du modèle ?**  
R : Environ 1,5 Go pour la version quantisée `q4_k_m`. Il est mis en cache après la première exécution, de sorte que les exécutions suivantes sont instantanées.

---

## Conclusion

Dans ce tutoriel, nous avons montré comment **extraire du texte d'image** avec Aspose OCR, configurer un petit modèle IA, appliquer un post‑processeur de vérification orthographique et libérer en toute sécurité les **ressources GPU**. Le flux couvre tout, du chargement de l’image au nettoyage final, vous offrant une chaîne fiable pour les scénarios **reconnaître le texte d’une facture**.

Prochaines étapes ? Essayez de remplacer le spell‑check par un modèle d’**entity‑extraction** personnalisé

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}