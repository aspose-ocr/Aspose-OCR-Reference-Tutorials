---
category: general
date: 2026-03-18
description: Le tutoriel de base OCR en Python montre comment convertir un TIFF en
  texte, charger l'OCR d'image, définir les couches GPU et corriger les zéros initiaux
  avec Aspose AI.
draft: false
keywords:
- basic ocr python
- convert tiff to text
- load image ocr
- set gpu layers
- fix leading zeroes
language: fr
og_description: Le tutoriel de base OCR en Python vous guide à travers la conversion
  de fichiers TIFF en texte propre, le chargement d’images, la configuration des couches
  GPU et la correction des zéros initiaux.
og_title: OCR basique Python – convertir le TIFF en texte
tags:
- OCR
- Python
- AI
- Aspose
title: OCR basique en Python – convertir TIFF en texte
url: /fr/python/general/basic-ocr-python-convert-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# basic ocr python – Convertir un TIFF en texte avec post‑traitement IA

Vous cherchez un moyen de faire du **basic ocr python** sur vos documents numérisés ? Dans ce guide, nous allons parcourir la conversion d’un fichier TIFF en texte propre et consultable en utilisant Aspose OCR et un post‑processeur IA.  

Si vous avez déjà eu du mal à **convertir TIFF en texte** parce que la sortie brute est truffée de fautes de frappe ou de symboles étranges, vous n’êtes pas seul. Nous vous montrerons également comment **charger l’image OCR**, ajuster le moteur pour **définir les couches GPU**, et même **corriger les zéros initiaux** qui apparaissent souvent dans les numéros de facture.

## Ce que vous allez apprendre

- Comment initialiser le moteur Aspose OCR pour les documents imprimés.  
- Les étapes exactes pour **charger l’image OCR** depuis un fichier TIFF et obtenir le texte brut.  
- Configurer un modèle IA, le télécharger automatiquement, et **définir les couches GPU** pour une inférence plus rapide.  
- Ajouter la vérification orthographique intégrée plus une fonction personnalisée qui **corrige les zéros initiaux**.  
- Nettoyer le résultat OCR et libérer correctement les ressources.  

À la fin de ce tutoriel, vous disposerez d’un script Python unique et réutilisable qui transforme n’importe quel TIFF en texte poli et consultable—sans copier‑coller manuel.

### Prérequis

- Python 3.8+ installé sur votre machine.  
- Le package `aspose-ocr` (`pip install aspose-ocr`).  
- Optionnel : un GPU avec au moins 4 Go de VRAM si vous souhaitez **définir les couches GPU** ; sinon le code revient automatiquement au CPU.

---

## basic ocr python – charger l’image et reconnaître le texte

La première chose à faire est **charger l’image OCR** afin que le moteur puisse lire les pixels. Le `OcrEngine` d’Aspose gère de nombreux formats, mais ici nous nous concentrons sur le TIFF car c’est le plus courant pour les factures numérisées.

```python
import aspose.ocr as ocr

# Initialise the OCR engine for printed documents
ocr_engine = ocr.OcrEngine()
ocr_engine.set_recognition_mode(ocr.RecognitionMode.PRINTED)   # use HANDWRITTEN for handwritten docs

# Load the TIFF file – replace with your own path
ocr_engine.load_image("YOUR_DIRECTORY/input.tif")
```

> **Astuce :** Si vous traitez des TIFF multi‑pages, Aspose les traite automatiquement page par page, vous n’avez donc pas besoin de boucles supplémentaires.

Une fois l’image chargée, exécutons une passe de reconnaissance basique.

```python
# Perform basic OCR and capture the raw string
raw_text = ocr_engine.recognize()
print("Raw OCR:", raw_text)
```

Vous verrez quelque chose comme :

```
Raw OCR: Inv0ce N0: 0123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Remarquez les *zéros* avant les lettres ? C’est un artefact OCR classique que nous corrigerons plus tard.

![flux de travail basic ocr python](/images/ocr-workflow.png "basic ocr python workflow diagram")

---

## Étape 2 : Convertir le TIFF en texte – préparer le post‑processeur IA

Le texte OCR brut est utile, mais la plupart des pipelines de production ont besoin d’une version polie. Aspose fournit un wrapper `AsposeAI` qui peut télécharger un modèle depuis Hugging Face, l’exécuter sur le GPU et appliquer automatiquement la vérification orthographique.

```python
from aspose.ocr.ai import AsposeAI, AsposeAIModelConfig

# Configure the AI model – we’ll download Qwen2.5‑3B‑Instruct automatically
ai_config = AsposeAIModelConfig(
    allow_auto_download="true",
    directory_model_path="YOUR_DIRECTORY/ocr_ai_models",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=25          # <-- this is where we **set GPU layers**
)

ocr_ai = AsposeAI(ai_config)
```

### Pourquoi le **set GPU layers** est important

Le paramètre `gpu_layers` indique au modèle GGUF sous‑jacent combien de couches de transformeur doivent rester sur le GPU. Plus de couches = inférence plus rapide mais consommation de VRAM plus élevée. Si vous êtes sur un ordinateur portable modeste, réduisez la valeur à `10` ou supprimez‑la complètement pour rester sur le CPU.

---

## Étape 3 : Appliquer la vérification orthographique et **corriger les zéros initiaux**

Aspose AI intègre un correcteur orthographique qui capture la plupart des fautes d’anglais. Cependant, les corrections spécifiques au domaine—comme transformer un `0` initial en `O` pour les codes de facture—nécessitent un post‑processeur personnalisé.

```python
# Enable the built‑in spell‑check
ocr_ai.set_post_processor("spellcheck")

# Custom function to replace a leading zero before three capital letters
def invoice_fix(txt: str) -> str:
    import re
    # Example: "0ABC" -> "OABC"
    return re.sub(r"\b0([A-Z]{3})\b", r"O\1", txt)

# Register the custom fix – it runs after spellcheck
ocr_ai.set_post_processor(invoice_fix)
```

> **Pourquoi cela fonctionne :** L’expression régulière recherche une frontière de mot (`\b`), un zéro, puis exactement trois lettres majuscules. Elle remplace ensuite le zéro par la lettre « O ». Vous pouvez étendre le motif pour d’autres particularités (par ex., `0[0-9]{2}` pour des nombres mal lus).

---

## Étape 4 : Nettoyer le résultat OCR avec le post‑processeur IA

Nous combinons maintenant tout : la chaîne brute du **basic ocr python**, la vérification orthographique, et notre correction de zéro. La méthode `run_postprocessor` renvoie une version nettoyée prête pour les systèmes en aval.

```python
cleaned_text = ocr_ai.run_postprocessor(raw_text)
print("\nCleaned OCR:", cleaned_text)
```

Sortie typique après le post‑processeur :

```
Cleaned OCR: Invoice No: O123AB4
Total Amt: $1,200.00
Date: 2024-07-15
```

Vous voyez que le zéro initial est devenu un `O`, et les fautes courantes sont corrigées. Le texte est maintenant adapté à l’indexation dans un moteur de recherche ou à l’alimentation d’un pipeline d’extraction de données.

---

## Étape 5 : Libérer les ressources IA – garder votre GPU heureux

Si vous exécutez plusieurs tâches OCR dans un service de longue durée, il est recommandé de libérer la mémoire GPU du modèle une fois terminé.

```python
ocr_ai.free_resources()
```

Ignorer cette étape peut entraîner des erreurs « out‑of‑memory » lors d’appels ultérieurs, surtout lorsque **set GPU layers** est réglé sur une valeur élevée.

---

## Variantes optionnelles & cas limites

| Situation | Ce qu’il faut modifier |
|-----------|------------------------|
| **Documents manuscrits** | Utilisez `ocr_engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)` au lieu de `PRINTED`. |
| **Pas de GPU disponible** | Réglez `gpu_layers=0` ou omettez l’argument ; le modèle s’exécutera sur le CPU (plus lent mais sûr). |
| **Langue différente** | Changez l’ID du dépôt Hugging Face vers un modèle spécifique à la langue, par ex., `microsoft/Florence-2-base`. |
| **Traitement par lots** | Enveloppez les étapes dans une boucle `for file in glob("*.tif"):` et accumulez les résultats dans une liste ou un CSV. |
| **Modèles de zéro plus complexes** | Étendez `invoice_fix` avec des regex supplémentaires, comme `r"\b0+([A-Z]{2,})\b"` pour plusieurs zéros initiaux. |

---

## Conclusion

Nous venons de terminer un pipeline **basic ocr python** qui charge un TIFF, extrait le texte brut, puis le nettoie à l’aide d’un modèle IA tout en **définissant les couches GPU** pour la performance. Le post‑processeur personnalisé montre comment **corriger les zéros initiaux**, un petit détail souvent négligé qui peut casser les analyses en aval.

N’hésitez pas à expérimenter : essayez une quantisation différente (`float16` pour plus de précision), remplacez la vérification orthographique par un dictionnaire spécifique à votre domaine, ou enchaînez plusieurs corrections personnalisées. Le schéma reste le même — charger, reconnaître, configurer l’IA, post‑traiter, et nettoyer.

**Prochaines étapes** que vous pourriez explorer :

- Intégrer la sortie nettoyée à une base de données ou à un index Elasticsearch.  
- Utiliser la même approche pour **convertir TIFF en texte** pour des PDF multilingues.  
- Ajouter une interface UI avec Flask ou FastAPI afin que des utilisateurs non techniques puissent télécharger des fichiers et recevoir instantanément du texte nettoyé.  

Bon codage, et que vos résultats OCR soient toujours nets et sans zéro !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}