---
category: general
date: 2026-06-22
description: Tutoriel OCR par lots en Python montrant comment exécuter un OCR multithread
  sur un dossier d'images PNG en utilisant Tesseract et pathlib. Apprenez l'OCR d'images
  par lots rapide en Python.
draft: false
keywords:
- python batch ocr tutorial
- multithreaded OCR in Python
- tesseract OCR batch processing
- pathlib image handling
- OCR thread count optimization
language: fr
og_description: Le tutoriel Python batch OCR vous guide à travers un script complet
  et exécutable qui traite de nombreux PNG avec Tesseract en utilisant plusieurs threads.
og_title: Tutoriel OCR par lots en Python – OCR multithread rapide pour les images
  PNG
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  headline: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  type: TechArticle
- description: python batch ocr tutorial showing how to run multithreaded OCR on a
    folder of PNG images using Tesseract and pathlib. Learn fast batch image OCR in
    Python.
  name: 'python batch ocr tutorial: Process Multiple PNGs Efficiently'
  steps:
  - name: '**Collects** every PNG with **pathlib image handling**.'
    text: '**Collects** every PNG with **pathlib image handling**.'
  - name: '**Spins up** a **multithreaded OCR in Python** worker pool.'
    text: '**Spins up** a **multithreaded OCR in Python** worker pool.'
  - name: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
    text: '**Optimizes** the number of threads for your hardware (**OCR thread count
      optimization**).'
  - name: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
    text: '**Writes** each result to a dedicated folder (**tesseract OCR batch processing**).'
  type: HowTo
tags:
- OCR
- Python
- Batch Processing
title: 'Tutoriel OCR par lots en Python : traiter plusieurs PNG efficacement'
url: /fr/python-java/general/python-batch-ocr-tutorial-process-multiple-pngs-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutoriel python batch ocr – OCR multithread rapide pour images PNG

Vous vous êtes déjà demandé comment **python batch ocr tutorial** traverser des centaines de captures d'écran PNG sans voir votre CPU surchauffer ? Vous n'êtes pas le seul. Que vous numérisiez des formulaires scannés, extrayiez du texte à partir de reçus, ou construisiez une archive consultable, un pipeline OCR batch solide vous fait gagner des heures.

Dans ce guide, nous allons créer un petit mais puissant script qui collecte chaque `*.png` dans un dossier, les transmet à Tesseract via un processeur multithread, et place les résultats en texte brut dans un répertoire de sortie bien organisé. Pas de bibliothèques mystérieuses—seulement `pathlib`, `concurrent.futures` et le toujours fiable `pytesseract`. À la fin, vous disposerez d’un **python batch ocr tutorial** que vous pourrez copier‑coller dans n’importe quel projet.

## Ce que vous apprendrez

- Comment collecter des fichiers image avec **pathlib image handling**
- Configurer un pool de travailleurs **multithreaded OCR in Python**
- Ajuster **OCR thread count optimization** pour les cœurs de votre CPU
- Enregistrer chaque résultat avec un schéma de nommage clair pour une recherche ultérieure
- Exécuter le tout comme un script unique et autonome

## Prérequis (Ce dont vous avez besoin d'abord)

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Python 3.9+ | Syntaxe moderne (`pathlib`, f‑strings) |
| Tesseract 5.x installé et accessible dans `PATH` | Le moteur OCR derrière `pytesseract` |
| `pytesseract` (`pip install pytesseract`) | Wrapper Python pour Tesseract |
| `Pillow` (`pip install pillow`) | Chargement d'images pour Tesseract |
| Un dossier de fichiers PNG que vous souhaitez traiter | Notre cible **tesseract OCR batch processing** |

> **Astuce :** Si vous êtes sous Windows, ajoutez `C:\Program Files\Tesseract-OCR` à votre `PATH` système afin que `pytesseract` puisse trouver l’exécutable automatiquement.

---

## Étape 1 – Rassembler toutes les images PNG (avec pathlib)

Première chose à faire : nous avons besoin d’une liste de chaque image sur laquelle nous prévoyons d’exécuter l’OCR. `pathlib` rend cela possible en une seule ligne et garde le code indépendant du système d’exploitation.

```python
import pathlib

# Adjust the path to point at your source folder
source_dir = pathlib.Path("YOUR_DIRECTORY/batch_images")
image_files = list(source_dir.glob("*.png"))

print(f"Found {len(image_files)} PNG files to process.")
```

*Pourquoi `pathlib` ?* Il abstrait les barres obliques inverses de Windows versus les barres obliques Unix, permettant au même script de fonctionner partout. C’est la pierre angulaire de **pathlib image handling** dans notre tutoriel.

---

## Étape 2 – Définir une classe simple de processeur OCR batch

Voici un wrapper léger qui masque le boilerplate du threading. Il reflète le pseudo‑code que vous avez vu précédemment mais est entièrement fonctionnel.

```python
import concurrent.futures
import pytesseract
from PIL import Image
import os

class BatchOcrProcessor:
    """Encapsulates multithreaded OCR logic."""

    def __init__(self):
        self.thread_count = os.cpu_count() or 4  # sensible default
        self.output_folder = pathlib.Path("ocr_results")
        self.output_folder.mkdir(parents=True, exist_ok=True)

    def set_thread_count(self, count: int):
        """Adjust the number of worker threads (OCR thread count optimization)."""
        if count < 1:
            raise ValueError("Thread count must be at least 1")
        self.thread_count = count
        print(f"Thread pool size set to {self.thread_count}")

    def set_output_folder(self, folder: str):
        """Where each OCR result will be saved (tesseract OCR batch processing)."""
        self.output_folder = pathlib.Path(folder)
        self.output_folder.mkdir(parents=True, exist_ok=True)
        print(f"Output folder set to {self.output_folder}")

    def _process_single(self, image_path: pathlib.Path):
        """Run OCR on a single image and write the text file."""
        try:
            img = Image.open(image_path)
            text = pytesseract.image_to_string(img)
            out_file = self.output_folder / f"{image_path.stem}.txt"
            out_file.write_text(text, encoding="utf-8")
            return f"✅ {image_path.name} → {out_file.name}"
        except Exception as exc:
            return f"❌ {image_path.name} failed: {exc}"

    def process(self, image_paths):
        """Run OCR on the entire batch using a thread pool."""
        print("🚀 Starting batch OCR...")
        with concurrent.futures.ThreadPoolExecutor(max_workers=self.thread_count) as executor:
            results = list(executor.map(self._process_single, image_paths))
        for line in results:
            print(line)
        print("🏁 Batch OCR completed.")
```

**Explication des choix clés**

- **ThreadPoolExecutor** nous offre un vrai multithreading pour les tâches I/O‑bound comme la lecture de fichiers et l’invocation du binaire externe Tesseract.  
- La méthode `set_thread_count` est l’endroit où vous pouvez expérimenter avec **OCR thread count optimization** ; plus de threads signifient souvent un débit plus rapide jusqu’au point où vos cœurs CPU deviennent saturés.  
- Chaque image produit un fichier `.txt` nommé d’après le PNG original—parfait pour l’indexation ou la recherche ultérieure.

---

## Étape 3 – Assembler le tout

Nous instancions maintenant le processeur, ajustons le nombre de threads, le pointons vers notre dossier de sortie, et enfin lui transmettons la liste des images.

```python
if __name__ == "__main__":
    # 1️⃣ Gather PNGs (already done above)
    # 2️⃣ Create processor instance
    ocr_processor = BatchOcrProcessor()

    # 3️⃣ Configure thread pool – feel free to change 8 → your core count
    ocr_processor.set_thread_count(8)   # multithreaded OCR in Python

    # 4️⃣ Choose where results land
    ocr_processor.set_output_folder("YOUR_DIRECTORY/ocr_results")

    # 5️⃣ Run the batch – this call blocks until everything is done
    ocr_processor.process(image_files)

    # 6️⃣ All done – a friendly console message
    print("✅ All images processed. Check the ocr_results folder.")
```

L’exécution du script produira une sortie similaire à :

```
Found 42 PNG files to process.
Thread pool size set to 8
Output folder set to YOUR_DIRECTORY/ocr_results
🚀 Starting batch OCR...
✅ invoice_001.png → invoice_001.txt
✅ receipt_2023-04-15.png → receipt_2023-04-15.txt
...
🏁 Batch OCR completed.
✅ All images processed. Check the ocr_results folder.
```

Chaque `.txt` contient la sortie OCR brute. Ouvrez n’importe quel fichier et vous verrez le texte extrait prêt pour l’indexation, l’analyse de sentiment, ou tout ce qui suit.

---

## Étape 4 – Pièges courants & comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Fichiers `.txt` vides | Tesseract ne trouve pas les données de langue ou l’image est trop sombre | Installez les packs de langue (`tesseract-ocr-eng`) et prétraitez les images (augmentez le contraste). |
| `UnicodeDecodeError` lors de la lecture des résultats | La sortie contient des caractères non‑UTF‑8 | Écrivez les fichiers avec `encoding="utf-8"` (déjà dans le code) ou utilisez `errors="ignore"` comme solution rapide. |
| Pics d’utilisation CPU, aucun gain de vitesse | Le nombre de threads dépasse les cœurs physiques | Réduisez `set_thread_count` à `os.cpu_count()` ou moins. |
| `FileNotFoundError` à l’ouverture de l’image | Le chemin contient des caractères non‑ASCII sous Windows | Préfixez la chaîne avec `r` ou utilisez directement les objets `pathlib` (comme nous le faisons). |

---

## Étape 5 – Étendre le tutoriel (Prochaines étapes)

- **Ajouter un prétraitement d’image** avec OpenCV (`cv2`) pour améliorer la précision de l’OCR (ex. redressement, seuillage).  
- **Paralléliser sur plusieurs machines** en utilisant `multiprocessing` ou une file de tâches simple comme RabbitMQ pour des charges de travail massives.  
- **Intégrer avec un moteur de recherche** (Elasticsearch) pour rendre le texte extrait interrogeable en temps réel.  
- **Remplacer Tesseract par une API OCR cloud** (Google Vision, Azure Computer Vision) si vous avez besoin d’une plus grande précision sur le texte manuscrit.

Toutes ces idées s’appuient sur la base que vous avez maintenant : un **python batch ocr tutorial** propre qui fonctionne immédiatement.

---

## Conclusion

Vous venez de créer un **python batch ocr tutorial** complet qui :

1. **Collecte** chaque PNG avec **pathlib image handling**.  
2. **Lance** un pool de travailleurs **multithreaded OCR in Python**.  
3. **Optimise** le nombre de threads pour votre matériel (**OCR thread count optimization**).  
4. **Écrit** chaque résultat dans un dossier dédié (**tesseract OCR batch processing**).  

Le script est prêt à être intégré dans n’importe quel pipeline, que vous traitiez des reçus, des documents juridiques, ou une montagne de captures d’écran. Jouez avec le nombre de threads, ajoutez du pré‑traitement d’image, ou connectez la sortie à une base de données—à vous de choisir.

Des questions ? N’hésitez pas à commenter ci‑dessous, et bon codage !

![Diagramme du flux de travail du tutoriel python batch ocr traitant plusieurs fichiers PNG en parallèle](/images/python-batch-ocr-workflow.png){.center width=600 alt="flux de travail du tutoriel python batch ocr"}

---


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Tutoriel Aspose OCR – Reconnaissance Optique de Caractères](/ocr/english/)
- [Comment faire du batch OCR d’images avec List dans Aspose.OCR pour .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extraire le texte d’une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}