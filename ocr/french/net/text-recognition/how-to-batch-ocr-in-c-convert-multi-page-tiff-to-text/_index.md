---
category: general
date: 2026-03-28
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) par
  lots en C# et à convertir facilement les fichiers TIFF en texte. Ce guide étape
  par étape montre comment extraire le texte des fichiers TIFF à l'aide d'Aspose OCR.
draft: false
keywords:
- how to batch ocr
- convert tiff to text
- extract text from tiff
- c# ocr tutorial
language: fr
og_description: Comment effectuer une OCR par lots en C# ? Suivez ce tutoriel complet
  pour convertir des fichiers TIFF multipages en texte interrogeable à l’aide d’Aspose
  OCR.
og_title: Comment faire de l’OCR par lots en C# – Convertir un TIFF multipage en texte
tags:
- OCR
- C#
- Aspose
title: Comment faire de l’OCR par lots en C# – Convertir un TIFF multipage en texte
url: /fr/net/text-recognition/how-to-batch-ocr-in-c-convert-multi-page-tiff-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR par lots en C# – Convertir un TIFF multi‑pages en texte

Vous êtes-vous déjà demandé **comment faire de l'OCR par lots** sur une pile de pages numérisées sans écrire une boucle pour chaque image ? Vous n'êtes pas le seul. Dans de nombreux projets—pensons au traitement de factures ou à la numérisation d'archives—le besoin de **convertir TIFF en texte** apparaît quotidiennement, et le faire page par page devient rapidement un cauchemar.

Bonne nouvelle ! En quelques lignes de C# et avec Aspose OCR, vous pouvez fournir un TIFF multi‑pages complet au moteur et obtenir un dictionnaire associant les numéros de page à leurs chaînes extraites. Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre exactement **comment faire de l'OCR par lots**, comment **extraire du texte d'un TIFF**, et pourquoi cette approche surpasse l'alternative manuelle.

## Ce que vous allez apprendre

- Installer la bibliothèque Aspose OCR dans un projet .NET.  
- Charger un fichier TIFF multi‑pages avec `Image.FromMultiPageFile`.  
- Exécuter `RecognizeBatch` pour obtenir un `Dictionary<int,string>` de résultats page par page.  
- Afficher la sortie dans un format propre et lisible.  

À la fin, vous disposerez d’une application console prête à l’emploi qui transforme n’importe quel TIFF multi‑pages en texte brut—sans outils supplémentaires.

### Prérequis

- SDK .NET 6.0 (ou toute version .NET récente).  
- Visual Studio 2022 ou VS Code—votre IDE préféré fera l’affaire.  
- Une licence Aspose OCR valide ou une clé d’évaluation gratuite (l’API fonctionne sans licence mais ajoute un filigrane).  
- Un exemple de TIFF multi‑pages nommé `multipage.tif` placé dans un dossier que vous pouvez référencer.

> **Astuce pro :** Si vous êtes sous Windows, le dossier de projet par défaut est un endroit pratique pour déposer le TIFF ; sous Linux/macOS, ajustez simplement le chemin en conséquence.

## Étape 1 : Installer le package NuGet Aspose OCR

Avant d’écrire du code, nous avons besoin de la bibliothèque OCR. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Cela récupère la dernière version stable (en date de mars 2026 v23.9) et ajoute les DLL nécessaires à votre projet. Aucune configuration supplémentaire n’est requise pour une simple application console.

## Étape 2 : Créer la structure de base de l’application console

Créons un programme minimal qui référence le moteur OCR. Les directives `using` sont cruciales—sans elles, le compilateur se plaindra de types manquants.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Required for Image class
```

> **Pourquoi c’est important :** La classe `Image` se trouve dans un sous‑espace de noms, et oublier l’import `ImageProcessing` entraînera une erreur « type ou espace de noms introuvable » qui peut faire perdre une heure de débogage.

Ajoutez maintenant la méthode `Main` et un bref commentaire décrivant l’objectif :

```csharp
/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        // Implementation will go here
    }
}
```

## Étape 3 : Initialiser le moteur OCR

Le `OcrEngine` est le cheval de bataille. L’instancier une fois et le réutiliser pour toutes les pages est à la fois économique en mémoire et rapide.

```csharp
// Step 3: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Que se passe‑t‑il en coulisses ?** Le moteur charge les modèles linguistiques et pré‑configure les paramètres par défaut (par ex., anglais, auto‑rotation). Vous pourrez les ajuster plus tard, mais les valeurs par défaut conviennent à la plupart des documents.

## Étape 4 : Charger le TIFF multi‑pages

Aspose rend le chargement d’images à plusieurs cadres très simple. Fournissez le chemin complet ou un chemin relatif depuis le répertoire de travail de l’exécutable.

```csharp
// Step 4: Load a multi‑page TIFF image
string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // ← replace with your actual path
var multiPageImage = Image.FromMultiPageFile(tiffPath);
```

Si le fichier n’est pas trouvé, `FromMultiPageFile` lève une `FileNotFoundException`. Enveloppez l’appel dans un `try/catch` si vous avez besoin d’une gestion d’erreur élégante—quelque chose que nous montrerons à l’étape suivante.

## Étape 5 : Effectuer l’OCR par lots

Voici la star du spectacle : `RecognizeBatch`. Elle renvoie un `Dictionary<int,string>` où la clé est l’indice de page (commençant à 0) et la valeur est le texte reconnu.

```csharp
// Step 5: Perform batch OCR on all pages
Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);
```

> **Cas limite :** Certains TIFF contiennent des pages blanches. Aspose renvoie une chaîne vide pour ces pages, que vous pouvez filtrer plus tard si vous ne voulez pas d’encombrement dans votre sortie.

## Étape 6 : Afficher les résultats

Enfin, parcourez le dictionnaire et imprimez le texte de chaque page. L’utilisation de chaînes interpolées garde le code propre.

```csharp
// Step 6: Output the recognized text for each page
foreach (var pageResult in ocrResults)
{
    Console.WriteLine($"--- Page {pageResult.Key + 1} ---"); // +1 for human‑friendly numbering
    Console.WriteLine(pageResult.Value);
    Console.WriteLine(); // Blank line for readability
}
```

L’exécution du programme devrait produire quelque chose comme :

```
--- Page 1 ---
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
...

--- Page 2 ---
Terms and Conditions
...
```

Si vous voyez une sortie illisible, vérifiez que le TIFF source n’est pas corrompu et que la langue du texte correspond à la langue par défaut du moteur (anglais). Vous pouvez également définir `ocrEngine.Language = OcrLanguage.Spanish;` pour des documents non anglais.

## Exemple complet fonctionnel

En assemblant tous les morceaux, voici le programme complet que vous pouvez copier‑coller dans `Program.cs` et exécuter :

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;   // Needed for Image class

/// <summary>
/// Demonstrates how to batch OCR a multi‑page TIFF and output each page's text.
/// </summary>
class BatchOcrTutorial
{
    static void Main()
    {
        try
        {
            // Step 1: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Step 2: Load a multi‑page TIFF image
            string tiffPath = "YOUR_DIRECTORY/multipage.tif";   // Change to your actual file location
            var multiPageImage = Image.FromMultiPageFile(tiffPath);

            // Step 3: Perform batch OCR on all pages
            Dictionary<int, string> ocrResults = ocrEngine.RecognizeBatch(multiPageImage);

            // Step 4: Output the recognized text for each page
            foreach (var pageResult in ocrResults)
            {
                Console.WriteLine($"--- Page {pageResult.Key + 1} ---");
                Console.WriteLine(pageResult.Value);
                Console.WriteLine(); // Extra line for visual separation
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
        }
    }
}
```

Enregistrez, compilez et lancez :

```bash
dotnet run
```

Vous devriez voir le contenu extrait de chaque page affiché dans la console. Voilà le **tutoriel c# ocr** complet que vous attendiez.

## Questions fréquentes & cas limites

### Que faire si mon TIFF contient des dizaines de pages ?

`RecognizeBatch` traite toutes les trames en un seul appel, mais l’utilisation de la mémoire augmente linéairement avec le nombre de pages. Pour des documents très volumineux (des centaines de pages), envisagez de les traiter par lots :

```csharp
for (int i = 0; i < multiPageImage.PageCount; i += 50)
{
    var subImage = multiPageImage.GetPages(i, Math.Min(50, multiPageImage.PageCount - i));
    var partialResults = ocrEngine.RecognizeBatch(subImage);
    // Merge partialResults into the main dictionary...
}
```

### Puis‑je enregistrer le texte extrait dans des fichiers au lieu de l’afficher ?

Absolument. Remplacez le bloc `Console.WriteLine` par des opérations d’I/O fichier :

```csharp
string outputFolder = "ExtractedText";
Directory.CreateDirectory(outputFolder);

foreach (var pageResult in ocrResults)
{
    string filePath = Path.Combine(outputFolder, $"Page_{pageResult.Key + 1}.txt");
    File.WriteAllText(filePath, pageResult.Value);
}
```

Chaque page obtiendra ainsi son propre fichier `.txt`—idéal pour l’indexation en aval.

### Comment changer la langue de sortie ou activer l’auto‑rotation ?

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
ocrEngine.AutoRotate = true;             // Detects rotated text automatically
```

Ces paramètres doivent être appliqués **avant** d’appeler `RecognizeBatch`.

## Conclusion

Nous avons couvert **comment faire de l'OCR par lots** sur un TIFF multi‑pages avec Aspose OCR en C#. En chargeant l’image une seule fois, en appelant `RecognizeBatch`, puis en parcourant le dictionnaire résultant, vous pouvez **convertir TIFF en texte** en quelques secondes. L’exemple montre également comment **extraire du texte d’un TIFF**, gérer les erreurs et éventuellement écrire les résultats dans des fichiers—le tout dans une application console propre et autonome.

Prêt pour l’étape suivante ? Essayez de combiner cette approche avec une bibliothèque de génération de PDF pour créer des PDF recherchables, ou intégrez la sortie dans une base de données pour des archives consultables. Vous pouvez aussi expérimenter avec d’autres formats d’image (PNG, JPEG) en remplaçant `Image.FromMultiPageFile` par `Image.FromFile`.

Vous avez d’autres questions sur l’OCR, les licences ou l’optimisation des performances ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}