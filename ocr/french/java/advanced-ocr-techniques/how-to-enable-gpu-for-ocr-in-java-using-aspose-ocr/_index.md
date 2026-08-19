---
category: general
date: 2026-08-18
description: Comment activer le GPU pour l'OCR en Java et reconnaître rapidement le
  texte d’une image, extraire le texte JPG, ajouter un filtre et définir la langue
  avec Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to enable gpu
- recognize image text
- extract text jpg
- how to add filter
- how to set language
language: fr
lastmod: 2026-08-18
og_description: Comment activer le GPU pour l’OCR en Java et reconnaître instantanément
  le texte d’une image, extraire le texte JPG, ajouter un filtre et définir la langue
  avec Aspose.OCR.
og_image_alt: Screenshot showing Java code that enables GPU for OCR with Aspose.OCR
og_title: Comment activer le GPU pour l'OCR en Java – guide complet d'Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-08-18'
  description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  headline: How to enable GPU for OCR in Java using Aspose.OCR
  type: TechArticle
- description: How to enable GPU for OCR in Java and quickly recognize image text,
    extract text JPG, add filter, and set language with Aspose.OCR.
  name: How to enable GPU for OCR in Java using Aspose.OCR
  steps:
  - name: 3.1 Set the OCR language
    text: '```java // Choose the language for recognition – this is the “how to set
      language” step engine.setLanguage(OcrLanguage.ENGLISH); ```'
  - name: 3.2 Add a preprocessing filter
    text: 'Noise, compression artifacts, or uneven lighting can hurt accuracy. Adding
      a denoise filter is the typical **how to add filter** approach:'
  - name: Expected output
    text: '``` Recognized text: The quick brown fox jumps over the lazy dog. ```'
  type: HowTo
tags:
- OCR
- Java
- Aspose
- GPU acceleration
title: Comment activer le GPU pour l’OCR en Java avec Aspose.OCR
url: /fr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer le GPU pour l'OCR en Java avec Aspose.OCR

Si vous avez besoin de **how to enable GPU** pour l'OCR en Java, ce guide vous accompagne pas à pas. L'activation de l'accélération GPU vous permet de **recognize image text** plusieurs fois plus rapidement, ce qui est essentiel lorsque vous devez **extract text JPG** des fichiers en masse. Nous couvrirons également **how to add filter**, **how to set language**, et comment récupérer le résultat final.

> **Prerequisite:** Java 17 ou version ultérieure, Maven, et une licence Aspose.OCR pour Java (l'essai gratuit fonctionne pour l'évaluation).

---

![Comment activer le GPU pour l'OCR en Java](/images/ocr-gpu.png){alt="Comment activer le GPU pour l'OCR en Java"}

## Ce dont vous aurez besoin

| Élément | Raison |
|------|--------|
| **Java Development Kit (JDK) 17+** | Nécessaire pour compiler et exécuter l'exemple. |
| **Maven** | Simplifie la gestion des dépendances pour Aspose.OCR. |
| **Aspose.OCR for Java** | Fournit la classe `OcrEngine` et la prise en charge du GPU. |
| **A sample JPEG image** (`sample.jpg`) | Utilisée pour démontrer **extract text JPG**. |
| **GPU‑compatible hardware** (optional but recommended) | Permet le gain de performance que nous allons configurer. |

---

## Étape 1 : Configurer le projet Maven

Créez un nouveau projet Maven (ou ajoutez‑le à un projet existant) et incluez la dépendance Aspose.OCR :

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-gpu-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <!-- Aspose.OCR for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.12</version> <!-- Use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

**Pro tip :** Gardez le numéro de version à jour ; les nouvelles versions améliorent la gestion du GPU et ajoutent des packs de langues.

---

## Étape 2 : Initialiser le moteur OCR et **how to enable GPU**

Le cœur de la solution est le `OcrEngine`. L'instancier est simple, mais vous devez activer explicitement l'accélération GPU :

```java
import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Step 2.1: Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // Step 2.2: Enable GPU acceleration (this is the “how to enable GPU” part)
        engine.setUseGpu(true); // <-- GPU is now active

        // Step 2.3: Configure language and preprocessing filter (covered later)
```

**Pourquoi activer le GPU ?**  
Lorsque `setUseGpu(true)` est appelé, Aspose.OCR décharge les noyaux de traitement d'image lourds vers la carte graphique. Sur un GPU NVIDIA/AMD moderne, la vitesse de reconnaissance peut passer d’environ 200 ms par page à moins de 80 ms, ce qui réduit considérablement le temps de traitement total pour de gros lots.

---

## Étape 3 : **How to set language** et **how to add filter**

### 3.1 Définir la langue OCR

```java
        // Choose the language for recognition – this is the “how to set language” step
        engine.setLanguage(OcrLanguage.ENGLISH);
```

Aspose.OCR est fourni avec des packs de langues pour plus de 100 langues. Remplacez `ENGLISH` par `FRENCH`, `CHINESE_SIMPLIFIED`, etc., pour correspondre à votre matériel source.

### 3.2 Ajouter un filtre de prétraitement

Le bruit, les artefacts de compression ou un éclairage inégal peuvent nuire à la précision. Ajouter un filtre de débruitage est l'approche typique **how to add filter** :

```java
        // Add a denoising filter to improve OCR quality – “how to add filter”
        engine.addPreprocessFilter(FilterType.DENOISE);
```

D'autres filtres utiles incluent `FilterType.CONTRAST`, `FilterType.BRIGHTNESS` et `FilterType.BINARIZE`. Vous pouvez chaîner plusieurs filtres en appelant `addPreprocessFilter` de façon répétée.

---

## Étape 4 : Charger l'image – **extract text JPG**

Nous pointons maintenant le moteur vers le fichier JPEG que nous voulons traiter :

```java
        // Load the JPEG image – this demonstrates “extract text JPG”
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

Remplacez `YOUR_DIRECTORY` par le chemin réel où se trouve `sample.jpg`. Aspose.OCR prend également en charge PNG, BMP, TIFF et PDF ; le même appel fonctionne pour ces formats.

---

## Étape 5 : Effectuer l'OCR et **recognize image text**

Avec le moteur configuré, invoquez la routine de reconnaissance :

```java
        // Run the OCR operation – “recognize image text”
        engine.recognize();

        // Retrieve the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);
    }
}
```

La méthode `recognize()` traite l'image sur le GPU (si activé) et remplit le tampon de texte interne. `getText()` renvoie une `String` en texte brut, que vous pouvez écrire dans un fichier, une base de données ou transmettre à des pipelines NLP en aval.

### Résultat attendu

```
Recognized text: The quick brown fox jumps over the lazy dog.
```

Si l'image contient plusieurs lignes, la chaîne renvoyée inclut les caractères de nouvelle ligne (`\n`) préservant la mise en page originale.

---

## Étape 6 : Vérifier l'utilisation du GPU (optionnel)

Pour confirmer que le GPU est réellement utilisé, activez la journalisation Aspose :

```java
        // Enable diagnostic logging (optional)
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
```

Inspectez `ocr-debug.log` après une exécution ; vous devriez voir des entrées comme `GPU device: NVIDIA GeForce RTX 3080` et `Processing time (GPU): 78 ms`. Si le journal mentionne **CPU**, revérifiez l'installation de vos pilotes et que l'appel `setUseGpu(true)` est présent.

---

## Problèmes courants et comment les éviter

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| **`java.lang.UnsatisfiedLinkError: no aspose_ocr_native`** | Bibliothèques GPU natives manquantes | Installez le dernier pilote GPU et assurez‑vous que les binaires natifs `aspose-ocr` sont sur le `java.library.path`. |
| **Poor accuracy on dark images** | Pas de filtre de prétraitement | Ajoutez `engine.addPreprocessFilter(FilterType.BRIGHTNESS)` ou augmentez `FilterType.CONTRAST`. |
| **`OutOfMemoryError` on large batches** | Épuisement de la mémoire GPU | Traitez les images par lots plus petits ou désactivez le GPU (`engine.setUseGpu(false)`) pour des résolutions très élevées. |
| **Incorrect language output** | Langue incorrecte définie | Vérifiez que `engine.setLanguage(OcrLanguage.YOUR_LANGUAGE)` correspond au texte source. |

---

## Exemple complet et exécutable

Voici la classe Java complète que vous pouvez copier‑coller dans `src/main/java/com/example/HelloWorldOcr.java`. Elle inclut toutes les étapes, la gestion des erreurs et la journalisation optionnelle.

```java
package com.example;

import com.aspose.ocr.*;

public class HelloWorldOcr {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine engine = new OcrEngine();

        // -------------------------------------------------
        // 1️⃣ Enable GPU acceleration – how to enable GPU
        // -------------------------------------------------
        engine.setUseGpu(true);

        // -------------------------------------------------
        // 2️⃣ Set language – how to set language
        // -------------------------------------------------
        engine.setLanguage(OcrLanguage.ENGLISH); // Change if needed

        // -------------------------------------------------
        // 3️⃣ Add preprocessing filter – how to add filter
        // -------------------------------------------------
        engine.addPreprocessFilter(FilterType.DENOISE);
        // Optional: engine.addPreprocessFilter(FilterType.CONTRAST);

        // -------------------------------------------------
        // 4️⃣ Load the JPEG image – extract text JPG
        // -------------------------------------------------
        String imagePath = "YOUR_DIRECTORY/sample.jpg";
        engine.setImage(ImageStream.fromFile(imagePath));

        // -------------------------------------------------
        // 5️⃣ Perform OCR – recognize image text
        // -------------------------------------------------
        engine.recognize();

        // Retrieve and display the recognized text
        String text = engine.getText();
        System.out.println("Recognized text: " + text);

        // -------------------------------------------------
        // 6️⃣ Optional: write output to a file
        // -------------------------------------------------
        java.nio.file.Files.writeString(
                java.nio.file.Paths.get("output.txt"),
                text,
                java.nio.charset.StandardCharsets.UTF_8
        );

        // -------------------------------------------------
        // 7️⃣ Optional: enable debug logging to verify GPU usage
        // -------------------------------------------------
        engine.setLogLevel(com.aspose.ocr.logging.LogLevel.DEBUG);
        engine.setLogFile("ocr-debug.log");
    }
}
```

**Exécution du programme**

```bash
mvn compile exec:java -Dexec.mainClass=com.example.HelloWorldOcr
```

Vous devriez voir le texte reconnu affiché dans la console et enregistré dans `output.txt`. Le fichier `ocr-debug.log` confirmera l’utilisation du GPU.

---

## Conclusion

Dans ce tutoriel nous avons démontré **how to enable GPU** pour Aspose.OCR en Java, comment **recognize image text**, **extract text JPG**, **how to add filter**, et **how to set language** — le tout dans un programme autonome unique. En activant le GPU, vous obtenez un gain de vitesse substantiel, tandis que les filtres et les paramètres de langue assurent une haute précision sur des sources d'images diverses.

**Étapes suivantes**

* Expérimentez avec des filtres supplémentaires tels que `FilterType.BINARIZE` pour les documents numérisés.  
* Passez à d’autres langues (`OcrLanguage.SPANISH`, `OcrLanguage.CHINESE_SIMPLIFIED`) pour élargir la prise en charge multilingue.  
* Combinez ce pipeline OCR avec Apache PDFBox pour extraire du texte directement depuis les pages PDF.  

N'hésitez pas à adapter le code pour le traitement par lots, l'intégrer dans un service Spring Boot, ou le connecter à une file de messages pour des charges de travail OCR en temps réel. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment lire du texte à partir d'une image en Java avec Aspose OCR – Guide complet](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Comment OCR du texte d'image avec langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Prétraiter l'image OCR en Java avec Aspose OCR – Améliorer la précision & extraire du texte](/ocr/english/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}