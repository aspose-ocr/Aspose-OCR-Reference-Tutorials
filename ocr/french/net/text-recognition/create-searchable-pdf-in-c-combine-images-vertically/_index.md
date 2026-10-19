---
category: general
date: 2026-02-28
description: Créer un PDF consultable en C# en combinant des images verticalement.
  Apprenez à empiler les images verticalement et à convertir des pages PDF numérisées
  avec Aspose OCR.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: fr
og_description: Créer un PDF recherchable en C# en combinant des images verticalement.
  Ce guide montre comment empiler les images verticalement et convertir des pages
  numérisées en PDF à l'aide d'Aspose OCR.
og_title: Créer un PDF recherchable en C# – Combiner les images verticalement
tags:
- Aspose OCR
- C#
- PDF generation
title: Créer un PDF interrogeable en C# – Combiner les images verticalement
url: /fr/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF interrogeable en C# – Combiner les images verticalement

Vous avez déjà eu besoin de **créer un PDF interrogeable** à partir d’une poignée de PNG numérisés mais vous ne saviez pas par où commencer ? Vous n’êtes pas seul. Dans de nombreux projets d’automatisation de documents, le principal problème est de transformer une pile de fichiers image en un PDF propre et interrogeable que vous pouvez indexer et partager.  

Dans ce tutoriel, nous parcourrons un exemple complet, prêt à l’exécution, qui vous montre **comment empiler les images verticalement**, **combiner les images verticalement**, et enfin **convertir les pages scannées en PDF** en un seul document interrogeable grâce au moteur accéléré par GPU d’Aspose.OCR. À la fin, vous disposerez d’un programme autonome que vous pourrez intégrer à n’importe quelle solution .NET.

> **Ce que vous allez apprendre**
> - Initialiser un moteur OCR avec prise en charge GPU.
> - Traiter un lot d’images en parallèle.
> - **Combiner les images verticalement** pour reproduire un scan multi‑pages.
> - Exporter un PDF interrogeable et un rapport JSON détaillé pour les analyses en aval.

## Prérequis

- .NET 6+ (le code se compile avec .NET 6, .NET 7 ou .NET 8)
- Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Une machine avec GPU si vous souhaitez conserver le paramètre `ProcessingMode.Gpu` (le fallback CPU fonctionne également)
- Un dossier contenant quelques fichiers PNG/JPEG numérisés (la démo utilise `page1.png`, `page2.png`, `page3.png`)

Aucun service externe, aucun fichier de configuration caché — juste du pur C#.

## Étape 1 – Configurer le moteur OCR pour **Créer un PDF interrogeable**

Tout d’abord, nous créons un `OcrEngine`, activons l’accélération GPU, sélectionnons l’anglais comme langue, et ajoutons quelques filtres de prétraitement. Ces filtres améliorent la précision en redressant les pages inclinées (`DeskewFilter`) et en supprimant le bruit (`DenoiseFilter`).

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Pourquoi c’est important :** Le moteur OCR effectue le travail lourd de reconnaissance du texte. Activer `ProcessingMode.Gpu` peut réduire le temps de reconnaissance de moitié sur une carte graphique moderne, tandis que les filtres réduisent les artefacts de numérisation courants qui produiraient autrement un résultat illisible.

## Étape 2 – Configurer un processeur de lot pour **Convertir les pages scannées en PDF** efficacement

Traiter chaque page une par une suffit pour quelques images, mais les projets réels impliquent souvent des dizaines ou des centaines de pages. `OcrBatchProcessor` d’Aspose.OCR nous permet d’exécuter les reconnaissances en parallèle, accélérant considérablement l’étape **convertir les pages scannées pdf**.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Astuce :** Si vous êtes sur une machine sans GPU, définissez `ProcessingMode = ProcessingMode.Cpu`. Le processeur de lot respectera toujours `MaxDegreeOfParallelism`, vous permettant de l’ajuster pour ne pas surcharger la machine.

## Étape 3 – Exécuter l’OCR sur le lot et rassembler les résultats

Nous reconnaissons maintenant le texte. La méthode `Recognize` renvoie une liste d’objets `OcrResult`, chacun contenant à la fois l’image originale et le texte extrait.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

À ce stade, vous avez tout ce qu’il faut pour **créer un PDF interrogeable** : les images (toujours en mémoire) et les couches de texte associées.

## Étape 4 – **Combiner les images verticalement** et générer le PDF interrogeable

La plupart des documents scannés sont des PDF multi‑pages, il faut donc assembler les images de chaque page en une seule image haute qui reproduit une pile physique. Aspose.OCR fournit `Image.CombineVertical` exactement pour cela.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Le fichier résultant (`combined_searchable.pdf`) contient du texte sélectionnable et interrogeable sous chaque image de page — exactement ce dont vous avez besoin pour **créer un PDF interrogeable** à partir de sources scannées.

![Exemple de création de PDF interrogeable](/images/create-searchable-pdf.png "exemple de création de PDF interrogeable")

*Texte alternatif de l’image : exemple de création de PDF interrogeable montrant un PDF combiné avec du texte interrogeable.*

**Pourquoi empiler verticalement ?** De nombreuses bibliothèques OCR traitent chaque image comme une page distincte. En les empilant, nous conservons l’ordre des pages du PDF tout en profitant d’une passe OCR unique pour l’ensemble du document.

## Étape 5 – Exporter le JSON détaillé pour la première page (Idéal pour les flux de travail en aval)

Parfois, vous avez besoin de plus qu’un PDF ; vous souhaitez peut‑être injecter les données OCR dans une base de données ou un pipeline de machine‑learning. Aspose.OCR vous permet de sérialiser chaque `OcrResult` en JSON, en conservant les boîtes englobantes, les scores de confiance, etc.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Extrait JSON attendu (truncaté) :**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Vous pouvez maintenant injecter ce JSON dans n’importe quel système en aval—que vous indexiez le texte dans Elasticsearch ou que vous le transmettiez à un tableau de bord analytique personnalisé.

---

## Comment **Empiler les images verticalement** – Récapitulatif rapide

Si vous vous demandez **comment empiler les images verticalement** sans Aspose, vous pourriez utiliser `System.Drawing` pour créer un nouveau bitmap et dessiner chaque page l’une après l’autre. Cependant, `Image.CombineVertical` intégré à Aspose gère le DPI, le format des pixels et la gestion de la mémoire pour vous, ce qui en fait le choix le plus fiable pour du code de production.

### Alternative : Utiliser `System.Drawing` (juste par curiosité)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

L’approche manuelle fonctionne, mais vous perdez la commodité de la gestion automatique du DPI et la capacité d’alimenter directement le résultat dans `RecognizeToPdf`. Restez avec `CombineVertical` sauf si vous avez un besoin très spécifique.

## Pièges courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Erreurs de mémoire insuffisante** lors du traitement de dizaines de scans haute résolution | Chaque image reste en mémoire jusqu’à l’écriture du PDF | Libérez les objets `Image` dès que possible (`using` blocks) ou réduisez la résolution avant de les combiner |
| **Texte illisible** après OCR | Scans inclinés ou faible contraste | Conservez les filtres `DeskewFilter` et `DenoiseFilter` ; ajoutez éventuellement `ContrastFilter` |
| **Absence de couche interrogeable** | Utilisation de `Recognize` au lieu de `RecognizeToPdf` | Assurez‑vous d’appeler `ocrEngine.RecognizeToPdf` sur l’image combinée |
| **Échec du fallback GPU** sur des machines sans pilotes adéquats | `ProcessingMode.Gpu` lève une exception | Encapsulez la création du moteur dans un try/catch et revenez à `ProcessingMode.Cpu` |

## Prochaines étapes – Étendre le flux de travail

Maintenant que vous savez **créer un PDF interrogeable**, vous pourriez :

- **Traiter en lot des dossiers entiers** avec `Directory.GetFiles` et une boucle `foreach`.
- **Ajouter des filigranes** à chaque page avant la combinaison (utilisez `ImageProcessor` d’Aspose.Imaging).
- **Scinder le PDF interrogeable en pages individuelles** si vous avez besoin de PDF par page plus tard (`PdfDocument.Split` d’Aspose.PDF).
- **Intégrer avec Azure Blob Storage** pour récupérer les images depuis le cloud et pousser le PDF final.

Toutes ces extensions reposent naturellement sur les mêmes concepts de base : configuration OCR, gestion des images et export PDF.

---

## Conclusion

Nous avons couvert tout ce qu’il faut pour **créer un PDF interrogeable** à partir d’une collection d’images scannées en C#. En initialisant un `OcrEngine` compatible GPU, en exécutant un lot parallèle avec `OcrBatchProcessor`, en **combinant les images verticalement**, puis en appelant `RecognizeToPdf`, vous obtenez un document propre et interrogeable, prêt à être archivé ou indexé. L’export JSON supplémentaire vous donne une visibilité complète sur les résultats OCR, ouvrant la porte à l’analyse ou à des flux de travail personnalisés.

Essayez, expérimentez avec différents filtres, et voyez votre pipeline d’automatisation documentaire devenir beaucoup plus fluide. Si vous rencontrez des difficultés, laissez un commentaire—bon codage !

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}