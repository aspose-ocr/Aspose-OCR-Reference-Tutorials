---
category: general
date: 2026-06-22
description: Créer un PDF consultable en Python avec OCR – apprenez comment convertir
  une image en PDF, reconnaître le texte du PDF et automatiser votre flux de travail.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- recognize text pdf
- python ocr pdf
language: fr
og_description: Créer un PDF consultable en Python avec OCR. Suivez ce tutoriel étape
  par étape pour convertir une image en PDF, reconnaître le texte du PDF et automatiser
  le traitement des documents.
og_title: Créer un PDF consultable en Python – Guide complet d’OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  headline: Create searchable PDF in Python – Complete OCR Guide
  type: TechArticle
- description: Create searchable PDF in Python using OCR – learn how to convert image
    to PDF, recognize text PDF, and automate your workflow.
  name: Create searchable PDF in Python – Complete OCR Guide
  steps:
  - name: Initialise the OCR engine
    text: The first thing you do is spin up an `OcrEngine` object. Think of it as
      turning on a scanner that’s ready to read your image.
  - name: Load the image you want to convert
    text: Next we feed the engine with an image stream. The `ImageStream.from_file`
      helper reads the file and wraps it in a format the OCR engine understands.
  - name: Tell the engine to output a searchable PDF
    text: By default many OCR SDKs output plain text. We need to switch the output
      format to PDF so the resulting file is both visual and searchable.
  - name: Prepare an in‑memory stream for the PDF data
    text: Instead of writing directly to disk, we capture the PDF in a `MemoryStream`.
      This keeps I/O fast and lets you pipe the bytes elsewhere (e.g., upload to S3)
      if you wish.
  - name: Run the recognition and write the PDF
    text: Now the heavy lifting happens. The `recognize` call reads the image, runs
      OCR, and streams the searchable PDF into `pdf_stream`.
  - name: Save the generated PDF to a file
    text: Finally, we dump the bytes from the memory stream onto disk. The resulting
      file can be opened in Adobe Reader, Preview, or any PDF viewer with full‑text
      search.
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Créer un PDF recherchable en Python – Guide complet d’OCR
url: /fr/python-java/general/create-searchable-pdf-in-python-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable en Python – Guide complet OCR

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d'un contrat numérisé mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul—de nombreux développeurs rencontrent le même obstacle lorsqu'ils essaient pour la première fois de transformer une image bitmap en document texte‑consultable. La bonne nouvelle, c'est qu'avec un petit script Python, vous pouvez **convertir une image en PDF**, laisser le moteur OCR reconnaître chaque mot, et obtenir un fichier parfaitement consultable.

Dans ce tutoriel, nous parcourrons l'ensemble du processus, de l'installation de la bonne bibliothèque à la gestion des cas particuliers comme les documents multi‑pages. À la fin, vous serez capable de **ocr image to pdf**, **recognize text pdf**, et d'intégrer le flux de travail dans des pipelines d'automatisation plus larges.

## Ce dont vous aurez besoin

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Python 3.8 or newer | Syntaxe moderne et meilleures annotations de type |
| `ocr` Python package (or any compatible OCR SDK) | Fournit `OcrEngine`, `ImageStream`, et la sortie PDF |
| A scanned image (JPEG, PNG, or TIFF) | Une image numérisée (JPEG, PNG ou TIFF) |
| Write access to a folder for the output PDF | Accès en écriture à un dossier pour le PDF de sortie |

Si vous n'avez pas encore installé le SDK, exécutez :

```bash
pip install ocr-sdk   # replace with the actual package name
```

> **Astuce pro :** Utilisez un environnement virtuel (`python -m venv .venv`) pour garder les dépendances propres.

## Vue d'ensemble du flux de travail

1. **Créer une instance du moteur OCR** – le cerveau derrière la reconnaissance.  
2. **Charger l'image** que vous souhaitez traiter.  
3. **Configurer le moteur** pour produire un PDF consultable plutôt que du texte brut.  
4. **Préparer un flux en mémoire** qui contiendra les octets du PDF.  
5. **Exécuter la reconnaissance** – le moteur lit l'image, extrait le texte et écrit le PDF.  
6. **Enregistrer le PDF sur le disque** afin de pouvoir l'ouvrir avec n'importe quel visualiseur.

C’est tout le processus en six lignes de code. Décomposons chaque étape.

---

## Créer un PDF consultable – Tutoriel OCR Python étape par étape

### Étape 1 : Initialiser le moteur OCR

La première chose à faire est d'instancier un objet `OcrEngine`. Considérez-le comme allumer un scanner prêt à lire votre image.

```python
import ocr

# Initialise the OCR engine – this is where all the magic begins
engine = ocr.OcrEngine()
```

> **Pourquoi c'est important :** Instancier le moteur alloue des tampons internes et charge les données de langue. Sauter cette étape provoquera une erreur `NoneType` plus tard lorsque vous essayerez de définir l'image.

### Étape 2 : Charger l'image que vous souhaitez convertir

Ensuite, nous alimentons le moteur avec un flux d'image. L'utilitaire `ImageStream.from_file` lit le fichier et le place dans un format compris par le moteur OCR.

```python
# Load the source image – replace the path with your own file
image_path = "YOUR_DIRECTORY/contract.jpg"
engine.set_image(ocr.ImageStream.from_file(image_path))
```

> **Cas particulier :** Si votre source est un TIFF multi‑pages, utilisez `ocr.MultiPageImageStream.from_file` à la place. Le moteur traitera chaque page comme une page PDF distincte automatiquement.

### Étape 3 : Indiquer au moteur de produire un PDF consultable

Par défaut, de nombreux SDK OCR produisent du texte brut. Nous devons changer le format de sortie en PDF afin que le fichier résultant soit à la fois visuel et consultable.

```python
# Configure the engine to produce a searchable PDF
engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
```

> **Que se passe-t-il en coulisses ?** Le moteur intègre maintenant une couche de texte invisible derrière le bitmap, vous permettant de rechercher des mots comme dans un PDF natif.

### Étape 4 : Préparer un flux en mémoire pour les données PDF

Au lieu d'écrire directement sur le disque, nous capturons le PDF dans un `MemoryStream`. Cela maintient les E/S rapides et vous permet de transmettre les octets ailleurs (par ex., télécharger sur S3) si vous le souhaitez.

```python
# Create a memory buffer that will receive the PDF bytes
pdf_stream = ocr.MemoryStream()
```

### Étape 5 : Exécuter la reconnaissance et écrire le PDF

Maintenant, le travail lourd s'effectue. L'appel `recognize` lit l'image, exécute l'OCR et diffuse le PDF consultable dans `pdf_stream`.

```python
# Perform OCR and write the searchable PDF into the memory stream
engine.recognize(pdf_stream)
```

> **Erreur fréquente :** Oublier d'appeler `engine.recognize` laissera `pdf_stream` vide, et tenter de l'enregistrer déclenchera une `ValueError`. Vérifiez toujours `pdf_stream.length` si vous devez confirmer que des données ont été produites.

### Étape 6 : Enregistrer le PDF généré dans un fichier

Enfin, nous vidons les octets du flux mémoire sur le disque. Le fichier résultant peut être ouvert dans Adobe Reader, Preview ou tout visualiseur PDF avec recherche de texte intégrale.

```python
output_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Write the PDF bytes to a file
with open(output_path, "wb") as f:
    f.write(pdf_stream.to_bytes())
print(f"✅ Searchable PDF saved to {output_path}")
```

> **Résultat attendu :** Ouvrez le PDF, appuyez sur `Ctrl+F`, tapez un mot qui apparaît dans le scan original, et voyez le visualiseur le mettre en surbrillance instantanément. C’est la caractéristique d'un **PDF consultable**.

---

## Convertir une image en PDF – Ajuster les paramètres pour de meilleurs résultats

Si votre objectif principal est simplement de **convertir une image en PDF** sans OCR, vous pouvez sauter l'étape 3 et définir le format de sortie sur `ocr.OutputFormat.IMAGE_PDF`. Le moteur intégrera le bitmap comme une page PDF sans couche de texte cachée.

```python
engine.get_settings().set_output_format(ocr.OutputFormat.IMAGE_PDF)
```

Utilisez ce mode lorsque vous avez besoin d'une réplique visuelle fidèle mais que la recherchabilité n'est pas nécessaire—peut-être pour l'archivage où l'OCR n'est pas requis.

---

## Reconnaître le texte PDF – Ajout de packs de langue et contrôle du DPI

Pour une expérience robuste de **recognize text PDF**, envisagez les ajustements optionnels suivants :

```python
settings = engine.get_settings()
settings.set_language("eng+spa")          # English + Spanish support
settings.set_dpi(300)                     # Higher DPI improves accuracy
settings.enable_auto_rotate(True)         # Auto‑rotate skewed scans
```

> **Pourquoi ajuster le DPI ?** Une résolution plus élevée fournit au moteur OCR plus de pixels à analyser, réduisant les erreurs de reconnaissance sur des scans de mauvaise qualité.

---

## PDF OCR Python – Intégration dans des pipelines plus larges

Maintenant que vous pouvez **python ocr pdf** en quelques lignes, imaginez intégrer cette logique dans une API Flask :

```python
from flask import Flask, request, send_file
import io, ocr

app = Flask(__name__)

@app.route("/upload", methods=["POST"])
def upload():
    file = request.files["image"]
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_bytes(file.read()))
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)
    pdf_stream = ocr.MemoryStream()
    engine.recognize(pdf_stream)

    return send_file(
        io.BytesIO(pdf_stream.to_bytes()),
        mimetype="application/pdf",
        as_attachment=True,
        download_name="searchable.pdf"
    )
```

Ce petit point de terminaison permet à un client d'envoyer (POST) une image et de recevoir instantanément un **PDF consultable**—parfait pour les services SaaS de traitement de documents.

---

## Pièges courants lorsque vous **ocr image to pdf**

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Pages PDF vides | Image non chargée (`engine.set_image` appelé avec un mauvais chemin) | Vérifiez le chemin et utilisez `os.path.abspath` |
| Pas de texte consultable | Output format still set to `IMAGE_PDF` | Appelez explicitement `set_output_format(ocr.OutputFormat.PDF)` |
| Caractères illisibles | Wrong language pack | Chargez la bonne langue avec `settings.set_language("eng")` |
| Traitement lent sur de gros fichiers | Using default DPI (72) on high‑resolution images | Augmentez le DPI à 300 ou traitez les pages par lots individuellement |

---

## Exemple complet, exécutable (prêt à copier‑coller)

```python
import ocr

def create_searchable_pdf(image_path: str, output_path: str) -> None:
    """
    Convert a scanned image to a searchable PDF using the ocr SDK.
    """
    # 1️⃣ Initialise engine
    engine = ocr.OcrEngine()

    # 2️⃣ Load image
    engine.set_image(ocr.ImageStream.from_file(image_path))

    # 3️⃣ Set output to searchable PDF
    engine.get_settings().set_output_format(ocr.OutputFormat.PDF)

    # Optional: improve accuracy
    settings = engine.get_settings()
    settings.set_language("eng")   # adjust as needed
    settings.set_dpi(300)

    # 4️⃣ Prepare in‑memory stream
    pdf_stream = ocr.MemoryStream()

    # 5️⃣ Run OCR
    engine.recognize(pdf_stream)

    # 6️⃣ Persist PDF
    with open(output_path, "wb") as f:
        f.write(pdf_stream.to_bytes())
    print(f"✅ Searchable PDF created at: {output_path}")

if __name__ == "__main__":
    create_searchable_pdf(
        image_path="YOUR_DIRECTORY/contract.jpg",
        output_path="YOUR_DIRECTORY/contract_searchable.pdf"
    )
```

Exécutez le script, ouvrez le PDF généré, et essayez de rechercher un mot que vous savez présent dans le scan original. Si tout s'est bien passé, vous avez maîtrisé **create searchable pdf** avec Python.

---

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **create searchable PDF** avec une bibliothèque OCR Python : initialiser le moteur, charger une image, configurer la sortie PDF, diffuser le résultat, et enfin l'enregistrer sur le disque. Vous avez également vu comment **convertir une image en PDF**, affiner **

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}