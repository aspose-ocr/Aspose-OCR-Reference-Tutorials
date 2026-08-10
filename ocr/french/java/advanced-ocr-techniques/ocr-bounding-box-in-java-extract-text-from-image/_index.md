---
category: general
date: 2026-06-16
description: Le tutoriel OCR bounding box en Java montre comment extraire du texte
  d’une image, lire le texte d’une image et obtenir le score de confiance OCR pour
  les fichiers JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: fr
og_description: La boîte englobante OCR en Java vous permet de reconnaître le texte
  à partir de fichiers JPG, d’extraire le texte d’une image et de visualiser les scores
  de confiance OCR — le tout dans un exemple de code simple.
og_title: Boîte englobante OCR en Java – Extraire le texte d’une image
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: Boîte englobante OCR en Java – Extraire le texte d’une image
url: /fr/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Boîte englobante OCR en Java – Extraire du texte à partir d'une image

Vous vous êtes déjà demandé comment obtenir la **ocr bounding box** pour chaque morceau de texte dans une image Java ? Dans ce tutoriel, nous vous montrerons comment **extract text from image** des fichiers, **read text from image**, et même voir le **ocr confidence score** pendant que vous **recognize text from jpg**. La réponse courte ? Quelques lignes de code utilisant une bibliothèque OCR moderne, plus une petite explication sur pourquoi chaque appel est important.

Vous trouverez ci‑dessous un exemple complet, prêt à l'exécution, une décomposition étape par étape, et une poignée de conseils pratiques que vous pouvez copier directement dans votre propre projet. À la fin, vous pourrez produire quelque chose comme :

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Ce dont vous avez besoin

- **Java 11** ou plus récent (la syntaxe ci‑dessous utilise le mot‑clé `var` pour plus de concision, mais vous pouvez l'omettre pour les JDK plus anciens).  
- Une bibliothèque OCR qui propose une API Java – pour ce guide nous utiliserons **[Tesseract4J](https://github.com/nguyenq/tess4j)**, un léger wrapper autour du moteur Tesseract populaire.  
- Une image JPEG (`.jpg`) contenant du texte imprimé clair.  
- Votre IDE préféré (IntelliJ IDEA, Eclipse, VS Code…) – n'importe lequel fera l'affaire.

Si vous n'avez pas la bibliothèque, ajoutez simplement cette dépendance Maven :

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Plongeons maintenant dans le vif du sujet.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## Boîte englobante OCR : configuration du moteur

La première chose à faire est de créer une instance du moteur OCR. Pensez-y comme allumer le scanner qui lira plus tard les pixels.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Pourquoi c’est important :**  
Sans définir le `datapath`, Tesseract ne saura pas où se trouvent ses packs de langues, et vous obtiendrez une erreur cryptique « Failed loading language ». L’appel `setLanguage` est optionnel si vous n’avez besoin que du pack anglais par défaut, mais être explicite rend le code plus clair pour les futurs lecteurs.

## Charger l'image que vous souhaitez traiter

Ensuite, fournissez au moteur le JPEG que vous souhaitez analyser. La bibliothèque accepte un `File` ou un `BufferedImage` ; nous utiliserons un `File` pour la simplicité.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Astuce :**  
Si votre image se trouve dans les ressources (par ex., à l'intérieur d'un JAR), utilisez `getResourceAsStream` et enveloppez‑la avec `ImageIO.read`. Ainsi le tutoriel fonctionne à la fois localement et dans une application empaquetée.

## Effectuer la reconnaissance OCR

Nous demandons maintenant au moteur de lire l'image. Le résultat est une chaîne de texte brut, mais nous voulons également le **ocr confidence score** et la **ocr bounding box** pour chaque ligne.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Pourquoi nous utilisons `getWords` au lieu du simple `doOCR` :**  
`doOCR` vous fournit la chaîne brute mais supprime les informations spatiales. En appelant `getWords` avec `RIL_WORD` (ou `RIL_TEXTLINE` si vous préférez les boîtes au niveau des lignes), nous récupérons une liste d'objets `Word` qui contiennent chacun le texte, la confiance et le rectangle englobant. C’est le cœur de la fonctionnalité **ocr bounding box**.

## Comprendre la sortie

Exécuter le fragment ci‑dessus sur un JPEG propre produit une sortie similaire à :

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – les caractères reconnus.  
- **Confidence** – une valeur flottante entre 0 et 1 ; plus élevée signifie que le moteur est plus sûr.  
- **Box** – le rectangle qui englobe le mot en coordonnées de pixels (x, y, largeur, hauteur).

Vous pouvez maintenant **read text from image** et savoir exactement où chaque extrait se trouve sur le canevas—parfait pour mettre en évidence, recadrer, ou alimenter des pipelines NLP en aval.

## Cas limites et pièges courants

| Situation | Points d’attention | Correction / Contournement |
|-----------|---------------------|-----------------------------|
| L'image est floue ou à faible contraste | Les scores de confiance chutent drastiquement (souvent en dessous de 0,6). | Pré‑traiter avec OpenCV : augmenter le contraste, appliquer un seuillage. |
| Le JPEG contient du texte tourné | Les boîtes englobantes apparaissent déformées ou manquantes. | Utilisez `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)` pour laisser Tesseract détecter automatiquement l'orientation. |
| Les grandes images provoquent OutOfMemoryError | Le tas Java se remplit lors du chargement de grandes images. | Redimensionner l'image avant l'OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Vous avez besoin de boîtes au niveau des lignes plutôt qu'au niveau des mots | `RIL_WORD` renvoie des boîtes par mot. | Passez à `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Les caractères non anglais apparaissent comme � | Les données linguistiques ne sont pas chargées. | Téléchargez le fichier `.traineddata` approprié et pointez `setDatapath` vers son dossier. |

Résoudre ces problèmes dès le départ vous fait gagner des heures de débogage plus tard.

## Exemple complet fonctionnel (Toutes les étapes dans un seul fichier)

Voici une classe Java autonome que vous pouvez copier‑coller dans un dossier `src/main/java` et exécuter avec `mvn exec:java`. Elle rassemble tout ce dont nous avons parlé.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte à partir d'une image Java avec Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extraire du texte des images – Bases de l'OCR avec Aspose.OCR pour Java](/ocr/english/java/ocr-basics/)
- [Comment OCR du texte d'image avec la langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}