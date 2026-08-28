---
category: general
date: 2026-08-28
description: Apprenez comment extraire du texte d'images png en Java en utilisant
  Aspose OCR. Ce tutoriel couvre le traitement OCR par lots, la lecture d'images depuis
  un dossier et le filtrage des fichiers par extension.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Apprenez comment extraire du texte d'images png en Java en utilisant
  Aspose OCR. Ce tutoriel couvre le traitement OCR par lots, la lecture d'images depuis
  un dossier et le filtrage des fichiers par extension.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Comment extraire du texte d'un png en Java – guide OCR par lots
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Comment extraire du texte d'un png en Java – guide OCR par lots
url: /fr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire du texte d'un PNG en Java – guide OCR par lots

Si vous avez déjà eu besoin d'**extraire du texte d'un png** fichiers mais que vous ne saviez pas comment mettre à l'échelle l'opération au-delà de quelques images, vous êtes au bon endroit. De nombreux développeurs commencent par un appel OCR sur une seule image et rencontrent rapidement des limites de performance lorsque le dossier passe à des dizaines ou des centaines de fichiers. Avec Aspose OCR for Java, vous pouvez mettre en place un pipeline OCR par lots robuste qui parcourt un répertoire, filtre uniquement les types d'images qui vous intéressent, exécute la reconnaissance en parallèle, et renvoie les résultats dans le même ordre que les fichiers source. À la fin de ce guide, vous disposerez d'un extrait Java prêt à l'emploi qui gère le **traitement OCR par lots** de manière fiable et efficace.

![Exemple de conversion d'images en texte](https://example.com/convert-images-to-text.png "Capture d'écran de la sortie console Java montrant le texte converti à partir de fichiers PNG")

## Réponses rapides
- **Quelle bibliothèque gère l'OCR ?** Aspose OCR for Java.
- **Puis-je traiter PNG et JPG ensemble ?** Yes – the sample filters both extensions.
- **Le moteur OCR est‑il thread‑safe ?** A single shared `AsposeOCR` instance is safe for concurrent use.
- **Ai‑je besoin d'une licence pour les tests ?** A free temporary key is available from Aspose.
- **Les sous‑dossiers seront‑ils scannés automatiquement ?** `Files.walk` traverses the whole tree recursively.

## Qu'est‑ce que l'extraction de texte d'un png ?

`extract text from png` désigne le processus d'application de la reconnaissance optique de caractères (OCR) aux fichiers Portable Network Graphics afin que les caractères visibles deviennent des chaînes recherchables et modifiables. Le moteur d'Aspose OCR lit les données de pixels, identifie les formes des glyphes, et renvoie du texte Unicode en un seul appel de méthode.

## Pourquoi utiliser Aspose OCR pour Java ?

Aspose OCR prend en charge **plus de 30 langues**, traite jusqu'à **500 images par minute** sur un serveur standard à 8 cœurs, et peut gérer des fichiers jusqu'à **200 Mo** sans charger l'image entière en mémoire. Ces capacités quantifiées signifient que vous pouvez exécuter de manière fiable des travaux par lots à grande échelle sur du matériel standard sans atteindre les limites de mémoire.

## Prérequis
- Java 17 (ou toute version LTS récente).
- Maven ou Gradle pour la gestion des dépendances.
- Un répertoire contenant des images PNG/JPG que vous souhaitez traiter.
- Familiarité de base avec les flux Java et le package `java.nio.file`.
- (Optionnel) Une clé de licence temporaire Aspose OCR pour l'évaluation.

> **Astuce :** La clé temporaire gratuite expire après 30 jours, mais elle vous donne un accès complet à l'API pour les tests.

## Comment le pipeline OCR par lots maintient‑il l'ordre ?

`Future<OcrResult>` représente un résultat OCR en attente qui peut être récupéré une fois le traitement terminé. Le pipeline préserve l'ordre original des fichiers en stockant les objets `Future<OcrResult>` dans une liste qui reflète l'ordre de la collection d'entrées `Path`. Lorsque vous itérez plus tard sur les futures et appelez `get()`, chaque appel ne bloque que pour son image correspondante, de sorte que la séquence de sortie correspond à la séquence d'entrée sans logique de tri supplémentaire.

## Qu'est‑ce qu'Aspose OCR pour Java ?

`AsposeOCR` est la classe principale de la bibliothèque Aspose OCR qui encapsule tous les packs de langues, les paramètres de reconnaissance et les ressources natives internes. Elle est conçue pour être instanciée une seule fois pendant la durée de vie de l'application et partagée en toute sécurité entre plusieurs threads. Comme elle charge les données de langue une seule fois, réutiliser la même instance réduit le surcoût d'initialisation et améliore le débit pour les opérations par lots.

## Comment configurer le projet et ajouter Aspose OCR

First, create a Maven (or Gradle) project and add the Aspose OCR dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Pourquoi c'est important :** Déclarer la dépendance dès le départ garantit que le compilateur peut voir `AsposeOCR`, `ParallelRecognizer` et les classes associées. Cela assure également que la même version est utilisée sur toutes les machines, ce qui est crucial pour un **traitement OCR par lots** reproductible.

Actualisez votre IDE après la fin de la construction ; vous devriez maintenant voir les packages Aspose sous **External Libraries**.

## Comment initialiser le moteur OCR – partager une seule instance

`AsposeOCR` est la classe principale du moteur OCR fournie par la bibliothèque Aspose OCR. Nous n'avons besoin que d'**une** instance du moteur OCR pour l'ensemble de l'exécution. La partager entre les threads économise de la mémoire et accélère les choses car le moteur charge les packs de langues une seule fois.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` est thread‑safe, vous pouvez donc le transmettre en toute sécurité à un `ParallelRecognizer` qui gérera un pool de threads de travail.

> **Explication :** `ParallelRecognizer` encapsule le moteur dans un pool de threads. Lorsque vous soumettez de nombreux fichiers, chacun obtient son propre thread de travail, permettant un véritable parallélisme sur les CPU multi‑cœurs.

## Comment lire les images depuis un dossier – parcourir l'arborescence du répertoire

`Files.walk` est une méthode Java NIO qui parcourt récursivement un arbre de fichiers et renvoie un flux d'objets `Path`. Nous devons maintenant **lire les images depuis le dossier** et collecter chaque PNG ou JPG. L'API `Files.walk` rend cela possible en une seule ligne, mais nous ajouterons un filtre pour **extraire du texte d'un png** uniquement lorsque nécessaire.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Pourquoi filtrer ici :** L'utilisation de `filter` nous permet de **filtrer les fichiers par extension** dès le départ, ce qui réduit les I/O inutiles plus tard. Cela rend également le code lisible — pas besoin d'expressions régulières complexes.

## Comment soumettre des tâches OCR de manière asynchrone

`recognizeAsync` soumet une image au moteur OCR pour un traitement asynchrone et renvoie un `Future<OcrResult>` représentant le résultat en attente. Avec la liste de fichiers prête, nous envoyons chaque chemin au `ParallelRecognizer`. La méthode `recognizeAsync` renvoie un `Future<OcrResult>` que nous stockons pour une récupération ultérieure.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Ce qui se passe en coulisses :** Chaque appel place une tâche dans le service d'exécution interne du recognizer. Les tâches s'exécutent en parallèle, ainsi un dossier contenant 100 images peut être traité en une fraction du temps qu'une boucle mono‑threadée prendrait.

## Comment récupérer les résultats tout en préservant la séquence des fichiers

`Future<OcrResult>` contient le résultat d'une tâche OCR asynchrone et fournit une méthode `get()` pour obtenir le texte reconnu. Comme nous avons stocké les futures dans le même ordre que `imagePaths`, nous pouvons simplement parcourir la liste et appeler `get()`. L'appel ne bloque que jusqu'à ce que l'image particulière soit terminée, préservant l'ordre sans gestion supplémentaire.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Exemple de sortie console** (truncée pour plus de concision) :

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Gestion des cas limites :** Si une image particulière lève une exception (fichier corrompu, format non pris en charge), nous l'attrapons et continuons le traitement du reste — une habitude essentielle pour des pipelines de **traitement OCR par lots** fiables.

## Comment nettoyer les ressources – arrêter le recognizer

`ParallelRecognizer.shutdown()` arrête le pool de threads interne, garantissant que toutes les tâches OCR sont terminées avant la fermeture de l'application. N'oubliez jamais d'arrêter le pool de threads interne ; sinon votre JVM pourrait rester bloquée à la sortie.

```java
recognizer.shutdown();
```

C’est tout ! Le programme parcourt désormais n'importe quel répertoire, filtre les fichiers PNG/JPG, exécute l'OCR en parallèle, et affiche les résultats dans l'ordre original.

---

## Exemple complet fonctionnel (copier‑coller)

Voici la classe Java complète, prête à être exécutée. Remplacez `"YOUR_DIRECTORY"` par le chemin de votre dossier d'images et exécutez-la depuis votre IDE ou la ligne de commande.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Exécutez la classe, observez la console se remplir de chaînes extraites, et célébrez le fait que vous avez simplement **converti des images en texte** sans écrire une seule boucle bloquante sur les I/O.

---

## Questions fréquemment posées (FAQ)

**Q : Puis‑je également traiter des PDF ou des TIFF ?**  
R : Absolument. Aspose OCR prend en charge plus de 30 formats — y compris PDF, TIFF, BMP et GIF — il suffit d'ajouter les extensions souhaitées au filtre lors de l'étape de parcours du répertoire.

**Q : Et si j'ai besoin d'une langue autre que l'anglais, comme l'espagnol ?**  
R : Changez `RecognitionLanguage.ENGLISH` en `RecognitionLanguage.SPANISH` (ou toute langue prise en charge). Les packs de langues sont fournis avec la bibliothèque, aucun téléchargement supplémentaire n'est nécessaire.

**Q : Mon dossier contient des sous‑dossiers — seront‑ils scannés ?**  
R : Oui. `Files.walk` parcourt l'arbre entier de façon récursive, donc chaque PNG/J

**Q : Comment gérer des images extrêmement grandes dépassant 200 Mo ?**  
R : Activez le mode streaming en appelant `ocrEngine.setUseStreaming(true)`. Cela indique au moteur de lire l'image par morceaux, réduisant considérablement l'utilisation maximale de la mémoire.

**Q : Existe‑t‑il un moyen de limiter le nombre de threads OCR concurrents ?**  
R : Oui. Lors de la construction de `ParallelRecognizer`, passez le nombre maximal de threads souhaité comme deuxième argument (par ex., `new ParallelRecognizer(ocrEngine, 4)`).

---

**Dernière mise à jour :** 2026-08-28  
**Testé avec :** Aspose OCR for Java 24.10  
**Auteur :** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Tutoriels associés

- [Convertir des images en texte dans le guide de traitement OCR par lots Java](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Lire le texte d'une image en Java – Guide complet Aspose OCR](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Extraire du texte d'images avec Aspose.OCR – Caractères autorisés](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}