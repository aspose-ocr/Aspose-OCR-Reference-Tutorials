---
category: general
date: 2026-03-13
description: Créez un PDF interrogeable à partir de n'importe quelle image en utilisant
  Aspose OCR. Apprenez comment convertir une image en EPUB, ajouter du texte interrogeable
  et générer un PDF interrogeable en C#.
draft: false
keywords:
- create searchable pdf
- convert image to epub
- ocr image to pdf
- add searchable text
- generate searchable pdf
language: fr
og_description: Créez un PDF consultable à partir de n'importe quelle image avec Aspose
  OCR. Ce guide montre comment convertir une image en EPUB, ajouter du texte consultable
  et générer un PDF consultable en C#.
og_title: Créer un PDF recherchable – Convertir l'image en EPUB et ajouter du texte
tags:
- Aspose OCR
- C#
- PDF
- EPUB
title: Créer un PDF interrogeable – Convertir l’image en EPUB et ajouter du texte
url: /fr/net/text-recognition/create-searchable-pdf-convert-image-to-epub-add-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF interrogeable – Convertir une image en EPUB et ajouter du texte

Vous souhaitez **créer un PDF interrogeable** à partir d'un reçu numérisé ou de toute image ? Dans ce tutoriel, nous vous montrerons comment créer un PDF interrogeable en utilisant Aspose OCR tout en **convertissant l'image en EPUB** et **en ajoutant des calques de texte interrogeable** — le tout dans un seul projet C#.

Si vous avez déjà eu du mal avec des PDF qui ont l'air bien mais qui ne peuvent pas être recherchés, vous n'êtes pas seul. La bonne nouvelle, c'est qu'un calque de texte caché peut transformer une image plate en un document entièrement interrogeable, et Aspose rend cela presque sans effort.

## Ce que vous apprendrez

* Comment initialiser le moteur Aspose OCR et définir la langue.  
* Les étapes exactes pour **convertir une image en EPUB** pour la distribution d'e‑books.  
* Comment configurer le générateur PDF afin que la sortie contienne un calque de texte caché et interrogeable.  
* Conseils pour gérer les cas particuliers tels que les reçus multi‑pages ou les langues non anglaises.  

Tout ce dont vous avez besoin au préalable est un environnement de développement .NET (Visual Studio 2022 ou ultérieur) et le package NuGet Aspose OCR. Aucun service externe, aucun fichier de configuration obscur — juste du C# pur que vous pouvez copier‑coller et exécuter.

## Prérequis

| Exigence | Pourquoi c’est important |
|----------|--------------------------|
| .NET 6.0+   | Aspose OCR cible .NET Standard 2.0+, donc .NET 6 vous offre les dernières améliorations du runtime. |
| Aspose.OCR NuGet package | Fournit les classes `OcrEngine`, `EpubWriter` et `PdfWriter` utilisées dans le code. |
| An image file (e.g., `receipt.jpg`) | Le fichier source sur lequel vous exécuterez l'OCR. Toute image raster (PNG, JPEG, BMP) fonctionne. |
| Basic C# knowledge | Vous lirez et ajusterez des extraits, sans avoir à apprendre le langage depuis le début. |

Vous pouvez installer le package avec la commande suivante :

```bash
dotnet add package Aspose.OCR
```

> **Astuce :** Si vous utilisez Visual Studio, l'interface du Gestionnaire de packages NuGet fait le même travail — il suffit de rechercher « Aspose.OCR ».

## Étape 1 – Créer un PDF interrogeable avec Aspose OCR

La première chose dont nous avons besoin est une instance `OcrEngine` qui sait quelle langue reconnaître. L'anglais est la langue par défaut, mais vous pouvez la remplacer par le français, l'allemand, etc., en définissant `ocrEngine.Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialise the OCR engine and set the language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English          // Change this if your document isn’t English
};
```

Pourquoi initialiser le moteur d'abord ? Le moteur conserve le modèle de reconnaissance en mémoire, ainsi le créer une fois et le réutiliser pour plusieurs images permet d'économiser à la fois le CPU et la RAM. Dans les traitements par lots plus importants, vous conserveriez la même instance active pendant toute l'exécution.

## Étape 2 – Charger l'image et effectuer l'OCR

Ensuite, nous pointons le moteur vers le fichier que nous voulons traiter. `ImageStream.FromFile` lit l'image dans un format compris par le moteur OCR.

```csharp
// Load the image you want to process
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Run the recognition engine – this populates the internal text buffer
ocrEngine.Recognize();
```

> **Et si l'image est multi‑pages ?**  
> Aspose OCR peut gérer les TIFF multi‑pages nativement. Il suffit de fournir le chemin du fichier TIFF ; le moteur parcourra chaque page automatiquement.

## Étape 3 – Convertir l'image en EPUB

Si vous avez également besoin d'une version e‑book du document numérisé, Aspose le fait en une seule ligne. Le `EpubWriter` utilise la même instance `OcrEngine`, ce qui signifie que les résultats OCR sont réutilisés sans traitement supplémentaire.

```csharp
// Export the recognised content to an ePub file
EpubWriter epubWriter = new EpubWriter();
epubWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt.epub");
```

Pourquoi exporter en EPUB ? EPUB est un format réajustable — parfait pour les lecteurs mobiles. Le texte OCR devient sélectionnable, et l'image originale reste en arrière‑plan, préservant l'apparence du scan d'origine.

## Étape 4 – Ajouter un calque de texte interrogeable au PDF

Voici maintenant la partie qui **crée réellement un PDF interrogeable**. En activant `AddSearchableTextLayer`, le générateur PDF intègre un calque de texte invisible qui reflète la sortie OCR. Les utilisateurs peuvent rechercher, copier ou mettre en surbrillance le texte comme dans un PDF natif.

```csharp
// Configure PDF writer to include a hidden searchable text layer
PdfWriter pdfWriter = new PdfWriter
{
    AddSearchableTextLayer = true   // Enables the hidden text layer for searchability
};

// Save the OCR result as a searchable PDF
pdfWriter.Save(ocrEngine, "YOUR_DIRECTORY/receipt_searchable.pdf");
```

> **Erreur fréquente :** Oublier de définir `AddSearchableTextLayer` produit un PDF qui a l'air identique mais ne contient aucun texte interrogeable. Vérifiez toujours ce drapeau lorsque vous avez besoin d'un document interrogeable.

## Étape 5 – Exemple complet fonctionnel

En rassemblant tous les éléments, voici une application console autonome que vous pouvez placer dans un nouveau projet .NET et exécuter immédiatement.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace OcrToPdfAndEpub
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the source image
            string imagePath = "YOUR_DIRECTORY/receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Perform OCR
            ocrEngine.Recognize();

            // 4️⃣ Convert to EPUB (optional but handy)
            EpubWriter epubWriter = new EpubWriter();
            string epubPath = "YOUR_DIRECTORY/receipt.epub";
            epubWriter.Save(ocrEngine, epubPath);
            Console.WriteLine($"EPUB saved to {epubPath}");

            // 5️⃣ Create searchable PDF
            PdfWriter pdfWriter = new PdfWriter
            {
                AddSearchableTextLayer = true
            };
            string pdfPath = "YOUR_DIRECTORY/receipt_searchable.pdf";
            pdfWriter.Save(ocrEngine, pdfPath);
            Console.WriteLine($"Searchable PDF saved to {pdfPath}");
        }
    }
}
```

### Résultat attendu

* `receipt.epub` – un fichier EPUB que vous pouvez ouvrir dans Calibre, Apple Books ou n'importe quel lecteur e‑book.  
* `receipt_searchable.pdf` – un PDF où vous pouvez appuyer sur **Ctrl + F** et trouver n'importe quel mot présent dans l'image originale.

Si vous ouvrez le PDF dans Adobe Acrobat et consultez **Fichier → Propriétés → Description**, vous verrez un flux de texte caché sous l'onglet **Polices**, confirmant la présence du calque interrogeable.

## Questions fréquentes et cas particuliers

**Q : Cela fonctionne-t-il avec des langues non anglaises ?**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}