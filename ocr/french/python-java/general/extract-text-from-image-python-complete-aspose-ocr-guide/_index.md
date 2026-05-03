---
category: general
date: 2026-05-03
description: Extraire du texte d’une image en Python avec Aspose OCR. Apprenez un
  tutoriel OCR Python étape par étape avec prise en charge du latin‑cyrillique mixte.
draft: false
keywords:
- extract text from image python
- Aspose OCR Python
- image to text conversion
- mixed language OCR
- Python OCR tutorial
language: fr
og_description: Extraire rapidement du texte d’une image avec Python. Ce guide montre
  comment utiliser Aspose OCR en Python pour des images mixtes latin‑cyrilliques.
og_title: Extraction de texte à partir d’une image en Python – Guide complet d’Aspose
  OCR
tags:
- OCR
- Python
- Aspose
title: Extraire du texte d’une image avec Python – Guide complet Aspose OCR
url: /fr/python-java/general/extract-text-from-image-python-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image Python – Guide complet Aspose OCR

Vous avez déjà eu besoin de **extract text from image python** mais vous n'étiez pas sûr de la bibliothèque capable de gérer un mélange de caractères latins et cyrilliques ? Vous n'êtes pas le seul — les développeurs rencontrent constamment ce problème lorsqu'ils effectuent de l'OCR sur des captures d'écran multilingues.  

La bonne nouvelle, c'est qu'Aspose OCR pour Python rend le processus presque indolore. Dans ce tutoriel, nous parcourrons l'installation du package, l'application de votre licence, le chargement d'une image multilingue, et enfin l'extraction du texte reconnu en quelques lignes de code. À la fin, vous disposerez d'un script prêt à l'emploi que vous pourrez intégrer à n'importe quel projet.

## Ce que vous apprendrez

- Comment configurer **Aspose OCR Python** dans un environnement virtuel.  
- Pourquoi indiquer les langues (comme le latin et le cyrillique) accélère la détection.  
- Le code exact nécessaire pour **extract text from image python** avec un appel de fonction unique.  
- Les pièges courants lors du traitement d'OCR multilingue et comment les éviter.  

### Prérequis

- Python 3.8 ou version supérieure installé sur votre machine.  
- Un fichier de licence Aspose OCR (`Aspose.OCR.Java.lic`). L'essai gratuit fonctionne pour les tests, mais un fichier sous licence supprime les filigranes.  
- Une image PNG/JPEG contenant à la fois des caractères latins et cyrilliques (nous l'appellerons `mixed_latin_cyrillic.png`).  

Si vous avez coché ces cases, vous êtes prêt à partir — aucun framework supplémentaire ou dépendance lourde n'est requis.

---

## Étape 1 – Extraire du texte d'une image Python : installer Aspose OCR

Première chose à faire : récupérer la bibliothèque depuis PyPI et s'assurer que votre environnement peut localiser le fichier de licence.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the Aspose OCR package
pip install asposeocrcloud
```

> **Conseil pro :** Si vous rencontrez une erreur de permission, ajoutez `--user` à la commande `pip install` ou exécutez le terminal en tant qu'administrateur.

Maintenant que le package est sur votre système, nous l'importerons et indiquerons au moteur où se trouve notre licence.

```python
import asposeocrcloud as ocr   # the library we just installed

# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Apply your license – replace the path with the actual location of your .lic file
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")
```

Pourquoi avons‑nous besoin d'une licence à ce stade ? Sans elle, le moteur fonctionne en **evaluation mode**, ce qui limite le nombre de pages et ajoute un filigrane à la sortie. Fournir la licence dès le départ garantit que l'appel `recognize` ultérieur renvoie du texte propre.

## Étape 2 – Charger votre image contenant du contenu latin‑cyrillique mixte

Ensuite, nous chargeons l'image en mémoire. Aspose OCR travaille avec sa propre classe `Image`, qui abstrait le format de fichier sous‑jacent.

```python
# Load the image that contains both Latin and Cyrillic characters
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")
```

Si vous vous demandez si d'autres formats fonctionnent — oui, JPEG, BMP, TIFF et même PDF sont pris en charge. Il suffit de changer l'extension du fichier et la méthode `from_file` s'occupera du reste.

## Étape 3 – Indiquer les langues pour une détection plus rapide (Optionnel mais utile)

Lorsque vous connaissez les langues présentes dans l'image, vous pouvez prévenir le moteur. Ce n'est pas obligatoire, mais cela **réduit considérablement le temps de traitement** et améliore la précision pour l'OCR multilingue.

```python
# Provide language hints: Latin and Cyrillic
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]
```

La liste d'indices accepte toute langue prise en charge par Aspose OCR (par ex., `"Arabic"`, `"Japanese"`). Si vous sautez cette étape, le moteur essaiera chaque langue intégrée, ce qui peut être plus lent sur de gros lots.

## Étape 4 – Exécuter le moteur OCR et extraire le texte

Voici le moment de vérité : reconnaître réellement les caractères. La méthode `recognize` renvoie un objet `OcrResult` qui contient le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

```python
# Perform OCR on the loaded image
ocr_result = ocr_engine.recognize(input_image)

# The recognised text is available via the .text attribute
extracted_text = ocr_result.text
```

> **Pourquoi cela fonctionne :** En interne, Aspose OCR combine un détecteur de texte à réseau neuronal avec des classificateurs spécifiques à chaque langue. En lui fournissant un objet `Image`, vous évitez toute nécessité de prétraitement manuel comme la binarisation.

## Étape 5 – Voir le texte extrait

Enfin, affichons le résultat dans la console. Dans une application réelle, vous pourriez l'écrire dans un fichier, le pousser vers une base de données, ou le transmettre à une API de traduction.

```python
print("Recognised text:")
print(extracted_text)
```

Lorsque vous exécutez le script, vous devriez voir quelque chose comme :

```
Recognised text:
Hello мир! This is a test.
```

Cette sortie confirme que nous avons réussi à **extract text from image python**, en gérant à la fois les caractères latins et cyrilliques en une seule passe.

## Exemple complet fonctionnel

Ci-dessous le script complet que vous pouvez copier‑coller dans un fichier nommé `extract_ocr.py`. Remplacez simplement les chemins factices par vos répertoires réels.

```python
import asposeocrcloud as ocr   # package installed via pip

# ------------------------------------------------------------
# Step 1 – Initialise engine and apply license
# ------------------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.license = ocr.License()
ocr_engine.license.set_license(r"YOUR_DIRECTORY/Aspose.OCR.Java.lic")   # path to your license file

# ------------------------------------------------------------
# Step 2 – Load the image (mixed Latin‑Cyrillic)
# ------------------------------------------------------------
input_image = ocr.Image.from_file(r"YOUR_DIRECTORY/mixed_latin_cyrillic.png")

# ------------------------------------------------------------
# Step 3 – (Optional) Hint the languages present
# ------------------------------------------------------------
ocr_engine.config.language_hints = ["Latin", "Cyrillic"]

# ------------------------------------------------------------
# Step 4 – Run OCR
# ------------------------------------------------------------
ocr_result = ocr_engine.recognize(input_image)

# ------------------------------------------------------------
# Step 5 – Display the recognised text
# ------------------------------------------------------------
print("Recognised text:")
print(ocr_result.text)
```

Enregistrez le fichier, activez votre environnement virtuel, puis exécutez :

```bash
python extract_ocr.py
```

Vous devriez voir le texte reconnu affiché, confirmant que le script fonctionne de bout en bout.

## Questions fréquentes & cas limites

**Et si l'image est floue ?**  
Aspose OCR intègre la désorientation et la réduction du bruit, mais pour des photos fortement dégradées vous pourriez vouloir les pré‑traiter avec OpenCV (par ex., appliquer un flou gaussien et un seuillage). La classe `Image` peut également accepter un tableau NumPy, vous permettant d'enchaîner des filtres personnalisés avant d'appeler `recognize`.

**Puis-je traiter un dossier entier d'images ?**  
Absolument. Enveloppez la logique dans une boucle `for`, changez `from_file` pour lire chaque nom de fichier, et stockez les résultats dans un dictionnaire. N'oubliez pas de respecter les limites de taux de l'API si vous utilisez la version cloud.

**Ai-je besoin d'une licence séparée pour chaque langue ?**  
Non, une seule licence Aspose OCR couvre toutes les langues prises en charge. La liste `language_hints` n'est qu'une indication de performance.

**Qu'en est‑il de l'entrée PDF ?**  
Remplacez `Image.from_file` par `ocr.Image.from_file("document.pdf")`. Le moteur OCR rasterisera automatiquement chaque page et renverra le texte concaténé.

## Conclusion

Nous venons de présenter une méthode concise et prête pour la production afin de **extract text from image python** avec Aspose OCR. Les étapes — installer, licence, charger, indiquer les langues, reconnaître et afficher — couvrent tout ce dont vous avez besoin pour obtenir des résultats fiables sur du contenu latin‑cyrillique mixte.  

À partir de là, vous pourriez explorer des sujets avancés comme la **conversion d'image en texte** pour le traitement par lots, intégrer la sortie avec un **tutoriel Python OCR** sur le traitement du langage naturel, ou expérimenter d'autres indices de langue pour des documents multilingues. Le ciel est la limite, et le code est déjà entre vos mains.

Vous avez un autre cas d'utilisation ou vous êtes tombé sur un problème ? Laissez un commentaire, partagez votre expérience, et continuons la conversation. Bon codage !  

![Exemple d'extraction de texte d'une image Python](/images/extract-text-from-image-python.png "Capture d'écran montrant la sortie OCR – extract text from image python")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}