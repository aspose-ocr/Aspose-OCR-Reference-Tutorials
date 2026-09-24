---
category: general
date: 2026-01-01
description: Comment effectuer une reconnaissance OCR par lots avec le moteur OCR
  Aspose en C#. Apprenez à reconnaître le texte à partir d’images et à extraire le
  texte des fichiers TIFF avec l’accélération GPU.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: fr
og_description: Comment réaliser une reconnaissance OCR par lots en C# avec le moteur
  Aspose OCR. Ce guide vous montre comment reconnaître du texte à partir d'images
  et extraire du texte de fichiers TIFF de manière efficace.
og_title: Comment réaliser une OCR par lots en C# – Guide complet d’Aspose
tags:
- OCR
- C#
- Aspose
- GPU
title: Comment faire de l'OCR par lots en C# avec le moteur OCR d'Aspose
url: /fr/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots en C# avec le moteur Aspose OCR

Vous êtes-vous déjà demandé **comment faire de l'OCR par lots** lorsque des dizaines de documents numérisés sont stockés dans un dossier ? Vous n'êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu'ils passent de la reconnaissance d'une seule image à celle d'une collection entière. La bonne nouvelle, c’est qu’Aspose OCR rend cela très simple, que vous utilisiez un CPU ou que vous profitiez de l’accélération GPU.

Dans ce tutoriel, nous allons parcourir un exemple complet et exécutable qui **reconnaît du texte à partir d’images** et même **extrait du texte de fichiers TIFF** en masse. Pas de raccourcis « voir la documentation », juste une solution autonome que vous pouvez copier‑coller et exécuter dès aujourd’hui.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou version ultérieure installé (le code cible .NET 6, mais .NET 5 fonctionne également).
* Le package NuGet Aspose.OCR pour .NET (les versions CPU et GPU sont disponibles ; installez celle qui correspond à votre matériel).
* Un dossier contenant quelques fichiers TIFF ou PNG d’exemple que vous souhaitez traiter.
* Visual Studio 2022 ou tout autre IDE de votre choix.

> **Astuce :** Si vous prévoyez d’utiliser la version GPU, vérifiez que votre pilote graphique est à jour et que CUDA 11+ est installé. Le moteur reviendra automatiquement au CPU s’il ne trouve pas de GPU compatible.

## Étape 1 – Configurer le projet et installer Aspose.OCR

### H2: Créez une nouvelle application console et ajoutez Aspose.OCR

Ouvrez un terminal (ou la console du Gestionnaire de packages dans Visual Studio) et exécutez :

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Si vous disposez d’une licence compatible GPU, ajoutez le package GPU à la place :

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

C’est tout — votre projet référence maintenant la bibliothèque OCR que nous utiliserons pour **l’OCR par lots**.

## Étape 2 – Initialiser le moteur OCR (CPU ou GPU)

### H2: Comment faire de l'OCR par lots – Initialisation du moteur

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Pourquoi c’est important :** En basculant `UseGpu`, vous laissez Aspose choisir le chemin le plus rapide. Si le GPU n’est pas disponible, le moteur bascule silencieusement vers le CPU, de sorte que votre tâche par lots ne plante jamais à cause d’un matériel manquant.

## Étape 3 – Rassembler les fichiers à traiter

### H2: Reconnaître du texte à partir d’images – Construction de la liste de fichiers

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Note sur les cas limites :** Si vous avez un mélange de formats, changez le motif de recherche en `"*.*"` et filtrez par extension à l’intérieur de la boucle. Cela garde le lot flexible.

## Étape 4 – Traiter chaque image et afficher un aperçu

### H2: Extraire du texte de TIFF – Boucle sur les fichiers

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Ce que vous verrez :** Pour chaque TIFF, la console affiche quelque chose comme :

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

Cet aperçu confirme que le lot a réussi sans avoir à ouvrir chaque fichier manuellement.

## Étape 5 – Enregistrer les résultats (Facultatif mais pratique)

### H3: Persister la sortie OCR dans des fichiers texte

Si vous avez besoin du texte complet pour un traitement en aval, ajoutez ceci à l’intérieur de la boucle `foreach` :

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Chaque TIFF obtient maintenant un fichier compagnon `.txt` contenant la sortie OCR complète — parfait pour l’indexation, la recherche ou l’alimentation d’un modèle de langage.

## Étape 6 – Exécuter la démo et vérifier

1. Compilez le projet : `dotnet build`.
2. Exécutez : `dotnet run --project GpuBatchDemo.csproj`.

Vous devriez voir les lignes d’aperçu affichées dans la console, et (si vous avez ajouté l’étape facultative) une série de fichiers `.txt` à côté de vos images sources.

### H3: Pièges courants & comment les résoudre

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| **Empty `ocrResult.Text`** | Image trop sombre ou DPI faible | Pré‑traitez les images (augmentez le contraste, upscale) ou définissez `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Pilote obsolète | Mettez à jour le pilote GPU, ou définissez `UseGpu = false` pour forcer le CPU. |
| **Exception “File not found”** | Séparateur de chemin incorrect sous Linux/macOS | Utilisez `Path.Combine` ou des barres obliques (`/`). |

## Étape 7 – Mise à l’échelle (au‑delà de quelques fichiers)

Lorsque vous passez de quelques TIFF à des milliers, pensez à :

* **Traitement parallèle :** Enveloppez le `foreach` dans `Parallel.ForEach` (assurez‑vous que l’instance du moteur est thread‑safe ; sinon créez‑en une par thread).
* **I/O par lots :** Lisez les images par lots pour éviter d’épuiser la RAM.
* **Journalisation :** Écrivez la progression dans un fichier log ; cela aide à reprendre après un plantage.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Rappel :** La mémoire GPU est partagée, donc lancer trop de jobs GPU parallèles peut en fait ralentir le processus. Testez d’abord avec quelques threads.

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

Exécuter ce programme **reconnaîtra du texte à partir d’images**, **extraira du texte de TIFF**, et démontrera **comment faire de l’OCR par lots** de manière efficace.

---

## Conclusion

Vous disposez maintenant d’un exemple complet, de bout en bout, de **comment faire de l’OCR par lots** en C# avec le moteur OCR d’Aspose. Le tutoriel a couvert tout, depuis la configuration du projet, le basculement de l’accélération GPU, la construction de la liste de fichiers, le traitement de chaque image, jusqu’à la persistance des résultats. Que vous extrayiez du texte de fichiers TIFF ou de tout autre format d’image, le même schéma s’applique — il suffit de changer les extensions de fichiers.

Prêt pour l’étape suivante ? Essayez d’intégrer la sortie OCR à un index de recherche, d’alimenter le texte dans un grand modèle de langage, ou expérimentez le traitement parallèle pour gagner des minutes sur des lots massifs. Le ciel est la limite, et vous avez les bases pour construire votre solution.

Des questions ou envie de partager vos propres astuces d’OCR par lots ? Laissez un commentaire ci‑dessous—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}