---
category: general
date: 2026-06-16
description: Définissez la région d'intérêt dans l'OCR pour extraire le texte espagnol
  des cartes d'identité. Apprenez comment charger l'image pour l'OCR et spécifier
  la ROI efficacement.
draft: false
keywords:
- define region of interest
- load image for ocr
- how to specify roi
- extract id card text
- extract spanish text image
language: fr
og_description: Définir la région d'intérêt (ROI) dans l'OCR pour extraire le texte
  espagnol des cartes d'identité. Guide étape par étape sur le chargement des images
  et la définition de la ROI.
og_title: Définir la région d'intérêt dans l'OCR – Tutoriel complet Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Define region of interest in OCR to extract Spanish text from ID cards.
    Learn how to load image for OCR and specify ROI efficiently.
  headline: Define region of interest in OCR – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Définir la région d'intérêt dans l'OCR – Tutoriel complet Python
url: /fr/python-java/general/define-region-of-interest-in-ocr-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir la région d'intérêt dans l'OCR – Tutoriel complet Python

Vous êtes-vous déjà demandé comment **définir la région d'intérêt dans l'OCR** afin de ne lire que la partie d'une image dont vous avez réellement besoin ? Dans ce tutoriel, nous vous guiderons pas à pas, et nous vous montrerons également comment **charger une image pour l'OCR** et extraire du texte espagnol d'une carte d'identité en quelques lignes de Python.  

Si vous avez déjà fixé votre regard sur un scan bruyant en pensant « Il doit y avoir un moyen plus propre de récupérer le champ du nom », vous êtes au bon endroit. À la fin, vous pourrez extraire le texte de la carte d'identité qui vous intéresse sans être gêné par le bruit de fond.

## Ce que vous allez apprendre

- Pourquoi vous devez **définir la région d'intérêt** avant d'exécuter l'OCR.  
- Les étapes exactes pour **charger une image pour l'OCR** en utilisant un wrapper Python OCR populaire.  
- Comment **spécifier la ROI** avec des coordonnées en pixels.  
- Des méthodes pour **extraire le texte d'une carte d'identité** de façon fiable, même lorsque la langue source est l'espagnol.  
- Des astuces pour gérer les cas particuliers comme les cartes pivotées ou les scans à faible contraste.  

Aucune maîtrise préalable de l'OCR n'est requise — seulement un environnement Python 3 fonctionnel et un fichier JPEG d'une carte d'identité que vous souhaitez tester.

---

![Define region of interest illustration](placeholder.png){alt="Exemple de définition de région d'intérêt montrant un rectangle mis en évidence sur l'image d'une carte d'identité"}

## Étape 1 : Installer et importer la bibliothèque OCR

Tout d'abord, vous avez besoin d'une bibliothèque qui expose une classe `OcrEngine` similaire à l'extrait que vous avez vu. Pour ce guide, nous utiliserons le package fictif `ocr`, mais les mêmes concepts s'appliquent à `pytesseract`, `easyocr` ou tout wrapper qui vous permet de définir une langue et une ROI.

```bash
pip install ocr   # Replace with the actual package name you use
```

```python
# Import the library and any helper classes
import ocr
from ocr import Rectangle, Image
```

*Astuce :* Si vous utilisez `pytesseract`, la classe `Rectangle` devient simplement un tuple `(left, top, width, height)`. Le reste du flux reste identique.

## Étape 2 : Charger l'image pour l'OCR

Nous **chargeons maintenant l'image pour l'OCR**. Le moteur attend un objet `ocr.Image`, donc nous le pointons vers le fichier contenant la carte d'identité. Assurez‑vous que le chemin soit absolu ou relatif au répertoire de travail de votre script.

```python
# Create the OCR engine instance
engine = ocr.OcrEngine()

# Tell the engine which language we’re interested in – Spanish in this case
engine.language = ocr.Language.SPANISH

# Load the source image that contains the text to be recognized
engine.image = Image.load_from_file("YOUR_DIRECTORY/id-card.jpg")
```

Si l'image est très grande, pensez à la redimensionner d'abord ; les moteurs OCR sont plus rapides sur des images de moins de 1500 px de largeur.

## Étape 3 : Comment spécifier la ROI (Définir la région d'intérêt)

Voici le cœur du tutoriel : **comment spécifier la ROI**. Une région d'intérêt est simplement un rectangle qui indique au moteur OCR : « Ne regarde que dans ces limites de pixels ». Pensez à cela comme dessiner une boîte autour du champ du nom sur une carte d'identité.

```python
# Define the region of interest – left, top, width, height (all in pixels)
engine.region_of_interest = Rectangle(
    left=120,   # X‑coordinate of the left edge
    top=80,     # Y‑coordinate of the top edge
    width=340,  # Width of the box
    height=200  # Height of the box
)
```

Pourquoi ces nombres ? Dans notre image d'exemple, le nom se situe à environ 120 px du bord gauche et 80 px du haut. Ajustez‑les pour correspondre à la mise en page des cartes que vous traitez.  

*Cas particulier :* Si la carte est pivotée de 90°, échangez `width` et `height` et ajustez `left`/`top` en conséquence, ou pré‑pivotez l'image avec Pillow avant de la transmettre au moteur.

## Étape 4 : Effectuer l'OCR dans la ROI

Une fois la ROI définie, le moteur ignorera tout ce qui se trouve en dehors du rectangle. Cela accélère le traitement et réduit les faux positifs causés par les graphiques de fond.

```python
# Run OCR only inside the defined ROI
roi_result = engine.recognize()
```

L'appel `recognize()` renvoie un objet contenant le texte reconnu, les scores de confiance et les boîtes englobantes pour chaque mot.

## Étape 5 : Extraire le texte de la carte d'identité (et vérifier la sortie en espagnol)

Enfin, nous **extrayons le texte de la carte d'identité** à partir du résultat de la ROI et l'affichons. Parce que nous avons défini la langue sur l'espagnol plus tôt, le moteur OCR appliquera les dictionnaires spécifiques à la langue, améliorant la précision pour les caractères accentués comme « ñ » ou « á ».

```python
# Output the recognized text from the ROI
print("ROI text:", roi_result.text)
```

### Sortie attendue

```
ROI text: JUAN PÉREZ GARCÍA
```

Si vous voyez des caractères illisibles, vérifiez que l'image est réellement en espagnol et que les fichiers de données linguistiques de la bibliothèque OCR sont installés.

## Pièges courants & comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Chaîne vide retournée | La ROI ne intersecte aucun texte | Vérifiez les coordonnées avec un visualiseur d'image ; utilisez `engine.debug_draw_roi()` si disponible. |
| Beaucoup de caractères parasites | Pack de langue incorrect | Réinstallez les données de langue espagnole ou passez à `ocr.Language.AUTO`. |
| Scores de confiance faibles | Image floue ou à faible contraste | Pré‑traitez avec OpenCV : appliquez `cv2.GaussianBlur` et `cv2.threshold`. |
| L'OCR s'exécute sur l'image entière malgré la ROI | Utilisation d'une version ancienne de la bibliothèque | Mettez à jour vers la dernière version du package `ocr` ; les versions plus anciennes ignoraient la ROI. |

## Extension de l'exemple : plusieurs ROIs

Parfois, vous devez extraire plus d'un champ (par ex., le nom et le numéro d'identité). Le principe reste le même : modifiez `engine.region_of_interest` et appelez à nouveau `recognize()`.

```python
# ROI for the ID number (different coordinates)
engine.region_of_interest = Rectangle(120, 300, 340, 80)
id_result = engine.recognize()
print("ID Number:", id_result.text)
```

Vous pouvez également traiter par lots une liste de rectangles si la bibliothèque le supporte, ce qui évite un aller‑retour supplémentaire vers le moteur OCR.

## Script complet fonctionnel

En rassemblant le tout, voici un script prêt à l'emploi qui **définit la région d'intérêt**, **charge l'image pour l'OCR**, et **extrait le texte espagnol** d'une carte d'identité.

```python
import ocr
from ocr import Rectangle, Image

def extract_name_from_id(image_path):
    """
    Loads an image, defines a ROI around the name field,
    runs OCR in Spanish, and returns the recognized text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.SPANISH
    engine.image = Image.load_from_file(image_path)

    # Adjust these numbers to match your card layout
    engine.region_of_interest = Rectangle(left=120, top=80, width=340, height=200)

    result = engine.recognize()
    return result.text.strip()

if __name__ == "__main__":
    name = extract_name_from_id("YOUR_DIRECTORY/id-card.jpg")
    print("Extracted Name:", name)
```

Exécutez le script et vous devriez voir le nom affiché dans la console. Changez les valeurs du rectangle pour cibler d'autres champs, et vous disposerez d'un utilitaire réutilisable pour tout document de type carte d'identité.

## Prochaines étapes

- **Traitement par lots :** Parcourez un dossier de cartes d'identité et enregistrez chaque nom extrait dans un fichier CSV.  
- **Détection de langue :** Laissez l'utilisateur choisir la langue dynamiquement ; `ocr.Language.AUTO` peut être pratique.  
- **Post‑traitement :** Appliquez des expressions régulières pour nettoyer les erreurs courantes d'OCR (par ex., remplacer « 0 » par « O » lorsqu'il apparaît dans les noms).  

En maîtrisant comment **définir la région d'intérêt**, vous avez débloqué une méthode puissante pour **extraire le texte d'une carte d'identité** rapidement et avec précision, surtout lorsqu'il s'agit de documents en langue espagnole.

---

### TL;DR

Nous vous avons montré comment **définir la région d'intérêt dans l'OCR**, **charger une image pour l'OCR**, et **spécifier la ROI** afin **d'extraire le texte espagnol d'une image** d'une carte d'identité. L'exemple complet s'exécute en moins d'une minute et peut être adapté à n'importe quelle mise en page avec quelques ajustements de coordonnées. Essayez, modifiez le rectangle, et voyez l'OCR se concentrer comme un laser.

Bon codage !

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}