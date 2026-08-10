---
category: general
date: 2026-06-22
description: Apprenez à lister les modèles d'IA mis en cache à l'aide du SDK IA en
  Python. Comprend les étapes pour récupérer le répertoire de cache des modèles et
  gérer efficacement les modèles d'IA locaux.
draft: false
keywords:
- list cached ai models
- retrieve model cache directory
- list local ai models
- ai sdk python
- manage ai model cache
language: fr
og_description: Listez les modèles d’IA mis en cache avec Python en utilisant le SDK
  d’IA. Suivez ce tutoriel étape par étape pour récupérer le répertoire du cache des
  modèles et gérer les modèles d’IA locaux.
og_title: Liste des modèles d'IA mis en cache en Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  headline: List Cached AI Models in Python – Complete Guide
  type: TechArticle
- description: Learn how to list cached AI models using the AI SDK in Python. Includes
    steps to retrieve model cache directory and manage local AI models efficiently.
  name: List Cached AI Models in Python – Complete Guide
  steps:
  - name: Import the AI SDK
    text: '```python # Step 1: Import the AI SDK (replace with the actual package
      name if different) import ai ```'
  - name: List All Cached Models
    text: '```python # Step 2: List all models that are cached locally cached_models
      = ai.list_local() print("Cached models:", cached_models) ```'
  - name: Retrieve the Model Cache Directory
    text: '```python # Step 3: Retrieve the directory where the model files are stored
      cache_dir = ai.get_local_path() print("Model cache directory:", cache_dir) ```'
  - name: Empty Cache
    text: If `ai.list_local()` returns an empty list, you might wonder whether the
      SDK is misconfigured. Double‑check the environment variable `AI_CACHE_DIR` (or
      the SDK’s config file) to ensure it points to a writable location.
  - name: Permissions Issues
    text: When accessing `ai.get_local_path()`, a `PermissionError` can surface on
      restrictive systems. The fix is usually to run the script with appropriate user
      rights or to adjust the directory’s ACLs.
  - name: Version Mismatches
    text: 'Sometimes the cache contains an older version of a model while your code
      requests a newer one. The SDK will automatically download the newer version,
      but you can pre‑empt this by inspecting the version tag in the list:'
  - name: Cleaning Up Old Models
    text: 'If you need to free up space, you can delete a specific model folder directly:'
  type: HowTo
- questions:
  - answer: Yes. The SDK abstracts away OS‑specific paths, so `ai.get_local_path()`
      returns a valid string on Linux, macOS, and Windows.
    question: Does this work on all operating systems?
  - answer: The built‑in `list_local()` only reports locally stored artifacts. For
      remote registries you’d use `ai.list_remote()` (if your SDK version provides
      it).
    question: Can I list models from a remote cache?
  - answer: 'Replace the import line with the actual package name, e.g., `import myai
      as ai`. All subsequent calls stay the same because the API contract is consistent
      across implementations. --- ## Conclusion You now have a solid, production‑ready
      method to **list cached AI models** using the **AI SDK Python** '
    question: What if the SDK name isn’t `ai`?
  type: FAQPage
tags:
- python
- ai
- sdk
title: Liste des modèles d'IA mis en cache en Python – Guide complet
url: /fr/python/general/list-cached-ai-models-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Lister les modèles IA mis en cache en Python – Guide complet

Vous êtes-vous déjà demandé comment **lister les modèles IA mis en cache** sur votre poste de travail sans fouiller dans des dossiers obscurs ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent vérifier quels modèles sont déjà stockés localement, surtout lorsqu'ils travaillent avec une bande passante limitée ou des déploiements hors ligne. Dans ce tutoriel, vous verrez une méthode rapide, sans fioritures, pour interroger l’AI SDK, afficher le contenu du cache et découvrir exactement où ces fichiers résident.

Nous aborderons également des sujets connexes comme **récupérer le répertoire du cache de modèles**, gérer les caches vides, et les meilleures pratiques pour **gérer le cache de modèles IA** dans des scripts de production. À la fin, vous disposerez d’un extrait autonome que vous pourrez insérer dans n’importe quel projet Python.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Python 3.8 ou une version plus récente installé.
- L’AI SDK (le paquet `ai`) installé via `pip install ai-sdk` ou le dépôt interne de votre organisation.
- Une connaissance de base de l’exécution de scripts depuis la ligne de commande.

Aucune bibliothèque supplémentaire n’est requise, ce qui rend l’exemple léger et portable.

---

## Lister les modèles IA mis en cache – Vue d’ensemble rapide

La première chose à faire est d’importer le SDK et d’appeler ses fonctions utilitaires. Le SDK expose deux méthodes pratiques :

1. `ai.list_local()` – renvoie une liste Python d’identifiants de modèles déjà mis en cache.
2. `ai.get_local_path()` – renvoie le répertoire absolu où résident ces fichiers de modèle.

Les deux appels sont synchrones et lèvent une `AIError` claire en cas de problème, ce qui simplifie la gestion des erreurs.

> **Pourquoi utiliser ces fonctions ?**  
> Connaître l’ensemble exact des modèles mis en cache vous permet d’éviter des téléchargements inutiles, de déboguer les incompatibilités de version et de nettoyer automatiquement les anciens artefacts. C’est un petit maillon du flux de travail plus large de **AI SDK Python**, mais cela peut vous faire gagner des heures de recherche manuelle dans le système de fichiers.

### Étape 1 : Importer l’AI SDK

```python
# Step 1: Import the AI SDK (replace with the actual package name if different)
import ai
```

*Pourquoi c’est important :* L’import du paquet enregistre les extensions C sous‑jacentes et charge les fichiers de configuration (comme les chemins de cache) depuis votre environnement. Ignorer cette étape déclenchera un `ModuleNotFoundError` dès que vous appellerez une fonction du SDK.

### Étape 2 : Lister tous les modèles mis en cache

```python
# Step 2: List all models that are cached locally
cached_models = ai.list_local()
print("Cached models:", cached_models)
```

**Ce que vous verrez :** Si vous avez trois modèles stockés, la sortie pourrait ressembler à :

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
```

Si le cache est vide, vous obtiendrez une liste vide :

```
Cached models: []
```

> **Astuce :** Enveloppez l’appel dans un bloc try/except si vous suspectez que le SDK n’est pas correctement initialisé.

```python
try:
    cached_models = ai.list_local()
except ai.AIError as e:
    print("Failed to list cached models:", e)
    cached_models = []
```

### Étape 3 : Récupérer le répertoire du cache de modèles

```python
# Step 3: Retrieve the directory where the model files are stored
cache_dir = ai.get_local_path()
print("Model cache directory:", cache_dir)
```

Sortie typique sur un système de type Unix :

```
Model cache directory: /home/you/.cache/ai/models
```

Sur Windows, vous pourriez voir quelque chose comme `C:\Users\you\AppData\Local\ai\models`. Connaître ce chemin est essentiel lorsque vous devez **gérer le cache de modèles IA** manuellement — par exemple pour purger d’anciennes versions ou copier des fichiers vers un lecteur partagé.

---

## Résumé visuel

![Diagram showing how to list cached AI models, retrieve their names, and locate the cache directory](https://example.com/images/list-cached-ai-models.png)

*Texte alternatif :* Diagramme illustrant le processus pour **lister les modèles IA mis en cache** à l’aide de l’AI SDK en Python.

---

## Gestion des cas limites et des pièges courants

### Cache vide

Si `ai.list_local()` renvoie une liste vide, vous pourriez vous demander si le SDK est mal configuré. Vérifiez la variable d’environnement `AI_CACHE_DIR` (ou le fichier de configuration du SDK) pour vous assurer qu’elle pointe vers un emplacement accessible en écriture.

```python
if not cached_models:
    print("No models are cached. Consider downloading a model first.")
```

### Problèmes de permissions

Lors de l’accès à `ai.get_local_path()`, une `PermissionError` peut survenir sur des systèmes restrictifs. La solution consiste généralement à exécuter le script avec les droits d’utilisateur appropriés ou à ajuster les ACL du répertoire.

### Incompatibilités de version

Parfois, le cache contient une version plus ancienne d’un modèle alors que votre code demande une version plus récente. Le SDK téléchargera automatiquement la version plus récente, mais vous pouvez anticiper cela en inspectant le tag de version dans la liste :

```python
for model in cached_models:
    if "v2" not in model:
        print(f"Model {model} may be outdated.")
```

### Nettoyage des anciens modèles

Si vous devez libérer de l’espace, vous pouvez supprimer directement le dossier d’un modèle spécifique :

```python
import shutil, os

def purge_model(model_name):
    path = os.path.join(cache_dir, model_name)
    if os.path.isdir(path):
        shutil.rmtree(path)
        print(f"Purged {model_name} from cache.")
    else:
        print(f"{model_name} not found in cache.")
```

L’appel `purge_model('bert-base-uncased')` supprimera ce modèle et libérera de l’espace disque.

---

## Script complet à copier‑coller

Voici un script prêt à l’emploi qui combine toutes les étapes, ajoute une gestion d’erreur basique et affiche un résumé convivial.

```python
#!/usr/bin/env python3
"""
Complete example: list cached AI models and show cache directory.
"""

import ai
import os
import sys
import shutil

def main():
    try:
        # Retrieve cached model list
        cached = ai.list_local()
        print("Cached models:", cached)

        # Retrieve cache directory
        cache_dir = ai.get_local_path()
        print("Model cache directory:", cache_dir)

        # Summarize status
        if not cached:
            print("\n⚠️  No models are currently cached.")
        else:
            print("\n✅  Found {} model(s) in cache.".format(len(cached)))

        # Optional: ask user if they want to purge an old model
        if cached:
            to_purge = input("\nEnter a model name to purge (or press Enter to skip): ").strip()
            if to_purge:
                purge_path = os.path.join(cache_dir, to_purge)
                if os.path.isdir(purge_path):
                    shutil.rmtree(purge_path)
                    print(f"🗑️  Purged {to_purge} from cache.")
                else:
                    print(f"❌  Model {to_purge} not found in cache.")
    except ai.AIError as err:
        print("AI SDK error:", err, file=sys.stderr)
        sys.exit(1)
    except Exception as exc:
        print("Unexpected error:", exc, file=sys.stderr)
        sys.exit(1)

if __name__ == "__main__":
    main()
```

**Sortie attendue (lorsque le cache est peuplé) :**

```
Cached models: ['gpt-4-mini', 'bert-base-uncased', 'stable-diffusion-v1']
Model cache directory: /home/you/.cache/ai/models

✅  Found 3 model(s) in cache.

Enter a model name to purge (or press Enter to skip):
```

Exécutez le script avec `python list_models.py` et vous connaîtrez instantanément ce qui se trouve sur le disque.

---

## Foire aux questions

**Q : Cela fonctionne-t-il sur tous les systèmes d’exploitation ?**  
R : Oui. Le SDK abstrait les chemins spécifiques aux OS, de sorte que `ai.get_local_path()` renvoie une chaîne valide sous Linux, macOS et Windows.

**Q : Puis‑je lister les modèles depuis un cache distant ?**  
R : La fonction intégrée `list_local()` ne rapporte que les artefacts stockés localement. Pour les registres distants, utilisez `ai.list_remote()` (si votre version du SDK le propose).

**Q : Et si le nom du SDK n’est pas `ai` ?**  
R : Remplacez la ligne d’importation par le nom réel du paquet, par ex. `import myai as ai`. Tous les appels suivants restent identiques car le contrat d’API est cohérent entre les implémentations.

---

## Conclusion

Vous disposez désormais d’une méthode solide, prête pour la production, afin de **lister les modèles IA mis en cache** à l’aide de la bibliothèque **AI SDK Python**, de récupérer le **répertoire du cache de modèles**, et même de nettoyer les anciens fichiers. Cette connaissance vous aide à garder votre environnement propre, à éviter les téléchargements redondants et à déboguer les problèmes de version avec aisance.

Prêt pour l’étape suivante ? Essayez d’étendre le script pour télécharger automatiquement les modèles manquants, ou intégrez‑le dans une pipeline CI qui valide la santé du cache avant chaque build. Explorer les stratégies de **gestion du cache de modèles IA** rendra vos applications alimentées par l’IA plus rapides et plus fiables.

Bon codage, et que vos caches restent légers !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}