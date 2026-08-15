---
category: general
date: 2026-03-28
description: Comment faire de l'OCR sur une ROI en Python – Apprenez à définir les
  options de prétraitement pour une extraction précise du texte à partir de régions
  d'image spécifiques.
draft: false
keywords:
- how to OCR ROI
- how to set preprocessing
- Aspose OCR Python
- ROI extraction
- image preprocessing OCR
language: fr
og_description: Comment réaliser l'OCR d'une ROI en Python – Ce guide montre comment
  configurer le prétraitement pour une extraction fiable du texte à partir de régions
  d'image définies.
og_title: Comment faire de l’OCR d’une ROI en Python – Comment définir le prétraitement
tags:
- OCR
- Python
- Aspose
title: Comment faire de l’OCR d’une ROI en Python – Comment définir le prétraitement
url: /fr/python-java/general/how-to-ocr-roi-in-python-how-to-set-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR sur une ROI en Python – Comment définir le prétraitement

Vous vous êtes déjà demandé **comment faire de l'OCR sur une ROI** dans une image de facture bruitée sans charger toute la page en mémoire ? Vous n'êtes pas le seul. Dans de nombreux projets réels, nous n'avons besoin que de quelques champs — nom du client, adresse, totaux — donc scanner le document entier est excessif.  

Bonne nouvelle ? Avec Aspose OCR, vous pouvez indiquer au moteur **où chercher** et même lui demander de nettoyer l'image au préalable. Dans ce tutoriel, nous allons parcourir **comment définir les options de prétraitement**, définir les Regions of Interest (ROIs) et extraire du texte propre en quelques lignes de Python.

À la fin de ce guide, vous disposerez d’un script prêt à l’emploi qui extrait des blocs spécifiques de n’importe quelle facture, reçu ou formulaire. Aucun outil supplémentaire requis, juste Aspose OCR et un peu de logique Python.

---

## Ce dont vous aurez besoin

- **Python 3.8+** (le code fonctionne avec n’importe quelle version récente)  
- **Aspose OCR for Python via .NET** – installez-le avec `pip install aspose-ocr`  
- Une image d’exemple (par ex., `invoice.png`) placée dans un dossier que vous pouvez référencer  
- Une connaissance de base des fonctions Python et de la syntaxe orientée objet  

Si vous avez déjà tout cela, super — passons directement au code.

---

![Diagramme comment faire de l'OCR sur une ROI](ocr-roi.png "Exemple de comment faire de l'OCR sur une ROI")

*Texte alternatif : diagramme montrant les boîtes de ROI sur une image de facture*

---

## Étape 1 – Initialiser le moteur OCR (Comment faire de l'OCR sur une ROI)

Avant de pouvoir dire au moteur *où* chercher, nous avons besoin d’une instance du processeur OCR. Cet objet contient toute la configuration et exécute le passage de reconnaissance.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the engine – this is the entry point for all OCR work
ocr_engine = aocr.OcrEngine()
```

*Pourquoi c’est important* : la classe `OcrEngine` abstrait le travail lourd (détection de polices, analyse de mise en page, etc.). En créant un seul moteur, vous évitez de ré‑initialiser des ressources lourdes pour chaque image, ce qui maintient des performances rapides.

---

## Étape 2 – Charger votre image source (Comment faire de l'OCR sur une ROI)

Aspose Storage rend le chargement des images simple. Pointez‑le vers le chemin du fichier, et vous obtenez un objet `Image` prêt à être traité.

```python
# Replace YOUR_DIRECTORY with the actual path where invoice.png lives
source_image = storage.Image.load("YOUR_DIRECTORY/invoice.png")
```

*Astuce* : si vous travaillez avec des flux (par ex., des images téléchargées via une API web), vous pouvez passer un objet `BytesIO` à `Image.load` au lieu d’un chemin de fichier.

---

## Étape 3 – Définir les Regions of Interest (ROIs)

Nous répondons maintenant à la question centrale **comment faire de l'OCR sur une ROI** : nous indiquons au moteur les rectangles exacts contenant les données qui nous intéressent. Chaque ROI est définie par son coin supérieur gauche (`x`, `y`) et sa taille (`width`, `height`).

```python
from aspose.ocr import Roi

# Each tuple is (x, y, width, height) in pixels
regions_of_interest = [
    Roi(50, 120, 400, 60),   # Customer name block
    Roi(50, 200, 400, 80)    # Address block
]
```

*Pourquoi utiliser des ROIs ?*  
- **Vitesse** – Le moteur ignore les parties non pertinentes de l’image.  
- **Précision** – En se concentrant sur une petite zone, le bruit ailleurs ne peut pas perturber le reconnaisseur.  
- **Flexibilité** – Vous pouvez ajouter autant de ROIs que nécessaire ; le moteur renvoie une liste de résultats dans le même ordre.

---

## Étape 4 – Comment définir le prétraitement pour une meilleure précision OCR

Les images provenant directement de scanners ou de téléphones souffrent souvent d’inclinaison, de faible contraste ou d’éclairage inégal. Aspose OCR propose un objet `PreprocessingOptions` qui vous permet d’activer des corrections courantes avant que la reconnaissance ne démarre.

```python
from aspose.ocr import PreprocessingOptions

preprocessing_options = PreprocessingOptions()
preprocessing_options.deskew = True          # Auto‑rotate tilted text
preprocessing_options.binarize = True        # Convert to black‑white for clarity
preprocessing_options.contrast = 1.5         # Boost contrast (1.0 = no change)
```

*Comment cela aide* :  
- **Deskew** supprime l’inclinaison qui rend les formes de caractères ambiguës.  
- **Binarize** réduit le bruit couleur, offrant au moteur OCR une image binaire propre.  
- **Contrast** amplifie les traits faibles, ce qui est particulièrement utile pour les reçus fanés.

Vous pouvez expérimenter avec ces drapeaux — désactivez‑en un et observez si la sortie change. C’est l’esprit de **comment définir le prétraitement** efficacement.

---

## Étape 5 – Effectuer l'OCR uniquement dans les ROIs définies

Avec le moteur, l’image, les ROIs et le prétraitement prêts, il est temps d’appeler `recognize`. La méthode renvoie un objet `OcrResult` contenant une collection `regions` — chaque entrée correspond à l’ordre des ROIs que nous avons fourni.

```python
ocr_result = ocr_engine.recognize(
    source_image,
    rois=regions_of_interest,
    preprocessing=preprocessing_options
)
```

*Dans les coulisses* : le moteur découpe chaque ROI, applique la chaîne de prétraitement, puis exécute le modèle de reconnaissance sur le fragment nettoyé. Parce que nous avons passé une liste, le résultat conserve le même ordre, ce qui simplifie le post‑traitement.

---

## Étape 6 – Lire et utiliser le texte extrait (Comment faire de l'OCR sur une ROI)

Enfin, parcourez la liste `regions` et affichez — ou stockez — les chaînes reconnues. L’objet `Region` expose une propriété `text` qui contient le résultat Unicode.

```python
for idx, region in enumerate(ocr_result.regions, start=1):
    print(f"Region {idx} text:")
    print(region.text)
    print("-" * 40)
```

**Sortie attendue (exemple)** :

```
Region 1 text:
John Doe
----------------------------------------
Region 2 text:
123 Maple Street
Springfield, IL 62704
----------------------------------------
```

Si le texte apparaît brouillé, revenez à **comment définir le prétraitement** : peut‑être augmenter `contrast` ou désactiver `binarize` pour les logos en couleur.

---

## Pièges courants et astuces professionnelles

| Problème | Pourquoi cela se produit | Solution (Comment définir le prétraitement) |
|----------|--------------------------|---------------------------------------------|
| Le texte incliné apparaît comme du charabia | `deskew` désactivé ou image trop tournée | Activez `preprocessing_options.deskew = True` |
| Les chiffres deviennent des points ou des marques errantes | Faible contraste ou binarisation agressive | Réduisez `contrast` (ex., `1.2`) ou définissez `binarize = False` |
| Les coordonnées de la ROI sont décalées de quelques pixels | DPI différent ou mise à l’échelle du scanner | Utilisez un outil (ex., Paint.NET) pour mesurer les positions exactes, ou ajoutez une petite marge (`+5` pixels) à chaque ROI |
| Résultat vide pour une région | ROI en dehors des limites de l’image | Vérifiez les dimensions de l’image : `source_image.width`, `source_image.height` |

---

## Étendre la solution (Comment faire de l'OCR sur une ROI dans différents scénarios)

- **ROIs dynamiques** : si vos factures ont des mises en page variables, vous pouvez d’abord exécuter un OCR rapide de page complète pour localiser des mots‑clés (“Customer:”, “Address:”) puis calculer les ROIs à la volée.  
- **Traitement par lots** : encapsulez les étapes ci‑dessus dans une fonction et bouclez sur un dossier d’images. N’oubliez pas de réutiliser la même instance `ocr_engine` pour garder une faible consommation mémoire.  
- **Exportation en JSON** : au lieu d’imprimer, construisez un dictionnaire et sérialisez‑le avec `json.dumps` ; cela facilite l’intégration en aval (par ex., alimentation d’un système ERP).

```python
import json

def extract_invoice_fields(image_path):
    img = storage.Image.load(image_path)
    result = ocr_engine.recognize(
        img,
        rois=regions_of_interest,
        preprocessing=preprocessing_options
    )
    data = {f"field_{i+1}": r.text.strip() for i, r in enumerate(result.regions)}
    return data

print(json.dumps(extract_invoice_fields("invoice.png"), indent=2))
```

---

## Conclusion

Vous disposez maintenant d’un exemple complet et exécutable qui montre **comment faire de l'OCR sur une ROI** en Python tout en maîtrisant **comment définir le prétraitement** pour une précision optimale. En limitant le moteur aux rectangles exacts qui vous intéressent et en nettoyant l’image au préalable, vous obtenez des résultats plus rapides et plus propres — parfait pour l’automatisation de factures, la numérisation de formulaires ou tout scénario où seule une partie de la page compte.

Prêt pour l’étape suivante ? Essayez d’ajuster les coordonnées de la ROI pour un type de document différent, ou expérimentez avec des drapeaux de prétraitement supplémentaires comme `sharpen` ou `noise_reduction`. La flexibilité d’Aspose OCR vous permet d’adapter le pipeline à pratiquement n’importe quelle qualité d’image.

Si vous rencontrez un problème, consultez la sortie console pour les régions vides et revérifiez les paramètres de prétraitement. Bon codage, et que votre OCR soit toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}