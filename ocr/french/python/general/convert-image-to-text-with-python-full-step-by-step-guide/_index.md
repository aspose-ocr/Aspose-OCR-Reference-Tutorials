---
category: general
date: 2026-03-26
description: Convertir une image en texte en utilisant Aspose OCR et nettoyer le texte
  OCR à la manière de Python. Apprenez comment extraire le texte d’une image et le
  post‑traiter dans un seul script.
draft: false
keywords:
- convert image to text
- how to extract image text
- clean ocr text python
- Aspose OCR Python
- AI spell‑checker Python
- post‑process OCR output
language: fr
og_description: Convertissez rapidement une image en texte. Ce guide montre comment
  extraire le texte d’une image et nettoyer le texte OCR à la façon de Python en utilisant
  Aspose OCR et un correcteur orthographique IA.
og_title: Convertir une image en texte avec Python – Tutoriel complet
tags:
- OCR
- Python
- Aspose
- AI
title: Convertir une image en texte avec Python – Guide complet étape par étape
url: /fr/python/general/convert-image-to-text-with-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir une image en texte – Tutoriel complet Python

Vous avez déjà eu besoin de **convertir une image en texte** mais vous obteniez des résultats désordonnés ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsque la sortie OCR est remplie d'erreurs d'orthographe, de symboles parasites ou de sauts de ligne incorrects. La bonne nouvelle ? En quelques lignes de Python et Aspose OCR, vous pouvez extraire du texte clair de n'importe quelle image **et** le nettoyer automatiquement.

Dans ce guide, nous vous montrerons **comment extraire le texte d'une image**, puis exécuter un correcteur orthographique alimenté par l'IA pour produire un contenu soigné et lisible. À la fin, vous disposerez d'un script unique qui passe d'un fichier PNG à un fichier `.txt` propre — sans copier‑coller manuel requis.  

> **Ce que vous apprendrez**  
> * Installer et configurer Aspose OCR.  
> * Reconnaître le texte d'un fichier image.  
> * Initialiser un modèle Aspose AI pour la correction orthographique.  
> * Appliquer le post‑processeur pour nettoyer la sortie OCR.  
> * Enregistrer le résultat final et libérer les ressources.  

Tout cela fonctionne avec le style **clean OCR text python** — ce qui signifie que le code est prêt à être intégré dans n'importe quel projet sans wrappers supplémentaires.

---

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Python 3.9 ou plus récent | Syntaxe moderne & annotations de type |
| `asposeocr` package (`pip install asposeocr`) | Moteur OCR principal |
| Accès Internet (première exécution) | Téléchargement automatique du modèle depuis Hugging Face |
| Une image PNG/JPEG que vous souhaitez lire | Source d'entrée |

Aucun GPU n'est requis, mais si vous en avez un, le modèle IA l'utilisera automatiquement pour une correction orthographique plus rapide.

---

## Étape 1 : Convertir une image en texte avec Aspose OCR

La première chose dont nous avons besoin est un moteur OCR fiable. Aspose OCR est une bibliothèque commerciale, mais elle propose un niveau gratuit généreux pour le développement. Ci-dessous, nous initialisons le moteur, définissons l'anglais comme langue et activons la correction d’inclinaison automatique pour gérer les scans inclinés.

```python
import asposeocr as ocr

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English   # English language pack
ocr_engine.auto_skew = True                  # Auto‑deskew images
```

> **Pourquoi activer `auto_skew` ?**  
> De nombreux documents numérisés ne sont pas parfaitement plats. L'auto‑skew fait pivoter l'image juste assez pour améliorer la reconnaissance des caractères, ce qui réduit à son tour le nombre de mots brouillés que vous devrez nettoyer plus tard.

Nous allons maintenant fournir un fichier image au moteur :

```python
# Recognise text from the input image (replace with your own path)
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR output:")
print(ocr_result.text[:200])  # Show first 200 characters for sanity check
```

La propriété `ocr_result.text` contient la chaîne brute extraite de l'image. À ce stade, vous remarquerez probablement une ponctuation errante, des particularités de sauts de ligne, ou même quelques mots mal orthographiés — exactement le problème que nous voulions résoudre.

![convert image to text workflow](image.png){alt="diagramme du flux de conversion d'image en texte"}

---

## Étape 2 : Configurer le correcteur orthographique IA (Clean OCR Text Python)

Nettoyer la sortie OCR peut être aussi simple qu'un remplacement regex, mais pour un texte réellement lisible, nous utiliserons Aspose AI avec un LLM léger spécialisé dans la correction orthographique. Le modèle est récupéré depuis Hugging Face lors de la première exécution du script, vous n'avez donc rien à télécharger manuellement.

```python
from asposeocr import AsposeAI, AsposeAIModelConfig

# Model configuration – auto‑download enabled
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30                # Use GPU if available, otherwise CPU fallback
)

# Initialise the AI spell‑checker
spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")
```

**Pourquoi ce modèle particulier ?**  
`Qwen2.5‑3B‑Instruct‑GGUF` est un modèle compact de 3 milliards de paramètres, ajusté pour les instructions, qui fonctionne confortablement sur le GPU d'un ordinateur portable (ou même sur le CPU avec quantisation int8). Il est suffisamment rapide pour une correction orthographique ligne par ligne sans exploser la mémoire.

---

## Étape 3 : Appliquer la correction orthographique à la sortie OCR

Avec le texte OCR en main et le modèle IA prêt, nous injectons simplement la chaîne brute dans le post‑processeur. La méthode renvoie une version nettoyée que vous pouvez écrire directement sur le disque.

```python
# Run the spell‑checking post‑processor
corrected_text = spell_checker.run_postprocessor(ocr_result.text)

print("\nCleaned OCR output (first 200 chars):")
print(corrected_text[:200])
```

Améliorations typiques que vous verrez :

* “teh” → “the”  
* “recieve” → “receive”  
* Espaces manquants après la ponctuation – corrigés automatiquement  
* Sauts de ligne étranges transformés en phrases correctes  

Si vous avez besoin de plus de contrôle, vous pouvez passer une invite personnalisée à `run_postprocessor`, mais le préréglage par défaut “spell_check” fonctionne dans la plupart des cas.

---

## Étape 4 : Enregistrer le texte nettoyé dans un fichier

Maintenant que le texte est propre, nous le persistons. L'utilisation de UTF‑8 garantit que tous les caractères spéciaux (par ex., les lettres accentuées) sont conservés.

```python
output_path = "YOUR_DIRECTORY/output_text.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\n✅ Processing complete: input_image.png → {output_path}")
```

Vous pouvez ouvrir le fichier dans n'importe quel éditeur et vous verrez un document lisible par l'homme, prêt pour le traitement en aval — que ce soit pour alimenter un modèle de langage, indexer pour la recherche, ou simplement archiver.

---

## Étape 5 : Libérer les ressources IA (Bonne hygiène)

Aspose AI conserve les poids du modèle en mémoire. Les libérer une fois terminé évite les fuites de mémoire, surtout dans les services de longue durée.

```python
spell_checker.free_resources()
```

C’est tout ! L’ensemble du pipeline — de l'image au texte propre — tient en moins de 30 lignes de Python.

---

## Questions fréquentes & cas particuliers

### Et si l'image n'est pas en anglais ?

Définissez `ocr_engine.language` sur l'énumération appropriée, par ex., `ocr.Language.French`. Le modèle de correcteur orthographique est agnostique à la langue pour l'orthographe de base, mais vous pourriez vouloir un modèle multilingue pour de meilleurs résultats.

### Mon GPU n'a que 20 couches — puis-je toujours utiliser le modèle ?

Absolument. Il suffit de réduire `gpu_layers` à `20` (ou `0` pour un CPU pur). La bibliothèque repassera automatiquement au CPU pour les couches restantes.

### Le téléchargement du modèle échoue derrière un proxy d'entreprise ?

Passez la configuration du proxy via les variables d'environnement (`HTTP_PROXY`, `HTTPS_PROXY`) avant d'exécuter le script. La routine de téléchargement respecte ces paramètres.

### Je n'ai besoin que d'un nettoyage rapide avec regex, pas d'IA ?

Vous pouvez ignorer l'étape IA et exécuter un nettoyage simple :

```python
import re
clean = re.sub(r'\s+', ' ', ocr_result.text).strip()
```

Mais rappelez‑vous, les regex ne corrigeront pas les fautes d'orthographe réelles — l'IA le fait pour vous.

---

## Script complet fonctionnel

Voici le script complet, prêt à être exécuté. Remplacez `YOUR_DIRECTORY` par le dossier contenant votre image et où vous souhaitez que le fichier de sortie soit créé.

```python
import asposeocr as ocr
from asposeocr import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1 – Initialise OCR engine
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
ocr_engine.auto_skew = True

# -------------------------------------------------
# Step 2 – Recognise text from image
# -------------------------------------------------
ocr_result = ocr_engine.recognize_image("YOUR_DIRECTORY/input_image.png")
print("Raw OCR (first 200 chars):")
print(ocr_result.text[:200])

# -------------------------------------------------
# Step 3 – Configure AI spell‑checker
# -------------------------------------------------
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="bartowski/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=30
)

spell_checker = AsposeAI()
spell_checker.initialize(model_cfg)
spell_checker.set_post_processor("spell_check")

# -------------------------------------------------
# Step 4 – Clean the OCR output
# -------------------------------------------------
corrected_text = spell_checker.run_postprocessor(ocr_result.text)
print("\nCleaned OCR (first 200 chars):")
print(corrected_text[:200])

# -------------------------------------------------
# Step 5 – Write to file
# -------------------------------------------------
output_path = "YOUR_DIRECTORY/output_text.txt"
with open(output_path, "w", encoding="utf-8") as out_file:
    out_file.write(corrected_text)

print(f"\nProcessing complete: input_image.png → {output_path}")

# -------------------------------------------------
# Step 6 – Free AI resources
# -------------------------------------------------
spell_checker.free_resources()
```

L'exécution de ce script produira `output_text.txt` contenant la transcription soignée de votre image.

---

## Conclusion

Nous venons de parcourir une méthode pratique pour **convertir une image en texte** à l'aide d'Aspose OCR, puis de **nettoyer le texte OCR** à la façon **clean OCR text python** avec un correcteur orthographique IA. La solution est autonome, ne nécessite qu'un seul fichier Python, et fonctionne sous Windows, macOS ou Linux.

Si vous cherchez la prochaine étape, envisagez :

* **Comment extraire le texte d'une image** à partir de PDF en convertissant d'abord les pages en images.  
* Alimenter le texte nettoyé dans un modèle de résumé pour la génération automatique de rapports.  
* Stocker les résultats dans une base de données vectorielle pour la recherche sémantique.

Essayez, jouez avec les paramètres du modèle, et laissez le pipeline OCR‑vers‑texte devenir un incontournable de votre boîte à outils d'ingestion de données. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}