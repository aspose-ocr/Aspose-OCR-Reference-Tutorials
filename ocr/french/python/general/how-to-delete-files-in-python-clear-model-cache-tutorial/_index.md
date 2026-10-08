---
category: general
date: 2026-02-22
description: Comment supprimer des fichiers en Python et vider rapidement le cache
  du modèle. Apprenez à lister les fichiers d’un répertoire en Python, filtrer les
  fichiers par extension et supprimer un fichier en Python en toute sécurité.
draft: false
keywords:
- how to delete files
- clear model cache
- list directory files python
- filter files by extension
- delete file python
language: fr
og_description: Comment supprimer des fichiers en Python et vider le cache du modèle.
  Guide étape par étape couvrant la liste des fichiers d’un répertoire en Python,
  le filtrage des fichiers par extension et la suppression de fichiers en Python.
og_title: Comment supprimer des fichiers en Python – tutoriel pour effacer le cache
  du modèle
tags:
- python
- file-system
- automation
title: Comment supprimer des fichiers en Python – tutoriel pour nettoyer le cache
  du modèle
url: /fr/python/general/how-to-delete-files-in-python-clear-model-cache-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment supprimer des fichiers en Python – tutoriel de nettoyage du cache du modèle

Vous êtes-vous déjà demandé **comment supprimer des fichiers** dont vous n’avez plus besoin, surtout lorsqu’ils encombrent un répertoire de cache de modèle ? Vous n’êtes pas seul ; de nombreux développeurs rencontrent ce problème lorsqu’ils expérimentent avec de grands modèles de langage et se retrouvent avec une montagne de fichiers *.gguf*.  

Dans ce guide, nous vous présentons une solution concise, prête à l’emploi, qui non seulement explique **comment supprimer des fichiers**, mais aussi **clear model cache**, **list directory files python**, **filter files by extension**, et **delete file python** de manière sûre et multiplateforme. À la fin, vous disposerez d’un script d’une ligne que vous pourrez intégrer à n’importe quel projet, ainsi que de quelques astuces pour gérer les cas limites.

![illustration de la suppression de fichiers](https://example.com/clear-cache.png "comment supprimer des fichiers en Python")

## Comment supprimer des fichiers en Python – nettoyer le cache du modèle

### Ce que couvre le tutoriel
- Récupérer le chemin où la bibliothèque AI stocke ses modèles en cache.  
- Lister chaque entrée dans ce répertoire.  
- Sélectionner uniquement les fichiers se terminant par **.gguf** (c’est l’étape de *filter files by extension*).  
- Supprimer ces fichiers tout en gérant les éventuelles erreurs de permission.  

Aucune dépendance externe, aucun package tiers sophistiqué — seulement le module intégré `os` et un petit helper du hypothétique `ai` SDK.

## Étape 1 : List Directory Files Python

Tout d’abord, nous devons savoir ce qui se trouve dans le dossier de cache. La fonction `os.listdir()` renvoie une simple liste de noms de fichiers, idéale pour un inventaire rapide.

```python
import os

# Assume `ai.get_local_path()` returns the absolute cache directory.
cache_dir_path = ai.get_local_path()

# Grab every entry – this is the “list directory files python” part.
all_entries = os.listdir(cache_dir_path)
print(f"Found {len(all_entries)} items in cache:")
for entry in all_entries:
    print(" •", entry)
```

**Pourquoi c’est important :**  
Lister le répertoire vous donne de la visibilité. Si vous sautez cette étape, vous pourriez supprimer accidentellement quelque chose que vous ne vouliez pas toucher. De plus, la sortie imprimée sert de contrôle de bon sens avant de commencer à effacer des fichiers.

## Étape 2 : Filter Files by Extension

Toutes les entrées ne sont pas des fichiers de modèle. Nous ne voulons purger que les binaires *.gguf*, donc nous filtrons la liste avec la méthode `str.endswith()`.

```python
# Keep only files that end with .gguf – our “filter files by extension” logic.
model_files = [f for f in all_entries if f.lower().endswith(".gguf")]
print(f"\nIdentified {len(model_files)} model file(s) to delete:")
for mf in model_files:
    print(" •", mf)
```

**Pourquoi filtrer :**  
Un effacement massif imprudent pourrait supprimer des journaux, des fichiers de configuration, voire des données utilisateur. En vérifiant explicitement l’extension, nous garantissons que **delete file python** ne cible que les artefacts prévus.

## Étape 3 : Delete File Python Safely

Voici le cœur de **comment supprimer des fichiers**. Nous itérerons sur `model_files`, construirons un chemin absolu avec `os.path.join()`, puis appellerons `os.remove()`. Envelopper l’appel dans un bloc `try/except` nous permet de signaler les problèmes de permission sans faire planter le script.

```python
for file_name in model_files:
    file_path = os.path.join(cache_dir_path, file_name)
    try:
        os.remove(file_path)
        print(f"Removed: {file_name}")
    except PermissionError:
        print(f"⚠️  Permission denied: {file_name}")
    except FileNotFoundError:
        # This could happen if another process already deleted the file.
        print(f"⚠️  Already gone: {file_name}")
    except OSError as e:
        # Catch‑all for unexpected OS errors.
        print(f"❌  Failed to delete {file_name}: {e}")

print("\nOld model files removed.")
```

**Ce que vous verrez :**  
Si tout se passe bien, la console affichera chaque fichier comme « Removed ». En cas d’erreur, vous recevrez un avertissement convivial plutôt qu’une trace d’erreur cryptique. Cette approche incarne la meilleure pratique pour **delete file python** — anticiper et gérer les erreurs.

## Bonus : Vérifier la suppression et gérer les cas limites

### Vérifier que le répertoire est propre

Après la boucle, il est judicieux de revérifier qu’aucun fichier *.gguf* ne reste.

```python
remaining = [f for f in os.listdir(cache_dir_path) if f.lower().endswith(".gguf")]
if not remaining:
    print("✅  Cache is now clean.")
else:
    print("⚡  Some files survived:", remaining)
```

### Et si le dossier de cache est absent ?

Il se peut que le SDK AI n’ait pas encore créé le cache. Protégez‑vous dès le départ :

```python
if not os.path.isdir(cache_dir_path):
    raise RuntimeError(f"The cache directory does not exist: {cache_dir_path}")
```

### Supprimer un grand nombre de fichiers efficacement

Si vous devez gérer des milliers de fichiers de modèle, envisagez d’utiliser `os.scandir()` pour un itérateur plus rapide, ou même `pathlib.Path.glob("*.gguf")`. La logique reste la même ; seule la méthode d’énumération change.

## Script complet, prêt à l’exécution

En rassemblant le tout, voici le fragment complet que vous pouvez copier‑coller dans un fichier nommé `clear_model_cache.py` :

```python
import os

# -------------------------------------------------
# Step 0: Obtain the cache directory from the AI SDK
# -------------------------------------------------
cache_dir_path = ai.get_local_path()

# -------------------------------------------------
# Safety check: make sure the directory exists
# -------------------------------------------------
if not os.path.isdir(cache_dir_path):
    raise RuntimeError(f"The cache directory does not exist: {cache_dir_path}")

# -------------------------------------------------
# Step 1: List everything (list directory files python)
# -------------------------------------------------
all_entries = os.listdir(cache_dir_path)

# -------------------------------------------------
# Step 2: Keep only .gguf model files (filter files by extension)
# -------------------------------------------------
model_files = [f for f in all_entries if f.lower().endswith(".gguf")]

# -------------------------------------------------
# Step 3: Delete each model file (delete file python)
# -------------------------------------------------
for file_name in model_files:
    file_path = os.path.join(cache_dir_path, file_name)
    try:
        os.remove(file_path)
        print(f"Removed: {file_name}")
    except PermissionError:
        print(f"⚠️  Permission denied: {file_name}")
    except FileNotFoundError:
        print(f"⚠️  Already gone: {file_name}")
    except OSError as e:
        print(f"❌  Failed to delete {file_name}: {e}")

# -------------------------------------------------
# Bonus: Verify everything is gone
# -------------------------------------------------
remaining = [f for f in os.listdir(cache_dir_path) if f.lower().endswith(".gguf")]
if not remaining:
    print("\n✅  Cache is now clean.")
else:
    print("\n⚡  Some files survived:", remaining)

print("\nOld model files removed.")
```

Exécuter ce script va :

1. Localiser le cache du modèle AI.  
2. Lister chaque entrée (satisfaire l’exigence **list directory files python**).  
3. Filtrer les fichiers *.gguf* (**filter files by extension**).  
4. Supprimer chacun en toute sécurité (**delete file python**).  
5. Confirmer que le cache est vide, vous offrant ainsi la tranquillité d’esprit.

## Conclusion

Nous avons parcouru **comment supprimer des fichiers** en Python en nous concentrant sur le nettoyage d’un cache de modèle. La solution complète vous montre comment **list directory files python**, appliquer un **filter files by extension**, et **delete file python** en toute sécurité tout en gérant les pièges courants comme les permissions manquantes ou les conditions de concurrence.  

Et après ? Essayez d’adapter le script à d’autres extensions (par ex. `.bin` ou `.ckpt`) ou intégrez‑le à une routine de nettoyage plus large qui s’exécute après chaque téléchargement de modèle. Vous pouvez également explorer `pathlib` pour une approche plus orientée objet, ou planifier le script avec `cron`/`Task Scheduler` afin de garder votre espace de travail propre automatiquement.

Des questions sur les cas limites, ou envie de voir comment cela fonctionne sous Windows vs. Linux ? Laissez un commentaire ci‑dessous, et bon nettoyage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}