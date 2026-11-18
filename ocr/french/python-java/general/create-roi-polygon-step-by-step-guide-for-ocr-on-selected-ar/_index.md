---
category: general
date: 2026-03-26
description: Créez un polygone de ROI pour exécuter l'OCR sur la zone sélectionnée.
  Apprenez à définir plusieurs régions, les enregistrer et extraire le texte avec
  un moteur OCR Python.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: fr
og_description: Créer un polygone de zone d'intérêt et exécuter l'OCR sur la zone
  sélectionnée avec un moteur Python. Code complet, explications et astuces inclus.
og_title: Créer un polygone ROI – OCR rapide sur la zone sélectionnée
tags:
- OCR
- Python
- Image Processing
title: Créer un polygone ROI – Guide étape par étape pour l’OCR sur la zone sélectionnée
url: /fr/python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un polygone ROI – Tutoriel complet pour l'OCR sur zone sélectionnée

Vous avez déjà eu besoin de **créer un polygone ROI** afin de lancer l'OCR uniquement sur la partie d'une image qui compte ? Peut‑être scannez‑vous des reçus et seuls les totaux vous intéressent, ou vous avez un formulaire où seul le champ de signature doit être lu. Dans ces cas, **ocr on selected area** fait gagner du temps et améliore la précision.  

Dans ce guide, nous passerons en revue tout ce dont vous avez besoin : de la définition de deux polygones, à leur enregistrement auprès d’un moteur OCR, jusqu’à l’extraction du texte reconnu en un seul appel propre. À la fin, vous disposerez d’un script prêt à l’emploi et d’une compréhension solide de l’importance de se concentrer sur les régions d’intérêt.

## Ce que vous allez apprendre

- Comment **créer des objets ROI polygon** en utilisant une bibliothèque OCR typique.
- La différence entre la définition d’une seule région et de plusieurs.
- Comment enregistrer ces régions auprès du moteur afin que `ocr on selected area` soit exécuté.
- Le résultat attendu et comment dépanner les problèmes courants (par ex., ROI qui se chevauchent, résultats vides).

### Prérequis

- Python 3.8+ installé.
- Une bibliothèque OCR qui expose les méthodes `Polygon`, `Point` et `add_region_of_interest` (l’exemple utilise un module fictif `ocr` ; remplacez‑le par votre SDK réel, comme les wrappers Tesseract‑Python ou EasyOCR).
- Un fichier image d’exemple (`sample.png`) contenant du texte aux coordonnées indiquées ci‑dessous.

> **Pro tip :** Si vous utilisez une bibliothèque réelle, assurez‑vous que l’image est chargée dans le même espace de coordonnées (origine en haut‑à‑gauche, X augmente vers la droite, Y augmente vers le bas).  

---  

## Étape 1 : Importer le module OCR et charger votre image  

Tout d’abord, importez le package OCR dans votre espace de travail et lisez l’image que vous souhaitez traiter.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Pourquoi c’est important :* Le moteur a besoin des données d’image avant que vous puissiez y attacher un **polygone ROI**. Certaines bibliothèques permettent également de passer l’image plus tard, mais une initialisation précoce rend le flux de travail plus propre.

## Étape 2 : Définir le premier polygone ROI  

Nous créons maintenant la première région d’intérêt. Pensez à cela comme dessiner un rectangle autour de l’en‑tête d’un tableau.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Explication :*  
- `ocr.Point(x, y)` utilise des coordonnées en pixels.  
- La liste des points est ordonnée dans le sens des aiguilles d’une montre, ce que la plupart des moteurs attendent.  
- Vous pouvez ajouter autant de points que vous le souhaitez pour créer des formes irrégulières ; un rectangle n’est qu’un cas particulier.

## Étape 3 : Définir des polygones ROI supplémentaires (optionnel)  

Vous n’avez pas besoin de vous arrêter à un seul. Voici un deuxième polygone qui capture un champ de signature plus bas sur la page.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Pourquoi en ajouter davantage ?* Exécuter **ocr on selected area** pour plusieurs zones vous permet d’extraire des morceaux de données disparates en un seul passage, ce qui est bien plus rapide que de recadrer et de traiter chaque tranche séparément.

## Étape 4 : Enregistrer les ROI auprès du moteur OCR  

Avec les polygones prêts, indiquez au moteur quelles zones inspecter.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Note importante :* Certains SDK exigent d’appeler une méthode `clear_regions()` avant d’ajouter de nouvelles régions si vous réutilisez le moteur pour une autre image.

## Étape 5 : Exécuter l’OCR et récupérer le texte  

Enfin, lancez la reconnaissance. Le moteur ne regardera qu’à l’intérieur des polygones que nous venons d’ajouter.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Résultat attendu** (en supposant que `sample.png` contienne les mots « Invoice Total: $123.45 » dans le premier ROI et « Signature: John Doe » dans le second) :

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

Si la sortie est vide, revérifiez que les coordonnées intersectent réellement du texte et que la résolution de l’image correspond au système de coordonnées.

## Cas limites et problèmes courants  

| Situation                               | À surveiller                                      | Correction / Solution                              |
|----------------------------------------|---------------------------------------------------|-----------------------------------------------------|
| **ROI qui se chevauchent**             | Le texte peut être renvoyé deux fois.            | Gardez les polygones disjoints ou dédupliquez la sortie. |
| **ROI hors des limites de l’image**    | Le moteur peut lever une erreur ou ne rien retourner. | Limitez les coordonnées à `0 ≤ x < width`, `0 ≤ y < height`. |
| **ROI très petit**                     | La précision de l’OCR diminue à cause d’un nombre insuffisant de pixels. | Agrandissez le polygone de quelques pixels ou augmentez d’abord la résolution de l’image. |
| **Forme non rectangulaire**            | Certains moteurs ne supportent que les polygones convexes. | Divisez les formes complexes en plusieurs ROI convexes. |
| **Changement de taille d’image**       | Les coordonnées codées en dur deviennent invalides. | Calculez les coordonnées ROI en fonction des dimensions de l’image (par ex., en pourcentage). |

## Exemple complet fonctionnel  

Voici le script complet que vous pouvez copier‑coller et exécuter (remplacez `ocr` par votre bibliothèque réelle).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Exécutez‑le avec `python ocr_roi_example.py` et vous devriez voir les chaînes extraites des deux zones définies.

## Prochaines étapes  

- **Génération dynamique de ROI :** Au lieu de coder en dur les coordonnées, utilisez le traitement d’image (par ex., détection de contours avec OpenCV) pour localiser automatiquement les tableaux ou champs.  
- **Post‑traitement :** Supprimez les espaces blancs, appliquez des expressions régulières, ou convertissez les nombres en types de données appropriés.  
- **Traitement par lots :** Parcourez un dossier d’images, en réutilisant les mêmes définitions de ROI si la mise en page est cohérente.  

Si vous êtes curieux au sujet de **ocr on selected area** pour des documents plus complexes—pensez aux PDF multi‑pages ou aux formulaires scannés—explorez les bibliothèques qui supportent l’enregistrement de ROI page par page.  

---  

### Aperçu visuel  

![Diagramme montrant deux polygones ROI sur une image d'exemple](roi_diagram.png){alt="exemple de création de polygone ROI montrant deux zones sélectionnées"}

Le diagramme illustre comment les deux rectangles (bleu et vert) se superposent à l’image sous‑jacente, mettant en évidence exactement ce que le moteur OCR lira.

---  

## Conclusion  

Nous venons **de créer des objets ROI polygon**, de les avoir enregistrés auprès d’un moteur OCR, et d’avoir exécuté `ocr on selected area` dans un script propre et reproductible. En limitant le moteur aux zones qui vous intéressent, vous réduisez le temps de traitement, améliorez la précision et simplifiez grandement la manipulation des données en aval.  

Testez‑le avec vos propres images — ajustez les coordonnées, ajoutez d’autres polygones, ou connectez la sortie à une base de données. Le ciel est la limite une fois que vous maîtrisez l’OCR basé sur les régions.  

Des questions ou un cas d’usage intéressant à partager ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}