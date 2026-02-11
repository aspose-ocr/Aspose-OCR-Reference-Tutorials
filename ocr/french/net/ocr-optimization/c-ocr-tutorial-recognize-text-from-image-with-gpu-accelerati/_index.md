---
category: general
date: 2026-01-15
description: Tutoriel C# OCR qui montre comment reconnaître du texte à partir d’une
  image, extraire le texte d’une facture et convertir une image en texte en utilisant
  Aspose OCR sur le GPU.
draft: false
keywords:
- c# ocr tutorial
- recognize text from image
- extract text from invoice
- convert image to text
- load image for ocr
language: fr
og_description: Tutoriel C# OCR qui vous apprend à reconnaître le texte à partir d’une
  image, extraire le texte d’une facture et convertir une image en texte avec Aspose
  OCR sur le GPU.
og_title: Tutoriel OCR C# – Reconnaissance de texte rapide propulsée par GPU
tags:
- OCR
- C#
- Aspose
- GPU
title: c# tutoriel OCR – Reconnaître le texte à partir d'une image avec accélération
  GPU
url: /fr/net/ocr-optimization/c-ocr-tutorial-recognize-text-from-image-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Reconnaître du texte à partir d'une image avec accélération GPU

Vous avez déjà eu besoin d'un **c# ocr tutorial** qui fonctionne réellement sans essais et erreurs interminables ? Peut-être êtes‑vous face à une facture haute résolution et vous vous demandez comment **extract text from invoice** en quelques secondes. La bonne nouvelle, c’est que vous n’avez pas besoin de réinventer la roue — Aspose.OCR vous fournit une API propre, accélérée par GPU, qui fait le travail lourd pour vous.

Dans ce guide, nous parcourrons un exemple complet et exécutable qui montre comment **recognize text from image** fichiers, **convert image to text**, et gérer les problèmes les plus courants. À la fin, vous disposerez d’un programme autonome capable de lire n’importe quelle image de document, des reçus aux contrats numérisés, et de produire du texte propre et consultable.

## Ce que vous apprendrez

- Comment installer et référencer le package NuGet Aspose.OCR.
- Comment configurer le moteur OCR pour qu’il s’exécute sur le GPU pour des performances fulgurantes.
- La bonne façon de **load image for ocr** en utilisant `OcrImage.FromFile`.
- Comment appeler `Recognize` avec la langue souhaitée et récupérer le résultat.
- Conseils pour gérer les PDF multi‑pages, les scans à faible contraste et la gestion des erreurs.

Aucune expérience préalable avec Aspose n’est requise ; il suffit d’un environnement de développement .NET fonctionnel (Visual Studio 2022 ou VS Code) et d’un GPU modeste (même un GPU intégré Intel suffit).

---

## Étape 1 – Installer Aspose.OCR et préparer votre projet

Tout d’abord : vous avez besoin de la bibliothèque Aspose.OCR. Le moyen le plus simple est via NuGet.

```bash
dotnet add package Aspose.OCR
```

> **Pro tip :** Si vous ciblez .NET 6 ou une version ultérieure, le package récupérera automatiquement les binaires GPU natifs pour Windows, Linux et macOS. Aucun DLL supplémentaire à copier.

Une fois le package ajouté, ouvrez votre fichier de projet (`*.csproj`) et vérifiez la référence :

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.12.0" />
</ItemGroup>
```

Vous avez maintenant tout ce qu’il faut pour commencer à coder.

## Étape 2 – Créer un moteur OCR activé GPU (c# ocr tutorial)

Le cœur du **c# ocr tutorial** est le `OcrEngine`. En définissant `Engine = Engine.Gpu`, nous indiquons à Aspose d’utiliser la carte graphique au lieu du CPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // Initialize the OCR engine with GPU acceleration.
            var ocrEngine = new OcrEngine
            {
                Engine = Engine.Gpu // GPU acceleration is selected; the library auto‑detects the device.
            };

            // The rest of the steps are broken out into separate methods for clarity.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            PerformOcr(ocrEngine, imagePath);
        }
    }
}
```

> **Pourquoi GPU ?** Un GPU peut traiter des milliers de pixels en parallèle, réduisant le temps d’OCR de secondes à une fraction de seconde sur des images grandes et à haute résolution DPI.

## Étape 3 – Charger l’image pour l’OCR (load image for ocr)

Charger correctement l’image est plus important que vous ne le pensez. `OcrImage.FromFile` prend en charge PNG, JPEG, BMP, TIFF et même les pages PDF. Il lit également le DPI de l’image, ce qui influence la précision.

```csharp
static void PerformOcr(OcrEngine engine, string filePath)
{
    // Step 3: Load the image you want to recognize.
    // The FromFile method automatically detects the format.
    var image = OcrImage.FromFile(filePath);

    // Optional: Pre‑process the image for better results.
    // For example, you can increase contrast or convert to grayscale.
    image = ImagePreprocessor.AdjustContrast(image, 1.2);
    image = ImagePreprocessor.ConvertToGrayscale(image);
    
    // Continue to recognition...
    RecognizeAndDisplay(engine, image);
}
```

**Note :** Si vous travaillez avec un PDF, vous pouvez extraire chaque page en tant qu’`OcrImage` et les fournir une par une.

## Étape 4 – Reconnaître le texte à partir d’une image (recognize text from image)

Maintenant, la magie opère. Nous demandons au moteur de reconnaître le texte anglais, mais vous pouvez fournir n’importe quelle langue prise en charge par Aspose (Espagnol, Allemand, Chinois, etc.).

```csharp
static void RecognizeAndDisplay(OcrEngine engine, OcrImage image)
{
    // Step 4: Perform OCR on the image using the desired language.
    var result = engine.Recognize(image, Language.English);

    // Step 5: Output the recognized text.
    Console.WriteLine("=== OCR RESULT ===");
    Console.WriteLine(result.Text);
}
```

La propriété `result.Text` contient la chaîne brute. Si vous avez besoin du score de confiance pour chaque mot, vous pouvez inspecter `result.Regions`.

### Résultat attendu

```
=== OCR RESULT ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,234.56
Thank you for your business!
```

Si l’image est floue, vous pourriez voir des caractères illisibles — c’est là que le prétraitement de l’Étape 3 aide.

## Étape 5 – Extraire le texte d’une facture – Exemple réel

Imaginons que vous ayez un dossier rempli de factures numérisées et que vous vouliez extraire le montant total. Voici une extension rapide du code précédent qui utilise une expression régulière simple.

```csharp
using System.Text.RegularExpressions;

static void ExtractTotalAmount(string ocrText)
{
    // Look for a pattern like "$1,234.56"
    var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
    if (match.Success)
        Console.WriteLine($"Detected total: {match.Value}");
    else
        Console.WriteLine("Total amount not found.");
}
```

Vous appelleriez `ExtractTotalAmount(result.Text);` immédiatement après avoir affiché le résultat OCR. Cela montre à quel point il est facile d’**extract text from invoice** une fois que vous avez la chaîne brute.

## Étape 6 – Convertir l’image en texte en masse (convert image to text)

Traiter un seul fichier suffit pour une démo, mais le code de production doit souvent gérer des dizaines ou des centaines d’images. Voici une boucle concise qui traite un répertoire complet :

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    foreach (var file in Directory.EnumerateFiles(folderPath, "*.*", SearchOption.TopDirectoryOnly)
                                 .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
    {
        Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
        var img = OcrImage.FromFile(file);
        var res = engine.Recognize(img, Language.English);
        Console.WriteLine(res.Text);
        ExtractTotalAmount(res.Text); // optional invoice extraction
    }
}
```

Exécuter `ProcessFolder(ocrEngine, @"C:\Invoices")` **convert image to text** pour chaque fichier pris en charge dans le dossier, en tirant parti du GPU pour la rapidité.

## Cas limites et pièges courants

| Situation | Pourquoi cela se produit | Solution rapide |
|-----------|--------------------------|-----------------|
| **Low‑contrast scan** | L’OCR a du mal à différencier le premier plan de l’arrière‑plan. | Augmenter le contraste (`ImagePreprocessor.AdjustContrast`) ou appliquer un seuillage adaptatif. |
| **Multi‑page PDF** | `OcrImage.FromFile` ne lit que la première page. | Utiliser `PdfDocument` pour extraire chaque page en tant qu’`OcrImage` et boucler. |
| **Unsupported language** | La langue par défaut est l’anglais. | Passer `Language.Spanish` ou toute autre valeur d’énumération prise en charge. |
| **GPU not detected** | Binaires natifs manquants ou pilote obsolète. | Vérifier que le pilote GPU est à jour ; réinstaller le package NuGet avec le drapeau `-runtime`. |
| **Out‑of‑memory on huge images** | La mémoire du GPU est limitée. | Réduire la taille de l’image (`image = ImagePreprocessor.Resize(image, 2000, 0)`). |

Résoudre ces problèmes dès le départ vous fait gagner des heures de débogage plus tard.

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans une nouvelle application console. Il inclut toutes les méthodes d’assistance discutées ci‑dessus.

```csharp
using System;
using System.IO;
using System.Linq;
using System.Text.RegularExpressions;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Initialize GPU‑accelerated OCR engine.
            var ocrEngine = new OcrEngine { Engine = Engine.Gpu };

            // 2️⃣ Define the path to a single image or a folder.
            string imagePath = @"YOUR_DIRECTORY/high_res_invoice.png";
            // string folderPath = @"C:\Invoices";

            // Uncomment one of the following lines:
            PerformOcr(ocrEngine, imagePath);
            // ProcessFolder(ocrEngine, folderPath);
        }

        // -------------------------------------------------
        // Load image, preprocess, recognize, and display.
        // -------------------------------------------------
        static void PerformOcr(OcrEngine engine, string filePath)
        {
            var image = OcrImage.FromFile(filePath);
            image = ImagePreprocessor.AdjustContrast(image, 1.2);
            image = ImagePreprocessor.ConvertToGrayscale(image);

            var result = engine.Recognize(image, Language.English);
            Console.WriteLine("=== OCR RESULT ===");
            Console.WriteLine(result.Text);

            ExtractTotalAmount(result.Text);
        }

        // -------------------------------------------------
        // Bulk processing of a folder.
        // -------------------------------------------------
        static void ProcessFolder(OcrEngine engine, string folderPath)
        {
            foreach (var file in Directory.EnumerateFiles(folderPath, "*.*")
                                          .Where(f => f.EndsWith(".png") || f.EndsWith(".jpg") || f.EndsWith(".tiff")))
            {
                Console.WriteLine($"\nProcessing: {Path.GetFileName(file)}");
                var img = OcrImage.FromFile(file);
                var res = engine.Recognize(img, Language.English);
                Console.WriteLine(res.Text);
                ExtractTotalAmount(res.Text);
            }
        }

        // -------------------------------------------------
        // Simple regex to pull the total amount from an invoice.
        // -------------------------------------------------
        static void ExtractTotalAmount(string ocrText)
        {
            var match = Regex.Match(ocrText, @"\$\d{1,3}(,\d{3})*(\.\d{2})?");
            if (match.Success)
                Console.WriteLine($"Detected total: {match.Value}");
            else
                Console.WriteLine("Total amount not found.");
        }
    }
}
```

**Run it** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}