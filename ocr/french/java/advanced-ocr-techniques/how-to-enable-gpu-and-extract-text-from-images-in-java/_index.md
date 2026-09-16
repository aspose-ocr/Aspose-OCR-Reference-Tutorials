---
category: general
date: 2026-09-16
description: Apprenez comment activer le GPU pour un OCR plus rapide en Java, reconnaître
  le texte à partir de fichiers image et convertir l'image en texte à l’aide d’Aspose
  OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize text from image
- extract text from image
- how to perform ocr
- convert image to text
language: fr
lastmod: 2026-09-16
og_description: Comment activer le GPU pour l’OCR en Java, reconnaître le texte à
  partir de fichiers image et convertir une image en texte avec Aspose OCR – un guide
  complet étape par étape.
og_image_alt: Screenshot showing Java code that enables GPU for OCR and extracts text
  from an image
og_title: Comment activer le GPU et extraire du texte à partir d'images en Java
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  headline: How to enable GPU and extract text from images in Java
  type: TechArticle
- description: Learn how to enable GPU for faster OCR in Java, recognize text from
    image files and convert image to text using Aspose OCR.
  name: How to enable GPU and extract text from images in Java
  steps:
  - name: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
    text: '**Pre‑processing** – de‑skew, binarize, and enhance contrast (GPU‑accelerated).'
  - name: '**Segmentation** – locate text lines, words, and characters.'
    text: '**Segmentation** – locate text lines, words, and characters.'
  - name: '**Classification** – match each character against the built‑in language
      model.'
    text: '**Classification** – match each character against the built‑in language
      model.'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Comment activer le GPU et extraire du texte d'images en Java
url: /fr/java/advanced-ocr-techniques/how-to-enable-gpu-and-extract-text-from-images-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer le GPU et extraire du texte à partir d'images en Java

Si vous avez besoin de **comment activer le GPU** pour la reconnaissance optique de caractères, ce guide vous montre les étapes exactes. En activant l'accélération GPU, vous pouvez **reconnaître du texte à partir de fichiers image** plusieurs fois plus rapidement qu'avec un traitement uniquement CPU. L'exemple utilise Aspose OCR pour Java, mais les concepts s'appliquent à toute bibliothèque OCR compatible GPU.

Dans ce tutoriel, vous apprendrez à :

* Activer l'accélération GPU dans le moteur OCR.  
* Charger une image et **extraire du texte à partir de fichiers image**.  
* **Convertir une image en texte** en quelques lignes de code seulement.  

Aucun service externe n'est requis — tout s'exécute localement sur votre machine. Un environnement de développement Java de base et la bibliothèque Aspose OCR pour Java sont les seules prérequis.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

| Exigence | Version / Détail |
|----------|------------------|
| Java Development Kit (JDK) | 8 ou plus récent |
| Maven ou Gradle (pour la gestion des dépendances) | Toute version récente |
| GPU avec support CUDA (optionnel mais recommandé) | GPU NVIDIA avec driver ≥ 450 |
| Bibliothèque Aspose OCR pour Java | 23.9 ou plus récent (téléchargement depuis le site Aspose) |

Si vous n'avez pas de GPU, le code fonctionne toujours ; il s'exécutera simplement sur le CPU.

## Étape 1 : Ajouter Aspose OCR à votre projet

Pour Maven, ajoutez la dépendance suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version>
</dependency>
```

Pour Gradle, placez ceci dans `build.gradle` :

```groovy
implementation 'com.aspose:aspose-ocr:23.9'
```

Ces entrées récupèrent automatiquement le moteur OCR ainsi que les binaires GPU natifs.

## Étape 2 : Comment activer le GPU pour le moteur OCR

La tâche principale consiste à indiquer au `OcrEngine` d'utiliser le GPU. Aspose OCR expose un drapeau simple :

```java
// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable GPU acceleration – this is the “how to enable gpu” step
ocrEngine.setGpuEnabled(true);
```

**Pourquoi c’est important :** Lorsque `setGpuEnabled(true)` est appelé, la bibliothèque charge des kernels basés sur CUDA qui parallélisent les étapes de prétraitement d'image et de segmentation des caractères. Sur une carte NVIDIA moderne, vous pouvez observer des gains de vitesse de 2 à 4 × comparé au chemin CPU par défaut.

> **Astuce pro :** Vérifiez que votre GPU est détecté en exécutant `SystemInfo.isCudaSupported()` avant d'activer le drapeau. Si la méthode renvoie `false`, le moteur reviendra automatiquement au CPU.

## Étape 3 : Charger l'image à traiter

Vous pouvez fournir au moteur OCR n'importe quel format d'image pris en charge par Aspose (JPEG, PNG, BMP, TIFF, etc.). Voici comment charger un fichier JPEG :

```java
// Load the image that contains the text to be recognized
String imagePath = "YOUR_DIRECTORY/sample.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

**Cas particulier :** Si l'image est volumineuse (plus de 5 Mo), envisagez de la redimensionner d'abord afin de réduire la consommation de mémoire. Le moteur OCR fonctionne au mieux avec des images d'environ 300 dpi.

## Étape 4 : Effectuer l'OCR et **reconnaître du texte à partir d'une image**

Une fois le moteur configuré et l'image chargée, vous pouvez lancer la reconnaissance :

```java
// Execute OCR – this is the core “how to perform ocr” step
String recognizedText = ocrEngine.recognize();
```

La méthode `recognize()` renvoie une `String` en texte brut. En interne, le moteur exécute plusieurs étapes :

1. **Pré‑traitement** – redressement, binarisation et amélioration du contraste (accéléré par GPU).  
2. **Segmentation** – localisation des lignes de texte, mots et caractères.  
3. **Classification** – correspondance de chaque caractère avec le modèle linguistique intégré.

Comme le GPU est actif, les étapes 1 et 2 bénéficient le plus de l'exécution parallèle.

## Étape 5 : Afficher ou stocker le texte extrait

Enfin, affichez le résultat dans la console, dans un fichier ou dans tout autre processeur en aval :

```java
// Show the extracted text – this completes the “convert image to text” flow
System.out.println("Recognized text:\n" + recognizedText);

// Optional: write the text to a file
Files.write(Paths.get("output.txt"), recognizedText.getBytes(StandardCharsets.UTF_8));
```

**Sortie typique** (pour une image d'exemple contenant « Hello World » ) :

```
Recognized text:
Hello World
```

Si l'OCR ne détecte aucun caractère, `recognizedText` sera une chaîne vide. Dans ce cas, revérifiez la qualité de l'image ou désactivez le GPU pour comparer les performances.

## Gestion des problèmes courants

| Problème | Cause | Solution |
|----------|-------|----------|
| **GPU non détecté** | Pilote CUDA manquant ou GPU non pris en charge | Installez le dernier pilote NVIDIA et vérifiez avec `nvidia-smi`. |
| **Caractères incorrects** | Faible contraste ou arrière‑plan bruité | Pré‑traitez l'image (par ex., augmentez le contraste) avant de la fournir au moteur. |
| **Erreur de dépassement de mémoire** | Images très grandes sur une mémoire GPU limitée | Redimensionnez l'image à ≤ 2000 px de largeur ou traitez‑la en tuiles. |
| **Mauvaise langue** | Le modèle linguistique par défaut est l'anglais alors que le texte est dans une autre langue | Appelez `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (ou l'énumération appropriée) avant `recognize()`. |

## Exemple complet, exécutable

Voici une classe Java autonome qui regroupe toutes les étapes. Enregistrez‑la sous le nom `GpuEnabledOcrExample.java`, ajustez le chemin de l'image, puis exécutez‑la avec `javac`/`java` ou via votre IDE.

```java
import com.aspose.ocr.*;
import java.nio.file.*;

public class GpuEnabledOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Turn on GPU acceleration for faster processing
        // This is the core "how to enable gpu" call
        ocrEngine.setGpuEnabled(true);

        // Optional sanity check – ensures CUDA is available
        if (!SystemInfo.isCudaSupported()) {
            System.out.println("CUDA not detected. Falling back to CPU.");
        }

        // Step 3: Load the image that contains the text to be recognized
        // Replace with the absolute path to your image file
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Perform the OCR operation and obtain the recognized text
        // This answers "how to perform ocr" and "recognize text from image"
        String recognizedText = ocrEngine.recognize();

        // Step 5: Display the extracted text – completes "convert image to text"
        System.out.println("Recognized text:\n" + recognizedText);

        // (Optional) Save the result to a text file
        Path output = Paths.get("recognized_output.txt");
        Files.write(output, recognizedText.getBytes());
        System.out.println("Text saved to " + output.toAbsolutePath());
    }
}
```

### Résultat attendu

L'exécution du programme affiche le texte extrait dans la console et écrit le même contenu dans `recognized_output.txt`. Avec le GPU activé, le temps d'exécution total pour une image de 2 MP est généralement inférieur à 200 ms sur une NVIDIA RTX 3060, contre environ 500 ms avec le seul CPU.

## Conclusion

Vous savez maintenant **comment activer le GPU** pour Aspose OCR en Java, **reconnaître du texte à partir d'images** et **convertir une image en texte** en quelques lignes de code simples. En tirant parti de l'accélération GPU, vous obtenez un traitement plus rapide, essentiel pour les applications batch ou en temps réel telles que la numérisation de factures, le traitement de reçus et la digitalisation de documents.

**Prochaines étapes**

* Expérimentez avec différents modèles linguistiques (`ocrEngine.setLanguage`) pour **extraire du texte à partir d'images** en français, allemand ou chinois.  
* Combinez la sortie OCR avec Apache Tika afin d'indexer automatiquement le contenu extrait.  
* Explorez le streaming de gros PDF page par page si vous devez **reconnaître du texte à partir d'images** à l'intérieur d'un document PDF.

N'hésitez pas à adapter l'exemple, l'intégrer à vos propres services et à partager vos résultats. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d'autres fonctionnalités de l'API et à explorer des approches d'implémentation alternatives dans vos projets.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [image to text java: Convert Image to Text with Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}