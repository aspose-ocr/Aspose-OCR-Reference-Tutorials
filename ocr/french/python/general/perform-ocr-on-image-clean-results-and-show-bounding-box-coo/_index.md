---
category: general
date: 2026-03-28
description: Effectuer une OCR sur l'image et obtenir du texte propre avec les coordonnées
  des boîtes englobantes. Apprenez comment extraire l'OCR, nettoyer l'OCR et afficher
  les résultats étape par étape.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: fr
og_description: Effectuer la reconnaissance optique de caractères sur une image, nettoyer
  le résultat et afficher les coordonnées des boîtes englobantes dans un tutoriel
  concis.
og_title: Effectuer une OCR sur l'image – Résultats propres et boîtes englobantes
tags:
- OCR
- Computer Vision
- Python
title: Effectuer l'OCR sur une image – Nettoyer les résultats et afficher les coordonnées
  des boîtes englobantes
url: /fr/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image – Nettoyer les résultats et afficher les coordonnées des boîtes englobantes

Vous avez déjà eu besoin d'**effectuer une OCR sur des fichiers image** mais vous obteniez du texte désordonné sans savoir où chaque mot se situe sur l'image ? Vous n'êtes pas seul. Dans de nombreux projets—numérisation de factures, scan de reçus ou extraction de texte simple—obtenir la sortie brute d'une OCR n'est que le premier obstacle. Bonne nouvelle : vous pouvez nettoyer cette sortie et voir instantanément les coordonnées de la boîte englobante de chaque région sans écrire une tonne de code boilerplate.

Dans ce guide, nous allons parcourir **comment extraire l'OCR**, exécuter un **post‑processus de nettoyage d'OCR**, puis **afficher les coordonnées des boîtes englobantes** pour chaque région nettoyée. À la fin, vous disposerez d'un script unique, exécutable, qui transforme une photo floue en texte structuré et propre, prêt pour le traitement en aval.

## Ce dont vous avez besoin

- Python 3.9+ (la syntaxe ci‑dessous fonctionne sur 3.8 et versions ultérieures)
- Un moteur OCR qui supporte `recognize(..., return_structured=True)` – par exemple, une bibliothèque fictive `engine` utilisée dans l'exemple. Remplacez‑la par Tesseract, EasyOCR ou tout SDK qui renvoie des données de région.
- Une connaissance de base des fonctions et boucles Python
- Un fichier image que vous souhaitez analyser (PNG, JPG, etc.)

> **Astuce :** Si vous utilisez Tesseract, la fonction `pytesseract.image_to_data` vous fournit déjà les boîtes englobantes. Vous pouvez envelopper son résultat dans un petit adaptateur qui imite l'API `engine.recognize` montrée ci‑dessous.

---

![perform OCR on image example](image-placeholder.png "exemple d'exécution d'OCR sur une image")

*Texte alternatif : diagramme montrant comment effectuer une OCR sur une image et visualiser les coordonnées des boîtes englobantes*

## Étape 1 – Effectuer une OCR sur l'image et obtenir les régions structurées

La première chose à faire est de demander au moteur OCR de renvoyer non seulement du texte brut mais une liste structurée de régions de texte. Cette liste contient la chaîne brute et le rectangle qui l'englobe.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Pourquoi c'est important :**  
Lorsque vous ne demandez que du texte brut, vous perdez le contexte spatial. Les données structurées vous permettent ensuite **d'afficher les coordonnées des boîtes englobantes**, d'aligner le texte avec des tableaux ou d'alimenter des modèles en aval avec des emplacements précis.

## Étape 2 – Comment nettoyer la sortie OCR avec un post‑processus

Les moteurs OCR sont excellents pour repérer les caractères, mais ils laissent souvent des espaces superflus, des artefacts de retour à la ligne ou des symboles mal reconnus. Un post‑processus normalise le texte, corrige les erreurs OCR courantes et supprime les espaces inutiles.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Si vous créez votre propre nettoyeur, pensez à :

- Supprimer les caractères non‑ASCII (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Réduire plusieurs espaces à un seul espace
- Appliquer un correcteur orthographique comme `pyspellchecker` pour les fautes évidentes

**Pourquoi cela compte :**  
Une chaîne propre rend la recherche, l'indexation et les pipelines NLP en aval beaucoup plus fiables. En d'autres termes, **comment nettoyer l'OCR** est souvent la différence entre un jeu de données exploitable et un cauchemar.

## Étape 3 – Afficher les coordonnées des boîtes englobantes pour chaque région nettoyée

Maintenant que le texte est propre, nous parcourons chaque région, affichant son rectangle et la chaîne nettoyée. C'est la partie où nous **affichons enfin les coordonnées des boîtes englobantes**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Exemple de sortie**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Vous pouvez maintenant injecter ces coordonnées dans une bibliothèque de dessin (par ex., OpenCV) pour superposer des boîtes sur l'image originale, ou les stocker dans une base de données pour des requêtes ultérieures.

## Script complet, prêt à l'exécution

Voici le programme complet qui réunit les trois étapes. Remplacez les appels fictifs `engine` par votre SDK OCR réel.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Comment l'exécuter

```bash
python perform_ocr.py sample_invoice.jpg
```

Vous devriez voir une liste de boîtes englobantes associées à du texte nettoyé, exactement comme l'exemple de sortie ci‑dessus.

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|---------|
| **Et si le moteur OCR ne supporte pas `return_structured` ?** | Écrivez un petit wrapper qui convertit la sortie brute du moteur (généralement une liste de mots avec coordonnées) en objets possédant les attributs `text` et `bounding_box`. |
| **Puis‑je obtenir des scores de confiance ?** | De nombreux SDK exposent une métrique de confiance par région. Ajoutez‑la à l'instruction d'affichage : `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Comment gérer du texte tourné ?** | Pré‑traitez l'image avec `cv2.minAreaRect` d'OpenCV pour la redresser avant d'appeler `recognize`. |
| **Et si j'ai besoin du résultat en JSON ?** | Sérialisez `processed_result.regions` avec `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Existe‑t‑il un moyen de visualiser les boîtes ?** | Utilisez OpenCV : `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` dans la boucle, puis `cv2.imwrite("annotated.jpg", img)`. |

## Conclusion

Vous venez d'apprendre **comment effectuer une OCR sur une image**, nettoyer la sortie brute, et **afficher les coordonnées des boîtes englobantes** pour chaque région. Le flux en trois étapes—reconnaître → post‑processer → itérer—est un modèle réutilisable que vous pouvez intégrer à n'importe quel projet Python nécessitant une extraction de texte fiable.

### Et après ?

- **Explorez différents back‑ends OCR** (Tesseract, EasyOCR, Google Vision) et comparez leur précision.  
- **Intégrez une base de données** pour stocker les données de région et créer des archives consultables.  
- **Ajoutez la détection de langue** afin de diriger chaque région vers le correcteur orthographique approprié.  
- **Superposez les boîtes sur l'image originale** pour une vérification visuelle (voir le snippet OpenCV ci‑dessus).

Si vous rencontrez des particularités, souvenez‑vous que le plus grand gain provient d'une étape de post‑traitement solide ; une chaîne propre est bien plus facile à manipuler qu'un dump brut de caractères.

Bon codage, et que vos pipelines OCR restent toujours impeccables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}