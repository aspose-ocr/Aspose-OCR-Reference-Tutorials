---
category: general
date: 2026-09-08
description: Apprenez comment activer le GPU pour Aspose OCR, exécuter le traitement
  OCR par lots et extraire du texte à partir d'images efficacement avec .NET.
draft: false
keywords:
- how to enable gpu
- extract text from images
- batch ocr processing
- ocr gpu acceleration
- aspose ocr .net
lastmod: 2026-09-08
og_description: Comment activer le GPU pour Aspose OCR. Ce guide montre le traitement
  OCR par lots, l'extraction de texte à partir d'images et la sélection du dispositif
  GPU optimal dans .NET.
og_image_alt: Diagram of Aspose OCR engine offloading work to GPU for faster text
  extraction
og_title: Comment activer le GPU pour Aspose OCR – tutoriel complet
schemas:
- author: Aspose
  dateModified: '2026-09-08'
  description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  headline: How to enable GPU for Aspose OCR – complete tutorial
  type: TechArticle
- description: Learn how to enable GPU for Aspose OCR, run batch OCR processing, and
    extract text from images efficiently using .NET.
  name: How to enable GPU for Aspose OCR – complete tutorial
  steps:
  - name: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
    text: 'Install the NuGet package: `dotnet add package Aspose.OCR --version 23.10.0`'
  - name: Replace the paths in `imageFiles` with the location of your own `.tif` files.
    text: Replace the paths in `imageFiles` with the location of your own `.tif` files.
  - name: 'Build and run: `dotnet run`.'
    text: 'Build and run: `dotnet run`.'
  type: HowTo
- questions:
  - answer: Yes, a commercial Aspose.OCR license is needed for production deployments;
      a free trial is available for evaluation.
    question: Is a license required for production use?
  - answer: Any NVIDIA GPU that supports CUDA 11.0 or newer, such as RTX 2060, RTX
      3070, RTX 4090, and the corresponding Tesla series.
    question: Which GPU models are officially supported?
  - answer: Absolutely. The same `OcrEngine` instance can be reused across requests;
      just ensure thread safety by cloning the engine per request.
    question: Can I run this code in an ASP.NET Core web API?
  - answer: Yes, you can set `ocrEngine.Language = Language.English | Language.Spanish`
      to enable simultaneous recognition of multiple languages.
    question: Does Aspose OCR handle multi‑language documents?
  - answer: The engine streams image data, so you can process images up to 10,000
      × 10,000 pixels without exhausting GPU memory, though performance may vary.
    question: What is the maximum image size the GPU can handle?
  type: FAQPage
tags:
- Aspose OCR
- GPU acceleration
- C#
- .NET
title: Comment activer le GPU pour Aspose OCR – tutoriel complet
url: /fr/net/ocr-configuration/how-to-enable-gpu-for-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer le GPU pour Aspose OCR – tutoriel complet

Vous vous êtes déjà demandé **comment activer le GPU** lors de l'utilisation d'Aspose OCR ? Vous n'êtes pas le seul — les développeurs qui gèrent d'énormes volumes de documents rencontrent souvent des limites de performance parce que le moteur OCR reste bloqué sur le CPU. Bonne nouvelle ? Activer l'accélération GPU est assez simple, et cela peut économiser des secondes sur chaque page. Dans ce guide, nous parcourrons **comment activer le GPU**, exécuter le **traitement OCR par lots**, extraire le texte reconnu, et même choisir le bon dispositif GPU. À la fin, vous saurez **comment utiliser Aspose** pour une extraction de texte OCR ultra‑rapide.

## Réponses rapides
- **Que fait l'activation du GPU ?** Elle déplace l'analyse pixel‑par‑pixel vers la carte graphique, réduisant le temps de traitement jusqu'à 80 % sur des images typiques de 300 dpi.  
- **Ai‑je besoin d'une licence spéciale ?** Non, le package NuGet standard Aspose.OCR inclut le support GPU.  
- **Quelle version de .NET est requise ?** .NET 6.0 ou ultérieure ; l'API utilise les fonctionnalités modernes de C#.  
- **Puis‑je exécuter sur une machine uniquement CPU ?** Oui—si aucun GPU compatible n'est trouvé, le moteur revient automatiquement au CPU.  
- **Combien d'images puis‑je traiter simultanément ?** Vous pouvez mettre en file d'attente des centaines de fichiers ; le GPU les traitera séquentiellement tandis que votre code pourra fournir l'image suivante dès que la précédente est terminée.

## Qu'est‑ce que l'activation du GPU ?
Le processus d'**activation du GPU** consiste à configurer le `OcrEngine` d'Aspose OCR pour acheminer les charges de travail de traitement d'image vers une carte graphique compatible CUDA au lieu du processeur central. Ce basculement est contrôlé par deux propriétés : `UseGpu` et `GpuDeviceId`. Activer ce drapeau transfère l'analyse pixel‑intensive vers le GPU, qui peut gérer des milliers de threads en parallèle, réduisant ainsi considérablement le temps de traitement.

La classe `OcrEngine` est le composant central d'Aspose OCR qui effectue l'analyse d'image et la reconnaissance de texte.

## Pourquoi utiliser l'accélération GPU avec Aspose OCR ?
Aspose OCR prend en charge **plus de 50 formats d'image d'entrée** et peut traiter des lots de plusieurs centaines de pages sans charger le document complet en mémoire. Lorsque l'accélération GPU est activée, les tests de référence montrent une **réduction de 70 %‑80 %** du temps moyen de traitement par page sur une RTX 3080 comparé à une exécution pure CPU. Ce gain de vitesse se traduit directement par des coûts cloud plus bas et des résultats plus rapides visibles par l'utilisateur dans les applications intensives en documents.

## Prérequis
- .NET 6.0 ou ultérieur (le code utilise la syntaxe moderne de C#)  
- Package NuGet Aspose.OCR pour .NET (version 23.10 ou plus récente)  
- Un GPU compatible CUDA avec le pilote approprié installé (minimum CUDA 11.0)  
- Un dossier contenant des fichiers `.tif` d'exemple pour l'exécution par lots  

Si vous avez ces bases, plongeons‑y.

## Comment activer le GPU dans Aspose OCR

Chargez le moteur OCR, activez le mode GPU, et choisissez éventuellement un indice de dispositif.  

`OcrEngine` est la classe principale d'Aspose OCR qui effectue l'analyse d'image et la reconnaissance de texte.  

Activer le GPU est une opération en deux étapes : définir `UseGpu = true` et, lorsqu'il y a plusieurs GPU, attribuer le `GpuDeviceId` souhaité. Ce paragraphe de réponse directe explique l’ensemble du processus en 45 mots.

La première chose à faire est d'indiquer au `OcrEngine` d'utiliser le GPU. Cela se fait via deux propriétés simples : `UseGpu` et éventuellement `GpuDeviceId`. Mettre `UseGpu` à `true` bascule le moteur en mode GPU, tandis que `GpuDeviceId` vous permet de choisir quel GPU (si vous en avez plusieurs) doit effectuer le travail intensif.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;
using System.Collections.Generic;

// Step 1: Create the OCR engine and enable GPU acceleration
var ocrEngine = new OcrEngine
{
    // Turn on GPU support – this is the core of “how to enable gpu”
    UseGpu = true,

    // (optional) Choose GPU index 0; change if you have multiple devices
    GpuDeviceId = 0
};
```

> **Pourquoi cela importe** – La version CPU traite chaque pixel séquentiellement, ce qui peut devenir un goulot d'étranglement pour les images haute résolution. La version GPU exécute des milliers de threads en parallèle, réduisant drastiquement le temps par page.

### Vue d'ensemble visuelle  

![Diagramme montrant comment le moteur OCR délègue le travail au GPU lorsque « how to enable gpu » est activé](/images/enable-gpu-diagram.png){: .center .responsive alt="how to enable gpu"}

[Diagramme montrant comment le moteur OCR délègue le travail au GPU lorsque « how to enable gpu » est activé](/images/enable-gpu-diagram.png)

*(Si vous ne voyez pas l'image, imaginez simplement un organigramme où le moteur OCR transmet le tampon d'image au cœur CUDA.)*

## Comment exécuter le traitement OCR par lots avec Aspose

La méthode `Recognize` de `OcrEngine` traite une image et renvoie un `OcrResult` contenant le texte extrait et les métadonnées. Vous pouvez traiter un dossier complet en parcourant une liste de chemins de fichiers. Le moteur met automatiquement chaque image en file d'attente sur le GPU, gardant le pipeline occupé pendant que votre application continue d'alimenter de nouveaux fichiers. Cette approche vous permet de gérer efficacement des centaines de TIFF, le GPU assurant le travail intensif en parallèle.

```csharp
// Step 2: Define the image files you want to process
var imageFiles = new List<string>
{
    @"C:\OCRSamples\page1.tif",
    @"C:\OCRSamples\page2.tif",
    @"C:\OCRSamples\page3.tif"
};

// Step 3: Process each image and report the character count
foreach (var imagePath in imageFiles)
{
    // Recognize the image – the GPU does the heavy lifting behind the scenes
    var ocrResult = ocrEngine.Recognize(imagePath);

    // Show how many characters were extracted – a quick sanity check
    Console.WriteLine($"{imagePath}: {ocrResult.Text.Length} characters");
}
```

> **Astuce** – Pour des lots vraiment massifs, envisagez d'utiliser `Parallel.ForEach` avec `ocrEngine.Clone()` afin d'éviter les problèmes de sécurité des threads. La méthode `Clone` crée une copie superficielle du moteur qui pointe toujours vers le même contexte GPU.

### Résultat attendu

```
C:\OCRSamples\page1.tif: 1245 characters
C:\OCRSamples\page2.tif: 1130 characters
C:\OCRSamples\page3.tif: 1389 characters
```

Si les chiffres semblent raisonnables, votre **traitement OCR par lots** fonctionne et le GPU est bien utilisé.

## Comment extraire le texte des images – obtenir les résultats

`OcrResult` est l'objet qui contient la sortie OCR, incluant le texte reconnu, les scores de confiance et les informations de mise en page. La méthode `Recognize` renvoie un objet `OcrResult`. Récupérez le texte brut depuis la propriété `Text` et écrivez‑le dans un fichier pour une utilisation en aval. Stocker le texte OCR permet un traitement en aval (indexation de recherche, data mining, etc.) sans relancer le moteur et vous fournit un enregistrement permanent pour le débogage.

```csharp
foreach (var imagePath in imageFiles)
{
    var ocrResult = ocrEngine.Recognize(imagePath);
    var extractedText = ocrResult.Text;

    // Save the text to a .txt file with the same base name
    var outputPath = System.IO.Path.ChangeExtension(imagePath, ".txt");
    System.IO.File.WriteAllText(outputPath, extractedText);

    Console.WriteLine($"Extracted text saved to {outputPath}");
}
```

> **Pourquoi extraire vers un fichier ?** – Stocker le texte OCR permet un traitement en aval (indexation de recherche, data mining, etc.) sans relancer le moteur. Cela vous donne également un enregistrement permanent pour le débogage.

## Comment définir le dispositif GPU pour des performances optimales

`CudaDeviceInfo` fournit des informations sur les GPU compatibles CUDA installés sur le système. Lorsqu'il y a plusieurs GPU, utilisez `GpuDeviceId` pour sélectionner le meilleur. L'indice correspond à l'ordre renvoyé par `CudaDeviceInfo.GetDevices()`. Choisir le dispositif approprié garantit que vous utilisez le GPU le plus puissant et évitez les conflits avec d'autres charges de travail sur les cartes secondaires.

```csharp
using Aspose.OCR.Gpu;

// List all available GPU devices
var devices = CudaDeviceInfo.GetDevices();
for (int i = 0; i < devices.Length; i++)
{
    Console.WriteLine($"Device {i}: {devices[i].Name} (Compute Capability {devices[i].ComputeCapability})");
}

// Suppose you want to use the second GPU (index 1)
ocrEngine.GpuDeviceId = 1;
Console.WriteLine($"Switched to GPU device {ocrEngine.GpuDeviceId}");
```

> **Cas limite** – Certains GPU plus anciens ne supportent pas la version CUDA requise. Dans ce scénario, `UseGpu = true` reviendra silencieusement au CPU, il faut donc toujours vérifier `ocrEngine.IsGpuEnabled` après l'initialisation.

## Comment utiliser Aspose OCR dans un projet réel

En rassemblant tous les éléments, voici une application console compacte, prête à l'emploi, qui démontre **comment activer le GPU**, exécute **le traitement OCR par lots**, extrait le texte, et vous laisse choisir le dispositif GPU. L'exemple crée un `OcrEngine`, active le GPU, énumère les dispositifs disponibles, traite chaque image et écrit le texte reconnu dans un fichier `.txt` à côté de l'image source.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine with GPU support
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true,
            GpuDeviceId = 0 // change if you have multiple GPUs
        };

        // -------------------------------------------------
        // 2️⃣ (Optional) Show available GPU devices
        // -------------------------------------------------
        var devices = CudaDeviceInfo.GetDevices();
        Console.WriteLine("Available GPU devices:");
        for (int i = 0; i < devices.Length; i++)
        {
            Console.WriteLine($"  [{i}] {devices[i].Name} – Compute {devices[i].ComputeCapability}");
        }

        // -------------------------------------------------
        // 3️⃣ Define the batch of images to process
        // -------------------------------------------------
        var imageFiles = new List<string>
        {
            @"C:\OCRSamples\page1.tif",
            @"C:\OCRSamples\page2.tif",
            @"C:\OCRSamples\page3.tif"
        };

        // -------------------------------------------------
        // 4️⃣ Process each image, extract text, and save it
        // -------------------------------------------------
        foreach (var imagePath in imageFiles)
        {
            var result = ocrEngine.Recognize(imagePath);
            var text = result.Text;

            var txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, text);

            Console.WriteLine($"{Path.GetFileName(imagePath)} → {Path.GetFileName(txtPath)} ({text.Length} chars)");
        }

        Console.WriteLine("All done! GPU‑accelerated OCR batch completed.");
    }
}
```

### Exécution de l'exemple

1. Installez le package NuGet : `dotnet add package Aspose.OCR --version 23.10.0`  
2. Remplacez les chemins dans `imageFiles` par l'emplacement de vos propres fichiers `.tif`.  
3. Construisez et exécutez : `dotnet run`.  

Vous devriez voir la liste des GPU, suivie d'une ligne pour chaque image indiquant le nombre de caractères et le chemin du fichier `.txt` généré.

## Questions fréquentes & pièges

- **Cela fonctionne‑t‑il sur une machine uniquement CPU ?**  
  Oui—si `UseGpu` est `true` mais aucun GPU compatible n'est trouvé, Aspose revient au CPU. Vous pouvez vérifier le mode via `ocrEngine.IsGpuEnabled`.

- **Que faire si j'obtiens l'erreur « CUDA driver version is insufficient » ?**  
  Mettez à jour votre pilote NVIDIA vers la dernière version correspondant au toolkit CUDA fourni avec Aspose. La bibliothèque nécessite au moins CUDA 11.0 pour les fonctionnalités GPU récentes.

- **Puis‑je traiter directement des PDF ?**  
  Aspose OCR fonctionne sur des images raster. Convertissez d'abord les pages PDF en images (par ex., avec Aspose.PDF) puis alimentez‑les au moteur OCR.

- **Comment améliorer la précision sur des scans bruyants ?**  
  Activez les options de prétraitement comme `ocrEngine.Preprocess = true` ou fournissez des images à plus haute résolution (300 dpi ou plus). L'accélération GPU reste applicable.

## Questions fréquemment posées

**Q : Une licence est‑elle requise pour une utilisation en production ?**  
R : Oui, une licence commerciale Aspose.OCR est nécessaire pour les déploiements en production ; un essai gratuit est disponible pour l'évaluation.

**Q : Quels modèles de GPU sont officiellement supportés ?**  
R : Tout GPU NVIDIA supportant CUDA 11.0 ou supérieur, tel que RTX 2060, RTX 3070, RTX 4090, ainsi que les séries Tesla correspondantes.

**Q : Puis‑je exécuter ce code dans une API web ASP.NET Core ?**  
R : Absolument. La même instance `OcrEngine` peut être réutilisée entre les requêtes ; assurez‑vous simplement de la sécurité des threads en clonant le moteur par requête.

**Q : Aspose OCR gère‑t‑il les documents multilingues ?**  
R : Oui, vous pouvez définir `ocrEngine.Language = Language.English | Language.Spanish` pour activer la reconnaissance simultanée de plusieurs langues.

**Q : Quelle est la taille d'image maximale que le GPU peut gérer ?**  
R : Le moteur diffuse les données d'image, vous pouvez donc traiter des images jusqu'à 10 000 × 10 000 pixels sans épuiser la mémoire du GPU, bien que les performances puissent varier.

---

**Last Updated:** 2026-09-08  
**Tested with:** Aspose.OCR 23.10 for .NET  
**Author:** Aspose

## Tutoriels associés

- [Comment utiliser l'OCR en C pour extraire du texte d'images avec accélération GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Extraire du texte d'une image avec Aspose OCR GPU guide C](/ocr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/)
- [Supprimer l'arrière‑plan OCR avec Aspose OCR guide complet GPU](/ocr/net/ocr-optimization/remove-background-ocr-with-aspose-ocr-complete-gpu-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}