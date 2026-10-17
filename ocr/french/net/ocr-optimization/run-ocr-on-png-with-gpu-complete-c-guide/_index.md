---
category: general
date: 2026-01-02
description: Exécutez rapidement la reconnaissance optique de caractères (OCR) sur
  des PNG avec Aspose OCR et la prise en charge du GPU. Apprenez à reconnaître le
  texte d’une image, à extraire le texte d’une image et à définir la limite de mémoire
  du GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: fr
og_description: Exécutez la reconnaissance optique de caractères (OCR) sur des PNG
  de manière efficace en tirant parti d'Aspose OCR et de l'accélération GPU. Ce tutoriel
  vous montre comment reconnaître le texte à partir d'une image, extraire le texte
  d'une image et contrôler l'utilisation de la mémoire GPU.
og_title: Exécuter l'OCR sur PNG avec GPU – Guide complet C#
tags:
- OCR
- C#
- GPU
title: Exécuter l'OCR sur PNG avec GPU – Guide complet C#
url: /fr/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter la OCR sur PNG avec GPU – Guide complet C#

Vous avez déjà eu besoin de **exécuter la OCR sur des fichiers PNG** mais vous êtes bloqué par les performances ? Vous n'êtes pas seul. Dans de nombreux pipelines réels, un seul PNG haute résolution peut saturer un moteur OCR fonctionnant uniquement sur CPU, transformant ce qui devrait être une recherche rapide en une attente d’une minute.

Bonne nouvelle : Aspose OCR propose des extensions GPU qui vous permettent de **reconnaître du texte à partir d’une image** en une fraction du temps. Dans ce tutoriel, nous allons parcourir un exemple pratique qui montre exactement comment **exécuter la OCR sur PNG** avec C#, comment **extraire du texte à partir d’une image**, et même comment **définir une limite de mémoire GPU** afin de rester dans votre budget matériel.

Nous couvrirons également le « comment » et le « pourquoi » de chaque étape, afin que vous repartiez avec un modèle mental solide – pas seulement un extrait à copier‑coller.

## Ce que vous allez apprendre

- Les prérequis pour utiliser le support GPU d’Aspose OCR.  
- Comment charger un PNG dans un `Bitmap` et le transmettre au moteur OCR.  
- Comment configurer `GpuDevice` et `GpuMemoryLimitMb` pour des performances optimales.  
- Comment **reconnaître du texte à partir d’une image** et récupérer le résultat en texte brut.  
- Astuces pour gérer les cas limites courants tels que les GPU à faible mémoire ou les PNG multi‑pages.  

À la fin de ce guide, vous pourrez **exécuter la OCR sur PNG** à la vitesse du GPU et contrôler en toute confiance l’empreinte mémoire de vos tâches OCR.

![Diagramme montrant l'exécution de la OCR sur PNG avec accélération GPU](run-ocr-on-png-diagram.png "exemple d'exécution de la OCR sur PNG")

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

1. .NET 6.0 ou supérieur (le code fonctionne également avec .NET Core et .NET Framework).  
2. Un GPU NVIDIA avec prise en charge CUDA (l’exemple utilise l’index de dispositif 0).  
3. Le package NuGet Aspose.OCR et ses extensions GPU (`Aspose.OCR.Extensions`).  
4. Un PNG d’exemple (`input.png`) placé dans un dossier que vous pouvez référencer depuis votre projet.  

Si l’un de ces éléments vous est inconnu, ne vous inquiétez pas — nous indiquerons des alternatives le cas échéant.

---

## Étape 1 – Installer Aspose OCR et les extensions GPU

Première chose à faire. Sans les bonnes bibliothèques, le reste du code ne compilera pas.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Le package `Aspose.OCR.Extensions` inclut les binaires CUDA natifs nécessaires à l’accélération GPU.  
*Astuce :* Si vous êtes sur une machine sans GPU, vous pouvez toujours compiler le projet ; il suffit de définir `PreferGpu = false` plus tard.

---

## Étape 2 – Charger le PNG que vous voulez traiter

Nous allons maintenant réellement **exécuter la OCR sur PNG** en le chargeant dans un `Bitmap`. Cette étape est simple mais mérite une petite précision : `Bitmap` attend un chemin de fichier, assurez‑vous donc que le chemin soit correct par rapport à votre exécutable.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Si le PNG est exceptionnellement grand (par ex., > 5000 px de côté), vous pourriez vouloir le réduire d’abord afin d’éviter d’épuiser la mémoire GPU. C’est là que l’option **définir une limite de mémoire GPU** devient pratique plus tard.

---

## Étape 3 – Créer et configurer le moteur OCR pour l’utilisation du GPU

Voici le cœur du tutoriel : configurer le moteur OCR pour **reconnaître du texte à partir d’une image** en utilisant le GPU. Deux propriétés sont essentielles :

- `GpuDevice` – sélectionne quel dispositif CUDA utiliser.  
- `GpuMemoryLimitMb` – plafonne la quantité de mémoire GPU que le moteur peut allouer.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Pourquoi définir une limite de mémoire ?** Certains GPU partagent la mémoire avec l’affichage ou exécutent plusieurs charges de travail simultanément. En plafonnant l’allocation, vous évitez les plantages « out‑of‑memory », surtout lors du traitement de nombreux PNG en parallèle.

---

## Étape 4 – Définir les options de reconnaissance (langue & préférence GPU)

L’objet `RecognitionOptions` indique au moteur quelle langue rechercher et s’il faut **préférer le GPU** même pour les petites images. Pour la plupart des documents anglais, cela suffit, mais vous pouvez remplacer `Language.English` par d’autres paramètres régionaux pris en charge.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Si vous avez besoin d’**extraire du texte à partir d’une image** dans une langue autre que l’anglais, changez simplement l’énumération `Language`. La bibliothèque prend en charge des dizaines de langues dès le départ.

---

## Étape 5 – Exécuter la OCR et récupérer le résultat

Une fois tout configuré, l’appel final se résume à une seule ligne qui **exécute la OCR sur PNG** et renvoie un objet résultat riche.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` contient non seulement le texte brut (`ocrResult.Text`) mais aussi des scores de confiance, des boîtes englobantes, et même l’image originale avec les mots surlignés — utile si vous devez déboguer ou visualiser l’extraction.

**Sortie attendue** (pour un PNG d’exemple contenant « Hello World ») :

```
=== OCR Output ===
Hello World
```

Si le texte apparaît illisible, vérifiez que le PNG n’est pas corrompu et que la limite de mémoire GPU n’est pas trop basse pour la taille de l’image.

---

## Étape 6 – Gestion des cas limites et bonnes pratiques

### GPU à faible mémoire

Si vous obtenez une exception du type `CudaException: out of memory`, réduisez `GpuMemoryLimitMb` ou découpez le PNG en tuiles avant le traitement. Le découpage peut être réalisé avec `Graphics.DrawImage` sur un clone de `Bitmap`.

### Plusieurs PNG en lot

Lors du traitement d’un dossier de PNG, réutilisez la même instance `OcrEngine` — l’initialiser une seule fois évite les changements de contexte GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Repli sur le CPU

Si aucun GPU n’est disponible, définissez simplement `PreferGpu = false`. Le moteur repassera automatiquement sur le CPU sans modification du code.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console. Il intègre toutes les étapes ci‑dessus, ainsi que quelques vérifications de sécurité.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Enregistrez le fichier sous le nom `Program.cs`, exécutez `dotnet run`, et le texte extrait devrait s’afficher dans la console.

---

## Conclusion

Nous venons de démontrer comment **exécuter la OCR sur PNG** avec les extensions GPU d’Aspose OCR, comment **reconnaître du texte à partir d’une image**, et comment **extraire du texte à partir d’une image** tout en contrôlant la **définition d’une limite de mémoire GPU**. En configurant `GpuDevice` et `GpuMemoryLimitMb`, vous gardez votre application rapide et stable, même sur des GPU modestes.

À partir d’ici, vous pouvez :

- Expérimenter d’autres langues (`Language.French`, `Language.Spanish`).  
- Intégrer l’étape OCR dans un pipeline de traitement de documents plus large.  
- Ajouter du post‑traitement comme la correction orthographique ou l’extraction d’entités pour affiner le texte brut.  

Rappelez‑vous, l’essentiel n’est pas seulement le code mais la compréhension du pourquoi de chaque paramètre. Quand vous savez comment **définir une limite de mémoire GPU** et quand basculer sur le CPU, vous créez des solutions OCR qui s’adaptent avec grâce.

Des questions sur une taille de PNG spécifique, des TIFF multi‑pages, ou le dépannage d’erreurs GPU ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}