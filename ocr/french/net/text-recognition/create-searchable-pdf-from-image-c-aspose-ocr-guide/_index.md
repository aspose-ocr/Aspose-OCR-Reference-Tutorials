---
category: general
date: 2026-05-06
description: Créer un PDF consultable à partir d’une image avec Aspose OCR en C#.
  Apprenez à convertir un PNG en PDF, extraire le texte d’une image et générer un
  PDF consultable.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: fr
og_description: Créer un PDF consultable à partir d’une image en utilisant Aspose
  OCR en C#. Ce tutoriel étape par étape montre comment convertir un PNG en PDF, extraire
  le texte de l’image et produire un PDF consultable.
og_title: Créer un PDF consultable à partir d’une image – Guide OCR Aspose en C#
tags:
- Aspose
- C#
- OCR
- PDF
title: Créer un PDF recherchable à partir d’une image – Guide OCR Aspose C#
url: /fr/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir d'une image – Guide C# Aspose OCR

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d'une image numérisée mais vous ne saviez pas par où commencer ? Peut-être avez‑vous un reçu au format PNG, un JPEG d'un contrat, ou tout autre bitmap que vous souhaitez transformer en PDF réellement interrogeable. C’est un problème fréquent, surtout lorsque vous avez des scans anciens qui restent inutilisés dans un dossier.

La bonne nouvelle, c’est qu’avec Aspose OCR vous pouvez **convertir une image en PDF**, extraire le texte caché, et obtenir un document entièrement consultable — le tout en quelques lignes de C#. Dans ce guide, nous vous montrerons également comment **convertir png en PDF**, **extraire du texte d’une image**, et même comment gérer le cas particulier des TIFF multi‑pages. À la fin, vous disposerez d’une solution autonome que vous pourrez intégrer à n’importe quel projet .NET.

## Ce dont vous avez besoin

- **.NET 6+** (le code fonctionne également avec .NET Framework 4.6+)
- **Visual Studio 2022** ou tout IDE de votre choix
- **Aspose.OCR** package NuGet (il ajoute automatiquement Aspose.PDF)
- Un fichier image (PNG, JPEG, BMP, TIFF) que vous souhaitez transformer en PDF consultable

Pas de tours de licence supplémentaires, pas de services externes — juste une référence NuGet unique et quelques minutes de codage.

## Étape 1 : Installer le package NuGet Aspose.OCR

Tout d’abord, ajoutez la bibliothèque à votre projet. Ouvrez la console du Gestionnaire de packages et exécutez :

```powershell
Install-Package Aspose.OCR
```

Cette unique commande récupère à la fois **Aspose.OCR** et l’assembly **Aspose.Pdf** dont il dépend, vous permettant ainsi de lire l’image et d’écrire le PDF.

> **Astuce :** Si vous utilisez le .NET CLI, l’équivalent est `dotnet add package Aspose.OCR`.

## Étape 2 : Initialiser le moteur OCR

Créer une instance de `OcrEngine` est la porte d’entrée de tout le travail OCR. Considérez‑le comme le cerveau qui examinera votre image et commencera à « lire » les caractères.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

Vous vous demandez peut‑être, *pourquoi ne pas simplement appeler une méthode statique ?* L’approche orientée‑objet vous permet d’ajuster les paramètres plus tard (langue, résolution, etc.) sans modifier le flux global.

## Étape 3 : Charger l’image que vous souhaitez convertir

C’est ici que nous **convertissons une image en PDF** en pratique — en injectant le bitmap dans le moteur OCR. Remplacez `"YOUR_DIRECTORY/input.png"` par le chemin réel de votre fichier.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

Si vous avez un scénario de **convertir png en pdf**, pointez simplement vers le PNG. Pour les TIFF multi‑pages, Aspose.OCR traitera automatiquement chaque trame comme une page distincte.

## Étape 4 : Exécuter l’OCR et éventuellement récupérer le texte

L’appel à `Recognize()` effectue le travail lourd : il analyse l’image, détecte les caractères et renvoie un résultat structuré. Vous pouvez conserver le texte pour la journalisation, l’indexation de recherche ou l’affichage.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Pourquoi extraire le texte ?** Même si nous l’intégrerons dans le PDF final, disposer de la chaîne brute peut être utile pour la validation ou l’analyse.

## Étape 5 : Configurer les options PDF pour un document consultable

Aspose.PDF nous propose un mode spécial `PdfSaveOptions` appelé **CreateSearchablePdf**. Il indique à la bibliothèque d’intégrer le texte OCR comme une couche invisible derrière l’image, rendant le PDF consultable.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

Si vous avez besoin d’un PDF simple contenant uniquement l’image (sans texte caché), vous pouvez passer à `PdfSaveOptions.CreatePdf()`. Mais pour notre objectif—**créer un PDF consultable**—le mode consultable est la vedette.

## Étape 6 : Enregistrer le PDF consultable sur le disque

Nous rassemblons maintenant le tout. La méthode `SavePdf` écrit l’image et le texte caché dans un seul fichier.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

À ce stade, vous disposez d’un **PDF consultable** que vous pouvez ouvrir dans Adobe Reader, taper un mot dans la zone de recherche et sauter instantanément à l’emplacement correspondant — même si la page visible reste simplement l’image originale.

## Exemple complet fonctionnel

En assemblant tous les éléments, voici une application console prête à l’emploi. Copiez‑collez‑la dans un nouveau projet C#, ajustez les chemins de fichiers, et appuyez sur **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### Sortie attendue

Lorsque vous exécutez le programme, la console affichera quelque chose comme :

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

Et dans `YOUR_DIRECTORY` vous trouverez `output.pdf`. Ouvrez‑le, appuyez sur **Ctrl F**, tapez « Invoice », et vous serez directement amené au mot — même si la page ressemble à un scan plat.

## Gestion des variations courantes

### Convertir plusieurs images en une fois

Si vous avez un dossier rempli de PNG et que vous souhaitez un PDF consultable unique, parcourez les fichiers et ajoutez chacun comme une page distincte :

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

Vous pouvez également utiliser `PdfFileEditor` d’Aspose.PDF pour fusionner les PDF temporaires en un fichier final.

### Gérer les scans à basse résolution

La précision de l’OCR diminue lorsque le DPI de l’image est inférieur à 150. Avant d’alimenter l’image, vous pouvez l’agrandir :

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### Sélectionner une langue spécifique

Si votre document n’est pas en anglais, définissez la langue avant `Recognize()` :

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Ces ajustements garantissent que **extraire du texte d’une image** fonctionne de manière fiable dans différents scénarios.

## Résultat visuel

![Searchable PDF created with Aspose OCR – create searchable PDF](https://example.com/images/searchable-pdf.png)

*La capture d’écran ci‑dessus montre un PDF où l’image est visible, mais la couche de texte peut être recherchée.*

## Conclusion

Vous disposez maintenant d’une recette complète, prête pour la production, pour **créer des PDF consultables** à partir de n’importe quelle image en utilisant Aspose OCR et C#. Nous avons vu comment **convertir une image en PDF**, **extraire du texte d’une image**, et même abordé les cas particuliers de **convertir png en pdf** et **ocr image to pdf**. Le code est entièrement autonome, fonctionne sur n’importe quel runtime .NET, et peut être étendu au traitement par lots ou à la prise en charge de langues personnalisées.

Et après ? Essayez d’ajouter un filigrane, de chiffrer le PDF, ou d’alimenter le texte extrait dans un index de recherche comme Elasticsearch. Les possibilités sont infinies, et le même schéma — charger → reconnaître → enregistrer — vous servira pour tout flux de travail basé sur l’OCR.

Si vous rencontrez des problèmes ou avez un cas d’utilisation intéressant à partager, laissez un commentaire ci‑dessous. Bon codage, et profitez de transformer ces scans récalcitrants en or consultable !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}