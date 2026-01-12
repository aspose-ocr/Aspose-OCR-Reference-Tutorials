---
category: general
date: 2026-01-12
description: Comment exécuter l'OCR et extraire le texte des images de factures en
  utilisant Aspose OCR et un modèle léger Hugging Face. Apprenez à télécharger le
  modèle, corriger les erreurs d'OCR et effectuer l'OCR sur l'image.
draft: false
keywords:
- how to run OCR
- extract text from invoice
- download hugging face model
- correct OCR errors
- perform OCR on image
language: fr
og_description: Comment exécuter l'OCR sur des images de factures, extraire le texte
  et corriger les erreurs avec un LLM Hugging Face. Suivez ce guide complet pour des
  résultats impeccables.
og_title: Comment effectuer l'OCR sur des images de factures – Tutoriel complet
tags:
- OCR
- Python
- AI post‑processing
- Hugging Face
title: Comment faire de l’OCR sur des images de factures – Guide complet étape par
  étape
url: /fr/python/general/how-to-run-ocr-on-invoice-images-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR sur des images de factures – Guide complet étape par étape

Vous vous êtes déjà demandé **comment exécuter l'OCR** sur une facture numérisée et obtenir du texte propre et interrogeable sans passer des heures à le nettoyer ? Vous n'êtes pas le seul. Dans de nombreux projets réels, la sortie brute de l'OCR est truffée d'erreurs de reconnaissance — pensez à « O » pour « 0 », « l » pour « 1 », ou même des mots entiers déformés. La bonne nouvelle ? En quelques lignes de Python, vous pouvez non seulement **perform OCR on image** files mais aussi corriger automatiquement les **correct OCR errors** à l'aide d'un modèle léger de Hugging Face.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : du chargement d'une image de facture, à l'extraction du texte brut, en passant par le téléchargement d'un modèle quantifié, jusqu'à l'affinage du résultat pour obtenir une transcription parfaite prête pour le traitement en aval. À la fin, vous serez capable d'**extract text from invoice** des PDF ou PNG en un seul script réutilisable.

## Prérequis et configuration

Avant de commencer, assurez-vous d'avoir :

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Python 3.9+ | Syntaxe moderne et annotations de type |
| `aspose-ocr` package | Fournit le `ocr.OcrEngine` utilisé dans l'exemple |
| `aspose-ai` package | Fournit le post‑processor `AsposeAI` |
| Access to a GPU (optional) | Accélère les couches LLM ; sinon le CPU fonctionne bien |
| Internet connection (first run) | Nécessaire pour **download Hugging Face model** automatiquement |

Vous pouvez installer les bibliothèques requises avec :

```bash
pip install aspose-ocr aspose-ai
```

> **Conseil pro :** Si vous prévoyez d'exécuter le LLM sur GPU, installez `torch` avec le support CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu118`).

Maintenant que l'environnement est prêt, passons au code.

---

## Étape 1 – Initialiser le moteur OCR et charger votre image de facture

La première chose à faire est de créer une instance du moteur OCR d'Aspose et de le pointer vers le fichier que vous souhaitez traiter. Cette étape est la base de **how to run OCR** sur n'importe quelle image.

```python
import ocr  # Aspose OCR package

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Load the invoice you want to read
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")
```

> **Pourquoi c'est important :** `load_image` accepte les PNG, JPEG, TIFF, et même les pages PDF, vous permettant de **perform OCR on image** quels que soient le format.

---

## Étape 2 – Exécuter l'OCR de base pour capturer le texte brut

Une fois l'image chargée, le moteur peut produire une transcription brute. Cette sortie est souvent bruyante, c'est pourquoi nous exécuterons plus tard une étape de correction.

```python
# Perform the OCR scan
raw_result = ocr_engine.recognize()

# Show what the engine saw
print("Raw OCR:", raw_result.text)
```

Un exemple de sortie brute peut ressembler à :

```
Raw OCR: Inv0ice No: 12345
Date: 2023/07/15
Total Am0unt: $1,200.00
```

Remarquez les zéros (`0`) où le chiffre « O » devrait être ? C'est exactement le type d'erreur que nous corrigerons plus tard.

---

## Étape 3 – Configurer le post‑processor IA avec un LLM léger

Nous introduisons maintenant un **download Hugging Face model** suffisamment petit pour fonctionner sur du matériel modeste mais assez puissant pour comprendre le langage des factures. L'exemple utilise le modèle Qwen 2.5 3B‑Instruct GGUF, quantifié en `int8` pour une empreinte mémoire minime.

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Define model configuration
model_config = AsposeAIModelConfig(
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",          # reduces size dramatically
    gpu_layers=20,                             # use GPU for the first 20 layers if available
    allow_auto_download="true"                # pulls the model on first run
)

# Initialise the AI processor and attach the post‑processor
ai_processor = AsposeAI()
ai_processor.set_post_processor("llm_correction", model_config)
```

> **Pourquoi ce modèle ?** La quantisation `int8` réduit le fichier à ~1,2 Go, le rendant utilisable sur la plupart des ordinateurs portables. Les couches GPU accélèrent l'inférence, mais le code revient proprement au CPU lorsqu'aucun GPU n'est détecté.

---

## Étape 4 – Exécuter la correction basée sur le LLM sur le résultat OCR brut

Avec le modèle prêt, nous injectons le texte brut dans le post‑processor. Le LLM réécrira la transcription, corrigeant les défauts OCR courants et normalisant les nombres.

```python
# Apply AI correction
corrected_result = ai_processor.run_postprocessor(raw_result)

# Display the cleaned output
print("AI‑corrected:", corrected_result.text)
```

Sortie nettoyée attendue :

```
AI‑corrected: Invoice No: 12345
Date: 2023/07/15
Total Amount: $1,200.00
```

Vous pouvez voir que les zéros sont redevenus la lettre « O », et « Am0unt » est maintenant « Amount ». C'est le cœur de **correct OCR errors** automatiquement.

---

## Étape 5 – Libérer les ressources et nettoyer

Les grands modèles de langage peuvent occuper la mémoire GPU, il est donc recommandé de libérer les ressources une fois terminé.

```python
# Free the model and any GPU buffers
ai_processor.free_resources()
```

Si vous prévoyez de traiter de nombreuses factures en lot, vous pouvez garder le modèle chargé et ne le libérer qu'à la toute fin du script.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici un script unique que vous pouvez placer dans un fichier `.py` et exécuter :

```python
# ------------------------------------------------------------
# How to Run OCR on Invoice Images – End‑to‑End Example
# ------------------------------------------------------------
import ocr
from aspose_ai import AsposeAI, AsposeAIModelConfig

def main():
    # 1️⃣ Initialise OCR engine
    ocr_engine = ocr.OcrEngine()
    ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

    # 2️⃣ Capture raw OCR text
    raw_result = ocr_engine.recognize()
    print("Raw OCR:", raw_result.text)

    # 3️⃣ Configure lightweight LLM from Hugging Face
    model_cfg = AsposeAIModelConfig(
        hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
        hugging_face_quantization="int8",
        gpu_layers=20,
        allow_auto_download="true"
    )
    ai = AsposeAI()
    ai.set_post_processor("llm_correction", model_cfg)

    # 4️⃣ Run AI correction
    corrected = ai.run_postprocessor(raw_result)
    print("AI‑corrected:", corrected.text)

    # 5️⃣ Clean up
    ai.free_resources()

if __name__ == "__main__":
    main()
```

L'exécution du script devrait produire une sortie similaire au bloc « AI‑corrected » présenté précédemment. N'hésitez pas à remplacer le chemin de l'image par toute autre facture ou reçu afin d'**extract text from invoice** en masse.

---

## Questions fréquentes et cas particuliers

### Et si je n'ai pas de GPU ?

Le paramètre `gpu_layers` est optionnel. Réglez-le à `0` ou omettez-le, et le modèle s'exécutera entièrement sur le CPU. Attendez-vous à une inférence plus lente — environ 2–3 secondes par page sur un ordinateur portable moderne.

### Mes factures sont des PDF multi‑pages. Comment les gérer ?

Convertissez chaque page en une image distincte (par ex., avec `pdf2image`) et bouclez sur les pages avec le même script. Le moteur OCR peut traiter chaque image indépendamment, et le LLM corrigera chaque bloc de texte.

```python
from pdf2image import convert_from_path

pages = convert_from_path("invoice.pdf", dpi=300)
for i, page_img in enumerate(pages):
    ocr_engine.load_image(page_img)
    # …run steps 2‑4…
```

### Le téléchargement du modèle échoue derrière un pare-feu ?

Téléchargez le modèle manuellement depuis le hub de modèles Hugging Face, décompressez-le dans un dossier local, et pointez `hugging_face_repo_id` vers le chemin local :

```python
model_cfg = AsposeAIModelConfig(
    hugging_face_repo_id="/local/path/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=20,
    allow_auto_download="false"
)
```

### Quelle est la précision de la correction ?

Pour les factures typiques en anglais, le LLM corrige >95 % des erreurs OCR courantes. Les notes manuscrites complexes peuvent encore nécessiter une révision manuelle.

---

## Astuces et conseils pour la mise en production

- **Batch processing :** Encapsulez les étapes 2‑4 dans une fonction et fournissez une liste de chemins de fichiers. Réutilisez la même instance `AsposeAI` pour éviter de recharger le modèle.
- **Logging :** Remplacez `print` par le module `logging` de Python afin de capturer les sorties brutes et corrigées pour les pistes d’audit.
- **Error handling :** Entourez l’appel OCR d’un bloc `try/except`. Si une image échoue, consignez le nom de fichier et continuez.
- **Performance tuning :** Expérimentez avec `gpu_layers`. Plus de couches sur le GPU accélèrent l’inférence mais augmentent l’utilisation de la VRAM.

---

## Conclusion

Nous avons couvert **how to run OCR** sur des images de factures du début à la fin, en vous montrant comment **perform OCR on image**, **download Hugging Face model**, et **correct OCR errors** automatiquement. Le script complet illustre un flux de travail pratique que vous pouvez intégrer à n'importe quel pipeline d'automatisation basé sur Python.

Prochaines étapes ? Essayez d'étendre le pipeline pour **extract key fields** (numéro de facture, date, total) en utilisant des expressions régulières sur le texte corrigé, ou injectez la sortie nettoyée dans une base de données pour des enregistrements interrogeables. Vous pouvez également expérimenter d'autres LLM légers de Hugging Face si vous avez besoin d'une langue différente ou de connaissances spécifiques à un domaine.

Bon codage, et que vos résultats OCR soient toujours d'une clarté cristalline !

![comment exécuter l'OCR sur une image de facture](ocr_invoice_example.png "comment exécuter l'OCR sur une facture")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}