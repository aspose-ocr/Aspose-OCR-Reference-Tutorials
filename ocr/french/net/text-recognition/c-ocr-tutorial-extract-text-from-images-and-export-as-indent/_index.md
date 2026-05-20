---
category: general
date: 2026-05-02
description: Tutoriel C# OCR qui montre comment extraire du texte d’une image en C#
  et reconnaître le texte PNG, puis écrire du JSON indenté avec JsonSerializer C#.
  Guide étape par étape pour les développeurs.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: fr
og_description: Tutoriel C# OCR qui montre comment extraire du texte d’une image C#,
  reconnaître le texte PNG, puis écrire du JSON indenté avec JsonSerializer C#. Exemple
  complet et exécutable.
og_title: c# tutoriel OCR – Extraire le texte et l'exporter en JSON indenté
tags:
- OCR
- C#
- Aspose
- JSON
title: Tutoriel OCR C# – Extraire le texte des images et l’exporter en JSON indenté
url: /fr/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutoriel c# ocr – Extraire du texte d'images et exporter en JSON indenté

Vous avez déjà eu besoin d'un **tutoriel c# ocr** qui passe d'une photo de texte directement à un fichier JSON joliment formaté ? Vous n'êtes pas seul. Dans de nombreux projets – pensez à la numérisation de factures, à l'analyse de reçus, ou même à l'extraction de texte de mèmes – vous vous retrouvez avec un fichier PNG et vous vous demandez comment extraire les mots sans écrire de reconnaisseur personnalisé.  

Ce guide vous propose une solution concrète : nous allons **extraire du texte image c#** avec Aspose.OCR, **reconnaître le texte png**, puis **écrire du json indenté** avec `JsonSerializer` en C#. À la fin, vous disposerez d’une application console autonome que vous pourrez intégrer à n’importe quelle solution .NET. Pas de liens vagues « voir la documentation », juste un exemple complet, prêt à copier‑coller.

## Ce dont vous avez besoin

- **.NET 6** (ou toute version .NET récente). Les frameworks plus anciens fonctionnent, mais la syntaxe présentée cible .NET 6+.
- **Aspose.OCR for .NET** – installez via NuGet : `dotnet add package Aspose.OCR`.
- Une image PNG d’exemple (`text.png`) contenant du texte clair et lisible par machine.
- Un IDE ou éditeur de votre choix – Visual Studio, VS Code, Rider, etc.

> **Astuce :** Si vous prévoyez de traiter de nombreuses images, envisagez de réutiliser une seule instance de `OcrEngine` plutôt que d’en créer une nouvelle pour chaque fichier. Cela réduit la surcharge et améliore le débit.

## Étape 1 : Créer un projet tutoriel c# ocr

Tout d’abord, créez un projet console. Les commandes suivantes créent la structure de base et ajoutent la bibliothèque OCR :

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Ouvrez maintenant le fichier `Program.cs` généré. Nous remplacerons son contenu par l’exemple complet plus tard, mais pour l’instant assurez‑vous simplement que le projet se compile :

```bash
dotnet build
```

S’il n’y a aucune erreur, vous êtes prêt à continuer.

## Étape 2 : Reconnaître le texte PNG d’une image

Le cœur de tout **tutoriel c# ocr** est le moteur OCR lui‑même. Aspose.OCR masque les détails bas‑niveau et vous propose une classe `OcrEngine` propre. Ci‑dessous, nous créons le moteur, le pointons vers un fichier PNG, et lui demandons de reconnaître le texte.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Pourquoi cela fonctionne

- **`RecognizeImage`** accepte de nombreux formats (PNG, JPEG, BMP). Nous **reconnaissons le texte png** car le PNG conserve les détails sans perte, ce qui est idéal pour l’OCR.
- Le `OcrResult` retourné contient non seulement le texte brut mais aussi un score de confiance par glyphe, utile si vous devez filtrer plus tard les caractères à faible confiance.

## Étape 3 : Écrire du JSON indenté avec JsonSerializer c#

Maintenant que nous disposons de `ocrResult`, l’étape logique suivante dans notre **tutoriel c# ocr** est de transformer cet objet en JSON lisible par l’homme. Le sérialiseur intégré `System.Text.Json` fait le travail, et nous le configurerons pour **écrire du json indenté** afin d’améliorer la lisibilité.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Utiliser correctement `JsonSerializer`

- Le drapeau `WriteIndented` est le moyen le plus simple d’**écrire du json indenté** sans faire appel à des bibliothèques tierces.
- Si vous avez besoin de noms de propriétés en camelCase, ajoutez `PropertyNamingPolicy = JsonNamingPolicy.CamelCase` aux options.
- La chaîne `jsonOutput` peut être enregistrée avec `File.WriteAllText("result.json", jsonOutput);` – une petite astuce pratique pour les pipelines de production.

## Étape 4 : Exécuter et vérifier la sortie

Compilez et lancez le programme :

```bash
dotnet run
```

En supposant que `text.png` contienne la phrase *« Hello, OCR World! »*, vous devriez obtenir quelque chose comme :

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

Ce JSON est **indenté**, ce qui le rend facile à lire dans les journaux ou à transmettre à des services en aval.

### Cas particuliers & astuces

| Situation | Action à entreprendre |
|-----------|-----------------------|
| **L'image est floue** | Augmentez `ocrEngine.Config.Dpi` (par ex., `ocrEngine.Config.Dpi = 300`) avant d’appeler `RecognizeImage`. |
| **Langue non‑anglaise** | Définissez `ocrEngine.Config.Language = OcrLanguage.German` (ou toute langue prise en charge). |
| **Grand lot de fichiers** | Parcourez un répertoire en réutilisant la même instance `OcrEngine` ; enregistrez chaque résultat JSON avec un nom de fichier unique. |
| **Nécessité de ne garder que le texte à haute confiance** | Filtrez `ocrResult.Lines` où `Confidence` ≥ 0.95 avant la sérialisation. |

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le *programme entier*, prêt à être placé dans `Program.cs`. Il inclut toutes les étapes, la gestion des erreurs et des commentaires qui rendent le code auto‑explicatif.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Exécutez le code, examinez la console ou le fichier `.json` généré, et vous verrez le texte extrait avec les scores de confiance, le tout joliment **indenté**.

## Conclusion

Vous disposez maintenant d’un **tutoriel c# ocr** complet montrant comment **extraire du texte image c#**, **reconnaître le texte png**, et **écrire du json indenté** à l’aide de `JsonSerializer`. L’exemple est complet, exécutable, et inclut des conseils pratiques pour des scénarios réels.  

Et après ? Essayez de remplacer Aspose.OCR par un autre moteur (par ex., Tesseract) et observez comment la forme de `OcrResult` change, ou alimentez le JSON dans une API en aval qui stocke les données OCR dans une base de données. Vous pouvez également expérimenter avec les options **use jsonserializer c#** comme des convertisseurs personnalisés pour le formatage des dates ou la gestion des énumérations.

Bon codage, et que vos pipelines OCR soient toujours précis !  

---  

![diagramme du tutoriel c# ocr](image.png "Diagram illustrating OCR flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}