---
category: general
date: 2026-04-29
description: Effectuez rapidement la reconnaissance optique de caractères (OCR) d'images
  par lots avec Aspose OCR en C#. Apprenez comment extraire du texte à partir de fichiers
  jpg, lire le texte des numérisations et traiter la liste d'images en parallèle.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: fr
og_description: Effectuez rapidement la reconnaissance OCR d'images par lots avec
  Aspose OCR. Ce guide montre comment extraire du texte à partir de fichiers JPG,
  lire le texte des numérisations et traiter une liste d'images en parallèle.
og_title: Traitement OCR par lots d'images en C# – OCR parallèle de scans JPG
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Traitement OCR par lots d'images en C# – OCR parallèle de scans JPG
url: /fr/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Traitement par lots d'images OCR en C# – OCR parallèle de scans JPG

Vous avez déjà eu besoin de **batch OCR images** mais vous n'étiez pas sûr de la façon de mettre à l'échelle le travail sur plusieurs fichiers ? Vous n'êtes pas seul—les développeurs rencontrent souvent un obstacle lorsqu'ils essaient de lire le texte des scans un par un. La bonne nouvelle, c'est qu'avec Aspose OCR vous pouvez **extract text from jpg** files, **read text from scans**, et **process image list** items en parallèle avec seulement quelques lignes de C#.

Dans ce tutoriel, nous allons parcourir un exemple complet, prêt à l'exécution, qui montre exactement comment procéder. À la fin, vous disposerez d’une application console autonome qui reconnaît un dossier de scans JPEG, affiche le texte de chaque page et indique la durée de chaque opération. Aucun document externe à rechercher, aucun extrait de code à moitié rempli—juste une solution complète que vous pouvez glisser dans Visual Studio et exécuter.

## Ce dont vous aurez besoin

- **.NET 6.0** ou version ultérieure (le code se compile également sur .NET Framework 4.6+)
- **Aspose.OCR** package NuGet (`Install-Package Aspose.OCR`)
- Une poignée de fichiers JPG ou d'images scannées que vous souhaitez traiter
- L'IDE de votre choix ; j'utilise Visual Studio 2022, mais VS Code fonctionne aussi très bien

C’est tout. Si vous avez déjà le package NuGet, vous êtes prêt à démarrer.

## Étape 1 – Initialiser le moteur OCR (Batch OCR Images Setup)

La première chose que nous faisons est de créer une instance `OcrEngine` et d'indiquer la langue à rechercher. Dans la plupart des cas, l'anglais suffit, mais vous pouvez remplacer `OcrLanguage.English` par n'importe quelle langue prise en charge.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Pourquoi c’est important :* Initialiser le moteur une fois et le réutiliser pour toutes les images est beaucoup plus efficace que de créer une nouvelle instance par fichier. Cela permet également à Aspose de partager des ressources internes, ce qui est essentiel pour le **parallel OCR processing**.

## Étape 2 – Construire la liste d'images (Process Image List)

Ensuite, nous définissons la collection de chemins de fichiers que nous voulons fournir au reconnaisseur par lots. Vous pouvez générer cette liste dynamiquement avec `Directory.GetFiles`, mais pour plus de clarté, nous allons coder en dur quelques entrées.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Astuce :* Si vous avez des milliers de scans, envisagez d'utiliser `Directory.EnumerateFiles` avec un filtre comme `*.jpg` afin d'éviter de charger toute la liste en mémoire d'un coup.

## Étape 3 – Exécuter la reconnaissance par lots (Parallel OCR Processing)

Voici le cœur du sujet : appeler `BatchRecognize`. La méthode accepte un argument `maxDegreeOfParallelism`, qui contrôle le nombre de threads qu'Aspose va créer. Par défaut, elle utilise quatre threads, mais vous pouvez augmenter ce nombre si votre CPU possède plus de cœurs.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*Que se passe-t-il en coulisses ?* Aspose divise la collection `imagePaths` en blocs, attribue chaque bloc à un thread séparé, puis agrège les résultats. C’est la façon la plus efficace d’**extract text from jpg** files lorsque vous avez un **process image list** qui peut être traité simultanément.

## Étape 4 – Afficher les résultats (Read Text from Scans)

Enfin, nous parcourons la collection `recognitionResults` et affichons le texte et le temps de traitement de chaque fichier. L'objet `OcrResult` fournit également le nom du fichier source, ce qui aide lorsqu’il faut journaliser ou stocker la sortie.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Sortie attendue (exemple) :**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Remarquez comment chaque bloc indique le nom du fichier, la durée de l’OCR et le texte extrait. C’est exactement l’information dont vous avez besoin lorsque vous **read text from scans** dans une chaîne de production.

## Gestion des cas limites courants

| Situation | Ce qu’il faut surveiller | Solution rapide |
|-----------|--------------------------|-----------------|
| **Fichier manquant** | `FileNotFoundException` levée à l’intérieur de `BatchRecognize` | Validez les chemins avec `File.Exists` avant de les ajouter à `imagePaths`. |
| **Format non pris en charge** | Aspose ne gère que les images raster (JPG, PNG, BMP, TIFF). | Convertissez les PDF en images d’abord (utilisez Aspose.PDF) ou ignorez ces fichiers. |
| **Pression mémoire** | Les images très volumineuses peuvent saturer la RAM lorsque de nombreux threads s’exécutent. | Réduisez `maxDegreeOfParallelism` ou redimensionnez les images avant l’OCR. |
| **Texte non anglais** | La langue définie sur l’anglais ignorera les autres scripts. | Changez `Language = OcrLanguage.French` (ou une combinaison multilingue). |

Ces conseils rendent votre job par lots robuste, surtout lorsque vous **process image list** provient de téléchargements utilisateurs ou d’une archive scannée.

## Astuce pro – Ajuster le parallélisme

Si vous exécutez cela sur une machine à 8 cœurs, augmentez le parallélisme à 6 ou 8 et observez l’amélioration de vitesse. Cependant, rappelez‑vous que chaque thread consomme également de la mémoire pour le bitmap. Une bonne règle de base :

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

Injectez `maxThreads` dans `BatchRecognize` pour une configuration dynamique, adaptée à la machine.

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être compilé. Remplacez simplement `YOUR_DIRECTORY` par le chemin contenant vos scans JPG.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Note :** La ligne `using System.IO;` est requise pour l’utilitaire `Directory`. Le code affiche un message convivial si aucun JPG n’est trouvé, évitant ainsi un échec silencieux.

## Conclusion

Nous venons de démontrer un flux de travail propre de **batch OCR images** qui **extracts text from jpg** files, **reads text from scans**, et traite efficacement une **process image list** grâce au **parallel OCR processing**. L’exemple complet et exécutable montre exactement comment configurer le moteur, lui fournir une collection de fichiers et gérer les résultats—tout en maîtrisant l’utilisation de la mémoire et le nombre de threads.

Prêt pour l’étape suivante ? Essayez de changer la langue en français, ajoutez la conversion PDF‑vers‑image, ou stockez le texte OCR dans une base de données. Le principe reste le même : initialiser une fois, fournir une liste, et laisser Aspose faire le travail lourd en parallèle.

Des questions ou des astuces à partager ? Laissez un commentaire ci‑dessous, et bon codage ! 

![Flux de traitement d'images OCR par lots](https://example.com/placeholder.png "Diagramme illustrant le flux de travail d'images OCR par lots")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}