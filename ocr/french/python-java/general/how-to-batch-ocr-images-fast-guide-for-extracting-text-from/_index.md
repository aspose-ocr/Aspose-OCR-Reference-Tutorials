---
category: general
date: 2026-01-12
description: Comment effectuer rapidement une OCR par lots d'images et extraire le
  texte des fichiers JPEG en Python. Apprenez le traitement par lots étape par étape
  avec un exemple complet et exécutable.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: fr
og_description: Comment effectuer une OCR par lots d'images et extraire le texte des
  fichiers JPEG. Ce guide vous accompagne à travers une solution Python complète,
  prête à l'emploi.
og_title: Comment faire de l’OCR par lots sur des images – Tutoriel Python rapide
tags:
- OCR
- Python
- image processing
title: Comment faire de l'OCR par lots d'images – Guide rapide pour extraire le texte
  des fichiers JPEG
url: /fr/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer la reconnaissance optique de caractères (OCR) par lots – Guide rapide pour extraire du texte de fichiers JPEG

Vous êtes-vous déjà demandé **comment effectuer la reconnaissance optique de caractères (OCR) par lots** sans écrire un script distinct pour chaque fichier ? Vous n'êtes pas seul. Dans de nombreux projets—numérisation de factures, archivage, modération de contenu—nous devons extraire du texte de dizaines ou de centaines de fichiers JPEG en une seule fois. La bonne nouvelle, c’est que cela ne nécessite que quelques lignes de Python, et vous disposerez d’un moteur réutilisable que vous pourrez intégrer à n’importe quel pipeline.

Dans ce tutoriel, nous vous montrons exactement **comment effectuer la reconnaissance optique de caractères (OCR) par lots**, puis nous détaillons l’extraction du texte des fichiers JPEG, la gestion des cas particuliers et la vérification du résultat. À la fin, vous disposerez d’un script autonome que vous pourrez exécuter sur n’importe quel dossier d’images, et vous comprendrez pourquoi le traitement par lots est essentiel pour les performances et la maintenabilité.

## Ce que vous allez apprendre

- Configurer un moteur OCR simple et le paramétrer pour l’anglais.  
- Rassembler tous les fichiers JPEG d’un répertoire avec `pathlib`.  
- Appeler le moteur OCR une seule fois pour traiter tout le lot.  
- Afficher un aperçu du texte reconnu pour chaque image.  
- Astuces pour gérer de gros lots, différentes langues et les pièges courants.

**Prérequis** : Python 3.8+, la bibliothèque `ocr` (ou tout wrapper compatible), et un dossier d’images JPEG que vous souhaitez analyser. Aucun service externe n’est requis — tout s’exécute localement.

---

## Étape 1 : Initialiser le moteur OCR – Le cœur de **Comment effectuer la reconnaissance optique de caractères (OCR) par lots**

Avant de pouvoir **effectuer la reconnaissance optique de caractères (OCR) par lots**, il nous faut un moteur capable de lire le texte. Dans la plupart des bibliothèques, vous créez un objet moteur, définissez éventuellement la langue, puis le réutilisez pour chaque fichier.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Pourquoi c’est important* : Initialiser le moteur une seule fois évite le surcoût de chargement répété des modèles linguistiques. Cela vous donne également un point unique où ajuster les paramètres (par ex., DPI, liste blanche de caractères) qui s’appliqueront à tout le lot.

> **Astuce** : Si vous prévoyez de traiter des documents multilingues, remplacez `ocr.Language.ENGLISH` par `ocr.Language.MULTI` ou chargez plusieurs packs de langues avant le démarrage du lot.

---

## Étape 2 : Rassembler tous les fichiers JPEG – La partie « Extraire le texte des fichiers JPEG »

Maintenant que le moteur est prêt, nous devons lui indiquer quelles images traiter. L’utilisation de `pathlib` rend le code indépendant de la plateforme et concis.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Pourquoi c’est important* : En collectant d’abord la liste des fichiers, nous pouvons fournir l’ensemble de la collection au moteur OCR en un seul appel — exactement ce que signifie **comment effectuer la reconnaissance optique de caractères (OCR) par lots**. Si vous avez des sous‑dossiers, vous pouvez changer `glob("**/*.jpg")` pour une recherche récursive.

> **Cas particulier** : Si vos images ont des extensions mixtes (`.jpeg`, `.JPG`), étendez le motif glob : `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## Étape 3 : Traiter tout le lot en un seul appel – La vraie puissance du batch OCR

La plupart des bibliothèques OCR modernes exposent une méthode `process_batch` (ou similaire) qui accepte un itérable de chemins de fichiers. C’est le cœur de **comment effectuer la reconnaissance optique de caractères (OCR) par lots** de façon efficace.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Pourquoi c’est important* : Un appel unique de lot réduit le nombre de transitions Python‑vers‑C, maintient le modèle linguistique chargé en mémoire et permet souvent une parallélisation interne. Le résultat est une liste d’objets — chacun contenant le texte reconnu et les scores de confiance.

> **Note de performance** : Pour des lots très volumineux (des milliers d’images), envisagez de diviser la liste en morceaux plus petits (par ex., 200 fichiers) afin d’éviter une consommation excessive de mémoire.

---

## Étape 4 : Afficher un aperçu du texte extrait – Validation rapide

Une fois le lot terminé, il est utile d’afficher les premiers caractères de chaque résultat. Cela vous permet de confirmer que l’OCR extrait réellement du texte de vos fichiers JPEG.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Pourquoi c’est important* : Un aperçu court vous aide à repérer les échecs évidents (texte vide, caractères illisibles) sans ouvrir chaque fichier. Si vous constatez des problèmes récurrents, vous pouvez ajuster les paramètres du moteur et relancer le lot.

> **Piège fréquent** : Oublier de supprimer les caractères de nouvelle ligne peut rendre l’aperçu désordonné. La ligne `replace("\n", " ")` nettoie cela.

---

## Exemple complet fonctionnel – Toutes les étapes combinées

Voici le script complet que vous pouvez copier‑coller, ajuster le chemin du répertoire, puis exécuter. Il illustre l’ensemble du workflow **comment effectuer la reconnaissance optique de caractères (OCR) par lots** du début à la fin.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Sortie attendue** (exemple) :

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

Si l’aperçu montre du texte significatif, vous avez réussi à **extraire du texte des fichiers JPEG** en utilisant une approche par lots.

---

## Gestion des gros lots et scénarios avancés

### Découpage des charges de travail importantes
Lorsque vous traitez des milliers d’images, la mémoire peut devenir un goulot d’étranglement. Divisez la liste en morceaux plus petits :

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Changement de langue
Si vos documents contiennent du français ou de l’espagnol, modifiez la langue avant le lot :

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Enregistrement des résultats sur disque
Au lieu d’afficher, vous pouvez écrire chaque résultat OCR dans un fichier `.txt` :

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Conclusion

Vous savez maintenant **comment effectuer la reconnaissance optique de caractères (OCR) par lots** et **extraire du texte des fichiers JPEG** à l’aide d’un script Python compact. En initialisant le moteur une fois, en rassemblant tous les chemins JPEG, en les traitant en un seul lot et en affichant un aperçu du résultat, vous obtenez à la fois rapidité et simplicité. Vous pouvez désormais étendre ce workflow — ajouter la prise en charge multilingue, stocker les résultats dans une base de données, ou intégrer le script à un pipeline de traitement de documents plus vaste.

Prêt pour l’étape suivante ? Essayez de remplacer la bibliothèque `ocr` par Tesseract, expérimentez différents pré‑traitements d’image (seuillage, redimensionnement), ou alimentez le texte extrait dans un modèle de traitement du langage naturel pour une catégorisation automatique. Le ciel est la limite, et vous disposez d’une base solide pour construire.

Bon codage, et que vos lots OCR restent toujours sans erreur !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}