---
category: general
date: 2026-09-23
description: Apprenez à extraire rapidement du texte d'un fichier tiff en activant
  l'accélération GPU dans Aspose OCR for Java. Ce guide étape par étape couvre le
  chargement du TIFF, la définition de l'ID du dispositif GPU et la lecture du texte.
draft: false
keywords:
- extract text from tiff file
- gpu acceleration java
- ocr tiff java
- aspose ocr gpu
lastmod: 2026-09-23
og_description: Apprenez à extraire rapidement du texte d'un fichier tiff en activant
  l'accélération GPU dans Aspose OCR for Java. Le guide montre le chargement du TIFF,
  la sélection d'un dispositif GPU et la lecture du texte extrait.
og_image_alt: 'Tutorial image: enabling GPU for OCR in Java'
og_title: Extraire du texte d'un fichier tiff avec l'accélération GPU dans OCR Java
schemas:
- author: Aspose
  dateModified: '2026-09-23'
  description: Learn how to extract text from tiff file quickly by enabling GPU acceleration
    in Aspose OCR for Java. Step‑by‑step guide covers loading TIFF, setting GPU device
    ID, and reading text.
  headline: How to extract text from tiff file using GPU in OCR Java
  type: TechArticle
- questions:
  - answer: Absolutely—Aspose OCR runs on Windows, Linux, and macOS as long as the
      CUDA toolkit and drivers are installed.
    question: Does this work on Linux?
  - answer: Omit the `setUseGpu(true)` call or explicitly call `setUseGpu(false)`;
      the engine will run on CPU.
    question: What if I don’t have a GPU?
  - answer: Yes. `setImage` accepts JPEG, PNG, BMP, PDF, and more.
    question: Can I extract text from other formats?
  - answer: Accuracy drops sharply below 300 dpi. Pre‑process the image (binarization,
      deskew) for better results.
    question: How accurate is OCR on low‑resolution TIFFs?
  - answer: The library handles 30+ raster and document formats, including TIFF, JPEG,
      PNG, BMP, PDF, and GIF.
    question: How many formats does Aspose OCR support?
  type: FAQPage
tags:
- OCR
- Java
- GPU acceleration
title: Comment extraire du texte d'un fichier tiff avec l'accélération GPU dans OCR
  Java
url: /fr/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-and-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire du texte d'un fichier tiff en utilisant le GPU dans OCR Java

Si vous devez **extraire du texte d'un fichier tiff** rapidement, activer l'accélération GPU dans Aspose OCR for Java est la méthode la plus rapide. Dans les 100 premiers mots, nous expliquerons pourquoi le GPU est important, puis nous vous guiderons à travers le chargement d'un TIFF, l'activation du GPU, le choix éventuel d'un dispositif spécifique, l'exécution de l'OCR, et enfin la lecture du texte extrait. À la fin, vous pourrez convertir un TIFF en texte en quelques lignes de code.

## Réponses rapides
- **Quel est le principal avantage de l'OCR GPU ?** Jusqu'à 5× plus rapide pour le traitement de gros TIFF multi‑pages.  
- **Quelle version de Java est requise ?** Java 17 ou plus récent (Java 8+ fonctionne également).  
- **Ai-je besoin d'une licence spéciale ?** Une licence valide d'Aspose OCR for Java est requise pour une utilisation en production.  
- **Puis-je exécuter cela sous Linux ?** Oui—Aspose OCR est multiplateforme ; il suffit d'installer le toolkit CUDA.  
- **Le GPU est-il optionnel ?** Vous pouvez revenir au CPU en appelant `setUseGpu(false)`.

## Qu'est‑ce que OcrEngine ?
La classe `OcrEngine` est le composant central d'Aspose OCR for Java. Elle encapsule toutes les fonctionnalités d'OCR, vous permettant de charger des images, de configurer les options de traitement telles que la langue et l'utilisation du GPU, et de récupérer le texte reconnu ainsi que les données de confiance dans un objet pratique.

`OcrEngine` est la classe principale d'Aspose OCR qui représente le moteur de traitement OCR et fournit des méthodes pour charger des images, configurer les options et récupérer les résultats.

## Comment activer le GPU pour l'OCR en Java ?
Chargez votre image, activez le GPU, et appelez `recognize`—c'est tout ce dont vous avez besoin. Activer le GPU avec `setUseGpu(true)` permet au moteur de déléguer le travail intensif en pixels à la carte graphique, réduisant considérablement le temps de traitement, notamment pour les TIFF haute résolution ou multi‑pages.

## Ce dont vous aurez besoin

- Java 17 ou plus récent (le code fonctionne également avec Java 8+).  
- Aspose OCR for Java 23.10 (ou la dernière version).  
- Un GPU compatible CUDA avec le dernier pilote installé.  
- Un fichier TIFF multi‑pages d'exemple (par ex., `sample_large.tif`).  

Pas de Maven ? Déposez simplement le JAR dans votre classpath.

![How to enable GPU tutorial](gpu-ocr.png)

[How to enable GPU tutorial](gpu-ocr.png)

*Texte alternatif de l'image : Comment activer le GPU pour l'OCR en Java*

## Étape 1 : charger une image TIFF pour l'OCR

La méthode `setImage` encapsule le fichier dans un `ImageStream`, permettant au moteur de gérer les TIFF multi‑pages sans découpage manuel. Si le fichier est introuvable, une `FileNotFoundException` claire est levée.

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the TIFF file – this is where we "read text from TIFF"
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/sample_large.tif"));
```

> **Pourquoi c'est important :** L'appel `setImage` abstrait la gestion des pages, vous permettant de traiter un document complet avec une seule instance du moteur.

## Étape 2 : activer l'accélération GPU

Activer le GPU se fait via un seul drapeau booléen. Sur la plupart des systèmes, le GPU par défaut est le dispositif 0, mais vous pouvez laisser Aspose sélectionner automatiquement le dispositif optimal.

```java
        // Enable GPU acceleration (requires a supported driver)
        ocrEngine.getEngineOptions().setUseGpu(true);
```

> **Astuce :** Sur les stations de travail disposant de plusieurs GPU, spécifier l'ID du dispositif évite un basculement inattendu vers un GPU intégré plus lent.

## Étape 3 : définir l'ID du dispositif GPU (optionnel)

Si vous savez quel GPU doit gérer l'OCR—peut-être une carte IA dédiée—vous pouvez le définir explicitement avec `setGpuDeviceId`.  

```java
        // Optional: select the GPU device (0 = first device, 1 = second, etc.)
        ocrEngine.getEngineOptions().setGpuDeviceId(0);
```

> **Cas limite :** Fournir un ID invalide déclenche `IllegalArgumentException`. Utilisez `ocrEngine.getEngineOptions().getAvailableGpuDevices()` pour lister les IDs valides.

## Étape 4 : traiter l'image et extraire le texte de l'image

L'exécution de l'OCR renvoie un `OcrResult` qui contient la chaîne brute et, éventuellement, les scores de confiance.  

```java
        // Perform OCR – this is where we "convert TIFF to text"
        OcrResult ocrResult = ocrEngine.process();

        // Output the recognized text
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

### Résultat attendu

Si le TIFF contient « Hello, World! », le résultat sera similaire à :

```
Recognized text:
Hello, World!
```

Le moteur gère automatiquement les sauts de ligne, la ponctuation et la détection de mise en page de base. Pour une extraction page par page, explorez `ocrResult.getPages()`.

## Étape 5 : vérifier la sortie et gérer les problèmes courants

Le GPU peut être contourné pour plusieurs raisons. Si la version du pilote installé est antérieure à la version minimale requise, la bibliothèque ne peut pas initialiser CUDA. Un manque de mémoire vidéo peut entraîner un basculement du moteur vers le CPU, et certaines cartes graphiques intégrées ne disposent pas de la capacité de calcul nécessaire à l'accélération de l'OCR.

### Pourquoi le GPU pourrait‑il ne pas être utilisé ?

- **Incompatibilité du pilote :** Le pilote GPU doit répondre à la version minimale indiquée dans les notes de version d'Aspose.  
- **Mémoire insuffisante :** Des images très volumineuses peuvent dépasser la VRAM ; le moteur bascule alors vers le CPU et consigne un avertissement.  
- **Matériel non pris en charge :** Les graphiques intégrés manquent souvent de la capacité de calcul requise.

### Comment revenir au CPU programmatiquement

Si vous devez garantir le traitement sur CPU, appelez le setter d'option du moteur avec un drapeau false. Cela désactive toute tentative d'utilisation du GPU et force le pipeline OCR à s'exécuter entièrement sur le processeur hôte, ce qui est utile sur les machines sans cartes graphiques compatibles.

```java
if (!ocrEngine.getEngineOptions().isGpuAvailable()) {
    System.out.println("GPU not available – switching to CPU.");
    ocrEngine.getEngineOptions().setUseGpu(false);
}
```

### Lire le texte d'un TIFF dans une boucle

Lors du traitement de nombreux fichiers, parcourez un répertoire tout en maintenant l'accélération GPU activée.

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".tif"))) {
    ocrEngine.setImage(ImageStream.fromFile(file.getAbsolutePath()));
    OcrResult result = ocrEngine.process();
    System.out.println("File: " + file.getName());
    System.out.println(result.getText());
}
```

Cet extrait montre comment **lire le texte à partir de fichiers TIFF** en masse sans perdre le gain de performance.

## Questions fréquemment posées (FAQ)

**Q : Cela fonctionne‑t‑il sous Linux ?**  
R : Absolument—Aspose OCR fonctionne sous Windows, Linux et macOS tant que le toolkit CUDA et les pilotes sont installés.

**Q : Et si je n’ai pas de GPU ?**  
R : Omettez l’appel `setUseGpu(true)` ou appelez explicitement `setUseGpu(false)` ; le moteur s’exécutera sur le CPU.

**Q : Puis‑je extraire du texte d’autres formats ?**  
R : Oui. `setImage` accepte JPEG, PNG, BMP, PDF, et plus encore.

**Q : Quelle est la précision de l'OCR sur des TIFF à basse résolution ?**  
R : La précision chute fortement en dessous de 300 dpi. Pré‑traitez l'image (binarisation, redressement) pour de meilleurs résultats.

**Q : Combien de formats Aspose OCR prend‑il en charge ?**  
R : La bibliothèque gère plus de 30 formats raster et de documents, y compris TIFF, JPEG, PNG, BMP, PDF et GIF.

## Conclusion

Vous savez maintenant **comment extraire du texte d'un fichier tiff** en utilisant l'accélération GPU dans Aspose OCR for Java, comment définir un ID de dispositif GPU spécifique, et comment traiter un ou plusieurs TIFF efficacement. En basculant un seul drapeau, vous obtenez d'énormes gains de vitesse sans modifier la logique OCR.

Prochaines étapes que vous pourriez essayer :
- Traitement par lots de centaines de TIFF en threads parallèles.  
- Chargement de packs de langues personnalisés pour améliorer la reconnaissance de vocabulaires spécialisés.  
- Post‑traitement du texte extrait avec des expressions régulières pour nettoyer le formatage.

Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous. Bon codage !

---

**Dernière mise à jour :** 2026-09-23  
**Testé avec :** Aspose OCR for Java 23.10  
**Auteur :** Aspose

## Tutoriels associés

- [Comment activer le GPU pour l'OCR Java – Guide étape par étape](/ocr/java/advanced-ocr-techniques/how-to-enable-gpu-for-java-ocr-step-by-step-guide/)
- [Reconnaître du texte à partir d'une image avec Aspose OCR – Guide complet Java](/ocr/java/advanced-ocr-techniques/recognize-text-from-image-with-aspose-ocr-full-java-guide/)
- [Prétraiter l'image OCR en Java pour améliorer la précision de l'extraction de texte](/ocr/java/advanced-ocr-techniques/preprocess-image-ocr-in-java-boost-accuracy-extract-text/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}