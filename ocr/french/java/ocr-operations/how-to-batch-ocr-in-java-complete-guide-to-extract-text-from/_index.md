---
category: general
date: 2026-02-09
description: Apprenez à réaliser la reconnaissance optique de caractères (OCR) par
  lots en Java avec Aspose OCR. Extrayez le texte des images, reconnaissez le texte
  des fichiers PNG, JPG et TIFF en un seul appel.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- recognize text from jpg
- recognize text from tiff
language: fr
og_description: Maîtrisez la reconnaissance optique de caractères par lots en Java.
  Ce tutoriel vous montre comment extraire du texte à partir d’images PNG, JPG et
  TIFF en utilisant Aspose OCR avec des exemples de code clairs.
og_title: Comment faire de l’OCR par lots en Java – Extraire le texte des images efficacement
tags:
- OCR
- Java
- Aspose
title: Comment effectuer une OCR par lots en Java – Guide complet pour extraire du
  texte à partir d’images
url: /fr/java/ocr-operations/how-to-batch-ocr-in-java-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR par lots en Java – Guide complet pour extraire du texte à partir d'images

Vous vous êtes déjà demandé **comment faire de l'OCR par lots** sur une poignée d'images sans écrire une boucle pour chaque fichier ? Vous n'êtes pas le seul. Dans de nombreux projets réels, vous obtenez un dossier rempli de scans — des reçus PNG, des captures d'écran JPG, ou même des TIFF multi‑pages — et vous avez besoin du texte rapidement.  

La bonne nouvelle, c'est qu'Aspose OCR vous permet de faire exactement cela : un appel de méthode unique qui reconnaît le texte des fichiers PNG, JPG et TIFF en une fois. Dans ce tutoriel, nous parcourrons l'ensemble du processus, de la configuration du projet à l'affichage des résultats, afin que vous puissiez commencer à extraire du texte à partir d'images dès aujourd'hui.

## Ce que couvre ce tutoriel

* **Comment faire de l'OCR par lots** en utilisant `OcrBatchProcessor` d'Aspose.
* Moyens d'**extraire du texte à partir d'images** de différents formats (PNG, JPG, TIFF).
* Conseils pour contrôler le parallélisme afin que votre application reste réactive.
* Un programme Java complet et exécutable que vous pouvez copier‑coller et exécuter immédiatement.

Aucune expérience préalable avec Aspose n'est requise — juste une installation Java de base et un IDE de votre choix. À la fin, vous disposerez d'une base solide pour reconnaître le texte des fichiers PNG, JPG et TIFF en masse.

---

![Diagramme illustrant comment faire de l'OCR par lots sur plusieurs fichiers image](/images/batch-ocr-diagram.png "comment faire de l'ocr par lots")

*Texte alternatif de l'image : diagramme montrant comment faire de l'OCR par lots avec plusieurs fichiers image traités ensemble.*

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Java 17 ou plus récent | Aspose OCR cible les JVM modernes. |
| Maven ou Gradle | Simplifie l'ajout de la bibliothèque Aspose OCR. |
| Connaissances de base en Java | Nécessaire pour comprendre le flux du code. |
| Un ensemble d'images d'exemple (`.png`, `.jpg`, `.tif`) | Pour voir l'extraction en action. |

Si vous avez déjà tout cela, super — plongeons-y.

## Étape 1 : Ajouter Aspose OCR à votre projet

La première chose dont vous avez besoin est le JAR Aspose OCR. Avec Maven, ajoutez ceci à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- use the latest stable version -->
</dependency>
```

Si vous préférez Gradle, l'équivalent est :

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

Ajouter la dépendance récupère tout ce qui est nécessaire pour **reconnaître le texte à partir de png**, **reconnaître le texte à partir de jpg**, et **reconnaître le texte à partir de tiff**. Aucune bibliothèque native supplémentaire n'est requise.

## Étape 2 : Définir les fichiers image à traiter

Nous allons maintenant indiquer au moteur OCR quels fichiers traiter. C'est ici que **comment faire de l'OCR par lots** brille vraiment — il suffit de passer une liste de chemins et de laisser la bibliothèque faire le travail lourd.

```java
import java.util.Arrays;
import java.util.List;

// Step 2: List your image files (PNG, JPG, TIFF)
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/img1.png",   // PNG file – recognize text from png
        "YOUR_DIRECTORY/img2.jpg",   // JPG file – recognize text from jpg
        "YOUR_DIRECTORY/img3.tif");  // TIFF file – recognize text from tiff
```

> **Astuce pro :** Gardez vos chemins de fichiers absolus ou utilisez `Paths.get(...)` pour éviter les surprises sur différents systèmes d'exploitation.

## Étape 3 : Créer le processeur par lots et ajuster le parallélisme

Aspose OCR fournit `OcrBatchProcessor`, qui peut exécuter plusieurs reconnaissances en parallèle. Contrôler le nombre de threads empêche votre application de monopoliser le CPU lorsque vous avez des dizaines d'images.

```java
import com.aspose.ocr.OcrBatchProcessor;

// Step 3: Initialise the batch processor
OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();

// Limit to 4 concurrent threads – a sweet spot for most desktops
ocrProcessor.setMaxParallelism(4);
```

Pourquoi limiter le parallélisme ? Si vous lancez trop de threads sur un ordinateur portable modeste, vous pourriez constater un ralentissement au lieu d'une accélération. Configurer `setMaxParallelism` vous permet d'équilibrer vitesse et stabilité.

## Étape 4 : Exécuter l'appel OCR par lots

Voici le cœur de **comment faire de l'OCR par lots** : un appel unique `recognize` qui renvoie une liste d'objets `RecognitionResult`, un par image.

```java
import com.aspose.ocr.RecognitionResult;
import java.util.List;

// Step 4: Execute batch OCR
List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);
```

La méthode bloque jusqu'à ce que chaque image soit traitée, puis vous fournit le texte. Si vous avez besoin d'un comportement non bloquant, vous pouvez envelopper cela dans un `CompletableFuture`, mais pour la plupart des scripts, l'appel synchrone garde le code propre.

## Étape 5 : Afficher le texte extrait

Enfin, parcourez les résultats et affichez les chaînes reconnues. Cela montre que nous avons réussi à **extraire du texte à partir d'images** de divers formats.

```java
// Step 5: Output the recognized text for each file
for (int i = 0; i < recognitionResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(recognitionResults.get(i).getText());
    System.out.println("---");
}
```

### Sortie attendue

```
File: YOUR_DIRECTORY/img1.png
The quick brown fox jumps over the lazy dog.
---
File: YOUR_DIRECTORY/img2.jpg
Invoice #12345
Total: $567.89
---
File: YOUR_DIRECTORY/img3.tif
Page 1 of 3
Report generated on 2026-02-09
---
```

Si le moteur OCR ne peut pas lire un fichier, la méthode `getText()` renvoie une chaîne vide, vous pouvez donc ajouter une vérification simple pour consigner des avertissements.

## Exemple complet fonctionnel

En réunissant tous les éléments, voici la classe Java complète, prête à être exécutée. Copiez‑la dans un fichier nommé `BatchOcrTutorial.java`, ajustez les chemins d'image, et exécutez `javac && java`.

```java
import com.aspose.ocr.*;
import java.util.Arrays;
import java.util.List;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {

        // Step 1: Define the image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/img1.png",
                "YOUR_DIRECTORY/img2.jpg",
                "YOUR_DIRECTORY/img3.tif");

        // Step 2: Create the batch OCR processor and optionally limit parallelism
        OcrBatchProcessor ocrProcessor = new OcrBatchProcessor();
        ocrProcessor.setMaxParallelism(4); // limit to 4 concurrent threads

        // Step 3: Perform OCR on all images in a single batch call
        List<RecognitionResult> recognitionResults = ocrProcessor.recognize(imageFiles);

        // Step 4: Output the recognized text for each file
        for (int i = 0; i < recognitionResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(recognitionResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

Exécutez‑le, et vous verrez la console afficher le texte extrait pour chaque fichier PNG, JPG et TIFF — exactement ce dont vous avez besoin lorsque **comment faire de l'OCR par lots** est la question qui vous préoccupe.

## Questions fréquentes & cas particuliers

### Et si j'ai plus de trois images ?

Ajoutez simplement plus d'entrées à la liste `imageFiles`. Le processeur par lots répartira automatiquement le travail entre les threads que vous avez configurés avec `setMaxParallelism`.

### Mes images sont dans un sous‑dossier — dois‑je les lister manuellement ?

Vous pouvez collecter programmatique tous les fichiers avec une extension spécifique :

```java
try (Stream<Path> paths = Files.walk(Paths.get("YOUR_DIRECTORY"))) {
    List<String> imageFiles = paths
        .filter(Files::isRegularFile)
        .filter(p -> p.toString().matches(".*\\.(png|jpg|tif|tiff)$"))
        .map(Path::toString)
        .collect(Collectors.toList());
}
```

Cela maintient le code flexible et respecte toujours **comment faire de l'OCR par lots**.

### Comment gérer les résultats à faible confiance ?

`RecognitionResult` fournit une méthode `getConfidence()`. Vous pouvez filtrer les résultats en dessous d'un seuil et réessayer avec des réglages DPI plus élevés :

```java
ocrProcessor.setResolution(300); // increase DPI for better accuracy
```

### Aspose OCR prend‑il en charge d'autres langues ?

Oui — il suffit d'appeler `ocrProcessor.setLanguage(OcrLanguage.Spanish)` (ou tout autre enum supporté) avant l'appel `recognize`. Cela étend l'utilité au-delà de l'anglais, rendant **extraire du texte à partir d'images** véritablement multilingue.

## Conseils de performance

* **La taille du lot compte** – Des lots plus grands réduisent la surcharge, mais des listes très volumineuses peuvent consommer plus de mémoire. Testez avec 50–200 images par lot.
* **Parallélisme** – Sur un CPU à 4 cœurs, `setMaxParallelism(4)` offre généralement le meilleur débit. Ajustez en fonction de la charge de votre serveur.
* **Prétraitement d'image** – Convertir les images en niveaux de gris ou augmenter le contraste avant l'OCR peut améliorer la précision, surtout pour les scans bruités.

## Conclusion

Vous savez maintenant **comment faire de l'OCR par lots** en Java avec Aspose OCR, comment **extraire du texte à partir d'images** de différents formats, et pourquoi le contrôle du parallélisme est important. L'exemple de code complet montre la reconnaissance du texte à partir de fichiers PNG, JPG et TIFF en un seul appel efficace.

Prêt pour l'étape suivante ? Essayez d'alimenter la sortie OCR dans un index de recherche, une base de données, ou même un résumeur IA. Vous pouvez également expérimenter avec l'entrée PDF (Aspose OCR le prend en charge) ou combiner cela avec des bibliothèques de prétraitement d'image comme OpenCV pour une précision encore plus élevée.

Bon codage, et rappelez‑vous—l'OCR par lots n'a pas besoin d'être une source de maux de tête. Avec les bons outils et un schéma clair, vous transformerez rapidement des piles d'images en texte interrogeable.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}