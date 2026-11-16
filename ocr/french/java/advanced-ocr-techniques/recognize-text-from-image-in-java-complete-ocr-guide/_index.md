---
category: general
date: 2026-08-12
description: Reconnaître le texte à partir d’une image en utilisant le moteur OCR
  Java. Apprenez comment extraire le texte d’une image, améliorer la précision de
  l’OCR et prétraiter l’image pour l’OCR sur des fichiers PNG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- recognize text from image
- how to extract text from image
- how to improve OCR accuracy
- how to preprocess image for OCR
- perform OCR on PNG
language: fr
lastmod: 2026-08-12
og_description: Reconnaître du texte à partir d'une image avec Java. Ce tutoriel montre
  comment extraire du texte d'une image, améliorer la précision de l'OCR et effectuer
  l'OCR sur des PNG en utilisant le multithreading et le GPU.
og_image_alt: Diagram showing Java OCR engine recognizing text from image
og_title: Reconnaître du texte à partir d'une image en Java – tutoriel OCR étape par
  étape
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  headline: recognize text from image in Java – complete OCR guide
  type: TechArticle
- description: recognize text from image using Java OCR engine. Learn how to extract
    text from image, improve OCR accuracy, and preprocess image for OCR on PNG files.
  name: recognize text from image in Java – complete OCR guide
  steps:
  - name: Explanation of each step
    text: '| Step | Why it matters | How it helps you **recognize text from image**
      | |------|----------------|-----------------------------------------------|
      | 1️⃣ Create the OCR engine | Instantiates the core component that drives all
      subsequent operations. | Provides the entry point for all OCR actions. | '
  - name: Expected output
    text: 'If `sample-image.png` contains the sentence “Hello, world! 123”, the console
      will display something similar to:'
  - name: 1. Binarization with Otsu’s method
    text: '```java import java.awt.image.BufferedImage; import com.example.image.Binarizer;
      // hypothetical helper class'
  - name: 2. Scaling to 300 dpi
    text: '```java import com.example.image.Resizer;'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Reconnaître du texte à partir d'une image en Java – guide complet d'OCR
url: /fr/java/advanced-ocr-techniques/recognize-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image en Java – guide complet OCR

Si vous devez **reconnaître du texte à partir d'une image** dans une application Java, ce tutoriel vous montre exactement comment faire. À la fin du guide, vous serez capable d'extraire du texte à partir de fichiers image, d'améliorer la précision de l'OCR et d'exécuter l'OCR sur des ressources PNG avec prise en charge multi‑cœur et GPU.

De nombreux développeurs se demandent **comment extraire du texte d'une image** sans écrire de réseau neuronal personnalisé. La solution consiste à utiliser un moteur OCR éprouvé, le configurer pour la vitesse et la précision, et appliquer les bonnes étapes de prétraitement. Les sections suivantes vous guident à travers chaque exigence, afin que vous puissiez copier le code directement dans votre projet.

## Ce que vous apprendrez

* Configurer un moteur OCR en Java.  
* Activer le multithreading et l'accélération GPU optionnelle.  
* Ajouter des packs de langues pour l'anglais et l'espagnol.  
* Appliquer des filtres de prétraitement d'image pour améliorer la qualité de reconnaissance.  
* Activer le correcteur orthographique intégré pour une sortie plus propre.  
* Effectuer l'OCR sur des fichiers PNG et afficher le texte reconnu.  

Aucun service externe n'est requis—tout fonctionne localement, ce qui le rend idéal pour les applications hors ligne ou sensibles à la confidentialité.

## Prérequis

* Java 17 ou version ultérieure (le code utilise la syntaxe moderne `var` mais peut être rétro‑porté).  
* Une bibliothèque OCR qui fournit les classes `OcrEngine`, `Language` et `EngineOptions` (par ex., **GroupDocs.Parser**, **Aspose.OCR**, ou tout SDK compatible).  
* Maven ou Gradle pour la gestion des dépendances.  
* Une image PNG d'exemple (`sample-image.png`) placée dans `YOUR_DIRECTORY`.  

> **Astuce :** Si vous prévoyez de traiter des milliers d'images, allouez suffisamment de RAM pour le tampon GPU et désactivez le correcteur orthographique uniquement lorsque vous avez besoin d'une sortie OCR brute.

## reconnaître du texte à partir d'une image avec le moteur OCR Java

Voici un programme Java complet et exécutable qui suit les huit étapes présentées dans l'extrait original. Il comprend les imports, une méthode `main`, et des commentaires en ligne qui expliquent le but de chaque ligne.

```java
// File: OcrDemo.java
import com.example.ocr.OcrEngine;            // Replace with your OCR library's package
import com.example.ocr.Language;
import com.example.ocr.EngineOptions;
import com.example.ocr.ImagePreprocessingOptions;

public class OcrDemo {

    public static void main(String[] args) {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable multi‑core processing for faster throughput
        ocrEngine.getEngineOptions().setUseMultiThreading(true);

        // Step 3: (Optional) Turn on GPU acceleration if a compatible GPU is present
        ocrEngine.getEngineOptions().setUseGpu(true);

        // Step 4: Add the languages you want to recognize (English and Spanish)
        ocrEngine.getLanguage().add(Language.English);
        ocrEngine.getLanguage().add(Language.Spanish);

        // Step 5: Apply common image‑preprocessing filters to improve OCR accuracy
        ImagePreprocessingOptions imgOpts = ocrEngine.getImagePreprocessingOptions();
        imgOpts.setRotate(true);   // Auto‑rotate based on EXIF orientation
        imgOpts.setDeskew(true);   // Straighten skewed text lines
        imgOpts.setDenoise(true);  // Reduce background noise

        // Step 6: Enable the built‑in spell corrector for cleaner output
        ocrEngine.getEngineOptions().setUseSpellCorrector(true);

        // Step 7: Perform OCR on the target PNG image
        // This demonstrates how to perform OCR on PNG files efficiently.
        String imagePath = "YOUR_DIRECTORY/sample-image.png";
        String ocrResult = ocrEngine.recognizeImage(imagePath);

        // Step 8: Output the recognized text
        System.out.println("=== OCR Result ===");
        System.out.println(ocrResult);
    }
}
```

### Explication de chaque étape

| Étape | Pourquoi c'est important | Comment cela vous aide à **reconnaître du texte à partir d'une image** |
|------|--------------------------|-----------------------------------------------|
| 1️⃣ Créer le moteur OCR | Instancie le composant principal qui pilote toutes les opérations suivantes. | Fournit le point d'entrée pour toutes les actions OCR. |
| 2️⃣ Activer le traitement multi‑cœur | Les CPU modernes ont plusieurs cœurs ; les exploiter réduit le temps de traitement total. | Accélère les traitements par lots lorsque vous **effectuez l'OCR sur des fichiers PNG** en parallèle. |
| 3️⃣ Activer l'accélération GPU (optionnel) | Les GPU excellent dans les opérations parallèles sur les pixels, surtout pour les grandes images. | Peut réduire le temps de reconnaissance jusqu'à 70 % sur le matériel supporté. |
| 4️⃣ Ajouter des packs de langues | La précision de l'OCR dépend des modèles de langue ; spécifier uniquement les langues nécessaires réduit les faux positifs. | Améliore les chances d'identifier correctement les caractères lorsque vous **comment extraire du texte d'une image** dans des scénarios multilingues. |
| 5️⃣ Prétraitement d'image | La rotation, le redressement et la réduction du bruit corrigent les problèmes de numérisation courants. | Améliore directement **comment améliorer la précision de l'OCR** en présentant un bitmap plus propre au moteur. |
| 6️⃣ Correcteur orthographique | Étape de post‑traitement qui corrige les fautes d'orthographe courantes de l'OCR. | Produit une sortie plus lisible sans nettoyage manuel. |
| 7️⃣ Effectuer l'OCR sur PNG | La méthode `recognizeImage` lit le fichier, applique le prétraitement et exécute le pipeline de reconnaissance. | Démontre **effectuer l'OCR sur PNG** tout en gérant les particularités du format (par ex., compression sans perte). |
| 8️⃣ Afficher le résultat | Vous donne un retour immédiat pour vérifier le succès. | Vous permet de confirmer que le texte a été correctement **reconnu à partir de l'image**. |

### Sortie attendue

Si `sample-image.png` contient la phrase « Hello, world! 123 », la console affichera quelque chose de similaire à :

```
=== OCR Result ===
Hello, world! 123
```

La sortie exacte peut varier légèrement selon la qualité de l'image et les paramètres de langue, mais le correcteur orthographique corrigera généralement les petites erreurs de reconnaissance comme « Helli » → « Hello ».

## comment prétraiter une image pour l'OCR – approfondissement

Bien que le code ci‑dessus utilise le prétraitement intégré du moteur, vous pouvez également appliquer des filtres personnalisés avant de transmettre l'image au moteur OCR. Voici deux techniques courantes :

### 1. Binarisation avec la méthode d'Otsu

```java
import java.awt.image.BufferedImage;
import com.example.image.Binarizer; // hypothetical helper class

BufferedImage original = ImageIO.read(new File(imagePath));
BufferedImage binary = Binarizer.otsuThreshold(original);
ocrEngine.recognizeImage(binary);
```

La binarisation convertit l'image en noir et blanc, ce qui améliore souvent **comment améliorer la précision de l'OCR** pour les numérisations à faible contraste.

### 2. Redimensionnement à 300 dpi

```java
import com.example.image.Resizer;

BufferedImage scaled = Resizer.scaleToDPI(original, 300);
ocrEngine.recognizeImage(scaled);
```

La plupart des moteurs OCR attendent au moins 300 dpi pour une reconnaissance optimale des caractères. Le redimensionnement empêche le moteur de mal lire les glyphes minuscules.

> **Note :** Si vous activez à la fois le prétraitement personnalisé et les options intégrées du moteur, le moteur appliquera ses filtres *après* les vôtres. Choisissez l'ordre qui convient le mieux aux caractéristiques de votre image.

## comment extraire du texte d'une image – gestion des cas limites

| Situation | Astuce recommandée |
|-----------|-------------------|
| **Fond très bruyant** | Augmenter l'intensité de `setDenoise(true)` ou appliquer un filtre médian avant l'OCR. |
| **Inclinaison > 15°** | Utiliser `setDeskew(true)` *et* fournir un angle de rotation manuel via `imgOpts.setRotateAngle(θ)`. |
| **Langues mixtes (par ex., anglais + espagnol)** | Ajouter les deux packs de langues comme indiqué à l'étape 4 ; le moteur changera de contexte automatiquement. |
| **Grands PDF convertis en PNG** | Traiter chaque page comme un PNG séparé et agréger les résultats ; le multithreading (étape 2) maintiendra le temps global bas. |
| **GPU non disponible** | Conserver `setUseGpu(true)` mais l'encadrer dans un try‑catch ; le moteur reviendra au CPU sans planter. |

## effectuer l'OCR sur PNG – exemple de traitement par lots

Lorsque vous devez **effectuer l'OCR sur des fichiers PNG** dans un répertoire, une boucle simple avec la même instance du moteur fonctionne bien :

```java
Path dir = Paths.get("YOUR_DIRECTORY");
try (Stream<Path> files = Files.list(dir)) {
    files.filter(p -> p.toString().endsWith(".png"))
         .forEach(p -> {
             String text = ocrEngine.recognizeImage(p.toString());
             System.out.println("File: " + p.getFileName());
             System.out.println(text);
             System.out.println("---");
         });
}
```

Comme le moteur est déjà configuré pour le multi‑cœur et le GPU, cette boucle peut traiter des dizaines d'images en parallèle sans code supplémentaire.

## Exemple complet fonctionnel

En rassemblant tous les éléments, voici une classe autonome que vous pouvez copier‑coller dans un IDE, ajouter la dépendance Maven appropriée, et exécuter immédiatement :



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment OCR le texte d'une image avec langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Extraire du texte d'une image Java avec le mode Détection de zones d'Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [image à texte java : Convertir une image en texte avec Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}