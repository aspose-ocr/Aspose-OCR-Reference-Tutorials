---
category: general
date: 2026-02-22
description: Apprenez à répertorier les modèles en cache et à afficher rapidement
  le répertoire de cache sur votre machine. Comprend les étapes pour visualiser le
  dossier de cache et gérer le stockage local des modèles d'IA.
draft: false
keywords:
- list cached models
- show cache directory
- how to view cache folder
- AI model cache
- local model storage
language: fr
og_description: Découvrez comment répertorier les modèles en cache, afficher le répertoire
  du cache et visualiser le dossier de cache en quelques étapes simples. Exemple complet
  en Python inclus.
og_title: Lister les modèles en cache – guide rapide pour afficher le répertoire de
  cache
tags:
- AI
- caching
- Python
- development
title: Lister les modèles mis en cache – comment visualiser le dossier de cache et
  afficher le répertoire de cache
url: /fr/python/general/list-cached-models-how-to-view-cache-folder-and-show-cache-d/
---

content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# list cached models – guide rapide pour afficher le répertoire du cache

Vous vous êtes déjà demandé comment **list cached models** sur votre poste de travail sans fouiller dans des dossiers obscurs ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent vérifier quels modèles d'IA sont déjà stockés localement, surtout lorsque l'espace disque est limité. La bonne nouvelle ? En quelques lignes seulement, vous pouvez à la fois **list cached models** et **show cache directory**, vous offrant une visibilité complète sur votre dossier de cache.

Dans ce tutoriel, nous allons parcourir un script Python autonome qui fait exactement cela. À la fin, vous saurez comment afficher le dossier de cache, comprendre où le cache réside sur différents systèmes d'exploitation, et même voir une liste imprimée propre de chaque modèle téléchargé. Pas de documentation externe, pas de devinettes — juste du code clair et des explications que vous pouvez copier‑coller dès maintenant.

## Ce que vous apprendrez

- Comment initialiser un client IA (ou un stub) qui offre des utilitaires de mise en cache.  
- Les commandes exactes pour **list cached models** et **show cache directory**.  
- Où le cache se trouve sous Windows, macOS et Linux, afin que vous puissiez y naviguer manuellement si vous le souhaitez.  
- Conseils pour gérer les cas limites tels qu'un cache vide ou un chemin de cache personnalisé.  

**Prerequisites** – vous avez besoin de Python 3.8+ et d'un client IA installable via pip qui implémente `list_local()`, `get_local_path()`, et éventuellement `clear_local()`. Si vous n'en avez pas encore, l'exemple utilise une classe factice `YourAIClient` que vous pouvez remplacer par le SDK réel (par ex., `openai`, `huggingface_hub`, etc.).  

Prêt ? Plongeons‑y.

## Étape 1 : Configurer le client IA (ou un Mock)

If you already have a client object, skip this block. Otherwise, create a tiny stand‑in that mimics the caching interface. This makes the script runnable even without a real SDK.

```python
# step_1_client_setup.py
import os
from pathlib import Path

class YourAIClient:
    """
    Minimal mock of an AI client that stores downloaded models in a
    directory called `.ai_cache` inside the user's home folder.
    """
    def __init__(self, cache_dir: Path | None = None):
        # Use a custom path if supplied, otherwise default to ~/.ai_cache
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        """Return a list of model folder names that exist in the cache."""
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        """Absolute path to the cache directory."""
        return str(self.cache_dir.resolve())

    # Optional helper for demonstration purposes
    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# Initialize the client (replace with real client if you have one)
ai = YourAIClient()
# Populate with dummy data the first time you run the script
if not ai.list_local():
    ai._populate_dummy_models()
```

> **Pro tip:** If you already have a real client (e.g., `from huggingface_hub import HfApi`), just replace the `YourAIClient()` call with `HfApi()` and make sure the methods `list_local` and `get_local_path` exist or are wrapped accordingly.

## Étape 2 : **list cached models** – récupérer et afficher les modèles

Now that the client is ready, we can ask it to enumerate everything it knows about locally. This is the core of our **list cached models** operation.

```python
# step_2_list_models.py
print("Cached models:")
for model_name in ai.list_local():
    print(" -", model_name)
```

**Sortie attendue** (avec les données factices de l'étape 1) :

```
Cached models:
 - model_1
 - model_2
 - model_3
```

Si le cache est vide, vous verrez simplement :

```
Cached models:
```

Cette petite ligne vide indique qu'aucune donnée n'est encore stockée — pratique lorsque vous écrivez des routines de nettoyage.

## Étape 3 : **show cache directory** – où le cache se trouve ?

Knowing the path is often half the battle. Different operating systems place caches in different default locations, and some SDKs let you override it via environment variables. The following snippet prints the absolute path so you can `cd` into it or open it in a file explorer.

```python
# step_3_show_path.py
print("\nCache directory:", ai.get_local_path())
```

**Sortie typique** sur un système de type Unix :

```
Cache directory: /home/youruser/.ai_cache
```

Sous Windows, vous pourriez voir quelque chose comme :

```
Cache directory: C:\Users\YourUser\.ai_cache
```

Vous savez maintenant exactement **how to view cache folder** sur n'importe quelle plateforme.

## Étape 4 : Tout rassembler – un script unique exécutable

Below is the complete, ready‑to‑run program that combines the three steps. Save it as `view_ai_cache.py` and execute `python view_ai_cache.py`.

```python
# view_ai_cache.py
import os
from pathlib import Path

class YourAIClient:
    """Simple mock client exposing cache‑related utilities."""
    def __init__(self, cache_dir: Path | None = None):
        self.cache_dir = Path(cache_dir) if cache_dir else Path.home() / ".ai_cache"
        self.cache_dir.mkdir(parents=True, exist_ok=True)

    def list_local(self):
        return [p.name for p in self.cache_dir.iterdir() if p.is_dir()]

    def get_local_path(self):
        return str(self.cache_dir.resolve())

    def _populate_dummy_models(self, count=3):
        for i in range(1, count + 1):
            (self.cache_dir / f"model_{i}").mkdir(exist_ok=True)

# ----------------------------------------------------------------------
# Main execution block
# ----------------------------------------------------------------------
if __name__ == "__main__":
    # Initialize (replace with real client if available)
    ai = YourAIClient()

    # Populate dummy data only on first run – remove this in production
    if not ai.list_local():
        ai._populate_dummy_models()

    # Step 1: list cached models
    print("Cached models:")
    for model_name in ai.list_local():
        print(" -", model_name)

    # Step 2: show cache directory
    print("\nCache directory:", ai.get_local_path())
```

Exécutez‑le et vous verrez instantanément à la fois la liste des modèles en cache **et** l'emplacement du répertoire du cache.

## Cas limites & variations

| Situation | What to Do |
|-----------|------------|
| **Cache vide** | Le script affichera « Cached models : » sans aucune entrée. Vous pouvez ajouter un avertissement conditionnel : `if not models: print("⚠️ No models cached yet.")` |
| **Chemin de cache personnalisé** | Passez un chemin lors de la construction du client : `YourAIClient(cache_dir=Path("/tmp/my_ai_cache"))`. L'appel `get_local_path()` reflétera cet emplacement personnalisé. |
| **Erreurs d'autorisation** | Sur des machines restreintes, le client peut lever `PermissionError`. Enveloppez l'initialisation dans un bloc `try/except` et revenez à un répertoire accessible en écriture par l'utilisateur. |
| **Utilisation du SDK réel** | Remplacez `YourAIClient` par la classe client réelle et assurez‑vous que les noms de méthodes correspondent. De nombreux SDK exposent un attribut `cache_dir` que vous pouvez lire directement. |

## Astuces pro pour gérer votre cache

- **Nettoyage périodique :** Si vous téléchargez fréquemment de gros modèles, programmez une tâche cron qui appelle `shutil.rmtree(ai.get_local_path())` après avoir confirmé que vous n'en avez plus besoin.  
- **Surveillance de l'utilisation du disque :** Utilisez `du -sh $(ai.get_local_path())` sous Linux/macOS ou `Get-ChildItem -Recurse | Measure-Object -Property Length -Sum` dans PowerShell pour garder un œil sur la taille.  
- **Dossiers versionnés :** Certains clients créent des sous‑dossiers par version de modèle. Lorsque vous **list cached models**, vous verrez chaque version comme une entrée distincte — utilisez cela pour supprimer les révisions plus anciennes.  

## Vue d'ensemble visuelle

![list cached models screenshot](https://example.com/images/list-cached-models.png "list cached models – console output showing models and cache path")

*Texte alternatif :* *list cached models – sortie console affichant les noms des modèles en cache et le chemin du répertoire du cache.*

## Conclusion

We’ve covered everything you need to **list cached models**, **show cache directory**, and generally **how to view cache folder** on any system. The short script demonstrates a complete, runnable solution, explains **why** each step matters, and offers practical tips for real‑world usage.  

Next, you might explore **how to clear the cache** programmatically, or integrate these calls into a larger deployment pipeline that validates model availability before launching inference jobs. Either way, you now have the foundation to manage local AI model storage with confidence.  

Des questions sur un SDK IA spécifique ? Laissez un commentaire ci‑dessous, et bon cache !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}