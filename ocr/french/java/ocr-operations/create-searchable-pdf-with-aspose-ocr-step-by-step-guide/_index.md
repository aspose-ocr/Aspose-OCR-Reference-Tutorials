---
category: general
date: 2026-01-02
description: Créez un PDF consultable à partir d’un PDF d’images numérisées en utilisant
  Aspose OCR. Apprenez à définir la langue OCR, à intégrer une couche de texte dans
  le PDF et à appliquer des options de compression PDF élevées.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: fr
og_description: Créez rapidement un PDF consultable. Ce guide montre comment convertir
  un PDF d’image numérisée, intégrer une couche de texte, définir la langue OCR et
  activer une compression élevée du PDF.
og_title: Créer un PDF consultable avec Aspose OCR – Guide complet
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Créer un PDF consultable avec Aspose OCR – Guide étape par étape
url: /fr/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF recherchable – Tutoriel de programmation complet

Vous avez déjà eu besoin de **créer des fichiers PDF recherchables** à partir d’images numérisées sans savoir par où commencer ? Vous n’êtes pas seul. Dans de nombreux flux de travail lourds en documents, un PDF contenant uniquement des images est une impasse pour la recherche et l’indexation.  

La bonne nouvelle, c’est qu’avec Aspose OCR vous pouvez **convertir un PDF d’image numérisée** en un document entièrement recherchable en quelques lignes de Java seulement. Ce tutoriel vous guide à chaque étape : initialisation du moteur OCR, configuration des paramètres PDF à haute compression, insertion d’une couche de texte cachée, et même le choix de la langue OCR appropriée.

À la fin de ce guide, vous disposerez d’un programme exécutable qui génère un PDF recherchable, un fichier que vous pourrez déposer dans n’importe quel moteur de recherche ou système de gestion documentaire sans problème.

---

## Créer un PDF recherchable – Vue d’ensemble

Avant de plonger dans le code, clarifions ce que signifie réellement « créer un PDF recherchable ». Un PDF recherchable comporte deux couches parallèles :

1. **Couche visuelle** – l’image numérisée originale (ou la page rendue).  
2. **Couche texte** – des caractères invisibles mais lisibles par machine, extraits par l’OCR.

Lorsque vous ouvrez un tel PDF dans Adobe Reader et que vous sélectionnez du texte, vous interagissez en fait avec la couche de texte cachée, pas avec l’image. Cette approche à double couche rend possible la fonctionnalité **embed text layer PDF**.

---

## Convertir un PDF d’image numérisée avec Aspose OCR

La première chose dont vous avez besoin est une image numérisée (PNG, JPEG, TIFF) que vous souhaitez transformer en PDF. Aspose OCR peut lire cette image, exécuter l’OCR et transmettre le résultat à un générateur de PDF.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Pourquoi cela fonctionne :**  
- `setCreateSearchablePdf(true)` indique à Aspose de générer la couche de texte cachée, répondant ainsi à l’exigence **embed text layer pdf**.  
- `setCompressionLevel(9)` pousse le fichier dans la fourchette **high compression pdf**, réduisant la taille finale sans sacrifier la précision de l’OCR.  
- L’argument `RecognitionLanguage.ENGLISH` montre comment **set OCR language** ; vous pouvez le remplacer par le français, l’allemand, etc., selon votre matériel source.

---

## Paramètres PDF à haute compression

Les PDF numérisés volumineux peuvent rapidement gonfler à plusieurs centaines de mégaoctets. Aspose propose une API de compression simple qui agit au niveau du PDF. La méthode `setCompressionLevel` accepte des valeurs de 0 (pas de compression) à 9 (compression maximale).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Quelques conseils :

- **Utilisez des formats d’image sans perte** (PNG) pour les numérisations riches en texte ; le JPEG convient mieux aux photos.  
- **Activez le sous‑ensemble de polices** si vous intégrez des polices personnalisées — Aspose le fait automatiquement lorsque vous créez un PDF recherchable.  
- **Testez la taille du résultat** après chaque modification ; parfois une compression de niveau 8 vous donne une réduction de 10 % avec une perte de qualité négligeable comparée au niveau 9.

---

## Insérer une couche de texte PDF pour la recherchabilité

Si vous omettez l’appel `setCreateSearchablePdf(true)`, le fichier résultant aura l’air correct mais vous ne pourrez pas rechercher son contenu. La couche de texte cachée est créée en associant chaque caractère reconnu à sa position sur la page.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Points d’attention :**  

- **Documents multilingues** – il peut être nécessaire d’exécuter l’OCR deux fois, une fois par langue, puis de fusionner les couches de texte.  
- **Mises en page complexes** (tables, colonnes multiples) – Aspose fait un travail correct, mais vérifiez le résultat avec un visualiseur PDF qui affiche le texte caché (par ex., le mode « Edit PDF » d’Adobe Acrobat).

---

## Définir la langue OCR pour une reconnaissance précise

La précision du moteur OCR dépend de la langue que vous indiquez. Aspose fournit un ensemble de langues intégrées, et vous pouvez également ajouter des packs de langues personnalisés.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Quand changer de langue :**  

- Les documents contiennent des **scripts non latins** (cyrillique, arabe) – passez à la `RecognitionLanguage` appropriée.  
- Pages à langues mixtes – vous pouvez appeler `recognizeImageAndSave` deux fois, chaque fois avec une langue différente, puis fusionner les PDF.

---

## Exécuter l’exemple complet

Voici le programme complet, prêt à être exécuté. Remplacez les chemins factices par de vrais emplacements de fichiers, assurez‑vous que le JAR Aspose OCR est dans votre classpath, puis lancez‑le.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Sortie attendue :** Lorsque vous exécutez le programme, la console affiche :

```
Searchable PDF created.
```

Ouvrez `searchable.pdf` dans n’importe quel lecteur PDF, essayez de sélectionner du texte, et vous verrez la couche invisible en action. Vous avez réussi à **create searchable pdf** à partir d’une image numérisée.

---

![exemple de création de pdf recherchable](image-placeholder.png "exemple de création de pdf recherchable")

*La capture d’écran ci‑dessus (espace réservé) montrerait typiquement le visualiseur PDF avec du texte sélectionnable sur une page numérisée.*

---

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **create searchable PDF** avec Aspose OCR :

- Initialiser le moteur OCR.  
- **Convertir un PDF d’image numérisée** en passant un PNG/JPEG à `recognizeImageAndSave`.  
- Utiliser `setCreateSearchablePdf(true)` pour **embed text layer PDF**.  
- Appliquer `setCompressionLevel(9)` pour un **high compression PDF** qui reste léger.  
- Choisir la bonne `RecognitionLanguage` pour **set OCR language** et obtenir la meilleure précision.

À partir d’ici, vous pouvez expérimenter le traitement par lots, différentes langues, ou même combiner plusieurs pages numérisées en un seul PDF recherchable. Le même schéma fonctionne pour d’autres langues comme l’espagnol ou le japonais—il suffit de remplacer l’énumération `RecognitionLanguage`.

N’hésitez pas à laisser un commentaire si vous rencontrez des difficultés, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}