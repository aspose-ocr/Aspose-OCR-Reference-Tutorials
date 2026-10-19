---
category: general
date: 2026-01-12
description: Tutoriel OCR en C# qui montre comment reconnaître du texte sur une image,
  extraire le texte d’une image en C# et générer un fichier OCR d’image en PDF avec
  les scores de confiance.
draft: false
keywords:
- c# ocr tutorial
- image to pdf ocr
- recognize text image
- ocr confidence scores
- extract text image c#
language: fr
og_description: Apprenez un tutoriel complet C# OCR pour reconnaître le texte d’une
  image, extraire le texte d’une image en C# et créer un document OCR image‑vers‑PDF
  avec des scores de confiance.
og_title: Tutoriel OCR C# – Convertir les images en PDF recherchables
tags:
- OCR
- C#
- PDF
title: Tutoriel OCR C# – Convertir les images en PDF consultables
url: /fr/net/text-recognition/c-ocr-tutorial-turn-images-into-searchable-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tutoriel c# ocr – Transformer des images en PDF recherchables

Vous êtes-vous déjà demandé comment **reconnaître du texte à partir d'images** dans un projet C# sans recourir à des services tiers ? Vous n'êtes pas seul. Dans de nombreuses applications réelles—pensez aux scanners de factures, aux traqueurs de reçus ou aux archives de documents multilingues—les développeurs ont besoin d'un moteur OCR fiable, installé sur site, qui fournit également des scores de confiance.  

Ce **tutoriel c# ocr** vous guidera à travers tout ce dont vous avez besoin : du chargement d’une image, à la sélection des modèles de langue, en passant par l’activation de l’accélération GPU, jusqu’à l’enregistrement du résultat sous forme de PDF recherchable. À la fin, vous disposerez d’un exemple de code prêt à l’emploi qui extrait le texte, rapporte la confiance OCR, et crée éventuellement un fichier *image to pdf ocr*—le tout en moins d’une minute de codage.

## Ce que vous allez créer

- Charger une image multilingue (`sample_multi_lang.jpg` est utilisé comme exemple).  
- Choisir les modèles de langue arabe, hindi et russe (vous pouvez en ajouter d’autres).  
- Activer le traitement GPU si votre machine le supporte.  
- Obtenir le résultat OCR brut **avec les scores de confiance**.  
- Sérialiser le résultat en JSON formaté **ou** écrire un PDF recherchable.  

Aucun service web externe, aucune magie cachée—juste Aspose.OCR pour .NET, quelques lignes de C#, et une explication claire du **pourquoi** de chaque ligne.

## Prérequis

- .NET 6.0 ou supérieur (le code compile sur .NET Core et .NET Framework).  
- Visual Studio 2022 (ou tout autre IDE de votre choix).  
- Une licence Aspose.OCR pour .NET (l’essai gratuit suffit pour les tests).  
- Optionnel : un GPU compatible CUDA si vous souhaitez accélérer la reconnaissance.

> **Astuce :** Si vous n’avez pas de GPU, définissez simplement `UseGpu = false` et le moteur reviendra automatiquement sur le CPU sans aucune modification du code.

## Étape 1 : Installer les packages NuGet requis

Ouvrez la **Console du Gestionnaire de Packages** et exécutez :

```powershell
Install-Package Aspose.OCR
Install-Package Aspose.OCR.Gpu
Install-Package Newtonsoft.Json
```

Ces trois packages vous fournissent le moteur OCR, l’accélération GPU et un sérialiseur JSON pratique pour les scores de confiance.

## Étape 2 : Configurer la structure du projet

Créez un nouveau projet console (`dotnet new console -n AsposeOcrDemo`) et remplacez le fichier `Program.cs` généré par le code ci‑dessous.  
Toute la logique se trouve dans la classe `Program` ; le seul type supplémentaire est une petite méthode d’extension qui formate le résultat OCR en JSON.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Gpu;
using Aspose.OCR.Models;
using Newtonsoft.Json;

namespace AsposeOcrDemo
{
    class Program
    {
        // Step 1: Input image and language models
        private const string InputImagePath = @"YOUR_DIRECTORY/sample_multi_lang.jpg";
        private static readonly string[] Languages = { LanguageModel.Arabic, LanguageModel.Hindi, LanguageModel.Russian };

        // Step 2: Processing options (GPU toggle & output format)
        private const bool UseGpu = true;               // set false if no GPU
        private const string OutputFormat = "Json";     // change to "Pdf" for PDF output

        static void Main()
        {
            // Step 3: Initialise the appropriate OCR engine
            IOcrEngine engine = UseGpu ? (IOcrEngine)new GpuOcrEngine() : new OcrEngine();

            // Step 4: Run OCR – language models are auto‑downloaded if missing
            OcrResult result = engine.Recognize(
                InputImagePath,
                new OcrOptions { LanguageModels = Languages, AutoDownloadResources = true });

            // Step 5: Emit the result in the chosen format
            if (OutputFormat.Equals("json", StringComparison.OrdinalIgnoreCase))
            {
                string json = JsonConvert.SerializeObject(
                    result.GetWordsWithConfidence(),
                    Formatting.Indented);
                Console.WriteLine(json);
            }
            else if (OutputFormat.Equals("pdf", StringComparison.OrdinalIgnoreCase))
            {
                string pdfPath = Path.ChangeExtension(InputImagePath, ".pdf");
                File.WriteAllBytes(pdfPath, result.Pdf);
                Console.WriteLine($"PDF saved to: {pdfPath}");
            }
        }
    }

    // Helper that flattens OcrResult into a JSON‑friendly structure
    internal static class OcrResultExtensions
    {
        public static object GetWordsWithConfidence(this OcrResult result)
        {
            var words = new System.Collections.Generic.List<object>();
            foreach (var w in result.Words)
                words.Add(new
                {
                    Text = w.Text,
                    Confidence = w.Confidence,
                    BoundingBox = new { w.Bounds.X, w.Bounds.Y, w.Bounds.Width, w.Bounds.Height }
                });

            return new
            {
                RecognizedText = result.Text,
                LanguageModels = result.UsedLanguageModels,
                Words = words,
                ProcessingTimeMs = result.ProcessingTime.TotalMilliseconds
            };
        }
    }
}
```

### Pourquoi ce code fonctionne

1. **Bascule GPU** – `GpuOcrEngine` exploite les cœurs CUDA ; l’opérateur ternaire rend le changement sans effort.  
2. **Téléchargement automatique des langues** – `AutoDownloadResources = true` garantit que les modèles arabe, hindi et russe sont récupérés lors de la première exécution de l’application.  
3. **Scores de confiance** – `result.Words` contient une propriété `Confidence` pour chaque mot reconnu ; la méthode d’extension les formate en un objet JSON propre.  
4. **PDF recherchable** – `result.Pdf` est déjà un PDF entièrement recherchable, il suffit donc d’écrire le tableau d’octets sur le disque. Aucune bibliothèque supplémentaire n’est nécessaire.

## Étape 6 : Exécuter l’exemple

Ouvrez un terminal, placez‑vous dans le dossier du projet, puis lancez :

```bash
dotnet run
```

Si vous avez choisi la sortie **JSON**, vous verrez quelque chose comme :

```json
{
  "RecognizedText": "مرحبا Hello Привет",
  "LanguageModels": [
    "Arabic",
    "Hindi",
    "Russian"
  ],
  "Words": [
    {
      "Text": "مرحبا",
      "Confidence": 0.98,
      "BoundingBox": { "X": 45, "Y": 12, "Width": 120, "Height": 30 }
    },
    {
      "Text": "Hello",
      "Confidence": 0.99,
      "BoundingBox": { "X": 180, "Y": 12, "Width": 80, "Height": 30 }
    },
    {
      "Text": "Привет",
      "Confidence": 0.97,
      "BoundingBox": { "X": 280, "Y": 12, "Width": 110, "Height": 30 }
    }
  ],
  "ProcessingTimeMs": 312
}
```

Si vous avez opté pour le **PDF**, la console affiche le chemin et vous trouverez un PDF recherchable juste à côté de l’image source.

## Questions fréquentes & cas particuliers

- **Et si un modèle de langue n’est pas disponible ?**  
  Le moteur OCR lève une `ResourceNotFoundException` claire. Comme nous avons `AutoDownloadResources = true`, le modèle manquant est téléchargé automatiquement lors de la première exécution, de sorte que l’exception apparaît rarement en production.

- **Puis‑je traiter un lot d’images ?**  
  Bien sûr. Enveloppez l’appel `engine.Recognize` dans une boucle `foreach` parcourant un répertoire de fichiers. La même classe `OcrResultExtensions` fonctionne pour chaque image.

- **Ai‑je besoin d’une licence pour le GPU ?**  
  Non. L’essai gratuit fonctionne à la fois sur CPU et GPU. Une licence complète supprime le filigrane d’essai et supprime les limites de pages.

- **Quelle est la précision des scores de confiance ?**  
  Les scores varient de 0,0 (aucune confiance) à 1,0 (confiance parfaite). En pratique, tout score supérieur à 0,90 est fiable pour les traitements en aval ; vous pouvez filtrer les mots à faible confiance si vous avez besoin d’une validation plus stricte.

## Étape 7 : Prochaines étapes (élargir votre boîte à outils OCR)

1. **Ajouter d’autres langues** – il suffit d’ajouter `LanguageModel.French` (ou tout autre modèle supporté) au tableau `Languages`.  
2. **Combiner OCR et conversion PDF/A** – Aspose.PDF peut intégrer la couche OCR dans un document PDF/A‑2b conforme pour l’archivage.  
3. **Intégrer avec Azure Functions** – encapsulez la logique dans un point d’accès serverless pour traiter les téléchargements à la volée.  
4. **Ajuster les seuils de confiance** – utilisez `result.Words.Where(w => w.Confidence < 0.85)` pour signaler les mots incertains et les soumettre à une révision manuelle.

---

### TL;DR

Ce **tutoriel c# ocr** vous montre comment :

- Charger une image et sélectionner plusieurs modèles de langue.  
- Activer l’accélération GPU avec un simple drapeau booléen.  
- Récupérer les résultats OCR **avec les scores de confiance** et les sérialiser en JSON.  
- Éventuellement écrire un PDF recherchable (**image to pdf ocr**).  

Tout cela est réalisable avec quelques lignes de code, un essai gratuit d’Aspose.OCR, et le code ci‑dessus. Essayez, modifiez la liste des langues, et vous disposerez d’un pipeline OCR prêt pour la production en quelques minutes.

---

![c# ocr tutorial example image](https://example.com/placeholder-image.jpg "c# ocr tutorial example image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}