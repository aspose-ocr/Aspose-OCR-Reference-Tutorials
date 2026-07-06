---
category: general
date: 2026-07-05
description: Compressez les images PDF lors de la conversion de PNG en PDF avec Java.
  Apprenez le prétraitement d'images pour l'OCR, reconnaissez le texte JPG et effectuez
  une OCR par lots vers PDF dans un seul tutoriel.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: fr
og_description: Compressez les images PDF et convertissez les PNG en PDF avec Java.
  Ce guide couvre le prétraitement d'images pour l'OCR, la reconnaissance de texte
  JPG et l'OCR par lots vers PDF.
og_title: Compresser les images PDF avec Java – Tutoriel complet d’OCR par lots
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Compresser les images PDF avec Java – Guide complet d’OCR par lots vers PDF
url: /fr/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Compresser les images PDF avec Java – Guide complet d’OCR par lots vers PDF

Vous avez déjà eu besoin de **compresser les images PDF** tout en transformant un dossier de PNG en PDF recherchables ? Vous n’êtes pas le seul. Dans de nombreuses pipelines d’automatisation, le principal point de friction est de jongler simultanément entre la qualité d’image, la précision de l’OCR et la taille finale du PDF.  

Dans ce tutoriel, nous allons parcourir une solution pratique qui **convertit PNG en PDF**, applique un **pré‑traitement d’image pour l’OCR**, puis **compresse les images PDF** afin que le résultat reste léger. À la fin, vous saurez comment **reconnaître du texte JPG**, mettre en place un workflow **batch OCR to PDF**, et garder vos PDF bien rangés.

## Ce que vous apprendrez

- Configurer Aspose OCR pour Java et appliquer une licence.  
- Configurer le moteur pour le multithreading, l’accélération GPU et la correction orthographique.  
- Construire un pipeline réutilisable de **pré‑traitement d’image pour l’OCR** (débruitage, contraste, binarisation).  
- Utiliser **PdfSaveOptions** pour **compresser les images PDF** sans sacrifier la lisibilité.  
- Parcourir un répertoire pour **convertir PNG en PDF** et **reconnaître du texte JPG** en masse.  
- Un programme Java complet, prêt à l’emploi, que vous pouvez intégrer à n’importe quel projet.

> **Prérequis** : Java 8+, Maven ou Gradle, une licence Aspose OCR pour Java, et un dossier d’images PNG/JPG que vous souhaitez traiter.

---

## Étape 1 : Appliquer la licence Aspose OCR (indispensable en production)

Avant de pouvoir appeler les API OCR, vous devez charger une licence valide ; sinon vous serez limité aux restrictions de la version d’essai.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Pourquoi c’est important* : Un moteur licencié débloque le support GPU, une précision supérieure et supprime les filigranes qui alourdiraient autrement vos fichiers PDF.

---

## Étape 2 : Configurer le moteur OCR – Threads, GPU et correction orthographique

Un moteur OCR rapide est la colonne vertébrale de tout travail **batch OCR to PDF**. Nous allons créer autant de threads que le CPU hôte peut gérer, activer l’accélération GPU (si vous avez une carte compatible) et renforcer la correction orthographique pour nettoyer les erreurs d’OCR.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Astuce pro* : Si vous exécutez sur un serveur sans tête sans GPU, il suffit de définir `gpu.setEnabled(false)` – le code fonctionnera toujours, juste un peu plus lent.

---

## Étape 3 : Construire un pipeline de pré‑traitement d’image

Les numérisations brutes souffrent souvent de bruit, de faible contraste ou d’éclairage inégal. Le **pré‑traitement d’image pour l’OCR** améliore considérablement les taux de reconnaissance, surtout dans les scénarios **reconnaître du texte JPG**.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Pourquoi nous chaînons ces étapes* : Le débruitage d’abord empêche le binarisateur d’amplifier les taches ; le contraste ensuite assure que les caractères ressortent ; enfin, la binarisation fournit au moteur OCR une image binaire propre.

---

## Étape 4 : Préparer les options d’enregistrement PDF – **Compresser les images PDF** efficacement

Aspose vous permet d’ajuster finement la sortie PDF. Nous activerons la compression d’image et définirons un niveau de qualité qui équilibre taille et lisibilité.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Résultat* : Chaque PDF recherchable sera nettement plus petit—idéal pour l’archivage ou l’envoi par courriel.

---

## Étape 5 : Traiter le dossier – **Convertir PNG en PDF** et **reconnaître du texte JPG** en une seule boucle

Nous réunissons maintenant tous les éléments. La boucle parcourt un répertoire d’entrée, exécute l’OCR sur chaque PNG ou JPG, puis écrit un PDF recherchable dans un dossier de sortie. Le nom du PDF reflète le nom de l’image source.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Résultat attendu

L’exécution du programme affiche une ligne pour chaque image, par exemple :

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Ouvrez n’importe quel PDF généré dans un lecteur et vous verrez du texte sélectionnable et recherchable, tandis que la taille du fichier est généralement **30‑50 % plus petite** qu’un équivalent non compressé.

---

## Questions fréquentes & cas particuliers

### Et si mon serveur n’a pas de GPU ?
Il suffit de définir `gpuSettings.setEnabled(false)`. Le reste du pipeline reste inchangé, et vous bénéficiez toujours du traitement multithreadé sur CPU.

### Mes PDF sont encore trop gros—puis‑je baisser davantage la qualité ?
Oui. Ajustez `options.setImageQuality(70)` ou même `50`. Des valeurs plus basses réduisent la taille plus agressivement mais peuvent flouter les glyphes fins. Testez avec un échantillon représentatif.

### Comment gérer d’autres formats d’image (TIFF, BMP) ?
Ajoutez les extensions au filtre lambda :

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Le même pipeline de pré‑traitement fonctionne pour la plupart des formats raster.

### Puis‑je conserver les images couleur d’origine au lieu de binariser ?
Remplacez `.addBinarize()` par `.addGrayscale()` dans le constructeur du pré‑processeur si vous avez besoin de conserver la couleur pour des analyses en aval.

---

## Astuces pro pour un OCR par lots prêt pour la production

- **Gestion de la mémoire** : Réutilisez une seule instance `OcrEngine` (comme montré) pour éviter le surcoût de création/destruction d’objets par image.  
- **Gestion des erreurs** : Enveloppez le bloc par fichier dans un `try/catch` afin d’enregistrer les échecs sans interrompre le traitement complet.  
- **Journalisation** : Utilisez un framework de logging approprié (SLF4J, Log4j) au lieu de `System.out.println` pour des solutions évolutives.  
- **Parallélisme** : Pour des dossiers massifs, envisagez de traiter les sous‑répertoires avec des streams parallèles, tout en surveillant la contention du GPU.  
- **Sécurité** : Stockez le fichier de licence en dehors du dépôt et protégez‑le avec des permissions système.

---

## Conclusion

Nous venons de démontrer comment **compresser les images PDF** tout en effectuant une conversion **batch OCR to PDF** qui **convertit PNG en PDF**, **reconnaît du texte JPG**, et applique un pipeline robuste de **pré‑traitement d’image pour l’OCR**. Le programme Java complet est autonome, s’exécute sur n’importe quel JDK moderne, et produit des PDF recherchables légers, prêts pour l’archivage ou l’analyse en aval.

Quelles sont les prochaines étapes ? Expérimentez avec différents paramètres de pré‑traitement, essayez des langues OCR autres que l’anglais, ou intégrez le workflow dans un micro‑service Spring Boot qui surveille un répertoire et traite les fichiers à la volée. Les concepts de base—chargement de licence, configuration du moteur, pré‑traitement et compression PDF—restent les mêmes, vous offrant une base solide pour tout projet axé sur l’OCR.

Des questions ou des ajustements à partager ? Laissez un commentaire ci‑dessous, et bon codage !

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Convert Image to Text in Java using Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}