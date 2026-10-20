---
category: general
date: 2026-03-07
description: Apprenez à redresser une image, à augmenter le contraste et à extraire
  le texte d’un scan à l’aide d’Aspose OCR. Effectuez la reconnaissance optique de
  caractères sur une image avec un exemple complet en C# et chargez facilement l’image
  pour l’OCR.
draft: false
keywords:
- how to deskew image
- extract text from scan
- how to boost contrast
- perform ocr on image
- load image for OCR
language: fr
og_description: Apprenez à redresser une image, améliorer le contraste et extraire
  le texte d’un scan à l’aide d’Aspose OCR en C#. Effectuez la reconnaissance optique
  de caractères sur une image avec un code étape par étape.
og_title: Comment redresser une image et exécuter l’OCR en C# – Guide complet
tags:
- C#
- OCR
- Image Processing
title: Comment redresser une image et exécuter l’OCR en C# – Guide complet
url: /fr/net/ocr-optimization/how-to-deskew-image-and-run-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image et exécuter l'OCR en C# – Guide complet

Si vous vous êtes déjà demandé **comment redresser une image** avant d'exécuter l'OCR, vous êtes au bon endroit. Dans ce tutoriel, nous vous guiderons à travers l'amélioration du contraste, le chargement d'une image pour l'OCR, et enfin **l'extraction du texte à partir d'un scan** avec Aspose OCR.  

Que vous numérisiez d'anciens reçus, nettoyiez des contrats scannés, ou que vous ayez simplement besoin d'une méthode fiable pour lire du texte à partir d'une photo de travers, les étapes ci‑dessous couvrent tout ce dont vous avez besoin. Pas de blabla—juste un exemple fonctionnel que vous pouvez copier‑coller dans Visual Studio.  

## Ce que vous allez accomplir

À la fin de ce guide, vous serez capable de :

* Corriger l'inclinaison jusqu'à 30° (c’est la partie **comment redresser une image**).  
* Augmenter le contraste de l'image pour des contours de caractères plus nets (**comment augmenter le contraste**).  
* Charger votre image dans le moteur OCR (**charger l'image pour l'OCR**).  
* Exécuter le processus de reconnaissance et **extraire le texte du scan**.  

Tout cela fonctionne avec le dernier package NuGet Aspose.OCR .NET (v23.11 au moment de la rédaction).  

---

![Exemple de redressement d'image](/images/deskew-example.png "comment redresser une image")

*L'image ci‑dessus montre un document scanné avant et après le redressement.*

## Prérequis

* .NET 6.0 ou version ultérieure (le code fonctionne également sur .NET Framework 4.7+).  
* Visual Studio 2022 (ou tout IDE C# de votre choix).  
* Package NuGet Aspose.OCR – à installer via `dotnet add package Aspose.OCR`.  

C’est tout. Aucun service externe, aucune clé API.

---

## Comment redresser une image avec Aspose OCR

La première chose que nous faisons est de créer un **ImageProcessingPipeline** et d’y ajouter un `DeskewFilter`. Le filtre détecte automatiquement l’angle dominant des lignes de texte et fait pivoter l’image pour la remettre à l’horizontale.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Build a pipeline – Deskew is the first filter
var processingPipeline = new ImageProcessingPipeline()
    .Add(new DeskewFilter { MaxAngle = 30 })   // how to deskew image up to 30°
    .Add(new DenoiseFilter { Level = DenoiseLevel.High }) // remove noise
    .Add(new ContrastBoostFilter { Strength = 1.5 })      // how to boost contrast
    .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize

// Attach the pipeline to the engine
ocrEngine.Settings.ImageProcessing = processingPipeline;
```

**Pourquoi c’est important :**  
Un scan incliné perturbe le moteur OCR car les caractères ne sont plus alignés avec la ligne de base. Le `DeskewFilter` analyse l’histogramme de l’image, trouve l’angle, et la fait pivoter, améliorant ainsi de façon spectaculaire la précision de reconnaissance.

> **Astuce pro :** Si vous savez que vos documents n’excèdent jamais une inclinaison de 15°, définissez `MaxAngle = 15` pour accélérer le traitement.

---

## Comment augmenter le contraste pour une meilleure reconnaissance

Après le redressement, l’étape suivante consiste à faire ressortir le texte. Le `ContrastBoostFilter` étire la plage d’intensité des pixels, ce qui est particulièrement utile pour les impressions fanées.

```csharp
// The ContrastBoostFilter is already in the pipeline above.
// You can tweak the Strength value (1.0 = no change, >1.0 = stronger boost)
.Add(new ContrastBoostFilter { Strength = 1.5 })
```

**Pourquoi cela aide :**  
Les scans à faible contraste produisent des caractères grisâtres que le binarisateur peut interpréter comme du fond. Augmenter le contraste rend les pixels sombres plus sombres et les pixels clairs plus clairs, offrant ainsi une toile plus propre au `BinarizationFilter` suivant.

---

## Effectuer l'OCR sur l'image – Chargement du fichier

Maintenant que l’image est pré‑traitée, nous devons **charger l'image pour l'OCR**. Aspose propose un utilitaire pratique `ImageStream.FromFile`.

```csharp
// Load the source image – replace the path with your own file
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Si votre image provient d’un flux (par ex., téléchargée via une API web), vous pouvez utiliser `ImageStream.FromStream(yourStream)` à la place. Le moteur accepte BMP, JPEG, PNG, TIFF, et bien d’autres formats.

---

## Exécuter le processus de reconnaissance et extraire le texte du scan

Une fois tout configuré, appeler `Recognize()` fait le gros du travail. Après l’appel, le texte reconnu est disponible via `ocrEngine.Text`.

```csharp
// Run OCR
ocrEngine.Recognize();

// Output the result
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrEngine.Text);
```

**Sortie attendue** (exemple pour une facture simple) :

```
=== Extracted Text ===
Invoice #12345
Date: 03/05/2026
Total: $1,250.00
Thank you for your business!
```

Si la sortie apparaît brouillée, revérifiez l’ordre du pipeline — redressement d’abord, puis débruitage, augmentation du contraste, et enfin binarisation. Les inverser peut détériorer les résultats.

---

## Pièges courants et cas particuliers

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Résultat vide** | L’image est trop sombre ou trop claire pour la méthode de binarisation par défaut. | Augmentez `ContrastBoostFilter.Strength` ou passez à `BinarizationMethod.Otsu`. |
| **Texte partiel manquant** | Du bruit subsiste après le débruitage. | Utilisez `DenoiseLevel.Medium` pour les images plus douces, ou ajoutez un second `DenoiseFilter`. |
| **Direction de rotation incorrecte** | Le document a une orientation mixte (par ex., une photo d’une page tournée). | Réduisez manuellement `DeskewFilter.MaxAngle` et pré‑faites pivoter l’image avec `ImageProcessor.Rotate`. |
| **Ralentissement des performances** | Grand lot d’images haute résolution. | Redimensionnez les images (`ImageProcessor.Resize`) avant le pipeline, ou traitez en parallèle (`Parallel.ForEach`). |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Build image‑processing pipeline
        var processingPipeline = new ImageProcessingPipeline()
            .Add(new DeskewFilter { MaxAngle = 30 })                     // how to deskew image up to 30°
            .Add(new DenoiseFilter { Level = DenoiseLevel.High })       // remove high‑level noise
            .Add(new ContrastBoostFilter { Strength = 1.5 })            // how to boost contrast
            .Add(new BinarizationFilter { Method = BinarizationMethod.Sauvola }); // binarize image

        // 3️⃣ Attach pipeline to OCR settings
        ocrEngine.Settings.ImageProcessing = processingPipeline;

        // 4️⃣ Load the image you want to OCR
        // Replace the path with the location of your own file
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

        // 5️⃣ Run the recognition engine
        ocrEngine.Recognize();

        // 6️⃣ Display the extracted text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

Enregistrez ceci sous le nom `Program.cs`, exécutez `dotnet run`, et observez la console afficher le résultat de **l'extraction du texte du scan**.  

---

## Prochaines étapes & sujets associés

* **Traitement par lots** – Enveloppez la logique ci‑dessus dans une boucle pour gérer des dizaines de fichiers.  
* **Packs de langues personnalisés** – Si vous devez lire des scripts non latins, chargez un modèle linguistique via `ocrEngine.Settings.Language = OcrLanguage.ChineseSimplified;`.  
* **Export PDF** – Combinez Aspose.PDF avec l’OCR pour intégrer du texte recherchable directement dans un fichier PDF.  
* **Optimisation des performances** – Expérimentez avec l’ordre du `ImageProcessingPipeline` ; parfois le débruitage avant le redressement donne de meilleurs résultats sur des photos bruyantes.  

Tous ces points s’appuient sur les concepts de base que nous avons couverts : **comment redresser une image**, **comment augmenter le contraste**, **charger l'image pour l'OCR**, **effectuer l'OCR sur l'image**, et enfin **extraire le texte du scan**.

---

## Conclusion

Nous venons de démontrer une méthode complète, prête pour la production, afin de **redresser une image** et d’exécuter l’OCR en C#. En chaînant un filtre de redressement, une étape de débruitage, une augmentation du contraste et un binarisateur, vous obtenez une entrée propre qui permet à Aspose OCR d’**extraire le texte du scan** de façon fiable.  

Testez le code, ajustez les paramètres des filtres selon vos propres documents, et vous verrez rapidement l’amélioration de la précision de reconnaissance. Des questions ? Laissez un commentaire, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}