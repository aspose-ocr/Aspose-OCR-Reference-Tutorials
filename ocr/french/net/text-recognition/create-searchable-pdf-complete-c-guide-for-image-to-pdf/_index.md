---
category: general
date: 2026-04-08
description: Créez rapidement des PDF recherchables et apprenez à compresser les images
  PDF, à incorporer les polices PDF et à reconnaître le texte d’image en C# avec Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: fr
og_description: Créez rapidement des PDF recherchables avec Aspose.OCR. Apprenez à
  compresser les images PDF, à intégrer des polices dans le PDF et à reconnaître le
  texte d’une image dans un seul tutoriel.
og_title: Créer un PDF recherchable – Guide complet C#
tags:
- Aspose.OCR
- C#
- PDF Generation
title: Créer un PDF recherchable – Guide complet C# pour convertir une image en PDF
url: /fr/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable – Guide complet C#

Besoin de **créer un PDF consultable** à partir d’une image numérisée ? Vous n’êtes pas le seul à avoir contemplé un énorme PNG en vous demandant comment le transformer en un document léger et **recherchable**. La bonne nouvelle, c’est qu’avec Aspose.OCR vous pouvez le faire en quelques lignes, et vous apprendrez également à **compresser les images PDF**, **intégrer les polices PDF**, et **reconnaître le texte d’une image** sans effort.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : du chargement d’une image, à l’exécution de l’OCR, en passant par le réglage des options d’enregistrement PDF, jusqu’à l’écriture finale d’un PDF consultable sur le disque. À la fin, vous disposerez d’une méthode prête à l’emploi que vous pourrez intégrer à n’importe quel projet .NET, ainsi que de quelques astuces professionnelles pour les cas particuliers que vous pourriez rencontrer plus tard.

## Ce dont vous avez besoin

- **.NET 6+** (le code fonctionne également sur .NET Framework 4.7, mais nous viserons .NET 6 pour une syntaxe moderne).  
- **Aspose.OCR for .NET** – installer via NuGet : `Install-Package Aspose.OCR`.  
- Un fichier image (PNG, JPEG, TIFF) contenant le texte que vous souhaitez rendre consultable.  
- Une petite dose de curiosité – le reste est expliqué ci‑dessous.

> **Astuce :** Si vous prévoyez de traiter des dizaines de pages, envisagez de réutiliser une seule instance de `OcrEngine` afin d’éviter le surcoût de chargement répété des données de langue.

## Étape 1 : Configurer le moteur OCR – Reconnaître le texte d’une image

La première chose dont nous avons besoin est un moteur OCR capable de lire les caractères du bitmap source. Aspose.OCR vous permet de spécifier la langue (anglais, français, etc.) et renvoie un objet `OcrResult` contenant à la fois le texte brut et les données d’image.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**Pourquoi c’est important :**  
- Définir la langue améliore considérablement la précision ; le moteur charge en arrière‑plan des dictionnaires spécifiques à la langue.  
- `OcrResult` ne contient pas seulement la chaîne extraite mais aussi le bitmap sous‑jacent, que nous intégrerons ensuite dans le PDF afin que le document reste visuellement identique à la numérisation d’origine.

## Étape 2 : Configurer les options d’enregistrement PDF – Compresser les images PDF & intégrer les polices

Un PDF consultable est essentiellement un PDF ordinaire avec une couche de texte invisible superposée à l’image numérisée. Si vous ignorez la compression, le fichier final peut devenir très volumineux. La classe `PdfSaveOptions` vous offre un contrôle granulaire sur la qualité de l’image, l’intégration des polices et la sous‑ensemble des polices.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**Pourquoi vous devez intégrer les polices dans le PDF :**  
Lorsqu’un PDF est ouvert sur un système qui ne possède pas la police exacte utilisée dans la couche OCR, le texte peut apparaître illisible. L’intégration garantit la fidélité visuelle sur toutes les plateformes, ce qui est essentiel pour les documents juridiques ou d’archives.

## Étape 3 : Enregistrer le résultat en PDF consultable – Image vers PDF consultable

Nous rassemblons maintenant le tout : prendre le `OcrResult`, appliquer nos `PdfSaveOptions` et écrire le fichier. La méthode `SaveAsSearchablePdf` effectue le travail lourd — elle crée une superposition de texte cachée qui reflète le résultat de l’OCR tout en conservant l’image originale.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### Exemple complet fonctionnel

Voici un programme console autonome que vous pouvez copier‑coller dans un nouveau projet console .NET. Il suppose que l’image se trouve dans un dossier nommé `YOUR_DIRECTORY` relatif à l’exécutable.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

L’exécution du programme générera `output.pdf` que vous pourrez ouvrir avec Adobe Reader, Foxit ou tout autre lecteur PDF et rechercher instantanément des mots qui n’étaient à l’origine que dans l’image.

## Étape 4 : Vérifier le résultat – La recherche fonctionne‑t‑elle ?

Une fois le fichier généré, ouvrez‑le et testez la fonction de recherche intégrée (Ctrl + F). Si vous pouvez localiser des mots comme « invoice », « date » ou « total », vous avez créé avec succès un **PDF consultable**.

Si la recherche ne renvoie rien :

1. **Vérifiez la précision de l’OCR** – il se peut que l’image source soit de basse résolution. Envisagez d’augmenter le DPI avant l’OCR (Aspose vous permet de définir `Resolution` sur le moteur).  
2. **Confirmez l’intégration des polices** – ouvrez les propriétés du PDF et consultez la section *Fonts* ; vous devriez y voir la police intégrée.  
3. **Inspectez la compression de l’image** – une `ImageQuality` très basse peut rendre la couche visuelle illisible, ce qui perturbe parfois les outils en aval.

## Variations courantes et cas particuliers

| Scénario | Ce qu’il faut ajuster | Pourquoi |
|----------|-----------------------|----------|
| **Multi‑page TIFF** | Boucler sur chaque trame, appeler `RecognizeImage` pour chaque page, puis utiliser `PdfSaveOptions` avec `AppendMode = true`. | Conserve chaque page numérisée comme une page consultable distincte. |
| **Non‑English language** | Modifiez `Language = "fr"` (ou le code ISO approprié) et, éventuellement, fournissez un dictionnaire personnalisé. | Améliore la reconnaissance des caractères accentués et des glyphes spécifiques à la langue. |
| **Very large images** | Réduisez la taille du bitmap avant l’OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | Réduit l’utilisation de la mémoire et accélère l’OCR sans sacrifier trop de précision. |
| **Need OCR confidence** | Accédez à `ocrResult.RecognizedWords` et examinez la propriété `Confidence`. | Vous permet de signaler les mots à faible confiance pour une révision manuelle. |

## Conseils de performance

- **Réutilisez le `OcrEngine`** lors du traitement d’un lot de fichiers – il met en cache les données de langue.  
- **Parallélisez** l’étape de reconnaissance avec `Parallel.ForEach` si vous êtes sur une machine multi‑cœur, mais gardez les écritures PDF séquentielles pour éviter les conflits d’accès aux fichiers.  
- **Ajustez `ImageQuality`** : 85‑90 donne des images quasi‑sans perte, tandis que 60‑70 suffit souvent pour les documents très textuels.

## Conclusion

Nous avons couvert tout ce dont vous avez besoin pour **créer des fichiers PDF consultables** à partir d’images en utilisant Aspose.OCR, tout en apprenant comment **compresser les images PDF**, **intégrer les polices PDF**, et **reconnaître le texte d’une image** de manière efficace. L’exemple de code complet est prêt à être intégré à n’importe quel projet C#, et les astuces supplémentaires vous aideront à adapter la solution à des charges de travail plus importantes ou à d’autres langues.

Prêt pour l’étape suivante ? Essayez d’ajouter un filigrane, de fusionner plusieurs PDF consultables, ou d’intégrer cette routine dans une API web afin que les utilisateurs puissent télécharger des numérisations et recevoir instantanément des PDF consultables. Les possibilités sont infinies, et avec les bases en place, vous trouverez facile d’étendre le flux de travail.

Bon codage, et que vos PDF restent petits, consultables et parfaitement rendus !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}