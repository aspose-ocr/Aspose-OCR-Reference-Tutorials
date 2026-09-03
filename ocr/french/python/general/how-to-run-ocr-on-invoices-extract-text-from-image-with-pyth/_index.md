---
category: general
date: 2026-01-07
description: Comment exécuter l’OCR et extraire le texte d’une image pour le traitement
  des factures. Apprenez à améliorer la précision de l’OCR, charger l’image pour l’OCR
  et traiter efficacement l’OCR des factures.
draft: false
keywords:
- how to run ocr
- extract text from image
- improve ocr accuracy
- load image for ocr
- process invoice ocr
language: fr
og_description: Comment exécuter l'OCR sur les factures étape par étape. Extraire
  le texte d’une image, améliorer la précision de l’OCR et charger l’image pour l’OCR
  à l’aide d’Aspose AI.
og_title: Comment exécuter l’OCR sur les factures – Guide complet Python
tags:
- OCR
- Python
- Image Processing
title: Comment faire de l’OCR sur les factures – Extraire le texte d’une image avec
  Python
url: /fr/python/general/how-to-run-ocr-on-invoices-extract-text-from-image-with-pyth/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR sur les factures – Extraire du texte d'une image avec Python

Vous vous êtes déjà demandé **comment exécuter l'OCR** sur une facture numérisée et obtenir un texte propre et consultable ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsque la sortie brute de l'OCR est truffée de fautes d'orthographe, de sauts de ligne cassés et de ponctuation manquante. Dans ce tutoriel, nous parcourrons une solution full‑stack qui non seulement **extrait du texte d'une image**, mais aussi **améliore la précision de l'OCR** grâce à un post‑traitement avec un modèle AI d'Aspose.

Vous verrez comment **charger une image pour l'OCR**, exécuter le moteur intégré, puis appliquer une vérification orthographique légère qui rend le résultat prêt pour les analyses en aval. À la fin, vous disposerez d'un script réutilisable que vous pourrez intégrer à n'importe quel pipeline de traitement de factures.

> **Ce dont vous aurez besoin**  
> * Python 3.9 ou plus récent  
> * paquets `aspose-ocr` et `aspose-ai` (installés via `pip`)  
> * Une image de facture (PNG, JPEG ou TIFF) – nous utiliserons `sample_invoice.png` comme exemple  
> * Optionnel : un GPU avec au moins 4 Go de VRAM pour une inférence de modèle plus rapide (le script fonctionne également sur CPU)

---

## Étape 1 : Installer les paquets requis et préparer l'environnement

Avant de pouvoir **charger une image pour l'OCR**, nous devons nous assurer que les bibliothèques nécessaires sont disponibles. Le moteur OCR d'Aspose est fourni avec un simple wrapper Python, tandis que le post‑processeur AI repose sur un modèle quantifié Hugging Face.

```bash
# Install Aspose OCR and AI packages
pip install aspose-ocr aspose-ai
```

> **Astuce :** Si vous prévoyez d'utiliser l'accélération GPU, installez `torch` avec le support CUDA (`pip install torch --extra-index-url https://download.pytorch.org/whl/cu121`).

---

## Étape 2 : Charger l'image de la facture

Le chargement de l'image est simple, mais il vaut la peine de mentionner pourquoi nous définissons explicitement le chemin comme une chaîne brute (`r"..."`). Cela évite les erreurs d'échappement accidentelles sur les chemins Windows.

```python
import aspose.ocr as ocr

# Define the path to your invoice image
image_path = r"YOUR_DIRECTORY/sample_invoice.png"

# Initialize the OCR engine and attach the image
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)
```

*Pourquoi c'est important :* L'utilisation de `ocr.Image.load` garantit que l'image est pré‑traitée (binarisation, redressement) selon les paramètres optimaux d'Aspose, ce qui **améliore déjà la précision de l'OCR** avant toute magie AI.

---

## Étape 3 : Exécuter le moteur OCR intégré

Nous allons maintenant réellement **exécuter l'OCR** et capturer le texte brut. Cette étape montre la sortie typique que vous obtiendriez d'une exécution OCR standard—souvent un désordre de sauts de ligne et de fautes d'orthographe occasionnelles.

```python
# Perform OCR
engine.recognize()
raw_text = engine.recognized_text

print("Raw OCR output:")
print(raw_text)
```

**Sortie brute typique** (truncée pour plus de concision) :

```
INVOICE NO: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Vous remarquerez peut‑être que « Invoice » apparaît comme « Invo1ce » ou que la ponctuation manque. C'est là que le post‑processeur AI intervient.

---

## Étape 4 : Configurer le modèle AI d'Aspose

Le modèle AI que nous allons utiliser est **Qwen2.5‑3B‑Instruct‑GGUF**, un LLM léger ajusté par instruction qui fonctionne confortablement sur un GPU de milieu de gamme. La configuration ci‑dessous indique à Aspose où récupérer le modèle, combien de couches garder sur le GPU, et la taille du contexte pour gérer de longs paragraphes.

```python
from aspose.ai import AsposeAI, AsposeAIModelConfig

model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,               # 30 layers on GPU, remainder on CPU
    context_size=4096            # larger context for long paragraphs
)

ai = AsposeAI()
ai.initialize(model_config)   # you could also pass `model_config` to the constructor
```

> **Pourquoi cette configuration ?**  
> * `gpu_layers=30` équilibre vitesse et mémoire—la plupart de l’inférence se fait sur le GPU, tandis que les couches restantes restent sur le CPU pour éviter les erreurs OOM.  
> * `context_size=4096` garantit que le modèle peut voir la facture entière d’un coup, évitant ainsi la troncature de champs importants.

---

## Étape 5 : Créer un post‑processeur de vérification orthographique simple

Nous allons encapsuler l’appel AI dans une petite fonction appelée `simple_spell_check`. L’invite est délibérément concise : « Correct spelling and punctuation: » suivi du texte OCR brut Le modèle renvoie une version nettoyée.

```python
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

# Register the post‑processor with the AI instance
ai.set_post_processor(simple_spell_check, None)
```

**Comment ça fonctionne :** `ai.run_prompt` envoie l’invite au LLM chargé localement, qui renvoie ensuite une chaîne unique avec l’orthographe corrigée, la ponctuation appropriée, et une mise en page des sauts de ligne plus naturelle.

---

## Étape 6 : Appliquer le post‑processeur au texte OCR brut

Maintenant, la magie opère. Nous injectons la sortie OCR brute dans notre post‑processeur et affichons le résultat amélioré.

```python
enhanced_text = ai.run_postprocessor(raw_text)

print("\nAI‑enhanced OCR output:")
print(enhanced_text)
```

**Exemple de sortie améliorée** :

```
Invoice No: 2023‑00123
Date: 06/15/2023
Bill To:
Acme Corp
123 Main St
...
Total Due: $1,250.00
```

Remarquez l’orthographe corrigée de « Invoice », l’utilisation correcte des deux‑points, et des sauts de ligne cohérents—exactement ce dont vous avez besoin pour une analyse fiable en aval.

---

## Étape 7 : Nettoyer les ressources

Le moteur OCR et le modèle AI allouent tous deux des ressources natives. Il est recommandé de les libérer une fois terminé, surtout dans les services de longue durée.

```python
ai.free_resources()
engine.dispose()
```

---

## Script complet – Prêt à coller

Ci‑dessous se trouve le script complet et exécutable qui relie toutes les étapes. Enregistrez‑le sous le nom `invoice_ocr.py`, remplacez `YOUR_DIRECTORY` par le dossier contenant votre image de facture, et exécutez-le avec `python invoice_ocr.py`.

```python
# invoice_ocr.py
import aspose.ocr as ocr
from aspose.ai import AsposeAI, AsposeAIModelConfig

# -------------------------------------------------
# Step 1: Load the image to be processed
# -------------------------------------------------
image_path = r"YOUR_DIRECTORY/sample_invoice.png"
engine = ocr.OcrEngine()
engine.image = ocr.Image.load(image_path)

# -------------------------------------------------
# Step 2: Run the built‑in OCR engine and obtain raw text
# -------------------------------------------------
engine.recognize()
raw_text = engine.recognized_text
print("Raw OCR output:")
print(raw_text)

# -------------------------------------------------
# Step 3: Configure the Aspose AI model for post‑processing
# -------------------------------------------------
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="q4_k_m",
    gpu_layers=30,
    context_size=4096
)

ai = AsposeAI()
ai.initialize(model_config)   # alternatively, pass config to the constructor

# -------------------------------------------------
# Step 4: Define a simple spell‑check post‑processor
# -------------------------------------------------
def simple_spell_check(text):
    prompt = f"Correct spelling and punctuation:\n{text}"
    return ai.run_prompt(prompt)

ai.set_post_processor(simple_spell_check, None)

# -------------------------------------------------
# Step 5: Apply the post‑processor to the raw OCR text
# -------------------------------------------------
enhanced_text = ai.run_postprocessor(raw_text)
print("\nAI‑enhanced OCR output:")
print(enhanced_text)

# -------------------------------------------------
# Step 6: Release resources
# -------------------------------------------------
ai.free_resources()
engine.dispose()
```

Exécutez le script et vous verrez à la fois le dump OCR brut bruyant et la version polie, **précision OCR améliorée**, côte à côte.

---

## Questions fréquentes & cas limites

### 1. Et si mon image de facture est un PDF multi‑pages ?

Aspose OCR peut charger directement les pages PDF. Remplacez la ligne de chargement d'image par :

```python
engine.image = ocr.Image.load("invoice.pdf", page_index=0)  # 0‑based page number
```

Itérez `page_index` pour traiter chaque page séquentiellement.

### 2. Mon GPU manque de mémoire—puis‑je n’utiliser que le CPU ?

Absolument. Réglez `gpu_layers=0` dans le `AsposeAIModelConfig`. Le modèle s’exécutera entièrement sur le CPU, ce qui est plus lent mais sûr pour le matériel bas de gamme.

### 3. Comment gérer les factures non‑anglais ?

Remplacez l’ID du dépôt du modèle par un modèle spécifique à la langue, par ex. `"mistralai/Mistral-7B-Instruct-v0.2"` pour le support multilingue. Le reste du pipeline reste inchangé.

### 4. Puis‑je chaîner plusieurs post‑processeurs (par ex., formater les dates, extraire les totaux) ?

Oui. `ai.set_post_processor` accepte une liste d’appels. Par exemple :

```python
def extract_totals(text):
    # simple regex to pull monetary values
    import re
    totals = re.findall(r"\$\d+(?:,\d{3})*(?:\.\d{2})?", text)
    return "\n".join(totals)

ai.set_post_processor([simple_spell_check, extract_totals], None)
```

La sortie sera d’abord vérifiée orthographiquement, puis les totaux seront extraits.

---

## Conseils de performance & bonnes pratiques

| Astuce | Pourquoi cela aide |
|-----|---------------|
| **Regrouper plusieurs factures** – chargez‑les dans une liste et traitez‑les dans une boucle. | Réduit la surcharge de l’interpréteur Python et maintient le modèle AI chargé en mémoire. |
| **Mettre en cache le modèle** – évitez d’appeler `initialize` de façon répétée dans un service web. | Le chargement du modèle peut prendre ~30 secondes ; le cache permet des réponses instantanées. |
| **Redimensionner les grandes images** à une largeur de 1500 px avant l’OCR. | Des images plus petites accélèrent à la fois l’OCR et l’inférence AI sans sacrifier la précision. |
| **Définir `allow_auto_download="false"` en production** – livrez le modèle avec votre déploiement. | Garantit des temps de démarrage déterministes et évite les problèmes de réseau. |

---

## Conclusion

Nous avons couvert **comment exécuter l'OCR** sur les factures, du chargement de l'image au polissage du résultat avec une vérification orthographique pilotée par l'IA. En suivant ces étapes, vous pouvez de façon fiable **extraire du texte d'une image**, **améliorer la précision de l'OCR**, et traiter sans effort **l'OCR de factures** dans n'importe quel flux de travail basé sur Python.

Testez-le avec différents formats de factures—peut‑être un reçu manuscrit ou un contrat numérisé. Le même pipeline s’adapte avec peu de modifications, prouvant qu’une combinaison OCR + IA bien structurée est un outil polyvalent pour tout projet d’automatisation de documents.

Si vous avez trouvé ce guide utile, pensez à le partager avec vos collègues ou à mettre une étoile sur le dépôt qui héberge les paquets Aspose

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}