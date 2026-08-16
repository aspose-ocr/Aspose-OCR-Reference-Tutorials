---
category: general
date: 2026-04-26
description: Apprenez à reconnaître le texte à partir d’une image en utilisant Aspose
  OCR avec accélération GPU en Java. Inclut la définition de la limite de mémoire
  GPU et le chargement de l’image pour les étapes d’OCR.
draft: false
keywords:
- recognize text from image
- set gpu memory limit
- load image for ocr
- Aspose OCR Java
- GPU acceleration OCR
language: fr
og_description: Découvrez comment reconnaître rapidement du texte à partir d’une image
  en utilisant l’OCR Aspose accéléré par GPU en Java. Guide étape par étape avec la
  définition de la limite de mémoire GPU et le chargement de l’image pour l’OCR.
og_title: Reconnaître le texte d’une image avec le GPU Aspose OCR (Java)
tags:
- OCR
- Java
- GPU
- Aspose
title: Reconnaître le texte d’une image avec le GPU Aspose OCR (Java)
url: /fr/java/advanced-ocr-techniques/recognize-text-from-image-with-gpu-aspose-ocr-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Reconnaître du texte à partir d'une image avec le GPU Aspose OCR (Java)

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** rapidement sur un backend Java ? Avec l’accélération GPU d’Aspose OCR, vous pouvez gagner plusieurs secondes sur chaque scan—plus besoin d’attendre que le CPU traite des mégaoctets de pixels. Dans ce tutoriel, nous allons activer le GPU, éventuellement **définir une limite de mémoire GPU**, puis **charger l’image pour l’OCR** afin d’obtenir une chaîne de texte propre en quelques lignes de code seulement.

Nous couvrirons tout ce qu’il faut pour exécuter la démo sur une carte compatible CUDA, expliquerons pourquoi chaque paramètre est important, et vous montrerons un exemple complet, prêt à l’emploi. À la fin, vous pourrez intégrer l’OCR accéléré par GPU dans n’importe quel service Java, qu’il s’agisse d’un pipeline d’ingestion de documents ou d’un backend mobile en temps réel.

## Ce dont vous avez besoin

- **Java 17** ou plus récent (le JAR Aspose OCR cible les JVM modernes)  
- Un **GPU compatible CUDA** avec au moins 2 Go de VRAM (la démo limite l’utilisation à 1024 Mo)  
- Bibliothèque **Aspose.OCR for Java** (téléchargez depuis le site Aspose ou récupérez via Maven)  
- Un fichier image que vous souhaitez traiter – de préférence un scan ou une photo haute résolution  

Aucun service externe, aucune clé cloud, juste une installation locale. Si vous n’avez pas encore de GPU, vous pouvez toujours exécuter le code ; l’appel `setUseGpu(true)` reviendra automatiquement au CPU.

## Étape 1 : Ajouter Aspose OCR à votre projet et reconnaître du texte à partir d’une image

Tout d’abord, assurez‑vous que le JAR Aspose OCR se trouve sur votre classpath. Si vous utilisez Maven, ajoutez :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Une fois la bibliothèque disponible, créez une instance d’`OcrEngine`. Cet objet est le point d’entrée pour les opérations de **reconnaître du texte à partir d’une image**.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Pourquoi instancier d’abord `OcrEngine` ? Il regroupe tous les paramètres de reconnaissance (drapeaux GPU, packs de langues, etc.) et isole chaque scan, de sorte que vous puissiez réutiliser la même instance pour plusieurs images sans fuite de mémoire.

## Étape 2 : Activer l’accélération GPU et éventuellement **définir une limite de mémoire GPU**

L’accélération GPU est la sauce secrète qui rend l’OCR à grande échelle viable. Aspose vous permet de l’activer d’un simple appel :

```java
// Step 2: Turn on GPU acceleration (requires a CUDA‑enabled GPU)
ocrEngine.getRecognitionSettings().setUseGpu(true);
```

Si votre GPU est partagé avec d’autres charges de travail, vous pouvez vouloir contraindre la quantité de VRAM que le moteur peut saisir. C’est là qu’intervient **définir une limite de mémoire GPU** :

```java
// Optional: Limit the amount of GPU memory the engine may use (in MB)
ocrEngine.getRecognitionSettings().setGpuMemoryLimit(1024);
```

Fixer un plafond de mémoire empêche les plantages « out‑of‑memory » lorsqu’on traite de nombreuses images haute résolution en parallèle. La valeur est exprimée en mégaoctets, donc `1024` signifie « utiliser au maximum 1 Go de VRAM ».

> **Astuce pro :** Sur une carte de 4 Go, une limite de 2 Go est généralement un bon compromis ; vous pouvez expérimenter avec des valeurs supérieures si vous constatez que le GPU reste inactif.

## Étape 3 : **Charger l’image pour l’OCR** – indiquer le fichier au moteur

Maintenant que le moteur est prêt, il faut lui dire quelle image scanner. Aspose accepte un chemin de fichier, un `java.io.File`, ou même un `java.awt.image.BufferedImage`. Pour la simplicité, nous utiliserons un chemin :

```java
// Step 3: Load the high‑resolution image to be processed
ocrEngine.setImage("YOUR_DIRECTORY/high_res_photo.jpg");
```

Remplacez `YOUR_DIRECTORY/high_res_photo.jpg` par le chemin réel de votre image de test. Si l’image se trouve dans votre dossier de ressources, vous pouvez utiliser `getClass().getResource("/images/sample.png").getPath()` à la place.

Pourquoi le chargement est‑il important ? Le moteur effectue une étape de pré‑traitement (redressement, binarisation) qui dépend fortement du GPU. Fournir un fichier propre et haute résolution permet au GPU de travailler efficacement et améliore la précision de **reconnaître du texte à partir d’une image**.

## Étape 4 : Exécuter la reconnaissance et récupérer la chaîne extraite

Avec le GPU activé et l’image chargée, l’appel final est simple :

```java
// Step 4: Run the recognition and retrieve the extracted text
String extractedText = ocrEngine.recognize().getText();
```

La méthode `recognize()` bloque jusqu’à ce que le GPU ait fini, puis `getText()` renvoie une `String` simple. En coulisses, Aspose utilise un modèle d’apprentissage profond qui s’exécute sur les cœurs CUDA, de sorte que la latence est généralement une fraction de ce qu’exigerait un OCR uniquement CPU.

## Étape 5 : Afficher le résultat

Imprimons la sortie OCR dans la console pour vérifier que tout fonctionne :

```java
// Step 5: Output the GPU‑accelerated OCR result
System.out.println("GPU‑accelerated result:\n" + extractedText);
```

Si tout est correctement câblé, vous verrez le texte transcrit apparaître instantanément. Sur un RTX 2060 modeste, une image de 3000 × 2000 px se traite en moins d’une seconde.

![recognize text from image using GPU Aspose OCR](/images/gpu-ocr-demo.png "GPU‑accelerated OCR demo")

*Texte alternatif de l'image :* **reconnaître du texte à partir d'une image** – capture d’écran de la sortie console après l’OCR GPU.

## Sortie attendue

L’exécution du programme complet sur un reçu d’exemple produit quelque chose du type :

```
GPU‑accelerated result:
Item      Qty   Price
Apple      2    $1.20
Banana     5    $0.75
Total          $3.75
```

Votre texte réel différera selon l’image source, mais le format ci‑dessus montre que le moteur extrait correctement les sauts de ligne et les chiffres.

## Écueils courants et conseils pratiques

| Problème | Pourquoi cela se produit | Comment le résoudre |
|----------|--------------------------|----------------------|
| **GPU non détecté** | Pilote CUDA manquant ou version du JAR incompatible | Installez le dernier pilote NVIDIA, vérifiez que `nvidia-smi` fonctionne, et utilisez Aspose OCR 23.12 ou plus récent |
| **Erreur out‑of‑memory** | Image trop grande pour la VRAM plafonnée | Augmentez `setGpuMemoryLimit` ou réduisez la résolution de l’image avant le chargement |
| **Caractères parasites** | Image floue ou à faible contraste | Pré‑traitez avec `ocrEngine.getPreprocessingSettings().setBinarization(true)` |
| **Performance lente au premier lancement** | Surcharge d’initialisation du contexte GPU | Réchauffez le moteur en traitant une petite image factice avant la charge réelle |

Rappelez‑vous, **définir une limite de mémoire GPU** est optionnel mais

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}