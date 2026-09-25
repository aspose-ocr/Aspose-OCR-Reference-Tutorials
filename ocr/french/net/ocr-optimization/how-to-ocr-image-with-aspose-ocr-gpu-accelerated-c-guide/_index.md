---
category: general
date: 2026-02-17
description: Apprenez à faire de l’OCR d’image avec Aspose OCR sur GPU. Code pas à
  pas pour reconnaître le texte d’une image, charger une image haute résolution, définir
  l’ID du dispositif GPU et extraire le texte avec Aspose.
draft: false
keywords:
- how to ocr image
- recognize text from image
- load high resolution image
- set gpu device id
- extract text using aspose
language: fr
og_description: Comment effectuer la reconnaissance OCR d’une image avec Aspose OCR
  sur GPU. Suivez le tutoriel complet en C# pour reconnaître le texte d’une image,
  charger une image haute résolution, définir l’ID du dispositif GPU et extraire le
  texte à l’aide d’Aspose.
og_title: Comment faire de l’OCR d’image avec Aspose OCR – Guide C# accéléré par GPU
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Comment effectuer l'OCR d’une image avec Aspose OCR – Guide C# accéléré par
  GPU
url: /fr/net/ocr-optimization/how-to-ocr-image-with-aspose-ocr-gpu-accelerated-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR d'image avec Aspose OCR – Guide C# accéléré par GPU

Vous vous êtes déjà demandé **comment faire de l'OCR d'image** lorsque le fichier est un scan massif de 300 DPI et que vous avez besoin de résultats en quelques secondes ? Vous n'êtes pas seul—les développeurs luttent constamment contre les moteurs d'OCR lents fonctionnant uniquement sur le CPU, surtout sur des images haute résolution. La bonne nouvelle ? Aspose OCR vous permet d'exploiter votre GPU, réduisant considérablement le temps de traitement tout en conservant une grande précision.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui **reconnaît le texte à partir de l'image**, vous montre comment **charger une image haute résolution**, vous permet de **définir l'ID du dispositif GPU**, et enfin **d'extraire le texte avec Aspose**. À la fin, vous disposerez d'un programme autonome que vous pourrez intégrer à n'importe quel projet .NET.

## Ce dont vous aurez besoin

- **.NET 6.0** ou version ultérieure (le code fonctionne également sur .NET Framework 4.7+)
- **Aspose.OCR for .NET** package NuGet (version 23.11 ou plus récente)
- Une machine avec GPU activé et CUDA 11+ (optionnel mais recommandé)
- Un JPEG/PNG haute résolution que vous souhaitez OCRiser (par ex., `highres_scan.jpg`)

Si l'un de ces éléments vous manque, récupérez le package NuGet avec :

```bash
dotnet add package Aspose.OCR
```

Aucune bibliothèque native supplémentaire n'est requise ; Aspose regroupe le runtime CUDA pour vous.

![diagramme comment faire de l'OCR d'image](image-placeholder.png "Diagramme illustrant le pipeline OCR accéléré par GPU – comment faire de l'OCR d'image")

## Étape 1 : Créer le moteur OCR et définir l'ID du dispositif GPU  

La première chose à faire est d'indiquer à Aspose d'exécuter le traitement sur le GPU. C'est ici que **set GPU device ID** entre en jeu—si vous avez plusieurs GPU, vous pouvez choisir celui qui convient à votre charge de travail.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine with GPU processing mode
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    ProcessingMode = ProcessingMode.Gpu, // Enable GPU acceleration
    GpuDeviceId = 0                     // Choose GPU #0 (change if you have several)
});
```

> **Pourquoi c’est important :** Le traitement GPU décharge le travail d'analyse d'image lourd vers des cœurs parallèles, vous offrant un gain de vitesse de 3‑5× sur les scans typiques. Si vous ne définissez pas `GpuDeviceId`, Aspose utilise par défaut le premier dispositif, ce qui suffit pour les configurations à GPU unique.

## Étape 2 : Charger une image haute résolution  

Ensuite, nous **load high resolution image** les données dans un format que le moteur OCR comprend. Aspose fournit `ImageStream.FromFile`, qui lit le fichier en mémoire sans conversions inutiles.

```csharp
// Path to your high‑resolution scan (300 DPI or more)
string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";

// Load the image; ImageStream handles large files efficiently
var image = ImageStream.FromFile(imagePath);
```

> **Astuce :** Si votre image se trouve dans un bucket cloud, vous pouvez également fournir directement un `Stream`—remplacez simplement `FromFile` par `FromStream(yourStream)`. Le moteur la traitera toujours comme une source haute résolution.

## Étape 3 : Reconnaître le texte à partir de l'image  

Maintenant que le moteur est prêt et que l'image est chargée, nous pouvons **recognize text from image**. La méthode `Recognize` renvoie un objet `OcrResult` contenant le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

```csharp
// Perform OCR; this call is where the GPU does its magic
OcrResult recognitionResult = ocrEngine.Recognize(image);

// For debugging, you can also inspect recognitionResult.Regions
```

> **Cas particulier :** Si l'image est trop sombre ou très bruitée, envisagez de la pré‑traiter (par ex., augmenter le contraste) avant d’appeler `Recognize`. Aspose propose une API `Preprocess`, mais pour la plupart des scans propres, les paramètres par défaut fonctionnent bien.

## Étape 4 : Extraire le texte avec Aspose et l'afficher  

Enfin, nous **extract text using Aspose** en lisant simplement la propriété `Text` du résultat. Imprimons‑le dans la console, mais vous pourriez également l’écrire dans un fichier ou une base de données.

```csharp
// Output the plain‑text result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognitionResult.Text);
```

**Sortie attendue** (exemple pour une facture numérisée) :

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,254.00
Thank you for your business!
```

Si vous voyez des caractères illisibles, vérifiez que l'image est réellement haute résolution et que la langue correcte est définie dans `OcrEngineSettings` (par ex., `Language = Language.English`).

## Exemple complet fonctionnel  

En rassemblant le tout, voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console :

```csharp
// ------------------------------------------------------------
// Full OCR example – Aspose OCR with GPU acceleration
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            ProcessingMode = ProcessingMode.Gpu, // GPU acceleration
            GpuDeviceId = 0                      // Change if you have multiple GPUs
        });

        // 2️⃣ Load a high‑resolution image
        string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";
        var image = ImageStream.FromFile(imagePath);

        // 3️⃣ Recognize text from the image
        OcrResult result = ocrEngine.Recognize(image);

        // 4️⃣ Extract and display the plain text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

Exécutez le programme avec `dotnet run`. Sur un GPU correct, vous devriez voir le résultat OCR apparaître en moins d'une seconde, même pour un scan de 5 MB, 300 DPI.

## Questions fréquentes & astuces pro  

### Et si je n’ai pas de GPU ?  
Vous pouvez toujours utiliser Aspose OCR sur le CPU en définissant `ProcessingMode = ProcessingMode.Cpu`. L'API reste identique ; seule la performance change.

### Comment gérer plusieurs langues ?  
Ajoutez `Language = Language.Multilingual` (ou un enum spécifique comme `Language.French`) dans `OcrEngineSettings`. Aspose chargera automatiquement les packs de langues appropriés.

### Puis‑je traiter les PDF directement ?  
Oui—Aspose OCR peut d'abord extraire les images des PDF, puis exécuter l'OCR sur chaque page. Combinez `Aspose.PDF` avec le même `OcrEngine` pour un pipeline fluide.

### Quand devrais‑je ajuster `GpuDeviceId` ?  
Si votre serveur exécute à la fois du traitement d'images et des charges de travail d'apprentissage automatique, vous pourriez dédier le GPU 1 à l'OCR (`GpuDeviceId = 1`) et garder le GPU 0 libre pour les tâches d’inférence.

### Comment améliorer la précision sur des scans bruyants ?  
Pré‑traitez l'image :  
```csharp
image = image.AdjustContrast(1.2f).ApplyThreshold(0.5f);
```
Ces méthodes font partie des utilitaires de traitement d'image d'Aspose.

## Conclusion  

Vous savez maintenant **comment faire de l'OCR d'image** avec Aspose OCR et l'accélération GPU, comment **reconnaître le texte à partir de l'image**, la bonne façon de **charger une image haute résolution**, comment **définir l'ID du dispositif GPU**, et enfin comment **extraire le texte avec Aspose** dans un programme C# propre et prêt pour la production.

Faites tourner le code sur différents fichiers — essayez un reçu flou, un flyer brillant ou même une note manuscrite. Expérimentez avec les paramètres de langue et les étapes de pré‑traitement pour voir comment la précision évolue.

Ensuite, vous pourriez explorer le **traitement par lots** (boucler sur un dossier de scans) ou intégrer le résultat OCR dans un **index de recherche** pour une récupération rapide des documents. Les deux sujets s'appuient naturellement sur les concepts abordés ici et constituent d'excellents projets de suivi.

Bon codage, et que vos pipelines OCR soient rapides et impeccables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}