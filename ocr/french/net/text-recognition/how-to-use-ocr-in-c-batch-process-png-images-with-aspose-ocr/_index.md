---
category: general
date: 2026-02-14
description: Comment utiliser l'OCR en C# pour extraire rapidement le texte des fichiers
  PNG. Apprenez le traitement OCR par lots d'images, traitez plusieurs images et utilisez
  Aspose OCR C# dans un guide unique.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: fr
og_description: Comment utiliser l’OCR en C# avec Aspose OCR C#. Ce tutoriel montre
  comment extraire du texte à partir de fichiers PNG, réaliser une OCR par lots d’images
  et traiter plusieurs images efficacement.
og_title: Comment utiliser l’OCR en C# – Extraction de texte PNG par lots
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Comment utiliser l'OCR en C# – Traitement par lots d'images PNG avec Aspose
  OCR
url: /fr/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en C# – Traitement par lots d'images PNG avec Aspose OCR

Vous vous êtes déjà demandé **comment utiliser l'OCR** pour extraire du texte d'un tas de fichiers PNG sans écrire une routine distincte pour chacun ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent **extraire du texte PNG** à grande échelle, surtout lorsque les images se trouvent dans un dossier et que vous devez lancer le moteur OCR pour chaque fichier.  

Dans ce guide, nous parcourrons une solution complète, prête à l’emploi, qui **effectue l'OCR par lots sur les images**, **traite plusieurs images** en parallèle, et exploite la puissante bibliothèque **Aspose OCR C#**. À la fin, vous disposerez d’un exécutable unique qui lit n’importe quel nombre de PNG, en extrait le texte et affiche les résultats dans la console — le tout avec seulement quelques lignes de code.

## Prérequis

- .NET 6.0 ou version ultérieure (le code fonctionne également avec .NET Core et .NET Framework)  
- Une licence valide d'Aspose.OCR pour .NET (ou l'essai gratuit) – vous pouvez l'obtenir sur le site web d'Aspose.  
- Un dossier contenant les fichiers PNG que vous souhaitez lire.  
- Visual Studio 2022 (ou tout IDE compatible C#).  

Aucun package NuGet supplémentaire n’est requis au-delà de `Aspose.OCR`.

## Étape 1 : Comment utiliser l'OCR – Initialiser le moteur Aspose OCR

La première chose dont vous avez besoin est une instance de la classe `Engine`. Cet objet abstrait la technologie OCR sous‑jacente et peut s’exécuter sur CPU ou GPU, selon votre matériel et votre licence.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Pourquoi c’est important :* Initialiser le moteur une fois et le réutiliser entre les threads économise de la mémoire et évite le surcoût de chargement répété des modèles OCR. Cela garantit également des paramètres cohérents pour toutes les images.

## Étape 2 : Extraire le texte PNG – Rassembler les chemins d’image

Ensuite, nous avons besoin d’une collection de chemins de fichiers. Dans un projet réel, vous pourriez lire le répertoire dynamiquement, mais pour plus de clarté, nous listerons quelques fichiers d’exemple.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*Astuce :* Remplacez `YOUR_DIRECTORY` par le chemin absolu ou relatif vers vos images. Si vous avez des dizaines de fichiers, vous pouvez remplacer la liste manuelle par `Directory.GetFiles("YOUR_DIRECTORY", "*.png")`.

## Étape 3 : OCR par lots d’images – Exécuter la reconnaissance en parallèle

Traiter les images les unes après les autres est simple mais lent. En utilisant `Parallel.ForEach`, nous pouvons **traiter plusieurs images** simultanément, en tirant parti des CPU multi‑cœurs.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Pourquoi le parallélisme ?* Chaque appel OCR est intensif en CPU mais indépendant, ainsi les exécuter simultanément peut réduire considérablement le temps d’exécution total, surtout sur une machine à 4 cœurs ou plus.

## Étape 4 : Traiter plusieurs images – Afficher le texte extrait

Maintenant que nous disposons d’une collection d’objets `OcrResult`, nous pouvons les parcourir et afficher le texte reconnu. C’est ici que vous stockeriez normalement la sortie dans une base de données ou écririez dans des fichiers, mais la sortie console rend l’exemple concis.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Sortie console attendue (exemple) :**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Si une image ne peut pas être chargée, Aspose lève une exception ; vous pouvez entourer l’appel `engine.Recognize` d’un bloc try/catch pour consigner les erreurs sans interrompre le traitement du lot complet.

## Étape 5 : Exemple complet – Tous les éléments réunis

Ci-dessous se trouve le programme complet que vous pouvez copier‑coller dans un nouveau projet console C#. Il comprend tout, des instructions `using` jusqu’à la boucle de sortie finale.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Exécution de l’exemple

1. Créez un nouveau projet **Console App** dans Visual Studio.  
2. Ajoutez le package NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`).  
3. Remplacez `YOUR_DIRECTORY` par le chemin contenant vos fichiers PNG.  
4. Compilez et exécutez – vous devriez voir le texte extrait affiché dans la console.

## Astuces pro & cas limites

- **Accélération GPU :** Si vous disposez d’un GPU compatible et d’une licence Aspose OCR, activez‑le via `EngineSettings` avant de créer le moteur. Cela peut économiser quelques secondes par image.  
- **Fichiers volumineux :** Pour les images supérieures à 10 Mo, envisagez de les réduire d’abord afin de diminuer la pression mémoire.  
- **Support linguistique :** Par défaut, le moteur suppose l’anglais. Définissez `engine.Language = Language.French;` (ou toute langue prise en charge) pour améliorer la précision sur du texte non anglais.  
- **Gestion des erreurs :** Le `try/catch` à l’intérieur de la boucle parallèle garantit qu’un fichier corrompu n’interrompt pas le lot complet. Vous pouvez également consigner les échecs dans un fichier pour une révision ultérieure.  
- **Stockage des résultats :** Au lieu d’afficher, vous pouvez écrire `result.Text` dans un fichier `.txt` en utilisant `File.WriteAllText(Path.ChangeExtension(path, ".txt"))`.

## Conclusion

Vous savez maintenant **comment utiliser l'OCR** en C# pour **extraire du texte PNG** des fichiers, **effectuer l'OCR par lots sur les images**, et **traiter plusieurs images** efficacement avec Aspose OCR C#. La solution est entièrement autonome, s’exécute en parallèle, et peut être étendue pour gérer des centaines voire des milliers de fichiers avec peu de modifications.

Prêt pour l’étape suivante ? Essayez de remplacer la sortie console par un rapport CSV, expérimentez l’accélération GPU, ou alimentez le texte OCR dans un index de recherche. Les possibilités sont infinies, et le schéma de base — initialiser une fois, exécuter en parallèle, gérer les erreurs avec grâce — vous sera très utile dans tout pipeline de traitement d’images.

Bon codage, et que vos tâches OCR soient rapides et sans erreur !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}