---
category: general
date: 2026-03-07
description: Comment créer un ePub à partir d'images numérisées avec Aspose OCR –
  apprenez à convertir une image en ePub, extraire le texte d’une image, ajouter un
  auteur à l’ePub et charger une image pour l’OCR.
draft: false
keywords:
- how to create epub
- convert image to epub
- extract text from image
- add author to epub
- load image for ocr
language: fr
og_description: Comment créer un ePub à partir d'images numérisées en C#. Ce tutoriel
  vous montre comment convertir une image en ePub, extraire le texte d’une image,
  ajouter un auteur à l’ePub et charger l’image pour l’OCR.
og_title: Comment créer un ePub à partir d'images en C# – Guide complet
tags:
- C#
- Aspose OCR
- ePub
- Document Conversion
title: Comment créer un ePub à partir d'images en C# – Guide étape par étape
url: /fr/net/text-recognition/how-to-create-epub-from-images-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer un ePub à partir d'images en C# – Guide complet

Vous vous êtes déjà demandé **comment créer un ePub** à partir d’une collection de pages numérisées ? Peut‑être avez‑vous quelques PNG d’un roman classique et vous aimeriez les transformer en un ePub propre que vous pouvez lire sur n’importe quel appareil. Bonne nouvelle : avec Aspose OCR, vous pouvez **charger l’image pour l’OCR**, extraire le texte, puis **convertir l’image en ePub** en quelques lignes de C#.

Dans ce tutoriel, nous passerons en revue l’ensemble du pipeline : chargement de l’image, extraction du texte, ajout de quelques métadonnées (oui, nous allons **ajouter l’auteur à l’ePub**), et enfin écriture d’un fichier ePub conforme aux standards. À la fin, vous disposerez d’un ePub prêt à publier et d’une compréhension solide de chaque étape, afin de pouvoir adapter le code pour des livres multi‑pages, des polices personnalisées ou même une distribution sans DRM.

## Ce dont vous avez besoin

- **.NET 6** ou version ultérieure (l’API fonctionne également avec .NET Standard 2.0+)  
- **Aspose.OCR for .NET** – vous pouvez obtenir une version d’essai gratuite sur le site d’Aspose.  
- Une image numérisée comme `book_page.png` placée quelque part sur le disque.  
- Un IDE préféré (Visual Studio, Rider ou VS Code – j’utiliserai Visual Studio dans les captures d’écran).

Aucun package NuGet supplémentaire n’est requis ; Aspose.OCR regroupe tout ce dont vous avez besoin pour l’export ePub.

---

![Comment créer un ePub à partir d’une image numérisée](/images/how-to-create-epub.png "Comment créer un ePub à partir d’une image numérisée avec Aspose OCR")

## Étape 1 – Configurer le projet et installer Aspose.OCR

Première chose à faire. Créez une nouvelle application console :

```bash
dotnet new console -n OcrToEpubDemo
cd OcrToEpubDemo
```

Ajoutez le package Aspose.OCR :

```bash
dotnet add package Aspose.OCR
```

C’est tout – la bibliothèque inclut à la fois les capacités d’OCR et d’export ePub, vous n’aurez donc besoin d’aucune dépendance supplémentaire.

## Étape 2 – Charger l’image pour l’OCR

Avant de pouvoir **extraire le texte de l’image**, il faut fournir quelque chose à lire au moteur OCR. L’assistant `ImageStream.FromFile` rend cela trivial :

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the PNG (or JPG, TIFF, etc.) you want to process
// This is the “load image for OCR” step.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");
```

> **Astuce :** Si votre image se trouve dans une ressource incorporée, utilisez `ImageStream.FromResource` au lieu de `FromFile`.

## Étape 3 – Extraire le texte de l’image

Maintenant le moteur lit réellement les pixels et les transforme en chaînes Unicode. La méthode `Recognize` fait le gros du travail.

```csharp
// Run the OCR process – this will fill ocrEngine.RecognitionResult
ocrEngine.Recognize();

// Optional: inspect the raw text
string rawText = ocrEngine.RecognitionResult.Text;
Console.WriteLine("Extracted text (first 200 chars):");
Console.WriteLine(rawText.Substring(0, Math.Min(200, rawText.Length)));
```

Pourquoi appeler `Recognize` séparément ? Cela vous permet d’inspecter la sortie brute de l’OCR, d’ajuster les paramètres de langue ou même d’exécuter une vérification orthographique avant de passer à la création de l’ePub.

## Étape 4 – Préparer les options d’export ePub (Ajouter l’auteur à l’ePub)

Créer un ePub soigné ne consiste pas seulement à déposer du texte ; il faut également des métadonnées correctes. La classe `EpubExportOptions` vous offre un moyen propre d’**ajouter l’auteur à l’ePub**, de définir un titre et de décider d’inclure ou non les images originales.

```csharp
var epubExportOptions = new EpubExportOptions
{
    Title = "Scanned Book",          // Title shown in eReader libraries
    Author = "Unknown",              // This is where we “add author to epub”
    IncludeImages = true             // Embeds the original PNGs for visual fidelity
};
```

Si vous avez plusieurs pages, vous pouvez continuer à appeler `ocrEngine.Image = …` et `ocrEngine.Recognize()` dans une boucle ; chaque appel ajoute le contenu de la nouvelle page au même document ePub.

## Étape 5 – Convertir l’image en ePub et exporter

Avec le texte extrait et les métadonnées définies, l’étape finale se résume à une seule ligne qui écrit le fichier ePub sur le disque :

```csharp
// Export the recognized content to an ePub file
ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

// Confirmation for the user
Console.WriteLine("ePub created.");
```

Le `book.epub` résultant peut être ouvert dans Calibre, Apple Books ou tout lecteur compatible EPUB. Parce que nous avons défini `IncludeImages = true`, le PNG original apparaîtra comme une page image, préservant l’aspect de la source numérisée.

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet, prêt à être exécuté :

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // This is the “load image for OCR” step.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book_page.png");

        // Step 3: Run the OCR recognition – we now “extract text from image”
        ocrEngine.Recognize();

        // (Optional) Print a snippet of the extracted text
        string snippet = ocrEngine.RecognitionResult.Text.Substring(0,
            Math.Min(200, ocrEngine.RecognitionResult.Text.Length));
        Console.WriteLine("Extracted text preview:");
        Console.WriteLine(snippet);
        Console.WriteLine();

        // Step 4: Set up ePub export options – we “add author to epub” here
        var epubExportOptions = new EpubExportOptions
        {
            Title = "Scanned Book",
            Author = "Unknown",
            IncludeImages = true   // embed the original images in the ePub
        };

        // Step 5: Export the recognized content – this is how we “convert image to epub”
        ocrEngine.ExportToEpub("YOUR_DIRECTORY/book.epub", epubExportOptions);

        // Step 6: Inform the user that the ePub has been created
        Console.WriteLine("ePub created.");
    }
}
```

### Sortie attendue

```
Extracted text preview:
Chapter 1
It was a bright cold day in April, and the...
 
ePub created.
```

Ouvrez `book.epub` dans votre lecteur préféré et vous verrez une page de titre, la ligne d’auteur (même si elle indique « Unknown »), ainsi que l’image numérisée affichée à côté du texte sélectionnable.

## Questions fréquentes & cas particuliers

### Et si la langue de l’OCR n’est pas l’anglais ?

Aspose.OCR prend en charge plus de 70 langues. Il suffit de définir la propriété `Language` avant d’appeler `Recognize` :

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

### Comment gérer les livres multi‑pages ?

Enveloppez la logique de chargement/reconnaissance dans une boucle `foreach` :

```csharp
string[] pages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var pagePath in pages)
{
    ocrEngine.Image = ImageStream.FromFile(pagePath);
    ocrEngine.Recognize();
}
ocrEngine.ExportToEpub("YOUR_DIRECTORY/full_book.epub", epubExportOptions);
```

Chaque itération ajoute le texte nouvellement reconnu au même ePub, en conservant l’ordre des pages.

### Puis‑je exclure les images originales ?

Bien sûr – définissez `IncludeImages = false` dans `EpubExportOptions`. L’ePub résultant sera alors du texte purement réflowable, ce qui réduit considérablement la taille du fichier.

### Qu’en est‑il des polices ou du style personnalisés ?

L’exportateur ePub d’Aspose.OCR vous permet de fournir une feuille de style CSS via la propriété `Css` de `EpubExportOptions`. Ainsi, vous pouvez imposer une famille de polices spécifique, une hauteur de ligne ou des marges particulières.

## Conclusion

Vous savez maintenant **comment créer un ePub** à partir d’une image numérisée en utilisant Aspose OCR en C#. Le tutoriel a couvert tout le processus, de **charger l’image pour l’OCR**, à **extraire le texte de l’image**, en passant par **ajouter l’auteur à l’ePub**, jusqu’à **convertir l’image en ePub** avec un appel d’export unique. Avec le code complet en main, vous pouvez étendre la solution pour traiter par lots des bibliothèques entières, injecter une couverture personnalisée, ou même intégrer le flux de travail dans une API web.

Prêt pour le prochain défi ? Essayez de convertir un PDF en ePub, ou expérimentez les seuils de confiance de l’OCR pour améliorer la précision sur des numérisations bruyantes. Le ciel est la limite quand vous combinez un OCR puissant avec une génération d’ePub flexible.

Bon codage, et bonne lecture de votre ePub fraîchement créé !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}