---
category: general
date: 2026-03-05
description: Convertir TIFF en texte en C# avec Aspose OCR — extraire rapidement le
  texte des fichiers d'images numérisées et apprendre comment charger un fichier image
  en C# pour le traitement OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: fr
og_description: Convertir le TIFF en texte en C# avec Aspose OCR. Découvrez le flux
  de travail complet pour extraire du texte à partir d’images numérisées et charger
  les fichiers image efficacement.
og_title: Convertir un TIFF en texte en C# – Extraire le texte d’une image scannée
tags:
- OCR
- C#
- Aspose
title: Convertir TIFF en texte en C# – Extraire le texte d’une image numérisée
url: /fr/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir TIFF en texte en C# – Extraire le texte d'une image numérisée

Besoin de **convertir TIFF en texte en C#** ? Vous n'êtes pas le seul à vous battre avec des images numérisées multi‑pages qui refusent obstinément de devenir des chaînes recherchables.  
Dans ce guide, nous parcourrons une solution complète, prête à l'emploi, qui prend un fichier TIFF, le transmet à Aspose OCR, et génère du texte brut — sans services supplémentaires, sans magie cachée.

> **Astuce :** Si vous travaillez avec des numérisations haute résolution, activer le traitement GPU peut économiser quelques secondes par page.

Nous vous montrerons également comment **extraire le texte d'images numérisées** et la meilleure façon de **charger un fichier image en C#** dans le moteur OCR, afin que vous puissiez intégrer cette logique dans n'importe quel projet .NET dès aujourd'hui.

---

## Ce dont vous avez besoin

Avant de commencer, assurez-vous d'avoir les éléments suivants sur votre machine :

| Exigence | Raison |
|----------|--------|
| .NET 6.0+ (or .NET Framework 4.7.2+) | Environnement d'exécution moderne, prend en charge `Span<T>` et les I/O asynchrones |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | Le moteur OCR que nous utiliserons |
| A valid Aspose OCR license file (`Aspose.OCR.lic`) | Sans cela, vous atteindrez les limites d'évaluation |
| A TIFF file (single‑ or multi‑page) to test | Exemple utilisé : `scanned_multi_page.tif` |
| GPU with CUDA 11+ (optional) | Accélère la reconnaissance lorsque `EngineMode = Gpu` |

Si l'un de ces éléments vous manque, récupérez le package NuGet maintenant :

```bash
dotnet add package Aspose.OCR
```

---

## Étape 1 : Configurer le projet et importer les espaces de noms

Créez une nouvelle application console (ou ajoutez le code à un projet existant). La première chose que nous faisons est d'importer les classes dont nous aurons besoin.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Pourquoi c'est important :** L'importation de `Aspose.OCR.Image` nous fournit la fabrique `ImageStream`, qui peut lire les fichiers TIFF directement depuis le disque ou un flux. Ignorer cette étape entraînera une erreur de compilation.

---

## Étape 2 : Initialiser le moteur OCR et choisir le mode de traitement

Le moteur OCR doit être configuré **avant** d'assigner une image. C'est ici que nous décidons d'exécuter le traitement sur le CPU ou d'utiliser le GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Si vous êtes sur un serveur sans affichage et sans carte graphique, changez `Gpu` en `Cpu` ou `Auto`.*  
Le mode du moteur influence l'allocation mémoire et la vitesse ; le mode GPU peut être 2‑3× plus rapide sur les TIFF volumineux et haute résolution.

---

## Étape 3 : Appliquer votre licence Aspose OCR

Exécuter sans licence vous limite à quelques pages et ajoute des filigranes. Chargez votre licence tôt afin que chaque opération suivante soit sans restriction.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Erreur courante :** Placer `SetLicense` après `Recognize()` fera revenir le moteur en mode d'essai pour cet appel.

---

## Étape 4 : Charger le fichier TIFF – Gestion des images à page unique et multi‑pages

Aspose OCR peut lire les TIFF multi‑pages nativement, mais vous devez fournir le bon flux. Voici un modèle robuste qui fonctionne pour les deux scénarios.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Pourquoi utiliser `ImageStream.FromFile` ?

- Il masque le `FileStream` sous‑jacent, gérant l'énumération des pages TIFF en interne.  
- Il fonctionne également avec `MemoryStream`, vous permettant de charger des images depuis une base de données ou une API web sans toucher au système de fichiers.

### Cas limite : TIFF très volumineux

Si votre TIFF dépasse 200 Mo, envisagez de le charger page par page pour éviter les exceptions de dépassement de mémoire :

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Étape 5 : Vérifier la sortie

Lorsque vous exécutez le programme, vous devriez voir quelque chose comme :

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Si le texte apparaît illisible, revérifiez :

1. **Résolution** – L'OCR fonctionne mieux avec 300 dpi ou plus.  
2. **EngineMode** – Passez à `Cpu` si le pilote GPU est obsolète.  
3. **Licence** – Assurez‑vous que le chemin du fichier de licence est correct et que le fichier est lisible.

---

## Questions fréquentes (FAQ)

### Cela fonctionne‑t‑il avec d'autres formats d'image ?

Absolument. `ImageStream.FromFile` prend en charge JPEG, PNG, BMP, et même PDF (via Aspose.PDF). Il suffit de remplacer l'extension du fichier.

### Et si je dois traiter des images stockées dans une base de données ?

Lisez le BLOB dans un `MemoryStream` et passez‑le à `ImageStream.FromStream(memoryStream)`. Le moteur OCR le traite de la même façon qu'un flux basé sur un fichier.

### Puis‑je exécuter cela sous Linux ?

Oui—Aspose OCR est multiplateforme. Installez le runtime .NET approprié et assurez‑vous que les bibliothèques natives requises pour le GPU (si utilisé) sont disponibles.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être compilé. Remplacez `YOUR_DIRECTORY` et le chemin du fichier de licence par vos emplacements réels.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Enregistrez ceci sous `Program.cs`, exécutez `dotnet run`, et observez le texte

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}