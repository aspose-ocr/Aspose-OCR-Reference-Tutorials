---
category: general
date: 2026-04-17
description: Extraire du texte d’une image avec Aspose OCR en C#. Apprenez à lire
  le texte d’un PNG, à convertir l’image en texte et à charger l’image pour l’OCR
  en quelques minutes.
draft: false
keywords:
- extract text from image
- read text from png
- convert image to text
- c# image to text
- load image for ocr
language: fr
og_description: Extraire du texte d’une image avec Aspose OCR en C#. Ce tutoriel montre
  comment lire du texte à partir d’un PNG, convertir une image en texte et charger
  une image pour l’OCR de manière efficace.
og_title: Extraire du texte d'une image en C# – Guide complet Aspose OCR
tags:
- Aspose OCR
- C#
- Image Processing
title: Extraire du texte d'une image en C# – image en texte C# avec Aspose OCR
url: /fr/net/text-recognition/extract-text-from-image-in-c-c-image-to-text-using-aspose-oc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en C# – Guide complet Aspose OCR

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais vous ne saviez pas quelle bibliothèque choisir ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à ce problème lorsqu'ils ont une capture d'écran PNG, une facture numérisée ou un panneau multilingue et souhaitent transformer les pixels en texte consultable.  

Dans ce tutoriel, nous parcourrons une solution pratique qui vous permet d'**lire du texte à partir d'un PNG**, **convertir une image en texte**, et **charger une image pour l'OCR** en utilisant Aspose OCR — le tout en C# moderne et propre. À la fin, vous disposerez d'un programme prêt à l'emploi que vous pourrez intégrer à n'importe quel projet .NET.

## Ce que vous allez apprendre

- Comment charger un fichier image pour l'OCR (l'étape « charger une image pour l'OCR »)  
- Comment configurer Aspose OCR pour un groupe de langues spécifique  
- Comment extraire la chaîne reconnue et l'afficher dans la console  
- Conseils pour gérer plusieurs langues, les gros fichiers et la gestion de la mémoire  

Aucune documentation externe n'est requise ; tout ce dont vous avez besoin se trouve dans les extraits de code ci-dessous.

## Prérequis

- .NET 6+ SDK (ou .NET Core 3.1+ – l'API est la même)  
- Visual Studio 2022, VS Code, ou tout IDE de votre choix  
- Package NuGet **Aspose.OCR** (installer avec `dotnet add package Aspose.OCR`)  

Si vous avez tout cela, plongeons‑nous dedans.

![Extraire du texte d'une image avec Aspose OCR en C#](https://example.com/aspsoe-ocr-demo.png "extraire du texte d'une image avec Aspose OCR")

## Étape 1 – Charger l'image pour l'OCR

La première chose à faire est de fournir quelque chose à lire au moteur OCR. Aspose OCR fonctionne avec une variété de formats, mais le PNG est un choix courant pour les captures d'écran et les graphiques numérisés.

```csharp
using Aspose.OCR;

// Replace with the actual path to your PNG file
string imagePath = @"C:\Images\sample.png";

// OcrImage.FromFile handles PNG, JPEG, BMP, TIFF, etc.
OcrImage ocrImage = OcrImage.FromFile(imagePath);
```

> **Pourquoi c'est important :** Charger correctement l'image garantit que le moteur voit exactement les données de pixels attendues. Si vous transmettez un flux corrompu, la reconnaissance échouera silencieusement.

## Étape 2 – Créer et configurer le moteur OCR

Ensuite, instanciez le `OcrEngine`. Vous pouvez éventuellement définir le groupe de langues ; pour de nombreux scripts occidentaux, la valeur par défaut fonctionne, mais si vous traitez du cyrillique, de l'arabe ou des caractères asiatiques, vous voudrez informer le moteur à l'avance.

```csharp
// The using statement guarantees proper disposal of native resources.
using var ocrEngine = new OcrEngine();

// Example: set language to Cyrillic if your PNG contains Russian or Ukrainian text.
// OcrLanguage.Cyrillic covers several Slavic languages.
ocrEngine.Language = OcrLanguage.Cyrillic;

// If you need to support multiple languages, you can combine flags:
 // ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

> **Astuce pro :** Définir la langue restreint l'ensemble de caractères que le moteur recherche, ce qui accélère la reconnaissance et améliore la précision.

## Étape 3 – Effectuer l'OCR et extraire le texte

C'est maintenant le moment du travail intensif. Appelez `Recognize` avec l'image que vous avez chargée précédemment, puis lisez la propriété `Text` du résultat.

```csharp
// Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(ocrImage);

// The recognized string is available via the Text property
string extractedText = ocrResult.Text;

// Output the result to the console (or write to a file, DB, etc.)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(extractedText);
```

### Sortie attendue

Si `sample.png` contient la phrase « Hello, World! », vous verrez :

```
=== OCR Output ===
Hello, World!
```

Si l'image est plus complexe (par ex., un reçu multi‑lignes), le moteur conserve les sauts de ligne, vous offrant un bloc de texte prêt à être traité.

## Étape 4 – Regrouper le tout dans un programme complet

Ci-dessous se trouve l'application console complète et autonome que vous pouvez copier‑coller dans un nouveau projet C#. Elle inclut la gestion des erreurs et des commentaires expliquant chaque partie.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            try
            {
                // 1️⃣ Load the image you want to recognize
                // Change the path to point at your own PNG file.
                var ocrImage = OcrImage.FromFile(@"YOUR_DIRECTORY/input.png");

                // 2️⃣ Create an OCR engine instance (disposed automatically)
                using var ocrEngine = new OcrEngine();

                // 3️⃣ Choose the language group.
                // Cyrillic works for Russian, Ukrainian, Bulgarian, etc.
                // For English only, you could use OcrLanguage.English.
                ocrEngine.Language = OcrLanguage.Cyrillic;

                // 4️⃣ Perform OCR
                var ocrResult = ocrEngine.Recognize(ocrImage);

                // 5️⃣ Output the recognized text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Simple error handling – in production you’d log this.
                Console.Error.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

Exécutez le programme (`dotnet run` depuis le dossier du projet) et observez la console afficher la chaîne extraite. Voilà l'intégralité du flux de travail **extract text from image** en moins de 30 lignes de code.

## Étape 5 – Variations courantes et cas limites

### Lire du texte à partir de PNG vs. d'autres formats

Bien que l'exemple utilise un PNG, Aspose OCR prend également en charge JPEG, BMP, TIFF et GIF. Il suffit de changer l'extension du fichier ; l'appel `OcrImage.FromFile` fonctionne sans modification.

### Convertir une image en texte dans une API Web

Si vous devez exposer cette fonctionnalité via un point de terminaison HTTP, vous pouvez accepter un téléchargement `IFormFile`, convertir le flux en `OcrImage` avec `OcrImage.FromStream`, et renvoyer la chaîne en JSON. La logique OCR principale reste identique.

```csharp
// Example snippet inside an ASP.NET Core controller action
[HttpPost("api/ocr")]
public async Task<IActionResult> OcrUpload(IFormFile file)
{
    using var stream = file.OpenReadStream();
    var ocrImage = OcrImage.FromStream(stream);
    using var engine = new OcrEngine { Language = OcrLanguage.English };
    var result = engine.Recognize(ocrImage);
    return Ok(new { text = result.Text });
}
```

### Gestion des images volumineuses

Les images grandes et haute résolution peuvent consommer beaucoup de mémoire. Une approche pratique consiste à réduire l'échelle de l'image avant de la transmettre au moteur :

```csharp
// Reduce resolution to 150 DPI (good trade‑off between speed and accuracy)
ocrEngine.ImagePreprocessing = ImagePreprocessingOptions.AutoResize;
ocrEngine.Dpi = 150;
```

### Documents multilingues

Si un document mélange anglais et cyrillique, combinez les indicateurs de langue :

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Cyrillic;
```

Le moteur tentera de reconnaître les caractères des deux ensembles.

### Libération des ressources

L'instruction `using` autour de `OcrEngine` garantit que les ressources natives sont libérées. Oublier cela peut entraîner des fuites de mémoire, surtout dans les services de longue durée.

## Astuces pro pour un OCR fiable

- **Images nettes gagnent** : pré‑traitez les images (redressement, débruitage) avec des bibliothèques comme **ImageSharp** avant l'OCR.  
- **La taille de la police compte** : le texte inférieur à 10 px est souvent manqué ; envisagez d'agrandir l'image.  
- **Vérifiez `ocrResult.Confidence`** : l'objet `OcrResult` expose également un score de confiance par mot—utilisez-le pour signaler les sections à faible confiance pour une révision manuelle.  
- **Traitement par lots** : pour des dizaines de fichiers, réutilisez une même instance de `OcrEngine` afin d'éviter le surcoût d'initialisation répété.

## Conclusion

Vous venez d'apprendre comment **extraire du texte d'une image** en C# avec Aspose OCR, couvrant tout, de **load image for OCR** à **convert image to text** et **read text from PNG**. L'exemple complet et exécutable montre le code exact dont vous avez besoin, explique pourquoi chaque étape existe, et propose des variations pratiques pour des scénarios réels.

Prêt pour le prochain défi ? Essayez d'alimenter la chaîne extraite dans un index de recherche, de la traduire avec Azure Cognitive Services, ou de générer un PDF consultable avec la même couche de texte. Les possibilités sont infinies, et vous avez maintenant une base solide pour tout projet **c# image to text**.

N'hésitez pas à expérimenter, ajuster les paramètres de langue, ou intégrer cet extrait dans une application plus grande. Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}