---
category: general
date: 2026-06-25
description: Comment utiliser l’OCR en Python – apprenez à charger une image pour
  l’OCR, à reconnaître le texte dans une région et à extraire rapidement le texte
  de cette région.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: fr
og_description: Comment utiliser l'OCR en Python – guide étape par étape pour charger
  une image, reconnaître le texte dans une région spécifique et extraire le numéro
  de facture.
og_title: 'Comment utiliser OCR Python : charger une image et extraire le texte d’une
  région'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Comment utiliser OCR Python : charger une image et extraire le texte d’une
  région'
url: /fr/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser OCR Python : charger une image et extraire le texte d’une région

**How to use OCR in Python** est plus simple que vous ne le pensez. Vous êtes-vous déjà retrouvé devant une facture numérisée en vous demandant comment extraire uniquement le numéro de facture sans analyser toute la page ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils s’initient à la reconnaissance optique de caractères. Dans ce guide, nous verrons comment charger une image pour l’OCR, définir un rectangle, reconnaître le texte dans cette zone, puis extraire le texte de la région. À la fin, vous disposerez d’un script prêt à l’emploi qui isole n’importe quel morceau de texte dont vous avez besoin.

> *Astuce :* Si vous travaillez avec des PDF, convertissez chaque page en image d’abord — la plupart des bibliothèques OCR gèrent le mieux le PNG/JPEG.

## Ce dont vous aurez besoin

- Python 3.8+ (la dernière version stable est recommandée)  
- Une bibliothèque OCR qui expose une classe `OcrEngine` (par ex., **ocr** depuis `pip install ocr-lib`)  
- Une image d’exemple — ici nous utiliserons `invoice.png` placé dans un dossier que vous contrôlez  
- Une connaissance de base des rectangles (x, y, largeur, hauteur)  

Aucune dépendance lourde, aucun GPU requis — seulement du CPU pur, ce qui rend le tout portable.

---

## Comment utiliser OCR : initialiser le moteur (Étape 1)

Avant de pouvoir lire du texte, vous avez besoin d’une instance du moteur OCR. Pensez‑y comme le cerveau qui analysera les motifs de pixels.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Pourquoi c’est important :* L’initialisation du moteur charge les modèles linguistiques et définit les configurations par défaut. Ignorer cette étape lèverait une exception dès l’appel à `recognize_region`.

---

## Charger l’image pour l’OCR (Étape 2)

Une fois le moteur prêt, nous lui fournissons une image. La méthode `Image.load` de la bibliothèque gère les formats courants et normalise le bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Si le fichier n’est pas trouvé, Python lèvera une `FileNotFoundError`. Assurez‑vous que le chemin soit absolu ou relatif au répertoire de travail de votre script.  

*Cas particulier :* Certaines implémentations OCR attendent une image en niveaux de gris. Si vous constatez une mauvaise précision, convertissez d’abord l’image :

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Reconnaître le texte dans une région (Étape 3)

Définir la région, c’est indiquer au moteur *où* regarder. La classe `Rectangle` accepte des valeurs à virgule flottante pour une précision sous‑pixel, ce qui peut être pratique avec des scans haute résolution.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – coin supérieur gauche du rectangle (en pixels)  
- **width, height** – taille du rectangle  

Vous vous demandez peut‑être comment obtenir ces nombres. La méthode la plus rapide consiste à ouvrir l’image dans n’importe quel éditeur (par ex., GIMP ou Paint.NET) et à utiliser l’outil de sélection pour lire les coordonnées.  

*Pourquoi ne pas simplement OCRiser toute la page ?* Limiter la zone réduit le bruit, accélère le traitement et améliore considérablement la précision pour de petits champs comme les numéros de facture.

---

## Extraire le texte de la région (Étape 4)

Une fois la région définie, demandez au moteur de reconnaître uniquement cette tranche. L’objet résultat contient le texte brut et les scores de confiance.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Si le moteur OCR prend en charge plusieurs langues, vous pouvez fournir un code de langue optionnel :

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Erreur fréquente :* Certains moteurs renvoient une liste de mots au lieu d’une chaîne unique. Dans ce cas, concaténez‑les :

```python
text = " ".join(region_result.words)
```

---

## Afficher le numéro de facture extrait (Étape 5)

Enfin, imprimez — ou stockez — le texte extrait. Vous pouvez également post‑traiter la chaîne pour supprimer les espaces superflus ou les caractères non numériques.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Lancer le script avec un rectangle correctement aligné devrait produire quelque chose comme :

```
Invoice number: 20231578
```

Si vous obtenez des caractères illisibles, revérifiez les coordonnées du rectangle ou envisagez d’augmenter la résolution de l’image.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici un script autonome que vous pouvez copier‑coller et exécuter :

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Enregistrez le fichier sous le nom `extract_invoice.py`, remplacez `YOUR_DIRECTORY` par le chemin réel du dossier, puis lancez :

```bash
python extract_invoice.py
```

Vous devriez voir le numéro de facture affiché dans la console.

---

## Questions fréquentes

**Q : Et si le numéro de facture est imprimé avec une police fantaisiste ?**  
R : La plupart des moteurs OCR modernes gèrent une large gamme de polices, mais vous pouvez améliorer la précision en entraînant un modèle linguistique personnalisé ou en pré‑traitant l’image (par ex., en appliquant un filtre de seuillage).

**Q : Puis‑je extraire plusieurs champs en même temps ?**  
R : Bien sûr. Créez une liste d’objets `Rectangle` — un par champ — et parcourez‑la, en stockant chaque résultat dans un dictionnaire.

**Q : Cela fonctionne‑t‑il sur des PDF multi‑pages ?**  
R : Convertissez chaque page en image d’abord (avec `pdf2image` ou un outil similaire), puis appliquez la même extraction basée sur la région page par page.

---

## Conclusion

Dans ce tutoriel, nous avons vu **comment utiliser OCR** en Python pour charger une image, reconnaître du texte dans une région précise et extraire le texte de cette zone — idéal pour récupérer des numéros de facture, des identifiants de commande ou tout petit fragment de données à partir de documents numérisés. En isolant la zone d’intérêt, vous gagnez en rapidité, en précision et vous réduisez les besoins de post‑traitement.

Prêt pour l’étape suivante ? Essayez d’étendre le script pour **charger des images pour OCR** depuis un dossier contenant plusieurs factures, ou expérimentez **reconnaître du texte dans une région** pour d’autres champs comme les dates et les totaux. Le même schéma s’applique — il suffit de modifier les coordonnées du rectangle.

Si vous avez rencontré des difficultés ou avez des idées d’amélioration, laissez un commentaire ci‑dessous. Bon codage, et que vos pipelines OCR soient toujours précis !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}