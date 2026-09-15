---
category: general
date: 2025-12-30
description: Créer un PDF consultable à partir d’une image en C# – apprenez comment
  convertir un TIFF en PDF, extraire le texte d’une image et automatiser la création
  de PDF.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- convert tiff to pdf
- extract text from image
- how to create pdf
language: fr
og_description: Créer un PDF consultable à partir d'une image en utilisant Aspose
  OCR en C#. Ce guide montre comment convertir un TIFF en PDF, extraire le texte et
  garantir la conformité PDF/A‑1b.
og_title: Créer un PDF interrogeable à partir d'un TIFF – Tutoriel C# étape par étape
tags:
- Aspose OCR
- C#
- PDF generation
title: Créer un PDF consultable à partir de TIFF – Guide complet C#
url: /fr/net/text-recognition/create-searchable-pdf-from-tiff-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF recherchable à partir d'un TIFF – Guide complet C#

Vous avez déjà eu besoin de **créer un PDF recherchable** à partir d'un TIFF numérisé mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul. De nombreux développeurs rencontrent cet obstacle lorsqu'ils ont besoin de PDF recherchables pour l'archivage ou la conformité, et la bonne nouvelle est que la solution est étonnamment simple avec Aspose OCR.

Dans ce tutoriel, nous allons parcourir la conversion d’une image en PDF, l’extraction de texte depuis l’image, et le polissage du résultat afin qu’il respecte les normes PDF/A‑1b. À la fin, vous serez capable de **convertir tiff en pdf**, **extraire du texte depuis une image**, et de savoir exactement **comment créer des pdf** qui sont à la fois recherchables et prêts pour l’archivage.

## Ce dont vous avez besoin

- .NET 6 (ou toute version récente de .NET) – le code fonctionne aussi bien sur .NET Core que sur .NET Framework.  
- Package NuGet Aspose.OCR – installez-le avec `dotnet add package Aspose.OCR`.  
- Un fichier TIFF d'exemple (`input.tif`) que vous souhaitez transformer en PDF recherchable.  
- Un environnement de développement (Visual Studio, VS Code, Rider… n'importe lequel fera l'affaire).  

C’est tout. Aucun SDK supplémentaire, aucun service externe, et aucune étape de configuration cachée.

![Exemple de PDF recherchable](image-placeholder.png "Aperçu du PDF recherchable")

## Étape 1 – Initialiser le moteur OCR et charger le modèle anglais

Avant de pouvoir transformer une image en texte recherchable, le moteur OCR doit savoir quelle langue rechercher. Aspose OCR est fourni avec des packs de langues que vous pouvez charger à la demande.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the English language model (you can swap this for other languages)
ocrEngine.LoadLanguage(LanguageModel.English);
```

**Pourquoi c’est important :** Charger le modèle linguistique correct améliore considérablement la précision de reconnaissance. Si vous sautez cette étape, le moteur revient à un modèle générique, ce qui produit souvent du texte illisible—surtout sur les TIFF à basse résolution.

## Étape 2 – Reconnaître le texte de l'image source (Optionnel mais pratique)

L’exécution de l’OCR vous fournit un objet `OcrResult` que vous pouvez inspecter, journaliser ou même enregistrer en texte brut. Cette étape est optionnelle si vous ne vous souciez que du PDF final, mais elle est très utile pour le débogage.

```csharp
// Perform OCR on the input TIFF
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/input.tif");

// Dump the raw text to the console (useful for validation)
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

**Astuce pro :** Si le texte extrait semble incorrect, envisagez de pré‑traiter l’image (redressement, débruitage) avant de la transmettre au moteur. Aspose OCR propose également des utilitaires d’amélioration d’image que vous pouvez chaîner ici.

## Étape 3 – Configurer l'exportateur PDF recherchable

Nous indiquons maintenant à Aspose comment nous voulons que le PDF final apparaisse. Le `SearchablePdfExporter` vous permet de spécifier le chemin de sortie, la conformité PDF/A, et quelques autres options pratiques.

```csharp
var pdfExporter = new SearchablePdfExporter
{
    // Where the searchable PDF will be saved
    OutputPath = "YOUR_DIRECTORY/output.pdf",

    // Enforce PDF/A‑1b compliance – ideal for long‑term archiving
    PdfACompliance = PdfACompliance.PdfA1b
};
```

**Pourquoi PDF/A‑1b ?** De nombreux secteurs (juridique, médical, financier) exigent des PDF conformes aux normes d’archivage. Définir `PdfACompliance` garantit que les polices sont incorporées, que les couleurs sont indépendantes du dispositif, et que le fichier passe les outils de validation.

## Étape 4 – Exporter le résultat OCR directement vers un PDF recherchable

Avec le moteur et l’exportateur prêts, le travail lourd se résume à une seule ligne. L’exportateur construit en interne une page PDF, superpose le texte reconnu comme une couche invisible, et écrit le fichier.

```csharp
// Export the OCR result to a searchable PDF
pdfExporter.Export(ocrEngine, "YOUR_DIRECTORY/input.tif");

// Confirmation message
Console.WriteLine("Searchable PDF created at YOUR_DIRECTORY/output.pdf");
```

**Que se passe-t-il en coulisses ?**  
1. Le TIFF original est intégré en tant qu'image raster.  
2. Le texte dérivé de l'OCR est placé au-dessus, invisible mais sélectionnable.  
3. Des métadonnées (comme la langue) sont ajoutées afin que les lecteurs PDF puissent indexer le texte.

## Étape 5 – Vérifier la sortie (vérification manuelle + validation programmatique)

Il est toujours bon de confirmer que le PDF est réellement recherchable.

```csharp
// Quick sanity check: open the PDF and try to extract its text
using var pdfReader = new Aspose.Pdf.Facades.PdfConverter();
pdfReader.BindPdf("YOUR_DIRECTORY/output.pdf");
var extracted = pdfReader.ExtractText();
Console.WriteLine("Text extracted from the PDF:");
Console.WriteLine(extracted);
```

Si vous pouvez copier‑coller le texte depuis le visualiseur PDF ou le voir dans la sortie console ci‑dessus, vous avez réussi.

## Cas limites et variations courantes

### Conversion d'autres formats d'image

Le même code fonctionne pour PNG, JPEG, BMP—il suffit de changer l'extension du fichier dans les appels `Recognize` et `Export`. Aucune configuration supplémentaire n'est nécessaire.

### Fichiers TIFF multi‑pages

Aspose OCR traite automatiquement chaque page d’un TIFF multi‑pages et l’exportateur les empile dans un PDF multi‑pages. Si vous devez ignorer une page, filtrez `ocrResult.Pages` avant l’exportation.

### Langues non‑anglais

Remplacez `LanguageModel.English` par `LanguageModel.Spanish`, `LanguageModel.French`, etc., ou chargez un pack de langue personnalisé. N'oubliez pas d’ajuster les métadonnées PDF si vous ciblez une locale spécifique.

### Réduction de la taille du PDF

Si les TIFF sont haute résolution, le PDF résultant peut être volumineux. Vous pouvez réduire l’échantillonnage de l’image avant l’OCR :

```csharp
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Dpi = 150 // Lower DPI reduces size, but test for acceptable quality
};
```

### Gestion des PDF protégés par mot de passe

Si vous devez protéger la sortie, encapsulez le `SearchablePdfExporter` dans l’API de chiffrement d’Aspose.Pdf après l’exportation :

```csharp
var pdfDoc = new Aspose.Pdf.Document("YOUR_DIRECTORY/output.pdf");
pdfDoc.Encrypt("userPassword", "ownerPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save("YOUR_DIRECTORY/output_protected.pdf");
```

## Exemple complet fonctionnel

Voici le programme complet, prêt à copier‑coller, qui intègre toutes les étapes et les ajustements optionnels abordés ci‑dessus.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Initialize OCR engine and load language model
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // Optional: lower DPI to shrink output size (adjust as needed)
        // ocrEngine.ImageProcessingOptions = new ImageProcessingOptions { Dpi = 150 };

        // -----------------------------------------------------------------
        // 2️⃣ Recognize text from the source TIFF
        // -----------------------------------------------------------------
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        var ocrResult = ocrEngine.Recognize(inputPath);
        Console.WriteLine("Extracted text from image:");
        Console.WriteLine(ocrResult.Text);

        // -----------------------------------------------------------------
        // 3️⃣ Configure the searchable PDF exporter
        // -----------------------------------------------------------------
        var pdfExporter = new SearchablePdfExporter
        {
            OutputPath = @"YOUR_DIRECTORY/output.pdf",
            PdfACompliance = PdfACompliance.PdfA1b // archival compliance
        };

        // -----------------------------------------------------------------
        // 4️⃣ Export OCR result to searchable PDF
        // -----------------------------------------------------------------
        pdfExporter.Export(ocrEngine, inputPath);
        Console.WriteLine("Searchable PDF created successfully.");

        // -----------------------------------------------------------------
        // 5️⃣ Verify by extracting text from the generated PDF
        // -----------------------------------------------------------------
        using var converter = new PdfConverter();
        converter.BindPdf(@"YOUR_DIRECTORY/output.pdf");
        var extractedFromPdf = converter.ExtractText();
        Console.WriteLine("Text extracted from the PDF:");
        Console.WriteLine(extractedFromPdf);
    }
}
```

**Sortie attendue :**  
- La console affiche le texte OCR brut du TIFF.  
- Un fichier `output.pdf` apparaît dans `YOUR_DIRECTORY`.  
- L'ouverture de `output.pdf` dans Adobe Reader vous permet de sélectionner et copier le texte, confirmant qu'il est recherchable.

## Récapitulatif

Nous avons couvert tout ce dont vous avez besoin pour **créer des PDF recherchables** à partir d’images TIFF en utilisant Aspose OCR en C#. De l’initialisation du moteur OCR, l’extraction du texte, la configuration de la conformité PDF/A, à la vérification du document final, chaque étape est clairement expliquée. Vous savez maintenant comment **convertir image en pdf**, **convertir tiff en pdf**, **extraire du texte depuis une image**, et la question plus large de **comment créer des pdf** avec des couches recherchables.

## Que explorer ensuite

- **Traitement par lots :** Enveloppez la logique dans une boucle pour gérer des dizaines d'images automatiquement.  
- **Polices personnalisées :** Intégrez les polices d'entreprise pour une cohérence de la marque.  
- **Intégration cloud :** Stockez les PDF directement dans Azure Blob Storage ou AWS S3 après création.  
- **Interface utilisateur :** Créez une application WinForms/WPF simple qui permet aux utilisateurs de glisser‑déposer des images pour une conversion instantanée.  

N’hésitez pas à expérimenter avec différents modèles linguistiques, réglages DPI et niveaux PDF/A. L’API est suffisamment flexible pour s’adapter à presque n’importe quel flux de travail que vous pouvez imaginer.

*Bonne programmation, et que vos PDF soient toujours recherchables !*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}