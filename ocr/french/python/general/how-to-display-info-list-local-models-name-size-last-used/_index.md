---
category: general
date: 2026-01-12
description: Apprenez à afficher les informations d’AsposeAI en listant les modèles
  locaux, en montrant le nom du modèle, sa taille et l’horodatage de la dernière utilisation
  dans un exemple Python clair.
draft: false
keywords:
- how to display info
- list local models
- display model name
- show model size
- show last used
language: fr
og_description: 'Comment afficher les informations d’AsposeAI : lister les modèles
  locaux, afficher le nom du modèle, la taille et l’horodatage de la dernière utilisation
  avec un guide complet en Python.'
og_title: Comment afficher les informations – Lister les modèles locaux, le nom, la
  taille, la dernière utilisation
tags:
- AsposeAI
- Python
- Model Management
title: Comment afficher les informations – Liste des modèles locaux, nom, taille,
  dernière utilisation
url: /fr/python/general/how-to-display-info-list-local-models-name-size-last-used/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment afficher les informations – Lister les modèles locaux, nom, taille, dernière utilisation

Vous vous êtes déjà demandé **comment afficher les informations** de votre installation AsposeAI sans fouiller dans les journaux ou l'interface ? Vous n'êtes pas le seul. Dans de nombreux pipelines de data‑science, la première chose dont vous avez besoin est un aperçu rapide des modèles présents sur votre machine, de leurs noms, de leur taille et de la dernière fois que vous les avez utilisés.

C’est exactement ce que nous allons couvrir : un extrait Python concis, de bout en bout, qui **liste les modèles locaux**, puis **affiche le nom du modèle**, **montre la taille du modèle**, et **affiche les horodatages de la dernière utilisation**. Aucun bibliothèque externe, aucune magie cachée—seulement le client AsposeAI que vous avez déjà.

À la fin de ce tutoriel, vous pourrez insérer le code dans n'importe quel script, l'exécuter, et obtenir instantanément un tableau propre de vos modèles mis en cache localement. C’est parfait pour vérifier la cohérence des environnements, créer des tableaux de bord de santé, ou simplement satisfaire une curiosité sur ce qui se cache sur le disque.

## Prérequis

- Python 3.8 ou plus récent (l'exemple utilise des f‑strings, donc 3.6+ est indispensable)
- paquet `asposeai` installé (`pip install asposeai`)
- Une licence AsposeAI fonctionnelle ou une clé d'essai (le client récupérera les informations d'identification depuis les variables d'environnement ou un fichier de configuration)

Si vous avez déjà coché ces cases, super—plongeons-y.

## Étape 1 : Comment afficher les informations – Initialiser le client AsposeAI

Avant de pouvoir **lister les modèles locaux**, nous avons besoin d'un objet client qui communique avec le runtime AsposeAI. Cette étape est la base ; sans elle, le reste du code lèverait une `NameError`.

```python
# Step 1: Create an instance of the AsposeAI client
# The client automatically reads credentials from the environment
aspose_ai = AsposeAI()
```

*Pourquoi c'est important* : L'initialisation du client établit une session avec le moteur d'inférence local, charge les bibliothèques natives nécessaires. Elle valide également que votre licence est active, évitant ainsi des erreurs obscures plus tard lorsque vous essayez d'interroger les modèles.

> **Astuce** : Si vous exécutez cela sur un serveur CI, définissez `ASPOSEAI_LICENSE` dans l'environnement afin que le client puisse démarrer sans invites interactives.

## Étape 2 : Lister les modèles locaux – Récupérer les modèles disponibles

Maintenant que le client est prêt, nous pouvons **lister les modèles locaux**. La méthode `list_local()` renvoie une collection d'objets, chacun exposant des propriétés comme `name`, `size_mb` et `last_used`.

```python
# Step 2: Retrieve the list of locally available models
local_models = aspose_ai.list_local()
```

*Ce qui se passe en coulisses* : `list_local()` parcourt le répertoire où AsposeAI met en cache les fichiers de modèle (`~/.asposeai/models` par défaut) et crée des objets de métadonnées légers. C’est rapide car il ne charge pas les poids du modèle—il lit simplement un petit manifeste JSON.

Si vous vous demandez un jour si un modèle particulier est déjà mis en cache, cet appel est le moyen le plus rapide de le confirmer.

## Étape 3 : Afficher le nom du modèle, la taille du modèle et la dernière utilisation

Avec les modèles en main, nous **affichons enfin les informations** en itérant sur la collection et en imprimant chaque attribut. C’est ici que nous **affichons le nom du modèle**, **montrons la taille du modèle**, et **affichons la dernière utilisation** en une seule ligne propre.

```python
# Step 3: Print each model's name, size (in MB), and last‑used timestamp
print("Available local models:")
print("-" * 50)
for model_info in local_models:
    # Using an f‑string to format the output cleanly
    print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
```

**Sortie attendue** (vos horodatages différeront) :

```
Available local models:
--------------------------------------------------
gpt‑tiny‑en – 120 MB – last used 2025-11-02 14:23:11
bert‑base‑fr – 420 MB – last used 2025-10-18 09:07:45
whisper‑large‑audio – 1580 MB – last used 2025-09-30 22:41:02
```

*Pourquoi nous le formatons ainsi* : Le tiret (`–`) sépare les champs pour la lisibilité, et la ligne d’en‑tête rend la sortie console facile à parcourir. Si vous avez besoin d’un format lisible par machine plus tard (CSV, JSON), vous pouvez facilement remplacer l’appel `print` par un `writer.writerow` ou `json.dump`.

### Gestion des cas limites

- **Aucun modèle mis en cache** – `list_local()` renvoie une liste vide. La boucle sautera simplement, ne vous laissant que l’en‑tête. Vous pourriez vouloir ajouter une protection :

  ```python
  if not local_models:
      print("No local models found. Use aspose_ai.download(...) to fetch one.")
  ```

- **Attributs manquants** – Dans de rares cas, un manifeste peut être corrompu. Accéder à `model_info.last_used` pourrait lever une `AttributeError`. Enveloppez le `print` dans un `try/except` si vous prévoyez de tels problèmes.

- **Grandes répertoires de modèles** – Si vous avez des centaines de modèles, envisagez de paginer la sortie ou d'écrire dans un fichier plutôt que d'imprimer à la console.

## Résumé visuel (optionnel)

Si vous préférez un indice visuel rapide, le diagramme ci‑dessous illustre le flux depuis l'initialisation du client jusqu'à l'affichage final.  

![Diagramme montrant comment afficher les informations depuis le client AsposeAI](/images/how-to-display-info.png "how to display info diagram")

*Texte alternatif* : **how to display info** – schéma de l'initialisation du client AsposeAI, de la liste des modèles et de l'affichage des informations.

## Script complet fonctionnel

En rassemblant tout, voici le script complet, prêt à être exécuté :

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

"""
How to display info from AsposeAI:
List local models and show each model's name, size, and last‑used timestamp.
"""

from asposeai import AsposeAI

def main():
    # Initialize client
    aspose_ai = AsposeAI()

    # Retrieve local models
    local_models = aspose_ai.list_local()

    # Header
    print("Available local models:")
    print("-" * 50)

    if not local_models:
        print("No local models found. Use aspose_ai.download(...) to fetch one.")
        return

    # Display each model's details
    for model_info in local_models:
        try:
            print(f"{model_info.name} – {model_info.size_mb} MB – last used {model_info.last_used}")
        except AttributeError:
            # Fallback if any attribute is missing
            print(f"{model_info.name} – info incomplete")

if __name__ == "__main__":
    main()
```

Enregistrez-le sous le nom `list_models.py`, rendez-le exécutable (`chmod +x list_models.py`), puis exécutez :

```bash
./list_models.py
```

Vous verrez la liste soignée démontrée précédemment.

## Conclusion

Nous avons parcouru **comment afficher les informations** depuis AsposeAI en **listant les modèles locaux**, puis en **affichant le nom du modèle**, **montrant la taille du modèle**, et **affichant les horodatages de la dernière utilisation**. L'approche est légère, ne nécessite que le paquet standard `asposeai`, et peut être intégrée à n'importe quel pipeline d'automatisation ou session de débogage.

À partir d'ici, vous pourriez :

- Exporter la sortie vers CSV pour une analyse tableur (`module csv`).
- Alimenter les horodatages dans un tableau de bord de surveillance pour alerter sur les modèles obsolètes.
- Combiner ce script avec `aspose_ai.download()` pour rafraîchir automatiquement les modèles qui n'ont pas été utilisés depuis un certain temps.

Rappelez‑vous, une visibilité claire sur votre inventaire de modèles fait gagner du temps, réduit l'encombrement du stockage, et maintient vos services d'IA en bon fonctionnement. Testez le script, ajustez le formatage à votre goût, et laissez‑le devenir un incontournable de votre boîte à outils.

Bon codage, et que vos modèles restent toujours frais !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}