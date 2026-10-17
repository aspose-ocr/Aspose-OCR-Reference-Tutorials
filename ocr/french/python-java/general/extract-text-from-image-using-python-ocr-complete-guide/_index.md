---
category: general
date: 2026-06-06
description: Extrayez du texte d’une image avec Python OCR en quelques minutes. Découvrez
  l’OCR d’images multilingues, la détection automatique de la langue OCR et comment
  extraire le texte OCR avec précision.
draft: false
keywords:
- extract text from image
- how to extract OCR text
- multilingual image OCR
- detect language OCR
- auto detect language OCR
language: fr
og_description: Extrayez du texte d’une image avec Python OCR rapidement. Apprenez
  l’OCR d’images multilingues, la détection automatique de la langue en OCR, et comment
  extraire le texte OCR étape par étape.
og_title: Extraire du texte d’une image avec OCR Python – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  headline: Extract Text from Image Using Python OCR – Complete Guide
  type: TechArticle
- description: Extract text from image with Python OCR in minutes. Discover multilingual
    image OCR, auto detect language OCR, and how to extract OCR text accurately.
  name: Extract Text from Image Using Python OCR – Complete Guide
  steps:
  - name: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
    text: '**Low‑resolution images** – OCR accuracy drops sharply below 150 dpi. Upscale
      or request a higher‑resolution scan.'
  - name: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
    text: '**Noise and compression artifacts** – Apply a simple threshold filter (`opencv`
      or `Pillow`) before feeding the image to the engine.'
  - name: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
    text: '**Mixed scripts on one page** – Some engines struggle with simultaneous
      Latin and CJK characters. Split the page into regions and run separate recognitions
      if needed.'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Multilingual
title: Extraire le texte d’une image avec OCR Python – Guide complet
url: /fr/python-java/general/extract-text-from-image-using-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image avec Python OCR – Guide complet

Vous avez déjà eu besoin d'**extraire du texte d'une image** sans savoir quelle bibliothèque pouvait gérer automatiquement plusieurs langues ? Vous n'êtes pas seul — les développeurs demandent constamment *comment extraire du texte OCR* lorsqu'ils traitent des documents internationaux, des reçus ou des flyers numérisés. Dans ce tutoriel, nous parcourrons un exemple pratique en Python qui non seulement extrait le texte d'une image mais **détecte également la langue** à la volée, rendant l'OCR d'images multilingues un jeu d'enfant.

Nous couvrirons tout, de l'installation du package OCR à l'activation de **l'OCR de détection automatique de langue**, en passant par l'exécution du moteur sur une image d'exemple, puis l'affichage à la fois de la langue détectée et de la chaîne extraite. À la fin, vous disposerez d'un extrait réutilisable que vous pourrez intégrer à n'importe quel projet, que vous construisiez un pipeline de traduction ou un service d'ingestion de données.

## Extraire du texte d'une image – Configuration de l'environnement

Avant de plonger dans le code, assurez‑vous que votre poste de travail répond à ces exigences minimales :

- Python 3.8 ou plus récent (la bibliothèque utilise des annotations de type que les versions antérieures ignorent)
- `pip` pour la gestion des paquets
- Un fichier image contenant du texte dans au moins deux langues différentes (par ex. anglais + espagnol)

Vous aurez également besoin de la bibliothèque OCR qui alimente cette démonstration. Pour les besoins de ce guide, nous utiliserons le package fictif `ocr`, qui reflète des outils réels populaires comme Tesseract ou EasyOCR tout en offrant une API Python propre.

```bash
# Install the OCR package and its optional image dependencies
pip install ocr[image]
```

> **Astuce :** Si vous rencontrez des erreurs de permission, préfixez la commande avec `python -m` ou utilisez un environnement virtuel — cela garde vos site‑packages globaux bien rangés.

## Créer une instance du moteur OCR

Maintenant que la bibliothèque est prête, la première étape logique est de **créer une instance du moteur OCR**. Pensez au moteur comme à un scanner intelligent que vous pouvez configurer avant de lui fournir des images.

```python
import ocr

# Step 1: Initialize the OCR engine
engine = ocr.OcrEngine()
```

Pourquoi instancier le moteur séparément au lieu d'appeler une méthode statique ? L'objet moteur conserve l'état de configuration (comme les préférences de langue) que vous pourriez vouloir réutiliser sur de nombreuses images, vous évitant ainsi le surcoût de le réinitialiser à chaque fois.

## Activer l'OCR de détection automatique de langue

La plupart des outils OCR vous obligent à spécifier un code de langue — `eng` pour l'anglais, `spa` pour l'espagnol, etc. Deviner manuellement la langue annule l'intérêt d'un flux de travail **OCR d'image multilingue**. Heureusement, le package `ocr` propose un mode *auto detect language OCR* qui inspecte l'image et sélectionne le meilleur modèle linguistique en coulisses.

```python
# Step 2: Turn on automatic language detection
engine.set_recognition_language(ocr.Language.AUTO_DETECT)
```

Activer **detect language OCR** de cette façon signifie que vous n'aurez plus à maintenir une longue liste de codes de langue. Le moteur essaiera de faire correspondre le script qu'il voit — latin, cyrillique, han, etc.—et chargera automatiquement le modèle approprié.

## Effectuer un OCR d'image multilingue

Avec le moteur prêt, il est temps d'**extraire du texte d'une image**. La méthode `recognize_image` accepte un chemin de fichier et renvoie un objet résultat contenant à la fois le texte brut et la langue qui a été détectée.

```python
# Step 3: Run OCR on a multilingual image
image_path = "YOUR_DIRECTORY/multilang_page.png"
result = engine.recognize_image(image_path)
```

Si vous vous demandez *comment extraire du texte OCR* d'un PDF au lieu d'un PNG, le même moteur propose `recognize_pdf`—il suffit de remplacer le nom de la méthode. La logique de détection sous‑jacente reste identique, vous bénéficiant ainsi de la même fonctionnalité **auto detect language OCR**.

## Afficher la langue détectée et le texte extrait

Enfin, nous affichons ce que le moteur a découvert. L'objet résultat expose `detected_language` (une balise BCP‑47 comme `en` ou `es`) et `text`, qui contient la sortie brute de l'OCR.

```python
# Step 4: Show the language and the extracted string
print(f"Detected language: {result.detected_language}")
print("Extracted text:")
print(result.text)
```

Exécuter le script sur notre image d'exemple devrait produire quelque chose de similaire à :

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

Remarquez comment le moteur a correctement identifié l'anglais comme langue principale, tout en capturant la ligne en espagnol—exactement ce que l’on attend d’une solution **OCR d'image multilingue** robuste.

### Et si la détection échoue ?

Parfois, le moteur OCR peut revenir à une langue par défaut (généralement l'anglais) si l'image est floue ou si le script est trop exotique. Dans ces cas, vous pouvez forcer une liste de langues :

```python
engine.set_recognition_language([ocr.Language.ENGLISH, ocr.Language.SPANISH])
```

Mais rappelez‑vous, forcer les langues annule la commodité de **auto detect language OCR**, donc utilisez‑le uniquement lorsque vous connaissez un sous‑ensemble de langues.

## Pièges courants et comment extraire du texte OCR de façon fiable

Même avec la détection automatique, quelques obstacles peuvent vous surprendre :

1. **Images à basse résolution** – La précision de l'OCR chute brutalement sous 150 dpi. Agrandissez ou demandez un scan à plus haute résolution.  
2. **Bruit et artefacts de compression** – Appliquez un filtre de seuillage simple (`opencv` ou `Pillow`) avant d'alimenter l'image au moteur.  
3. **Scripts mixtes sur une même page** – Certains moteurs peinent avec des caractères latins et CJK simultanés. Divisez la page en régions et lancez des reconnaissances séparées si nécessaire.

Traiter ces problèmes améliore considérablement la qualité du processus **extract text from image**, surtout lorsqu'il s'agit de documents multilingues du monde réel.

## Exemple complet fonctionnel

Voici le script complet, prêt à être exécuté, qui combine toutes les étapes abordées. Enregistrez‑le sous le nom `multilingual_ocr.py` et lancez‑le depuis la ligne de commande.

```python
import ocr

def main():
    # Initialize engine with auto language detection
    engine = ocr.OcrEngine()
    engine.set_recognition_language(ocr.Language.AUTO_DETECT)

    # Path to your multilingual image
    image_path = "YOUR_DIRECTORY/multilang_page.png"

    # Perform OCR
    result = engine.recognize_image(image_path)

    # Output results
    print(f"Detected language: {result.detected_language}")
    print("Extracted text:")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Sortie attendue** (en supposant que l'image d'exemple contienne du texte en anglais et en espagnol) :

```
Detected language: en
Extracted text:
Welcome to our multilingual brochure.
¡Bienvenidos a nuestro folleto multilingüe!
```

N'hésitez pas à remplacer `multilang_page.png` par n'importe quelle image contenant du texte dans d'autres langues — grâce à **auto detect language OCR**, le script vous fournira toujours une balise de langue sensée et le texte correspondant.

![Extract text from image example](https://example.com/ocr-sample.png "Extract text from image")

## Conclusion

Vous savez maintenant exactement **comment extraire du texte OCR** d'une image, comment activer **auto detect language OCR**, et comment gérer les scénarios **OCR d'image multilingue** avec un minimum de code. En créant une instance du moteur OCR, en activant la détection automatique de langue, et en appelant `recognize_image`, vous pouvez extraire de façon fiable à la fois l'identifiant de langue et le texte brut.

Et après ? Essayez d'alimenter les chaînes extraites dans une API de traduction, stockez‑les dans une base de données consultable, ou combinez plusieurs pages en un seul rapport PDF. Vous pouvez également expérimenter avec différents back‑ends OCR (Tesseract, EasyOCR, Google Vision) tout en conservant le même flux de travail de haut niveau—grâce à l'interface cohérente **detect language OCR**.

Si vous rencontrez des particularités, revenez à la section « Pièges courants » ou ajustez les étapes de pré‑traitement d'image. Bon codage, et que votre prochain projet regorge de texte correctement détecté et parfaitement extrait !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}