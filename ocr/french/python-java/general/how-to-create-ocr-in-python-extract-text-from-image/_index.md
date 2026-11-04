---
category: general
date: 2026-04-26
description: Comment créer de l'OCR rapidement et de manière fiable. Apprenez à extraire
  du texte d'une image, à charger une image pour l'OCR, et à exécuter l'OCR sur un
  PNG avec un dictionnaire personnalisé.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: fr
og_description: Comment créer un OCR en Python et extraire du texte d’une image. Ce
  guide montre comment charger une image pour l’OCR, exécuter l’OCR sur un PNG et
  utiliser un dictionnaire personnalisé.
og_title: Comment créer un OCR en Python – Extraction rapide de texte
tags:
- OCR
- Python
- Image Processing
title: Comment créer un OCR en Python – Extraire le texte d’une image
url: /fr/python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un OCR en Python – Guide étape par étape

Vous vous êtes déjà demandé **comment créer un OCR** capable de lire vos PDFs numérisés, captures d'écran ou notes manuscrites ? Vous n'êtes pas seul. Dans de nombreux projets réels, nous devons *extraire du texte à partir de fichiers image*, mais les moteurs prêts à l'emploi peinent souvent avec les mots spécifiques à un domaine.  

Dans ce tutoriel, vous verrez un exemple complet et exécutable qui charge une image pour l'OCR, applique un dictionnaire personnalisé, et enfin **exécute l'OCR sur des fichiers PNG**. À la fin, vous pourrez extraire du texte de n'importe quelle image et adapter le moteur à votre propre terminologie.

## Ce que couvre ce tutoriel

* Installer le petit mais puissant paquet `aocr` (ou toute bibliothèque compatible).  
* Configurer un **dictionnaire personnalisé** afin que des termes comme `aspocorp` ou `licensekey` soient reconnus.  
* **Charger une image pour l'OCR**, qu'il s'agisse d'un PNG, JPEG ou d'une page PDF numérisée.  
* Exécuter le processus OCR et afficher le résultat.  

Pas de liens vers une documentation externe, juste une solution autonome que vous pouvez copier‑coller et exécuter dès aujourd'hui.

### Prérequis

* Python 3.8 ou plus récent (le code utilise les f‑strings).  
* Familiarité de base avec la ligne de commande – vous taperez quelques commandes `pip install`.  
* Un fichier image (`technical_doc.png` dans l'exemple) placé quelque part où vous pouvez le référencer.  

Si vous remplissez ces trois critères, vous êtes prêt à y aller.  

---

## Étape 1 : Installer la bibliothèque OCR

Tout d'abord, nous avons besoin d'un moteur OCR qui prend en charge un objet de configuration programmable. Le paquet `aocr` est une couche légère autour d'un moteur OCR natif et fonctionne bien pour les démonstrations.

```bash
# Install the library (run once)
pip install aocr
```

> **Astuce :** Si vous êtes sous Windows et rencontrez une erreur de compilation, essayez `pip install aocr‑binary` qui fournit des roues pré‑compilées.

### Pourquoi installer cette bibliothèque ?

`aocr` nous donne un accès direct à un objet `config` où nous pouvons injecter un **dictionnaire personnalisé**. C’est l’ingrédient secret pour améliorer la précision sur des vocabulaires spécialisés.

---

## Étape 2 : Créer l'instance du moteur OCR et ajouter un dictionnaire personnalisé

Nous lançons maintenant le moteur et lui indiquons quels mots il doit considérer comme connus.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Pourquoi un dictionnaire personnalisé est important

Les modèles OCR standards sont entraînés sur des corpus génériques. Lorsque le modèle voit « aspocorp », il peut le découper en « aspo corp » ou supprimer des lettres complètement. En fournissant une liste personnalisée, nous orientons le reconnaisseur vers l'orthographe exacte dont nous avons besoin, réduisant ainsi de façon spectaculaire le travail de post‑traitement.

---

## Étape 3 : Charger l'image que vous souhaitez traiter

C’est ici que nous **chargeons l'image pour l'OCR**. La méthode `Image.load` accepte une chaîne de chemin et détermine automatiquement le type de fichier.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Cas particulier :** Si votre source est un PDF multi‑pages, convertissez chaque page en PNG d'abord (par ex., avec `pdf2image`) et alimentez‑les une à une dans le moteur.

### Conseils pour une meilleure qualité d'image

* Conservez une résolution d'au moins 300 dpi.  
* Assurez‑vous que l'image est droite ; faites une rotation avec `Pillow` si nécessaire.  
* Convertissez les scans en couleur en niveaux de gris pour réduire le bruit.

---

## Étape 4 : Exécuter le processus OCR sur le fichier PNG

Avec le moteur configuré et l'image chargée, nous **exécutons enfin l'OCR sur le PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

L'appel `process()` renvoie un objet contenant le texte reconnu, les scores de confiance et les boîtes englobantes pour chaque mot.

---

## Étape 5 : Afficher le texte reconnu

Le moyen le plus simple de voir ce que le moteur a trouvé est d'imprimer l'attribut `text`.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Résultat attendu

Si `technical_doc.png` contient la phrase *« The Aspocorp licensekey expires on 2025‑12‑31. »*, la console devrait afficher :

```
The Aspocorp licensekey expires on 2025-12-31.
```

Remarquez comment le dictionnaire personnalisé a conservé le nom de la marque intact—ce qu'un OCR standard aurait pu déformer.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le script complet, prêt à être enregistré sous `run_ocr.py`. Remplacez simplement le chemin factice par l'emplacement de votre image.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Exécutez‑le depuis le terminal :

```bash
python run_ocr.py
```

Vous devriez voir le texte extrait affiché dans la console, exactement comme dans l'exemple précédent.

---

## Questions fréquentes (FAQ)

| Question | Réponse |
|----------|--------|
| **Puis-je extraire du texte d'un PDF numérisé ?** | Oui. Convertissez chaque page en PNG (ou TIFF) d'abord, puis alimentez les images au même script. |
| **Et si mon image est un JPEG au lieu d'un PNG ?** | La méthode `Image.load` prend en charge JPEG, BMP, TIFF et PNG nativement. Changez simplement l'extension du fichier. |
| **Comment améliorer la précision sur des scans à faible contraste ?** | Pré‑traitez avec `Pillow` – augmentez le contraste, appliquez une binarisation, ou utilisez `opencv` pour redresser. |
| **Existe‑t‑il un moyen d'obtenir les scores de confiance pour chaque mot ?** | `ocr_result` inclut `words` – chaque mot possède un attribut `confidence` que vous pouvez parcourir. |
| **Puis‑je exécuter cela sur un serveur sans interface graphique ?** | Absolument. `aocr` n'a aucune dépendance GUI, ce qui le rend parfait pour les pipelines CI. |

---

## Prochaines étapes et sujets connexes

Maintenant que vous savez **comment créer un OCR** et **extraire du texte à partir de fichiers image**, envisagez d'explorer :

* **Techniques de pré‑traitement** – `load image for OCR` n'est que la première étape ; utilisez `opencv` pour débruiter ou affûter.  
* **Traitement par lots** – parcourez un répertoire de PNG pour générer une archive consultable.  
* **Support multilingue** – ajoutez des packs de langues au moteur si vous devez lire des documents en français ou en allemand.  
* **Intégration avec Elasticsearch** – indexez le texte extrait pour une recherche en texte intégral à travers les ressources numérisées.  

Chacune de ces extensions s'appuie sur le modèle de base que nous venons de couvrir, vous trouverez donc la transition sans effort.

---

## Conclusion

En quelques minutes, nous avons répondu à la question **comment créer un OCR** qui extrait de manière fiable le **texte à partir de fichiers image**, en particulier les PNG, et nous vous avons montré comment **charger une image pour l'OCR**, appliquer un **dictionnaire personnalisé**, et **exécuter l'OCR sur PNG** sans aucun service externe.  

Lancez le script, ajustez le dictionnaire pour correspondre à votre propre jargon, et vous disposerez d'une base solide pour tout projet de numérisation de documents.  

Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—nous serons heureux d'aider. Et n'oubliez pas de partager vos réussites ; la communauté apprend le mieux des exemples concrets.  

**Prêt à automatiser votre paperasse ?** Prenez le code, adaptez‑le, et commencez dès aujourd'hui à transformer les pixels en texte consultable !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}