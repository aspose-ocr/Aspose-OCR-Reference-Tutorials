---
category: general
date: 2026-01-13
description: Apprenez à reconnaître le texte d’une image et à extraire rapidement
  le texte d’un reçu à l’aide d’Aspose OCR. Comprend les étapes de chargement de l’image
  pour l’OCR et de définition de l’ID du dispositif GPU.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for ocr
- set gpu device id
language: fr
og_description: Reconnaissez le texte d’une image instantanément avec Aspose OCR.
  Suivez ce guide étape par étape pour charger l’image pour l’OCR, définir l’ID du
  dispositif GPU et extraire le texte du reçu.
og_title: Reconnaître du texte à partir d'une image – Guide complet C# accéléré par
  GPU
tags:
- Aspose OCR
- C#
- GPU computing
title: Reconnaître le texte à partir d'une image avec Aspose OCR – Tutoriel C# accéléré
  par GPU
url: /fr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image – Guide complet C# accéléré par GPU

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** mais la version CPU était douloureusement lente ? Peut‑être essayez‑vous d'**extraire du texte d'un reçu** et la latence tue votre expérience utilisateur. La bonne nouvelle, c’est que vous n’avez pas à vous contenter de performances médiocres — le package GPU d’Aspose OCR peut turbo‑charger le processus, et le code ne tient que quelques lignes.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre comment **charger une image pour l’OCR**, configurer le GPU avec **set GPU device ID**, puis récupérer le résultat en texte brut. À la fin, vous disposerez d’un extrait prêt à être intégré qui fonctionne sur n’importe quelle machine Windows ou Linux moderne avec une carte NVIDIA prise en charge.

---

## Ce dont vous aurez besoin

- **.NET 6+** (ou .NET Framework 4.7.2+) – l’API fonctionne avec les deux.
- Package NuGet **Aspose.OCR** **plus** le module **Aspose.OCR.Gpu**.
- Un GPU NVIDIA avec au moins 2 Go de VRAM (la démo limite l’utilisation à 1 Go).
- Une image d’exemple, par ex. un reçu scanné (`receipt.jpg`).

Si vous avez déjà un projet, exécutez simplement `dotnet add package Aspose.OCR` et `dotnet add package Aspose.OCR.Gpu`. Aucune bibliothèque native supplémentaire n’est requise ; le SDK fournit les binaires CUDA nécessaires.

---

## Implémentation étape par étape

### ## Comment reconnaître du texte à partir d'une image avec Aspose OCR et GPU

Voici le **programme complet et autonome**. Copiez‑collez‑le dans un nouveau projet console et lancez `Ctrl+F5`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑accelerated namespace

class GpuOcrDemo
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize a GPU‑enabled OCR engine
        // -------------------------------------------------
        var ocrEngine = new GpuOcrEngine();

        // -------------------------------------------------
        // Step 2: (Optional) Select the GPU device and limit memory usage
        // -------------------------------------------------
        ocrEngine.DeviceId = 0;        // set GPU device ID – first GPU in the system
        ocrEngine.MaxMemoryMb = 1024;  // cap at 1 GB to avoid OOM on shared machines

        // -------------------------------------------------
        // Step 3: Load the image you want to recognize
        // -------------------------------------------------
        var receiptImage = OcrImage.FromFile(@"YOUR_DIRECTORY/receipt.jpg");

        // -------------------------------------------------
        // Step 4: Perform OCR – here we extract text from receipt (English)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);

        // -------------------------------------------------
        // Step 5: Output the recognized plain text
        // -------------------------------------------------
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

> **Astuce :** Si votre machine possède plusieurs GPU, modifiez `DeviceId` à `1`, `2`, etc., pour choisir la carte la moins occupée. Le SDK lèvera une claire `GpuDeviceNotFoundException` si l’ID est hors limites.

### ### Étape 1 : Charger l’image pour l’OCR

L’appel `OcrImage.FromFile` fait plus que lire un bitmap — il pré‑traite l’image (redressement, binarisation) selon des heuristiques internes. C’est pourquoi **load image for OCR** est une étape distincte : vous pouvez remplacer par un `MemoryStream` si votre image réside dans une base de données.

```csharp
var receiptImage = OcrImage.FromFile(@"C:\Invoices\receipt.jpg");
```

Si vous devez **reconnaître du texte à partir d'une image** déjà en mémoire :

```csharp
using (var ms = new MemoryStream(File.ReadAllBytes(@"receipt.jpg")))
{
    var receiptImage = OcrImage.FromStream(ms);
}
```

### ### Étape 2 : Définir l’ID du dispositif GPU et les limites de mémoire

Les ressources GPU sont limitées. En exposant `DeviceId` et `MaxMemoryMb`, Aspose vous permet de **set GPU device ID** en toute sécurité, évitant qu’un processus monopolise toute la carte.

```csharp
ocrEngine.DeviceId = 0;        // first GPU
ocrEngine.MaxMemoryMb = 1024; // 1 GB ceiling
```

Si vous dépassez la limite de mémoire, le moteur déversera automatiquement les données vers la RAM système, ce qui est plus lent mais évite les plantages.

### ### Étape 3 : Extraire le texte du reçu (reconnaître du texte à partir d'une image)

La méthode `Recognize` effectue le travail lourd. Vous pouvez passer n’importe quelle langue prise en charge par Aspose OCR ; pour les reçus, l’anglais fonctionne la plupart du temps, mais vous pouvez aussi ajouter `OcrLanguage.Spanish` ou un pack de langue personnalisé.

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, OcrLanguage.English);
Console.WriteLine(ocrResult.Text);
```

**Sortie attendue** (exemple) :

```
Store: QuickMart
Date: 2025-12-01
Total: $23.45
Thank you for shopping!
```

---

## Variations courantes & cas limites

| Situation | Ce qu'il faut changer | Pourquoi |
|-----------|-----------------------|----------|
| **Plusieurs reçus dans une même image** | Appelez `ocrEngine.Recognize` sur chaque région découpée (utilisez `OcrImage.Crop`) | Améliore la précision car le moteur voit une zone plus petite et plus propre. |
| **Scans basse résolution (<150 dpi)** | Pré‑agrandissez avec `receiptImage.Resize(2.0)` avant la reconnaissance | Une densité de pixels plus élevée donne plus de données au GPU. |
| **Reçus non anglais** | Passez `OcrLanguage.French` (ou un `.traineddata` personnalisé) | Les modèles spécifiques à une langue réduisent les faux positifs. |
| **GPU non disponible** | Repli sur `OcrEngine` (CPU) dans un bloc try‑catch | Garantit que l’application fonctionne toujours sur des serveurs sans affichage. |

```csharp
try
{
    var gpuEngine = new GpuOcrEngine();
    // configure GPU as shown earlier …
    var result = gpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
catch (GpuDeviceNotFoundException)
{
    // Graceful fallback
    var cpuEngine = new OcrEngine();
    var result = cpuEngine.Recognize(receiptImage, OcrLanguage.English);
    Console.WriteLine(result.Text);
}
```

---

## Conseils pour un OCR prêt pour la production

- **Traitement par lots :** Enveloppez la boucle de reconnaissance dans `Parallel.ForEach` mais limitez le degré de parallélisme au nombre de flux GPU que vous pouvez allouer (généralement 1‑2 par carte).
- **Hygiène de la mémoire :** Libérez rapidement les objets `OcrImage` (`receiptImage.Dispose()`), surtout lors du traitement de milliers de reçus.
- **Journalisation :** Capturez `ocrResult.Confidence` pour chaque ligne ; une faible confiance peut déclencher un workflow de révision manuelle.
- **Sécurité :** Lors du traitement de reçus sensibles, assurez‑vous que les fichiers image sont stockés dans des dossiers temporaires chiffrés et supprimés après le traitement.

---

## Conclusion

Vous disposez maintenant d’un **exemple complet et exécutable** montrant comment **reconnaître du texte à partir d'une image** avec l’accélération GPU d’Aspose OCR, **charger l’image pour l’OCR**, **set GPU device ID**, et enfin **extraire le texte du reçu** en quelques étapes concises. Le code est prêt à être copié‑collé, et les explications vous donnent suffisamment de contexte pour l’adapter à des scénarios multilingues, multi‑GPU ou à haut débit.

Prêt pour le prochain défi ? Essayez d’alimenter un flux vidéo en direct dans `GpuOcrEngine` pour une numérisation de reçus en temps réel, ou intégrez le résultat à une API de comptabilité. Le ciel est la limite lorsqu’on combine un OCR GPU rapide avec un design C# propre.

*Bon codage, et que votre OCR soit toujours rapide !*

![recognize text from image demo screenshot](placeholder-image.png "recognize text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}