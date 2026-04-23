---
category: general
date: 2026-03-20
description: Apprenez à redresser les images et à éliminer le bruit des images avec
  Aspose OCR. Ce guide étape par étape montre également comment prétraiter les images
  pour l’OCR et améliorer la précision de l’OCR.
draft: false
keywords:
- how to deskew image
- remove image noise
- preprocess image for OCR
- recognize text from image
- improve OCR accuracy
language: fr
og_description: Apprenez à redresser les images et à éliminer le bruit avec Aspose
  OCR. Améliorez la précision de votre OCR en quelques minutes.
og_title: Comment redresser une image – Guide complet C# pour le prétraitement OCR
tags:
- OCR
- C#
- Image Processing
title: Comment redresser une image – Guide complet C# pour le prétraitement OCR
url: /fr/net/ocr-optimization/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image – Guide complet C# pour le pré‑traitement OCR

Vous vous êtes déjà demandé **comment redresser une image** qui provient d'un scanner avec un angle étrange ? Vous n'êtes pas le seul ; de nombreux développeurs rencontrent ce problème lorsqu'ils essaient d'alimenter une photo dans un moteur OCR. La bonne nouvelle, c'est qu'avec quelques lignes de C# et Aspose OCR, vous pouvez redresser, débruiter et augmenter le contraste en une seule pipeline propre — sans Photoshop.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : du chargement d'une image inclinée, à la **suppression du bruit de l'image**, au **prétraitement de l'image pour l'OCR**, et enfin à la **reconnaissance de texte à partir de l'image** avec un score élevé d'**amélioration de la précision OCR**. À la fin, vous disposerez d'une application console prête à l'emploi qui transforme un scan désordonné en texte propre et consultable.

## Ce dont vous avez besoin

- .NET 6 ou ultérieur (le code utilise la syntaxe `using var`, prise en charge depuis C# 8)
- Un package NuGet Aspose OCR (`Aspose.OCR`) – installez via `dotnet add package Aspose.OCR`
- Une image d'exemple à la fois inclinée et bruitée (par ex., `skewed_noisy.png`)
- Un IDE ou éditeur de votre choix (Visual Studio, VS Code, Rider… à vous de choisir)

> **Astuce :** Si vous n'avez pas de fichier d'exemple, il suffit de faire pivoter une capture d'écran nette de quelques degrés et d'ajouter du bruit « sel‑et‑poivre » avec un éditeur d'image. La pipeline fonctionne de la même manière.

## Étape 1 : Comment redresser une image avec un filtre Deskew

La première chose que nous faisons est de corriger la rotation. Aspose fournit un `DeskewFilter` qui peut détecter automatiquement les angles jusqu'à un `MaxAngle` configurable. Le régler à **5°** est une valeur sûre pour la plupart des documents numérisés.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image class

// Initialize the OCR engine – English is the most common language
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};

// Build the preprocessing pipeline
var preprocessPipeline = new PreprocessPipeline()
    .Add(new DeskewFilter { MaxAngle = 5 })          // This is where we answer “how to deskew image”
    .Add(new DespeckleFilter { Strength = 2 })      // Next we’ll remove image noise
    .Add(new ContrastFilter { Level = 1.5 });        // Finally we boost contrast for OCR
```

**Pourquoi c'est important :**  
Si le texte est incliné, l'algorithme OCR peut mal interpréter les caractères — par exemple « l » devenant « i ». En **redressant** d'abord, vous fournissez au moteur une toile droite sur laquelle travailler.

## Étape 2 : Suppression du bruit de l'image avec Despeckle

Les scans provenant de téléphones bon marché ou de vieux scanners contiennent souvent des taches qui ressemblent à des points aléatoires. Ces taches perturbent le reconnaisseur de caractères. Le `DespeckleFilter` lisse l'image tout en préservant les contours.

```csharp
// The DespeckleFilter is already part of the pipeline (see Step 1)
// Strength = 2 is a balanced setting; increase for very noisy pics
```

Si vous devez **supprimer le bruit de l'image** de manière plus agressive, augmentez `Strength` à 3 ou 4 — mais attention à la perte de traits fins.

## Étape 3 : Prétraitement de l'image pour l'OCR – Augmentation du contraste

Les scans à faible contraste (gris clair sur papier blanc) peuvent faire que l'OCR manque des lettres pâles. Le `ContrastFilter` étire la gamme tonale, rendant les pixels sombres plus sombres et les pixels clairs plus clairs.

```csharp
// Contrast level of 1.5 is a good starting point.
// You can experiment with values between 1.0 (no change) and 2.0 (strong boost).
```

**Cas particulier :** Si votre image source est déjà à fort contraste, appliquer ce filtre peut estomper les détails. Dans ce cas, réglez `Level` à `1.0` (désactivant effectivement le filtre).

## Étape 4 : Charger et nettoyer l'image source

Nous chargeons maintenant réellement l'image et la faisons passer à travers la pipeline que nous venons d'assembler.

```csharp
// Load the source image – replace the path with your own file location
var sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_noisy.png");

// Apply the entire preprocessing pipeline
var cleanedImage = preprocessPipeline.Apply(sourceImage);
```

> **Note :** La méthode `Apply` renvoie un nouvel objet `Image` ; l'original reste intact. Cela facilite la comparaison « avant » et « après » si vous souhaitez déboguer le processus.

## Étape 5 : Reconnaître le texte à partir de l'image avec Aspose OCR

Avec une image droite, sans bruit et à fort contraste en main, nous la transmettons enfin au moteur OCR.

```csharp
// Perform OCR on the cleaned image
var ocrResult = ocrEngine.Recognize(cleanedImage);

// Output the recognized text to the console
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Ce que vous devriez voir :** La console affiche le contenu textuel du scan original, généralement avec beaucoup moins d’erreurs de reconnaissance que si vous aviez fourni le fichier brut directement.

## Étape 6 : Vérifier et améliorer la précision OCR

Même avec une pipeline solide, certains caractères peuvent encore être erronés — surtout si la police d'origine est inhabituelle. Voici quelques astuces rapides pour **améliorer la précision OCR** :

| Problème | Solution rapide |
|----------|-----------------|
| Petite ponctuation manquante | Ajouter un `BinaryThresholdFilter` avant l'étape de contraste |
| Langues mixtes (p. ex. Anglais + Espagnol) | Set `ocrEngine.Language = Language.English | Language.Spanish;` |
| Fond très sombre | Invert the image (`new InvertFilter()`) before deskew |
| Documents volumineux | Process pages in parallel (`Parallel.ForEach`) to speed up |

Expérimentez avec l'ordre des filtres ; parfois appliquer le **contraste** avant le **despeckle** donne de meilleurs résultats sur des scans de basse qualité.

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console. Il inclut toutes les pièces que nous avons abordées, ainsi que quelques vérifications de sécurité.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine (English language)
        // -------------------------------------------------
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // -------------------------------------------------
        // 2️⃣ Build preprocessing pipeline:
        //    Deskew → Despeckle → Contrast Boost
        // -------------------------------------------------
        var preprocessPipeline = new PreprocessPipeline()
            .Add(new DeskewFilter { MaxAngle = 5 })          // how to deskew image
            .Add(new DespeckleFilter { Strength = 2 })      // remove image noise
            .Add(new ContrastFilter { Level = 1.5 });        // preprocess image for OCR

        // -------------------------------------------------
        // 3️⃣ Load the source image (adjust path as needed)
        // -------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/skewed_noisy.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ File not found: {imagePath}");
            return;
        }

        var sourceImage = Image.FromFile(imagePath);

        // -------------------------------------------------
        // 4️⃣ Apply the pipeline → cleaned image
        // -------------------------------------------------
        var cleanedImage = preprocessPipeline.Apply(sourceImage);

        // -------------------------------------------------
        // 5️⃣ Recognize text (this is the “recognize text from image” step)
        // -------------------------------------------------
        var ocrResult = ocrEngine.Recognize(cleanedImage);

        // -------------------------------------------------
        // 6️⃣ Output the result
        // -------------------------------------------------
        Console.WriteLine("\n=== OCR Output ===\n");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Sortie attendue** (en supposant que l'image d'exemple contienne « Hello World! ») :

```
=== OCR Output ===

Hello World!
```

Si vous voyez des caractères illisibles, revérifiez l'ordre de la pipeline ou augmentez le `DespeckleFilter.Strength`.

## Conclusion

Nous avons couvert **comment redresser une image**, **supprimer le bruit de l'image**, **prétraiter l'image pour l'OCR**, et enfin **reconnaître le texte à partir de l'image** en utilisant Aspose OCR — tout en gardant un œil sur **l'amélioration de la précision OCR**. L'exemple complet et exécutable montre chaque étape dans son contexte, vous permettant de l'intégrer dans n'importe quel projet .NET et de commencer à extraire du texte immédiatement.

Prêt pour le prochain défi ? Essayez d'étendre la pipeline pour gérer les PDF multi‑pages, ou expérimentez les packs de langues pour les documents multilingues. Les mêmes concepts s'appliquent — il suffit d'échanger le drapeau `Language` et éventuellement d'ajouter un `RotateFilter` pour les pages à l'envers.

Des questions ou une image récalcitrante qui ne coopère toujours pas ? Laissez un commentaire ci‑dessous, et nous résoudrons le problème ensemble. Bon codage !

![exemple de comment redresser une image](/images/deskew-example.png "Illustration de comment redresser une image avec Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}