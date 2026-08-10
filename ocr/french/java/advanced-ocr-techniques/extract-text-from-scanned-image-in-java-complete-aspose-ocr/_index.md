---
category: general
date: 2026-06-06
description: Extraire du texte d’une image numérisée à l’aide d’Aspose OCR pour Java.
  Apprenez comment reconnaître le texte des fichiers TIFF avec un traitement parallèle.
draft: false
keywords:
- extract text from scanned image
- recognize text from tiff
- Aspose OCR Java tutorial
- parallel OCR processing
- Java image recognition
language: fr
og_description: Extrayez le texte d’une image numérisée avec Aspose OCR. Ce guide
  montre comment reconnaître le texte des fichiers TIFF efficacement en Java.
og_title: Extraire le texte d'une image numérisée – Tutoriel Java OCR Aspose
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  headline: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  type: TechArticle
- description: Extract text from scanned image using Aspose OCR for Java. Learn how
    to recognize text from tiff files with parallel processing.
  name: Extract Text from Scanned Image in Java – Complete Aspose OCR Guide
  steps:
  - name: Maven users
    text: 'Add the following dependency to your `pom.xml`:'
  - name: Manual JAR setup
    text: Download the latest `aspose-ocr-xx.jar` from the Aspose website and place
      it on your classpath.
  - name: Expected Output
    text: '``` === Extracted Text === Invoice Number: 12345 Date: 2024‑05‑01 Total:
      $1,250.00 ... ```'
  - name: What’s Next?
    text: '- **Batch processing**: Loop over a directory of TIFFs, store each result
      in its own file. - **Integrate with Elasticsearch**: Index the extracted text
      for fast full‑text search. - **Add language detection**: Use `OcrLanguage.AutoDetect`
      for multi‑lingual documents.'
  type: HowTo
- questions:
  - answer: Absolutely. `OcrInputImage` accepts any format that Java’s ImageIO can
      read. Just replace the file extension in the path.
    question: Does this work with PNG or JPEG files?
  - answer: You could, but remember other services may need CPU cycles. A good rule
      of thumb is “total cores – 1” for dedicated OCR workers.
    question: My server has 8 cores—should I set `setMaxThreads(8)`?
  - answer: 'Check that the image isn’t completely white, that you set the correct
      language, and that the resolution is at least 200 DPI. Low‑quality scans often
      need pre‑processing (deskew, contrast boost) before feeding them to Aspose OCR.
      --- ## Wrap‑Up We’ve just **extracted text from scanned image** files u'
    question: What if the OCR result is empty?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Extraire le texte d’une image numérisée en Java – Guide complet Aspose OCR
url: /fr/java/advanced-ocr-techniques/extract-text-from-scanned-image-in-java-complete-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d’une image numérisée – Guide complet Aspose OCR

Vous avez déjà eu besoin d'**extraire du texte d’une image numérisée** mais vous ne saviez pas comment ? Vous n'êtes pas seul. Que vous numérisiez d'anciennes archives, extrayiez des données de factures, ou construisiez une bibliothèque PDF consultable, obtenir un texte fiable à partir d’un scan TIFF peut être un vrai casse‑tête.  

Bonne nouvelle : avec Aspose OCR for Java, vous pouvez **reconnaître du texte à partir de tiff** en quelques lignes seulement, et même gagner en rapidité en limitant le moteur à quelques cœurs CPU. Dans ce tutoriel, nous parcourrons l’ensemble du processus — de l’installation de la bibliothèque à la gestion du résultat—afin que vous puissiez copier‑coller un exemple fonctionnel immédiatement.

## Ce que couvre ce tutoriel

- Installation d’Aspose OCR for Java (Maven ou JAR manuel)
- Chargement d’une grande image TIFF numérisée
- Configuration du moteur pour utiliser jusqu’à 4 threads (OCR parallèle)
- Exécution du processus OCR et affichage du texte extrait
- Pièges courants (mémoire, TIFF multi‑pages) et comment les éviter
- Astuce de performance rapide : quand ajuster `setMaxThreads`

À la fin, vous serez capable d'**extraire du texte d’une image numérisée** de façon fiable, et vous comprendrez pourquoi ajuster le nombre de threads est important lorsque vous *reconnaissez du texte à partir de tiff* dans une chaîne de production.

---

![exemple d'extraction de texte d'une image numérisée](example.png "Capture d'écran montrant le texte extrait d'une image TIFF numérisée")

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

1. **Java Development Kit (JDK) 8+** – toute version récente convient.
2. **Maven** (ou la possibilité d’ajouter des JAR manuellement) – nous utiliserons Maven par simplicité.
3. Une licence **Aspose OCR for Java** (l’évaluation gratuite fonctionne, mais ajoute un filigrane).  
4. Un **grand scan TIFF** (par ex. `large_scan.tif`) que vous souhaitez traiter.

Si l’un de ces éléments vous est inconnu, ne vous inquiétez pas — chaque étape est expliquée ci‑dessous.

## Étape 1 : Ajouter Aspose OCR à votre projet

### Utilisateurs Maven

Ajoutez la dépendance suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version on Maven Central -->
</dependency>
```

### Installation manuelle du JAR

Téléchargez le dernier `aspose-ocr-xx.jar` depuis le site Aspose et placez‑le sur votre classpath.  

> **Astuce :** Conservez le JAR dans un dossier `libs/` et référencez‑le dans les paramètres de votre IDE. Cela évite les surprises du type « class not found » plus tard.

## Étape 2 : Créer une classe Java simple

Créez un fichier nommé `ParallelOcrDemo.java` dans votre répertoire source (`src/main/java`). Cette classe contiendra tout le flux de travail OCR.

```java
package com.example.ocr;

import com.aspose.ocr.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 2.1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2.2: Load the scanned TIFF image you want to process
        // Replace the path with the actual location of your image
        ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/large_scan.tif"));

        // Step 2.3: Limit the engine to use up to 4 CPU cores.
        // This is useful on servers where you don't want to hog all cores.
        ocrEngine.getSettings().setMaxThreads(4);

        // Step 2.4: Run the OCR operation
        OcrResult ocrResult = ocrEngine.process();

        // Step 2.5: Output the recognized text to the console
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

> **Pourquoi limiter les threads :** Par défaut, Aspose OCR tente d’utiliser tous les cœurs, ce qui peut priver d’autres services de ressources sur une machine partagée. Définir `setMaxThreads(4)` indique au moteur de lancer jusqu’à quatre travailleurs parallèles — suffisant pour un gain de vitesse perceptible sur la plupart des CPU modernes sans monopoliser les ressources.

## Étape 3 : Compiler et exécuter

Ouvrez un terminal à la racine du projet et lancez :

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ParallelOcrDemo"
```

Si vous n’utilisez pas Maven, compilez avec `javac` et exécutez :

```bash
javac -cp "libs/*" src/main/java/com/example/ocr/ParallelOcrDemo.java
java -cp "libs/*:src/main/java" com.example.ocr.ParallelOcrDemo
```

### Sortie attendue

```
=== Extracted Text ===
Invoice Number: 12345
Date: 2024‑05‑01
Total: $1,250.00
...
```

La console affichera la version texte brut de ce qui était présent sur la page numérisée. Si l’image comporte plusieurs pages, Aspose OCR les concatène dans l’ordre.

## Étape 4 : Gestion des TIFF multi‑pages (cas particulier)

Un scénario fréquent est le **TIFF multi‑pages** — pensez à un livre numérisé. Par défaut, `OcrInputImage` ne lit que la première trame. Pour traiter toutes les pages, utilisez `OcrInputImage` avec un `FileInputStream` et activez la prise en charge multi‑pages :

```java
import java.io.FileInputStream;
import com.aspose.ocr.*;

FileInputStream fis = new FileInputStream("YOUR_DIRECTORY/multi_page.tif");
ocrEngine.setImage(new OcrInputImage(fis, true)); // 'true' enables multi‑page
```

Désormais, `ocrEngine.process()` renverra un seul `OcrResult` contenant le texte concaténé de chaque page.

## Étape 5 : Affiner la précision de la reconnaissance

Si vous remarquez des **caractères illisibles** ou des mots manquants, essayez les ajustements suivants :

| Paramètre | Ce qu’il fait | Quand l’utiliser |
|-----------|----------------|-------------------|
| `ocrEngine.getSettings().setLanguage(OcrLanguage.English)` | Force le modèle de langue anglaise (plus rapide, plus précis pour les scans anglais) | Votre document est uniquement en anglais |
| `ocrEngine.getSettings().setResolution(300)` | Augmente la résolution des images basse résolution avant la reconnaissance | Scans inférieurs à 200 DPI |
| `ocrEngine.getSettings().setNoiseRemoval(true)` | Tente de nettoyer les taches et artefacts | Scans très bruyants |

Exemple de fragment :

```java
ocrEngine.getSettings().setLanguage(OcrLanguage.English);
ocrEngine.getSettings().setResolution(300);
ocrEngine.getSettings().setNoiseRemoval(true);
```

## Étape 6 : Exporter les résultats vers un fichier

Afficher le texte dans la console suffit pour les démonstrations, mais le code de production écrit généralement la sortie quelque part d’utile :

```java
import java.io.FileWriter;
import java.io.IOException;

// After processing
String extractedText = ocrResult.getText();
try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write(extractedText);
}
System.out.println("Text saved to output.txt");
```

Vous obtenez ainsi un fichier texte brut que vous pouvez injecter dans un index de recherche, une base de données ou une chaîne d’analyse en aval.

---

## Questions fréquentes (FAQ)

**Q : Cela fonctionne‑t‑il avec des fichiers PNG ou JPEG ?**  
R : Absolument. `OcrInputImage` accepte tout format que Java ImageIO peut lire. Il suffit de remplacer l’extension du fichier dans le chemin.

**Q : Mon serveur possède 8 cœurs—devrais‑je mettre `setMaxThreads(8)` ?**  
R : Vous pourriez, mais n’oubliez pas que d’autres services peuvent avoir besoin de cycles CPU. Une bonne règle de base est « nombre total de cœurs – 1 » pour des travailleurs OCR dédiés.

**Q : Que faire si le résultat OCR est vide ?**  
R : Vérifiez que l’image n’est pas complètement blanche, que vous avez défini la bonne langue, et que la résolution est d’au moins 200 DPI. Les scans de mauvaise qualité nécessitent souvent un pré‑traitement (redressement, amélioration du contraste) avant d’être passés à Aspose OCR.

---

## Conclusion

Nous venons d’**extraire du texte d’une image numérisée** grâce à Aspose OCR for Java, et vous savez maintenant comment **reconnaître du texte à partir de tiff** efficacement avec un traitement parallèle. Le code complet se trouve dans les extraits ci‑dessus, et vous pouvez le copier‑coller dans votre propre projet immédiatement.

### Et après ?

- **Traitement par lots** : Parcourez un répertoire de TIFF et stockez chaque résultat dans son propre fichier.  
- **Intégration avec Elasticsearch** : Indexez le texte extrait pour une recherche plein texte ultra‑rapide.  
- **Détection de langue** : Utilisez `OcrLanguage.AutoDetect` pour les documents multilingues.  

Expérimentez ces idées, et vous transformerez rapidement une montagne de documents numérisés en données consultables et exploitables.

Bon codage, et n’hésitez pas à laisser un commentaire si vous rencontrez un problème !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos projets.

- [How to recognize tiff with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}