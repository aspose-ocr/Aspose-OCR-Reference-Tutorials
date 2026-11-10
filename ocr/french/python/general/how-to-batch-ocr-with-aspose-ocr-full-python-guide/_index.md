---
category: general
date: 2026-05-03
description: Comment effectuer une reconnaissance OCR par lots d’images avec Aspose
  OCR et la vérification orthographique IA. Apprenez à extraire le texte des images,
  appliquer la vérification orthographique, libérer les ressources IA et corriger
  les erreurs d’OCR.
draft: false
keywords:
- how to batch ocr
- extract text from images
- free ai resources
- apply spell check
- correct ocr errors
language: fr
og_description: Comment traiter en lot des images avec OCR en utilisant Aspose OCR
  et la correction orthographique IA. Suivez un guide étape par étape pour extraire
  le texte des images, appliquer la vérification orthographique, exploiter des ressources
  IA gratuites et corriger les erreurs d’OCR.
og_title: Comment réaliser une OCR par lots avec Aspose OCR – Tutoriel complet Python
tags:
- OCR
- Python
- AI
- Aspose
title: Comment faire de l'OCR par lots avec Aspose OCR – Guide complet Python
url: /fr/python/general/how-to-batch-ocr-with-aspose-ocr-full-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire du OCR par lots avec Aspose OCR – Guide complet Python

Vous vous êtes déjà demandé **comment faire du OCR par lots** sur un dossier entier de PDF numérisés ou de photos sans écrire un script séparé pour chaque fichier ? Vous n'êtes pas seul. Dans de nombreuses pipelines réelles, vous devez **extraire du texte d'images**, corriger les fautes d'orthographe, et enfin libérer les ressources IA que vous avez allouées. Ce tutoriel vous montre exactement comment faire cela avec Aspose OCR, un post‑processeur IA léger, et quelques lignes de Python.

Nous allons parcourir l'initialisation du moteur OCR, l'intégration d'un correcteur orthographique IA, la boucle sur un répertoire d'images, et le nettoyage du modèle à la fin. À la fin, vous disposerez d'un script prêt à l'emploi qui **corrige automatiquement les erreurs OCR** et libère les **ressources IA** afin que votre GPU reste heureux.

## Ce dont vous avez besoin

- Python 3.9+ (le code utilise des annotations de type mais fonctionne sur les versions 3.x antérieures)
- `asposeocr` package (`pip install asposeocr`) – fournit le moteur OCR.
- Accès au modèle Hugging Face `bartowski/Qwen2.5-3B-Instruct-GGUF` (téléchargé automatiquement).
- Un GPU avec au moins quelques Go de VRAM (le script définit `gpu_layers = 30`, vous pouvez le réduire si nécessaire).

Aucun service externe, aucune API payante – tout s'exécute localement.

---

## Étape 1 : Configurer le moteur OCR – **Comment faire du OCR par lots** efficacement

Avant de pouvoir traiter mille images, nous avons besoin d'un moteur OCR solide. Aspose OCR nous permet de choisir la langue et le mode de reconnaissance en un seul appel.

```python
# Step 1: Initialize the OCR engine for English plain‑text output
def init_ocr() -> aocr.OcrEngine:
    ocr_engine = aocr.OcrEngine()
    ocr_engine.language = aocr.Language.English          # English language pack
    ocr_engine.recognize_mode = aocr.RecognitionMode.Plain  # Returns raw string, no layout
    return ocr_engine
```

**Pourquoi c’est important :** Définir `recognize_mode` à `Plain` garde la sortie légère, ce qui est idéal lorsque vous prévoyez d'exécuter une vérification orthographique plus tard. Si vous avez besoin d'informations de mise en page, vous passeriez à `Layout`, mais cela ajoute une surcharge que vous ne voulez probablement pas dans un travail par lots.

> **Astuce :** Si vous traitez des scans multilingues, vous pouvez passer une liste comme `ocr_engine.language = [aocr.Language.English, aocr.Language.Spanish]`.

---

## Étape 2 : Initialiser le post‑processeur IA – **Appliquer la vérification orthographique** à la sortie OCR

Aspose AI est fourni avec un post‑processeur intégré qui peut exécuter n'importe quel modèle de votre choix. Ici, nous récupérons un modèle Qwen 2.5 quantifié depuis Hugging Face et connectons la routine de vérification orthographique.

```python
# Step 2: Configure and start the AI post‑processor
def init_ai() -> aocr.ai.AsposeAI:
    model_cfg = AsposeAIModelConfig()
    model_cfg.allow_auto_download = "true"
    model_cfg.hugging_face_repo_id = "bartowski/Qwen2.5-3B-Instruct-GGUF"
    model_cfg.hugging_face_quantization = "q4_k_m"
    model_cfg.gpu_layers = 30          # Adjust based on your GPU memory
    ai_processor = AsposeAI()
    ai_processor.initialize(model_cfg)

    # Attach the built‑in spell‑check post‑processor
    ai_processor.set_post_processor(ai_processor.postprocessor_spell_check, {})
    return ai_processor
```

**Pourquoi c’est important :** Le modèle est quantifié (`q4_k_m`), ce qui réduit considérablement l'utilisation de mémoire tout en offrant une compréhension linguistique décente. En appelant `set_post_processor`, nous indiquons à Aspose AI d'exécuter automatiquement l'étape **apply spell check** sur toute chaîne que nous lui fournissons.

> **Attention :** Si votre GPU ne peut pas gérer 30 couches, réduisez le nombre à 15 voire 5 – le script fonctionnera toujours, simplement un peu plus lent.

---

## Étape 3 : Exécuter l'OCR et **corriger les erreurs OCR** sur une seule image

Maintenant que le moteur OCR et le correcteur orthographique IA sont prêts, nous les combinons. Cette fonction charge une image, extrait le texte brut, puis exécute le post‑processeur IA pour le nettoyer.

```python
# Step 3: OCR an image and run the spell‑check post‑processor
def ocr_and_correct(image_path: str,
                    ocr_engine: aocr.OcrEngine,
                    ai_processor: aocr.ai.AsposeAI) -> str:
    image = aocr.Image.load(image_path)               # Load any supported format
    raw_text = ocr_engine.recognize(image)           # Plain string from OCR
    corrected_text = ai_processor.run_postprocessor(raw_text)
    return corrected_text
```

**Pourquoi c’est important :** Alimenter directement la chaîne OCR brute dans le modèle IA nous donne un passage **correct OCR errors** sans écrire de regexes ou de dictionnaires personnalisés. Le modèle comprend le contexte, il peut corriger « recieve » → « receive » et même des erreurs plus subtiles.

---

## Étape 4 : **Extraire du texte d'images** en masse – La vraie boucle par lots

C’est ici que la magie du **how to batch OCR** se révèle. Nous parcourons un répertoire, ignorons les fichiers non pris en charge, et écrivons chaque sortie corrigée dans un fichier `.txt`.

```python
# Step 4: Process an entire folder of images
if __name__ == "__main__":
    # Initialize once – reuse for every file
    ocr_engine = init_ocr()
    ai_processor = init_ai()

    input_dir = "YOUR_DIRECTORY/input_images"
    output_dir = "YOUR_DIRECTORY/output_text"
    os.makedirs(output_dir, exist_ok=True)

    for file_name in os.listdir(input_dir):
        # Only handle common image extensions
        if not file_name.lower().endswith(('.png', '.jpg', '.jpeg', '.tif', '.tiff')):
            continue

        image_path = os.path.join(input_dir, file_name)
        corrected = ocr_and_correct(image_path, ocr_engine, ai_processor)

        txt_path = os.path.join(output_dir,
                                os.path.splitext(file_name)[0] + ".txt")
        with open(txt_path, "w", encoding="utf-8") as txt_file:
            txt_file.write(corrected)

        print(f"Processed {file_name}")

    # Step 5: Release **free AI resources** after the batch finishes
    ai_processor.free_resources()
```

### Sortie attendue

Pour une image contenant la phrase *« The quick brown fox jumps over the lazzy dog. »* vous verrez un fichier texte contenant :

```
The quick brown fox jumps over the lazy dog.
```

Remarquez que le double « z » a été corrigé automatiquement – c’est le correcteur orthographique IA en action.

**Pourquoi c’est important :** En créant les objets OCR et IA **une seule fois** et en les réutilisant, nous évitons le surcoût de chargement du modèle pour chaque fichier. C’est la façon la plus efficace de **how to batch OCR** à grande échelle.

---

## Étape 5 : Nettoyer – **Libérer les ressources IA** correctement

Lorsque vous avez terminé, appeler `free_resources()` libère la mémoire GPU, les contextes CUDA, et tous les fichiers temporaires créés par le modèle.

```python
# Step 5: Explicitly free GPU and model memory
ai_processor.free_resources()
```

Ignorer cette étape peut laisser des allocations GPU en suspens, ce qui pourrait faire planter les processus Python suivants ou consommer de la VRAM. Considérez cela comme l’étape « éteindre les lumières » d’un travail par lots.

---

## Pièges courants & astuces supplémentaires

| Issue | What to Look For | Fix |
|-------|------------------|-----|
| **Erreurs de mémoire insuffisante** | Le GPU s'épuise après quelques dizaines d'images | Réduisez `gpu_layers` ou passez au CPU (`model_cfg.gpu_layers = 0`). |
| **Pack de langue manquant** | OCR renvoie des chaînes vides | Assurez‑vous que la version `asposeocr` inclut les données de langue anglaise ; réinstallez si nécessaire. |
| **Fichiers non‑image** | Le script plante sur un `.pdf` errant | La garde `if not file_name.lower().endswith(...)` les ignore déjà. |
| **Vérification orthographique non appliquée** | La sortie ressemble à l'OCR brut | Vérifiez que `ai_processor.set_post_processor` a été appelé avant la boucle. |
| **Vitesse de lot lente** | Prend plus de 5 secondes par image | Activez `model_cfg.allow_auto_download = "false"` après la première exécution, afin que le modèle ne soit pas re‑téléchargé à chaque fois. |

**Astuce :** Si vous devez **extraire du texte d'images** dans une langue autre que l'anglais, changez simplement `ocr_engine.language` à l'énumération appropriée (par ex., `aocr.Language.French`). Le même post‑processeur IA appliquera toujours la vérification orthographique, mais vous pourriez vouloir un modèle spécifique à la langue pour de meilleurs résultats.

---

## Récapitulatif & étapes suivantes

Nous avons couvert l’ensemble du pipeline pour **how to batch OCR** :

1. **Initialiser** un moteur OCR texte brut pour l'anglais.  
2. **Configurer** un modèle de vérification orthographique IA et le lier comme post‑processeur.  
3. **Exécuter** l'OCR sur chaque image et laisser l'IA **corriger les erreurs OCR** automatiquement.  
4. **Boucler** sur un répertoire pour **extraire du texte d'images** en masse.  
5. **Libérer les ressources IA** une fois le travail terminé.

À partir d'ici, vous pourriez :

- Acheminer le texte corrigé dans une pipeline NLP en aval (analyse de sentiment, extraction d'entités, etc.).
- Remplacer le post‑processeur de vérification orthographique par un résumeur personnalisé en appelant `ai_processor.set_post_processor(your_custom_func, {})`.
- Paralléliser la boucle du dossier avec `concurrent.futures.ThreadPoolExecutor` si votre GPU peut gérer plusieurs flux.

---

## Réflexions finales

Le traitement OCR par lots n’a pas besoin d’être une corvée. En combinant Aspose OCR avec un modèle IA léger, vous obtenez une **solution tout‑en‑un** qui **extrait du texte d'images**, **applique la vérification orthographique**, **corrige les erreurs OCR**, et **libère proprement les ressources IA**. Testez le script sur un dossier d’essai, ajustez le nombre de couches GPU pour correspondre à votre matériel, et vous disposerez d’un pipeline prêt pour la production en quelques minutes.

Des questions sur l’ajustement du modèle, la gestion des PDF, ou l’intégration dans un service web ? Laissez un commentaire ci‑dessous ou contactez‑moi sur GitHub. Bon codage, et que votre OCR soit toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}