---
category: general
date: 2026-01-07
description: Créer un PDF consultable à partir d’une image en utilisant Aspose OCR
  en Java. Apprenez comment convertir une image en PDF, reconnaître le texte d’une
  image et générer un PDF à partir d’un JPG.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- how to use ocr
- generate pdf from jpg
language: fr
og_description: Créer un PDF consultable à partir d'une image avec Aspose OCR en Java.
  Guide étape par étape pour convertir une image en PDF, reconnaître le texte de l'image
  et générer un PDF à partir d'un JPG.
og_title: Créer un PDF consultable à partir d'une image – Guide OCR Java
tags:
- OCR
- Java
- PDF
- Aspose
title: Créer un PDF consultable à partir d'une image avec OCR – Tutoriel Java
url: /fr/java/ocr-operations/create-searchable-pdf-from-image-with-ocr-java-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir d'une image avec OCR – Tutoriel Java

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d’une image numérisée mais vous ne saviez pas par où commencer ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils essaient de transformer un JPEG en un PDF réellement interrogeable.  

Dans ce guide, nous parcourrons un exemple complet et exécutable qui montre comment **convertir une image en PDF**, **reconnaître du texte à partir d’une image**, puis **générer un PDF à partir d’un JPG** en utilisant Aspose OCR for Java. Pas de références vagues, seulement du code que vous pouvez copier‑coller et exécuter dès aujourd’hui.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir les éléments suivants sur votre machine :

* **Java 17** ou une version plus récente (l’API fonctionne avec n’importe quel JDK récent).  
* Bibliothèque **Aspose.OCR for Java** — vous pouvez récupérer le JAR le plus récent depuis Maven Central ou le site d’Aspose.  
* Une image d’exemple, par ex. `sample.jpg`, placée dans un dossier que vous pouvez référencer.  
* Un IDE ou un simple éditeur de texte plus un terminal — ce qui vous convient le mieux.

C’est tout. Pas de frameworks lourds, pas de dépendances natives supplémentaires. Allons‑y.

## Étape 1 – Créer un PDF consultable : initialiser le moteur OCR

La première chose que nous faisons est d’instancier un `OcrEngine` et de le pointer vers l’image source. Cet objet est le cœur d’Aspose OCR ; il gère tout, du chargement du bitmap à l’exposition du texte reconnu.

```java
import com.aspose.ocr.*;

public class HelloOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the image you want to turn into a searchable PDF
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Pourquoi c’est important :** Initialiser correctement le moteur garantit que la bibliothèque peut lire le format d’image que vous lui fournissez. Si le chemin est incorrect, vous obtiendrez une `FileNotFoundException` et toute la chaîne s’arrêtera.

## Étape 2 – Optimiser les performances : activer le GPU, le CPU multi‑cœur et la correction orthographique

L’OCR peut être gourmand en CPU, surtout sur de gros documents. Aspose vous propose plusieurs paramètres que vous pouvez ajuster pour rendre le processus plus rapide et plus précis.

```java
        // 2️⃣ Turn on performance helpers – GPU, multi‑core CPU, and spell correction
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)                 // uses GPU if one is available
                 .setUseMultiCore(true)           // spreads work across CPU cores
                 .setEnableSpellCorrection(true); // cleans up common OCR mistakes
```

> **Astuce pro :** Si vous exécutez le code sur un serveur sans GPU, `setUseGpu(false)` ne posera aucun problème — vous reviendrez simplement au traitement multi‑cœur du CPU.

## Étape 3 – Améliorer la qualité de l’image : redressement et débruitage (facultatif mais recommandé)

Les numérisations sont rarement parfaites. Un léger angle ou du bruit peut perturber le reconnaisseur. La classe `ImageProcessingOptions` vous permet de nettoyer l’image avant que le moteur ne tente de la lire.

```java
        // 3️⃣ Pre‑process the image – straighten it and remove noise
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)   // automatically rotates tilted text
                 .setDespeckle(true); // reduces background speckles
```

> **Cas particulier :** Si votre image source est déjà propre, vous pouvez ignorer cette étape. Cela ne causera aucun dommage, mais ajoutera quelques millisecondes de surcharge.

## Étape 4 – Reconnaître le texte de l’image et générer le PDF

Le moment magique arrive. Nous appelons `recognize()` et le moteur renvoie un `OcrResult`. À partir de là, nous pouvons enregistrer le résultat dans divers formats — le PDF étant le plus courant pour les documents consultables.

```java
        // 4️⃣ Perform OCR and get the result object
        OcrResult ocrResult = ocrEngine.recognize();

        // 5️⃣ Save the result as a searchable PDF (you could also choose TXT, DOCX, etc.)
        ocrResult.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);
    }
}
```

> **Ce que vous verrez :** `sample-output.pdf` contient l’image originale en tant que couche de fond, tandis que le texte reconnu se trouve au-dessus sous forme de superposition invisible. Ouvrez‑le avec Adobe Reader et essayez de sélectionner du texte — vous serez surpris.

## Étape 5 – Vérifier la sortie du PDF consultable

Une fois le fichier écrit, il est recommandé de vérifier que le PDF est réellement consultable.

```java
import java.awt.Desktop;
import java.io.File;

public class VerifyPdf {
    public static void main(String[] args) throws Exception {
        File pdf = new File("YOUR_DIRECTORY/sample-output.pdf");
        if (pdf.exists() && Desktop.isDesktopSupported()) {
            Desktop.getDesktop().open(pdf); // opens the PDF in the default viewer
        } else {
            System.out.println("PDF not found or cannot be opened on this platform.");
        }
    }
}
```

Ouvrez le PDF, appuyez sur **Ctrl F**, tapez un mot que vous savez présent dans l’image — si la recherche le trouve, vous avez réussi à **créer un PDF consultable** !

## Utilisation de l’OCR dans des scénarios réels (Bonus)

* **Traitement par lots :** Encapsulez le code dans une boucle qui parcourt un dossier de JPG. Pensez à réutiliser une même instance de `OcrEngine` pour limiter la consommation de mémoire.  
* **Support linguistique :** Aspose OCR prend en charge plus de 60 langues. Il suffit d’appeler `ocrEngine.getEngineOptions().setLanguage(Language.English);` (ou toute autre valeur d’énumération).  
* **Gestion des erreurs :** Capturez `OcrException` pour gérer proprement les fichiers corrompus.  

Ces ajustements rendent la solution suffisamment robuste pour des pipelines de production.

## Exemple complet en Java – Créer un PDF consultable à partir d’un JPG

Voici le programme complet, autonome, que vous pouvez compiler et exécuter tel quel. Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre machine.

```java
import com.aspose.ocr.*;

public class CreateSearchablePdf {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Load the source image
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // -------------------------------------------------
        // 2️⃣ Performance helpers
        // -------------------------------------------------
        ocrEngine.getEngineOptions()
                 .setUseGpu(true)
                 .setUseMultiCore(true)
                 .setEnableSpellCorrection(true);

        // -------------------------------------------------
        // 3️⃣ Image pre‑processing (optional but helpful)
        // -------------------------------------------------
        ocrEngine.getImageProcessingOptions()
                 .setDeskew(true)
                 .setDespeckle(true);

        // -------------------------------------------------
        // 4️⃣ Run OCR and save as searchable PDF
        // -------------------------------------------------
        OcrResult result = ocrEngine.recognize();
        result.save("YOUR_DIRECTORY/sample-output.pdf", OcrOutputFormat.PDF);

        System.out.println("✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf");
    }
}
```

**Sortie attendue :**  

```
✅ Searchable PDF created at YOUR_DIRECTORY/sample-output.pdf
```

Ouvrez le PDF généré et vous devriez pouvoir rechercher n’importe quel mot présent dans `sample.jpg`. Si vous ne voyez pas la couche de texte, revérifiez le chemin de l’image et assurez‑vous que le moteur OCR ne lève pas d’exception cachée.

## Conclusion

Nous venons de vous montrer comment **créer un PDF consultable** à partir d’un JPEG en utilisant Aspose OCR for Java. De la charge de l’image, en passant par l’ajustement des paramètres de performance, le nettoyage de la photo, jusqu’à la reconnaissance du texte et l’enregistrement d’un PDF consultable — chaque étape a été expliquée avec le *pourquoi* et le *comment*.  

Vous pouvez maintenant **convertir une image en PDF**, **reconnaître du texte à partir d’une image**, et **générer un PDF à partir d’un JPG** dans vos propres applications. Prochaine étape : essayer de traiter un dossier complet de scans, expérimenter avec différentes langues, ou ajouter une protection par mot de passe au PDF de sortie. Le ciel est la limite.

Des questions sur les cas limites, la licence ou l’optimisation des performances ? Laissez un commentaire ci‑dessous, et bon codage ! 

![Diagramme illustrant le pipeline OCR – créer un PDF consultable](/images/ocr-pipeline.png "Diagramme de création d’un PDF consultable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}