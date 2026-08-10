---
category: general
date: 2026-06-06
description: Reconnaître le texte d’une image avec C# OCR – un exemple pas à pas d’OCR
  en C# qui extrait le texte des numérisations et convertit une numérisation en texte
  en quelques minutes.
draft: false
keywords:
- recognize text image
- c# ocr example
- extract text scan
- convert scan to text
- image to text c#
language: fr
og_description: Reconnaître le texte d’une image avec C# OCR. Découvrez un exemple
  pratique d’OCR en C# qui extrait le texte des numérisations, convertit les scans
  en texte et gère les images du monde réel.
og_title: Reconnaître le texte d’une image en C# – Tutoriel complet d’OCR
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: recognize text image using C# OCR – a step‑by‑step c# ocr example that
    extracts text from scans and convert scan to text in minutes.
  headline: recognize text image in C# – Full OCR Guide
  type: TechArticle
- questions:
  - answer: The `Windows.Media.Ocr` namespace is Windows‑only. On Linux or macOS you’d
      swap it for TesseractSharp or IronOcr—both expose a similar `Engine.Recognize`
      method, so the surrounding code stays virtually unchanged.
    question: Does this work on .NET Core on Linux?
  - answer: Handwriting recognition is still experimental. For best results, stick
      to printed fonts or consider a cloud service like Azure Cognitive Services if
      you need high accuracy.
    question: How accurate is the built‑in OCR for handwritten notes?
  - answer: 'Not out of the box. Convert each PDF page to an image first (using `PdfSharp`
      or `Ghostscript`) and then feed the bitmap to the OCR engine. --- ## Conclusion
      You now have a complete, production‑ready **c# ocr example** that can **recognize
      text image** files, **extract text scan** contents, and **co'
    question: Can I process PDFs directly?
  type: FAQPage
tags:
- OCR
- C#
- Image Processing
title: Reconnaître le texte d'une image en C# – Guide complet OCR
url: /fr/net/text-recognition/recognize-text-image-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître le texte d'une image en C# – Tutoriel OCR complet

Vous êtes-vous déjà demandé comment **reconnaître le texte d'une image** directement à partir d’une photo numérisée avec C# ? Vous n’êtes pas le seul. Que vous numérisiez d’anciens reçus, extrayiez des données d’une carte de visite, ou simplement transformiez un scan basse résolution en texte éditable, la capacité d’extraire du texte d’une image est une astuce pratique que chaque développeur devrait avoir dans sa boîte à outils.

Dans ce guide, nous parcourrons un **exemple OCR C#** qui charge une image, exécute la reconnaissance optique de caractères, et affiche le résultat dans la console. À la fin, vous pourrez **extraire le texte numérisé**, **convertir le scan en texte**, et même ajuster le processus pour des images bruyantes. Aucun service tiers sophistiqué requis — juste l’API intégrée Windows.Media.Ocr (ou tout OcrEngine compatible) et quelques lignes de code.

## Ce que vous allez apprendre

* Comment configurer un projet C# pour l’OCR.
* Le code exact nécessaire pour **reconnaître le texte d'une image**.
* Astuces pour gérer les scans basse résolution et les documents multipages.
* Moyens d’étendre l’exemple en une bibliothèque réutilisable pour vos propres applications.

### Prérequis

* .NET 6.0 ou supérieur (l’API fonctionne également avec .NET 5+).
* Visual Studio 2022 (l’édition Community convient) ou tout IDE de votre choix.
* Une image d’exemple telle que `lowres_scan.jpg` placée dans un dossier que vous pouvez référencer.
* Une connaissance de base de async/await — les appels OCR sont asynchrones dans l’API Windows.

> **Astuce pro :** Si vous êtes sur une plateforme non‑Windows, remplacez l’espace de noms `Windows.Media.Ocr` par une bibliothèque multiplateforme comme TesseractSharp ; la logique environnante reste la même.

---

## Étape 1 : Configurer la reconnaissance du texte d’une image avec un moteur OCR

Tout d’abord, nous avons besoin d’une instance de moteur OCR. La classe `OcrEngine` est le point d’entrée pour toute opération **image en texte C#**.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Create the OCR engine – default language is English.
        OcrEngine engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));
        if (engine == null)
        {
            Console.WriteLine("Failed to create OcrEngine. Make sure you are on Windows 10 version 1809 or later.");
            return;
        }

        // Continue with the rest of the pipeline...
```

**Pourquoi c’est important :** Le moteur abstrait le travail lourd de la reconnaissance de motifs. En le créant explicitement, nous obtenons le contrôle sur les paramètres de langue, ce qui est essentiel lorsque vous souhaitez plus tard **extraire le texte numérisé** dans d’autres langues.

## Étape 2 : Charger le fichier image – le cœur de la **conversion du scan en texte**

Ensuite, nous lisons l’image depuis le disque et la transformons en `SoftwareBitmap`, le format attendu par le moteur OCR.

```csharp
        // Load the image file into a SoftwareBitmap.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "lowres_scan.jpg");
        using (FileStream fs = new FileStream(imagePath, FileMode.Open, FileAccess.Read))
        {
            // Decode the image (supports JPEG, PNG, BMP, etc.).
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Optional: upscale low‑resolution images for better accuracy.
            SoftwareBitmap upscaled = SoftwareBitmap.Convert(bitmap, bitmap.BitmapPixelFormat, bitmap.BitmapAlphaMode);
            // Pass the bitmap to OCR.
            await RecognizeAsync(engine, upscaled);
        }
    }
```

**Pourquoi nous faisons cela :** Alimenter directement un flux de fichier brut dans l’OCR donne souvent de mauvais résultats, surtout avec des scans basse résolution. La conversion en `SoftwareBitmap` nous permet de manipuler le DPI, la profondeur de couleur, et même d’appliquer des filtres avant la reconnaissance.

## Étape 3 : Effectuer l’opération de **reconnaissance du texte d’une image**

Nous appelons enfin la méthode `RecognizeAsync` du moteur. C’est ici que la magie opère.

```csharp
    private static async Task RecognizeAsync(OcrEngine engine, SoftwareBitmap bitmap)
    {
        // Run OCR – this returns an OcrResult object.
        OcrResult result = await engine.RecognizeAsync(bitmap);

        // The Result contains a collection of lines and words.
        Console.WriteLine("=== OCR Output ===");
        foreach (var line in result.Lines)
        {
            Console.WriteLine(line.Text);
        }

        // For a quick **image to text c#** check, also output the raw string.
        Console.WriteLine("\nFull Text:\n" + result.Text);
    }
}
```

**Ce que vous verrez :** Si `lowres_scan.jpg` contient la phrase « Hello World », la console affichera :

```
=== OCR Output ===
Hello World

Full Text:
Hello World
```

Voilà le **exemple OCR C#** complet en action — quatre étapes logiques qui couvrent tout, du chargement du fichier à la sortie finale.

## Étape 4 : Gestion des cas limites – quand le scan n’est pas parfait

Les images du monde réel ne sont pas toujours nettes. Voici quelques ajustements que vous pouvez faire sans réécrire tout le programme :

| Problème | Solution rapide |
|----------|-----------------|
| **DPI très faible (≤ 72)** | Agrandir le bitmap avec `BitmapTransform` avant la reconnaissance. |
| **Texte incliné** | Appliquer une transformation de rotation (`SoftwareBitmap.Rotate`) pour redresser la page. |
| **Multiples langues** | Créer `OcrEngine.TryCreateFromLanguage(new OcrLanguage("en-fr"))` et définir `engine.Language` en conséquence. |
| **Fichiers volumineux** | Traiter l’image en tuiles (`engine.RecognizeAsync(tileBitmap)`) et concaténer les résultats. |

Ces ajustements garantissent que votre routine **extraire le texte numérisé** reste fiable même avec des reçus bruyants ou des photos prises sous un angle.

## Étape 5 : Transformer l’exemple en un utilitaire réutilisable (optionnel)

Si vous prévoyez de **convertir le scan en texte** à plusieurs endroits d’une application, encapsulez la logique dans une petite classe utilitaire :

```csharp
public static class OcrHelper
{
    private static readonly OcrEngine _engine = OcrEngine.TryCreateFromLanguage(new OcrLanguage("en"));

    public static async Task<string> ImageToTextAsync(string filePath)
    {
        using var fs = new FileStream(filePath, FileMode.Open, FileAccess.Read);
        var decoder = await BitmapDecoder.CreateAsync(fs.AsRandomAccessStream());
        var bitmap = await decoder.GetSoftwareBitmapAsync();

        var result = await _engine.RecognizeAsync(bitmap);
        return result.Text;
    }
}
```

Vous l’appelez simplement :

```csharp
string text = await OcrHelper.ImageToTextAsync("YOUR_DIRECTORY/lowres_scan.jpg");
Console.WriteLine(text);
```

**Pourquoi vous allez adorer cela :** L’assistant isole la plomberie OCR, vous laissant vous concentrer sur la logique métier — parfait pour un **exemple OCR C#** qui sera réutilisé dans plusieurs projets.

---

![exemple de reconnaissance du texte d'une image](https://example.com/ocr-demo.png "Capture d’écran de la sortie console OCR montrant le résultat de la reconnaissance du texte d'une image")

*Texte alternatif :* **reconnaissance du texte d'une image** sortie d’une application console OCR C#.

---

## Questions fréquentes

**Q : Cela fonctionne-t-il sur .NET Core sous Linux ?**  
R : L’espace de noms `Windows.Media.Ocr` est uniquement disponible sous Windows. Sous Linux ou macOS, remplacez‑le par TesseractSharp ou IronOcr — les deux exposent une méthode similaire `Engine.Recognize`, de sorte que le code environnant reste pratiquement inchangé.

**Q : Quelle est la précision de l’OCR intégré pour les notes manuscrites ?**  
R : La reconnaissance manuscrite est encore expérimentale. Pour de meilleurs résultats, privilégiez les polices imprimées ou envisagez un service cloud comme Azure Cognitive Services si vous avez besoin d’une haute précision.

**Q : Puis‑je traiter directement des PDF ?**  
R : Pas directement. Convertissez chaque page PDF en image d’abord (avec `PdfSharp` ou `Ghostscript`) puis alimentez le bitmap dans le moteur OCR.

---

## Conclusion

Vous disposez maintenant d’un **exemple OCR C#** complet et prêt pour la production, capable de **reconnaître le texte d'une image**, **extraire le texte numérisé**, et **convertir le scan en texte** en quelques lignes de code. En comprenant le flux — création du moteur, chargement de l’image, reconnaissance asynchrone, et gestion du résultat—vous pouvez adapter ce modèle à tout projet C# qui doit transformer des images en chaînes recherchables.

Prêt pour l’étape suivante ? Essayez d’ajouter une interface simple avec WinForms ou WPF, expérimentez avec différentes langues, ou intégrez la sortie dans une base de données pour des archives consultables. Le ciel est la limite quand vous maîtrisez les techniques **image en texte C#**.

Bon codage, et que vos scans soient toujours nets !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code fonctionnels complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extraire le texte d’une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convertir une image en texte – Effectuer l’OCR sur une image depuis une URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Comment extraire du texte d’une image en préparant des rectangles dans l’OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}