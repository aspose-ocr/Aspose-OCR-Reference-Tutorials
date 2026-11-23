---
category: general
date: 2026-06-16
description: Prétraiter l'image pour l'OCR en utilisant Aspose OCR en C#. Apprenez
  à améliorer le contraste de l'image et à éliminer le bruit de l'image numérisée
  pour une extraction de texte précise.
draft: false
keywords:
- preprocess image for OCR
- enhance image contrast
- remove noise from scanned image
language: fr
og_description: Prétraitez l'image pour l'OCR avec Aspose OCR. Améliorez la précision
  en augmentant le contraste de l'image et en supprimant le bruit de l'image numérisée.
og_title: Prétraitement d'image pour l'OCR en C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  headline: Preprocess Image for OCR in C# – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  name: Preprocess Image for OCR in C# – Complete Guide
  steps:
  - name: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
    text: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
  - name: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
    text: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
  - name: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
    text: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
  - name: '**Build** the console project (`dotnet build`).'
    text: '**Build** the console project (`dotnet build`).'
  - name: '**Run** (`dotnet run`). You should see something like:'
    text: '**Run** (`dotnet run`). You should see something like:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: Prétraitement d'image pour l'OCR en C# – Guide complet
url: /fr/net/ocr-optimization/preprocess-image-for-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Prétraiter l'image pour l'OCR – Guide complet

Vous êtes-vous déjà demandé pourquoi vos résultats d'OCR ressemblent à un méli‑mélange alors que la photo source est assez nette ? La vérité, c’est que la plupart des moteurs OCR—y compris Aspose OCR—attendent une image propre et bien alignée. **Prétraiter l'image pour l'OCR** est la première étape pour transformer un scan flou et à faible contraste en texte net et lisible par la machine.

Dans ce tutoriel, nous parcourrons un exemple pratique, de bout en bout, qui non seulement **prétraite l'image pour l'OCR** mais montre aussi comment **améliorer le contraste de l'image** et **supprimer le bruit d'une image scannée** à l'aide des filtres intégrés d'Aspose. À la fin, vous disposerez d’une application console C# prête à l’emploi qui fournit des résultats de reconnaissance bien plus fiables.

---

## Ce dont vous avez besoin

- **.NET 6.0 ou version ultérieure** (le code fonctionne également avec .NET Framework 4.6+)
- **Aspose.OCR for .NET** – vous pouvez récupérer le package NuGet `Aspose.OCR`
- Une image d’exemple présentant du bruit, un angle ou un contraste médiocre (nous utiliserons `skewed-photo.jpg` dans la démo)
- L’IDE de votre choix – Visual Studio, Rider ou VS Code conviendra parfaitement

Aucune bibliothèque native supplémentaire ni installation complexe n’est requise ; tout réside dans le package Aspose.

---

## ## Prétraiter l'image pour l'OCR – Implémentation étape par étape

Voici le fichier source complet que vous compilerez. N’hésitez pas à le copier‑coller dans un nouveau projet console et à appuyer sur **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Add preprocessing filters to improve recognition.
        // 2a – Remove noise from scanned image.
        ocrEngine.Settings.Filters.Add(new DenoiseFilter()); // Reduces random speckles.
        // 2b – Correct skew (deskew) that often appears in photographed documents.
        ocrEngine.Settings.Filters.Add(new DeskewFilter()); // Straightens the baseline.
        // 2c – Enhance image contrast for better character separation.
        ocrEngine.Settings.Filters.Add(new ContrastEnhanceFilter()); // Boosts contrast.

        // Step 3: (Optional) Rotate the image if it was captured at an angle.
        // Negative values rotate clockwise, positive counter‑clockwise.
        ocrEngine.Settings.Filters.Add(new RotateFilter(-3)); // Small correction.

        // Step 4: Perform OCR on the image file.
        // Replace the path with the actual location of your test image.
        string extractedText = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed-photo.jpg");

        // Step 5: Display the recognized text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

### Pourquoi chaque filtre est important

| Filtre | Ce qu’il fait | Pourquoi il aide l'OCR |
|--------|---------------|------------------------|
| **DenoiseFilter** | Élimine le bruit aléatoire des pixels qui apparaît souvent dans les scans en faible lumière. | Le bruit peut être confondu avec des fragments de glyphes, corrompant la forme des caractères. |
| **DeskewFilter** | Détecte l’angle dominant des lignes de texte et fait pivoter l’image à 0°. | Des lignes de base inclinées font croire au moteur OCR que les caractères sont penchés, entraînant des erreurs de reconnaissance. |
| **ContrastEnhanceFilter** | Amplifie la différence entre le texte sombre et le fond clair. | Un contraste plus élevé améliore l’étape de seuillage binaire dans la plupart des pipelines OCR. |
| **RotateFilter** (optionnel) | Applique une rotation manuelle que vous spécifiez. | Pratique lorsque le désalignement automatique n’est pas suffisant, par ex. une photo prise sous un léger angle. |

> **Astuce :** Si votre source est un PDF scanné, exportez d’abord la page en tant qu’image (par ex. avec `PdfRenderer`) puis alimentez‑la avec la même chaîne de filtres. La même logique de prétraitement s’applique.

---

## ## Améliorer le contraste de l'image avant l'OCR – Confirmation visuelle

Ajouter un filtre, c’est bien ; voir l’effet, c’est mieux. Voici une illustration simple avant‑et‑après (remplacez par vos propres captures d’écran lors de vos tests).

![Diagram of preprocess image for OCR pipeline](image.png){alt="Diagram of preprocess image for OCR pipeline"}

Le côté gauche montre le scan brut et bruité, tandis que le côté droit affiche la même image après **améliorer le contraste de l'image**, **supprimer le bruit d'une image scannée**, et désalignement. Remarquez comment les caractères deviennent nets et isolés — exactement ce dont le moteur OCR a besoin.

---

## ## Supprimer le bruit d'une image scannée – Cas limites et conseils

Tous les documents ne souffrent pas du même type de bruit. Voici quelques scénarios que vous pourriez rencontrer et comment ajuster la chaîne de traitement :

1. **Bruit sel‑et‑poivre important** – Augmentez l’agressivité du `DenoiseFilter` en passant un objet `DenoiseOptions` personnalisé (par ex. `new DenoiseFilter(new DenoiseOptions { Strength = 2 })`).  
2. **Encre fanée sur papier jaune** – Associez `ContrastEnhanceFilter` à un `BrightnessAdjustFilter` pour éclaircir le fond avant d’augmenter le contraste.  
3. **Texte coloré** – Convertissez d’abord l’image en niveaux de gris (`new GrayscaleFilter()`) car la plupart des moteurs OCR, y compris Aspose, fonctionnent mieux avec des données monochromes.  

L’ordre des filtres peut également influencer le résultat. En pratique, je place le `DenoiseFilter` **avant** le `DeskewFilter` parce qu’une image plus propre fournit à l’algorithme de désalignement des données de bord plus fiables.

---

## ## Exécuter la démo et vérifier la sortie

1. **Construisez** le projet console (`dotnet build`).  
2. **Exécutez** (`dotnet run`). Vous devriez voir quelque chose comme :

```
=== OCR RESULT ===
The quick brown fox jumps over the lazy dog.
```

Si la sortie contient encore des caractères illisibles, vérifiez que le chemin de l’image est correct et que le fichier source n’est pas déjà trop basse résolution (minimum 300 dpi recommandé pour la plupart des tâches OCR).

---

## Conclusion

Vous disposez maintenant d’un modèle solide, prêt pour la production, pour **prétraiter l'image pour l'OCR** en C#. En chaînant les filtres `DenoiseFilter`, `DeskewFilter` et `ContrastEnhanceFilter` d’Aspose—et éventuellement un `RotateFilter`—vous pouvez **améliorer le contraste de l'image**, **supprimer le bruit d'une image scannée**, et augmenter considérablement la précision de l’extraction de texte suivante.

Et après ? Essayez d’alimenter l’image nettoyée à d’autres étapes de post‑traitement comme la correction orthographique, la détection de langue, ou l’alimentation du texte brut dans un pipeline de traitement du langage naturel. Vous pouvez également explorer le `BinarizationFilter` d’Aspose pour des flux de travail uniquement binaires, ou passer à un autre moteur OCR (Tesseract, Microsoft OCR) tout en réutilisant la même chaîne de prétraitement.

Vous avez une image difficile qui refuse toujours de coopérer ? Laissez un commentaire, et nous résoudrons le problème ensemble. Bon codage, et que vos résultats OCR soient toujours d’une clarté cristalline !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}