---
category: general
date: 2026-02-14
description: Apprenez à effectuer l’OCR sur un fichier TIFF ou une image et à convertir
  un PDF en utilisant l’OCR pour créer un PDF consultable — guide C# étape par étape.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: fr
og_description: Découvrez comment effectuer la reconnaissance optique de caractères
  (OCR) sur des images, convertir des PDF à l'aide de l'OCR et créer un PDF consultable
  avec Aspose OCR dans un tutoriel C# concis.
og_title: Comment effectuer l’OCR et créer un PDF consultable en C#
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: Comment effectuer l’OCR et créer un PDF consultable en C#
url: /fr/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer l'OCR et créer un PDF consultable en C#

Vous avez déjà eu besoin d'**effectuer de l'OCR** sur un document numérisé mais vous ne saviez pas comment transformer le résultat en PDF consultable ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils travaillent avec des archives TIFF héritées ou des PDF uniquement images. La bonne nouvelle ? En quelques lignes de C# et avec la bibliothèque Aspose.OCR, vous pouvez convertir un TIFF ou n'importe quelle image en un PDF entièrement consultable en quelques secondes.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : de l'installation de la bibliothèque, le chargement d'un TIFF multi‑pages, à l'appel de `RecognizeToPdf` afin que vous puissiez **convertir un PDF avec OCR** et **créer des PDF consultables** que vos utilisateurs pourront réellement rechercher. À la fin, vous disposerez d'une application console prête à l'emploi qui produit un PDF consultable à partir d'une source image.

## Prérequis

- **.NET 6.0** ou ultérieur (le code fonctionne également sur .NET Framework 4.7+).
- Une licence valide **Aspose.OCR** ou une clé d'évaluation temporaire (l'essai gratuit suffit pour les tests).
- Visual Studio 2022 (ou tout autre éditeur de votre choix) avec le gestionnaire de paquets **NuGet**.
- Un fichier d'entrée nommé `input.tif` placé dans un dossier que vous contrôlez—les TIFF multi‑pages fonctionnent immédiatement.

> **Astuce :** Si vous êtes sous Windows, copiez le TIFF dans le même dossier que le `.exe` compilé pour éviter les problèmes liés aux chemins.

## Étape 1 : Installer le package NuGet Aspose.OCR

Ouvrez le dossier de votre projet dans un terminal et exécutez :

```bash
dotnet add package Aspose.OCR
```

Cela récupère la dernière version stable (en date de février 2026, il s'agit de la 23.10) et ajoute toutes les dépendances requises. Une fois la restauration terminée, vous verrez `Aspose.OCR` répertorié sous **Dependencies** dans l'Explorateur de solutions.

## Étape 2 : Créer une application console minimale

Créez un nouveau projet console si vous n'en avez pas déjà un :

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Remplacez le `Program.cs` généré automatiquement par le code complet présenté à la **Étape 3**. Le programme :

1. Instancie le moteur OCR.
2. Charge l'image source (ou le TIFF multi‑pages).
3. Exécute l'OCR et écrit la sortie directement dans un PDF consultable.
4. Notifie l'utilisateur que le processus a réussi.

## Étape 3 : Code complet fonctionnel – De l'image au PDF consultable

Ci-dessous se trouve le fichier source **complet**. Copiez‑collez‑le dans `Program.cs`. Des commentaires sont inclus pour expliquer les parties non évidentes.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Ce que vous verrez :** Après l'exécution du programme, un fichier nommé `searchable.pdf` apparaît dans le dossier cible. Ouvrez-le avec Adobe Reader ou n'importe quel lecteur PDF et essayez de rechercher un mot présent dans le TIFF original. Le texte devrait être trouvé instantanément, prouvant que vous avez bien **créé un PDF consultable** à partir d'une image.

### Exécution de l'application

```bash
dotnet run
```

Si tout est correctement configuré, vous obtiendrez :

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

Ouvrez le PDF, appuyez sur `Ctrl+F`, tapez un mot provenant de la source, et observez le surlignage se déplacer vers l'emplacement correct.

## Étape 4 : Variantes courantes et cas limites

### Conversion d'un PDF standard (image‑only) en PDF consultable

Si votre source est un PDF contenant des images numérisées plutôt que du texte, vous pouvez toujours utiliser la même méthode—il suffit de changer la source `ImageStream` :

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Cela répond au scénario **convertir un PDF avec OCR** sans aucun code supplémentaire.

### Gestion de documents multi‑pages volumineux

Pour les documents dépassant quelques centaines de pages, envisagez :

- **Augmenter les limites de mémoire** (`Engine.MemoryLimit = 2_000; // MB`).
- **Traitement par lots** : charger un sous‑ensemble de pages, écrire des PDF intermédiaires, puis les fusionner à l'aide d'une bibliothèque PDF (par ex., Aspose.PDF).

### Gestion des langues autres que l'anglais

Aspose.OCR prend en charge de nombreuses langues dès l'installation. Définissez la langue avant la reconnaissance :

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Si vous avez besoin de **tiff en PDF consultable** dans un script non latin, assurez‑vous que le pack de langue approprié est installé.

### Que faire si le PDF de sortie est vide ?

- Vérifiez que le fichier d'entrée n'est pas corrompu.
- Assurez‑vous que le moteur OCR possède une licence valide—le mode d'évaluation peut imposer des limites de pages.
- Vérifiez que la résolution de l'image est d'au moins 300 dpi ; des résolutions inférieures peuvent entraîner une mauvaise reconnaissance.

## Étape 5 : Vérifier le résultat programmatique (facultatif)

Parfois, vous souhaitez confirmer que le PDF contient réellement une couche de texte. Vous pouvez utiliser Aspose.PDF pour extraire le texte :

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

Si `extracted` n'est pas vide, vous avez bien **créé un PDF consultable**.

## Conclusion

Nous avons couvert **comment effectuer de l'OCR** sur un TIFF (ou n'importe quelle image) et **convertir un PDF avec OCR** de manière fluide pour créer un **PDF consultable** qui se comporte comme un document natif. Les étapes clés sont :

1. Installer Aspose.OCR.  
2. Initialiser `Engine`.  
3. Charger l'image via `ImageStream`.  
4. Appeler `RecognizeToPdf`.  

À partir de là, vous pouvez expérimenter avec les paramètres de langue, le traitement de gros lots, ou combiner la sortie avec d'autres tâches de manipulation de PDF. Le même schéma fonctionne pour **tiff en PDF consultable**, **PDF consultable à partir d'une image**, et même les PDF numérisés.

Prêt pour le prochain défi ? Essayez d'intégrer l'OCR dans une API web afin que les utilisateurs puissent télécharger des numérisations et recevoir des PDF consultables instantanément, ou explorez l'OCR sur des notes manuscrites en utilisant les paramètres avancés du `OcrEngine`. Les possibilités sont infinies—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}