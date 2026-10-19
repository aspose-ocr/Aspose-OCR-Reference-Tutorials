---
category: general
date: 2026-01-10
description: Apprenez à reconnaître le texte à partir d’une image, à extraire les
  coordonnées du texte et à convertir un reçu en JSON à l’aide d’Aspose OCR en C#.
  Tutoriel étape par étape.
draft: false
keywords:
- recognize text from image
- how to extract text
- extract text coordinates
- convert receipt to json
language: fr
og_description: reconnaître le texte d'une image en C# avec Aspose OCR. Ce guide montre
  comment extraire le texte, obtenir les coordonnées et convertir le reçu en JSON.
og_title: Reconnaître le texte à partir d'une image – Tutoriel complet OCR C#
tags:
- OCR
- C#
- Aspose
title: Reconnaître du texte à partir d'une image en C# – Guide complet de l'OCR et
  du JSON
url: /fr/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image – Tutoriel complet C# OCR

Vous avez déjà eu besoin de reconnaître du texte à partir d'une image mais vous ne saviez pas quelle bibliothèque choisir ? Vous n'êtes pas seul. Dans de nombreuses applications réelles — suiveurs de dépenses, scanners de reçus ou archivistes de documents — extraire du texte de manière fiable est le premier obstacle.  

Dans ce tutoriel, nous allons parcourir **comment extraire du texte**, récupérer ses boîtes englobantes, et enfin **convertir le reçu en JSON** en utilisant Aspose.OCR pour .NET. À la fin, vous disposerez d'un projet C# autonome qui prend une photo d'un reçu et génère un fichier JSON propre avec les scores de confiance et les coordonnées.

## Ce dont vous avez besoin

Avant de plonger, assurez‑vous d’avoir les éléments suivants sur votre machine :

- **.NET 6.0 SDK** (ou toute version ultérieure). Les anciens frameworks fonctionnent aussi, mais .NET 6 est le point idéal pour les bibliothèques modernes.
- **Visual Studio 2022** ou VS Code avec l'extension C#.
- **Aspose.OCR for .NET** package NuGet (`Aspose.OCR` et `Aspose.OCR.Output`). Vous pouvez l'installer via la console du gestionnaire de packages :

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Output
```

- Une image de reçu d'exemple (par ex., `receipt.jpg`) placée dans un dossier que vous référencerez plus tard.

C’est tout — pas de SDK supplémentaires, pas de binaires natifs, juste du code géré pur.

## Étape 1 : Créer un nouveau projet console

Tout d'abord, créez une application console. C’est le moyen le plus rapide de tester l'OCR sans surcharge d'interface utilisateur.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll fill this in later.
        }
    }
}
```

> **Astuce :** Gardez le dossier du projet propre ; créez un sous‑dossier appelé `Resources` et déposez `receipt.jpg` à l'intérieur. Cela rend la gestion des chemins sans effort.

## Étape 2 : Charger l'image du reçu

Maintenant nous **reconnaissons réellement du texte à partir d'une image**. La première étape consiste à pointer le moteur OCR vers le fichier.

```csharp
// Inside Main()
string imagePath = @"Resources/receipt.jpg";
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// Initialise the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    Image = ImageStream.FromFile(imagePath)
};

Console.WriteLine("✅ Image loaded successfully.");
```

Pourquoi enveloppons‑nous le chargement dans une simple vérification d'existence ? Parce qu'en production vous traitez souvent des téléchargements d'utilisateurs qui peuvent être manquants ou corrompus. Détecter le problème tôt vous évite des exceptions obscures plus tard.

## Étape 3 : Effectuer l'OCR – **reconnaître du texte à partir d'une image**

Avec l'image en mémoire, nous demandons à Aspose de **reconnaître du texte à partir d'une image**. Cette opération est synchrone et renvoie un ensemble de résultats riche.

```csharp
// Still inside Main()
try
{
    ocrEngine.Recognize();
    Console.WriteLine("🧠 OCR completed.");
}
catch (Exception ex)
{
    Console.WriteLine($"❗ OCR failed: {ex.Message}");
    return;
}
```

En coulisses, Aspose exécute un réseau neuronal entraîné sur des millions de caractères. Le moteur remplit `ocrEngine.Text`, `ocrEngine.RecognitionResult` et une collection d'objets `OcrRegion` contenant les coordonnées. C’est exactement ce dont nous avons besoin pour l’étape suivante.

## Étape 4 : **Comment extraire du texte** – Obtenir la chaîne brute

Si vous ne vous souciez que du texte brut (peut‑être pour une recherche rapide), vous pouvez le récupérer directement depuis le moteur :

```csharp
string plainText = ocrEngine.Text;
Console.WriteLine("\n--- Extracted Text ---");
Console.WriteLine(plainText);
```

Vous remarquerez des sauts de ligne là où l'OCR a détecté des limites de paragraphe. Dans de nombreux scénarios de numérisation de reçus, la chaîne brute suffit pour extraire les totaux, dates ou noms de fournisseurs à l'aide de simples expressions régulières.

## Étape 5 : **extraire les coordonnées du texte** – Boîtes englobantes pour chaque mot

Souvent vous devez savoir *où* sur l'image se trouve un morceau de texte particulier — par exemple, pour mettre en évidence le montant total dans une interface. Aspose nous fournit cela via des objets `OcrRegion`.

```csharp
Console.WriteLine("\n--- Text Coordinates (extract text coordinates) ---");
foreach (var region in ocrEngine.RecognitionResult.Regions)
{
    // Each region represents a word or a line depending on the engine settings.
    string word = region.Text;
    var bounds = region.BoundingBox; // X, Y, Width, Height
    Console.WriteLine($"Word: \"{word}\" | Box: X={bounds.X}, Y={bounds.Y}, W={bounds.Width}, H={bounds.Height}");
}
```

Remarquez que nous parcourons **extraire les coordonnées du texte** pour chaque segment reconnu. Les coordonnées sont relatives à l'image originale, vous pouvez donc les superposer sur un canevas graphique ou un élément HTML `<canvas>`.

## Étape 6 : **convertir le reçu en JSON** – Enregistrement des résultats détaillés

Vient maintenant la partie qui relie tout : nous voulons une structure lisible par machine incluant le texte, les scores de confiance et les boîtes englobantes. Aspose fournit `JsonSaveOptions` qui simplifient cela.

```csharp
// Define where the JSON will be saved
string jsonPath = @"Resources/receipt.json";

// Configure JSON options to keep confidence and bounding boxes
JsonSaveOptions jsonOptions = new JsonSaveOptions
{
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};

// Save the OCR result
ocrEngine.Save(jsonPath, jsonOptions);
Console.WriteLine($"\n💾 Detailed OCR results saved to {jsonPath}");
```

Le fichier résultant ressemble à ceci (abrégé pour la concision) :

```json
{
  "Regions": [
    {
      "Text": "Store",
      "Confidence": 0.99,
      "BoundingBox": { "X": 45, "Y": 120, "Width": 80, "Height": 20 }
    },
    {
      "Text": "Total",
      "Confidence": 0.97,
      "BoundingBox": { "X": 300, "Y": 560, "Width": 70, "Height": 22 }
    }
    // ... more regions ...
  ]
}
```

Vous avez maintenant un artefact **convertir le reçu en JSON** qui peut être alimenté dans des services en aval — pensez aux API de rapports de dépenses, aux pipelines d'analyse, ou même à une interface simple qui dessine des rectangles autour de chaque mot.

## Exemple complet fonctionnel

En assemblant toutes les pièces, voici le `Program.cs` complet que vous pouvez copier‑coller dans votre projet :

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image
            // -------------------------------------------------
            string imagePath = @"Resources/receipt.jpg";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found at {imagePath}");
                return;
            }

            OcrEngine ocrEngine = new OcrEngine
            {
                Image = ImageStream.FromFile(imagePath)
            };
            Console.WriteLine("✅ Image loaded.");

            // -------------------------------------------------
            // 2️⃣ Run OCR – recognize text from image
            // -------------------------------------------------
            try
            {
                ocrEngine.Recognize();
                Console.WriteLine("🧠 OCR completed.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"❗ OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 3️⃣ Extract plain text (how to extract text)
            // -------------------------------------------------
            Console.WriteLine("\n--- Extracted Text ---");
            Console.WriteLine(ocrEngine.Text);

            // -------------------------------------------------
            // 4️⃣ Get coordinates (extract text coordinates)
            // -------------------------------------------------
            Console.WriteLine("\n--- Text Coordinates ---");
            foreach (var region in ocrEngine.RecognitionResult.Regions)
            {
                var box = region.BoundingBox;
                Console.WriteLine($"Word: \"{region.Text}\" | Box: X={box.X}, Y={box.Y}, W={box.Width}, H={box.Height}");
            }

            // -------------------------------------------------
            // 5️⃣ Save detailed JSON (convert receipt to json)
            // -------------------------------------------------
            string jsonPath = @"Resources/receipt.json";
            JsonSaveOptions jsonOptions = new JsonSaveOptions
            {
                IncludeConfidence = true,
                IncludeBoundingBoxes = true
            };
            ocrEngine.Save(jsonPath, jsonOptions);
            Console.WriteLine($"\n💾 JSON saved at {jsonPath}");
        }
    }
}
```

Exécutez le programme (`dotnet run`) et observez la sortie console. Ouvrez `Resources/receipt.json` pour vérifier la structure.

## Questions fréquentes & cas limites

- **Que faire si l'image est floue ?**  
  Aspose OCR fonctionne mieux avec 300 dpi ou plus. Si vous obtenez de faibles scores de confiance, envisagez d'appliquer un filtre de netteté avant d'alimenter l'image au moteur.

- **Puis-je reconnaître plusieurs langues ?**  
  Oui. Définissez `ocrEngine.Language = Language.English | Language.Spanish;` avant d'appeler `Recognize()`.

- **Comment limiter la sortie aux seuls nombres (par ex., totaux) ?**  
  Après avoir le texte brut, exécutez une expression régulière comme `\d+\.\d{2}` sur `ocrEngine.Text`. Comme nous disposons déjà des coordonnées, vous pouvez mapper la chaîne correspondante à sa région pour la mise en évidence visuelle.

- **Le format JSON est‑il personnalisable ?**  
  La classe `JsonSaveOptions` expose quelques indicateurs. Si vous avez besoin d'un schéma totalement personnalisé, vous pouvez parcourir `ocrEngine.RecognitionResult.Regions` et sérialiser les objets vous‑même avec `System.Text.Json`.

## Conclusion

Nous venons de démontrer comment **reconnaître du texte à partir d'une image** en C# avec Aspose.OCR, **comment extraire du texte**, récupérer les **coordonnées du texte extrait**, et enfin **convertir le reçu en JSON**. L’ensemble du flux réside dans une seule application console facile à exécuter, ce qui la rend parfaite pour les prototypes ou comme bloc de construction dans des systèmes plus grands.

Prochaines étapes ? Essayez d’alimenter le JSON dans un front‑end qui dessine les boîtes englobantes, ou branchez la sortie dans un service de rapports de dépenses. Vous pouvez également expérimenter différents formats d'image (PNG, TIFF) ou traiter par lots un dossier de reçus.

Vous avez d’autres questions sur l’OCR, Aspose ou la manipulation du JSON ? Laissez un commentaire ci‑dessous, et bon codage ! 

![Exemple d'image de reçu pour reconnaître du texte à partir d'une image](receipt.jpg "Exemple d'image de reçu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}