---
category: general
date: 2026-02-25
description: Reconnaître du texte à partir d’une image rapidement grâce à l’OCR accéléré
  par GPU. Apprenez à activer le mode GPU, charger une image pour l’OCR et extraire
  le texte d’un fichier TIFF.
draft: false
keywords:
- recognize text from image
- set gpu mode
- gpu accelerated ocr
- load image for ocr
- extract text from tiff
language: fr
og_description: Reconnaître le texte d’une image instantanément grâce à l’OCR accéléré
  par GPU. Tutoriel C# étape par étape couvrant la configuration du mode GPU, le chargement
  de l’image pour l’OCR et l’extraction du texte d’un fichier TIFF.
og_title: Reconnaître le texte à partir d'une image avec OCR accéléré par GPU – Guide
  C#
tags:
- Aspose OCR
- C#
- GPU computing
title: Reconnaître le texte d’une image en utilisant l’OCR accéléré par GPU en C#
url: /fr/net/ocr-optimization/recognize-text-from-image-using-gpu-accelerated-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image avec OCR accéléré par GPU en C#

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** alors que votre CPU était surchargé par un scan haute résolution ? Vous n'êtes pas seul. Dans de nombreux projets réels—par exemple la numérisation de factures ou l'archivage de vieux journaux—un seul fichier TIFF peut bloquer votre pipeline pendant plusieurs minutes. La bonne nouvelle ? Aspose.OCR vous permet d'activer un commutateur et de confier le travail lourd à votre GPU, transformant une opération lente en une quasi‑instantanée.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : comment **activer le mode GPU**, comment **charger l’image pour l’OCR**, et comment **extraire le texte des fichiers TIFF**. À la fin, vous disposerez d’un exemple autonome, prêt pour la production, que vous pourrez intégrer à n’importe quel projet .NET 6+.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Le SDK .NET 6 (ou supérieur) installé.  
- Visual Studio 2022 ou tout autre éditeur de votre choix.  
- Le package NuGet Aspose.OCR (`Aspose.OCR`) ajouté à votre projet.  
- Un GPU compatible DirectX 11 ou supérieur (la plupart des GPU modernes le sont).  
  *Si vous n’avez pas de GPU, vous pouvez toujours exécuter le code avec `GpuMode.Auto` — la bibliothèque reviendra automatiquement au CPU.*

> **Astuce :** Vérifiez que le pilote de votre GPU est à jour ; des pilotes obsolètes peuvent provoquer des erreurs d’initialisation obscures.

## Étape 1 – Créer le moteur OCR et définir le mode GPU

La première chose dont vous avez besoin est une instance de `OcrEngine`. Cet objet contient toute la configuration, y compris le choix d’utiliser ou non le GPU.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // Step 1: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Enable GPU acceleration.
            // Use GpuMode.Auto if you want the library to pick CPU when a GPU isn’t available.
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled);

            // The rest of the workflow continues below…
        }
    }
}
```

**Pourquoi c’est important :** Activer le mode GPU déplace le pré‑traitement d’image gourmand en calculs (binarisation, suppression du bruit, etc.) vers la carte graphique. Sur un RTX 3060 de milieu de gamme, vous pouvez observer un **gain de vitesse de 3‑5×** par rapport à un traitement purement CPU.

## Étape 2 – Charger l’image pour l’OCR (exemple TIFF)

Aspose.OCR accepte de nombreux formats, mais le TIFF est courant pour les documents numérisés car il conserve une qualité sans perte. Utilisez `ImageStream.FromFile` pour lire le fichier en mémoire.

```csharp
// Step 2: Load the high‑resolution TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"C:\Data\high_res_scan.tif");

// Optional: If you need to work with a stream (e.g., from a web API), use:
// ocrEngine.Image = ImageStream.FromStream(yourInputStream);
```

**Cas particulier :** Certains fichiers TIFF contiennent plusieurs pages. `ImageStream.FromFile` ne lit que la première page. Si vous devez traiter chaque page, parcourez `ImageInfo.Pages` et transmettez chaque page au moteur séparément.

## Étape 3 – Effectuer la reconnaissance

Une fois le moteur configuré et l’image chargée, appelez `Recognize()`. La méthode renvoie un objet `OcrResult` contenant le texte brut et des métadonnées supplémentaires.

```csharp
// Step 3: Run OCR
OcrResult result = ocrEngine.Recognize();

// The result may include confidence scores per line, if you enable them in the config.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(result.Text);
```

**Et si le texte apparaît illisible ?**  
- Assurez‑vous que l’image est dans une orientation lisible (pivotez si nécessaire).  
- Ajustez les options de pré‑traitement comme `ocrEngine.Config.DeskewEnabled = true;`.  
- Pour les documents multilingues, définissez `ocrEngine.Config.Language = Language.English;` ou l’énumération appropriée.

## Étape 4 – Vérifier la sortie et gérer les erreurs

Une implémentation robuste vérifie les résultats nuls et intercepte les exceptions potentielles (par ex., pilotes GPU manquants).

```csharp
try
{
    OcrResult result = ocrEngine.Recognize();

    if (result?.Text == null)
    {
        Console.WriteLine("No text detected – double‑check the image quality.");
    }
    else
    {
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
    }
}
catch (Exception ex)
{
    Console.WriteLine($"OCR failed: {ex.Message}");
    // You might want to fallback to CPU mode here:
    // ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
}
```

**Pourquoi l’envelopper ?** L’initialisation du GPU peut lever une `DllNotFoundException` si les bibliothèques natives requises sont absentes. Le bloc `catch` vous offre une voie de dégradation élégante.

## Exemple complet, exécutable

En rassemblant le tout, voici un programme complet que vous pouvez compiler et exécuter immédiatement. Remplacez le chemin du fichier par un vrai TIFF présent sur votre machine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace GpuOcrDemo
{
    public class Program
    {
        public static void Main()
        {
            // 1️⃣ Create OCR engine and enable GPU acceleration
            var ocrEngine = new OcrEngine();
            ocrEngine.Config.SetGpuMode(GpuMode.Enabled); // or GpuMode.Auto for fallback

            // 2️⃣ Load the image you want to process
            string imagePath = @"C:\Data\high_res_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Optional: tweak preprocessing (helps with noisy scans)
            ocrEngine.Config.DeskewEnabled = true;
            ocrEngine.Config.RemoveNoiseEnabled = true;

            // 4️⃣ Run recognition and handle the result
            try
            {
                OcrResult result = ocrEngine.Recognize();

                if (string.IsNullOrWhiteSpace(result?.Text))
                {
                    Console.WriteLine("No text found – consider improving image quality.");
                }
                else
                {
                    Console.WriteLine("=== Recognized Text ===");
                    Console.WriteLine(result.Text);
                }
            }
            catch (Exception e)
            {
                Console.WriteLine($"Error during OCR: {e.Message}");
                // Fallback to CPU if GPU failed
                ocrEngine.Config.SetGpuMode(GpuMode.Disabled);
                // You could retry here…
            }
        }
    }
}
```

**Sortie attendue**

Si le TIFF contient du texte anglais lisible, vous verrez quelque chose comme :

```
=== Recognized Text ===
Invoice #12345
Date: 2024‑11‑08
Total Amount: $1,235.00
...
```

Si l’image est vide ou illisible, la console vous conseillera de vérifier le fichier source.

## Questions fréquentes & variantes

| Question | Réponse |
|----------|---------|
| **Puis‑je traiter du JPEG ou du PNG à la place du TIFF ?** | Absolument. `ImageStream.FromFile` fonctionne avec n’importe quel format supporté par Aspose.OCR (PNG, JPEG, BMP, etc.). |
| **Que faire s’il y a plusieurs pages dans un même TIFF ?** | Parcourez `ImageInfo.Pages` et affectez chaque page à `ocrEngine.Image` avant d’appeler `Recognize()`. |
| **Ai‑je besoin d’une licence pour Aspose.OCR ?** | Une évaluation gratuite fonctionne jusqu’à 100 pages. En production, achetez une licence pour supprimer le filigrane d’évaluation. |
| **Comment changer le modèle de langue ?** | Définissez `ocrEngine.Config.Language = Language.Spanish;` (ou toute autre énumération prise en charge). |
| **Existe‑t‑il un moyen d’obtenir les scores de confiance ?** | Activez `ocrEngine.Config.EnableConfidence = true;` et inspectez `result.Confidence` ligne par ligne. |

## Conclusion

Vous savez maintenant comment **reconnaître du texte à partir d’une image** en utilisant une **pipeline OCR accélérée par GPU** en C#. En **activant le mode GPU**, **chargeant une image pour l’OCR**, et **extraitant le texte des fichiers TIFF**, vous avez construit une solution rapide et évolutive prête pour les charges de travail réelles.

Et après ? Essayez de chaîner ce code avec un générateur de PDF pour créer des PDF recherchables, ou alimentez les chaînes extraites dans un pipeline de traitement du langage naturel. Vous pouvez également expérimenter avec `GpuMode.Auto` pour rendre votre application adaptable aux environnements sans GPU.

Bon codage, et que vos traitements OCR soient ultra‑rapides ! 

![recognize text from image example](https://example.com/ocr-demo.png "recognize text from image using GPU‑accelerated OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}