---
category: general
date: 2026-07-21
description: Extraire du texte d’une image avec Java OCR. Apprenez comment convertir
  un PNG en texte, lire le texte d’un PNG, charger une image pour l’OCR et effectuer
  l’OCR sur une image en quelques étapes seulement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: fr
lastmod: 2026-07-21
og_description: Extraire du texte d’une image avec Java. Ce guide vous montre comment
  convertir un PNG en texte, lire le texte d’un PNG, charger une image pour l’OCR
  et effectuer l’OCR sur une image de manière efficace.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Extraire du texte d’une image en Java – Tutoriel OCR étape par étape
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Extraire du texte d’une image en Java – Guide complet de l’OCR
url: /fr/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en Java – Guide complet OCR

Vous avez déjà eu besoin d'**extraire du texte d'une image** sans savoir quelle bibliothèque Java choisir ? Vous n'êtes pas seul. Que vous numérisiez des reçus, scanniez des PDF ou construisiez une archive consultable, extraire du texte d'un PNG est un point de douleur quotidien pour de nombreux développeurs.

Dans ce tutoriel, nous allons parcourir une solution pratique qui vous permet de **convertir PNG en texte**, **lire du texte depuis PNG**, **charger une image pour l'OCR**, et **effectuer l'OCR sur une image** — le tout avec quelques lignes de code Java propre. À la fin, vous disposerez d'un programme exécutable que vous pourrez intégrer à n'importe quel projet.

## Ce que vous allez créer

Nous créerons une petite application console Java qui :

1. Charge un fichier PNG depuis le disque.  
2. Envoie l'image à un moteur OCR (Tess4J, un wrapper Java pour Tesseract).  
3. Affiche le texte reconnu dans la console.

Pas de services externes, pas de magie — juste du Java pur et un moteur OCR open‑source.

## Prérequis

- **Java 17** ou supérieur (le code compile avec des versions antérieures, mais Java 17 vous donne les dernières fonctionnalités du langage).  
- **Maven** ou **Gradle** pour la gestion des dépendances.  
- Un PNG d'exemple nommé `sample.png` placé dans un dossier que vous pouvez référencer (par ex. `src/main/resources`).  
- Une connaissance de base de la méthode `main` de Java et de la gestion des exceptions.

Si l'un de ces points vous semble inconnu, ne vous inquiétez pas — chaque étape comprend un bref rappel.

## Étape 1 : Configurer le projet et ajouter la bibliothèque OCR

Tout d'abord, créez un nouveau projet Maven (ou Gradle si vous préférez). Ajoutez la dépendance Tess4J, qui inclut les binaires de Tesseract pour vous.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Tess4J – Java wrapper for Tesseract OCR -->
        <dependency>
            <groupId>net.sourceforge.tess4j</groupId>
            <artifactId>tess4j</artifactId>
            <version>5.5.1</version>
        </dependency>
    </dependencies>
</project>
```

> **Astuce :** Si vous utilisez Gradle, la ligne équivalente est `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Ajouter cette bibliothèque vous donne la classe `Tesseract`, qui gère le travail lourd de **performing OCR on image**.

## Étape 2 : Charger l'image pour l'OCR

Nous devons maintenant **load image for OCR**. Tess4J travaille avec `java.awt.image.BufferedImage`, nous allons donc lire le PNG avec `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

La méthode ci‑dessus isole proprement la logique de **load image for OCR**, ce qui rend le reste du code plus facile à tester. Remarquez le commentaire – il reflète le fragment original tout en l'étendant pour plus de clarté.

## Étape 3 : Effectuer l'OCR sur l'image

Avec l'image en mémoire, nous pouvons maintenant **perform OCR on image**. L'instance `Tesseract` est notre moteur ; nous la configurerons pour utiliser les données linguistiques anglaises par défaut fournies avec Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Ici, nous avons fusionné les « Step 1 » et « Step 4 » originaux en une seule méthode, car l'objet `Tesseract` est peu coûteux à créer et nous voulons que le code reste compact. Le commentaire fait toujours référence aux étapes originales pour la traçabilité.

## Étape 4 : Assembler le tout – Méthode `main`

Enfin, nous rassemblons tout dans `main`. C’est ici que vous **read text from PNG** et voyez le résultat affiché dans la console.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Lorsque vous exécutez `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (ou l'équivalent Gradle), vous devriez voir quelque chose comme :

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Cette sortie prouve que vous avez réussi à **extract text from image**, **convert PNG to text**, et **read text from PNG** dans un programme unique et bien structuré.

## Gestion des cas limites courants

### Images de basse qualité

Si le PNG est flou ou a un faible contraste, la précision de l'OCR diminue. Une solution rapide consiste à pré‑traiter l'image :

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Support multilingue

Tess4J peut gérer de nombreuses langues. Téléchargez simplement le fichier `.traineddata` approprié et indiquez `tesseract.setLanguage("spa")` pour l'espagnol, par exemple.

### Gros PDF ou images multipages

Si vous devez **extract text from image** contenues dans un PDF, découpez chaque page en PNG d'abord (avec PDFBox) puis alimentez chaque PNG à la même routine OCR.

## Exemple complet fonctionnel (tout le code en un seul endroit)

Voici la classe Java complète, prête à être exécutée. Copiez‑collez‑la dans `src/main/java/com/example/ocrdemo/OcrDemo.java` et vous êtes prêt.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Lancer la classe affiche le résultat OCR, confirmant que vous avez bien **performed OCR on image** et transformé votre PNG en texte éditable.

## Récapitulatif & étapes suivantes

Nous avons commencé par **extracting text from image** avec une configuration Java légère. Vous savez maintenant comment **load image for OCR**, **perform OCR on image**, et **read text from PNG** — des blocs de construction essentiels pour toute chaîne de numérisation de documents.

Envie d'aller plus loin ? Essayez ces idées :

- **Traitement par lots** : parcourez un répertoire de PNG et écrivez chaque résultat dans un fichier `.txt`.  
- **Intégration avec une base de données** : stockez les chaînes extraites avec leurs métadonnées pour des archives consultables.  
- **Combinaison avec le NLP** : alimentez la sortie OCR dans un modèle d'analyse de sentiment pour obtenir rapidement des insights.  

Chacune de ces extensions repose sur les mêmes concepts de base que nous avons abordés, vous êtes donc prêt à expérimenter.

---

*Bon codage ! Si vous rencontrez des difficultés*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}