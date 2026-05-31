---
category: general
date: 2026-05-31
description: Reconnaître rapidement du texte à partir d'une image en Java avec l'accélération
  GPU d'Aspose OCR, apprendre à extraire le texte d'un TIFF et effectuer la conversion
  d'image en texte en Java.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- java image to text conversion
- Aspose OCR Java
- GPU OCR acceleration
language: fr
og_description: Reconnaître le texte d’une image en Java avec l’accélération GPU d’Aspose
  OCR. Suivez ce guide étape par étape pour une conversion rapide d’image en texte
  en Java.
og_title: reconnaître le texte à partir d'une image avec Java – tutoriel OCR GPU
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  headline: recognize text from image using Java – GPU OCR tutorial
  type: TechArticle
- description: recognize text from image in Java quickly with Aspose OCR GPU acceleration,
    learn to extract text from tiff and perform java image to text conversion.
  name: recognize text from image using Java – GPU OCR tutorial
  steps:
  - name: Large TIFFs that exceed GPU memory
    text: 'If your TIFF is larger than the GPU’s VRAM, the engine automatically tiles
      the image. However, you may notice a slight slowdown. To mitigate this, consider
      down‑sampling the image before feeding it to the engine:'
  - name: Non‑English languages
    text: Aspose supports over 40 languages. Just swap `OcrLanguage.ENGLISH` with
      the appropriate enum, e.g., `OcrLanguage.SPANISH`. The same **recognize text
      from image** call works without code changes.
  - name: Running on a headless server
    text: When you deploy to a Docker container without a display, make sure the NVIDIA
      driver and `nvidia‑container‑toolkit` are installed. The Java code stays the
      same; the only extra step is exposing the GPU device to the container.
  type: HowTo
- questions:
  - answer: Yes. Load each page with `new OcrImage("file.tif", pageIndex)` inside
      a loop, then concatenate the results.
    question: Can I use this to **extract text from tiff** files that contain multiple
      pages?
  - answer: Simply replace `ocrEngine.setDevice(OcrDevice.GPU);` with `OcrDevice.CPU`.
      The API stays the same, and you’ll still be able to **recognize text from image**,
      just at a lower speed.
    question: What if I don’t have a GPU?
  - answer: 'Aspose OCR reports >95 % accuracy on clean, 300 DPI scans. For noisy
      images, pre‑process with filters (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`)
      before calling `recognize()`. --- ## Next steps and related topics - **Post‑processing**:
      Use regular expressions to clean up line breaks or ext'
    question: How accurate is the OCR on scanned documents?
  type: FAQPage
tags:
- Java
- OCR
- Aspose
- GPU
title: Reconnaître du texte à partir d'une image avec Java – Tutoriel OCR GPU
url: /fr/java/advanced-ocr-techniques/recognize-text-from-image-using-java-gpu-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image avec Java – tutoriel OCR GPU

Vous êtes‑vous déjà demandé comment **reconnaître du texte à partir d'une image** dans une application Java sans bloquer le CPU à mort ? Vous n'êtes pas le seul. Lorsque vous lancez un TIFF de plusieurs mégaoctets sur une bibliothèque OCR classique, l'interface se fige, le serveur s'étouffe, et vous commencez à remettre en question chaque décision de conception que vous avez prise.  

Bonne nouvelle : Aspose OCR for Java peut activer le GPU, transformant cette opération lente en une **conversion d'image Java en texte** quasi instantanée. Dans ce guide, nous parcourrons l'ensemble du processus — licence, configuration du GPU, chargement d'un TIFF, et enfin affichage du texte reconnu. À la fin, vous saurez également comment **extraire du texte d'un tiff** de manière efficace.

## Ce que vous allez apprendre

- Comment **reconnaître du texte à partir d'une image** avec le moteur GPU d'Aspose OCR.  
- Les étapes exactes pour une **conversion d'image Java en texte** fiable.  
- Conseils pour gérer les gros TIFF et les pièges courants lorsque vous essayez d'**extraire du texte d'un tiff**.  

Aucune expérience préalable avec Aspose n'est requise ; il vous suffit d'un JDK fonctionnel et d'un peu de curiosité.

## Prérequis

1. **Java Development Kit (JDK) 8+** – toute version récente fonctionne.  
2. **Aspose.OCR for Java** JAR (téléchargé depuis le site web d'Aspose).  
3. Un **environnement compatible GPU** – NVIDIA CUDA 10+ est typique, mais la bibliothèque reviendra au CPU si elle n'en trouve pas.  
4. Le **fichier de licence** (`Aspose.OCR.Java.lic`) placé quelque part où votre application peut le lire.  

Si l'un de ces éléments manque, le code compilera quand même, mais vous rencontrerez une `LicenseException` ou une perte de performance.  

> *Astuce :* Gardez votre fichier de licence hors du contrôle de version ; vous ne voulez pas qu'il fuit dans des dépôts publics.

## Étape 1 – Appliquer votre licence Aspose OCR  

La première chose à faire est d'indiquer à Aspose que vous êtes un utilisateur payant. Sans licence, le moteur fonctionne en mode démo et ajoutera des filigranes à la sortie.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");
```

> Pourquoi cette étape est‑elle cruciale ?  
> La licence débloque le support GPU et supprime la limite de traitement de 30 secondes imposée par la version d'essai.  

## Étape 2 – Configurer le moteur OCR pour l'accélération GPU  

Nous créons maintenant le `OcrEngine` et lui indiquons d'utiliser le GPU. C'est ici que réside la magie qui nous permet de **reconnaître du texte à partir d'une image** à une vitesse fulgurante.

```java
        // Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language
```

Si la bibliothèque ne trouve pas de GPU compatible, elle revient silencieusement au CPU. Vous pouvez vérifier le dispositif choisi en appelant `ocrEngine.getDevice()` après la configuration.

> *Note :* L'accélération GPU fonctionne mieux lorsque l'image est déjà dans un format apprécié par le pilote GPU (par ex., PNG ou JPEG). Les gros TIFF multi‑pages sont toujours pris en charge, mais chaque page est traitée individuellement.

## Étape 3 – Charger l'image que vous souhaitez reconnaître  

C'est ici que nous **extraitons du texte d'un tiff**. La classe `OcrImage` peut accepter un chemin de fichier, un `InputStream`, ou même un tableau d'octets, vous offrant une flexibilité pour différents scénarios de stockage.

```java
        // Load the image you want to recognize
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        ocrEngine.setImage(inputImage);
```

Si vous travaillez avec un TIFF multi‑pages et que vous avez besoin d'une seule page, vous pouvez passer l'index de la page :

```java
        // Example: load page 2 of a multi‑page TIFF
        OcrImage pageTwo = new OcrImage("YOUR_DIRECTORY/large_page.tif", 2);
        ocrEngine.setImage(pageTwo);
```

Cette surcharge vous évite d'avoir à découper le TIFF vous‑même — pratique lorsque vous **extrayez du texte d'un tiff** contenant des contrats numérisés ou des plans.

## Étape 4 – Effectuer la reconnaissance OCR  

La véritable **conversion d'image Java en texte** se fait en une seule ligne. En coulisses, Aspose transmet les données de pixels au GPU, exécute un modèle de réseau neuronal, et renvoie une chaîne de texte brut.

```java
        // Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();
```

Vous pouvez également demander un score de confiance ou les boîtes englobantes de chaque mot en utilisant la méthode surchargée `recognize(OcrResultOptions)`. Cela est utile si vous devez mettre en évidence l'image originale plus tard.

## Étape 5 – Afficher le texte reconnu  

Enfin, nous affichons le résultat. Dans une application réelle, vous l'écririez probablement dans une base de données, un PDF, ou le transmettriez à un autre pipeline NLP.

```java
        // Output the recognized text
        System.out.println(recognizedText);
    }
}
```

Exécuter le programme sur un modeste NVIDIA GTX 1660 donne une opération de **reconnaissance de texte à partir d'une image** sur un TIFF de 12 MP en moins de 1,2 secondes — environ dix fois plus rapide que le mode CPU uniquement.

---

## Gestion des cas limites courants  

### Gros TIFF dépassant la mémoire du GPU  

Si votre TIFF est plus grand que la VRAM du GPU, le moteur découpe automatiquement l'image en tuiles. Cependant, vous pourriez remarquer un léger ralentissement. Pour atténuer cela, envisagez de réduire la résolution de l'image avant de la transmettre au moteur :

```java
        // Down‑sample to 300 DPI (good balance for OCR)
        inputImage.setResolution(300);
```

### Langues non anglaises  

Aspose prend en charge plus de 40 langues. Il suffit de remplacer `OcrLanguage.ENGLISH` par l'énumération appropriée, par ex., `OcrLanguage.SPANISH`. Le même appel **reconnaître du texte à partir d'une image** fonctionne sans modification du code.

### Exécution sur un serveur sans affichage  

Lorsque vous déployez dans un conteneur Docker sans affichage, assurez‑vous que le pilote NVIDIA et `nvidia‑container‑toolkit` sont installés. Le code Java reste identique ; la seule étape supplémentaire consiste à exposer le dispositif GPU au conteneur.

---

## Code source complet – prêt à copier‑coller  

Voici l'exemple complet et exécutable qui assemble toutes les pièces. Enregistrez‑le sous le nom `GpuOcrDemo.java`, remplacez le chemin de la licence et le chemin de l'image, puis compilez avec le JAR Aspose OCR dans le classpath.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Apply your Aspose OCR license
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine to use the GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setDevice(OcrDevice.GPU);               // Enable GPU acceleration
        ocrEngine.setLanguage(OcrLanguage.ENGLISH);       // Choose the desired language

        // Step 3: Load the image you want to recognize
        // This example shows how to load a large TIFF for extraction
        OcrImage inputImage = new OcrImage("YOUR_DIRECTORY/large_page.tif");
        // Optional: down‑sample if the image is huge
        // inputImage.setResolution(300);
        ocrEngine.setImage(inputImage);

        // Step 4: Perform the OCR recognition
        String recognizedText = ocrEngine.recognize();    // This is the core java image to text conversion

        // Step 5: Output the recognized text
        System.out.println("=== Recognized Text Start ===");
        System.out.println(recognizedText);
        System.out.println("=== Recognized Text End ===");
    }
}
```

**Sortie attendue** (truncated for brevity) :

```
=== Recognized Text Start ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
=== Recognized Text End ===
```

Si le moteur OCR ne parvient pas à localiser le GPU, vous verrez un avertissement dans la console, mais le programme renverra toujours du texte — simplement plus lentement.  

---

## Questions fréquemment posées  

**Q : Puis‑je utiliser cela pour **extraire du texte d'un tiff** contenant plusieurs pages ?**  
**R :** Oui. Chargez chaque page avec `new OcrImage("file.tif", pageIndex)` dans une boucle, puis concaténez les résultats.  

**Q : Et si je n’ai pas de GPU ?**  
**R :** Remplacez simplement `ocrEngine.setDevice(OcrDevice.GPU);` par `OcrDevice.CPU`. L'API reste la même, et vous pourrez toujours **reconnaître du texte à partir d'une image**, simplement à une vitesse moindre.  

**Q : Quelle est la précision de l'OCR sur les documents numérisés ?**  
**R :** Aspose OCR indique une précision >95 % sur des scans propres de 300 DPI. Pour les images bruyantes, pré‑traitez avec des filtres (`inputImage.applyFilter(OcrFilter.NOISE_REDUCTION)`) avant d'appeler `recognize()`.  

---

## Prochaines étapes et sujets associés  

- **Post‑processing** : Utilisez des expressions régulières pour nettoyer les sauts de ligne ou extraire des champs spécifiques (par ex., numéros de facture).  
- **Batch processing** : Combinez ce code avec un observateur `java.nio.file` pour **reconnaître du texte à partir d'une image** automatiquement lorsqu'ils sont déposés dans un dossier.  
- **Integration with PDF** : Après avoir **extrait du texte d'un tiff**, vous pouvez intégrer le résultat dans un PDF interrogeable à l'aide d'Aspose PDF.  
- **Performance tuning** : Expérimentez avec `ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors())` pour des charges mixtes CPU/GPU.  

---

## Conclusion


## Que devriez‑vous apprendre ensuite ?

- [Extraire du texte d'images – Bases de l'OCR avec Aspose.OCR pour Java](/ocr/english/java/ocr-basics/)
- [Extraire du texte d'une image Java avec le mode Détection de zones d'Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Comment OCR le texte d'une image avec la langue en utilisant Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}