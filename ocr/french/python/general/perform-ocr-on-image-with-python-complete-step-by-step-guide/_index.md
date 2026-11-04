---
category: general
date: 2026-07-05
description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  avec Python. Apprenez comment convertir une image en texte avec Python, charger
  une image pour l’OCR et extraire du texte cyrillique d’une image en quelques minutes.
draft: false
keywords:
- perform OCR on image
- convert image to text python
- load image for OCR
- extract Cyrillic text from image
- recognize Cyrillic text
language: fr
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  en Python. Ce guide vous montre comment convertir une image en texte avec Python,
  charger une image pour l'OCR et extraire rapidement du texte cyrillique d’une image.
og_title: Effectuer la reconnaissance optique de caractères sur une image avec Python
  – Tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Python. Learn how to convert image to text
    python, load image for OCR and extract Cyrillic text from image in minutes.
  headline: Perform OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- Cyrillic
title: Effectuer l'OCR sur une image avec Python – Guide complet étape par étape
url: /fr/python/general/perform-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image avec Python – Guide complet étape par étape

Vous vous êtes déjà demandé comment **effectuer une OCR sur une image** sans la confier à un service tiers ? Vous n'êtes pas seul. Dans de nombreux projets—scanners de passeports, numériseurs de reçus ou outils d'archivage—obtenir le texte brut d'une image est le premier obstacle.  

Dans ce tutoriel, nous parcourrons un exemple pratique qui **convertit image en texte python** style, vous montre comment **charger une image pour l'OCR**, et enfin **extraire du texte cyrillique d'une image** en utilisant la bibliothèque open‑source `aocr`. À la fin, vous serez capable de **reconnaître du texte cyrillique** dans n'importe quelle image que vous lui soumettez.

> **Ce que vous en retirerez :** un script prêt à l'emploi, des explications claires de chaque étape, et des astuces pour gérer les problèmes courants (comme les numérisations floues ou les polices inattendues). Aucun API externe, juste du Python pur.

---

## Prérequis

- Python 3.8 ou une version plus récente installé.
- Un terminal ou invite de commande avec lequel vous êtes à l'aise.
- Le package `aocr` (installable via `pip install aocr`).
- Un fichier image contenant des caractères cyrilliques (par ex., un passeport russe numérisé).  

Si l'un de ces points vous semble inconnu, ne paniquez pas — chaque puce sera brièvement abordée au fur et à mesure.

---

## Étape 1 : Effectuer une OCR sur une image – Configurer l'environnement

La première chose dont nous avons besoin est un environnement Python propre où réside la bibliothèque OCR. Utiliser un environnement virtuel isole les dépendances et évite les conflits de versions.

```bash
# Create a virtual environment (optional but recommended)
python -m venv ocr-env
# Activate it (Windows)
ocr-env\Scripts\activate
# Activate it (macOS/Linux)
source ocr-env/bin/activate

# Install the aocr library
pip install aocr
```

**Pourquoi ?**  
Un environnement dédié garantit que le package `aocr` et ses binaires natifs n'interfèrent pas avec d'autres projets. Il rend également la reproductibilité très simple—quelqu'un d'autre peut cloner votre dépôt et exécuter la même commande `pip install -r requirements.txt`.

> **Astuce pro :** Geler vos dépendances avec `pip freeze > requirements.txt` afin de toujours savoir exactement quelles versions ont été utilisées.

---

## Étape 2 : Charger une image pour l'OCR – Importation et préparation du fichier

Maintenant que la bibliothèque est prête, nous devons **charger une image pour l'OCR**. La méthode `aocr.Image.from_file` gère la plupart des formats courants (PNG, JPEG, TIFF). Voici comment procéder :

```python
import aocr

# Path to the Cyrillic image – replace with your actual file location
image_path = "YOUR_DIRECTORY/rus_passport.png"

# Load the image into an aocr.Image object
cyrillic_image = aocr.Image.from_file(image_path)
```

**Que se passe-t-il ici ?**  
`aocr.Image.from_file` lit les données binaires, les décode et les stocke dans un objet que le moteur OCR peut comprendre. Si le fichier est introuvable, Python lèvera une `FileNotFoundError`, que vous pourrez intercepter plus tard si vous avez besoin d'une gestion d'erreur élégante.

> **Cas particulier :** Certains scanners produisent des TIFF multi‑pages. Dans ce cas, vous devez d'abord diviser les pages—`aocr` fournit `Image.from_tiff_pages()` pour cela.

---

## Étape 3 : Configurer le moteur OCR – Forcer la reconnaissance cyrillique

Par défaut, de nombreux moteurs OCR essaient de deviner la langue, ce qui peut entraîner une sortie brouillée pour les scripts non latins. Pour **reconnaître du texte cyrillique** de manière fiable, nous définissons explicitement la langue sur « cyrillic ».

```python
# Create an OCR engine instance
ocr_engine = aocr.OcrEngine()

# Force the engine to use the Cyrillic recognizer
ocr_engine.language = "cyrillic"
```

**Pourquoi forcer la langue ?**  
Les caractères cyrilliques partagent des similitudes visuelles avec les lettres latines (par ex., « A » vs « А »). Indiquer au moteur d’attendre du cyrillique réduit considérablement les erreurs de reconnaissance, surtout sur des numérisations à basse résolution.

---

## Étape 4 : Effectuer une OCR sur une image – Lancer la reconnaissance

Avec l'image chargée et le moteur réglé, nous **effectuons enfin une OCR sur l'image**. La méthode `recognize` renvoie un objet `OcrResult` contenant le texte extrait et les scores de confiance.

```python
# Run the OCR process
ocr_result = ocr_engine.recognize(cyrillic_image)

# Print the raw text
print("Cyrillic text:")
print(ocr_result.text)
```

**Que vous fournit `ocr_result` ?**  
- `text` : la chaîne simple des caractères reconnus.  
- `confidence` : un flottant (0‑1) indiquant la certitude globale.  
- `lines` : une liste d'objets ligne si vous avez besoin d'un contrôle granulaire.

> **Question fréquente :** *Et si le texte est à l'envers ?*  
> `aocr` peut auto‑tourner les images ; il suffit de définir `ocr_engine.auto_rotate = True` avant d'appeler `recognize`.

---

## Étape 5 : Convertir une image en texte Python – Post‑traitement du résultat

La chaîne brute peut contenir des espaces superflus ou des artefacts de saut de ligne. Pour **convertir image en texte python** style, nous allons la nettoyer avec quelques étapes simples :

```python
import re

# Remove extra whitespace and normalize line breaks
clean_text = re.sub(r'\s+', ' ', ocr_result.text).strip()

print("\nCleaned Cyrillic text:")
print(clean_text)
```

**Pourquoi s'en soucier ?**  
Une sortie nettoyée est plus facile à intégrer dans les pipelines en aval—que vous la stockiez dans une base de données, l'envoyiez à une API de traduction, ou exécutiez des recherches regex pour des numéros de passeport.

---

## Étape 6 : Extraire du texte cyrillique d'une image – Tout assembler

Regroupons tout dans une fonction unique et réutilisable. Cela rend **extraire du texte cyrillique d'une image** une simple ligne de code dans vos projets.

```python
def extract_cyrillic_text(image_path: str) -> str:
    """
    Loads an image, forces Cyrillic OCR, and returns cleaned text.
    """
    # Load image
    img = aocr.Image.from_file(image_path)

    # Configure OCR engine for Cyrillic
    engine = aocr.OcrEngine()
    engine.language = "cyrillic"

    # Recognize text
    result = engine.recognize(img)

    # Clean up the output
    cleaned = re.sub(r'\s+', ' ', result.text).strip()
    return cleaned

# Example usage
if __name__ == "__main__":
    path = "YOUR_DIRECTORY/rus_passport.png"
    print("Extracted text:", extract_cyrillic_text(path))
```

**Résultat attendu (exemple) :**  

```
Extracted text: ПАСПОРТ РФ № 1234567890 ИМЯ ФАМИЛИЯ ДАТА РОЖДЕНИЯ 01.01.1990
```

Si l'image est nette et que la police correspond au modèle OCR, vous obtiendrez une transcription quasi parfaite.

---

## Dépannage & Astuces

| Problème | Cause probable | Solution |
|----------|----------------|----------|
| Caractères brouillés | Paramètre de langue incorrect | Assurez‑vous que `ocr_engine.language = "cyrillic"` |
| Sortie vide | Image trop sombre ou basse résolution | Prétraiter avec `opencv` pour augmenter le contraste |
| Mauvaise orientation | Image pivotée de 90° | Définir `ocr_engine.auto_rotate = True` |
| Performance lente | Image volumineuse (>5 MP) | Redimensionner avec `aocr.Image.resize(width=1024)` avant la reconnaissance |

![exemple d'OCR sur image montrant du code Python extrayant du texte cyrillique d'une numérisation de passeport.](ocr_example.png "exemple d'OCR sur image")

*Texte alternatif : “exemple d'OCR sur image montrant du code Python extrayant du texte cyrillique d'une numérisation de passeport.”*

---

## Conclusion

Nous venons d'**effectuer une OCR sur des fichiers image** en utilisant du Python pur, d'avoir appris comment **charger une image pour l'OCR**, d'avoir forcé le moteur à **reconnaître du texte cyrillique**, et enfin d'**extraire du texte cyrillique d'une image** avec une fonction d'aide pratique. L'ensemble du pipeline—de l'installation de `aocr` au nettoyage du résultat—se résume à quelques dizaines de lignes de code et peut être intégré à n'importe quel projet qui a besoin de **convertir image en texte python**.

## Prochaines étapes

- **Traitement par lots :** Parcourir un dossier de numérisations et stocker les résultats dans SQLite.
- **Détection de langue :** Combiner `langdetect` avec `aocr` pour basculer automatiquement entre le cyrillique et le latin.
- **Prétraitement avancé :** Utiliser `opencv` pour redresser, débruiter ou binariser les images afin d'améliorer la précision.
- **Intégration avec FastAPI :** Exposer la fonction `extract_cyrillic_text` comme point d'accès REST pour les applications web.

N'hésitez pas à expérimenter—changez la langue en « latin » pour les passeports anglais, ou essayez un autre moteur OCR. Les concepts restent les mêmes, et le code est suffisamment flexible pour s'adapter.

Bon codage, et que vos images soient toujours lisibles !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image avec Aspose OCR – Guide étape par étape](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convertir une image en texte – Effectuer une OCR sur une image depuis une URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extraire le texte d'une image en C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}