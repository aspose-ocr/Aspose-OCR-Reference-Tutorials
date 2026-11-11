---
category: general
date: 2026-04-03
description: Reconnaître le texte d’une image en utilisant Aspose OCR en C#. Apprenez
  à charger une image pour l’OCR, extraire le texte de l’image, écrire un fichier
  JSON en C# et effectuer l’OCR sur un PNG.
draft: false
keywords:
- recognize text from image
- write json file c#
- load image for ocr
- extract text from image
- perform ocr on png
language: fr
og_description: Reconnaître le texte d’une image avec Aspose OCR en C#. Guide étape
  par étape pour charger une image pour l’OCR, extraire le texte de l’image, écrire
  un fichier JSON en C# et effectuer l’OCR sur un PNG.
og_title: Reconnaître du texte à partir d'une image en C# – Tutoriel complet Aspose
  OCR
tags:
- OCR
- C#
- Aspose
title: Reconnaître du texte à partir d'une image en C# – Guide complet d'Aspose OCR
url: /fr/net/text-recognition/recognize-text-from-image-in-c-full-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image en C# – Tutoriel complet Aspose OCR

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** sans savoir quelle bibliothèque choisir ? Peut‑être avez‑vous un lot de reçus numérisés, une capture d’écran PNG, ou une note manuscrite que vous souhaitez transformer en données consultables. Bonne nouvelle : avec Aspose.OCR, vous pouvez le faire en quelques lignes de code C#, et vous obtiendrez même un fichier JSON propre que vous pourrez injecter dans d’autres systèmes.

Dans ce tutoriel, nous allons parcourir le chargement d’une image pour l’OCR, l’extraction du texte à partir de l’image, la sérialisation du résultat dans un fichier JSON, puis la gestion des fichiers PNG sans effort. À la fin, vous disposerez d’une application console prête à l’emploi qui **reconnaît du texte à partir d'une image** et écrit la sortie dans *output.json*.

## Ce dont vous avez besoin

- .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework)
- Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Un PNG (ou tout format supporté) que vous souhaitez traiter
- Visual Studio, VS Code, ou tout éditeur C# de votre choix

Aucune bibliothèque tierce supplémentaire n’est requise — seulement le moteur Aspose OCR et le sérialiseur intégré `System.Text.Json`.

## Étape 1 : Reconnaître du texte à partir d'une image avec Aspose OCR

La première chose à faire est de créer une instance de `OcrEngine`. Cet objet effectue le travail lourd en coulisses.

```csharp
using Aspose.OCR;
using System.Drawing;
using System.IO;
using System.Text.Json;

class JsonExportDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this is where the magic starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image for OCR – replace the path with your own file.
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/input.png");

        // Perform OCR on the loaded image and get a structured result.
        OcrResult ocrResult = ocrEngine.RecognizeToResult(sourceImage);

        // Serialize the result into a nicely indented JSON string.
        string json = JsonSerializer.Serialize(
            ocrResult,
            new JsonSerializerOptions { WriteIndented = true });

        // Write JSON file C# – this will create output.json next to your exe.
        File.WriteAllText(@"YOUR_DIRECTORY/output.json", json);
    }
}
```

**Pourquoi c’est important :** Instancier `OcrEngine` une fois et le réutiliser est plus efficace que de créer un nouveau moteur pour chaque fichier. L’appel `RecognizeToResult` renvoie un objet `OcrResult` qui contient déjà le texte extrait, les scores de confiance et les boîtes englobantes — parfait pour le traitement en aval.

## Étape 2 : Charger l’image pour l’OCR – gestion des différents formats

Aspose OCR peut lire PNG, JPEG, BMP et bien d’autres formats. Si vous traitez un PNG contenant de la transparence, il peut être judicieux de le aplatir d’abord afin d’éviter des espaces vides inattendus.

```csharp
// Optional: flatten PNG with transparency to a white background.
if (sourceImage.RawFormat.Equals(System.Drawing.Imaging.ImageFormat.Png))
{
    Bitmap flat = new Bitmap(sourceImage.Width, sourceImage.Height);
    using (Graphics g = Graphics.FromImage(flat))
    {
        g.Clear(Color.White);
        g.DrawImage(sourceImage, 0, 0);
    }
    sourceImage = flat;
}
```

**Astuce :** Vérifiez toujours que les dimensions de l’image sont raisonnables (par ex., largeur > 50 px). Les images très petites peuvent faire manquer des caractères à l’engin OCR, entraînant de faibles scores de confiance.

## Étape 3 : Écrire un fichier JSON en C# – rendre la sortie exploitable

Le sérialiseur `System.Text.Json` est rapide et intégré, mais vous pouvez le remplacer par `Newtonsoft.Json` si vous avez besoin de convertisseurs personnalisés. L’exemple ci‑dessus utilise déjà `WriteIndented = true` afin que le fichier résultant soit lisible par l’homme.

```csharp
// Expected output (truncated):
{
  "Text": "Hello World",
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Hello World",
          "Confidence": 0.98,
          "BoundingBox": { "X": 10, "Y": 20, "Width": 120, "Height": 30 }
        }
      ]
    }
  ]
}
```

Disposer des données OCR en JSON vous permet de les importer facilement dans des bases de données, de les envoyer via HTTP, ou de les alimenter dans des pipelines d’apprentissage automatique.

## Étape 4 : Vérifier le résultat – contrôle rapide

Après l’exécution du programme, ouvrez `output.json` et cherchez le champ `"Text"`. S’il contient la chaîne attendue, vous avez **extrait du texte à partir d'une image** avec succès. Si la confiance est faible, envisagez de pré‑traiter l’image (par ex., augmenter le contraste ou appliquer un seuillage binaire).

```csharp
Console.WriteLine($"Extracted text: {ocrResult.Text}");
Console.WriteLine($"Overall confidence: {ocrResult.Confidence:P2}");
```

L’exécution de la console affichera quelque chose comme :

```
Extracted text: Hello World
Overall confidence: 98.00%
```

C’est un bon indicateur que l’OCR a fonctionné comme prévu.

## Problèmes courants et cas limites

| Problème | Pourquoi cela se produit | Comment corriger |
|----------|--------------------------|------------------|
| **Sortie vide** | L’image est trop sombre ou possède un espace colorimétrique non supporté | Convertir en niveaux de gris, augmenter la luminosité, ou aplatir le PNG (voir Étape 2) |
| **Caractères indésirables** | DPI faible (< 72) ou bruit important | Agrandir l’image ou appliquer un filtre de débruitage avant de la passer à `RecognizeToResult` |
| **Les gros fichiers provoquent une pression mémoire** | Charger un PNG multi‑méga‑pixel dans un `Bitmap` consomme de la RAM | Traiter les images par morceaux ou les réduire tout en conservant la lisibilité |
| **Erreur de sérialisation JSON** | `OcrResult` contient des références circulaires (peu probable) | Utiliser `JsonSerializerOptions { ReferenceHandler = ReferenceHandler.IgnoreCycles }` |

## Bonus : Effectuer l’OCR sur des PNG dans une boucle batch

Si vous avez un dossier rempli de fichiers PNG, vous pouvez étendre la démo pour les parcourir :

```csharp
string[] pngFiles = Directory.GetFiles(@"YOUR_DIRECTORY", "*.png");
foreach (var file in pngFiles)
{
    Image img = Image.FromFile(file);
    OcrResult res = ocrEngine.RecognizeToResult(img);
    string outPath = Path.ChangeExtension(file, ".json");
    File.WriteAllText(outPath, JsonSerializer.Serialize(res, new JsonSerializerOptions { WriteIndented = true }));
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(outPath)}");
}
```

Le programme **effectue l’OCR sur des PNG** en masse, en écrivant un fichier JSON correspondant pour chaque image.

## Conclusion

Vous venez d’apprendre comment **reconnaître du texte à partir d'une image** en C# avec Aspose OCR, **charger l’image pour l’OCR**, **extraire du texte à partir d'une image**, et **écrire un fichier JSON en C#** pour stocker les résultats. L’exemple complet et exécutable couvre les étapes essentielles, explique pourquoi chaque partie est importante, et montre même comment gérer les particularités des PNG.

Et après ? Essayez d’alimenter le JSON dans un index de recherche, combinez‑le avec une détection de langue, ou intégrez‑le dans une API web qui traite les téléchargements à la volée. Vous pouvez également explorer le support d’Aspose pour la reconnaissance d’écriture manuscrite si votre cas d’usage le nécessite.

Des questions sur les cas limites ou l’optimisation des performances ? Laissez un commentaire ci‑dessous—bon codage !

![démo de reconnaissance de texte à partir d'une image](/images/ocr-demo.png "Diagramme montrant comment Aspose OCR reconnaît le texte à partir d'une image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}