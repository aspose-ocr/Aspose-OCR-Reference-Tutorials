---
category: general
date: 2026-03-23
description: Créez un PDF consultable à partir d’une image avec Aspose OCR. Apprenez
  comment convertir un TIFF en PDF avec une forte compression et reconnaître le texte
  de l’image en quelques minutes.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: fr
og_description: Créer un PDF consultable à partir d'une image avec Aspose OCR. Ce
  tutoriel montre comment convertir un TIFF en PDF, ajouter une couche de texte consultable
  et appliquer une compression élevée.
og_title: Créer un PDF consultable à partir d'une image – Guide complet C#
tags:
- Aspose OCR
- C#
- PDF generation
title: Créer un PDF recherchable à partir d'une image – Guide complet C#
url: /fr/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir d'une image – Guide complet C#  

Ever needed to **create searchable pdf** from a scanned document but weren't sure where to start? You're not the only one—many developers hit the same wall when turning TIFF scans into searchable PDFs. The good news? With Aspose OCR you can **convert tiff to pdf**, slap a hidden text layer on top, and even squeeze the file size with **high compression pdf** options, all in a handful of lines of C#.

Dans ce tutoriel, nous parcourrons l'ensemble du processus : de l'installation des bons packages NuGet, au chargement d'une image TIFF, à la reconnaissance de son texte, et enfin à l'exportation d'un PDF consultable. À la fin, vous disposerez d'une application console exécutable qui **recognize image text** et produit un PDF compact et consultable prêt pour l'indexation. Aucun outil supplémentaire, aucune étape OCR manuelle — juste du code propre et quelques explications.

## Prérequis et ce dont vous aurez besoin

- **.NET 6+** (ou .NET Framework 4.6+). L'API fonctionne sur les deux, mais .NET 6 vous offre les dernières améliorations du runtime.  
- **Visual Studio 2022** ou tout IDE de votre choix.  
- Packages NuGet **Aspose.OCR** et **Aspose.OCR.Gpu** (le package GPU est optionnel mais accélère la reconnaissance sur le matériel supporté).  
- Un fichier TIFF d'exemple (par ex. `invoice.tif`) placé dans un dossier que vous contrôlez.  

Si vous avez déjà ces éléments, super — passez à la suite. Sinon, l'étape d'installation ci‑dessous couvrira tout.

## Étape 1 : Installer les packages Aspose OCR

Pour commencer, ouvrez le dossier de votre projet dans un terminal et exécutez :

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Ces commandes récupèrent à la fois le moteur OCR de base et la bibliothèque d'accélération GPU. Cette dernière n'est pas obligatoire ; le moteur reviendra en mode CPU s'il ne trouve pas de GPU compatible.  

> **Pro tip :** Lors du ciblage d'un environnement de production, verrouillez les versions des packages dans votre `csproj` afin d'éviter des changements incompatibles inattendus.

## Étape 2 : Configurer la structure du projet

Créez une nouvelle application console (si vous n'en avez pas déjà une) :

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Remplacez le `Program.cs` généré automatiquement par le code complet affiché plus tard. Le programme :

1. Initialise un `OcrEngine` avec le support GPU.  
2. Charge l'image TIFF.  
3. Exécute l'OCR et interrompt proprement en cas d'échec.  
4. Configure **PdfExportOptions** pour une couche consultable et **high compression**.  
5. Écrit le fichier de sortie.

## Étape 3 : Écrire le code complet (exemple complet)

Voici le fichier source *entier*. Copiez‑collez‑le dans `Program.cs`. Les commentaires expliquent le « pourquoi » derrière chaque ligne, pas seulement le « quoi ».

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Pourquoi cela fonctionne

- **GPU acceleration** peut réduire le temps de reconnaissance de secondes à millisecondes sur les cartes modernes — pratique pour le traitement en masse.  
- **IncludeTextLayer** intègre le texte dérivé de l'OCR de façon invisible, permettant aux lecteurs PDF de rechercher dans le document sans modifier son apparence visuelle.  
- **High compression** utilise la compression Flate (ZIP) sur le flux d'image, ce qui est sans perte mais réduit la taille du fichier de façon spectaculaire — idéal pour l'archivage de milliers de factures.

## Étape 4 : Exécuter l'application et vérifier la sortie

Ouvrez un terminal dans le dossier du projet et exécutez :

```bash
dotnet run
```

Si tout est correctement configuré, vous verrez :

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

Ouvrez `invoice.pdf` dans n'importe quel lecteur PDF (Adobe Acrobat, Edge ou même un navigateur). Essayez de rechercher un mot que vous savez présent dans le TIFF original — par ex., « Total ». Le lecteur devrait mettre en surbrillance le mot même s'il fait partie de l'image. C’est la marque d'un **searchable pdf**.

### Taille de fichier attendue

Une facture numérisée typique (≈300 KB TIFF) se réduit souvent à **~80 KB** après l'application de `PdfCompression.High`. La taille exacte dépend de la complexité de l'image, mais vous constaterez une réduction nette.

## Étape 5 : Variations courantes et cas limites

| Situation | Ce qu'il faut ajuster | Pourquoi |
|-----------|-----------------------|----------|
| **No GPU available** | Change `new OcrEngine(GpuMode.Enabled)` to `new OcrEngine(GpuMode.Disabled)` | Empêche le moteur de tenter l'initialisation du GPU, ce qui peut entraîner un léger délai. |
| **Multiple pages (multi‑page TIFF)** | Set `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` | Charge toutes les trames ; Aspose traitera chaque page et générera un PDF multi‑pages. |
| **Need OCR language other than English** | `ocrEngine.Language = Language.French;` (or any supported language) | Améliore la précision pour les documents non‑anglais. |
| **Want a visible text overlay instead of hidden layer** | `pdfExportOptions.IncludeTextLayer = false;` and manually add `TextFragment` objects. | Utile lorsque vous souhaitez que le texte OCR apparaisse comme texte sélectionnable au-dessus de l'image. |
| **Ultra‑small PDFs** | Combine `PdfCompression.High` with `ImageResolution = 150` DPI before recognition. | Une résolution DPI plus basse réduit les données d'image, diminuant davantage le PDF au prix d'une fidélité visuelle réduite. |

> **Note :** Testez toujours les cas limites sur un petit échantillon avant de passer à la production. La précision de l'OCR peut varier selon la qualité de l'image, le bruit et la langue.

## Étape 6 : Conseils pour des implémentations prêtes pour la production

1. **Error Logging** – Remplacez `Console.WriteLine` par un framework de journalisation approprié (Serilog, NLog) pour des diagnostics plus simples.  
2. **Batch Processing** – Encapsulez la logique principale dans une méthode qui accepte les chemins d'entrée/sortie, puis parcourez un répertoire de fichiers TIFF.  
3. **Async I/O** – Bien qu'Aspose OCR soit synchrone, le chargement et l'enregistrement des fichiers peuvent être asynchrones pour garder les threads UI réactifs.  
4. **Security** – Si vous exposez cette fonctionnalité via une API web, validez les chemins de fichiers et limitez la taille des fichiers pour éviter les abus.  
5. **Version Pinning** – Utilisez des numéros de version exacts (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`) pour garantir un comportement cohérent entre les builds.

## Conclusion

Nous venons de créer une **solution complète, de bout en bout** qui **create searchable pdf** à partir d'images numérisées, **convert tiff to pdf**, et le fait avec les paramètres **high compression pdf** tout en **recognize image text** avec précision. Le **searchable pdf from image** résultant est léger, consultable et prêt pour les flux de travail en aval tels que l'indexation, l'archivage ou l'e‑discovery.

Vous avez un lot de factures ? Intégrez la méthode dans une boucle, pointez‑la vers un dossier, et laissez Aspose OCR faire le gros du travail. Vous voulez expérimenter différents niveaux de compression ou packs de langues ? Le code est suffisamment modulaire pour échanger ces options en quelques secondes.

---

*Prêt à passer au niveau supérieur ?* Essayez d'ajouter un filigrane, d'intégrer des métadonnées, ou même d'assembler plusieurs PDF traités par OCR. La suite Aspose propose de nombreuses extensions — explorez la documentation et maintenez l'élan. Bon codage !

![Capture d'écran d'exemple de création de PDF consultable à partir d'une image](https://example.com/images/create-searchable-pdf.png "exemple de création de PDF consultable")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}