---
category: general
date: 2026-06-22
description: Reconnaître le texte à partir de fichiers PNG en utilisant Aspose OCR
  en Python. Apprenez la reconnaissance OCR par lots d'images et configurez les couches
  GPU pour un traitement rapide.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: fr
og_description: Reconnaître le texte à partir de fichiers PNG avec Aspose OCR en Python.
  Ce guide montre comment effectuer une reconnaissance OCR par lots d'images et configurer
  les couches GPU pour accélérer le traitement.
og_title: Reconnaître du texte à partir d’un PNG – Tutoriel Aspose OCR étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: Reconnaître le texte à partir de PNG – Guide complet avec Aspose OCR et IA
url: /fr/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir de png – Tutoriel complet Aspose OCR & AI

Vous avez déjà eu besoin de **reconnaître du texte à partir de png** mais vous vous êtes enlisé dans les détails d'installation ? Vous n'êtes pas seul. Que vous numérisiez des reçus, scanniez des formulaires ou transformiez des captures d'écran en texte recherchable, maîtriser le **batch OCR images** en Python peut vous faire gagner des heures.

Dans ce guide, nous parcourrons un exemple prêt à l’emploi qui non seulement **reconnaît du texte à partir de png**, mais montre aussi comment **set GPU layers** pour obtenir un gain de vitesse notable. À la fin, vous disposerez d’un script autonome, d’une explication claire de chaque étape, et de plusieurs astuces pratiques à copier‑coller dans vos propres projets.

## Ce que couvre ce tutoriel

- Installation des packages Python Aspose OCR et Aspose AI  
- Configuration d’un modèle IA avec téléchargement automatique depuis Hugging Face  
- Création d’un petit post‑processueur qui corrige les fautes d’OCR les plus courantes  
- Exécution d’une boucle **batch OCR images** sur l’ensemble d’un dossier de PNG  
- Utilisation de l’option **set GPU layers** pour exploiter votre carte graphique  
- Nettoyage sécurisé des ressources après le traitement  

Aucun service externe, aucune magie cachée — juste du code Python pur que vous pouvez placer dans un fichier `.py` et exécuter.

![Diagram of recognize text from png workflow](workflow.png){alt="diagramme du flux de reconnaissance de texte à partir de png"}

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|--------------------------|
| Python 3.8+ | Les wheels Aspose AI ciblent les interpréteurs récents |
| Un GPU compatible CUDA (optionnel) | Nécessaire si vous voulez **set GPU layers** pour l’accélération |
| Accès Internet lors du premier lancement | Le modèle sera téléchargé automatiquement depuis Hugging Face |
| `pip` installé | Pour récupérer les packages Aspose |

Si vous avez déjà tout cela, super — vous êtes prêt à démarrer. Sinon, les étapes d’installation ci‑dessous vous guideront pour combler les manques.

---

## Étape 1 : Installer les packages Aspose OCR et Aspose AI

Tout d’abord, récupérez les bibliothèques depuis PyPI. La commande ci‑dessous télécharge à la fois le moteur OCR et l’assistant IA en une seule fois.

```bash
pip install aspose-ocr aspose-ai
```

*Astuce :* utilisez un environnement virtuel (`python -m venv .venv`) afin que les packages restent isolés de votre installation Python globale.

---

## Étape 2 : Créer et configurer l’instance Aspose AI

Le composant IA alimente le mode « intelligent » du moteur OCR. Nous le pointons vers le modèle `Qwen/Qwen2.5-3B-Instruct-GGUF`, demandons le téléchargement automatique s’il manque, et **set GPU layers** à 30 (vous pourrez ajuster cela plus tard).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Pourquoi c’est important :**  
- `allow_auto_download` élimine l’étape manuelle de récupération d’un modèle d’environ 2 Go.  
- `gpu_layers=30` indique au transformeur sous‑jacent d’exécuter les 30 premières couches sur le GPU, réduisant considérablement le temps d’inférence lorsqu’un GPU compatible est présent.  
- L’utilisation de la quantification `int8` maintient une faible consommation de mémoire sans sacrifier trop de précision.

---

## Étape 3 : Définir un post‑processueur simple pour nettoyer les erreurs d’OCR

L’OCR n’est pas parfait—surtout sur des PNG à basse résolution. Une correction rapide consiste à remplacer les caractères fréquemment mal lus. La fonction suivante échange le “0” avec le “o” et le “1” avec le “l”, un motif que l’on voit souvent sur les factures scannées.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

Nous l’attacherons à l’instance IA à l’étape suivante afin que chaque résultat de reconnaissance le traverse automatiquement.

---

## Étape 4 : Lier le post‑processueur et le moteur OCR

Nous connectons maintenant tout : le moteur OCR, le modèle IA et le post‑processueur.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Que se passe‑t‑il en coulisses ?**  
Le `OcrEngine` délègue le travail lourd au modèle IA que vous avez configuré. Après que le modèle renvoie le texte brut, Aspose appelle `fix_common_errors` pour nettoyer la sortie avant que vous ne la voyiez.

---

## Étape 5 : Batch OCR Images – Traiter chaque PNG d’un dossier

Voici le cœur du tutoriel : une boucle qui parcourt un répertoire, charge chaque `.png`, exécute l’OCR et affiche le résultat nettoyé. Ce schéma est la manière canonique d’effectuer un **batch OCR images** de façon efficace.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Sortie attendue** (exemple pour un reçu) :

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Si vous avez des dizaines ou des centaines de fichiers, cette boucle les traitera séquentiellement, en réutilisant la même instance IA pour éviter le surcoût du rechargement du modèle.

---

## Étape 6 : Nettoyage – Libérer les ressources et disposer du moteur

Lorsque vous avez terminé, il est recommandé de libérer la mémoire GPU et les autres ressources natives. Aspose fournit des méthodes explicites à cet effet.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Ignorer cette étape peut laisser de la mémoire GPU allouée, ce qui peut entraîner des erreurs de type out‑of‑memory lors du prochain lancement du script.

---

## Bonus : Ajuster les GPU Layers selon le matériel

La valeur `gpu_layers` que vous avez définie plus haut constitue un bon compromis pour de nombreux GPU modernes, mais vous pourriez devoir l’ajuster :

| Mémoire GPU (Go) | gpu_layers recommandé |
|------------------|-----------------------|
| 4 Go ou moins    | 10‑15                 |
| 6‑8 Go           | 20‑30                 |
| 12 Go+           | 35‑45 (ou plus)       |

Si vous dépassez la mémoire de votre GPU, le moteur repassera automatiquement sur le CPU pour les couches restantes, donc vous ne crasherez pas—juste plus lent. N’hésitez pas à expérimenter et à surveiller l’utilisation avec `nvidia‑smi`.

---

## Pièges courants & comment les éviter

1. **Échec du téléchargement du modèle** – Assurez‑vous que votre environnement peut atteindre `https://huggingface.co`. Un proxy d’entreprise peut nécessiter une configuration (`https_proxy` env var).  
2. **GPU non détecté** – Vérifiez que la bibliothèque `torch` (installée en dépendance) voit le GPU : `import torch; print(torch.cuda.is_available())`. Si cela renvoie `False`, installez la wheel PyTorch compatible CUDA.  
3. **Chemin d’image incorrect** – `Path.glob("*.png")` est sensible à la casse sous Linux. Utilisez `*.PNG` ou `*.png` en conséquence, ou ajoutez `pathlib.Path(...).rglob("*.[pP][nN][gG]")` pour plus de sécurité.  
4. **Post‑processueur sur‑corrige** – Le remplacement simple peut transformer des caractères “0” légitimes en “o”. Testez sur un échantillon représentatif et ajustez la logique si besoin.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Exécutez‑le avec :

```bash
python recognize_text_from_png_batch.py
```

Vous devriez voir chaque nom de fichier PNG suivi du texte extrait, exactement comme démontré précédemment.

---

## Conclusion

Nous venons de parcourir un workflow complet, prêt pour la production, afin de **reconnaître du texte à partir de png** avec Aspose OCR et Aspose AI en Python. En regroupant les étapes dans un script clair, vous pouvez facilement **batch OCR images**, et grâce à `set gpu layers`


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}