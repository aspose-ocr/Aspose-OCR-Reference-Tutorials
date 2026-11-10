---
category: general
date: 2026-06-16
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) sur
  des fichiers image en Java. Ce tutoriel couvre la reconnaissance de texte à partir
  de PNG, l'extraction de texte d'une image, la conversion d'image en texte et le
  chargement d'image pour l'OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: fr
og_description: Effectuez la reconnaissance OCR d’une image avec Java. Ce guide montre
  comment reconnaître le texte à partir d’un PNG, extraire le texte d’une image et
  convertir une image en texte avec un exemple prêt à l’emploi.
og_title: Effectuer la reconnaissance optique de caractères sur une image en Java
  – Tutoriel complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Effectuer la reconnaissance optique de caractères sur une image en Java – Guide
  complet étape par étape
url: /fr/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer la reconnaissance OCR sur une image en Java – Guide complet étape par étape

Vous avez déjà eu besoin d'**effectuer la reconnaissance OCR sur une image** mais vous ne saviez pas quelle bibliothèque Java choisir ? Vous n'êtes pas seul. Que vous construisiez un scanner de reçus, un archiviste de documents, ou que vous soyez simplement curieux de transformer des images en texte interrogeable, apprendre à **effectuer la reconnaissance OCR sur une image** avec Java est une compétence pratique.

Dans ce tutoriel, nous parcourrons tout ce dont vous avez besoin pour **effectuer la reconnaissance OCR sur une image** : charger l'image, configurer le moteur, reconnaître le texte, puis afficher le résultat. À la fin, vous serez capable de **reconnaître du texte à partir de PNG**, **extraire du texte d'une image**, et **convertir une image en texte** en quelques lignes de code seulement.

## Prérequis

- Java 17 ou plus récent (le code se compile avec n'importe quel JDK récent)
- Maven installé (ou votre outil de construction préféré)
- Familiarité de base avec la syntaxe Java
- Un fichier PNG que vous souhaitez tester (nous l'appellerons `hello.png`)

> **Astuce pro :** Si vous n'avez pas de PNG sous la main, créez‑en un en prenant une capture d'écran de n'importe quel texte et en l'enregistrant sous le nom `hello.png` dans un dossier appelé `resources`.

## Ce que nous allons construire

Une petite application console nommée `OcrDemo` qui :

1. **Charge l'image pour l'OCR** – lit un PNG depuis le disque.
2. **Effectue l'OCR sur l'image** – utilise le moteur Tesseract via Tess4J.
3. **Extrait le texte de l'image** – renvoie une `String` contenant le contenu reconnu.
4. Affiche le résultat dans la console.

Plongeons‑nous.

## Étape 1 : Configurer le projet et ajouter Tess4J

Tout d'abord, créez un nouveau projet Maven (ou Gradle si vous préférez). Ajoutez la dépendance Tess4J, qui encapsule le populaire moteur Tesseract OCR.

```xml
<!-- pom.xml -->
<project>
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

> **Pourquoi Tess4J ?** Il est activement maintenu, fonctionne sur toutes les plateformes, et vous offre une API Java propre pour les tâches d'**effectuer la reconnaissance OCR sur une image**.

## Étape 2 : Préparer la logique de chargement d'image

Nous allons maintenant écrire une méthode d'aide qui **charge l'image pour l'OCR**. La méthode utilise `ImageIO` de Java pour lire un PNG dans un `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Remarquez que le nom de la méthode reflète clairement l'intention de **charger l'image pour l'OCR**, rendant le code auto‑documenté.

## Étape 3 : Configurer le moteur OCR pour **Effectuer l'OCR sur l'image**

Avec l'image en main, nous créons une instance `Tesseract`, activons la détection automatique de la langue, et appelons `doOCR`. C’est le cœur de la façon dont nous **effectuons la reconnaissance OCR sur une image**.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Pourquoi activer la détection automatique ?** Cela permet au moteur de choisir le meilleur modèle linguistique pour l'image, ce qui est particulièrement utile lorsque vous **convertissez une image en texte** à partir de sources mêlant anglais et autres scripts.

## Étape 4 : Assembler le tout – L'application principale

Voici le point d'entrée qui **reconnaît du texte à partir de PNG**, **extrait du texte d'une image**, puis affiche le résultat. C’est l’exemple complet et exécutable.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Résultat attendu

Si `hello.png` contient la phrase « Hello, OCR world! », la console affichera quelque chose comme :

```
=== Recognized Text ===
Hello, OCR world!
```

Le résultat exact peut varier légèrement selon la qualité de l'image, mais vous devriez voir le texte que vous avez placé dans le PNG.

## Étape 5 : Gestion des cas limites courants

### 5.1 Traitement des images basse résolution

Si le PNG source est flou, la précision de l'OCR diminue. Une solution rapide consiste à agrandir l'image avant de la transmettre au moteur :

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Appelez `upscale(image, 2)` avant `engine.recognize(image)` pour améliorer les résultats.

### 5.2 Documents multilingues

Si vous prévoyez du texte en français ou en allemand, ajoutez simplement les codes de langue à `setLanguage` :

```java
tesseract.setLanguage("eng+fra+deu");
```

Le moteur tentera alors d'**extraire du texte d'une image** en utilisant les modèles linguistiques combinés.

### 5.3 Ignorer les pages vides

Parfois, une page PDF numérisée apparaît comme un PNG blanc. Détecter une image vide permet d'économiser du temps de traitement :

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Étape 6 : Emballage et exécution de l'application

1. **Compiler :** `mvn clean compile`
2. **Exécuter :** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Assurez‑vous que le dossier `tessdata` (contient les fichiers de langue) se trouve à côté du JAR compilé ou spécifiez son chemin absolu dans `OcrEngine`.

## Conclusion

Vous disposez maintenant d’un modèle solide, prêt pour la production, afin d’**effectuer la reconnaissance OCR sur une image** avec Java. Du **chargement de l'image pour l'OCR** à la **reconnaissance du texte à partir de PNG**, nous avons couvert comment **extraire du texte d'une image**, **convertir une image en texte**, et gérer des scénarios complexes comme les scans basse résolution ou le contenu multilingue.

Ensuite, vous pourriez explorer :

- **Traitement par lots** – parcourir un répertoire de PNG et écrire chaque résultat dans un fichier `.txt`.
- **Génération de PDF** – intégrer le texte extrait dans des PDF interrogeables.
- **Services OCR cloud** – comparer les performances locales de Tesseract avec des API comme Google Vision ou Azure Cognitive Services.

N’hésitez pas à expérimenter, à ajuster les paramètres, et à partager vos découvertes. Bon codage, et que vos images se transforment toujours en texte propre et interrogeable ! 

![Diagramme montrant le flux de travail OCR pour effectuer la reconnaissance OCR sur une image](https://example.com/ocr-workflow.png "exemple de réalisation de la reconnaissance OCR sur une image")


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Reconnaître le texte d'une image avec Aspose OCR – Tutoriel complet OCR Java](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convertir une image en texte en Java avec Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extraire le texte d'une image Java avec Aspose.OCR mode Détection des zones](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}