---
category: general
date: 2026-01-02
description: Convertir des images en texte avec Java en utilisant Aspose OCR. Maîtrisez
  le traitement OCR par lots, lisez les images depuis un dossier et filtrez les fichiers
  par extension.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: fr
og_description: Convertissez rapidement des images en texte avec Java. Ce tutoriel
  couvre le traitement OCR par lots, la lecture d'images depuis un dossier et le filtrage
  des fichiers par extension.
og_title: Convertir des images en texte en Java – Guide complet d'OCR par lots
tags:
- OCR
- Java
- Aspose
title: Convertir des images en texte en Java – Guide de traitement OCR par lots
url: /fr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir des images en texte en Java – Guide de traitement OCR par lots

Vous avez déjà eu besoin de **convertir des images en texte** sans savoir comment gérer des dizaines de fichiers à la fois ? Vous n'êtes pas seul — les développeurs luttent constamment pour extraire des données de PNG, JPG et d'autres scans. La bonne nouvelle ? Avec Aspose OCR, vous pouvez créer en quelques minutes un pipeline de traitement OCR par lots, lire les images depuis des structures de dossiers, et même filtrer les fichiers par extension afin de ne travailler que sur ce qui compte.

Dans ce tutoriel, nous allons construire un programme Java autonome qui parcourt un répertoire, sélectionne chaque `.png` ou `.jpg`, envoie chaque image à Aspose OCR de façon asynchrone, et affiche le texte extrait dans l'ordre d'origine. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet nécessitant de **convertir des images en texte** à grande échelle.

---

![Convertir des images en texte exemple](https://example.com/convert-images-to-text.png "Capture d’écran de la console Java affichant le texte converti à partir de fichiers PNG")

## Ce que vous allez créer

- Un moteur `AsposeOCR` unique partagé entre les threads (efficace et thread‑safe).  
- Un `ParallelRecognizer` qui exécute les tâches OCR en parallèle, idéal pour le **traitement OCR par lots**.  
- Une logique qui **lit les images depuis un dossier** à l’aide de `java.nio.file.Files`.  
- Des filtres simples pour **extraire le texte des fichiers PNG** tout en gérant les JPG.  
- Un arrêt propre du pool de threads interne afin d’éviter les fuites de ressources.

### Prérequis

- Java 17 (ou toute version LTS récente).  
- Maven ou Gradle pour récupérer la bibliothèque Aspose OCR.  
- Un dossier rempli d’images PNG/JPG que vous souhaitez traiter.  
- Une connaissance de base des streams Java — rien de compliqué.

> **Astuce pro :** Si vous n’avez pas encore de licence, Aspose propose une clé temporaire gratuite que vous pouvez utiliser pour les tests.

---

## Étape 1 – Configurer le projet et ajouter Aspose OCR

Tout d’abord, créez un nouveau projet Maven (ou Gradle, à vous de choisir). Ajoutez la dépendance Aspose OCR dans le `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Pourquoi c’est important :** Déclarer la dépendance dès le départ garantit que le compilateur voit `AsposeOCR`, `ParallelRecognizer` et les classes associées. Cela assure également que la même version est utilisée sur toutes les machines, ce qui est crucial pour un **traitement OCR par lots** reproductible.

Une fois la construction terminée, rafraîchissez votre IDE ; vous devriez voir les packages Aspose sous `External Libraries`.

---

## Étape 2 – Convertir des images en texte – Initialiser le moteur OCR

Nous n’avons besoin que d’**une** instance du moteur OCR pour toute l’exécution. Le partager entre les threads économise de la mémoire et accélère le processus car le moteur charge les packs de langues une seule fois.

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

> **Explication :** `ParallelRecognizer` encapsule le moteur dans un pool de threads. Lorsque vous soumettez de nombreux fichiers, chacun obtient son propre thread de travail, permettant un vrai parallélisme sur les CPU multi‑cœurs.

---

## Étape 3 – Lire les images depuis le dossier – Parcourir l’arborescence du répertoire

Nous devons maintenant **lire les images depuis le dossier** et collecter chaque PNG ou JPG. L’API `Files.walk` rend cela possible en une seule ligne, mais nous ajouterons un filtre pour **extraire le texte des PNG** uniquement lorsque cela est nécessaire.

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

> **Pourquoi filtrer ici :** Utiliser `filter` nous permet de **filtrer les fichiers par extension** dès le départ, ce qui réduit les I/O inutiles plus tard. Cela rend également le code lisible — pas besoin d’expressions régulières complexes.

---

## Étape 4 – Traitement OCR par lots – Soumettre les tâches de façon asynchrone

Une fois la liste des fichiers prête, nous envoyons chaque chemin au `ParallelRecognizer`. La méthode `recognizeAsync` renvoie un `Future<OcrResult>` que nous stockons pour une récupération ultérieure.

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

> **Ce qui se passe en coulisses :** Chaque appel place une tâche dans le service d’exécution interne du reconnaisseur. Les tâches s’exécutent en parallèle, de sorte qu’un dossier contenant 100 images peut être traité en une fraction du temps qu’une boucle mono‑threadée prendrait.

---

## Étape 5 – Récupérer les résultats dans l’ordre d’origine – Conserver la séquence des fichiers

Comme nous avons stocké les `Future` dans le même ordre que `imagePaths`, il suffit d’itérer sur la liste et d’appeler `get()`. L’appel ne bloque que jusqu’à ce que l’image particulière soit terminée, préservant ainsi l’ordre sans logique supplémentaire.

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

**Exemple de sortie console** (truncée pour la brièveté) :

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

> **Gestion des cas limites :** Si une image particulière lève une exception (fichier corrompu, format non supporté), nous la capturons et continuons le traitement des autres — une habitude essentielle pour des pipelines **de traitement OCR par lots** fiables.

---

## Étape 6 – Nettoyage – Fermer le reconnaisseur

N’oubliez jamais de fermer le pool de threads interne ; sinon votre JVM peut rester bloquée à la fermeture.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

C’est tout ! Le programme parcourra désormais n’importe quel répertoire, filtrera les fichiers PNG/JPG, exécutera l’OCR en parallèle et affichera les résultats.

---

## Exemple complet fonctionnel

Voici la classe Java complète, prête à copier‑coller. Remplacez `"YOUR_DIRECTORY"` par le chemin de votre dossier d’images et exécutez‑la depuis votre IDE ou la ligne de commande.

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

Exécutez la classe, observez la console se remplir de chaînes extraites, et félicitez‑vous d’avoir **converti des images en texte** sans écrire une seule boucle bloquante sur les I/O.

---

## Questions fréquentes (FAQ)

**Q : Puis‑je également traiter des PDF ou des TIFF ?**  
R : Absolument. Aspose OCR prend en charge de nombreux formats — il suffit d’ajouter les extensions de fichiers appropriées au filtre de l’Étape 2.

**Q : Et si j’ai besoin d’une autre langue, comme l’espagnol ?**  
R : Changez `RecognitionLanguage.ENGLISH` en `RecognitionLanguage.SPANISH`. Assurez‑vous que le pack de langue est installé (Aspose inclut la plupart des langues majeures dès le départ).

**Q : Mon dossier contient des sous‑dossiers — seront‑ils analysés ?**  
R : Oui. `Files.walk` parcourt tout l’arbre de façon récursive, donc chaque PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}