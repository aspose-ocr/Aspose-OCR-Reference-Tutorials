---
category: general
date: 2026-04-29
description: Comment redresser une image et améliorer la précision de l’OCR avec Aspose
  OCR – apprenez à supprimer le bruit, augmenter le contraste de l’image et extraire
  le texte des images.
draft: false
keywords:
- how to deskew image
- remove noise from image
- boost image contrast
- extract text from image
- improve ocr accuracy
language: fr
og_description: Comment redresser une image et améliorer la précision de l’OCR. Ce
  tutoriel montre comment supprimer le bruit d’une image, augmenter le contraste de
  l’image et extraire le texte d’une image à l’aide d’Aspose OCR.
og_title: Comment redresser une image – Guide complet Aspose OCR
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Comment redresser une image – Guide de prétraitement OCR d'Aspose
url: /fr/net/ocr-optimization/how-to-deskew-image-aspose-ocr-preprocessing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment redresser une image – Guide complet Aspose OCR

Vous êtes-vous déjà demandé **comment redresser une image** avant de la soumettre à un moteur OCR ? Vous n'êtes pas le seul. Un scan de travers ou une photo prise sous un angle peut fausser la reconnaissance du texte, vous laissant avec un résultat illisible.  

Dans ce tutoriel, nous parcourrons une solution complète, de bout en bout, qui non seulement **comment redresser une image** mais aussi **supprimer le bruit d’une image**, **améliorer le contraste de l’image**, et finalement **extraire le texte d’une image** avec Aspose OCR. À la fin, vous verrez comment **améliorer la précision OCR** sans devoir fouiller dans la documentation.

> **Ce que vous obtiendrez :** une application console C# prête à l’emploi, une explication claire de chaque étape de prétraitement, et une poignée de conseils pratiques que vous pourrez copier‑coller dans vos propres projets.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Core et .NET Framework)  
- Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Une image d’exemple qui est inclinée, bruitée ou à faible contraste (par ex., `skewed_noisy.jpg`)  
- Visual Studio, VS Code ou tout éditeur C# de votre choix  

Aucune bibliothèque native supplémentaire n’est requise – Aspose gère tout en‑processus.

---

## Comment redresser une image avec Aspose OCR

La première chose dont nous avons besoin est un filtre de redressement qui corrige l’angle de rotation. Aspose OCR fournit `FilterDeskew`, qui analyse les lignes de base du texte et fait pivoter le bitmap en conséquence.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that will later recognize text.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Build an image‑processing pipeline.
        //    The order matters: deskew → denoise → contrast boost.
        ImageProcessingPipeline processingPipeline = new ImageProcessingPipeline();
        processingPipeline.Add(new FilterDeskew());          // ✅ how to deskew image
        processingPipeline.Add(new FilterDenoise());         // ✅ remove noise from image
        processingPipeline.Add(new FilterContrastBoost());   // ✅ boost image contrast

        // 3️⃣ Load your source picture.
        var sourceImage = OcrEngine.LoadImage(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // 4️⃣ Apply the pipeline – the image is now straight, cleaner, and sharper.
        var processedImage = processingPipeline.Apply(sourceImage);

        // 5️⃣ Run OCR on the cleaned‑up bitmap.
        var ocrResult = ocrEngine.Recognize(processedImage);

        // 6️⃣ Print the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Pourquoi commencer par le redressement :**  
Si les lignes de texte ne sont pas horizontales, le moteur OCR tentera d’interpréter des caractères inclinés comme des glyphes différents, ce qui réduit considérablement **améliorer la précision OCR**. Le redressement aligne les lignes de base, offrant au reconnaisseur une toile propre.

> *Astuce :* Si vous connaissez l’angle de rotation à l’avance (par ex., tous les scans sont décalés de 90°), vous pouvez ignorer le filtre et faire la rotation manuellement – c’est un petit gain de performance.

---

## Supprimer le bruit d’une image – Nettoyer le scan

Le bruit apparaît sous forme de taches noires ou blanches aléatoires (le classique motif « sel‑et‑poivre ») et peut perturber la segmentation des caractères. `FilterDenoise` applique un filtre médian qui lisse ces taches tout en préservant les contours.

```csharp
// Inside the pipeline we already added FilterDenoise.
// If you need a custom strength, you can instantiate it like:
var denoise = new FilterDenoise { Strength = 2 }; // 1‑3 are typical values
processingPipeline.Add(denoise);
```

**Quand ajuster l’intensité :**  
- **Strength = 1** – Grain léger, traitement rapide.  
- **Strength = 3** – Scans très bruités (par ex., documents faxés).  

Augmenter trop l’intensité peut flouter les traits fins, ce qui pourrait *nuire* à **améliorer la précision OCR**. Testez quelques valeurs sur un échantillon représentatif.

---

## Améliorer le contraste de l’image – Mettre en évidence les caractères faibles

Les images à faible contraste (pensez aux reçus fanés) font souvent que le moteur OCR ne détecte pas les glyphes légers. `FilterContrastBoost` étire l’histogramme de sorte que les pixels sombres deviennent plus sombres et les pixels clairs plus clairs.

```csharp
var contrast = new FilterContrastBoost { ContrastLevel = 1.5f }; // 1.0 = no change
processingPipeline.Add(contrast);
```

**Pourquoi le contraste est important :**  
Un contraste plus élevé améliore le rapport signal‑bruit, facilitant la distinction de “I” et “l” par le reconnaisseur neuronal d’Aspose. Cependant, un excès de boost peut saturer l’image, transformant les dégradés doux en bords durs qui ressemblent à des artefacts. Visez un équilibre ; 1,5‑2,0 est un bon point de départ.

---

## Extraire le texte d’une image – L’étape OCR finale

Maintenant que l’image est droite, propre et vive, le moteur OCR peut faire son travail. La méthode `Recognize` renvoie un objet `OcrResult` contenant le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin.

```csharp
var ocrResult = ocrEngine.Recognize(processedImage);
Console.WriteLine(ocrResult.Text);
```

**Exemple de sortie** (en supposant que l’image source contient « Invoice #12345 » ):

```
=== OCR Output ===
Invoice #12345
Date: 04/28/2026
Total: $1,234.56
```

Si vous constatez des caractères manquants, revérifiez la chaîne de prétraitement – il se peut que l’image nécessite encore un débruitage plus fort ou un niveau de contraste différent.  

> *Question fréquente :* « Et si je dois reconnaître une langue autre que l’anglais ? »  
> Il suffit de définir `ocrEngine.Language = Language.English;` sur une autre langue prise en charge (par ex., `Language.French`). Les étapes de prétraitement restent les mêmes.

---

## Améliorer la précision OCR – Ajustements supplémentaires

Même avec une chaîne parfaite, quelques réglages supplémentaires peuvent pousser **améliorer la précision OCR** encore plus loin :

| Astuce | Quand l’utiliser | Comment |
|--------|------------------|---------|
| **Seuil binaire** | Scans très sombres ou très clairs | `processingPipeline.Add(new FilterBinarize());` |
| **Redimensionner l’image** | Polices petites (<10 pt) | `processedImage = OcrEngine.Resize(processedImage, 2.0);` |
| **Spécifier le jeu de caractères** | Alphabet connu (chiffres uniquement, etc.) | `ocrEngine.Characters = "0123456789";` |
| **PDF multi‑pages** | Traitement par lots | Boucler sur chaque page et réutiliser la même pipeline. |

Rappelez‑vous : chaque filtre supplémentaire ajoute du temps de traitement, donc activez uniquement ce dont vous avez réellement besoin.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être compilé. Remplacez `YOUR_DIRECTORY` par le dossier contenant `skewed_noisy.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Build preprocessing pipeline
        ImageProcessingPipeline pipeline = new ImageProcessingPipeline();
        pipeline.Add(new FilterDeskew());                     // how to deskew image
        pipeline.Add(new FilterDenoise { Strength = 2 });    // remove noise from image
        pipeline.Add(new FilterContrastBoost { ContrastLevel = 1.8f }); // boost image contrast

        // Load source image
        var sourcePath = @"YOUR_DIRECTORY/skewed_noisy.jpg";
        var sourceImage = OcrEngine.LoadImage(sourcePath);

        // Apply pipeline
        var cleanImage = pipeline.Apply(sourceImage);

        // Perform OCR
        var result = ocrEngine.Recognize(cleanImage);

        // Output
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

**Résultat attendu :** texte propre et redressé affiché dans la console, avec beaucoup moins d’erreurs de reconnaissance que si vous aviez passé le fichier brut directement à `ocrEngine.Recognize`.

---

## Conclusion

Nous avons couvert **comment redresser une image**, comment **supprimer le bruit d’une image**, comment **améliorer le contraste de l’image**, et enfin comment **extraire le texte d’une image** avec Aspose OCR. En chaînant ces filtres, vous constaterez une nette amélioration de **améliorer la précision OCR**, surtout sur des scans de mauvaise qualité.

Prêt pour le prochain défi ? Essayez d’alimenter un PDF multi‑pages dans la même pipeline, ou expérimentez avec des seuils personnalisés pour la binarisation. Les mêmes principes s’appliquent – redresser, nettoyer, éclaircir, puis reconnaître.

Des questions ou un cas particulier ? Laissez un commentaire, et résolvons-le ensemble. Bon codage !  

![exemple de comment redresser une image](deskew-example.png "exemple de comment redresser une image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}