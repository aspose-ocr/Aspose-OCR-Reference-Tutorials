---
category: general
date: 2026-07-05
description: Créer un PDF consultable en Java avec Aspose OCR. Apprenez à compresser
  les images dans le PDF, à convertir une image numérisée en PDF et à désactiver l’incorporation
  des polices dans le PDF pour obtenir des fichiers plus petits.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: fr
og_description: Créer un PDF consultable en Java avec Aspose OCR. Ce tutoriel montre
  comment compresser les images dans un PDF, convertir une image numérisée en PDF
  et désactiver l’incorporation des polices dans le PDF.
og_title: Créer un PDF consultable en Java – Guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Créer un PDF recherchable en Java – Guide complet
url: /fr/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF interrogeable en Java – Guide complet

Vous avez déjà eu besoin de **créer un PDF interrogeable** à partir d'un document numérisé mais vous êtes resté bloqué sur la partie « comment‑faire‑cela » ? Vous n'êtes pas seul. Dans de nombreux projets, transformer un TIFF ou un JPEG en un PDF réellement consultable est une fonctionnalité *indispensable*, surtout lorsque vous souhaitez également **compresser les images dans le PDF** pour garder des tailles de fichier gérables.  

Dans ce tutoriel, nous parcourrons un exemple pratique en utilisant Aspose OCR pour Java. À la fin, vous saurez exactement comment **convertir une image numérisée en PDF**, ajuster le paramètre **compress images in PDF** et même **disable font embedding PDF** pour économiser quelques kilo‑octets supplémentaires. Pas de superflu—juste une solution complète et exécutable que vous pouvez intégrer immédiatement à votre code.

## Ce que vous apprendrez

- Configurer le moteur Aspose OCR dans un projet Java.  
- Effectuer l'OCR sur un TIFF (ou toute image raster).  
- Configurer `PdfSaveOptions` pour **compress images in PDF** et **disable font embedding PDF**.  
- Enregistrer le résultat en tant que **searchable PDF** que vous pouvez indexer ou rechercher instantanément.  

**Prérequis**  
- Java 8 ou version supérieure installé.  
- Maven ou Gradle pour la gestion des dépendances (nous montrerons l'extrait Maven).  
- Un fichier image numérisé (TIFF, PNG ou JPEG) prêt à être traité.  

Si vous avez tout cela, plongeons‑y.

![Flux de travail pour créer un PDF interrogeable – conversion OCR Java vers PDF](/images/create-searchable-pdf-workflow.png "Diagramme montrant les étapes pour créer un PDF interrogeable avec Aspose OCR")

## Étape 1 : Ajouter la dépendance Aspose OCR

Tout d'abord, ajoutez la bibliothèque Aspose OCR à votre projet. Avec Maven, ajoutez ceci à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Si vous préférez Gradle, l'équivalent est :

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Astuce :** Surveillez les notes de version d'Aspose ; les versions plus récentes offrent souvent des gains de performance pour la précision de l'OCR.

## Étape 2 : Initialiser le moteur OCR

Créer un moteur OCR est aussi simple que d'instancier `OcrEngine`. Cet objet gérera tout, du chargement de l'image à l'extraction du texte.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Pourquoi avons‑nous besoin d'un moteur dédié ? Aspose sépare le travail intensif (prétraitement d'image, modèles linguistiques) du reste de votre application, ce qui vous permet de réutiliser le même `engine` sur plusieurs fichiers sans réinitialiser les ressources lourdes.

## Étape 3 : Effectuer l'OCR sur l'image numérisée

Nous alimentons maintenant le moteur avec un fichier numérisé. La méthode `recognizeImage` renvoie un `RecognitionResult` contenant le texte extrait et les informations de mise en page.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **Et si l'image n'est pas un TIFF ?**  
> Aspose OCR détecte automatiquement les formats raster courants, vous pouvez donc la pointer vers un JPEG, PNG ou BMP sans modifier le code.

## Étape 4 : Configurer les options d’enregistrement PDF (Compression d'images & Désactivation de l’incorporation de polices)

C’est ici que les mots‑clés secondaires brillent. Nous indiquerons à Aspose de **compress images in PDF** et de **disable font embedding PDF**. Les deux paramètres réduisent la taille finale du fichier—pratique lorsque vous expédiez des dizaines de documents.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Pourquoi compresser les images ?**  
Les pages numérisées sont souvent en haute résolution ; les compresser à 80 % de qualité peut réduire un PDF de 10 pages de 12 Mo à moins de 3 Mo sans perte visuelle perceptible.

**Pourquoi désactiver l’incorporation de polices ?**  
Si le moteur OCR utilise des polices système standard (comme Arial ou Times New Roman), les incorporer est redondant. Désactiver cette option réduit davantage la taille du fichier, surtout pour de gros lots.

## Étape 5 : Enregistrer le résultat OCR en PDF interrogeable

L’étape finale assemble le tout : l’image brute, la couche de texte extraite et les options PDF que nous venons de définir.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Lorsque vous ouvrez `document.pdf` dans Adobe Reader ou tout lecteur moderne, vous verrez l’image numérisée originale **plus** une couche de texte invisible. Taper un mot dans la zone de recherche mettra en surbrillance les correspondances—exactement ce que promet « create searchable pdf ».

### Résultat attendu

Exécuter le programme avec un TIFF valide produit quelque chose comme :

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Ouvrez le PDF, appuyez sur `Ctrl+F`, tapez un mot qui apparaît sur la page numérisée, et observez-le se placer au bon endroit. C’est la marque d’un flux de travail **create searchable pdf** réussi.

## Pièges courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **PDF vide** | `PdfSaveOptions` n'est pas passé à `saveAsSearchablePdf`. | Assurez‑vous d’appeler la surcharge qui accepte `PdfSaveOptions`. |
| **Caractères corrompus** | Langue OCR non définie (la valeur par défaut est l'anglais). | Utilisez `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` avant `recognizeImage`. |
| **Taille de fichier énorme** | `setCompressImages(false)` ou `setEmbedFonts(true)`. | Conservez les deux indicateurs comme indiqué ci‑dessus. |
| **Distorsion de l'image** | `setImageQuality` réglé trop bas (<50). | Restez entre 70‑90 pour un bon compromis. |

## Étendre l'exemple

Maintenant que vous pouvez **convertir une image numérisée en PDF** et contrôler la taille, vous pourriez vouloir :

- **Traiter par lots** un dossier de numérisations avec une simple boucle `for(File f : folder.listFiles())`.  
- Ajouter des **filigranes** avec Aspose PDF (`PdfDocument.addWatermarkText`).  
- Exporter le texte OCR vers un fichier **.txt brut** pour les systèmes d'indexation (`result.getText().writeToFile("doc.txt")`).  

Toutes ces extensions réutilisent la même instance `OcrEngine`, maintenant une faible consommation de mémoire.

## Code complet, prêt à l'exécution

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Copiez‑collez ceci dans votre IDE, remplacez `YOUR_DIRECTORY` par un chemin réel, et lancez l'exécution. Si tout est correctement configuré, vous obtiendrez un **PDF interrogeable** également léger grâce à la compression d'image et à la désactivation de l’incorporation de polices.

## Conclusion

Nous venons de couvrir tout ce dont vous avez besoin pour **create searchable pdf** en Java avec Aspose OCR. De l'initialisation du moteur, à l'exécution de l'OCR, en passant par le réglage de **compress images in pdf** et **disable font embedding pdf**, jusqu'à l'enregistrement final d'un document interrogeable—chaque étape a été expliquée avec le *pourquoi* qui la sous-tend.

Prêt pour le prochain défi ? Essayez d'ajouter des packs de langues OCR, de traiter par lots des dossiers entiers, ou de superposer des PDF avec des annotations. Les bases que vous venez d’acquérir rendront ces extensions faciles.

Des questions ou envie de partager vos astuces ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Reconnaître le texte PDF – Opérations OCR avec Aspose.OCR pour Java](/ocr/english/java/ocr-operations/)
- [Reconnaissance OCR de documents PDF dans Aspose.OCR pour Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Comment faire de l'OCR sur un PDF en .NET avec Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}