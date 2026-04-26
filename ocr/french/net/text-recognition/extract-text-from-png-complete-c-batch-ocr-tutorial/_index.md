---
category: general
date: 2026-04-26
description: Extrayez rapidement du texte à partir de fichiers PNG avec C#. Apprenez
  à convertir des images en texte, lire des fichiers PNG, parcourir les images et
  effectuer une reconnaissance optique de caractères en lot en quelques minutes.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: fr
og_description: Extrayez du texte des fichiers PNG rapidement avec C#. Ce guide montre
  comment convertir des images en texte, lire des fichiers PNG, parcourir les images
  et réaliser une OCR par lots.
og_title: Extraire du texte d’un PNG – Tutoriel complet d’OCR par lots en C#
tags:
- C#
- OCR
- Aspose
title: Extraction de texte à partir de PNG – Tutoriel complet d’OCR par lots en C#
url: /fr/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'un PNG – Tutoriel complet OCR en C# par lots

Vous avez déjà eu besoin d'**extraire du texte de fichiers PNG** sans savoir par où commencer ? Vous n'êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu'ils essaient pour la première fois l'OCR sur un dossier de captures d'écran. La bonne nouvelle, c'est qu'avec quelques lignes de C# et Aspose OCR, vous pouvez convertir des images en texte, lire des fichiers PNG, parcourir les images et tout traiter par lots en une seule fois.  

Dans ce tutoriel, nous allons parcourir une application console prête à l'emploi qui fait exactement cela. À la fin, vous disposerez d'une solution autonome qui extrait le texte de chaque PNG d'un répertoire et crée un fichier `.txt` correspondant à côté de chaque image. Aucun script supplémentaire, aucun copier‑coller manuel — juste du code pur.

## Ce dont vous avez besoin

- **.NET 6 SDK** (ou toute version .NET plus récente). C’est gratuit, rapide, et fonctionne partout.
- **Aspose.OCR for .NET** (le package NuGet). La bibliothèque inclut l'accélération GPU si vous avez un GPU compatible, mais elle revient automatiquement au CPU sinon.
- Un dossier contenant quelques **images PNG** que vous souhaitez traiter.  
- Un éditeur de texte ou un IDE — Visual Studio, VS Code, Rider—ce que vous préférez.

C’est tout. Si vous avez déjà ces éléments, vous êtes prêt à démarrer.

![extract text from png example](image.png "extract text from png demo screenshot")

*Texte alternatif de l'image : « extraction de texte à partir de PNG avec OCR en C# par lots »*

## Étape 1 – Créer le projet et installer Aspose.OCR

Tout d'abord, créez un nouveau projet console et ajoutez le package Aspose OCR.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Pourquoi utiliser une application console ? C’est l’hôte le plus simple pour les travaux par lots, et vous pouvez l’exécuter depuis la ligne de commande ou le planifier avec un planificateur de tâches. Si vous avez besoin plus tard d’une interface graphique, il suffit de déplacer la logique principale dans une bibliothèque de classes.

## Étape 2 – Initialiser un moteur OCR accéléré par GPU (ou repli CPU)

Aspose propose un `GpuOcrEngine` qui détecte automatiquement un GPU supporté. S’il n’est pas trouvé, il revient au moteur CPU standard—aucun code supplémentaire n’est nécessaire.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**Astuce :** Si vous êtes sur un serveur sans écran et sans GPU, vous pouvez remplacer `GpuOcrEngine` par `OcrEngine` et le code se comportera exactement de la même façon.

## Étape 3 – Parcourir les images du répertoire cible

Nous devons **parcourir les images** et ne sélectionner que les fichiers PNG. La méthode `Directory.GetFiles` fait le gros du travail, et nous nous protégerons contre un dossier vide.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

Remarquez l’utilisation de `SearchOption.TopDirectoryOnly`. Si vous devez plus tard parcourir les sous‑dossiers, il suffit de passer à `AllDirectories`. Ce petit changement vous permet de **convertir des images en texte** dans tout un arbre avec une seule ligne.

## Étape 4 – Effectuer l'OCR et enregistrer le résultat

Voici le cœur du flux de travail **OCR d'images par lots**. Nous chargeons chaque PNG, exécutons `Recognize()`, puis écrivons la chaîne extraite dans un fichier `.txt` portant le même nom de base.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Pourquoi l’envelopper dans un try/catch ?** Les lots d'images réels contiennent souvent un fichier corrompu ou un PNG avec un profil couleur inhabituel. Attraper l’exception empêche l’arrêt complet du processus et vous permet de continuer à traiter les fichiers restants.

## Étape 5 – Exécuter l'application et vérifier la sortie

Compilez et lancez l'application :

```bash
dotnet run
```

Vous devriez voir un journal console similaire à :

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Ouvrez l’un des fichiers `.txt` générés — le texte extrait s’y trouve. Si un fichier est vide, revérifiez la qualité de l’image ; l’OCR fonctionne mieux avec du texte clair et à fort contraste.

### Script de vérification rapide (optionnel)

Si vous voulez vous assurer que chaque PNG a reçu un fichier texte correspondant, exécutez ce petit one‑liner PowerShell :

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Variantes courantes & cas limites

| Situation | Ce qu’il faut modifier |
|-----------|------------------------|
| **Langues non latines** (p. ex. cyrillique) | `ocrEngine.Language = Language.Cyrillic;` |
| **Grand jeu d'images (>10 000 fichiers)** | Utilisez `Parallel.ForEach` pour accélérer le traitement, mais surveillez l’utilisation de la mémoire GPU. |
| **Conserver l'ordre original des images** | Triez `pngFiles` avant le `foreach` (`Array.Sort(pngFiles);`). |
| **Exécution sur un serveur CI sans GPU** | Remplacez `GpuOcrEngine` par `OcrEngine` pour éviter les erreurs d'initialisation GPU. |
| **Ne traiter que les fichiers contenant un mot‑clé spécifique** | Après avoir récupéré `result.Text`, vérifiez `result.Text.Contains("Invoice")` avant d’écrire le fichier. |

Ces ajustements vous permettent d’adapter le pipeline **convertir des images en texte** à presque toutes les situations que vous pourriez rencontrer.

## Code source complet (prêt à copier‑coller)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Enregistrez-le sous le nom `Program.cs`, exécutez `dotnet run`, et observez la magie opérer.

## Conclusion

Vous disposez maintenant d’une **méthode complète, prête pour la production, d'extraire du texte de fichiers PNG** avec C#. Le tutoriel a couvert tout le processus — de la configuration du projet, à l'initialisation d'un moteur OCR accéléré par GPU, en passant par le **parcours des images**, jusqu'au **OCR d'images par lots** et à l'enregistrement des résultats en texte brut.  

Si vous êtes curieux des étapes suivantes, essayez :

- **Convertir des images en texte** pour d’autres formats (JPG, BMP

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}