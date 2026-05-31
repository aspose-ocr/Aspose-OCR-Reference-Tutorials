---
category: general
date: 2026-05-31
description: Apprenez à reconnaître le texte à partir d’une image en C# avec Aspose
  OCR, y compris comment extraire le texte des fichiers TIFF et charger l’image pour
  l’OCR de manière efficace.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: fr
og_description: Guide étape par étape pour reconnaître le texte d’une image avec Aspose
  OCR, couvrant l’extraction depuis un TIFF et le chargement correct de l’image pour
  l’OCR.
og_title: Reconnaître du texte à partir d'une image en C# avec Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Reconnaître le texte d’une image en C# avec Aspose OCR
url: /fr/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image en C# avec Aspose OCR

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** mais vous ne saviez pas par où commencer en C# ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils traitent des documents numérisés ou des TIFF multi‑pages. Dans ce guide, nous vous présenterons un exemple complet, prêt à l'exécution, qui **reconnaît du texte à partir d'une image** en utilisant la bibliothèque Aspose OCR, et nous vous montrerons également comment **extraire du texte d'un TIFF** et la meilleure façon de **charger une image pour l'OCR** sans perdre patience.

Nous couvrirons tout, de l'installation du package NuGet à la gestion de l'accélération GPU et du retour en douceur vers le CPU si nécessaire. À la fin de ce tutoriel, vous disposerez d'une application console qui affiche le texte reconnu et le temps de traitement—sans pièces manquantes, sans références vagues.

## Ce que vous allez créer

- Une application console .NET simple qui charge une image (y compris les TIFF multi‑pages)  
- Un moteur OCR configuré pour l'utilisation du GPU, avec un retour en douceur vers le CPU  
- Extraction du texte brut de l'image, affiché dans la console  
- Informations de chronométrage afin que vous puissiez voir l'impact de performance du GPU vs. le CPU  

**Prérequis**

- .NET 6 SDK ou ultérieur (le code fonctionne avec .NET Core et .NET Framework)  
- Familiarité de base avec C# et la ligne de commande  
- Accès à Internet pour récupérer le package NuGet Aspose.OCR  

Si vous avez cela, plongeons‑y.

![Code C# pour reconnaître du texte à partir d'une image avec Aspose OCR](image.png "Code C# pour reconnaître du texte à partir d'une image avec Aspose OCR")

## Étape 1 – Reconnaître du texte à partir d'une image : Configurer le moteur OCR

Tout d'abord, nous avons besoin d'une instance `OcrEngine`. Aspose OCR vous permet de choisir le dispositif de traitement — GPU pour la rapidité, CPU comme filet de sécurité. Le moteur accepte également un indice de limite de mémoire, ce qui peut être utile sur des machines partagées.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Pourquoi c'est important :**  
Choisir `OcrDevice.Gpu` peut économiser des secondes sur le temps de reconnaissance pour les grandes images, en particulier les TIFF multi‑pages. Le `GpuMemoryLimit` empêche votre application d'absorber toute la mémoire GPU sur une station de travail partagée.

## Étape 2 – Charger une image pour l'OCR (prise en charge du TIFF)

Nous fournissons maintenant une image au moteur. `ImageStream.FromFile` d'Aspose accepte **tout** format supporté par la bibliothèque — TIFF, PNG, JPEG, etc. Cette étape répond directement à l'exigence de **charger une image pour l'OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Astuce :** Si vous travaillez avec un TIFF multi‑pages, Aspose traite automatiquement chaque page comme une trame distincte, et le moteur les traitera séquentiellement. Aucun code supplémentaire n'est nécessaire.

## Étape 3 – Lancer la reconnaissance et **extraire du texte d'un TIFF**

Avec le moteur prêt et l'image chargée, nous lançons l'opération OCR. La méthode `Recognize` renvoie un `OcrResult` qui contient le texte brut, les scores de confiance et les détails de chronométrage.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Gestion des cas limites :**  
Si le GPU n'est pas disponible, `engine.Recognize()` fonctionne toujours car le moteur bascule silencieusement vers le CPU. Vous pouvez vérifier `engine.Device` après la reconnaissance si vous devez enregistrer le dispositif réellement utilisé.

## Étape 4 – Récupérer le texte brut reconnu

Extraire le texte est simple — il suffit de lire la propriété `Text`. C'est ici que nous **extrayons finalement le texte d'un TIFF** (ou de toute autre image) et le présentons à l'utilisateur.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Vous verrez les caractères bruts, les sauts de ligne conservés tels qu'ils apparaissent dans l'image source. Pour une sortie plus structurée (comme JSON ou CSV), vous pouvez explorer `result.Regions` et `result.Lines`, mais le texte brut suffit généralement pour des scripts rapides.

## Étape 5 – Mesurer le temps de traitement et gérer le retour GPU

La performance compte, surtout lorsque vous traitez des dizaines de pages. La propriété `ProcessingTime` indique exactement la durée de l'OCR, que ce soit sur GPU ou CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Pourquoi cela vous concerne :**  
Si vous remarquez que le temps augmente, vous pouvez ajuster `GpuMemoryLimit` ou passer explicitement au CPU (`Device = OcrDevice.Cpu`). Inversement, un résultat inférieur à une seconde sur un grand TIFF signifie que votre accélération GPU fait son travail.

## Exemple complet, prêt à l'exécution

Copiez le code ci‑dessous dans un nouveau projet console (`dotnet new console -n OcrDemo`) et exécutez `dotnet add package Aspose.OCR`. Remplacez ensuite `YOUR_DIRECTORY/sample_multi_page.tif` par le chemin de votre image.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Sortie attendue (troncature pour la brièveté) :**  

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Si votre machine ne possède pas de GPU performant, le temps écoulé peut être quelques secondes de plus, mais le texte sera tout de même extrait correctement.

## Questions fréquentes & pièges

- **Et si l'image est énorme (plus de 10 Mo) ?**  
  Réduisez sa résolution avant de la fournir au moteur, ou augmentez `GpuMemoryLimit` si vous avez suffisamment de VRAM.  
- **Puis-je traiter plusieurs images dans une boucle ?**  
  Absolument. Réutilisez simplement la même instance `OcrEngine` et assignez un nouveau `ImageStream` à chaque itération.  
- **Dois-je libérer des ressources ?**  
  `OcrEngine` implémente `IDisposable`. Enveloppez-le dans un bloc `using` pour une gestion propre des ressources, surtout lorsqu'on travaille avec des ressources GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **Qu'en est‑il des langues autres que l'anglais ?**  
  Définissez `engine.Language = OcrLanguage.Spanish` (ou toute langue prise en charge) avant d'appeler `Recognize()`.

## Conclusion

Vous disposez maintenant d'une solution complète, de bout en bout, qui **reconnaît du texte à partir d'une image** en C# avec Aspose OCR. Le tutoriel a couvert comment **charger une image pour l'OCR**, comment **extraire du texte d'un TIFF**, et comment mesurer les performances tout en gérant élégamment le retour GPU.

À partir d'ici, vous pourriez :

- Expérimenter différents formats d'image (BMP, PDF) pour voir comment Aspose les gère.  
- Explorer `result.Regions` pour les données de boîte englobante si vous avez besoin d'une prise en compte de la mise en page


## Que devriez‑vous apprendre ensuite ?

- [Comment utiliser Aspose pour reconnaître une image à partir d'un flux dans la reconnaissance d'image OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extraire du texte d'une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)
- [Extraire du texte d'une image – Reconnaître la ligne avec Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}