---
category: general
date: 2026-04-26
description: Comment exécuter la reconnaissance optique de caractères (OCR) sur un
  formulaire numérisé, apprendre à prétraiter l'image pour réduire le bruit et extraire
  rapidement le texte de l'image.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: fr
og_description: Comment exécuter la reconnaissance optique de caractères sur des documents
  numérisés, prétraiter les images, réduire le bruit et extraire le texte efficacement.
og_title: Comment exécuter l’OCR et prétraiter les images – Guide rapide
tags:
- OCR
- image processing
- Python
title: Comment exécuter l’OCR et prétraiter les images – Extraire le texte des formulaires
  numérisés
url: /fr/python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR – Guide complet pour extraire du texte d'images

Vous vous êtes déjà demandé **comment exécuter l'OCR** sur un formulaire numérisé désordonné et obtenir un texte propre et consultable ? Vous n'êtes pas seul. Dans de nombreux projets réels, l'image brute est remplie de taches, d'éclairage inégal et d'autres particularités qui font échouer l'OCR « prêt à l'emploi ».

Bonne nouvelle ? Avec seulement quelques lignes de Python et un pipeline de pré‑traitement intelligent, vous pouvez augmenter considérablement la précision de reconnaissance, **réduire le bruit**, et extraire exactement les mots dont vous avez besoin. Dans ce tutoriel, nous parcourrons chaque étape — du chargement de l'image à l'affichage de la chaîne finale— afin que vous repartiez avec un extrait de code prêt à être adapté aux factures, reçus ou tout document numérisé.

## Ce que vous allez créer

- Une instance `OcrEngine` qui communique avec la bibliothèque OCR sous‑jacent.  
- Une chaîne de pré‑traitement qui **binarise** l'image et applique un **flou médian** pour lisser les taches.  
- Un appel simple à `process()` qui renvoie un objet exposant `text`, la chaîne extraite.  

À la fin, vous disposerez d’un script autonome que vous pourrez exécuter sur n’importe quel fichier image et voir immédiatement le texte extrait dans la console.

## Prérequis

- Python 3.9+ (la syntaxe utilisée ici correspond à la dernière version stable).  
- Le package fictif `aocr` — considérez‑le comme une fine couche autour de Tesseract ou de tout moteur OCR moderne. Installez‑le avec `pip install aocr`.  
- Une image numérisée (`scanned_form.jpg`) placée dans un dossier que vous pouvez référencer.  

Si vous utilisez une vraie bibliothèque OCR comme `pytesseract`, vous pouvez remplacer `OcrEngine` par la classe appropriée — tout le reste reste identique.

![](how-to-run-ocr-example.png "exemple d'exécution de l'OCR montrant un formulaire numérisé et le texte extrait")

*Texte alternatif : comment exécuter l'OCR sur un document numérisé et visualiser le texte extrait.*

---

## Étape 1 : Comment exécuter l'OCR – Initialiser le moteur

Avant que le moteur puisse lire quoi que ce soit, nous devons créer une instance. Pensez à `OcrEngine` comme le cerveau qui interprétera plus tard les données visuelles.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Pourquoi c’est important :** Instancier le moteur configure les modèles internes, charge les packs de langues et prépare l’environnement d’exécution. Ignorer cette étape entraîne généralement une erreur `NoneType` lorsque vous appelez plus tard `process()`.

---

## Étape 2 : Comment pré‑traiter l'image – Charger votre formulaire numérisé

Maintenant que le cerveau est prêt, nous lui fournissons une image. L’image peut être dans n’importe quel format supporté par `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Astuce :** Utilisez des chemins absolus pendant le développement pour éviter les surprises « fichier introuvable » lorsque le script s’exécute depuis un répertoire de travail différent.

---

## Étape 3 : Comment réduire le bruit – Appliquer binarisation & flou médian

Les numérisations brutes contiennent souvent des points parasites, un fond inégal ou des ombres légères. Deux astuces classiques—**binarisation** et **flou médian**—nettoient l’image sans sacrifier les contours qui définissent les caractères.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Approfondissement

- **Binarisation** : La valeur `threshold=180` indique à l’algorithme : « Tout ce qui est plus clair que 180 devient blanc ; tout le reste devient noir. » Ajustez ce nombre si votre scan est trop sombre ou trop clair.  
- **Flou médian** : Un rayon de `2` signifie que le filtre examine une fenêtre de 5 × 5 pixels et remplace le pixel central par la valeur médiane. Cela lisse les taches isolées tout en conservant les traits des lettres.

> **Cas particulier :** Si votre document comporte des surlignages colorés, un simple seuil binaire peut les effacer. Dans ce cas, envisagez d’utiliser `aocr.ImageFilters.adaptive_threshold()` à la place — cela adapte le seuil localement sur l’image.

---

## Étape 4 : Comment extraire le texte – Exécuter le processus OCR

Avec une image propre en main, nous laissons enfin le moteur faire sa magie.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **Que se passe‑t‑il en coulisses ?** Le moteur exécute un réseau de neurones (ou un moteur de correspondance de motifs hérité) sur la matrice de pixels, traduit chaque glyphe reconnu en caractères Unicode, puis les assemble en lignes et paragraphes.

---

## Étape 5 : Comment extraire le texte – Afficher le résultat

L’objet `ocr_result` expose un attribut pratique `text`. Voyons ce que nous obtenons.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Résultat attendu

Si le formulaire numérisé contient :

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Vous devriez voir quelque chose comme :

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Remarquez comment l’étape de pré‑traitement a éliminé les points parasites qui transformaient auparavant « Amount » en « Am0unt ». C’est la puissance de **la réduction du bruit** avant l’OCR.

---

## Pièges courants & comment les corriger

| Symptom | Likely Cause | Quick Fix |
|---------|--------------|-----------|
| Caractères brouillés (ex. “@#%”) | Image trop sombre ou trop claire | Ajustez le `threshold` dans `binarize()` ; essayez `adaptive_threshold`. |
| Mots manquants | Bruit encore présent | Augmentez le `radius` du `median_blur` ou ajoutez un filtre `gaussian_blur`. |
| Mauvaise langue (ex. lettres anglaises devenant chinoises) | Pack de langue incorrect chargé | Passez `language="eng"` lors de la création de `OcrEngine()` si la bibliothèque le supporte. |
| Traitement lent sur de gros fichiers | Résolution élevée | Redimensionnez d’abord l’image : `aocr.ImageFilters.resize(width=1200)` avant la binarisation. |

---

## Aller plus loin – Prochaines étapes et sujets associés

- **Traitement par lots** : Enveloppez la logique ci‑dessus dans une boucle pour gérer des dizaines de fichiers automatiquement.  
- **Sortie structurée** : Utilisez des expressions régulières sur `ocr_result.text` pour extraire des champs comme les dates ou les montants.  
- **Bibliothèques alternatives** : Remplacez `aocr` par `pytesseract`—le code ne change qu’à l’étape d’initialisation du moteur.  
- **Comment pré‑traiter les images de PDFs** : Convertissez chaque page PDF en image, puis appliquez le même pipeline.  

Ces extensions vous permettent de passer d’un seul formulaire à une chaîne d’ingestion de documents de niveau entreprise.

---

## Conclusion

Nous avons couvert **comment exécuter l'OCR** de bout en bout, montré **comment pré‑traiter l'image** pour **réduire le bruit**, et démontré **comment extraire le texte d’une image** avec un script propre et reproductible. La leçon principale ? Quelques filtres simples—binarisation et flou médian—peuvent transformer un scan bruyant en une source de données fiable, vous faisant gagner des heures de nettoyage manuel.

Testez le script avec vos propres documents, ajustez les seuils, et observez la précision grimper. Quand vous serez prêt, explorez le traitement par lots ou intégrez la sortie dans une base de données pour des archives consultables. Bon codage, et que votre OCR soit toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}