---
category: general
date: 2026-07-05
description: Comment répertorier les modèles avec Aspose AI, activer le téléchargement
  automatique et télécharger un modèle Hugging Face en Python. Suivez ce tutoriel
  étape par étape pour configurer le cache et commencer à utiliser Aspose AI dès aujourd'hui.
draft: false
keywords:
- how to list models
- enable auto download
- download hugging face model
- how to use aspose
- how to set cache
language: fr
og_description: Comment répertorier les modèles avec Aspose AI, activer le téléchargement
  automatique et télécharger un modèle Hugging Face. Apprenez à configurer le cache
  et à utiliser Aspose AI en quelques minutes.
og_title: Comment lister les modèles avec Aspose AI – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  headline: How to list models with Aspose AI – Complete Guide
  type: TechArticle
- description: How to list models with Aspose AI, enable auto download, and download
    Hugging Face model in Python. Follow this step‑by‑step tutorial to set up cache
    and start using Aspose AI today.
  name: How to list models with Aspose AI – Complete Guide
  steps:
  - name: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
    text: Create an `AsposeAI` object and a `AsposeAIModelConfig`.
  - name: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
    text: Set `allow_auto_download = "true"` and point `directory_model_path` to a
      folder you control.
  - name: Initialise the AI, then call `list_local()` to see exactly what’s cached.
    text: Initialise the AI, then call `list_local()` to see exactly what’s cached.
  - name: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
    text: Use the listed model name for inference, and you’re ready to build real‑world
      applications.
  type: HowTo
tags:
- Aspose
- Python
- LLM
- Model Management
title: Comment répertorier les modèles avec Aspose AI – Guide complet
url: /fr/python/general/how-to-list-models-with-aspose-ai-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment lister les modèles avec Aspose AI – Guide complet

Comment lister les modèles avec Aspose AI est une question qui apparaît dès que vous commencez à expérimenter avec de grands modèles de langage en Python. Dans ce tutoriel, nous parcourrons l'activation du **téléchargement automatique**, la configuration d'un cache local, et le téléchargement d'un modèle directement depuis Hugging Face—pour que vous puissiez démarrer sans chercher manuellement les fichiers.

Si vous vous êtes déjà demandé *« comment utiliser Aspose pour une IA pilotée par OCR ? »* ou *« quelle est la façon la plus simple de configurer le cache pour les fichiers de modèle ? »* vous êtes au bon endroit. À la fin, vous disposerez d'un script entièrement fonctionnel qui liste chaque modèle stocké localement, télécharge automatiquement ceux qui manquent, et vous indique exactement où les fichiers résident sur le disque.

---

## Ce dont vous avez besoin

- Python 3.9 ou plus récent (la bibliothèque utilise des annotations de type qui nécessitent un interpréteur récent)
- `pip` accès pour installer le package **Aspose OCR** (`aocr`).  
  ```bash
  pip install aocr
  ```
- Une connexion Internet pour le premier téléchargement depuis Hugging Face.
- Un dossier où vous souhaitez conserver le cache des modèles (par ex., `./model_cache`).

C’est tout—pas de conteneurs Docker supplémentaires, pas d’environnements virtuels lourds au-delà d’une installation Python propre.

---

## ## Comment lister les modèles avec Aspose AI

Le cœur de ce guide est la capacité à **lister les modèles** que Aspose AI a mis en cache localement. Une fois le cache configuré, la bibliothèque peut énumérer tout ce qu’elle connaît, facilitant le débogage et le contrôle de version.

```python
import aocr

# 1️⃣ Create an Aspose AI instance
ai = aocr.AsposeAI()

# 2️⃣ Configure the model cache and auto‑download behavior
cfg = aocr.AsposeAIModelConfig()
cfg.allow_auto_download = "true"                     # ← enable auto download
cfg.directory_model_path = r"./model_cache"          # ← how to set cache
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

# 3️⃣ Initialise the AI with the config we just built
ai.initialize(cfg)

# 4️⃣ List the models that are already cached locally
print("🗂️ Models cached at:", ai.get_local_path())
print("📦 Available models:", ai.list_local())
```

**Pourquoi cela fonctionne :**  
- `AsposeAI()` crée le point d’entrée de haut niveau qui communique avec le moteur d’inférence sous‑jacent.  
- `AsposeAIModelConfig()` contient tous les paramètres réglables ; définir `allow_auto_download` à `"true"` indique à la bibliothèque de récupérer automatiquement les fichiers manquants depuis le dépôt que vous spécifiez.  
- `directory_model_path` est le *répertoire de cache*—l’endroit où résident tous les binaires téléchargés.  
- `initialize()` applique la configuration, effectuant le premier téléchargement si le cache est vide.  
- Enfin, `list_local()` parcourt le dossier de cache et renvoie une liste Python d’identifiants de modèles, que nous affichons.

### Sortie attendue (première exécution)

```
🗂️ Models cached at: ./model_cache
📦 Available models: ['Qwen2.5-3B-Instruct-GGUF']
```

Si vous exécutez à nouveau le script, la bibliothèque sautera le téléchargement et listera simplement le modèle déjà présent, prouvant que **la configuration du cache** est réellement bénéfique pour les exécutions suivantes.

---

## ## Activer le téléchargement automatique pour les modèles manquants

Souvent, vous travaillerez avec plusieurs modèles à travers des projets. Récupérer manuellement chaque modèle depuis Hugging Face peut être fastidieux. En activant le téléchargement automatique, Aspose AI se charge du travail lourd.

```python
cfg.allow_auto_download = "true"
```

> **Astuce :** Gardez `allow_auto_download` réglé sur `"true"` **uniquement** dans les environnements de développement ou d’intégration continue. En production, vous pourriez vouloir verrouiller le cache afin d’éviter un trafic réseau inattendu.

Si vous décidez plus tard de le désactiver, il suffit de régler le drapeau sur `"false"` avant d’appeler à nouveau `initialize()`.

---

## ## Télécharger le modèle Hugging Face à la volée

```python
cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"
```

indique à Aspose AI quel dépôt distant récupérer. La bibliothèque prend en charge tout modèle public sur Hugging Face qui fournit un fichier GGUF. Vous voulez un modèle différent ? Changez l’ID du dépôt :

```python
cfg.hugging_face_repo_id = "mistralai/Mistral-7B-Instruct-v0.2"
```

Lorsque vous exécutez le script, Aspose AI vérifie le cache :

- **Si le modèle existe**, il le charge instantanément.  
- **S’il n’existe pas**, le drapeau de téléchargement automatique déclenche un téléchargement, stocke le fichier sous `directory_model_path`, puis l’enregistre pour une utilisation immédiate.

Cette approche élimine le processus en deux étapes « télécharger‑puis‑exécuter » que de nombreux tutoriels vous obligent à suivre.

---

## ## Comment utiliser Aspose AI après que le modèle soit listé

Lister les modèles n’est que la moitié de l’histoire. Une fois que vous savez qu’un modèle est présent, vous pouvez lancer l’inférence :

```python
# Assume the model we just listed is the one we want to use
model_name = ai.list_local()[0]

# Create a simple prompt
prompt = "Explain the difference between supervised and unsupervised learning."

# Run inference
response = ai.run_inference(model_name, prompt)

print("🤖 Model response:", response)
```

**Pourquoi c’est important :**  
- `run_inference()` abstrait la tokenisation, le batching et la gestion du GPU.  
- En passant le *nom du modèle* obtenu via `list_local()`, vous garantissez que l’appel d’inférence correspond exactement au fichier sur le disque.

---

## ## Comment définir l’emplacement du cache pour plusieurs projets

Si vous gérez plusieurs projets, vous pouvez vouloir que chacun possède son propre dossier de cache. Le champ `directory_model_path` n’est qu’une simple chaîne, vous pouvez donc le construire dynamiquement :

```python
import os

project_name = "sentiment_analysis"
cache_root   = "./model_cache"
cfg.directory_model_path = os.path.join(cache_root, project_name)
```

Chaque projet obtient maintenant un sous‑dossier isolé (`./model_cache/sentiment_analysis`), évitant les conflits de version et simplifiant le nettoyage.

---

## ## Pièges courants et comment les éviter

| Symptom | Cause probable | Solution |
|---------|----------------|----------|
| **`PermissionError` lors de l'accès au cache** | Dossier de cache appartenant à un autre utilisateur (courant sur les serveurs partagés) | Créez le dossier manuellement avec les permissions appropriées : `mkdir -p ./model_cache && chmod 775 ./model_cache` |
| **Le modèle n’apparaît jamais dans `list_local()`** | `allow_auto_download` réglé sur `"false"` et le modèle n’est pas encore en cache | Activez temporairement le drapeau, exécutez une fois, puis désactivez-le si désiré |
| **Version de modèle inattendue** | Deux dépôts différents partagent le même nom mais des fichiers différents | Fixez l’ID exact du dépôt (incluant le tag/commit) ou verrouillez le cache en désactivant le téléchargement automatique après le premier tirage réussi |
| **Erreurs de mémoire insuffisante** | Fichiers GGUF volumineux sur une machine sans RAM/VRAM suffisante | Utilisez un modèle plus petit (par ex., `Qwen2.5-1.5B`) ou définissez `cfg.device = "cpu"` pour forcer l’inférence sur le CPU |

---

## ## Script complet à copier‑coller

Voici l’exemple complet, prêt à l’exécution, qui intègre tous les concepts ci‑dessus. Enregistrez‑le sous le nom `list_models_demo.py` et exécutez‑le avec `python list_models_demo.py`.

```python
# list_models_demo.py
import os
import aocr

def main():
    # ------------------------------------------------------------------
    # 1️⃣ Create the Aspose AI instance
    # ------------------------------------------------------------------
    ai = aocr.AsposeAI()

    # ------------------------------------------------------------------
    # 2️⃣ Build configuration: enable auto download, set cache path,
    #    and point at a Hugging Face repo
    # ------------------------------------------------------------------
    cfg = aocr.AsposeAIModelConfig()
    cfg.allow_auto_download = "true"                               # enable auto download
    cfg.directory_model_path = os.path.abspath("./model_cache")   # how to set cache
    cfg.hugging_face_repo_id = "Qwen/Qwen2.5-3B-Instruct-GGUF"

    # ------------------------------------------------------------------
    # 3️⃣ Initialise the AI with the configuration
    # ------------------------------------------------------------------
    ai.initialize(cfg)

    # ------------------------------------------------------------------
    # 4️⃣ Verify cache location and list all locally available models
    # ------------------------------------------------------------------
    print("🗂️ Models cached at:", ai.get_local_path())
    print("📦 Available models:", ai.list_local())

    # ------------------------------------------------------------------
    # 5️⃣ (Optional) Run a quick inference using the first listed model
    # ------------------------------------------------------------------
    if ai.list_local():
        model_name = ai.list_local()[0]
        prompt = "Give a short summary of the Python GIL."
        response = ai.run_inference(model_name, prompt)
        print("\n🤖 Model response:", response)

if __name__ == "__main__":
    main()
```

**L’exécuter** produira une sortie similaire à l’exemple précédent, suivie d’une réponse concise du modèle. N’hésitez pas à remplacer l’invite par ce que vous voulez—c’est la façon la plus rapide de vérifier que le modèle est réellement utilisable après que vous ayez **listé les modèles**.

---

## ## Résumé

Nous avons couvert tout ce dont vous avez besoin pour **lister les modèles** avec Aspose AI, de l’activation du **téléchargement automatique** à la configuration d’un **cache** persistant et au téléchargement à la demande d’un **modèle Hugging Face**. Les points clés :

1. Créez un objet `AsposeAI` et un `AsposeAIModelConfig`.  
2. Définissez `allow_auto_download = "true"` et pointez `directory_model_path` vers un dossier que vous contrôlez.  
3. Initialisez l’IA, puis appelez `list_local()` pour voir exactement ce qui est en cache.  
4. Utilisez le nom du modèle listé pour l’inférence, et vous êtes prêt à créer des applications réelles.

---

## Et après ?

- **Expérimentez avec différents modèles** – remplacez `cfg.hugging_face_repo_id` par un autre dépôt et observez comment la liste change.  
- **Affinez le cache**

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment traiter par lots des images OCR avec List dans Aspose.OCR pour .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Comment définir la licence Aspose OCR et la vérifier en Java](/ocr/english/java/ocr-basics/set-license/)
- [Comment extraire du texte d’une image avec Aspose.OCR pour .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}