---
category: general
date: 2026-03-13
description: Comment effectuer une OCR en lot rapidement et de manière fiable tout
  en apprenant à extraire du texte à partir de fichiers TIFF avec Aspose.OCR. Suivez
  ce tutoriel étape par étape.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: fr
og_description: Apprenez à effectuer la reconnaissance optique de caractères par lots
  en C# et à extraire du texte à partir de fichiers TIFF avec Aspose.OCR. Ce guide
  couvre l'installation, le code et les conseils de bonnes pratiques.
og_title: Comment réaliser un OCR par lots en C# – Guide complet de programmation
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Comment réaliser une OCR par lots en C# – Guide complet de programmation
url: /fr/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

top-button >}}

We must keep them unchanged.

Now produce final content with all translations and placeholders.

Check that we didn't miss any markdown elements.

Make sure code block placeholders are on their own lines as original.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots en C# – Guide complet de programmation

Vous vous êtes déjà demandé **comment faire de l'OCR par lots** sur une montagne de factures numérisées sans écrire un script séparé pour chaque fichier ? Vous n'êtes pas le seul. Dans de nombreux projets réels, le problème n'est pas la précision de l'OCR elle‑même, mais le volume énorme d'images—souvent des TIFF—qui doivent être transformées en texte interrogeable.  

Ce tutoriel vous montre **comment faire de l'OCR par lots** en utilisant le `BatchProcessor` d’Aspose.OCR tout en vous apprenant comment **extraire du texte d'un tiff** dans une exécution unique et propre. À la fin, vous disposerez d’une application console prête à l’emploi qui traite un dossier complet, exploite l’accélération GPU optionnelle et génère des résultats en texte brut où vous le souhaitez.

## Ce dont vous aurez besoin

- **.NET 6+** (ou .NET Framework 4.7.2 si vous préférez le runtime classique)  
- **Aspose.OCR for .NET** – vous pouvez récupérer le package NuGet avec `dotnet add package Aspose.OCR`.  
- Un dossier d’images **TIFF** que vous souhaitez lire (le tutoriel utilise `Invoices` comme exemple).  
- Optionnel : un GPU qui prend en charge DirectX 11 ou CUDA si vous voulez accélérer le traitement.  

Aucun service supplémentaire, aucune clé cloud—juste un projet C# local et la bibliothèque Aspose.

## Étape 1 : Configurer le projet et installer Aspose.OCR

Tout d’abord, créez une application console.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Astuce :** Si vous êtes sous Windows et prévoyez d’utiliser l’accélération GPU, assurez‑vous que le pilote graphique le plus récent est installé. Sinon le drapeau `UseGpu = true` reviendra automatiquement au CPU.

## Étape 2 : Créer la configuration du BatchProcessor

Nous allons maintenant configurer le `BatchProcessor`. C’est le cœur de **comment faire de l'OCR par lots**—vous indiquez à Aspose la langue attendue, les filtres de pré‑traitement à appliquer, et si vous devez exploiter le GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Pourquoi ces paramètres ?**  
- `Language = Language.English` indique au moteur d’utiliser le modèle de langue anglaise, qui est bien plus précis que le modèle générique.  
- `UseGpu` peut réduire le temps de traitement de moitié sur un GPU correct, mais il est prudent de le laisser à `false` si vous êtes sur un ordinateur portable sans GPU.  
- Le pipeline de filtres reproduit ce qu’un humain ferait : redresser la page et nettoyer les taches avant de la transmettre au moteur OCR.

## Étape 3 : Pointer le processeur vers votre dossier TIFF

La prochaine étape de **comment faire de l'OCR par lots** consiste à indiquer à la bibliothèque où se trouvent les fichiers source. Les caractères génériques sont pris en charge, vous pouvez donc récupérer chaque fichier `.tif` en une seule fois.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Cas particulier :** Si vos images ont des extensions mixtes (`.tiff`, `.tif`, `.png`), appelez `AddFolder` plusieurs fois ou utilisez `*.*` puis filtrez plus tard dans le code.

## Étape 4 : Choisir où les résultats de l'OCR seront enregistrés

Vous vous demandez peut‑être « Où le texte extrait se retrouve‑t‑il ? » C’est le troisième pilier de **comment faire de l'OCR par lots**—définir l’emplacement et le format de sortie. Nous stockerons les fichiers texte brut à côté des originaux.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Si vous avez besoin de JSON ou XML au lieu du texte brut, remplacez simplement `OutputFormat.PlainText` par `OutputFormat.Json` ou `OutputFormat.Xml`. La bibliothèque gère la conversion pour vous.

## Étape 5 : Exécuter le travail par lots et rapporter les résultats

Enfin, lancez le travail. La méthode `Execute` bloque jusqu’à ce que chaque fichier soit traité, puis vous pouvez inspecter `ProcessedCount` pour confirmer le succès.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Sortie attendue

Lorsque vous exécutez le programme, la console affichera quelque chose comme :

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

Dans le dossier `Output`, vous trouverez un fichier `.txt` par TIFF source, chacun nommé d’après l’image originale (par ex., `Invoice_001.txt`). Ouvrez n’importe quel fichier et vous verrez le texte OCR brut—parfait pour l’alimenter dans un index de recherche ou un pipeline d’extraction de données en aval.

## Gestion des problèmes courants

### 1. GPU non disponible

Si `UseGpu = true` mais aucun appareil compatible n’est trouvé, Aspose revient silencieusement au CPU. Pour être explicite, vous pouvez intercepter l’exception `DeviceNotFoundException` :

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Fichiers non‑TIFF dans le même dossier

Lorsque vous avez un dossier mixte, filtrez programmatique :

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Fichiers volumineux dépassant la mémoire

Pour des TIFF multi‑pages gigantesques, activez le streaming :

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Astuces pro pour une meilleure précision lorsque vous **extrayez du texte d'un tiff**

- **La résolution compte** – Visez 300 dpi ou plus. En dessous, le moteur OCR peut manquer des caractères.  
- **Couleur vs. niveaux de gris** – Convertissez les scans couleur en niveaux de gris avant l’OCR ; le `DeskewFilter` le fait déjà en interne, mais vous pouvez ajouter `ColorDepthReductionFilter` pour plus de rapidité.  
- **Post‑traitement** – Après avoir obtenu le texte brut, lancez une vérification orthographique ou un nettoyage par expressions régulières pour corriger les particularités courantes de l’OCR (par ex., “0” vs “O”).

## Exemple complet fonctionnel (prêt à copier‑coller)

Ci‑dessous se trouve le programme complet que vous pouvez compiler et exécuter. Remplacez simplement les chemins factices par vos propres répertoires.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Compilez et exécutez :

```bash
dotnet run
```

Vous devriez maintenant disposer d’un ensemble ordonné de fichiers `.txt`—chacun étant le résultat de **l'extraction de texte d'un tiff** via un processus batch entièrement automatisé.

## Conclusion

Nous avons parcouru **comment faire de l'OCR par lots** en C# du début à la fin, couvrant tout ce dont vous avez besoin pour **extraire du texte d'un tiff** efficacement. Les points clés sont :

1. Utilisez le `BatchProcessor` d’Aspose.OCR pour éviter d’écrire des boucles répétitives.  
2. Exploitez les filtres de pré‑traitement (deskew, despeckle) pour une meilleure précision.  
3. Activez l’accélération GPU lorsque c’est possible, mais assurez toujours un repli sur le CPU.  
4. Stockez les résultats dans une structure de dossiers prévisible afin que les jobs en aval puissent les récupérer automatiquement.

À partir d’ici, vous pourriez explorer :

- Alimenter le texte brut dans un **index de recherche** (par ex., Elasticsearch) pour rendre les factures interrogeables.  
- Convertir la sortie en **JSON** et la transmettre à un modèle d’apprentissage automatique qui extrait les lignes d’articles.  
- Ajouter une **gestion des erreurs** pour les TIFF corrompus ou les problèmes de permissions.

Essayez‑le,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}