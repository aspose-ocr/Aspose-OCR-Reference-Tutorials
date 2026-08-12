---
category: general
date: 2026-02-22
description: Comment réaliser une OCR par lots d’images JPEG en C# avec Aspose.OCR.
  Apprenez à extraire le texte d’un jpg, à convertir un jpg en txt, et à traiter les
  images par lots efficacement.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: fr
og_description: Comment effectuer une reconnaissance OCR par lots d’images JPEG en
  C# avec Aspose.OCR. Ce tutoriel vous montre comment extraire du texte d’un JPG,
  convertir un JPG en TXT et traiter des images par lots en quelques minutes.
og_title: Comment effectuer une reconnaissance OCR par lots d'images JPEG en C# –
  Guide complet
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Comment effectuer une OCR par lots d'images JPEG en C# – Guide complet
url: /fr/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

Let's craft final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots d'images JPEG en C# – Guide complet

Vous vous êtes déjà demandé **comment faire une OCR par lots** d'un dossier rempli d'images sans écrire un programme séparé pour chaque fichier ? Dans ce guide, nous vous montrerons exactement **comment faire une OCR par lots** de fichiers JPEG en utilisant Aspose.OCR, afin que vous puissiez **extraire du texte d'un jpg** et **convertir un jpg en txt** avec seulement quelques lignes de code.  

Si vous avez déjà regardé un répertoire de factures numérisées en vous disant « Il doit y avoir un moyen plus rapide », vous êtes au bon endroit. Nous passerons en revue chaque étape, expliquerons pourquoi chaque élément est important, et ajouterons même quelques astuces professionnelles pour gérer de gros lots.

## Ce que vous allez créer

À la fin de ce tutoriel, vous aurez une petite application console qui :

* Analyse un répertoire donné à la recherche de fichiers `*.jpg`.  
* Envoie chaque image à travers le moteur OCR d'Aspose (accéléré par GPU si vous disposez d'une carte compatible).  
* Écrit le texte reconnu dans un fichier `.txt` placé à côté de l'image originale.  

Pas de services externes, pas de copier‑coller manuel—juste du pur C# et une bibliothèque OCR fiable.

### Prérequis

* .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.8).  
* Visual Studio 2022 ou tout éditeur supportant C#.  
* Un package NuGet Aspose.OCR (l'essai gratuit fonctionne pour les tests).  

Si l’un d’eux vous manque, faites une pause maintenant et installez‑le ; le reste du guide suppose qu’ils sont déjà en place.

![How to batch OCR example](/images/how-to-batch-ocr.png "how to batch ocr diagram")

## Étape 1 : Installer le package NuGet Aspose.OCR

First thing’s first—your project needs the OCR library. Open a terminal in the solution folder and run:

```bash
dotnet add package Aspose.OCR
```

Or use the NuGet Package Manager UI in Visual Studio. This pulls in everything you need, including the GPU‑enabled binaries if your machine supports them.

> **Astuce pro :** Si vous prévoyez d’exécuter cela sur un serveur sans GPU, définissez `UseGpu = false` plus tard ; le moteur reviendra automatiquement au CPU.

## Étape 2 : Configurer le moteur OCR

Creating and configuring the `OcrEngine` is where the magic starts. You’ll tell the engine which language to expect, whether to use the GPU, and what format the output should be.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**Pourquoi c’est important :** Définir `Language` améliore la précision car le moteur peut restreindre les jeux de caractères. Activer `UseGpu` peut réduire le temps de traitement de moitié sur une carte graphique moderne, ce qui est un vrai avantage lorsque vous **traitez des images par lots**.

## Étape 3 : Reconnaître tous les fichiers JPEG d’un dossier

Now we let Aspose do the heavy lifting. The static `BatchProcessor.RecognizeFolder` method walks the directory, runs OCR on each matching file, and returns a collection of results.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**Gestion des cas limites :** Si le dossier contient des sous‑dossiers, vous pouvez ajouter une surcharge `SearchOption.AllDirectories` (ou parcourir manuellement) pour vous assurer de ne manquer aucun fichier.

## Étape 4 : Écrire chaque résultat dans un fichier `.txt` correspondant

The `OcrResult` objects contain the original file path and the recognized text. Loop through them, change the extension, and write the output.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

That’s it—each JPEG now has a sibling text file that you can feed into downstream processes, search indexes, or simply archive.

## Étape 5 : Exécuter l’application et vérifier la sortie

Compile and run the program:

```bash
dotnet run
```

Assuming the folder contains `invoice1.jpg` and `receipt2.jpg`, you should see `invoice1.txt` and `receipt2.txt` appear alongside them. Open any of the `.txt` files; you’ll find the raw OCR output, e.g.:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

If the text looks garbled, double‑check that the source images are high‑contrast and that the `Language` property matches the document language.

## Étape 6 : Ajustements avancés (optionnel)

### a) Gestion des scans de mauvaise qualité

Sometimes JPEGs are noisy. You can pre‑process images with Aspose.Imaging or any other library:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) Paralleliser le lot

If you have many files and a multi‑core CPU, wrap the loop in `Parallel.ForEach`:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

Just be aware that the Aspose OCR engine itself isn’t thread‑safe; you’d need a separate `OcrEngine` instance per thread or use a concurrent queue.

### c) Journalisation et gestion des erreurs

A robust solution logs failures so you can retry later:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## Exemple complet fonctionnel

Putting everything together, here’s the full program you can copy‑paste into a new Console App:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

Run it, watch the console output, and then open a few `.txt` files to confirm the **extract text from jpg** step succeeded.  

---

## Conclusion

We’ve just covered **how to batch OCR** a collection of JPEG images in C# using Aspose.OCR, turning each picture into a searchable `.txt` file. The solution is compact, GPU‑aware, and easy to extend for error handling, image pre‑processing, or parallel execution.  

If you’re ready to go further, consider these next steps:

* **Traiter par lots des images** d’autres formats (`*.png`, `*.tif`) en modifiant le `searchPattern`.  
* Combinez la sortie avec un moteur de recherche en texte intégral comme Lucene.NET pour une recherche instantanée de documents.  
* Explorez les fonctionnalités de conversion PDF d’Aspose pour générer des PDF recherchables directement à partir des résultats OCR.  

Feel free to experiment—swap out the language, turn off the GPU, or pipe the text into a database. The core pattern stays the same, and now you have a solid foundation to build on.

Happy coding, and may your OCR pipelines be ever fast and accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}