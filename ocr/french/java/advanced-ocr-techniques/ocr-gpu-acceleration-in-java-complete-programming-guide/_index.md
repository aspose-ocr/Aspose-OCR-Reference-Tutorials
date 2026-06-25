---
category: general
date: 2026-06-25
description: L'accélération GPU de l'OCR en Java vous permet de reconnaître rapidement
  le texte à partir d'une image. Apprenez à extraire le texte d'un JPG, à définir
  la limite de mémoire GPU et à traiter l'image avec l'OCR.
draft: false
keywords:
- ocr gpu acceleration
- recognize text from image
- extract text from jpg
- set gpu memory limit
- process image with OCR
language: fr
og_description: L'accélération GPU de l'OCR en Java vous permet de reconnaître rapidement
  le texte d'une image. Découvrez comment extraire du texte d'un jpg, définir la limite
  de mémoire GPU et traiter l'image avec l'OCR.
og_title: Accélération GPU de l'OCR en Java – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: OCR GPU acceleration in Java lets you recognize text from image quickly.
    Learn to extract text from jpg, set GPU memory limit, and process image with OCR.
  headline: OCR GPU Acceleration in Java – Complete Programming Guide
  type: TechArticle
- description: OCR GPU acceleration in Java lets you recognize text from image quickly.
    Learn to extract text from jpg, set GPU memory limit, and process image with OCR.
  name: OCR GPU Acceleration in Java – Complete Programming Guide
  steps:
  - name: Point to the Image You Want to Process
    text: '```java // Step 1 – Specify the image file (can be a JPG, PNG, BMP, etc.)
      String imagePath = "YOUR_DIRECTORY/sample.jpg"; ```'
  - name: Build an OCR Configuration with GPU Support
    text: '```java // Step 2 – Create OCR configuration and turn on GPU acceleration
      OcrConfig ocrConfig = new OcrConfig() .setGpuSettings(new GpuSettings() .setEnabled(true)
      // <-- enable GPU usage .setDeviceId(0) // first GPU in the system .setMemoryLimitMb(4096));
      // optional: set GPU memory limit ```'
  - name: Instantiate the OCR Engine
    text: '```java // Step 3 – Create the OCR engine with the GPU‑enabled configuration
      AsposeOCR ocrEngine = new AsposeOCR(ocrConfig); ```'
  - name: Run the Recognition
    text: '```java // Step 4 – Perform text recognition on the chosen image ImageRecognitionResult
      result = ocrEngine.recognizeImage(imagePath); ```'
  - name: Output the Recognized Text
    text: '```java // Step 5 – Print the extracted text to the console System.out.println("Recognized
      text:

      " + result.getText()); ```'
  type: HowTo
tags:
- Java
- OCR
- GPU
title: Accélération GPU de l'OCR en Java – Guide complet de programmation
url: /fr/java/advanced-ocr-techniques/ocr-gpu-acceleration-in-java-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Accélération GPU OCR en Java – Guide de programmation complet

Vous êtes-vous déjà demandé comment **ocr gpu acceleration** peut faire gagner des secondes à votre pipeline d’extraction de texte ? Si vous avez passé des heures à faire défiler manuellement des pages de PDF numérisés ou à lutter contre un OCR lent uniquement CPU, vous n’êtes pas seul. En quelques lignes de Java, vous pouvez **recognize text from image** en un éclair, même lorsqu’il s’agit de gros JPG.

Dans ce tutoriel, nous allons parcourir un exemple réel qui vous montre comment **extract text from jpg**, configurer une limite de mémoire avec **set gpu memory limit**, et enfin **process image with OCR** à l’aide du SDK Java d’Aspose. À la fin, vous disposerez d’un programme prêt à copier‑coller qui s’exécute sur n’importe quelle machine disposant d’un GPU compatible.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir :

| Prérequis | Pourquoi c’est important |
|--------------|----------------|
| Java 17 (ou plus récent) | La bibliothèque Aspose OCR cible les JDK modernes. |
| Maven ou Gradle | Pour récupérer la dépendance `aspose-ocr`. |
| Un GPU compatible CUDA (NVIDIA) avec au moins 4 Go de VRAM | Active **ocr gpu acceleration** ; sinon le SDK revient au CPU. |
| Un fichier image (`sample.jpg`) que vous souhaitez lire | Nous allons **extract text from jpg** dans la démo. |

Si l’un de ces éléments manque, le code fonctionnera toujours—mais attendez‑vous à des performances plus lentes.

## Accélération GPU OCR – Configuration de l'environnement

Tout d’abord, ajoutez la bibliothèque Aspose OCR à votre projet. Avec Maven, cela donne :

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the latest version -->
</dependency>
```

> **Astuce :** Gardez le numéro de version à jour ; les nouvelles versions apportent souvent un meilleur support GPU et des corrections de bugs.

Une fois la dépendance résolue, vous êtes prêt à activer **ocr gpu acceleration**.

## Recognize Text from Image Using Aspose OCR

Le cœur de la solution repose sur quatre étapes simples. Décomposons‑les.

### Étape 1 : Indiquer l’image à traiter

```java
// Step 1 – Specify the image file (can be a JPG, PNG, BMP, etc.)
String imagePath = "YOUR_DIRECTORY/sample.jpg";
```

> **Pourquoi ?** Le moteur OCR a besoin d’un chemin de fichier concret ; les chemins relatifs fonctionnent aussi, tant que la JVM peut localiser le fichier.

### Étape 2 : Construire une configuration OCR avec le support GPU

```java
// Step 2 – Create OCR configuration and turn on GPU acceleration
OcrConfig ocrConfig = new OcrConfig()
        .setGpuSettings(new GpuSettings()
                .setEnabled(true)          // <-- enable GPU usage
                .setDeviceId(0)            // first GPU in the system
                .setMemoryLimitMb(4096));  // optional: set GPU memory limit
```

* `setEnabled(true)` est le commutateur qui indique à Aspose d’utiliser le GPU au lieu du CPU.  
* `setDeviceId(0)` sélectionne le premier GPU ; changez l’index si vous avez plusieurs cartes.  
* `setMemoryLimitMb(4096)` **set gpu memory limit** à 4 Go, évitant les plantages « out‑of‑memory » sur les images volumineuses. Ajustez cette valeur en fonction de votre matériel.

### Étape 3 : Instancier le moteur OCR

```java
// Step 3 – Create the OCR engine with the GPU‑enabled configuration
AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);
```

Le moteur sait maintenant qu’il doit déléguer le travail intensif au GPU, ce qui se traduit par des temps de reconnaissance plus rapides—en particulier pour les photos haute résolution.

### Étape 4 : Lancer la reconnaissance

```java
// Step 4 – Perform text recognition on the chosen image
ImageRecognitionResult result = ocrEngine.recognizeImage(imagePath);
```

En coulisses, le SDK transmet l’image au GPU, exécute un réseau de neurones convolutionnel, et renvoie un objet résultat contenant la transcription en texte brut.

### Étape 5 : Afficher le texte reconnu

```java
// Step 5 – Print the extracted text to the console
System.out.println("Recognized text:\n" + result.getText());
```

**Résultat attendu** (truncaté pour la brièveté) :

```
Recognized text:
Hello, world!
This is a sample image containing text.
```

Si le GPU n’est pas disponible, Aspose revient automatiquement en mode CPU et affiche un avertissement—ainsi votre programme ne plante jamais.

## Extract Text from JPG – Gestion des chemins de fichiers

Lorsque vous travaillez avec **extract text from jpg**, il est fréquent de rencontrer des problèmes d’encodage de chemin sous Windows. Une approche sûre consiste à utiliser `java.nio.file.Paths` :

```java
import java.nio.file.Paths;

// Convert a possibly relative path to an absolute one
String absolutePath = Paths.get(imagePath).toAbsolutePath().toString();
ImageRecognitionResult result = ocrEngine.recognizeImage(absolutePath);
```

Cette petite astuce élimine les surprises « file not found », surtout lorsque vous lancez le programme depuis un IDE plutôt que depuis la ligne de commande.

## Set GPU Memory Limit for Stable Performance

Vous vous demandez peut‑être pourquoi nous utilisons `setMemoryLimitMb`. Les GPU modernes allouent la mémoire à la demande, et un job OCR incontrôlé peut facilement consommer toute la VRAM, entraînant l’arrêt du processus. En plafonnant l’allocation :

```java
.setMemoryLimitMb(2048) // limit to 2 GB if your GPU is modest
```

vous protégez le reste de votre système d’une pénurie de ressources graphiques. Si la limite est trop basse, le SDK basculera automatiquement sur la RAM système, ce qui est plus lent mais reste fonctionnel.

> **Attention :** Fixer la limite en dessous du tampon requis par l’image peut provoquer une `GpuMemoryException`. Dans ce cas, augmentez la limite ou réduisez la résolution de l’image avant l’OCR.

## Process Image with OCR – Exemple complet de bout en bout

En réunissant tous les éléments, voici une classe complète, prête à être exécutée :

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.config.GpuSettings;
import com.aspose.ocr.config.OcrConfig;
import com.aspose.ocr.ImageRecognitionResult;
import java.nio.file.Paths;

public class GpuExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Specify the image to be processed
        String imagePath = "YOUR_DIRECTORY/sample.jpg";

        // 2️⃣ Build OCR configuration with GPU acceleration enabled
        OcrConfig ocrConfig = new OcrConfig()
                .setGpuSettings(new GpuSettings()
                        .setEnabled(true)          // enable GPU usage
                        .setDeviceId(0)            // select the first GPU device
                        .setMemoryLimitMb(4096));  // optional memory limit

        // 3️⃣ Create the OCR engine using the configured settings
        AsposeOCR ocrEngine = new AsposeOCR(ocrConfig);

        // 4️⃣ Convert to absolute path (helps when extracting text from jpg)
        String absolutePath = Paths.get(imagePath).toAbsolutePath().toString();

        // 5️⃣ Perform text recognition on the image
        ImageRecognitionResult recognitionResult = ocrEngine.recognizeImage(absolutePath);

        // 6️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + recognitionResult.getText());
    }
}
```

**Exécution du programme** :

```bash
$ mvn compile exec:java -Dexec.mainClass=GpuExample
```

Vous devriez voir s’afficher dans la console le texte contenu dans `sample.jpg`. Si vous constatez que le processus prend plus de quelques secondes, vérifiez que le pilote de votre GPU est à jour et que le drapeau `setGpuSettings().setEnabled(true)` est bien pris en compte (le journal contiendra une ligne du type *« GPU acceleration enabled – device 0 »*).

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|--------|
| **Et si je n’ai pas de GPU ?** | Le SDK revient élégamment en mode CPU. Vous pouvez toujours utiliser le même code ; il suffit de mettre `setEnabled(false)` ou d’omettre le bloc `GpuSettings`. |
| **Mon image est en résolution 8 K – cela fonctionnera‑t‑il toujours ?** | Oui, mais il se peut que vous deviez augmenter la valeur `setMemoryLimitMb` ou réduire la résolution de l’image pour éviter une `GpuMemoryException`. |
| **Puis‑je traiter un lot d’images ?** | Enveloppez l’appel de reconnaissance dans une boucle. Réutiliser la même instance `AsposeOCR` est plus efficace car le contexte GPU reste actif. |
| **Existe‑t‑il un moyen d’obtenir les scores de confiance ?** | `ImageRecognitionResult` expose `getConfidence()` pour chaque bloc reconnu ; vous pouvez journaliser ou filtrer les résultats à faible confiance. |
| **Comment passer à un autre dispositif GPU ?** | Changez `setDeviceId(1)` (ou l’indice correspondant à votre seconde carte). Utilisez `nvidia-smi` pour lister les IDs. |

## Conseils pour des déploiements prêts pour la production

1. **Warm‑up the GPU** – Exécutez une toute petite image factice une fois au démarrage ; cela évite le pic de latence du premier appel.  
2. **Thread safety** – L’instance `AsposeOCR` est thread‑safe après initialisation, vous pouvez donc la partager à travers un

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [reconnaître le texte d’une image avec Aspose OCR – Tutoriel complet Java OCR](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extraire du texte d’une image Java avec le mode Détection de zones Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Comment OCR le texte d’une image avec la langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}