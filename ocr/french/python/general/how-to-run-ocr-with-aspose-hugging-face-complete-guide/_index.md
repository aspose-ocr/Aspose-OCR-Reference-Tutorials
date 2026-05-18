---
category: general
date: 2026-04-29
description: Apprenez à exécuter la reconnaissance optique de caractères sur vos numérisations,
  à utiliser automatiquement le modèle Hugging Face et à reconnaître le texte des
  numérisations avec Aspose OCR en quelques minutes.
draft: false
keywords:
- how to run OCR
- use hugging face model
- recognize text from scans
- download model automatically
language: fr
og_description: Comment exécuter la reconnaissance optique de caractères sur des numérisations
  avec Aspose OCR, télécharger automatiquement un modèle Hugging Face et obtenir un
  texte propre et ponctué.
og_title: Comment exécuter l'OCR avec Aspose et Hugging Face – Guide complet
tags:
- OCR
- Aspose
- Hugging Face
- Python
title: Comment exécuter l’OCR avec Aspose et Hugging Face – Guide complet
url: /fr/python/general/how-to-run-ocr-with-aspose-hugging-face-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR avec Aspose & Hugging Face – Guide complet

Vous vous êtes déjà demandé **comment exécuter l'OCR** sur une pile de documents numérisés sans passer des heures à ajuster les paramètres ? Vous n'êtes pas seul. Dans de nombreux projets, les développeurs doivent **reconnaître du texte à partir de scans** rapidement, mais ils se heurtent aux téléchargements de modèles et au post‑traitement.  

Bonne nouvelle : ce tutoriel vous montre une solution prête à l’emploi qui **utilise un modèle Hugging Face**, le télécharge automatiquement, et ajoute la ponctuation afin que la sortie ressemble à un texte rédigé par un humain. À la fin, vous disposerez d’un script qui traite chaque image d’un dossier et crée un fichier `.txt` propre à côté de chaque scan.

## Ce dont vous avez besoin

- Python 3.8+ (le code utilise les f‑strings, les versions antérieures ne fonctionneront pas)
- Le package `aspose-ocr` (installez‑le avec `pip install aspose-ocr`)
- Un accès Internet pour le premier téléchargement du modèle  
- Un dossier contenant des scans d’images (`.png`, `.jpg` ou `.tif`)

C’est tout—pas de binaires supplémentaires, pas de manipulation manuelle de modèle. Plongeons‑y.

![exemple d'exécution d'OCR](https://example.com/ocr-demo.png "exemple d'exécution d'OCR")

## Étape 1 : Importer les classes Aspose OCR & configurer l’environnement

Nous commençons par extraire les classes nécessaires de la bibliothèque Aspose OCR. Importer tout d’un coup garde le script propre et facilite la détection des dépendances manquantes.

```python
# Step 1: Import Aspose OCR classes
import os
from aspose.ocr import OcrEngine, AsposeAI, AsposeAIModelConfig
```

*Pourquoi c’est important* : `OcrEngine` effectue le travail lourd, tandis que `AsposeAI` nous permet de brancher un grand modèle de langage pour un post‑traitement plus intelligent. Si vous oubliez l’import, le reste du code ne compilera même pas—ne l’oubliez donc pas.

## Étape 2 : Configurer un modèle Hugging Face compatible GPU  

Nous indiquons maintenant à Aspose où récupérer le modèle et combien de couches doivent s’exécuter sur le GPU. Le drapeau `allow_auto_download="true"` assure le **téléchargement automatique du modèle** pour vous.

```python
# Step 2: Configure a GPU‑aware AI model (replace with your own model folder)
model_config = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    gpu_layers=40,                     # use GPU for faster inference
    directory_model_path=r"YOUR_DIRECTORY/models"
)
```

> **Astuce** : Si vous n’avez pas de GPU, définissez `gpu_layers=0`. Le modèle reviendra alors au CPU, ce qui est plus lent mais fonctionne tout de même.

### Pourquoi choisir un modèle Hugging Face ?

Hugging Face héberge une vaste collection de LLM prêts à l’emploi. En pointant vers `Qwen/Qwen2.5-3B-Instruct-GGUF`, vous obtenez un modèle compact, ajusté pour les instructions, capable d’ajouter de la ponctuation, de corriger les espaces et même de réparer de petites erreurs d’OCR. C’est l’essence même de **l’utilisation d’un modèle Hugging Face** en pratique.

## Étape 3 : Initialiser le moteur IA et activer le post‑traitement de ponctuation  

Le moteur IA ne sert pas uniquement aux chats sophistiqués—ici nous y attachons un *ajouteur de ponctuation* qui nettoie la sortie brute de l’OCR.

```python
# Step 3: Initialise the AI engine and enable punctuation post‑processing
ai_engine = AsposeAI()
ai_engine.set_post_processor("punctuation_adder", {})
```

*Que se passe‑t‑il ?* L’appel `set_post_processor` enregistre un post‑processeur intégré qui s’exécute après la fin du moteur OCR. Il prend la chaîne brute et insère des virgules, points et majuscules aux bons endroits, rendant le texte final beaucoup plus lisible.

## Étape 4 : Créer le moteur OCR et y attacher le moteur IA  

Connecter le moteur IA au moteur OCR nous donne un seul objet capable à la fois de lire les caractères et de peaufiner le résultat.

```python
# Step 4: Create the OCR engine and attach the AI engine
ocr_engine = OcrEngine()
ocr_engine.set_ai_engine(ai_engine)
```

Si vous sautez cette étape, l’OCR fonctionnera toujours, mais vous perdrez l’apport de ponctuation—le résultat ressemblera alors à un flot de mots.

## Étape 5 : Traiter chaque image d’un dossier  

Voici le cœur du tutoriel. Nous parcourons chaque image, exécutons l’OCR, appliquons le post‑processeur, puis écrivons le texte nettoyé dans un fichier `.txt` parallèle.

```python
# Step 5: Run OCR on each image in a folder, post‑process the result, and save the text
scans_folder = r"YOUR_DIRECTORY/scans"
for image_file in os.listdir(scans_folder):
    # Filter only supported image types
    if not image_file.lower().endswith(('.png', '.jpg', '.tif')):
        continue

    image_path = os.path.join(scans_folder, image_file)

    # Recognise text from the image
    ocr_result = ocr_engine.recognize(image_path)

    # Apply the punctuation post‑processor
    ocr_result = ocr_engine.run_postprocessor(ocr_result)

    # Show a brief confidence summary
    print(f"{image_file} – confidence {ocr_result.confidence:.2%}")

    # Save the cleaned text next to the source image
    txt_path = image_path + ".txt"
    with open(txt_path, "w", encoding="utf-8") as txt_file:
        txt_file.write(ocr_result.text)
```

### À quoi s’attendre

L’exécution du script affiche quelque chose comme :

```
invoice_001.png – confidence 96.73%
receipt_2024.tif – confidence 94.12%
```

Chaque ligne indique le score de confiance (un rapide contrôle de santé) et crée `invoice_001.png.txt`, `receipt_2024.tif.txt`, etc., contenant du texte ponctué et lisible par un humain.

### Cas limites & variantes

- **Scans non‑anglais** : changez le `hugging_face_repo_id` vers un modèle multilingue (par ex. `microsoft/Multilingual-LLM-GGUF`).
- **Grandes quantités** : encapsulez la boucle dans un `concurrent.futures.ThreadPoolExecutor` pour un traitement parallèle, mais surveillez les limites de mémoire GPU.
- **Post‑traitement personnalisé** : remplacez `"punctuation_adder"` par votre propre script si vous avez besoin d’un nettoyage spécifique au domaine (par ex. suppression de numéros de facture).

## Étape 6 : Nettoyer les ressources  

Lorsque le travail se termine, libérer les ressources évite les fuites de mémoire, ce qui est crucial si vous exécutez cela dans un service de longue durée.

```python
# Step 6: Release resources
ai_engine.free_resources()
ocr_engine.dispose()
```

Négliger cette étape peut laisser de la mémoire GPU occupée, ce qui compromettrait les exécutions suivantes.

## Récapitulatif : Comment exécuter l'OCR de bout en bout  

En quelques lignes seulement, nous avons montré **comment exécuter l'OCR** sur un dossier de scans, **utiliser un modèle Hugging Face** qui se télécharge automatiquement la première fois, et **reconnaître du texte à partir de scans** avec ponctuation ajoutée automatiquement. Le script complet est prêt à être copié‑collé, à ajuster vos chemins, et à exécuter.

## Prochaines étapes & sujets associés  

- **Post‑traitement par lots** : explorez `ocr_engine.run_batch_postprocessor` pour un traitement en masse encore plus rapide.  
- **Modèles alternatifs** : essayez la famille `openai/whisper` si vous avez besoin de reconnaissance vocale en plus de l’OCR.  
- **Intégration avec des bases de données** : stockez le texte extrait dans SQLite ou Elasticsearch pour des archives consultables.  

N’hésitez pas à expérimenter—changez de modèle, ajustez `gpu_layers`, ou ajoutez votre propre post‑processeur. La flexibilité d’Aspose OCR combinée au hub de modèles de Hugging Face en fait une base polyvalente pour tout projet de numérisation de documents.

---

*Bon codage ! Si vous rencontrez un problème, laissez un commentaire ci‑dessous ou consultez la documentation Aspose OCR pour des options de configuration plus avancées.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}