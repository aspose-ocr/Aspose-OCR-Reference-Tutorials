---
category: general
date: 2026-03-26
description: Exécutez la reconnaissance optique de caractères (OCR) sur une image
  en utilisant le support GPU d'Aspose OCR en C#. Apprenez à charger une image pour
  l'OCR, à définir l'ID du dispositif GPU et à extraire rapidement le texte de l'image.
draft: false
keywords:
- run OCR on image
- extract text from image
- load image for OCR
- recognize text from document
- set GPU device ID
language: fr
og_description: Exécutez la reconnaissance optique de caractères (OCR) sur une image
  en utilisant Aspose OCR GPU en C#. Ce guide montre comment charger une image pour
  l'OCR, définir l'ID du dispositif GPU et extraire le texte de l'image de manière
  efficace.
og_title: Effectuer l'OCR sur une image avec GPU en C# – Guide complet
tags:
- C#
- OCR
- GPU
- Aspose
title: Exécuter l'OCR sur une image avec le GPU en C# – Guide complet de programmation
url: /fr/net/ocr-optimization/run-ocr-on-image-with-gpu-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter la reconnaissance optique de caractères (OCR) sur une image avec GPU en C# – Guide de programmation complet

Vous avez déjà eu besoin de **run OCR on image** mais avez trouvé la version CPU douloureusement lente ? Vous n'êtes pas seul. Dans de nombreuses applications réelles—pensez aux scanners de factures ou aux archives de documents à grande échelle—le goulot d'étranglement est le moteur OCR lui‑même.  

Dans ce tutoriel, nous allons parcourir un **exemple complet et exécutable** qui montre comment **load image for OCR**, éventuellement **set GPU device ID**, et enfin **extract text from image** en utilisant l’API accélérée par GPU d’Aspose OCR. À la fin, vous serez capable de **recognize text from document** en une fraction du temps qu’une approche pure‑CPU nécessiterait.

## What You’ll Learn

- Comment installer et référencer les packages Aspose.OCR et Aspose.OCR.Gpu.  
- Les étapes exactes pour **run OCR on image** avec accélération GPU.  
- Pourquoi le choix du bon **GPU device ID** est important sur les machines multi‑GPU.  
- Astuces pour gérer les gros fichiers, stratégies de secours et pièges courants.  

### Prerequisites

| Requirement | Reason |
|-------------|--------|
| .NET 6.0 ou ultérieur | Fonctionnalités modernes du langage et meilleures performances |
| Visual Studio 2022 (ou tout IDE C#) | Pour une configuration de projet simplifiée |
| NVIDIA GPU avec support CUDA (optionnel) | Nécessaire uniquement si vous voulez l’accélération GPU |
| Packages NuGet Aspose.OCR & Aspose.OCR.Gpu | Fournit la classe `GpuOcrEngine` |

Si vous n’avez pas de GPU, ne paniquez pas — le code revient automatiquement à l’engin CPU, que nous aborderons plus loin.

---

## Step 1: Install Aspose OCR Packages

Avant de pouvoir **run OCR on image**, vous avez besoin des bibliothèques. Ouvrez votre terminal (ou la console du gestionnaire de packages) et exécutez :

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Ces deux packages apportent le moteur OCR de base ainsi que les extensions spécifiques au GPU. Après l’installation, vous verrez les références suivantes dans votre `.csproj` :

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
  <PackageReference Include="Aspose.OCR.Gpu" Version="23.10.0" />
</ItemGroup>
```

> **Pro tip :** Gardez les versions des packages synchronisées ; des versions incompatibles peuvent provoquer des erreurs d’exécution.

---

## Step 2: Create a GPU‑Enabled OCR Engine

Maintenant que les bibliothèques sont en place, **run OCR on image** en utilisant le GPU. La classe `GpuOcrEngine` est le point d’entrée pour le traitement accéléré.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Instantiate the GPU OCR engine
        var gpuEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Choose which GPU to use – 0 = first GPU
        // This is where the "set GPU device ID" keyword comes into play.
        gpuEngine.DeviceId = 0;

        // The rest of the workflow continues in the following steps...
```

**Pourquoi un GPU ?**  
Les cœurs GPU excellent dans les opérations parallèles sur les pixels, exactement ce dont l’OCR a besoin lorsqu’il scanne des images haute résolution. En définissant `DeviceId`, vous indiquez à la bibliothèque quelle carte physique utiliser—pratique sur les stations de travail disposant de plusieurs GPU.

---

## Step 3: Load Image for OCR

Avant la reconnaissance, vous devez **load image for OCR**. Aspose fournit une méthode statique pratique qui prend en charge de nombreux formats (JPEG, PNG, TIFF, etc.).

```csharp
        // Step 3: Load the image you want to recognize
        // Replace the path with your actual file location.
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");

        // Quick sanity check – ensure the image was loaded.
        if (ocrImage == null)
        {
            Console.WriteLine("Failed to load image. Check the file path.");
            return;
        }
```

> **Edge case :** Si l’image dépasse 10 Mo, envisagez de la sous‑échantillonner d’abord afin d’éviter l’épuisement de la mémoire GPU. Vous pouvez le faire avec `ocrImage.Resize(width, height)` avant la reconnaissance.

---

## Step 4: Recognize Text from Document

Avec le moteur prêt et l’image chargée, il est temps de **recognize text from document**. La méthode `Recognize` renvoie un objet `OcrResult` contenant le texte brut et des métadonnées supplémentaires.

```csharp
        // Step 4: Run the OCR process on the image
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);

        // Verify that OCR succeeded
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR failed or returned empty result.");
            return;
        }
```

**Que se passe‑t‑il en coulisses ?**  
Le moteur GPU transmet les données de pixels aux kernels CUDA, qui effectuent la binarisation, la segmentation des caractères et l’inférence du réseau neuronal—tout cela en parallèle. C’est pourquoi vous pouvez **run OCR on image** des fichiers qui prendraient autrement des secondes sur CPU.

---

## Step 5: Extract Text from Image and Output

Enfin, nous **extract text from image** et l’affichons. Vous pouvez également écrire le résultat dans un fichier, une base de données, ou le transmettre à des pipelines NLP en aval.

```csharp
        // Step 5: Output the recognized plain‑text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // Optional: Save to a .txt file for later processing
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }
}
```

**Résultat attendu** (truncaté pour la brièveté) :

```
=== OCR Result ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Si vous exécutez le programme et voyez un bloc similaire, félicitations — vous avez réussi à **run OCR on image** en utilisant l’accélération GPU !

---

## Handling Situations Without a GPU (Fallback)

Que faire si la machine cible ne possède pas de GPU compatible ? Le constructeur `GpuOcrEngine` lèvera une `GpuNotSupportedException`. Enveloppez l’initialisation dans un try‑catch et revenez à `OcrEngine` (CPU) comme suit :

```csharp
        try
        {
            var gpuEngine = new GpuOcrEngine { DeviceId = 0 };
            // Continue with GPU workflow...
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not available – switching to CPU OCR.");
            var cpuEngine = new OcrEngine();
            OcrResult result = cpuEngine.Recognize(ocrImage);
            Console.WriteLine(result.Text);
        }
```

Ce schéma garantit que votre application reste fonctionnelle quel que soit le matériel, une considération cruciale pour les déploiements cloud.

---

## Full Working Example (Copy‑Paste Ready)

Voici le **programme complet**—aucune pièce manquante, il suffit de remplacer les chemins de fichiers par les vôtres.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // Namespace for GPU support

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Create a GPU‑enabled OCR engine
        GpuOcrEngine gpuEngine;
        try
        {
            gpuEngine = new GpuOcrEngine { DeviceId = 0 }; // set GPU device ID
        }
        catch (GpuNotSupportedException)
        {
            Console.WriteLine("GPU not detected. Falling back to CPU engine.");
            var cpuEngine = new OcrEngine();
            RunCpuOcr(cpuEngine);
            return;
        }

        // 2️⃣ Load image for OCR
        var ocrImage = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        if (ocrImage == null)
        {
            Console.WriteLine("Unable to load image – check the path.");
            return;
        }

        // 3️⃣ Recognize text from document
        OcrResult ocrResult = gpuEngine.Recognize(ocrImage);
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("OCR returned no text.");
            return;
        }

        // 4️⃣ Extract text from image and output
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        System.IO.File.WriteAllText(@"C:\Output\ocr_result.txt", ocrResult.Text);
    }

    // Helper for CPU fallback
    static void RunCpuOcr(OcrEngine cpuEngine)
    {
        var img = OcrImage.FromFile(@"C:\Images\large_document.jpg");
        var result = cpuEngine.Recognize(img);
        Console.WriteLine("=== CPU OCR Result ===");
        Console.WriteLine(result.Text);
    }
}
```

> **Note :** Le code ci‑dessus **extracts text from image** automatiquement et l’écrit dans `ocr_result.txt`. Ajustez les chemins selon vos besoins.

---

## Frequently Asked Questions & Tips

| Question | Answer |
|----------|--------|
| *Do I need a specific NVIDIA driver?* | Oui—CUDA 11.x ou plus récent est recommandé. Consultez les notes de version d’Aspose pour la compatibilité exacte. |
| *Can I process multiple images concurrently?* | Absolument. Enveloppez l’appel OCR dans une boucle `Parallel.ForEach`, mais gardez à l’esprit les limites de mémoire du GPU. |
| *What if the OCR result contains garbled characters?* | Essayez d’ajuster le pré‑traitement de l’image : `ocrImage.Binarize()` ou `ocrImage.Deskew()` avant la reconnaissance. |
| *Is there a way to limit the language model?* | Définissez `gpuEngine.Language = OcrLanguage.English;` pour accélérer le traitement si vous n’avez besoin que de l’anglais. |

---

## Conclusion

Vous disposez maintenant d’une **solution complète, de bout en bout** pour **run OCR on image**  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}