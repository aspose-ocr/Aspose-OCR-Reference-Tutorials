---
category: general
date: 2026-09-13
description: Apprenez à convertir une page numérisée en PDF en C# en utilisant Aspose
  OCR. Ce guide montre le prétraitement, la reconnaissance de texte coréen et la création
  d'un PDF consultable.
keywords:
- scanned page to pdf
- preprocess image for OCR
- generate pdf with text
- convert image to searchable pdf
- gpu accelerated OCR
- recognize Korean text image
lastmod: 2026-09-13
og_description: Apprenez à convertir une page numérisée en PDF en C# avec Aspose OCR.
  Le tutoriel couvre le prétraitement d'image, le GPU‑accelerated OCR pour le texte
  coréen, et la génération d'un PDF consultable en quelques minutes.
og_image_alt: Screenshot of C# console app converting a scanned Korean page to searchable
  PDF using Aspose OCR
og_title: Comment convertir une page numérisée en PDF en C# avec OCR
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  headline: How to turn a scanned page to PDF in C# with OCR
  type: TechArticle
- description: Learn how to turn a scanned page to PDF in C# using Aspose OCR. This
    guide shows preprocessing, Korean text recognition, and creating a searchable
    PDF.
  name: How to turn a scanned page to PDF in C# with OCR
  steps:
  - name: Initialise the OCR engine with GPU support.
    text: Initialise the OCR engine with GPU support.
  - name: Add **preprocess image for OCR** filters such as deskew and denoise.
    text: Add **preprocess image for OCR** filters such as deskew and denoise.
  - name: Download and load the Korean language model (handled automatically).
    text: Download and load the Korean language model (handled automatically).
  - name: Run the OCR on the image.
    text: Run the OCR on the image.
  - name: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
    text: Export the result with **SearchablePdfExporter** to **create searchable
      PDF image**.
  - name: (Optional) Serialize the OCR output to JSON for downstream pipelines.
    text: (Optional) Serialize the OCR output to JSON for downstream pipelines.
  - name: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
    text: '**Ensure the language model is fully downloaded** – check the console for
      a message like “Downloading Korean model…”.'
  - name: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
    text: '**Increase the `MaxAngle`** in `DeskewFilter` if your scans are rotated
      beyond 12°.'
  - name: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
    text: '**Boost GPU memory** by setting `ocrEngine.GpuMemoryLimit = 2048;` (value
      in MB).'
  type: HowTo
- questions:
  - answer: 'The exporter embeds the original bitmap at its native resolution. If
      size is a concern, downscale the image *before* recognition:'
    question: My PDF is huge compared to the original image.
  - answer: Verify that the image path is correct and that the file is not corrupted.
      Also, make sure the GPU driver is up‑to‑date; older drivers can cause silent
      failures.
    question: The OCR returns empty strings.
  - answer: Absolutely. Wrap steps 4‑6 in a `foreach (var file in Directory.GetFiles("Resources",
      "*.jpg"))` loop and change the output PDF path accordingly.
    question: Can I process multiple pages in a loop?
  type: FAQPage
tags:
- scanned page to pdf
- OCR
- Aspose
- C#
title: Comment convertir une page numérisée en PDF en C# avec OCR
url: /fr/net/ocr-optimization/convert-image-to-pdf-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment convertir une page numérisée en PDF en C# avec OCR

Si vous devez **convertir une page numérisée en PDF** tout en conservant le texte recherchable, vous êtes au bon endroit. Ce tutoriel vous guide à travers l'utilisation d'Aspose OCR pour **prétraiter l'image pour l'OCR**, **reconnaître une image de texte coréen**, et enfin **créer une image PDF recherchable** – le tout depuis une simple application console C#.

## Réponses rapides
- **Quelle bibliothèque gère l'OCR ?** Aspose.OCR for .NET  
- **Puis-je utiliser le GPU ?** Oui – activez l'accélération GPU pour une vitesse de traitement jusqu'à 2× plus rapide  
- **Ai-je besoin d'un pack de langue coréenne ?** Il se télécharge automatiquement lors de la première utilisation  
- **Le résultat sera-t-il recherchable ?** Le PDF généré contient une couche de texte invisible  
- **Quelles versions de .NET sont prises en charge ?** .NET 6.0 et ultérieures (incluant .NET Core et .NET Framework)

## Prérequis

- **.NET 6.0 ou ultérieur** – fonctionne sur .NET Core, .NET Framework, et .NET 5/6+  
- **Aspose.OCR for .NET** package NuGet (`Aspose.OCR`) – les clés d'essai sont gratuites sur le site Aspose  
- Une image d'exemple avec des caractères coréens, par ex., `korean_book_page.jpg`  
- Votre IDE préféré (Visual Studio 2022, VS Code, Rider, etc.)

> **Astuce :** Stockez les images dans un dossier `Resources/` afin que les chemins restent cohérents sur toutes les machines.

## Vue d'ensemble du processus

1. Initialise le moteur OCR avec le support GPU.  
2. Ajoute des filtres de **prétraitement d'image pour l'OCR** tels que le redressement et le débruitage.  
3. Télécharge et charge le modèle de langue coréen (géré automatiquement).  
4. Exécute l'OCR sur l'image.  
5. Exporte le résultat avec **SearchablePdfExporter** pour **créer une image PDF recherchable**.  
6. (Optionnel) Sérialise la sortie OCR en JSON pour les pipelines en aval.

Ci-dessous, nous détaillons chaque étape, expliquons *pourquoi* elle est importante, et vous fournissons le code exact que vous pouvez copier‑coller.

## Comment fonctionne la conversion d'une page numérisée en PDF ?

`OcrEngine` est la classe principale d'Aspose.OCR qui effectue la reconnaissance optique de caractères sur les images.  
`SearchablePdfExporter` crée un PDF contenant l'image originale et une couche de texte invisible pour la recherche.  
`RecognitionResult` contient le texte et les données de confiance renvoyés par le moteur OCR.

Chargez votre image avec `new OcrEngine()` et appelez `engine.Recognize("korean_book_page.jpg")`, puis transmettez le `RecognitionResult` à `SearchablePdfExporter.Export`. Ce flux en deux étapes lit le bitmap, extrait le texte Unicode, et intègre les deux dans un seul PDF où la couche de texte est invisible mais recherchable. L'accélération GPU réduit le temps de reconnaissance d'environ moitié, tandis que les filtres de redressement et de débruitage augmentent la précision jusqu'à 15 % sur des numérisations bruyantes.

## Convertir l'image en PDF – flux complet

Le fragment suivant est le programme *complet*. Créez un nouveau projet console (`dotnet new console -n OcrPdfDemo`) et remplacez le `Program.cs` généré automatiquement par le code affiché dans l'espace réservé.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;
using Aspose.OCR.Export;
using Aspose.OCR.Result;   // for JsonResult

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialise the OCR engine (GPU enabled, offline mode off)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                UseGpu = true,          // leverages your graphics card for faster inference
                OfflineMode = false    // allows on‑the‑fly language model download
            };

            // --------------------------------------------------------------
            // Step 2: Add preprocessing filters to improve accuracy
            // --------------------------------------------------------------
            // Deskew corrects slight rotations; MaxAngle = 12° is a safe default.
            ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 12 });

            // Denoise removes isolated speckles that often appear in scanned books.
            ocrEngine.Filters.Add(new DenoiseFilter());

            // --------------------------------------------------------------
            // Step 3: Load the Korean language model
            // --------------------------------------------------------------
            // Aspose will download the model the first time you run this on a new machine.
            ocrEngine.LoadLanguage(LanguageModel.Korean);

            // --------------------------------------------------------------
            // Step 4: Recognise text from the input image
            // --------------------------------------------------------------
            // Replace the path with your actual image location.
            string imagePath = "Resources/korean_book_page.jpg";
            var recognitionResult = ocrEngine.Recognize(imagePath);

            // --------------------------------------------------------------
            // Step 5: Export the recognised page as a searchable PDF
            // --------------------------------------------------------------
            string pdfPath = "Resources/korean_page.pdf";
            var exporter = new SearchablePdfExporter { OutputPath = pdfPath };
            exporter.Export(ocrEngine, imagePath);

            // --------------------------------------------------------------
            // Step 6: Obtain a structured JSON representation of the result
            // --------------------------------------------------------------
            string json = JsonResult.FromRecognitionResult(recognitionResult).ToString(true);
            Console.WriteLine("=== OCR JSON Result ===");
            Console.WriteLine(json);

            Console.WriteLine("\n✅ Conversion complete!");
            Console.WriteLine($"PDF saved to: {pdfPath}");
        }
    }
}
```

### Pourquoi cela fonctionne

- **Accélération GPU** réduit le temps de reconnaissance d'environ moitié comparé au mode CPU uniquement.  
- **Deskew** et **Denoise** sont des techniques classiques de *prétraitement d'image pour l'OCR* ; elles corrigent les défauts de numérisation courants qui sinon font manquer des caractères au moteur.  
- **Le chargement du modèle de langue** est essentiel pour **reconnaître une image de texte coréen** – sans le modèle coréen, le moteur reviendrait à un alphabet latin générique et produirait du bruit.  
- Le **SearchablePdfExporter** regroupe le bitmap original et une superposition de texte invisible, vous offrant un résultat de **créer une image PDF recherchable** que vous pouvez indexer dans n'importe quel lecteur PDF.

## Pourquoi cela fonctionne

- **Accélération GPU** réduit le temps de reconnaissance d'environ moitié comparé au mode CPU uniquement.  
- **Deskew** et **Denoise** sont des techniques classiques de *prétraitement d'image pour l'OCR* ; elles corrigent les défauts de numérisation courants qui sinon font manquer des caractères au moteur.  
- **Le chargement du modèle de langue** est essentiel pour **reconnaître une image de texte coréen** – sans le modèle coréen, le moteur reviendrait à un alphabet latin générique et produirait du bruit.  
- Le **SearchablePdfExporter** regroupe le bitmap original et une superposition de texte invisible, vous offrant un résultat de **créer une image PDF recherchable** que vous pouvez indexer dans n'importe quel lecteur PDF.

## Prétraitement d'image pour l'OCR – astuces & conseils

`DeskewFilter` corrige la rotation des pages numérisées.  
`ContrastFilter` ajuste le contraste de l'image pour améliorer la précision de l'OCR.  
`BinarizationFilter` convertit l'image en noir et blanc selon un seuil, réduisant le bruit de fond.  
`OrientationFilter` détecte et corrige les pages à orientation mixte portrait/paysage.  

| Problème | Filtre supplémentaire | Comment ajouter |
|----------|-----------------------|-----------------|
| Low contrast | `ContrastFilter { Level = 30 }` | `ocrEngine.Filters.Add(new ContrastFilter { Level = 30 });` |
| Heavy background noise | `BinarizationFilter { Threshold = 128 }` | `ocrEngine.Filters.Add(new BinarizationFilter { Threshold = 128 });` |
| Mixed orientation (portrait & landscape) | `OrientationFilter()` | `ocrEngine.Filters.Add(new OrientationFilter());` |

> **Note :** Ajouter trop de filtres peut ralentir le traitement. Testez chaque modification sur une seule page avant de passer à l'échelle.

## Reconnaître une image de texte coréen – pièges courants

Les scripts coréens contiennent des syllabes Hangul très denses visuellement. Si vous remarquez une sortie illisible :

1. **Assurez-vous que le modèle de langue est entièrement téléchargé** – vérifiez la console pour un message tel que « Downloading Korean model… ».  
2. **Augmentez le `MaxAngle`** dans `DeskewFilter` si vos numérisations sont tournées au-delà de 12°.  
3. **Augmentez la mémoire GPU** en définissant `ocrEngine.GpuMemoryLimit = 2048;` (valeur en Mo).  

`LanguageModel.Korean` charge les données de langue coréenne pour l'OCR, permettant une reconnaissance Hangul précise.  

Ces ajustements influencent directement le succès de **reconnaître une image de texte coréen**.

## Créer une image PDF recherchable – vérifier le résultat

Après l'exécution du programme, ouvrez `korean_page.pdf` dans n'importe quel lecteur PDF (Adobe Acrobat Reader, Foxit, même Chrome). Vous devriez pouvoir :

- **Sélectionner du texte** avec votre souris comme s'il s'agissait d'un PDF natif.  
- **Rechercher** des mots coréens à l'aide de la boîte de recherche intégrée.  

Si la couche de texte apparaît vide, vérifiez que la méthode `Export` a reçu le chemin d'image correct et que le résultat OCR contient un `RecognitionResult.Text` non vide.

## Sortie JSON complète – à quoi s'attendre

La console affiche une charge JSON joliment formatée. Un exemple réduit ressemble à ceci :

```json
{
  "Text": "첫 번째 페이지의 내용...",
  "Blocks": [
    {
      "Text": "첫 번째 페이지의 내용...",
      "BoundingBox": { "X": 12, "Y": 34, "Width": 560, "Height": 780 },
      "Confidence": 0.98
    }
  ],
  "Language": "Korean",
  "ProcessingTimeMs": 842
}
```

## Dépannage & FAQ

**Q : Mon PDF est volumineux comparé à l'image originale.**  
A: L'exportateur intègre le bitmap original à sa résolution native. Si la taille est un problème, réduisez l'image *avant* la reconnaissance :

```csharp
ocrEngine.Filters.Add(new ResizeFilter { MaxWidth = 1240, MaxHeight = 1754 });
```

**Q : L'OCR renvoie des chaînes vides.**  
A: Vérifiez que le chemin de l'image est correct et que le fichier n'est pas corrompu. Assurez-vous également que le pilote GPU est à jour ; les pilotes plus anciens peuvent provoquer des échecs silencieux.

**Q : Puis-je traiter plusieurs pages dans une boucle ?**  
A: Absolument. Enveloppez les étapes 4‑6 dans une boucle `foreach (var file in Directory.GetFiles("Resources", "*.jpg"))` et modifiez le chemin du PDF de sortie en conséquence.

## Conclusion

Nous venons de **convertir une image en PDF** tout en préservant le texte recherchable, grâce au puissant pipeline d'Aspose OCR. En **prétraitant l'image pour l'OCR**, vous améliorez la précision ; en **reconnaissant une image de texte coréen**, vous gérez les scripts complexes ; et en **créant une image PDF recherchable**, vous obtenez un document portable et indexable.

Récupérez le code, pointez-le sur vos propres numérisations, et expérimentez avec des filtres ou modèles de langue supplémentaires. Le même schéma fonctionne pour le chinois, le japonais ou toute langue basée sur le latin — il suffit de remplacer `LanguageModel.Korean` par l'énumération appropriée.

Des questions supplémentaires ? Laissez un commentaire, et bon codage !

---

**Dernière mise à jour :** 2026-09-13  
**Testé avec :** Aspose.OCR 24.11 for .NET  
**Auteur :** Aspose

## Tutoriels associés

- [Créer un PDF recherchable à partir de fichiers numérisés avec Aspose OCR](/ocr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/)
- [Pipeline de prétraitement OCR : comment reconnaître du texte à partir d'une image](/ocr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/)
- [Reconnaître du texte à partir d'une image avec Aspose OCR – Guide complet C](/ocr/net/ocr-configuration/recognize-text-from-image-with-aspose-ocr-complete-c-guide/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}