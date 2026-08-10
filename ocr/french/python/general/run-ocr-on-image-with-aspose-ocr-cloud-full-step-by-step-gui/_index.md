---
category: general
date: 2026-03-28
description: Apprenez à exécuter l’OCR sur une image, à télécharger automatiquement
  le modèle Hugging Face, à nettoyer le texte OCR et à configurer le modèle LLM en
  Python en utilisant Aspose OCR Cloud.
draft: false
keywords:
- run OCR on image
- download hugging face model
- clean OCR text
- configure LLM model
language: fr
og_description: Exécutez la reconnaissance optique de caractères sur une image et
  nettoyez le résultat à l'aide d'un modèle Hugging Face téléchargé automatiquement.
  Ce guide montre comment configurer le modèle LLM en Python.
og_title: Exécuter l'OCR sur une image – Tutoriel complet Aspose OCR Cloud
tags:
- OCR
- Python
- LLM
- HuggingFace
title: Exécuter la reconnaissance optique de caractères sur une image avec Aspose OCR Cloud
  – Guide complet étape par étape
url: /fr/python/general/run-ocr-on-image-with-aspose-ocr-cloud-full-step-by-step-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter l'OCR sur une image – Tutoriel complet Aspose OCR Cloud

Vous avez déjà eu besoin d'exécuter l'OCR sur des fichiers image mais la sortie brute ressemblait à un méli-mélo ? D'après mon expérience, le principal point douloureux n'est pas la reconnaissance elle‑-même — c'est le nettoyage. Heureusement, Aspose OCR Cloud vous permet d'attacher un post‑processeur LLM qui peut *nettoyer le texte OCR* automatiquement. Dans ce tutoriel, nous passerons en revue tout ce dont vous avez besoin : du **téléchargement d'un modèle Hugging Face** à la configuration du LLM, en passant par l'exécution du moteur OCR, jusqu'à la finition du résultat.

À la fin de ce guide, vous disposerez d'un script prêt à l'emploi qui :

1. Récupère un modèle compact Qwen 2.5 depuis Hugging Face (téléchargé automatiquement pour vous).  
2. Configure le modèle pour exécuter une partie du réseau sur le GPU et le reste sur le CPU.  
3. Exécute le moteur OCR sur une image de note manuscrite.  
4. Utilise le LLM pour nettoyer le texte reconnu, vous fournissant une sortie lisible par l'homme.

> **Pré-requis** – Python 3.8+, package `asposeocrcloud`, un GPU avec au moins 4 Go de VRAM (optionnel mais recommandé), et une connexion internet pour le premier téléchargement du modèle.

---

## Ce dont vous aurez besoin

- **Aspose OCR Cloud SDK** – installez via `pip install asposeocrcloud`.  
- **Une image d'exemple** – par ex., `handwritten_note.jpg` placée dans un dossier local.  
- **Support GPU** – si vous disposez d'un GPU compatible CUDA, le script déchargera 30 couches ; sinon il reviendra automatiquement au CPU.  
- **Permission d'écriture** – le script met en cache le modèle dans `YOUR_DIRECTORY` ; assurez‑vous que le dossier existe.

---

## Étape 1 – Configurer le modèle LLM (télécharger le modèle Hugging Face)

La première chose que nous faisons est d'indiquer à Aspose AI où récupérer le modèle. La classe `AsposeAIModelConfig` gère le téléchargement automatique, la quantisation et l'allocation des couches GPU.

```python
import asposeocrcloud as ocr
from asposeocrcloud.ai import AsposeAI, AsposeAIModelConfig

# ----------------------------------------------------------------------
# Step 1: Model configuration – this will download the model if it’s missing
# ----------------------------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",                           # Enables auto‑download
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF", # Repo on Hugging Face
    hugging_face_quantization="int8",                     # Small footprint, fast inference
    gpu_layers=30,                                        # 30 layers on GPU, rest on CPU
    directory_model_path=r"YOUR_DIRECTORY"               # Cache folder (optional)
)
```

**Pourquoi c'est important** – Quantiser en `int8` réduit drastiquement l'utilisation de mémoire (≈ 4 Go vs 12 Go). Diviser le modèle entre GPU et CPU vous permet d'exécuter un LLM de 3 milliards de paramètres même sur un RTX 3060 modeste. Si vous n'avez pas de GPU, définissez `gpu_layers=0` et le SDK gardera tout sur le CPU.

> **Astuce :** La première exécution téléchargera ~ 1,5 Go, donc accordez‑lui quelques minutes et une connexion stable.

---

## Étape 2 – Initialiser le moteur IA avec la configuration du modèle

Nous lançons maintenant le moteur Aspose AI et lui fournissons la configuration que nous venons de créer.

```python
# ----------------------------------------------------------------------
# Step 2: Initialise the AI engine – pulls the model if needed
# ----------------------------------------------------------------------
ocr_ai = AsposeAI()
ocr_ai.initialize(model_config)  # This call blocks until the model is ready
```

**Ce qui se passe en coulisses ?** Le SDK vérifie `directory_model_path` pour un modèle existant. S'il trouve une version correspondante, il la charge instantanément ; sinon il télécharge le fichier GGUF depuis Hugging Face, le décompresse et prépare le pipeline d'inférence.

---

## Étape 3 – Créer le moteur OCR et attacher le post‑processeur IA

Le moteur OCR effectue le travail lourd de reconnaissance des caractères. En attachant `ocr_ai.run_postprocessor`, nous activons automatiquement le **nettoyage du texte OCR** après la reconnaissance.

```python
# ----------------------------------------------------------------------
# Step 3: Build the OCR engine and bind the LLM post‑processor
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=None)
```

**Pourquoi utiliser un post‑processeur ?** L'OCR brut inclut souvent des sauts de ligne aux mauvais endroits, une ponctuation mal détectée ou des symboles parasites. Le LLM peut réécrire la sortie en phrases correctes, corriger l'orthographe et même deviner les mots manquants — transformant essentiellement un dump brut en texte poli.

---

## Étape 4 – Exécuter l'OCR sur un fichier image

Avec tout connecté, il est temps de fournir une image au moteur.

```python
# ----------------------------------------------------------------------
# Step 4: Load the image and run OCR
# ----------------------------------------------------------------------
input_image = ocr.Image.load(r"YOUR_DIRECTORY/handwritten_note.jpg")
raw_result = ocr_engine.recognize(input_image)   # Returns an OcrResult object
```

**Cas particulier :** Si l'image est grande (> 5 MP), vous pourriez vouloir la redimensionner d'abord pour accélérer le traitement. Le SDK accepte un objet Pillow `Image`, vous pouvez donc pré‑traiter avec `PIL.Image.thumbnail()` si nécessaire.

---

## Étape 5 – Laisser l'IA nettoyer le texte reconnu et afficher les deux versions

Enfin nous invoquons le post‑processeur que nous avons attaché précédemment. Cette étape montre le contraste entre le *avant* et le *après* nettoyage.

```python
# ----------------------------------------------------------------------
# Step 5: Clean the OCR output using the LLM and display both results
# ----------------------------------------------------------------------
cleaned_result = ocr_engine.run_postprocessor(raw_result)

print("=== Before AI ===")
print(raw_result.text)

print("\n=== After AI ===")
print(cleaned_result.text)
```

### Sortie attendue

```
=== Before AI ===
Th1s 1s a h@ndwr1tt3n n0te.  It c0nta1ns m1st@k3s, l1n3 br3aks, & sp3c!@l ch@r@ct3rs.

=== After AI ===
This is a handwritten note. It contains mistakes, line breaks, and special characters.
```

Remarquez comment le LLM a :

- Corrigé les erreurs de reconnaissance OCR courantes (`Th1s` → `This`).  
- Supprimé les symboles parasites (`&` → `and`).  
- Normalisé les sauts de ligne en phrases correctes.

---

## 🎨 Vue d'ensemble visuelle (Flux de travail Exécuter OCR sur image)

![Flux d'exécution OCR sur image](run_ocr_on_image_workflow.png "Diagramme montrant le pipeline d'exécution OCR sur image, du téléchargement du modèle à la sortie nettoyée")

Le diagramme ci‑dessus résume le pipeline complet : **télécharger le modèle Hugging Face → configurer le LLM → initialiser l'IA → moteur OCR → post‑processeur IA → nettoyer le texte OCR**.

---

## Questions fréquentes & Astuces pro

### Et si je n'ai pas de GPU ?

Définissez `gpu_layers=0` dans le `AsposeAIModelConfig`. Le modèle s'exécutera entièrement sur le CPU, ce qui est plus lent mais toujours fonctionnel. Vous pouvez également passer à un modèle plus petit (par ex., `Qwen/Qwen2.5-1.5B‑Instruct‑GGUF`) pour garder un temps d'inférence raisonnable.

### Comment changer le modèle plus tard ?

Il suffit de mettre à jour `hugging_face_repo_id` et de relancer `ocr_ai.initialize(model_config)`. Le SDK détectera le changement de version, téléchargera le nouveau modèle et remplacera les fichiers en cache.

### Puis‑je personnaliser le prompt du post‑processeur ?

Oui. Passez un dictionnaire à `custom_settings` avec une clé `prompt_template`. Par exemple :

```python
custom_prompt = {
    "prompt_template": "Correct the following OCR text and keep line breaks:\n{ocr_text}"
}
ocr_engine.set_post_processor(ocr_ai.run_postprocessor, custom_settings=custom_prompt)
```

### Dois‑je enregistrer le texte nettoyé dans un fichier ?

Absolument. Après le nettoyage, vous pouvez écrire le résultat dans un fichier `.txt` ou `.json` pour un traitement en aval :

```python
with open("cleaned_note.txt", "w", encoding="utf-8") as f:
    f.write(cleaned_result.text)
```

---

## Conclusion

Nous venons de vous montrer comment **exécuter l'OCR sur des images** avec Aspose OCR Cloud, **télécharger automatiquement un modèle Hugging Face**, configurer avec expertise les paramètres du **modèle LLM**, et enfin **nettoyer le texte OCR** à l'aide d'un puissant post‑processeur LLM. L'ensemble du processus tient dans un seul script Python facile à exécuter et fonctionne à la fois sur des machines avec GPU et uniquement CPU.

Si vous êtes à l'aise avec ce pipeline, envisagez d'expérimenter avec :

- **Différents LLMs** – essayez `meta-llama/Meta-Llama-3-8B‑Instruct‑GGUF` pour une fenêtre de contexte plus large.  
- **Traitement par lots** – parcourez un dossier d'images et agrégerez les résultats nettoyés dans un CSV.  
- **Prompts personnalisés** – adaptez l'IA à votre domaine (documents juridiques, notes médicales, etc.).

N'hésitez pas à ajuster la valeur `gpu_layers`, changer de modèle, ou brancher votre propre prompt. Le ciel est la limite, et le code que vous avez maintenant est votre rampe de lancement.

Bon codage, et que vos sorties OCR restent toujours propres ! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}