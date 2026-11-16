---
category: general
date: 2026-09-10
description: Effectuez la reconnaissance OCR sur une image avec Aspose OCR Java. Apprenez
  à reconnaître le texte à partir d’un JPEG, à extraire le texte d’une image et à
  convertir l’image en texte efficacement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- recognize text from JPEG
- extract text from image
- convert image to text
- load image for OCR
language: fr
lastmod: 2026-09-10
og_description: Effectuez la reconnaissance OCR sur une image avec Aspose OCR Java.
  Ce tutoriel montre comment reconnaître le texte à partir d’un JPEG, extraire le
  texte d’une image et convertir une image en texte en quelques lignes de code.
og_image_alt: Screenshot of Java code that performs OCR on an image using Aspose OCR
og_title: Effectuer la reconnaissance optique de caractères (OCR) sur une image avec
  Aspose OCR – Guide Java
schemas:
- author: Aspose
  dateModified: '2026-09-10'
  description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  headline: How to perform OCR on image with Aspose OCR in Java
  type: TechArticle
- description: perform OCR on image using Aspose OCR Java. Learn to recognize text
    from JPEG, extract text from image, and convert image to text efficiently.
  name: How to perform OCR on image with Aspose OCR in Java
  steps:
  - name: Prerequisites
    text: '* Java Development Kit (JDK) 8 or later. * Maven or Gradle to manage dependencies
      (the example uses Maven). * A valid Aspose OCR for Java license (or a temporary
      evaluation key). * An image file named `sample.jpg` placed in a known directory.'
  - name: Load image for OCR
    text: '```java // Step 1: Load the image you want to process String imagePath
      = "YOUR_DIRECTORY/sample.jpg"; ImageStream imageStream = ImageStream.fromFile(imagePath);
      ```'
  - name: Create and configure the OCR engine
    text: '```java // Step 2: Create an OCR engine instance OcrEngine engine = new
      OcrEngine();'
  - name: Recognize text from JPEG
    text: '```java // Step 3: Attach the image to the engine engine.setImage(imageStream);'
  - name: Extract text from image and output
    text: '```java // Step 5: Output the recognized text System.out.println("=== Recognized
      Text ==="); System.out.println(result.getText()); ```'
  - name: Expected output
    text: 'Assuming `sample.jpg` contains the text “Hello World”, the console will
      display:'
  type: HowTo
tags:
- OCR
- Java
- Aspose
title: Comment effectuer l'OCR sur une image avec Aspose OCR en Java
url: /fr/java/ocr-operations/how-to-perform-ocr-on-image-with-aspose-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR sur une image avec Aspose OCR en Java

Si vous devez **effectuer une OCR sur des fichiers image** dans une application Java, ce guide fournit une solution complète, prête à l’emploi. Vous verrez comment **reconnaître du texte à partir de fichiers JPEG**, **extraire du texte d’une image** et **convertir une image en texte** en utilisant l’API moderne d’Aspose OCR.

Le tutoriel parcourt chaque étape requise — du chargement de l’image à l’affichage du texte reconnu — afin que vous puissiez intégrer la fonctionnalité OCR sans chercher d’autres ressources. Aucun outil externe n’est nécessaire en dehors de la bibliothèque Aspose OCR pour Java.

## Ce que vous allez accomplir

À la fin de cet article vous serez capable de :

* **Charger une image pour l’OCR** directement depuis le système de fichiers.  
* Activer le prétraitement d’Aspose OCR (par ex., débruitage) pour améliorer la précision.  
* **Reconnaître du texte à partir d’un JPEG** et d’autres formats raster.  
* **Extraire du texte d’une image** et l’afficher dans la console.  
* Comprendre comment **convertir une image en texte** dans un exemple de code prêt pour la production.

### Prérequis

* Java Development Kit (JDK) 8 ou supérieur.  
* Maven ou Gradle pour gérer les dépendances (l’exemple utilise Maven).  
* Une licence valide d’Aspose OCR pour Java (ou une clé d’évaluation temporaire).  
* Un fichier image nommé `sample.jpg` placé dans un répertoire connu.

> **Astuce :** Utilisez des JPEG haute résolution (300 dpi ou plus) pour obtenir les meilleurs taux de reconnaissance.  

## Étape 1 : Ajouter Aspose OCR à votre projet

Si vous gérez les dépendances avec Maven, insérez le fragment suivant dans votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

Pour Gradle, ajoutez :

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

Ces coordonnées récupèrent la dernière version stable de la bibliothèque Aspose OCR, qui inclut les fonctionnalités de prétraitement utilisées plus loin.

## Effectuer l'OCR sur une image – étape par étape

Les sections suivantes décomposent le programme complet. Chaque bloc est autonome et peut être copié, collé et exécuté.

### Charger l'image pour l'OCR

```java
// Step 1: Load the image you want to process
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ImageStream imageStream = ImageStream.fromFile(imagePath);
```

*Pourquoi c’est important :*  
`ImageStream.fromFile` lit les octets bruts du JPEG et les prépare pour le moteur OCR. La méthode fonctionne avec tout format raster pris en charge par Aspose OCR, vous pouvez donc remplacer le JPEG par un PNG ou BMP sans modifier le code.

### Créer et configurer le moteur OCR

```java
// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();

// Enable preprocessing to improve accuracy (e.g., denoising)
engine.getPreprocessing().setDenoise(true);
```

*Pourquoi c’est important :*  
Instancier `OcrEngine` alloue le moteur de reconnaissance principal. Activer le drapeau **denoise** supprime le bruit visuel qui interfère souvent avec la détection des caractères, notamment dans les JPEG numérisés.

### Reconnaître le texte à partir d’un JPEG

```java
// Step 3: Attach the image to the engine
engine.setImage(imageStream);

// Step 4: Perform OCR recognition
OcrResult result = engine.recognize();
```

*Pourquoi c’est important :*  
`engine.setImage` lie les données de l’image au pipeline OCR. `engine.recognize()` exécute le processus complet de reconnaissance, renvoyant un `OcrResult` contenant le texte extrait et les métriques de confiance.

### Extraire le texte de l'image et l'afficher

```java
// Step 5: Output the recognized text
System.out.println("=== Recognized Text ===");
System.out.println(result.getText());
```

*Pourquoi c’est important :*  
`result.getText()` fournit la représentation texte brut du contenu de l’image. L’afficher dans la console montre que **convertir une image en texte** a réussi, et vous pouvez rediriger cette chaîne vers des fichiers, bases de données ou services en aval.

## Exemple complet et exécutable

Voici la classe Java complète qui intègre toutes les étapes. Remplacez `YOUR_DIRECTORY` par le chemin absolu vers votre fichier JPEG.

```java
import com.aspose.ocr.*;

public class OcrDemo {
    public static void main(String[] args) throws Exception {
        // Load the image for OCR
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ImageStream imageStream = ImageStream.fromFile(imagePath);

        // Create and configure the OCR engine
        OcrEngine engine = new OcrEngine();
        engine.getPreprocessing().setDenoise(true); // improve accuracy

        // Attach the image and run recognition
        engine.setImage(imageStream);
        OcrResult result = engine.recognize();

        // Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Sortie attendue

En supposant que `sample.jpg` contienne le texte « Hello World », la console affichera :

```
=== Recognized Text ===
Hello World
```

Si l’image contient plusieurs lignes, chaque ligne apparaîtra sur sa propre ligne dans la sortie.

## Variations courantes et cas limites

| Situation                                 | Ajustement recommandé |
|-------------------------------------------|-----------------------|
| **JPEG basse résolution (≤150 dpi)**      | Augmentez `engine.getPreprocessing().setUpsample(true);` pour laisser Aspose agrandir avant la reconnaissance. |
| **Fond coloré (p. ex., formulaires numérisés)** | Activez `engine.getPreprocessing().setBinarize(true);` pour convertir l’image en noir et blanc. |
| **Script non latin (p. ex., cyrillique)** | Définissez la langue : `engine.getLanguage().setLanguage(OcrLanguage.RUSSIAN);`. |
| **Traitement par lots important**         | Réutilisez une même instance de `OcrEngine` pour plusieurs images afin de réduire le temps d’initialisation. |
| **Besoin de scores de confiance**         | Accédez à `result.getConfidence()` pour obtenir les valeurs de confiance caractère par caractère. |

Ces ajustements illustrent comment vous pouvez **charger une image pour l’OCR** dans différentes conditions tout en **effectuant une OCR sur une image** de façon fiable.

## Considérations de performance

* **Utilisation mémoire :** Chaque `ImageStream` charge l’image entière en mémoire. Pour des fichiers très volumineux (p. ex., >10 MB), envisagez de diffuser l’image par blocs avec `ImageStream.fromByteArray`.  
* **Sécurité des threads :** `OcrEngine` n’est *pas* thread‑safe. Créez une instance distincte par thread si vous prévoyez de paralléliser les tâches OCR.  
* **Mode licence :** Le mode d’évaluation limite le nombre de pages traitées par session. Déployez une version sous licence pour les charges de travail en production.

## Conclusion

Vous savez maintenant comment **effectuer une OCR sur des fichiers image** en Java avec Aspose OCR. Le tutoriel a couvert le chargement d’une image, l’activation du prétraitement, la reconnaissance du texte à partir d’un JPEG, l’extraction du texte et la conversion de l’image en texte—le tout dans un programme concis.

À partir d’ici, vous pouvez explorer des sujets connexes tels que **reconnaître du texte à partir de JPEG** en masse, intégrer la sortie à un index de recherche, ou combiner l’OCR avec le traitement du langage naturel pour des pipelines de documents plus intelligents. Expérimentez les options de prétraitement afin d’obtenir la meilleure précision pour vos sources d’images spécifiques.

--- 

*Image illustrant la sortie du code*  
![exemple d'OCR sur image Java](image-placeholder.png){alt="effectuer OCR sur une image avec Aspose OCR Java"}

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Preprocess Image OCR in Java with Aspose OCR – Boost Accuracy & Extract Text](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}