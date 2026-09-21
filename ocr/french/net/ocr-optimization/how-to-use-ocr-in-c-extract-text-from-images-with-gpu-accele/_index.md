---
category: general
date: 2025-12-29
description: Comment utiliser l'OCR en C# pour extraire du texte à partir d'images,
  afficher le nombre de caractères et améliorer les performances grâce à l'accélération
  GPU avec Aspose OCR.
draft: false
keywords:
- how to use OCR
- extract text image
- display character count
- gpu acceleration ocr
- c# ocr aspose
language: fr
og_description: Comment utiliser l'OCR en C# pour extraire du texte d'images, afficher
  le nombre de caractères et accélérer le traitement avec le GPU grâce à Aspose OCR.
og_title: Comment utiliser l'OCR en C# – Extraction rapide de texte avec GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: Comment utiliser l’OCR en C# – Extraire du texte d’images avec accélération
  GPU
url: /fr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en C# – Guide complet

Vous vous êtes déjà demandé **comment utiliser l'OCR** dans un projet .NET sans écrire des milliers de lignes de code ? Peut‑être avez‑vous scanné un fichier TIFF massif et avez besoin du texte rapidement, ou vous voulez simplement compter les caractères pour un tableau de bord de reporting. Dans les deux cas, vous êtes au bon endroit. Dans ce tutoriel, nous allons parcourir l'extraction de texte d'une image, l'affichage du nombre de caractères, et accélérer le processus avec **l'OCR accéléré par GPU** – le tout avec la bibliothèque **C# Aspose OCR**.

Nous ajouterons également les sujets secondaires que vous pourriez rechercher : **extract text image**, **display character count**, et les astuces **c# ocr aspose**. À la fin, vous disposerez d'une application console prête à l'emploi capable de traiter de gros scans en un clin d'œil.

---

## Ce que vous allez apprendre

- Configurer Aspose OCR dans un projet C# (sans mystères NuGet).
- Activer **GPU acceleration OCR** pour les fichiers volumineux.
- Charger une image et **extract text from the image**.
- **Display character count** et le temps de traitement.
- Gérer les pièges courants comme les pilotes GPU manquants ou les formats d'image non pris en charge.

> **Pré-requis :** .NET 6+ (ou .NET Framework 4.7.2) et un GPU compatible. Si vous n’avez pas de GPU, le code reviendra proprement en mode CPU.

![Comment utiliser l'OCR avec accélération GPU en C#](ocr-gpu.png "exemple d'utilisation de l'OCR montrant l'utilisation du GPU")

*Texte alternatif de l'image : illustration de l'utilisation de l'OCR avec accélération GPU*

## Étape 1 : Installer Aspose OCR et préparer le projet

### Pourquoi c’est important

Avant de pouvoir **utiliser l'OCR**, la bibliothèque doit être référencée. Aspose OCR est fourni sous forme d'un seul paquet NuGet qui regroupe les binaires natifs pour CPU et GPU, ainsi vous n’aurez pas à rechercher manuellement les DLL.

```csharp
// In your terminal or Package Manager Console
dotnet add package Aspose.OCR
```

> **Astuce :** Si vous ciblez .NET Framework, utilisez l’interface NuGet de Visual Studio pour éviter les conflits de version.

### Structure complète du projet

Créez une nouvelle application console et collez le `Program.cs` suivant. Il inclut toutes les instructions `using` requises, vous n’aurez donc pas à deviner ce qu’il faut importer.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing; // optional, for advanced pre‑processing

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Call the helper that does the heavy lifting
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            // Step 2: Create and configure the OCR engine (see next section)
        }
    }
}
```

Enregistrez le fichier, restaurez les paquets, et vous êtes prêt pour l’étape suivante.

## Étape 2 : Utiliser le moteur OCR avec accélération GPU

### Pourquoi activer le GPU ?

Traiter un TIFF multi‑méga‑pixel sur un CPU peut prendre des secondes voire des minutes. Le chemin **GPU acceleration OCR** décharge les opérations pixel par pixel sur votre carte graphique, réduisant le temps de façon spectaculaire—souvent à une fraction de l’original.

```csharp
static void RunOcr(string imagePath)
{
    // Create an OCR engine instance
    var ocrEngine = new OcrEngine();

    // Enable GPU acceleration – if a compatible device is found
    ocrEngine.UseGpu = true;
    ocrEngine.GpuDeviceId = 0; // 0 = first GPU; change if you have multiple

    // Optional sanity check – fall back to CPU if GPU init fails
    try
    {
        // This call forces the engine to initialize GPU resources
        ocrEngine.InitializeGpu();
        Console.WriteLine("✅ GPU acceleration enabled.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
        ocrEngine.UseGpu = false;
    }

    // Load the image (this also validates format)
    var inputImage = Image.Load(imagePath);
    
    // Perform OCR – the heavy lifting happens here
    var ocrResult = ocrEngine.Recognize(inputImage);

    // Step 3: Display results (character count & processing time)
    DisplayResult(ocrResult);
}
```

> **Pourquoi cela fonctionne :** `UseGpu` active le pipeline interne. `InitializeGpu()` force une validation précoce afin que vous puissiez détecter les problèmes de pilotes avant l’appel long `Recognize`.

## Étape 3 : Extraire le texte de l'image et afficher le nombre de caractères

Maintenant que le moteur tourne, extrayons le **text from the image** et affichons le nombre de caractères reconnus. C’est la partie que la plupart des développeurs négligent, mais elle est cruciale pour la validation et les analyses en aval.

```csharp
static void DisplayResult(OcrResult ocrResult)
{
    // The raw OCR text
    string extractedText = ocrResult.Text;

    // Character count – includes spaces and line breaks
    int charCount = extractedText.Length;

    // Processing time in milliseconds (provided by Aspose)
    long processingMs = ocrResult.ProcessingTime;

    // Output to console – easy to pipe to a file or logger
    Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
    Console.WriteLine("----- Begin OCR Text -----");
    Console.WriteLine(extractedText);
    Console.WriteLine("------ End OCR Text ------");
}
```

**Sortie attendue** (exemple pour un scan de 2 pages) :

```
✅ GPU acceleration enabled.
🖋️ Extracted 12,345 characters in 842 ms
----- Begin OCR Text -----
Lorem ipsum dolor sit amet, consectetur...
... (rest of the page) ...
------ End OCR Text ------
```

Si le GPU n’est pas disponible, vous verrez un avertissement et le même résultat, simplement plus lent.

## Étape 4 : Gestion des gros fichiers et des cas limites

### Et si l’image est énorme ?

Aspose OCR peut diffuser les pages, mais vous avez toujours besoin de suffisamment de RAM. Une bonne pratique consiste à réduire la résolution DPI non essentielle avant la reconnaissance :

```csharp
// Optional pre‑processing: downscale to 300 DPI if original > 600 DPI
if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
{
    inputImage = inputImage.Resize(0.5, 0.5); // 50% reduction
    Console.WriteLine("🔎 Image downscaled for faster OCR.");
}
```

### Pilotes GPU manquants ?

Le `try/catch` autour de `InitializeGpu()` capture déjà la plupart des problèmes, mais vous pouvez également interroger les appareils disponibles :

```csharp
var gpuInfo = GpuDeviceManager.GetDevices();
if (gpuInfo.Count == 0)
{
    Console.WriteLine("⚡ No GPU detected – defaulting to CPU.");
    ocrEngine.UseGpu = false;
}
```

### Formats d'image non pris en charge ?

Aspose prend en charge TIFF, PNG, JPEG, BMP et quelques formats exotiques. Si vous obtenez une `UnsupportedFormatException`, convertissez d’abord le fichier avec un outil comme ImageMagick ou la méthode intégrée `Image.Save` en PNG.

## Étape 5 : Conclusion – Exemple complet fonctionnel

Copiez‑collez le programme complet ci‑dessous dans `Program.cs`. C’est une démo autonome que vous pouvez exécuter immédiatement (remplacez simplement le chemin).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.ImageProcessing;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust the path to point at your scanned TIFF or JPEG
            RunOcr(@"YOUR_DIRECTORY/large_scanned_page.tif");
        }

        static void RunOcr(string imagePath)
        {
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,
                GpuDeviceId = 0
            };

            try
            {
                ocrEngine.InitializeGpu();
                Console.WriteLine("✅ GPU acceleration enabled.");
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ GPU init failed ({ex.Message}), switching to CPU.");
                ocrEngine.UseGpu = false;
            }

            var inputImage = Image.Load(imagePath);

            // Optional downscale for gigantic files
            if (inputImage.DpiX > 600 || inputImage.DpiY > 600)
            {
                inputImage = inputImage.Resize(0.5, 0.5);
                Console.WriteLine("🔎 Image downscaled for faster OCR.");
            }

            var ocrResult = ocrEngine.Recognize(inputImage);
            DisplayResult(ocrResult);
        }

        static void DisplayResult(OcrResult ocrResult)
        {
            string extractedText = ocrResult.Text;
            int charCount = extractedText.Length;
            long processingMs = ocrResult.ProcessingTime;

            Console.WriteLine($"🖋️ Extracted {charCount} characters in {processingMs} ms");
            Console.WriteLine("----- Begin OCR Text -----");
            Console.WriteLine(extractedText);
            Console.WriteLine("------ End OCR Text ------");
        }
    }
}
```

Exécutez‑le avec `dotnet run` et observez la console afficher le **character count** et le texte OCR. Voilà tout le cycle **how to use OCR** du début à la fin.

## Conclusion

Nous venons de couvrir **how to use OCR** en C# pour **extract text from images**, **display character count**, et accélérer tout le pipeline avec **GPU acceleration OCR** en utilisant la bibliothèque **c# ocr aspose**. Les points clés :

1. Installer Aspose OCR via NuGet et référencer les bons espaces de noms.  
2. Activer le GPU, mais toujours prévoir un repli sur le CPU.  
3. Charger votre image, éventuellement la réduire, puis appeler `Recognize`.  
4. Récupérer `ocrResult.Text` et `ocrResult.ProcessingTime` pour **display character count** et les métriques de performance.  

À partir de là, vous pouvez vous diversifier — stocker le texte dans une base de données, l’alimenter à un index de recherche, ou exécuter une détection de langue sur la chaîne extraite. Si vous devez traiter des PDF, fournissez simplement chaque page sous forme d’image ; le même code fonctionne.

**Prochaines étapes** que vous pourriez explorer :

- Utiliser **extract text image** à partir de PDF multi‑pages avec `PdfConverter`.  
- Ajuster les paramètres OCR (packs de langues, réduction du bruit) pour une meilleure précision.  
- Faire évoluer la solution dans Azure Functions ou AWS Lambda avec des instances activées GPU.  

Essayez‑le, cassez‑le, puis améliorez‑le. C’est ainsi que les projets OCR du monde réel sont construits. Bon codage, et que vos scans soient toujours lisibles !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}