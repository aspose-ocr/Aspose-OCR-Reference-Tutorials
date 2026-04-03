---
category: general
date: 2026-04-03
description: Apprenez à effectuer la reconnaissance optique de caractères par lots
  avec Aspose.OCR en C#. Ce guide vous montre comment extraire du texte à partir d’images
  PNG et convertir les images en texte de manière efficace.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: fr
og_description: Découvrez comment réaliser une OCR par lots en C# pour extraire du
  texte d'images PNG et convertir les images en texte avec Aspose.OCR. Code complet
  inclus.
og_title: Comment réaliser une OCR par lots en C# – Guide rapide
tags:
- OCR
- C#
- Aspose
title: Comment faire de l'OCR par lots en C# – Méthode rapide pour extraire le texte
  des fichiers PNG
url: /fr/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots en C# – Méthode rapide pour extraire le texte des fichiers PNG

Vous vous êtes déjà demandé **comment faire une OCR par lots** d'un dossier complet de captures d'écran sans écrire une boucle pour chaque fichier ? Vous n'êtes pas le seul. Dans de nombreux projets—pensez à la numérisation de factures ou à l'archivage de reçus scannés—vous vous retrouvez avec des dizaines, parfois des centaines, de fichiers PNG dont il faut extraire le texte. La bonne nouvelle ? Avec Aspose.OCR vous pouvez **extraire le texte PNG** des images en parallèle, et l'ensemble du processus peut être encapsulé en quelques lignes de C#.

Dans ce tutoriel, nous passerons en revue un exemple complet, prêt à l'exécution, qui vous montre comment **convertir des images en texte** à l'aide d'un processeur par lots. Nous couvrirons les prérequis, expliquerons pourquoi chaque ligne est importante, et ajouterons même quelques pro‑tips pour que vous n'ayez pas de mauvaises surprises plus tard.

## Prérequis

- **.NET 6.0** (ou ultérieur) installé sur votre machine. Les runtimes plus anciens fonctionnent, mais la version la plus récente offre de meilleures performances et la prise en charge async.
- Package **Aspose.OCR for .NET**. Vous pouvez l'obtenir via NuGet : `dotnet add package Aspose.OCR`.
- Un dossier rempli d'images **PNG** que vous souhaitez traiter. Nous l'appellerons `YOUR_DIRECTORY` tout au long du guide.
- Une quantité modeste de RAM—l'OCR par lots peut être gourmand en mémoire si vous augmentez le parallélisme, mais l'utilisation de `Environment.ProcessorCount` le maintient sous contrôle.

> **Astuce pro :** Si vous utilisez un pipeline CI/CD, ajoutez le fichier de licence Aspose comme secret pour éviter la limite de 20 pages de l'évaluation gratuite.

Maintenant, mettons les mains dans le cambouis.

## Étape 1 : Configurer le processeur OCR par lots (Mot‑clé principal dans l’en‑tête)

La première chose dont vous avez besoin est une instance de `BatchOcrProcessor`. Cette classe abstrait la logique de threading et vous permet de vous concentrer sur ce qu'il faut faire avec chaque image.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Pourquoi c’est important :**  
- `Engine = new OcrEngine()` vous fournit un nouveau moteur OCR pour chaque thread, évitant les contentions.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` s’ajuste automatiquement au nombre de cœurs, vous offrant le meilleur débit possible sans réglage manuel.

## Étape 2 : Brancher les événements de progression (Aide à suivre l’extraction)

Voir la progression est essentiel lors du traitement de centaines de fichiers. L'événement `ProgressChanged` se déclenche après chaque fichier traité, vous permettant d’enregistrer le statut.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Pourquoi vous allez l’aimer :**  
- Un retour en temps réel vous évite de vous demander si l'application est bloquée.  
- Si vous avez besoin de mettre en pause ou d’annuler, vous avez déjà un point d’accroche pour inspecter `e.Current` vs `e.Total`.

## Étape 3 : Définir le scan du dossier et le motif de fichier (Extraire le texte PNG)

Nous indiquons maintenant au processeur où chercher et quel type de fichiers récupérer. Le motif `"*.png"` garantit que nous ne traitons que les images PNG.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Pourquoi c’est crucial :**  
- L’utilisation d’un motif glob rend le code flexible ; changez `*.png` en `*.jpg` si vous devez plus tard gérer des JPEG.  
- Le rappel reçoit à la fois le chemin de l’image et le texte reconnu, vous donnant un contrôle total sur la suite.

## Étape 4 : Enregistrer le texte reconnu à côté de la source (Convertir des images en texte)

Dans le rappel, nous écrirons la sortie OCR dans un fichier `.txt` qui se trouve juste à côté du PNG original. C’est la façon la plus simple de **convertir des images en texte** pour le traitement en aval.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Pourquoi nous choisissons un fichier `.txt` côte à côte :**  
- Cela garde la relation évidente — ouvrez le PNG, ouvrez le TXT, comparez.  
- Aucun besoin de base de données ou de couche de stockage supplémentaire dans les projets de petite envergure.

## Étape 5 : Conclure avec un message de fin convivial

Un message console soigné vous indique quand tout est terminé.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Lorsque vous exécutez le programme, vous verrez une sortie similaire à :

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Chaque PNG possède désormais un fichier `.txt` frère contenant le texte extrait.

## Exemple complet fonctionnel (Toutes les étapes combinées)

Ci‑dessous se trouve le programme complet que vous pouvez copier‑coller dans un nouveau projet console. Aucun élément ne manque — remplacez simplement `YOUR_DIRECTORY` par le chemin absolu de vos images.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Résultat attendu

- Pour chaque `image.png` dans `C:\MyImages`, un `image.txt` apparaît à côté.
- La console affiche des lignes de progression, facilitant la surveillance de gros lots.
- Aucun boucle manuelle ou gestion de thread—`BatchOcrProcessor` gère tout.

## Questions fréquentes & cas limites

### Et si mes images ne sont pas des PNG ?

Il suffit de changer le deuxième argument de `ProcessFolder` en `"*.jpg"` ou `"*.*"` pour inclure tous les fichiers. Le moteur OCR fonctionne avec la plupart des formats raster.

### Quelle quantité de mémoire cela consomme‑t‑il ?

`BatchOcrProcessor` charge une image par thread. Avec `Environment.ProcessorCount` réglé, par exemple, sur 8 cœurs, vous aurez huit images en mémoire simultanément. Si vous rencontrez des exceptions OutOfMemory, réduisez le parallélisme :

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Puis‑je personnaliser la langue OCR ?

Absolument. Après avoir créé le moteur, définissez sa propriété `Language` :

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose prend en charge de nombreuses langues ; ajoutez simplement le package NuGet approprié si nécessaire.

### Qu’en est‑il de la gestion des erreurs ?

Enveloppez le rappel dans un bloc try/catch et consignez les échecs. Le processeur continuera avec le fichier suivant, évitant qu’une image corrompue n’interrompe l’ensemble du processus.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Astuces pro pour monter en échelle

- **Divisez le dossier** : Si vous avez des dizaines de milliers de fichiers, séparez‑les en sous‑dossiers et exécutez plusieurs jobs par lots en séquence.
- **Utilisez une VM cloud** : Une machine avec plus de cœurs (par ex., 32 cœurs) terminera beaucoup plus rapidement. N’oubliez pas d’ajuster les limites de licence.
- **Post‑traitez le texte** : Après l’extraction, vous pourriez vouloir exécuter des expressions régulières pour extraire les numéros de facture ou les dates. Les fichiers `.txt` sont une entrée parfaite pour de tels pipelines.

## Conclusion

Vous disposez maintenant d’une recette solide, prête pour la production, pour **comment faire une OCR par lots** d’un répertoire de PNG, **extraire le texte PNG** des fichiers, et **convertir des images en texte** en utilisant Aspose.OCR en C#. L’exemple est autonome, explique le « pourquoi » de chaque ligne, et inclut des astuces pour gérer des charges de travail plus importantes ou différents types de fichiers.

Prêt pour l’étape suivante ? Essayez de remplacer le rappel pour pousser les résultats dans une base de données, ou ajoutez un pré‑traitement d’image (par ex., redressement) avant l’OCR. Le modèle s’adapte bien, vous pouvez donc le personnaliser à tout scénario de traitement par lots que vous rencontrez.

Bon codage, et que vos pipelines OCR soient rapides et sans erreur !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}