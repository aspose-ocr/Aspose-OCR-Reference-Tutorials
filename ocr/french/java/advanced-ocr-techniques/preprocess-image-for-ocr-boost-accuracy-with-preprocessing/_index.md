---
category: general
date: 2026-05-31
description: Prétraitez l'image pour l'OCR afin d'améliorer considérablement la précision
  de l'OCR grâce au prétraitement avec Aspose OCR Java. Suivez un guide complet étape
  par étape.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy with preprocessing
language: fr
og_description: Prétraitez l'image pour l'OCR et apprenez comment améliorer la précision
  de l'OCR grâce au prétraitement en Java avec Aspose OCR.
og_title: Prétraiter l'image pour l'OCR – Améliorez la précision grâce au prétraitement
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  headline: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  type: TechArticle
- description: Preprocess image for OCR to dramatically improve OCR accuracy with
    preprocessing using Aspose OCR Java. Follow a complete step‑by‑step guide.
  name: Preprocess Image for OCR – Boost Accuracy with Preprocessing
  steps:
  - name: Loads the original PNG.
    text: Loads the original PNG.
  - name: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
    text: Feeds it through `AutoDeskew`, `DenoiseMedian`, and `ContrastStretch`.
  - name: Runs the recognizer on the cleaned bitmap.
    text: Runs the recognizer on the cleaned bitmap.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Prétraiter l'image pour l'OCR – Améliorer la précision grâce au prétraitement
url: /fr/java/advanced-ocr-techniques/preprocess-image-for-ocr-boost-accuracy-with-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prétraiter l'image pour l'OCR – Améliorer la précision avec le prétraitement

Vous êtes‑vous déjà demandé pourquoi vos résultats OCR ressemblent à un méli‑mélo même si l'image source semble correcte ? Dans la plupart des cas, le coupable est caché dans l'image — inclinaison, bruit, faible contraste — des éléments qui perturbent même le reconnaisseur le plus intelligent. **Preprocess image for OCR** et vous verrez un bond spectaculaire en qualité.  

Dans ce tutoriel, nous ne nous contenterons pas de vous montrer comment preprocess image for OCR, nous expliquerons également **how to improve OCR accuracy with preprocessing** en construisant un petit mais puissant pipeline avec Aspose OCR for Java. À la fin, vous disposerez d'un programme prêt à l'emploi qui transforme un PNG bruyant et incliné en texte propre et lisible.

## Ce que vous apprendrez

- Pourquoi le prétraitement est important pour les moteurs OCR  
- Comment configurer Aspose OCR dans un projet Java  
- Code étape par étape qui **preprocesses image for OCR** en utilisant les filtres de désinclinaison, de débruitage et de contraste  
- Conseils pour ajuster le pipeline afin de **improve OCR accuracy with preprocessing** sur vos propres jeux de données  

Pas de fioritures, juste un exemple complet et exécutable ainsi que le raisonnement derrière chaque ligne.

## Prérequis

Avant de plonger, assurez‑vous d'avoir :

| Requirement | Reason |
|-------------|--------|
| Java 8 or newer | La bibliothèque Aspose OCR Java cible Java 8+ |
| Maven or Gradle (optional) | Simplifie l'ajout de la dépendance Aspose OCR |
| Aspose OCR for Java license file (`Aspose.OCR.Java.lic`) | Nécessaire pour débloquer toutes les fonctionnalités |
| A sample image (e.g., `noisy_skewed.png`) | L'image sur laquelle vous effectuerez le *preprocess image for OCR* |

Si l'un de ces éléments manque, faites une pause maintenant et procurez‑vous ce qu'il faut — essayer d'exécuter le code sans licence déclenchera simplement une exception.

## Étape 1 : Appliquer votre licence Aspose OCR

Première chose à faire. Le moteur OCR ne fera rien d'utile sans licence valide. Cette étape **preprocesses image for OCR** débloque indirectement l'ensemble complet des filtres d'image.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Astuce :** Conservez le fichier de licence hors du contrôle de version. Utilisez des variables d'environnement ou un coffre sécurisé en production.

## Étape 2 : Initialiser le moteur OCR et charger l'image source

Nous créons maintenant le moteur, indiquons la langue attendue, et le pointons vers le fichier que nous voulons *preprocess image for OCR*.

```java
        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Set the language – English works for most demos
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);

        // Load the source image (the one that needs preprocessing)
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));
```

Pourquoi définir la langue ? Parce que le moteur peut appliquer des heuristiques spécifiques à la langue, ce qui **improve OCR accuracy with preprocessing** déjà avant même de toucher aux filtres.

## Étape 3 : Construire un pipeline de prétraitement

C’est le cœur du tutoriel. Ici nous **preprocess image for OCR** en chaînant trois filtres :

| Filter | Ce qu'il fait | Pourquoi c'est important pour la précision |
|--------|--------------|-----------------------------|
| `AutoDeskew` | Détecte et corrige la rotation | Les lignes de texte inclinées perturbent la segmentation des caractères |
| `DenoiseMedian(3)` | Réduction du bruit par filtre médian (noyau = 3) | Supprime les taches qui ressemblent à des caractères errants |
| `ContrastStretch` | Étire l'histogramme pour augmenter le contraste | Les fonds sombres deviennent lisibles, le texte clair se démarque |

```java
        // Access the preprocessor
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();

        // 1️⃣ Correct image skew
        preprocessor.addFilter(new AutoDeskew());

        // 2️⃣ Reduce noise with a median filter (kernel size = 3)
        preprocessor.addFilter(new DenoiseMedian(3));

        // 3️⃣ Enhance contrast for sharper edges
        preprocessor.addFilter(new ContrastStretch());
```

Remarquez que nous n'avons pas besoin d'écrire du code de traitement d'image à partir de zéro — Aspose fournit des filtres prêts à l'emploi. Cela **improves OCR accuracy with preprocessing** de façon spectaculaire tout en gardant l'implémentation concise.

## Étape 4 : Exécuter l'OCR sur l'image pré‑traitée

Avec le pipeline en place, le moteur applique automatiquement les filtres avant la reconnaissance. Tout ce dont vous avez besoin est un appel unique :

```java
        // Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();
```

En coulisses, le moteur :

1. Charge le PNG original.  
2. Le fait passer par `AutoDeskew`, `DenoiseMedian` et `ContrastStretch`.  
3. Exécute le reconnaisseur sur le bitmap nettoyé.  

C’est la magie du **preprocess image for OCR** — le travail lourd est abstrait.

## Étape 5 : Sortir le texte reconnu

Enfin, imprimez le résultat dans la console ou écrivez‑le dans un fichier. À des fins de démonstration, un simple `System.out.println` suffit.

```java
        // Show the extracted text
        System.out.println(extractedText);
    }
}
```

Si tout s'est bien passé, vous devriez voir des phrases propres et lisibles au lieu d'un méli‑mélô. La sortie exacte dépend de l'image source, mais vous remarquerez une nette amélioration par rapport à l'exécution de l'OCR sur le fichier brut.

### Sortie attendue (exemple)

```
The quick brown fox jumps over the lazy dog.
This is a sample text line for OCR testing.
```

Si vous obtenez encore des caractères étranges, revérifiez l'ordre des filtres — parfois appliquer `ContrastStretch` *avant* `DenoiseMedian` donne de meilleurs résultats sur des scans fortement dégradés.

## Visualiser le pipeline (optionnel)

Ci‑dessous se trouve un schéma montrant comment l'image circule à travers chaque filtre. Cela peut vous aider à expliquer le processus à vos coéquipiers ou à l'intégrer dans la documentation.

![schéma du prétraitement d'image pour OCR](pipeline.png "Diagramme montrant les étapes AutoDeskew → DenoiseMedian → ContrastStretch pour preprocess image for OCR")

*Texte alternatif :* *diagramme preprocess image for OCR illustrant les trois filtres appliqués avant la reconnaissance.*

## Problèmes courants et comment les résoudre

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Le texte reste flou après le prétraitement | Le filtre de contraste n'est pas assez fort | Augmentez le facteur d'étirement ou essayez `HistogramEqualization` |
| OCR génère `NullPointerException` | Chemin du fichier de licence incorrect | Vérifiez le chemin et assurez‑vous que le fichier est lisible |
| L'inclinaison persiste | Rotation de l'image > 15° (limite AutoDeskew) | Pré‑tournez manuellement en utilisant `AffineTransform` avant le pipeline |
| Trop de faux positifs | Niveau de bruit élevé, taille du noyau trop petite | Augmentez le noyau médian (par ex., `new DenoiseMedian(5)`) |

En anticipant ces problèmes, vous **improve OCR accuracy with preprocessing** même sur les scans les plus difficiles.

## Étendre le pipeline

Vous voulez plus de contrôle ? Aspose OCR vous permet d'ajouter des filtres personnalisés ou de réorganiser ceux existants. Voici quelques idées :

- **Binarization** : `preprocessor.addFilter(new BinarizeOtsu());` – force le noir et blanc pur, utile pour les documents imprimés.  
- **Resize** : `preprocessor.addFilter(new Scale(2.0));` – agrandit les images basse résolution, souvent en augmentant la précision.  
- **Sharpen** : `preprocessor.addFilter(new Sharpen());` – accentue les contours pour les petites polices.  

Rappelez‑vous que chaque filtre supplémentaire ajoute du temps de traitement, donc effectuez des benchmarks sur votre matériel cible.

## Code source complet (prêt à copier‑coller)

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine and configure language & source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);
        ocrEngine.setImage(new OcrImage("YOUR_DIRECTORY/noisy_skewed.png"));

        // Step 3: Build a preprocessing pipeline to improve OCR accuracy with preprocessing
        OcrPreprocessor preprocessor = ocrEngine.getPreprocessor();
        preprocessor.addFilter(new AutoDeskew());               // Correct image skew
        preprocessor.addFilter(new DenoiseMedian(3));           // Reduce noise (kernel size = 3)
        preprocessor.addFilter(new ContrastStretch());         // Enhance contrast

        // Step 4: Perform OCR on the pre‑processed image
        String extractedText = ocrEngine.recognize();

        // Step 5: Output the recognized text
        System.out.println(extractedText);
    }
}
```

Enregistrez ceci sous le nom `PreprocessDemo.java`, ajoutez le JAR Aspose OCR à votre classpath (ou déclarez‑le dans Maven), et exécutez :



## Que devriez‑vous apprendre ensuite ?

- [Comment OCR du texte d'image avec la langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extraire du texte d'une image Java avec Aspose.OCR en mode Détection de zones](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Comment calculer l'angle d'inclinaison en Java avec Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}