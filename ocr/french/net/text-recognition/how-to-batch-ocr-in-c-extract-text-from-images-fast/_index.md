---
category: general
date: 2026-03-21
description: Comment réaliser une OCR par lots en C# simplement — apprenez à extraire
  du texte à partir d'images, à convertir des images en texte et à enregistrer l'OCR
  en texte avec les paramètres de langue.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: fr
og_description: Comment réaliser un OCR par lots en C# vous permet d'extraire du texte
  à partir d'images, de convertir les images en texte et d'enregistrer l'OCR sous
  forme de texte tout en définissant facilement la langue de l'OCR.
og_title: Comment faire de l’OCR par lots en C# – Guide rapide
tags:
- OCR
- C#
- Aspose
title: Comment réaliser une OCR par lots en C# – Extraire rapidement du texte à partir
  d’images
url: /fr/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire du OCR par lots en C# – Extraire du texte d'images rapidement

Vous vous êtes déjà demandé **comment faire du OCR par lots** lorsque vous avez des centaines d'images dans un dossier ? Vous n'êtes pas seul—les développeurs demandent constamment comment extraire du texte d'images sans écrire une boucle pour chaque fichier. La bonne nouvelle, c’est qu’Aspose.OCR vous offre une méthode propre, prête au parallélisme, pour **convertir des images en texte** en quelques lignes de C#.

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l’exécution, qui vous montre comment **enregistrer le OCR en texte**, choisir la bonne langue et augmenter le traitement parallèle pour la vitesse. À la fin, vous disposerez d’une solution autonome que vous pourrez intégrer à n’importe quel projet .NET.

## Ce dont vous avez besoin

- .NET 6 ou version ultérieure (l’API fonctionne avec .NET Core et .NET Framework)
- Aspose.OCR pour .NET (package NuGet `Aspose.OCR`)
- Un dossier d’images que vous souhaitez traiter (PNG, JPEG, TIFF, etc.)
- Un peu de curiosité sur la programmation parallèle (optionnel, mais utile)

Pas de services supplémentaires, pas de clés cloud—juste du code C# pur qui s’exécute localement.

---

![flux de OCR par lots](placeholder.png){alt="diagramme du flux de OCR par lots"}

## Étape 1 : Configurer le projet et installer Aspose.OCR

Tout d’abord, créez une application console (ou réutilisez-en une existante) et ajoutez le package Aspose.OCR :

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Astuce :** Si vous utilisez Visual Studio, faites un clic droit sur le projet → *Manage NuGet Packages* → recherchez *Aspose.OCR* et installez la dernière version stable.

Cela vous donne accès à `OcrBatchProcessor`, `OcrEngineSettings` et à l’énumération `Language`.

## Étape 2 : Définir les dossiers d’entrée et de sortie

Le processeur par lots doit connaître l’emplacement des images sources et où les fichiers texte extraits doivent être écrits. Conservez les chemins absolus ou relatifs à la racine du projet—assurez‑vous simplement que les dossiers existent avant d’exécuter le code.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Pourquoi c’est important :** Si le dossier de sortie est absent, le processeur lèvera une exception, interrompant tout le lot. Le créer à l’avance garantit une exécution fluide.

## Étape 3 : Configurer les paramètres OCR (y compris la langue)

C’est ici que vous **définissez la langue du OCR** pour l’ensemble du lot. Aspose.OCR prend en charge des dizaines de langues ; l’anglais est la valeur par défaut, mais vous pouvez passer au français, à l’espagnol, etc., en modifiant la valeur de l’énumération `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Si vous avez besoin de traiter différentes langues par image, vous pouvez ensuite remplacer ce paramètre par fichier—plus d’informations plus tard.

## Étape 4 : Construire l’objet `OcrBatchProcessor`

Nous rassemblons maintenant le tout. Le `OcrBatchProcessor` vous permet de spécifier le dossier d’entrée, le dossier de sortie, le format de sortie, les options parallèles et les paramètres partagés que nous venons de créer.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Pourquoi le parallélisme ?** Lorsque vous avez des dizaines ou des centaines d’images, les traiter une par une peut être très lent. Définir `MaxDegreeOfParallelism` à 4 permet à l’environnement d’exécution d’utiliser quatre cœurs CPU simultanément, réduisant considérablement le temps total sur une station de travail typique.

## Étape 5 : Exécuter l’opération par lots

Avec le processeur configuré, l’exécution se fait en un seul appel de méthode. La bibliothèque gère automatiquement l’énumération des fichiers, le OCR et l’écriture des résultats.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Lorsque la console affiche *« Batch OCR completed. »*, vous trouverez un fichier `.txt` à côté de chaque image originale dans `BatchResults`. Chaque fichier texte contient les caractères bruts extraits de son image source—exactement ce dont vous avez besoin pour **extraire du texte d’images** pour le traitement en aval.

### Sortie attendue

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Ouvrez l’un de ces fichiers et vous verrez la représentation en texte brut du contenu de l’image.

## Étape 6 : Vérifier les résultats (optionnel)

C’est une bonne habitude de revérifier quelques fichiers pour s’assurer que le OCR a fonctionné comme prévu. Une façon rapide est de lire la première ligne de chaque fichier généré et de l’afficher dans la console :

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Si vous remarquez des caractères illisibles, envisagez de changer le paramètre `Language` ou d’ajuster la qualité de l’image (par ex., augmenter le DPI, convertir en niveaux de gris).

## Variations avancées et cas limites

### 1. Remplacements de langue par fichier

Parfois, un lot contient des documents multilingues. Vous pouvez inspecter chaque nom d’image et assigner une langue à la volée :

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Formats de sortie différents

Si vous avez besoin de PDF recherchables au lieu de texte brut, modifiez `OutputFormat` :

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Cela **convertira les images en texte** à l’intérieur d’un conteneur PDF, en préservant la mise en page originale.

### 3. Gestion des images volumineuses

Des images très haute résolution peuvent consommer beaucoup de mémoire. Pour garder le processus léger, activez le sous‑échantillonnage d’image :

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Journalisation des erreurs

Le processeur lève des exceptions pour les fichiers illisibles. Enveloppez `Execute` dans un try/catch et consignez les noms de fichiers problématiques :

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Exemple complet fonctionnel

En rassemblant tout, voici le programme complet, prêt à copier‑coller :

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Enregistrez ceci sous `Program.cs`, compilez le projet et exécutez `dotnet run`. Vous verrez la sortie console confirmant la fin, suivie d’un court aperçu du texte extrait.

---

## Conclusion

Nous venons de couvrir **comment faire du OCR par lots** en C# avec Aspose.OCR, en vous montrant comment **extraire du texte d’images**, **convertir des images en texte**, et **enregistrer le OCR en texte** tout en **définissant la langue du OCR** pour correspondre à votre contenu. L’exemple est pleinement fonctionnel, inclut le traitement parallèle pour la rapidité, et offre des points d’extension pour des scénarios avancés comme les remplacements de langue par fichier ou la sortie PDF.

Prêt pour l’étape suivante ? Essayez de remplacer `OcrOutputFormat.PlainText` par `SearchablePdf` et voyez à quel point il est facile de générer des PDF recherchables. Ou expérimentez avec différentes valeurs de `MaxDegreeOfParallelism` pour extraire chaque milliseconde sur une machine multi‑cœur.

Si vous rencontrez des problèmes, revérifiez les chemins des dossiers, assurez‑vous que les images sont lisibles, et vérifiez que l’énumération de langue correspond au texte de vos images. Bon codage, et que vos lots de OCR soient rapides et précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}