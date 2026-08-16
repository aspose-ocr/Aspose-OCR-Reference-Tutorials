---
category: general
date: 2026-04-26
description: Comment effectuer une OCR par lots de vos documents et extraire le texte
  des numérisations en Python. Apprenez le traitement par lots étape par étape avec
  OcrEngine pour une sortie JSON.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: fr
og_description: Comment réaliser une OCR par lots de vos fichiers numérisés et extraire
  le texte des scans en un seul script. Code complet, astuces et prise en charge des
  cas limites.
og_title: Comment faire de l'OCR par lots – Guide Python rapide
tags:
- OCR
- Python
- Automation
title: Comment réaliser une OCR par lots – Extraire le texte des numérisations efficacement
url: /fr/python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire du OCR par lots – Extraire du texte à partir de numérisations efficacement

Vous vous êtes déjà demandé **comment faire du OCR par lots** sur une montagne de PDF numérisés sans perdre la tête ? Vous n'êtes pas seul — les développeurs demandent constamment : *« Comment extraire du texte des numérisations en une seule passe ? »* La bonne nouvelle, c’est que quelques lignes de Python peuvent transformer cette tâche fastidieuse en un pipeline fluide et automatisé.

Dans ce tutoriel, nous parcourrons une solution complète, prête à l’emploi, qui **extrait du texte à partir de numérisations**, enregistre les résultats au format JSON, et vous donne une vérification rapide à la fin. Aucun service externe, aucune magie — juste du Python pur, la classe `OcrEngine`, et un peu de gestion de dossiers.

## Ce que vous allez retenir

- Un script pleinement fonctionnel qui **effectue du OCR par lots** sur n’importe quel dossier d’images.
- Des explications claires du *pourquoi* de chaque ligne, pas seulement du *quoi*.
- Des astuces pour gérer les dossiers vides, les fichiers non‑image et les gros lots.
- Un moyen de vérifier que la sortie JSON contient réellement le texte extrait.

### Prérequis (le strict minimum)

| Prérequis | Pourquoi c’est important |
|-----------|---------------------------|
| Python 3.8+ | Syntaxe moderne & annotations de type |
| Bibliothèque `OcrEngine` (ou un wrapper compatible) | Fonctionnalité OCR centrale |
| Un répertoire contenant des fichiers d’image numérisés (PNG, JPG, TIFF) | Données d’entrée |
| Permissions d’écriture pour le dossier de sortie | Enregistrement des résultats JSON |

Si vous avez déjà tout cela, super — plongeons‑y.

![how to batch OCR workflow](image-placeholder.png){alt="flux de travail du OCR par lots"}

## Étape 1 – Initialiser le moteur OCR (how to batch OCR)

Avant de pouvoir traiter quoi que ce soit, nous avons besoin d’une instance du moteur OCR. Pensez‑y comme le « cerveau » qui lira chaque image et produira du texte. L’initialiser une fois et le réutiliser sur tout le lot est le schéma le plus efficace.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Pourquoi réutiliser la même instance ?**  
> Créer un nouveau moteur pour chaque fichier chargerait à plusieurs reprises des modèles lourds en mémoire, ralentissant considérablement le traitement par lots. Une seule instance garde le modèle en RAM et vous permet de traiter des milliers d’images sans ralentissement perceptible.

## Étape 2 – Pointer vers votre dossier de numérisations (extract text from scans)

Vos numérisations résident quelque part sur le disque. Indiquons au script où les trouver. Utiliser des chemins absolus évite les surprises « fichier introuvable » lorsque le script est lancé depuis un répertoire de travail différent.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Astuce pro :**  
> Si vous êtes sous Windows, les barres obliques (`/`) fonctionnent très bien avec `os.path.abspath`, vous n’avez donc pas besoin d’échapper les antislashs.

## Étape 3 – Choisir où placer les résultats JSON

Vous voulez probablement un dossier bien rangé pour les résultats OCR. Garder la sortie séparée de la source facilite le nettoyage ultérieur ou l’alimentation du JSON dans un autre pipeline.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Pourquoi créer le dossier par programme ?**  
> Cela garantit que le script ne plantera pas si le répertoire est absent, et `exist_ok=True` rend l’opération idempotente — exécutez le script plusieurs fois sans erreurs.

## Étape 4 – Exécuter le processus par lots (how to batch OCR)

Voici le cœur du sujet : demander à `ocr_engine` de parcourir chaque fichier de `input_dir`, d’exécuter le OCR, puis de déposer le JSON dans `output_dir`. Le drapeau `format="json"` indique au moteur de sérialiser le résultat de façon structurée, ce que les outils en aval apprécient.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### Que se passe-t-il en coulisses ?

1. **Découverte des fichiers** – Le moteur explore `input_folder` de façon récursive, en ignorant les fichiers cachés.  
2. **Validation des fichiers** – Seules les extensions d’image prises en charge (`.png`, `.jpg`, `.tif`, etc.) sont envoyées au modèle OCR.  
3. **Exécution du OCR** – Chaque image est transmise au moteur OCR ; le texte, les scores de confiance et les données de mise en page sont capturés.  
4. **Sérialisation JSON** – Le résultat est écrit dans un fichier portant le même nom de base mais avec l’extension `.json` dans `output_folder`.

> **Gestion des cas limites :**  
> - **Dossier vide :** Le moteur consigne « No files found » et se termine gracieusement.  
> - **Image corrompue :** Le fichier est sauté, une entrée d’erreur est enregistrée dans `batch_errors.log`, et le traitement continue.  
> - **Gros lot (10 k+ fichiers) :** L’utilisation de la mémoire reste faible car chaque image est traitée indépendamment.

## Étape 5 – Confirmer que la conversion est terminée

Une simple instruction `print` fournit un retour immédiat dans la console. Pour des pipelines de production, vous remplacerez peut‑être cela par un appel de journalisation ou une notification par e‑mail.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

Lorsque vous voyez cette ligne, vous pouvez inspecter en toute sécurité le dossier `json_output`. Chaque fichier JSON ressemblera approximativement à ceci :

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

Vous pouvez maintenant injecter ces fichiers JSON dans une base de données, un index de recherche, ou tout autre outil d’analyse en aval.

## Questions fréquentes (et réponses rapides)

**Q : Et si je dois traiter des PDF au lieu d’images ?**  
R : Convertissez chaque page PDF en image d’abord (par ex., avec `pdf2image`) et placez les fichiers PNG/JPG résultants dans `input_dir`. La logique du OCR par lots reste inchangée.

**Q : Puis‑je changer le format de sortie en texte brut ?**  
R : Bien sûr. Remplacez `format="json"` par `format="txt"` et le moteur écrira un fichier `.txt` contenant uniquement le texte extrait.

**Q : Mes numérisations sont réparties dans plusieurs sous‑dossiers—le script parcourt‑il tout ?**  
R : Oui. `batch_process` parcourt l’arborescence par défaut. Si vous voulez une sortie plate, définissez `flatten=True` (si la bibliothèque le supporte) ou post‑traitez les noms de fichiers JSON.

**Q : Comment gérer les scripts non latins ?**  
R : Initialise `OcrEngine` avec un paramètre de langue, par ex., `OcrEngine(lang="spa+eng")`. La boucle de lot elle‑même ne nécessite aucun changement.

## Astuces pro & pièges courants

- **La taille du lot compte :** Si vous remarquez des pics CPU, limitez le processus avec un simple `time.sleep(0.1)` entre les fichiers.  
- **Journalisation :** Remplacez l’appel `print` par le module `logging` de Python pour capturer les horodatages et les niveaux d’erreur.  
- **Collisions de noms de fichiers :** Si deux numérisations partagent le même nom de base mais se trouvent dans des sous‑dossiers différents, les fichiers JSON s’écraseront. Ajoutez un hash du chemin relatif au nom de sortie pour éviter cela.  
- **Fuites de mémoire :** Certains back‑ends OCR conservent des ressources natives. Appelez `ocr_engine.close()` à la fin de votre script si la bibliothèque propose une méthode de nettoyage.

## Script complet – Prêt à copier‑coller

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Sortie console attendue**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

Vous pouvez vérifier le JSON en ouvrant n’importe quel fichier dans `json_output` avec un éditeur de texte ou en le chargeant dans Python :

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

Vous devriez voir le texte brut extrait par OCR affiché dans la console.

## Conclusion

Nous venons de couvrir **comment faire du OCR par lots** sur un répertoire complet d’images numérisées et **extraire du texte à partir de numérisations** dans des fichiers JSON propres et lisibles par machine. L’approche est volontairement simple : configurez le moteur une fois, pointez‑le vers un dossier, et laissez la bibliothèque faire le travail lourd. À partir d’ici, vous pouvez :

- Brancher le JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}