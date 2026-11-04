---
category: general
date: 2026-02-09
description: Comment exécuter l’OCR avec Aspose AI et un modèle Hugging Face – apprenez
  à télécharger le modèle Hugging Face, corriger les erreurs d’OCR et libérer la mémoire
  GPU.
draft: false
keywords:
- how to run OCR
- download hugging face model
- free gpu memory
- how to free gpu
- correct OCR errors
language: fr
og_description: Comment exécuter l’OCR avec Aspose AI est expliqué dans le premier
  paragraphe – découvrez comment télécharger le modèle Hugging Face, corriger les
  erreurs d’OCR et libérer la mémoire GPU.
og_title: Comment exécuter l'OCR avec Aspose AI – Guide complet
tags:
- OCR
- Aspose
- AI
- HuggingFace
title: Comment exécuter l’OCR avec Aspose AI – Guide étape par étape
url: /fr/python/general/how-to-run-ocr-with-aspose-ai-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment exécuter l'OCR avec Aspose AI – Guide complet

Ever wondered **how to run OCR** on a scanned invoice and get perfectly clean numbers without spending hours fixing typos? You're not alone. In many real‑world projects the raw text that comes out of a classic OCR engine still contains stray characters, broken currency symbols, or garbled digits—especially when the source image is noisy.  

The good news is that you can hook an LLM up to Aspose OCR, download a Hugging Face model on‑the‑fly, and let the AI polish the output for you. In this tutorial we’ll walk through the whole pipeline, from pulling the model (yes, we’ll show you how to **download hugging face model** automatically) to freeing up GPU resources when you’re done. By the end you’ll have a reproducible script that **corrects OCR errors**, runs fast on a modest GPU, and cleans up after itself so you don’t waste memory.

## Ce que vous apprendrez

- Configure Aspose AI to fetch a **Qwen2.5‑3B‑Instruct‑GGUF** model from Hugging Face.
- Run the standard Aspose OCR engine on an image file.
- Use a custom LLM prompt that keeps numbers and currency symbols intact.
- Release GPU memory with the built‑in **free gpu memory** routine.
- Tweak the workflow for edge cases like multi‑page PDFs or low‑end GPUs.

> **Prerequisites** – Python 3.9+, `aspose-ocr` package, internet access for the first model download, and a GPU with at least 4 GB VRAM (optional but recommended). If you don’t have a GPU, the script will automatically fall back to CPU for the remaining layers.

---

## Comment exécuter l'OCR et améliorer les résultats

Voici le script Python complet, prêt à être exécuté. Enregistrez‑le sous le nom `ocr_with_ai.py` et remplacez les chemins d’accès factices par vos propres fichiers.

```python
# ocr_with_ai.py
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Configure the AI engine (download hugging face model)
# -------------------------------------------------
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",                     # auto‑download if missing
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # tiny memory footprint
    gpu_layers=20,                                  # 20 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY/Models"  # optional custom folder
)
ai = AsposeAI(ai_config)

# -------------------------------------------------
# Step 2 – Load an image and run the classic OCR engine
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()   # returns plain‑text string

# -------------------------------------------------
# Step 3 – Register a custom LLM prompt (correct OCR errors)
# -------------------------------------------------
def financial_prompt():
    # Bias the model toward financial terminology
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# -------------------------------------------------
# Step 4 – Let the LLM polish the output
# -------------------------------------------------
corrected_text = ai.run_postprocessor(raw_text)

print("Original :", raw_text)
print("Enhanced :", corrected_text)

# -------------------------------------------------
# Step 5 – Release resources (free gpu memory)
# -------------------------------------------------
ai.free_resources()
```

> **Pro tip** : le paramètre `gpu_layers` vous permet de décider combien de couches de transformeur restent sur le GPU. Si vous rencontrez des erreurs de dépassement de mémoire, réduisez ce nombre et le reste s’exécutera sur le CPU – vous pourrez toujours **free gpu memory** plus tard avec `ai.free_resources()`.

### Résultat attendu

L’exécution du script sur une facture d’exemple produit quelque chose comme :

```
Original : Invoic # 12345 \n Total: $1O0.00\n Date: 2023-07-15
Enhanced : Invoice # 12345
Total: $100.00
Date: 2023-07-15
```

Remarquez comment l’IA a corrigé le « O » dans `$1O0.00` en un zéro correct tout en préservant le signe dollar. C’est l’essence de **correct OCR errors** pour les documents financiers.

---

## Télécharger le modèle Hugging Face – Que se passe-t-il en coulisses ?

Lorsque vous définissez `allow_auto_download="true"`, le wrapper Aspose AI vérifie le `directory_model_path`. Si les fichiers du modèle ne sont pas présents, il contacte le Hugging Face Hub, récupère la version **int8‑quantized** de `Qwen2.5‑3B‑Instruct‑GGUF`, et la stocke localement. Ce téléchargement unique fait généralement moins de 2 GB, ce qui le rend réalisable même sur des SSD modestes.

> **Why int8?** La quantisation en 8 bits réduit la consommation de mémoire de façon spectaculaire — crucial lorsque vous souhaitez également **free gpu memory** après le traitement. Le compromis est une légère perte de précision, mais pour le post‑traitement du texte OCR l’impact est négligeable.

Si vous préférez héberger le modèle vous‑même, déposez simplement les fichiers `.gguf` dans `YOUR_DIRECTORY/Models` et Aspose les utilisera sans se reconnecter à Internet.

---

## Comment libérer le GPU – Bonnes pratiques

Les ressources GPU sont une commodité partagée sur de nombreuses stations de travail. Laisser des tenseurs vivants après la fin de votre script peut provoquer des erreurs « CUDA out of memory » pour les tâches suivantes. L’appel `ai.free_resources()` effectue trois actions :

1. **Libère le transformeur sous‑jacent** – tous les poids résidant sur le GPU sont libérés.
2. **Vide le cache PyTorch** – `torch.cuda.empty_cache()` est invoqué en interne.
3. **Supprime les fichiers temporaires** – tout cache sur disque créé pendant le téléchargement est supprimé.

Vous pouvez également invoquer manuellement `torch.cuda.empty_cache()` si vous combinez Aspose AI avec d’autres charges de travail PyTorch, mais la méthode intégrée est généralement suffisante.

---

## Guide étape par étape (H2 avec mots‑clés secondaires)

### Télécharger automatiquement le modèle Hugging Face

Le constructeur `AsposeAIModelConfig` masque la complexité de l’interaction avec l’API Hugging Face. Assurez‑vous simplement d’avoir un accès Internet la première fois que vous exécutez le script. Par la suite, le modèle réside dans `YOUR_DIRECTORY/Models`, et les exécutions suivantes démarrent instantanément.

### Libérer la mémoire GPU après l’inférence

Si vous exécutez cela au sein d’un service de longue durée (par ex., une API Flask), appelez `ai.free_resources()` après chaque requête. Cela empêche les fuites de mémoire et garantit que la requête suivante peut réutiliser le même GPU sans accroc.

### Corriger les erreurs OCR avec une invite personnalisée

Notre fonction `financial_prompt` renvoie un dictionnaire avec une seule clé `prompt`. Vous pouvez l’adapter à n’importe quel domaine :

```python
def medical_prompt():
    return {"prompt": "Fix OCR mistakes, keep dosage numbers and units unchanged"}
```

Remplacez le nom de la fonction dans `ai.set_post_processor(...)` et vous obtenez un pipeline **correct OCR errors** pour les dossiers médicaux.

### Comment exécuter l'OCR sur des PDF multi‑pages

Aspose OCR peut gérer les PDF nativement :

```python
ocr_engine.load_document(r"YOUR_DIRECTORY/multi_page.pdf")
raw_text = ocr_engine.recognize()  # concatenates pages automatically
```

Après avoir obtenu la chaîne brute, le même post‑processeur LLM nettoiera le texte de chaque page. Aucun code supplémentaire n’est nécessaire.

### Quand vous n’avez pas de GPU – Comment libérer le GPU (même sans)

Même sur des machines uniquement CPU, appeler `ai.free_resources()` est sans danger. Cela vide simplement les caches internes, ce qui peut encore libérer de la RAM. Ainsi, le conseil **how to free gpu** s’applique universellement : nettoyez toujours après vous.

---

## Pièges courants et comment nous les avons résolus

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Out‑of‑Memory on GPU** | `gpu_layers` trop élevé pour votre carte | Réduisez `gpu_layers` à 10 ou 5, laissez le reste s’exécuter sur le CPU |
| **Model never downloads** | Le pare‑feu d’entreprise bloque le HTTPS vers huggingface.co | Téléchargez le modèle manuellement sur un autre réseau, puis pointez `directory_model_path` vers le dossier local |
| **Numbers get corrupted** | Invite pas assez explicite sur la conservation des chiffres | Ajoutez « preserve all numeric values and currency symbols exactly as they appear » à l’invite |
| **`free_resources` raises an exception** | Utilisation d’une version plus ancienne d’Aspose OCR | Mettez à jour vers le dernier paquet `aspose-ocr` (pip install --upgrade aspose-ocr) |

---

## Récapitulatif complet de l’exemple

Voici à nouveau le script, cette fois avec des commentaires en ligne qui expliquent chaque ligne pour référence future :

```python
import aspose.ocr as aocr
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# 1️⃣ Configure AI – will auto‑download the model if needed
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,                     # adjust based on your GPU size
    directory_model_path=r"YOUR_DIRECTORY/Models"
)
ai = AsposeAI(ai_config)               # initialise the engine

# 2️⃣ Run classic OCR on an image (or PDF)
ocr_engine = aocr.OcrEngine()
ocr_engine.load_image(r"YOUR_DIRECTORY/invoice.png")
raw_text = ocr_engine.recognize()      # plain‑text result

# 3️⃣ Define a prompt that tells the LLM to keep numbers intact
def financial_prompt():
    return {"prompt": "Correct OCR errors, keep numbers and currency symbols intact"}

ai.set_post_processor("llm_correction", financial_prompt)

# 4️⃣ Let the LLM clean the text
corrected_text = ai.run_postprocessor(raw_text)

# 5️⃣ Show before/after
print("Original :", raw_text)
print("Enhanced :", corrected_text)

# 6️⃣ Clean up – this frees GPU memory for the next run
ai.free_resources()
```

---

## Conclusion

Nous avons couvert **how to run OCR** avec Aspose, téléchargé un modèle Hugging Face à la demande, créé une invite qui **corrects OCR errors**, et enfin **free gpu memory** afin que votre station de travail reste réactive. L’ensemble du flux de travail tient dans un seul fichier Python autonome — aucun script externe, aucune gestion manuelle du modèle, et aucune allocation GPU persistante.

Next steps? Try swapping the `financial_prompt` for a

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}