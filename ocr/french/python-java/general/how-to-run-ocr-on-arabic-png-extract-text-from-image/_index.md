---
category: general
date: 2026-03-26
description: Apprenez à exécuter la reconnaissance optique de caractères (OCR) sur
  des images PNG en arabe et à extraire rapidement du texte arabe. Ce guide montre
  comment convertir une image en texte avec du code Python étape par étape.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: fr
og_description: Comment exécuter la reconnaissance optique de caractères (OCR) sur
  des images PNG en arabe ? Suivez ce guide complet pour extraire le texte arabe,
  reconnaître le texte arabe et convertir l’image en texte à l’aide de Python.
og_title: Comment exécuter l'OCR sur un PNG arabe – Extraire le texte d’une image
tags:
- OCR
- Python
- Arabic
title: Comment exécuter l’OCR sur un PNG arabe – Extraire le texte d’une image
url: /fr/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR sur un PNG arabe – Extraire le texte d'une image

Vous êtes-vous déjà demandé **comment exécuter l'OCR** sur une image contenant du texte arabe ? Peut‑être avez‑vous un reçu numérisé, un manuscrit historique, ou simplement une capture d’écran d’un post sur les réseaux sociaux et vous avez besoin du texte dans un format consultable. Vous n’êtes pas seul — les développeurs du monde entier rencontrent ce problème avec les langues de droite à gauche.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre **comment exécuter l'OCR** sur un fichier PNG, extraire le texte arabe et afficher le résultat dans la console. Pas de liens vagues « voir la documentation » ; juste le code que vous pouvez copier‑coller, ainsi que des explications sur l'importance de chaque ligne. À la fin, vous serez capable de **convertir une image en texte** de manière fiable, même lorsque la source est un PNG arabe difficile.

> **Ce que vous apprendrez**
> - Configurer un moteur OCR Python pour l'arabe  
> - Charger une image PNG et gérer les pièges courants  
> - Reconnaître le texte arabe et vérifier la sortie  
> - Astuces pour **extraire du texte arabe** à partir de différentes qualités d'image  

Avant de commencer, assurez‑vous d'avoir Python 3.8+ installé et une version récente de la bibliothèque `ocr` (celle utilisée dans l'extrait). Si vous utilisez un environnement virtuel, activez‑le maintenant — cela maintient les dépendances propres.

## Prérequis

- Python 3.8 ou plus récent  
- paquet `ocr` (`pip install ocr‑engine` – remplacez par le nom réel du paquet)  
- Une image PNG arabe (`arabic_doc.png`) placée quelque part où vous pouvez la référencer  
- Familiarité de base avec les fonctions et classes Python  

C’est tout. Aucun framework lourd, aucun conteneur Docker — juste du Python pur.

## Étape 1 : Installer et importer la bibliothèque OCR

Tout d'abord. Nous avons besoin du moteur OCR lui‑même. La bibliothèque que nous utiliserons expose une classe `OcrEngine` avec une API simple.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Pourquoi importer `Imaging` séparément ?* Le sous‑module `Imaging` nous fournit une méthode pratique `Image.load` qui comprend nativement les formats PNG, JPEG et TIFF. Ignorer cette étape vous obligerait à gérer les octets bruts vous‑même, ce qui est inutile dans la plupart des cas d'utilisation.

## Étape 2 : Créer l'instance du moteur OCR

Nous créons maintenant une instance du moteur. Pensez à cet objet comme le « cerveau » qui traitera l'image.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Astuce :** Si vous prévoyez de traiter de nombreuses images consécutivement, réutilisez la même instance `ocr_engine`. Elle met en cache les modèles de langue, ce qui accélère les reconnaissances suivantes.

## Étape 3 : Définir la langue sur l'arabe

L'arabe n'est pas latin ; il possède son propre jeu de caractères, une direction de droite à gauche et une mise en forme contextuelle. C'est pourquoi nous devons indiquer explicitement au moteur quel modèle de langue charger.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

Si vous oubliez cette ligne, le moteur utilise par défaut l'anglais et vous obtiendrez une sortie illisible — un problème que j'ai vu se produire trop souvent.

## Étape 4 : Charger votre image PNG

Voici où la partie **convertir une image en texte** commence réellement. Nous chargerons le fichier PNG contenant le script arabe.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Cas limites courants

| Problème | Symptôme | Solution |
|----------|----------|----------|
| L'image est trop sombre | La sortie contient de nombreux espaces vides | Pré‑traiter avec Pillow (`ImageEnhance.Brightness`) |
| Le PNG possède un canal alpha | Certains moteurs OCR lisent mal les pixels transparents | Convertir en RGB (`image.convert("RGB")`) avant le chargement |
| Le texte est tourné | Le texte reconnu est à l'envers | Faire pivoter l'image (`image.rotate(90, expand=True)`) avant de la passer au moteur |

## Étape 5 : Exécuter le processus de reconnaissance

Une fois tout configuré, nous demandons enfin au moteur d'effectuer son travail.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

La méthode `recognize` renvoie un objet contenant la chaîne Unicode brute, les scores de confiance et les boîtes englobantes. Pour la plupart des développeurs, le texte brut est tout ce dont vous avez besoin.

## Étape 6 : Afficher le texte arabe reconnu

Nous affichons maintenant le résultat. Dans une application réelle, vous pourriez l'écrire dans un fichier, une base de données ou le transmettre à une API de traduction.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

Lorsque vous exécutez le script, vous devriez voir les caractères arabes affichés dans votre console (assurez‑vous que votre terminal prend en charge Unicode). Si vous voyez des points d'interrogation ou des chaînes vides, revérifiez le paramètre de langue et la qualité de l'image.

### Sortie attendue

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

Si la sortie ressemble à la ligne ci‑dessus, félicitations — vous avez réussi à **extraire du texte arabe** d'un PNG !

## Exemple complet fonctionnel

Ci‑dessous se trouve le script complet, prêt à être copié‑collé. Remplacez `YOUR_DIRECTORY/arabic_doc.png` par le chemin vers votre propre fichier.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Exécutez‑le avec `python run_ocr.py` (ou quel que soit le nom que vous avez donné au fichier). Si tout est installé correctement, vous verrez la phrase arabe affichée dans la console.

## Comment exécuter l'OCR sur différents formats d'image

Le même code fonctionne pour JPEG, TIFF ou BMP — il suffit de changer l'extension du fichier. La méthode `Image.load` détecte automatiquement le format, vous permettant de **convertir une image en texte** sans code supplémentaire.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Rappelez‑vous que la qualité de l'image source influence fortement la précision de l'étape **reconnaître le texte arabe**. Les images haute résolution et à faible compression donnent les meilleurs résultats.

## Extraire du texte d'un PNG : conseils pour une meilleure précision

1. **DPI important** – Visez au moins 300 dpi. Un DPI inférieur entraîne souvent des caractères manquants.  
2. **Le contraste est roi** – Utilisez des outils de traitement d'image (par ex., OpenCV) pour augmenter le contraste avant de fournir l'image au moteur OCR.  
3. **Élimination du bruit** – De petites taches peuvent perturber le modèle ; le filtrage médian aide.  

Voici un extrait rapide utilisant Pillow pour améliorer un PNG avant l'OCR :

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec d'autres langues de droite à gauche que l'arabe ?**  
R : Absolument. Changez simplement le code de langue (`"ar"` → `"he"` pour l'hébreu, `"fa"` pour le persan) et le moteur chargera le modèle approprié.

**Q : Et si je dois extraire du texte de plusieurs PNG dans un dossier ?**  
R : Parcourez les fichiers, réutilisez la même instance `ocr_engine`, et collectez les résultats dans une liste ou écrivez chaque résultat dans un fichier `.txt` séparé.

**Q : Puis‑je obtenir des scores de confiance pour chaque mot ?**  
R : Oui. `ocr_result` expose souvent une méthode `get_confidences()`. Associez chaque confiance au mot correspondant pour le contrôle de qualité.

## Prochaines étapes

Maintenant que vous savez **comment exécuter l'OCR** sur des PNG arabes, envisagez ces idées complémentaires :

- **Traitement par lots :** Combinez le script avec `os.listdir` pour **extraire du texte arabe** d'un répertoire complet.  
- **Post‑traitement :** Utilisez les bibliothèques `arabic_reshaper` et `python-bidi` pour afficher correctement la sortie de droite à gauche dans les PDF.  
- **Intégration :** Alimentez le texte extrait dans un index de recherche (par ex., Elasticsearch) afin de rendre les documents numérisés recherchables.  

Chacun de ces sujets s'appuie sur les fondamentaux présentés ici, et ils vous aideront à transformer un simple script de **conversion d'image en texte** en un pipeline prêt pour la production.

---

![comment exécuter l'OCR sur un PNG arabe](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}