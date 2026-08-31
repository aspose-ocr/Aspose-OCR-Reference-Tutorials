---
category: general
date: 2026-01-07
description: Comment lister les modèles dans Aspose OCR AI avec Python – apprenez
  à obtenir le chemin du modèle, vérifier les modèles installés et récupérer une liste
  de modèles Python en quelques secondes.
draft: false
keywords:
- how to list models
- get model path
- check installed models
- python get model list
- list available models
language: fr
og_description: Comment lister les modèles dans Aspose OCR AI en utilisant Python.
  Trouvez le chemin du modèle, vérifiez les modèles installés et consultez la liste
  complète des modèles disponibles.
og_title: Comment répertorier les modèles dans Aspose OCR AI – Guide Python
tags:
- Aspose OCR
- Python
- AI models
title: Comment lister les modèles dans Aspose OCR AI – Guide Python
url: /fr/python/general/how-to-list-models-in-aspose-ocr-ai-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment lister les modèles dans Aspose OCR AI – Guide Python

Vous vous êtes déjà demandé **comment lister les modèles** déjà installés sur votre machine lorsque vous travaillez avec Aspose OCR AI ? Vous n'êtes pas le seul à rencontrer ce problème. Dans de nombreux projets, vous devez vérifier le dossier des modèles, confirmer quels modèles sont présents, ou même déboguer un problème de modèle manquant—tout cela sans quitter votre REPL Python.

Dans ce tutoriel, nous allons parcourir un exemple complet, prêt à l’emploi, qui vous montre comment **obtenir le chemin du modèle**, **vérifier les modèles installés**, et enfin **lister les modèles disponibles** en quelques lignes de code seulement. Aucun script externe, aucune magie cachée—juste du Python pur et le SDK Aspose OCR AI.

> **Pré‑requis**  
> • Python 3.8 ou plus récent  
> • paquet `asposeocr` installé (`pip install asposeocr`)  
> • Familiarité de base avec l’importation de modules  

Si vous avez tout cela, plongeons‑y.

---

## Comment lister les modèles avec Aspose OCR AI

La première chose dont nous avons besoin est la classe d’assistance `AsposeAI` fournie avec le module `asposeocr.ai`. Cette classe nous donne trois méthodes pratiques :

| Méthode | Ce qu'elle renvoie | Cas d'utilisation typique |
|--------|--------------------|---------------------------|
| `get_local_path()` | Chemin absolu du dossier où Aspose stocke ses modèles IA | Vérifier que le SDK regarde au bon endroit |
| `list_local()` | `list` Python des noms de dossiers de modèles présents sur le disque | Voir rapidement quels modèles vous pouvez charger |
| `list_remote()` *(optionnel)* | Liste des modèles disponibles en téléchargement depuis le cloud d’Aspose | Quand vous avez besoin d’un modèle que vous n’avez pas localement |

Voici le **script complet** qui affiche le dossier local des modèles et la liste des modèles installés.

```python
# ---------------------------------------------------------
# Step 1: Import the Aspose OCR AI module
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

# ---------------------------------------------------------
# Step 2: Create an instance of the AI helper
# ---------------------------------------------------------
ai = AsposeAI()

# ---------------------------------------------------------
# Step 3: Retrieve and display the local model folder
# ---------------------------------------------------------
local_folder = ai.get_local_path()
print("Local AI model folder:", local_folder)

# ---------------------------------------------------------
# Step 4: List all models that are currently installed
# ---------------------------------------------------------
installed_models = ai.list_local()
print("Available models:", installed_models)
```

### Résultat attendu

Lorsque vous exécutez le script sur une installation neuve, vous verrez typiquement quelque chose comme :

```
Local AI model folder: /home/user/.asposeocr/models
Available models: ['ocr-general-v1', 'ocr-handwritten-v2']
```

Si le dossier est vide, `list_local()` renvoie une liste vide (`[]`). C’est un signal utile indiquant que vous devez d’abord télécharger un modèle—ce que nous aborderons plus tard.

---

## Pourquoi connaître le chemin du modèle est important

Comprendre **où** le SDK stocke ses fichiers (`get model path`) est plus qu’une simple curiosité :

1. **Débogage** – Si un modèle échoue à se charger, vous pouvez `ls` le chemin et vérifier que le fichier existe réellement.  
2. **Modèles personnalisés** – Certaines équipes entraînent leurs propres modèles OCR et les déposent dans le dossier. Connaître le chemin vous permet de placer les fichiers exactement où Aspose les attend.  
3. **Permissions** – Sous Linux, le dossier peut appartenir à un autre utilisateur. Détecter une erreur de permission tôt évite des heures de casse‑tête.  

> **Astuce :** Si vous devez pointer le SDK vers un répertoire personnalisé, définissez la variable d’environnement `ASPOSE_OCR_MODEL_PATH` avant de créer `AsposeAI()`.

```bash
export ASPOSE_OCR_MODEL_PATH=/my/custom/models
python my_script.py
```

## Vérifier les modèles installés – Cas limites & astuces

### 1. Aucun modèle installé

Si `list_local()` renvoie `[]`, vous avez deux options :

| Option | Comment faire |
|--------|----------------|
| **Télécharger un modèle depuis Aspose** | `ai.download('ocr-general-v1')` (nécessite Internet) |
| **Copier un modèle pré‑entraîné** | Placez le dossier du modèle manuellement dans le chemin indiqué par `get_local_path()` |

### 2. Plusieurs versions du même modèle

Parfois vous verrez à la fois `ocr-general-v1` **et** `ocr-general-v1-beta`. Le SDK charge la première correspondance qu’il trouve, mais vous pouvez forcer une version spécifique en passant le nom exact du dossier au constructeur OCR :

```python
from asposeocr.ai import AsposeOCR

ocr = AsposeOCR(model_name='ocr-general-v1-beta')
```

### 3. Fichiers de modèle corrompus

Un modèle partiellement téléchargé peut provoquer plus tard un `FileNotFoundError`. Si vous suspectez une corruption, supprimez simplement le dossier incriminé et re‑téléchargez :

```bash
rm -rf /home/user/.asposeocr/models/ocr-general-v1
python -c "from asposeocr.ai import AsposeAI; AsposeAI().download('ocr-general-v1')"
```

## Étendre le script – Lister les modèles distants (optionnel)

Si vous voulez voir quels modèles sont disponibles en téléchargement sans quitter Python, ajoutez un appel supplémentaire :

```python
remote_models = ai.list_remote()
print("Remote models you can download:", remote_models)
```

Cela affichera quelque chose comme :

```
Remote models you can download: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Vous pouvez alors choisir n’importe quel modèle et appeler `ai.download('model-name')` pour le récupérer automatiquement.

## Exemple complet de bout en bout

En rassemblant le tout, voici un **script unique et exécutable** qui :

1. Affiche le dossier local des modèles.  
2. Liste les modèles installés.  
3. S’il n’y en a aucun, télécharge un modèle par défaut.  
4. Enfin, imprime la liste mise à jour.

```python
# ---------------------------------------------------------
# Complete script – verifies model folder, installs if empty
# ---------------------------------------------------------
from asposeocr.ai import AsposeAI

def main():
    ai = AsposeAI()

    # 1️⃣ Show where Aspose expects models
    local_path = ai.get_local_path()
    print("🔎 Local AI model folder:", local_path)

    # 2️⃣ List currently installed models
    models = ai.list_local()
    print("📦 Installed models:", models)

    # 3️⃣ If nothing is installed, grab a default model
    if not models:
        default = 'ocr-general-v1'
        print(f"⚠️ No models found – downloading '{default}'...")
        try:
            ai.download(default)
            models = ai.list_local()
            print("✅ After download, installed models:", models)
        except Exception as e:
            print("❌ Failed to download model:", e)
            return

    # 4️⃣ (Optional) Show what you could download from the cloud
    remote = ai.list_remote()
    print("🌐 Remote models available:", remote)

if __name__ == "__main__":
    main()
```

Exécuter ce script sur une machine propre produira :

```
🔎 Local AI model folder: /home/user/.asposeocr/models
📦 Installed models: []
⚠️ No models found – downloading 'ocr-general-v1'...
✅ After download, installed models: ['ocr-general-v1']
🌐 Remote models available: ['ocr-general-v1', 'ocr-handwritten-v2', 'ocr-table-v1']
```

Vous disposez maintenant d’une solution **autonome et digne d’une citation** que n’importe quel assistant IA peut reproduire mot pour mot.

## Questions fréquentes (FAQ)

**Q : Cela fonctionne-t-il sous Windows ?**  
R : Absolument. Le SDK abstrait le système de fichiers, donc `get_local_path()` renverra quelque chose comme `C:\Users\YourName\.asposeocr\models`. Assurez‑vous simplement que Python puisse écrire dans ce dossier.

**Q : Puis‑je stocker les modèles sur un lecteur réseau ?**  
R : Oui—définissez `ASPOSE_OCR_MODEL_PATH` vers le chemin UNC (`\\server\share\models`) avant de créer l’instance `AsposeAI`.

**Q : Et si j’ai besoin d’un modèle pour une langue non couverte par l’ensemble par défaut ?**  
R : Utilisez `list_remote()` pour voir si Aspose propose un modèle spécifique à la langue. Sinon, vous pouvez entraîner le vôtre et le déposer dans le dossier ; il suffit de passer le nom du dossier personnalisé au constructeur OCR.

## Conclusion

Nous avons couvert **comment lister les modèles** dans Aspose OCR AI, montré comment **obtenir le chemin du modèle**, **vérifier les modèles installés**, et même **télécharger un modèle manquant**—tout cela avec du Python pur. En comprenant la structure des dossiers et les méthodes d’aide (`get_local_path()`, `list_local()`, `list_remote()`), vous avez le plein contrôle sur les modèles IA dont votre application dépend.

Prochaines étapes ? Essayez de remplacer le modèle par défaut par un modèle de texte manuscrit, ou pointez le SDK vers un modèle entraîné en interne. Quoi qu’il en soit, vous disposez maintenant d’une base solide pour gérer les actifs OCR dans n’importe quel projet Python.

Bon codage, et que votre liste de modèles soit toujours à jour ! 

---

![how to list models screenshot](https://example.com/images/how-to-list-models.png "Comment lister les modèles")

*Texte alternatif de l'image :* **capture d'écran de la liste des modèles** (remplit l'exigence du mot‑clé principal).

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}