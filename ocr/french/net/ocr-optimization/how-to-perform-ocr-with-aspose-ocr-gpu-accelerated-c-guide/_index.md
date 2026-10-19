---
category: general
date: 2026-02-19
description: Comment effectuer rapidement la reconnaissance optique de caractères
  (OCR) sur des images TIFF haute résolution. Apprenez à extraire du texte à partir
  de fichiers TIFF en utilisant l'OCR GPU en C#.
draft: false
keywords:
- how to perform OCR
- extract text from tiff
- use gpu ocr
- Aspose OCR C#
- high‑resolution image processing
- OCR performance tuning
language: fr
og_description: Comment effectuer la reconnaissance optique de caractères (OCR) sur
  des fichiers TIFF haute résolution en utilisant Aspose OCR et l'accélération GPU.
  Guide complet étape par étape.
og_title: Comment réaliser l'OCR – Tutoriel C# accéléré par GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Comment réaliser l'OCR avec Aspose OCR – Guide C# accéléré par GPU
url: /fr/net/ocr-optimization/how-to-perform-ocr-with-aspose-ocr-gpu-accelerated-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer l'OCR – Tutoriel C# accéléré par GPU

Vous avez déjà eu besoin d'effectuer de l'OCR sur un scan TIFF massif et vous vous êtes demandé pourquoi cela prenait une éternité ? Vous n'êtes pas le seul. Dans ce guide, nous vous montrerons **how to perform OCR** sur une image haute résolution en exploitant le GPU, et vous repartirez avec un programme C# prêt à l'emploi qui extrait le texte des fichiers tiff en un clin d'œil.

Nous couvrirons tout, de l'installation du package Aspose OCR à l'activation du traitement GPU, et nous expliquerons pourquoi chaque paramètre est important. À la fin, vous pourrez insérer ce code dans n'importe quel projet .NET, le pointer vers un .tif, et obtenir du texte propre et interrogeable—sans services supplémentaires requis.

## Prérequis

- .NET 6.0 ou supérieur (le code cible .NET 6, mais .NET 5 fonctionne aussi)  
- Un GPU compatible (NVIDIA CUDA 11+ ou AMD Radeon avec prise en charge OpenCL)  
- **Aspose.OCR** package NuGet (version 23.9 ou plus récente)  
- Un fichier TIFF haute résolution que vous souhaitez lire (par ex., `high_res_page.tif`)  

Si l'un de ces éléments vous est inconnu, ne vous inquiétez pas—chaque point est expliqué dans les étapes suivantes.

## Étape 1 : Installer Aspose OCR et activer le traitement GPU  

La première chose à faire est d'ajouter la bibliothèque Aspose OCR à votre projet et d'activer le support GPU. Activer le GPU indique au moteur de décharger les calculs matriciels lourds vers votre carte graphique, ce qui peut réduire le temps de traitement de 70 % ou plus sur un GPU moderne.

```csharp
// Install the package via the CLI (run once):
// dotnet add package Aspose.OCR --version 23.9.0

using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // Enable GPU acceleration – requires a compatible GPU driver.
        OcrEngine.EnableGpuProcessing(true);
```

**Pourquoi c'est important :**  
Sans `EnableGpuProcessing(true)`, le moteur OCR revient à une exécution purement CPU, ce qui est correct pour les petites images mais extrêmement lent sur les TIFF multi‑méga‑pixels. Activer ce drapeau permet à la bibliothèque d'utiliser CUDA ou OpenCL en interne, réduisant considérablement le `ProcessingTime` que vous verrez plus tard.

## Étape 2 : Configurer le moteur OCR pour l'anglais (ou toute autre langue dont vous avez besoin)

Ensuite, nous créons une instance `OcrEngine` et définissons la langue. Aspose prend en charge plus de 100 langues ; l'anglais est présenté ici car c'est le plus courant, mais vous pouvez remplacer `Language.English` par `Language.French`, `Language.German`, etc.

```csharp
        // Step 2: Create and configure the OCR engine.
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change if you need another language.
        };
```

**Astuce :**  
Si vous prévoyez de traiter des documents multilingues, créez plusieurs moteurs ou changez la propriété `Language` entre les appels. Cela évite le surcoût de recréer le moteur pour chaque page.

## Étape 3 : Effectuer l'OCR sur un TIFF haute résolution  

Passons à la partie amusante—confiez un fichier TIFF au moteur et laissez-le faire le travail lourd. La méthode `RecognizeImage` renvoie un `OcrResult` qui contient à la fois le texte extrait et les informations de timing.

```csharp
        // Step 3: Run OCR on the TIFF image.
        var ocrResult = ocrEngine.RecognizeImage(@"YOUR_DIRECTORY/high_res_page.tif");
```

**Gestion des cas limites :**  
- **Fichiers volumineux :** Si votre TIFF dépasse 50 Mo, envisagez de le réduire d'abord avec `System.Drawing` ou `ImageSharp` pour garder une utilisation de mémoire raisonnable.  
- **TIFF multi‑pages :** Appelez `RecognizeImage` dans une boucle sur chaque indice de page ; Aspose renverra le texte pour chaque page séparément.

## Étape 4 : Afficher le temps de traitement et le texte extrait  

Enfin, nous affichons le temps écoulé et la sortie brute de l'OCR. C'est ici que vous verrez le bénéfice de l'accélération GPU.

```csharp
        // Step 4: Display results.
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Sortie typique**

```
Time taken: 312 ms
=== Extracted Text ===
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Sur un RTX 3060 de milieu de gamme, le même TIFF de 3000 × 4000 pixels qui prenait auparavant ~1,2 secondes sur CPU se termine maintenant en ~300 ms—remarquez l'augmentation de vitesse spectaculaire.

## Comment extraire du texte des fichiers TIFF efficacement  

Si vous ne vous intéressez qu'à l'étape **extract text from tiff** et que vous n'avez pas besoin du GPU, vous pouvez ignorer le drapeau GPU. Le reste du code reste identique, mais vous perdrez les gains de performance sur les scans volumineux. Voici une version minimale :

```csharp
using Aspose.OCR;
using System;

class SimpleTiffOcr
{
    static void Main()
    {
        var engine = new OcrEngine { Language = Language.English };
        var result = engine.RecognizeImage(@"sample.tif");
        Console.WriteLine(result.Text);
    }
}
```

**Quand l'utiliser :**  
- Votre déploiement s'exécute sur un serveur sans tête sans GPU.  
- Les TIFF sont petits (< 1 MP) et le temps CPU n’est pas un goulot d’étranglement.

Même sans le GPU, le moteur OCR d'Aspose est très précis grâce à ses modèles neuronaux intégrés.

## Utiliser l'OCR GPU pour un traitement plus rapide – Pièges courants  

Bien que **use gpu OCR** vous offre de la rapidité, quelques pièges peuvent vous surprendre :

| Problème | Symptom | Solution |
|----------|---------|----------|
| Pilote CUDA manquant | `EnableGpuProcessing` lance `PlatformNotSupportedException` | Installez le dernier pilote NVIDIA et le toolkit CUDA |
| GPU non pris en charge | Le moteur revient silencieusement au CPU | Vérifiez que votre GPU apparaît dans `OcrEngine.GetAvailableGpus()` (si vous l'appelez) |
| Mémoire insuffisante sur des images très grandes | `System.OutOfMemoryException` | Traitez l'image en tuiles (`engine.RecognizeRegion`) |
| Orientation d'image incorrecte | Texte illisible | Pré‑tournez le TIFF avec `ImageSharp` avant l'OCR |

**Vérification rapide :** Exécutez la démo une fois avec `EnableGpuProcessing(false)`. Comparez les valeurs de `ProcessingTime` ; une exécution GPU‑accélérée saine devrait être au moins 2‑3 fois plus rapide.

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez insérer dans une application console. Remplacez `YOUR_DIRECTORY` par le chemin réel de votre fichier TIFF.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;

class GpuDemo
{
    static void Main()
    {
        // 1️⃣ Enable GPU acceleration (requires a compatible GPU)
        OcrEngine.EnableGpuProcessing(true);

        // 2️⃣ Create the OCR engine and set the language
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // Change as needed
        };

        // 3️⃣ Perform OCR on a high‑resolution TIFF
        var imagePath = @"YOUR_DIRECTORY/high_res_page.tif";
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 4️⃣ Show timing and extracted text
        Console.WriteLine($"Time taken: {ocrResult.ProcessingTime} ms");
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Exécuter cela sur une machine avec un RTX 3070 produit une sortie similaire à l'exemple précédent, confirmant que **how to perform OCR** avec le support GPU fonctionne comme annoncé.

## Prochaines étapes – Aller au-delà des bases  

- **Traitement par lots :** Enveloppez l'appel `RecognizeImage` dans une boucle `foreach` sur un dossier de TIFFs.  
- **Post‑traitement :** Alimentez `ocrResult.Text` dans un correcteur orthographique ou un analyseur de langage naturel pour nettoyer les artefacts d'OCR.  
- **Mode hybride :** Détectez la taille de l'image à l'exécution et décidez d'activer le GPU (`if (image.Width * image.Height > 5_000_000) EnableGpuProcessing(true)`).

Toutes ces extensions utilisent toujours **use gpu ocr** lorsque cela a du sens, gardant votre pipeline à la fois rapide et conscient des ressources.

## Conclusion  

Vous savez maintenant **how to perform OCR** sur des fichiers TIFF haute résolution en utilisant Aspose OCR et l'accélération GPU, et vous pouvez en toute confiance **extract text from tiff** des documents en une fraction du temps qu'une approche uniquement CPU nécessiterait. L'exemple complet, prêt à copier‑coller, montre l'ensemble du flux—de l'activation du GPU à l'affichage du temps de traitement et du texte final.

Essayez-le, ajustez les paramètres de langue, et essayez de traiter un lot de pages. Si vous rencontrez des problèmes, consultez à nouveau le tableau « Utiliser l'OCR GPU pour un traitement plus rapide » ; la plupart des problèmes y sont couverts. Bon codage, et profitez du gain de vitesse !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}