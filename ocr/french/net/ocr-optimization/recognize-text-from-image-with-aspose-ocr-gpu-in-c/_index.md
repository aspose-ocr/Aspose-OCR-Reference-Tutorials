---
category: general
date: 2026-03-29
description: reconnaître le texte à partir d'une image en utilisant le moteur OCR
  GPU d'Aspose – extraire le texte des fichiers TIFF rapidement et efficacement.
draft: false
keywords:
- recognize text from image
- extract text from tiff
language: fr
og_description: Reconnaissez le texte d’une image instantanément avec Aspose OCR GPU
  en C#. Apprenez à extraire le texte des fichiers TIFF, à configurer les appareils
  et à éviter les pièges courants.
og_title: Reconnaître du texte à partir d'une image avec Aspose OCR GPU – Guide complet
tags:
- OCR
- C#
- Aspose
- GPU
title: reconnaître le texte d'une image avec Aspose OCR GPU en C#
url: /fr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image avec Aspose OCR GPU – Guide complet

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** mais le fichier était un TIFF haute résolution gigantesque ? Vous n'êtes pas seul. Dans de nombreux projets réels, la numérisation d'archives ou le traitement de factures vous laisse avec d'énormes fichiers .tif que les bibliothèques OCR classiques ne supportent pas.  

Heureusement, le moteur GPU d’Aspose OCR peut **reconnaître du texte à partir d'une image** en un éclair, et il télécharge même automatiquement les packs de langues lorsque vous en avez besoin. Dans ce tutoriel, nous vous montrerons également comment **extraire du texte d'un fichier tiff** sans exploser votre budget mémoire.

## Ce dont vous avez besoin

- .NET 6 (ou tout runtime .NET récent) – le code fonctionne également sur .NET Core.  
- Package NuGet Aspose.OCR pour .NET (version 23.10 ou ultérieure).  
- Un GPU avec au moins 2 Go de VRAM – optionnel mais fortement recommandé pour les scans volumineux.  

Si vous n’avez pas de GPU, le moteur CPU fonctionnera toujours ; il suffit de remplacer `GpuOcrEngine` par `OcrEngine`.  

## Installer Aspose OCR pour .NET

Tout d'abord, ajoutez la bibliothèque à votre projet :

```bash
dotnet add package Aspose.OCR
```

## Étape 1 : Initialiser le moteur GPU OCR

Pour **reconnaître du texte à partir d'une image** sur le GPU, vous créez une instance de `GpuOcrEngine`. Cet objet communique directement avec le pilote graphique, ce qui vous offre des gains de vitesse considérables sur les gros fichiers raster.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU engine namespace

// Create a GPU‑accelerated OCR engine
var ocrEngine = new GpuOcrEngine();
```

> **Pourquoi c’est important :** Le moteur GPU décharge les calculs matriciels lourds sur la carte graphique, ce qui est particulièrement utile lorsque l’image source est un TIFF haute résolution (par exemple 3000 × 4000 px ou plus).

## Étape 2 : (Optionnel) Sélectionner le dispositif GPU et limiter la mémoire

Si votre machine possède plusieurs GPU, vous pouvez en choisir un via son `DeviceId`. Vous pouvez également plafonner la VRAM que le moteur peut allouer—utile sur les serveurs partagés.

```csharp
// Choose the first GPU (ID 0) – change if you have more than one
ocrEngine.DeviceId = 0;

// Reserve at most 2 GB of VRAM for this OCR session
ocrEngine.MaxMemoryInMb = 2048;
```

> **Astuce pro :** Lors du traitement de dizaines de pages en lot, gardez `MaxMemoryInMb` légèrement inférieur à la mémoire totale de la carte pour éviter les plantages de type out‑of‑memory.

## Étape 3 : Choisir la langue (et téléchargement automatique si nécessaire)

Aspose OCR est fourni avec l’anglais dès l’installation, mais vous pouvez demander n’importe quelle langue. Si le fichier de langue n’est pas présent localement, le moteur le récupère automatiquement depuis le CDN d’Aspose.

```csharp
// Set the recognition language – English in this example
ocrEngine.Language = Language.English;
```

> **Cas particulier :** Si vous devez reconnaître le japonais ou l’arabe, définissez `Language.Japanese` ou `Language.Arabic`. Le premier appel peut prendre quelques secondes pendant que le pack se télécharge.

## Étape 4 : Reconnaître le texte d’une image TIFF

Nous allons maintenant réellement **extraire du texte d’un tiff**. La méthode `RecognizeImage` renvoie un `OcrResult` contenant le texte brut, les scores de confiance et les boîtes englobantes.

```csharp
// Path to your high‑resolution TIFF file
string imagePath = @"C:\Scans\high_res_scan.tif";

// Perform OCR – this is where the GPU shines
OcrResult result = ocrEngine.RecognizeImage(imagePath);
```

> **Pourquoi le chemin complet ?** Les chemins relatifs fonctionnent, mais les chemins absolus évitent le rare « fichier introuvable » lorsque le répertoire de travail diffère (par ex., lors de l’exécution depuis VS Code vs. Visual Studio).

## Étape 5 : Sortir le texte reconnu

Enfin, affichez le texte dans la console ou écrivez-le dans un fichier. La propriété `Text` contient déjà les sauts de ligne tels qu’ils apparaissent dans l’image.

```csharp
// Print the OCR output to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(result.Text);
```

**Sortie attendue** (troncature pour la brièveté) :

```
=== OCR RESULT ===
Invoice #12345
Date: 2026‑03‑01
Total: $1,274.56
Thank you for your business!
```

Si l’image contenait plusieurs pages, vous pourriez les parcourir en boucle et concaténer les résultats.

## Exemple complet fonctionnel

En rassemblant le tout, voici un programme autonome que vous pouvez copier‑coller dans un nouveau projet console :

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU engine namespace

class Program
{
    static void Main()
    {
        // 1️⃣ Create the GPU OCR engine
        var ocrEngine = new GpuOcrEngine();

        // 2️⃣ (Optional) Pick GPU device & limit VRAM usage
        ocrEngine.DeviceId = 0;            // first GPU
        ocrEngine.MaxMemoryInMb = 2048;    // cap at 2 GB

        // 3️⃣ Choose language – English will be auto‑downloaded if missing
        ocrEngine.Language = Language.English;

        // 4️⃣ Path to the TIFF you want to process
        string tiffPath = @"YOUR_DIRECTORY/high_res_scan.tif";

        // 5️⃣ Run OCR – this returns the recognized text and metadata
        OcrResult result = ocrEngine.RecognizeImage(tiffPath);

        // 6️⃣ Show the result
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
```

Enregistrez le fichier sous `Program.cs`, exécutez `dotnet run`, et observez le GPU faire sa magie.

## Extraire du texte d’un TIFF efficacement – considérations supplémentaires

### Gestion des TIFF multi‑pages

Si votre fichier source contient plus d’une page, Aspose OCR traite chaque page comme une image distincte. Vous pouvez itérer ainsi :

```csharp
var pages = ocrEngine.RecognizeMultipageImage(tiffPath);
foreach (var pageResult in pages)
{
    Console.WriteLine("--- Page ---");
    Console.WriteLine(pageResult.Text);
}
```

### Gestion de la mémoire pour les scans volumineux

- **Réduire l’échelle uniquement si nécessaire** : Le moteur GPU peut traiter la résolution originale, mais si vous atteignez les limites de mémoire, envisagez `ocrEngine.DownscaleFactor = 0.5;`.
- **Libérer** : Appelez `ocrEngine.Dispose();` lorsque vous avez terminé pour libérer rapidement les ressources GPU.

### Pièges courants

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Sortie vide | Mauvais `DeviceId` ou pilote non initialisé | Vérifiez les pilotes GPU, essayez `DeviceId = 0` ou omettez de le définir. |
| Faible précision | Pack de langue incorrect | Définissez `ocrEngine.Language` sur la langue correcte, assurez‑vous que le pack est entièrement téléchargé. |
| Plantage hors‑mémoire | `MaxMemoryInMb` trop élevé pour la carte | Réduisez la limite ou traitez les pages une à une. |

## Astuces pro & bonnes pratiques

- **Traitement par lots** : Enveloppez la boucle OCR dans un `Parallel.ForEach` uniquement si votre GPU possède suffisamment de VRAM ; sinon, le traitement séquentiel évite le throttling.
- **Journalisation** : Utilisez `ocrEngine.Logger = new ConsoleLogger();` pour obtenir des informations détaillées sur les temps d’exécution—utile pour l’optimisation des performances.
- **Sécurité** : Si vous traitez des documents sensibles, activez `ocrEngine.Sanitize = true;` pour supprimer toute métadonnée cachée du résultat.

## Conclusion

Vous disposez maintenant d’une solution complète, de bout en bout, pour **reconnaître du texte à partir d’une image** en utilisant le moteur GPU d’Aspose OCR, et vous savez comment **extraire du texte d’un tiff** efficacement. Le code d’exemple montre chaque étape requise — de l’installation du package NuGet à la gestion des scans multi‑pages et des contraintes de mémoire.  

Ensuite, vous voudrez peut‑être explorer le **post‑traitement** de la sortie OCR (vérification orthographique, extraction par expression régulière des numéros de facture, etc.) ou intégrer le résultat dans une base de données pour des archives consultables. Si vous êtes curieux d’autres formats, essayez d’alimenter un JPEG ou PNG dans le même pipeline — l’API est indépendante du format.  

Des questions sur le choix du GPU, les packs de langues, ou le dimensionnement à des centaines de pages par jour ? Laissez un commentaire ci‑dessous, et bon codage !  

![Diagramme illustrant le pipeline OCR où un TIFF haute résolution est injecté dans le moteur GPU, produisant une sortie de texte reconnu – reconnaître du texte à partir d'une image](https://example.com/ocr-pipeline.png "reconnaître du texte à partir d'une image avec le moteur GPU d'Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}