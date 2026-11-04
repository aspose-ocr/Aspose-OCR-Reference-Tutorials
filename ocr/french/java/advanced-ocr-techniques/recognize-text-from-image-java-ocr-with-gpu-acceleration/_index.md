---
category: general
date: 2026-04-29
description: Apprenez à reconnaître le texte à partir d’une image en utilisant Aspose
  OCR en Java. Comprend les étapes pour extraire le texte d’un JPG, charger l’image
  pour l’OCR et définir l’ID du dispositif GPU.
draft: false
keywords:
- recognize text from image
- extract text from jpg
- how to extract text image
- load image for OCR
- set GPU device ID
language: fr
og_description: Reconnaître du texte à partir d’une image rapidement avec Aspose OCR.
  Ce guide montre comment charger une image pour l’OCR, extraire le texte d’un JPG
  et définir l’ID du dispositif GPU.
og_title: reconnaître le texte d’une image – OCR Java avec accélération GPU
tags:
- Java
- OCR
- GPU
- Aspose
title: reconnaître le texte à partir d'une image – OCR Java avec accélération GPU
url: /fr/java/advanced-ocr-techniques/recognize-text-from-image-java-ocr-with-gpu-acceleration/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image – OCR Java avec accélération GPU

Vous avez déjà essayé de reconnaître du texte à partir d'une image et obtenu un résultat illisible ? Vous n'êtes pas seul. Dans de nombreux projets—que vous numérisiez des reçus, scanniez des passeports ou extrayiez des données d'étiquettes de produits—la qualité de l'OCR peut faire ou défaire toute la chaîne.  

La bonne nouvelle ? Avec Aspose OCR, vous pouvez **reconnaître du texte à partir d'une image** en quelques secondes, et si vous disposez d'un GPU compatible CUDA, vous pouvez encore réduire le temps de traitement. Dans ce tutoriel, nous allons parcourir le chargement d'une image pour l'OCR, l'activation de l'accélération GPU, puis l'extraction du texte d'un fichier JPG. À la fin, vous saurez exactement comment **extraire du texte à partir de fichiers jpg**, comment **définir l'ID du dispositif GPU**, et pourquoi chaque étape est importante.

## Ce dont vous avez besoin

- **Java Development Kit (JDK) 11+** – le code utilise les fonctionnalités standard du langage Java.
- **Aspose OCR for Java** library (latest version as of 2026). Vous pouvez l'obtenir depuis Maven Central ou télécharger le JAR depuis le site web d'Aspose.
- **CUDA‑enabled GPU** avec le pilote 11+ (optionnel mais fortement recommandé pour la vitesse).
- Une image d'exemple, par ex. `sample.jpg`, placée dans un dossier que vous pouvez référencer depuis votre code.

Pas de services externes, pas de clés cloud—juste un projet Java local et une machine prête pour le GPU.

## Étape 1 – Charger l'image pour l'OCR

Avant de pouvoir reconnaître du texte, vous devez fournir quelque chose à lire au moteur OCR. C’est ici que l’étape **load image for OCR** intervient.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the image
        OcrEngine engine = new OcrEngine();

        // Load a JPG file – this is the “extract text from jpg” part
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));
```

> **Pourquoi c’est important :** La méthode `ImageStream.fromFile` prend en charge de nombreux formats (JPG, PNG, BMP). Utiliser un JPG garde la taille du fichier petite, ce qui est particulièrement pratique lorsque vous traitez des centaines d'images sur un GPU.

## Étape 2 – Activer l'accélération GPU et définir l'ID du dispositif GPU

Si votre machine possède un GPU compatible CUDA, vous pouvez demander à Aspose OCR d’exécuter les calculs lourds sur la carte graphique. C’est l’étape **set GPU device ID**.

```java
        // Step 2: Enable GPU acceleration (requires CUDA 11+ and a compatible driver)
        engine.getProcessingSettings().setUseGpu(true);

        // Optional: Choose a specific GPU device (0 = first GPU)
        engine.getProcessingSettings().setGpuDeviceId(0);
```

> **Astuce :** Si vous avez plusieurs GPU, vous pouvez expérimenter avec différentes valeurs `gpuDeviceId` pour voir laquelle offre le meilleur débit. La valeur par défaut (`0`) pointe généralement vers le GPU principal.

## Étape 3 – Exécuter le processus OCR

Maintenant que l'image est chargée et que le moteur est prêt pour le travail GPU, il est temps de réellement reconnaître les caractères.

```java
        // Step 3: Run the OCR process
        OcrResult result = engine.recognize();
```

> **Que se passe-t-il en coulisses ?** Le moteur OCR divise l'image en lignes de texte, exécute un réseau de neurones sur chaque segment, puis assemble les résultats. Lorsque `setUseGpu(true)` est actif, ce réseau de neurones s'exécute sur le GPU au lieu du CPU, réduisant considérablement la latence.

## Étape 4 – Extraire et afficher le texte reconnu

La dernière pièce du puzzle est de **extraire du texte à partir d'un jpg** et de l'afficher à l'utilisateur. L'objet `OcrResult` contient le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

```java
        // Step 4: Display the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());

        // Optional: Print confidence (helps with quality checks)
        System.out.println("Overall confidence: " + result.getConfidence());
    }
}
```

### Résultat attendu

Si `sample.jpg` contient la phrase « Hello World », la console devrait afficher :

```
Recognized text:
Hello World
Overall confidence: 0.98
```

La valeur de confiance varie de 0 à 1 ; les valeurs supérieures à 0,8 sont généralement fiables pour des numérisations propres.

## Étape 5 – Variations courantes & cas limites

### Travailler avec des fichiers PNG ou BMP

Si votre image source n’est pas un JPG, changez simplement l’extension du fichier :

```java
engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.png"));
```

Le reste du flux de travail reste identique—**how to extract text image** ne dépend pas du format de fichier tant qu'Aspose le prend en charge.

### Gérer les images basse résolution

Les images basse résolution produisent souvent des scores de confiance plus faibles. Vous pouvez améliorer les résultats en :

1. Agrandissant l'image avec une bibliothèque comme OpenCV avant de la fournir à Aspose.
2. Ajustant `engine.getProcessingSettings().setResolution(300);` pour forcer une résolution DPI plus élevée lors du traitement interne.

### Exécution uniquement sur le CPU

Si vous n’avez pas de GPU compatible CUDA, sautez simplement les lignes GPU :

```java
engine.getProcessingSettings().setUseGpu(false);
```

L'OCR reviendra alors au CPU, ce qui est plus lent mais toujours parfaitement fonctionnel.

## Conseils pratiques pour la production

- **Batch Processing:** Enveloppez la logique OCR dans une boucle et réutilisez la même instance `OcrEngine`. Cela réduit la surcharge liée au chargement répété des bibliothèques natives.
- **Error Handling:** Capturez toujours `IOException` et `OcrException` pour gérer gracieusement les fichiers corrompus.
- **Memory Management:** Après le traitement, appelez `engine.dispose();` pour libérer la mémoire GPU native, surtout lors du traitement de milliers d'images.

```java
        // Clean up resources
        engine.dispose();
```

- **Logging:** Enregistrez `result.getConfidence()` avec le texte extrait. Les entrées à faible confiance peuvent être envoyées à une file de révision manuelle.

## Exemple complet fonctionnel

Ci-dessous le programme complet et autonome que vous pouvez copier‑coller dans votre IDE. Remplacez simplement `YOUR_DIRECTORY` par le chemin de votre dossier d'images.

```java
import com.aspose.ocr.*;

public class GpuExample {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine engine = new OcrEngine();

        // Load a JPG image – this is how you extract text from jpg
        engine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample.jpg"));

        // Enable GPU acceleration (requires CUDA 11+ and a compatible driver)
        engine.getProcessingSettings().setUseGpu(true);

        // Optional: Select a specific GPU device (0 = first GPU)
        engine.getProcessingSettings().setGpuDeviceId(0);

        // Run the OCR process
        OcrResult result = engine.recognize();

        // Show the recognized text
        System.out.println("Recognized text:");
        System.out.println(result.getText());

        // Show confidence for quality checks
        System.out.println("Overall confidence: " + result.getConfidence());

        // Release native resources
        engine.dispose();
    }
}
```

> **Vérification du résultat :** Comparez le texte imprimé avec l'image originale. Si la confiance est faible, envisagez les astuces de la section « Variations courantes & cas limites ».

## Conclusion

Nous venons de couvrir tout ce dont vous avez besoin pour **reconnaître du texte à partir d'une image** avec Aspose OCR en Java, du chargement du fichier à l'activation de l'accélération GPU, jusqu'à l'extraction du texte. En suivant ces étapes, vous pouvez de manière fiable **extraire du texte à partir de fichiers jpg**, contrôler quel GPU exécute la charge de travail avec **set GPU device ID**, et même adapter le flux à d'autres formats d'image.

Prêt pour le prochain défi ? Essayez d'enchaîner ce pipeline OCR avec une insertion dans une base de données, ou alimentez les résultats dans un modèle de traitement du langage naturel pour une catégorisation automatique. Les possibilités sont infinies, et le schéma de base—**load image for OCR → enable GPU → recognize → extract**—reste le même.

Si vous rencontrez des problèmes, revérifiez la version de votre pilote CUDA, assurez‑vous que le JAR Aspose OCR correspond à votre JDK, et n'oubliez pas de libérer le moteur après chaque lot. Bon codage, et que votre OCR soit toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}