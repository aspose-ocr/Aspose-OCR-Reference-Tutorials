---
category: general
date: 2026-09-16
description: télécharger le modèle OCR et extraire le texte d’un PNG avec Aspose.OCR.
  Apprenez à convertir une image en texte et à lire le texte d’une image en C#.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- download OCR model
- extract text from PNG
- convert image to text
- recognize text from image
- read text from image
language: fr
lastmod: 2026-09-16
og_description: téléchargez le modèle OCR et extrayez le texte d’un PNG en C#. Ce
  tutoriel étape par étape montre comment convertir une image en texte et lire le
  texte d’une image en utilisant Aspose.OCR.
og_image_alt: Diagram showing OCR engine loading a model, processing a PNG, and outputting
  recognized text
og_title: Téléchargez le modèle OCR et extrayez le texte d’un PNG avec Aspose.OCR
  – Guide C#
schemas:
- author: Aspose
  dateModified: '2026-09-16'
  description: download OCR model and extract text from PNG with Aspose.OCR. Learn
    to convert image to text and read text from image in C#.
  headline: How to download OCR model and extract text from PNG using Aspose.OCR in
    C#
  type: TechArticle
tags:
- OCR
- Aspose.OCR
- C#
- image-processing
title: Comment télécharger le modèle OCR et extraire du texte d’un PNG avec Aspose.OCR
  en C#
url: /fr/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment télécharger le modèle OCR et extraire du texte d'un PNG avec Aspose.OCR en C#

Si vous devez **télécharger le modèle OCR** pour Aspose.OCR, ce guide vous montre comment **extraire du texte d'un PNG** rapidement et de manière fiable. Vous verrez comment **convertir une image en texte**, **reconnaître le texte à partir d'une image**, et enfin **lire le texte à partir d'une image** dans une application console C# propre.

Le tutoriel couvre tout ce dont vous avez besoin — de l'installation du SDK à la gestion des problèmes courants — afin que vous puissiez intégrer l'OCR dans n'importe quel projet .NET sans chercher d'autres ressources.

## Ce dont vous aurez besoin

| Pré-requis | Raison |
|------------|--------|
| .NET 6.0 SDK or later | Fournit le runtime pour l'application console |
| Visual Studio 2022 (or any IDE) | Facilite l'édition et le débogage |
| Aspose.OCR for .NET NuGet package | Fournit le moteur OCR et les modèles de langue |
| An image file (`input.png`) containing text | La source que vous allez **convertir l'image en texte** |

Vous pouvez ajouter le package Aspose.OCR via la console NuGet :

```bash
dotnet add package Aspose.OCR
```

> **Astuce :** La première fois que vous définissez la propriété `Language`, Aspose.OCR télécharge automatiquement les fichiers du **modèle OCR** dans le cache local de l'utilisateur. Aucun téléchargement manuel n'est requis.

## Comment télécharger le modèle OCR pour Aspose.OCR

Le moteur OCR n'est pas fourni avec les données de langue afin de garder la bibliothèque légère. Lorsque vous attribuez une langue (par ex., Cyrillic), le SDK vérifie le cache ; si le modèle est absent, il le télécharge depuis le CDN d'Aspose.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Models;   // contains Language enum
using System;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Select the required language model.
        // This triggers a download if the model is not present locally.
        ocrEngine.Language = Language.Cyrillic;
        Console.WriteLine("OCR model for Cyrillic is ready.");
```

Le `Console.WriteLine` confirme que l'étape de **téléchargement du modèle OCR** s'est terminée avec succès. Le téléchargement ne se produit qu'une fois par machine, après quoi le modèle mis en cache est réutilisé.

### Pourquoi le téléchargement automatique est important

* **Reduced bundle size** – Votre application reste petite car les packs de langue sont récupérés à la demande.  
* **Up‑to‑date accuracy** – Aspose met à jour les modèles régulièrement ; la dernière version est toujours récupérée.  
* **Simplified deployment** – Aucun besoin d'inclure de gros fichiers `.dat` avec votre installateur.

## Comment extraire du texte d'un PNG avec C#

Avec le modèle de langue prêt, l'étape suivante consiste à charger le fichier PNG que vous souhaitez traiter. Le PNG est sans perte, ce qui préserve la qualité des contours du texte et améliore la précision de la reconnaissance.

```csharp
        // Step 3: Load the image that contains the text.
        // ImageStream.FromFile reads the file into a stream compatible with Aspose.OCR.
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
        Console.WriteLine("Image loaded successfully.");
```

> **Cas particulier :** Si votre PNG utilise une palette de couleurs indexée, convertissez‑le en RGB 24 bits avant de le transmettre au moteur OCR afin d'éviter une mauvaise reconnaissance.

## Conversion d'image en texte : reconnaissance du texte à partir de l'image

Vous lancez maintenant le processus OCR. La méthode `Recognize` effectue tout le travail lourd — pré‑traitement, segmentation, classification des caractères et post‑traitement.

```csharp
        // Step 4: Run the OCR process.
        // Recognize returns an OcrResult object that holds the recognized text and confidence scores.
        OcrResult result = ocrEngine.Recognize();

        // Verify that the engine actually found text.
        if (result == null || string.IsNullOrWhiteSpace(result.Text))
        {
            Console.WriteLine("No text was recognized. Check image quality or language settings.");
            return;
        }
```

L'objet `result` contient non seulement la chaîne brute mais aussi des propriétés optionnelles telles que `ResultPage` (pour les images multipages) et `Confidence` (score de confiance global). Vous pouvez les utiliser pour une validation avancée ou un retour d'interface utilisateur.

## Lecture du texte à partir de l'image et gestion des résultats

Enfin, affichez ou enregistrez la chaîne reconnue. C’est l'étape de **lecture du texte à partir de l'image** qui complète le pipeline de conversion.

```csharp
        // Step 5: Retrieve and display the recognized text.
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);

        // Optional: Write the output to a .txt file for later processing.
        System.IO.File.WriteAllText("output.txt", result.Text);
        Console.WriteLine("Text saved to output.txt");
    }
}
```

**Sortie attendue** (exemple pour une image simple contenant « Hello World ») :

```
=== Recognized Text ===
Hello World
Text saved to output.txt
```

### Variations courantes

| Variation | Quand l'utiliser | Ajustement du code |
|-----------|------------------|--------------------|
| **English language** | La plupart des documents occidentaux | `ocrEngine.Language = Language.English;` |
| **Multiple languages** | Pages multilingues | `ocrEngine.Language = Language.English | Language.Russian;` |
| **Custom DPI scaling** | Scans à basse résolution | `ocrEngine.Image = ImageStream.FromFile(...).Resize(2.0);` |
| **PDF input** | Lorsque la source est une page PDF | Convertissez d'abord le PDF en image, puis transmettez le bitmap à `ocrEngine.Image`. |

## Exemple complet et exécutable

Voici le programme complet que vous pouvez copier, coller et exécuter. Remplacez `YOUR_DIRECTORY` par le chemin contenant `input.png`.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Models;
using System;

class Program
{
    static void Main()
    {
        // Create OCR engine instance (downloads model if needed)
        var ocrEngine = new OcrEngine();

        // Choose language – this triggers the automatic model download
        ocrEngine.Language = Language.Cyrillic;
        Console.WriteLine("OCR model for Cyrillic downloaded (if not cached).");

        // Load the PNG image containing the text
        ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
        Console.WriteLine("PNG image loaded.");

        // Perform OCR
        OcrResult result = ocrEngine.Recognize();

        // Validate result
        if (result == null || string.IsNullOrWhiteSpace(result.Text))
        {
            Console.WriteLine("No text recognized. Verify image quality or language settings.");
            return;
        }

        // Output the recognized text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);

        // Save to a file for further processing
        System.IO.File.WriteAllText("output.txt", result.Text);
        Console.WriteLine("Recognized text saved to output.txt");
    }
}
```

Run the program with:

```bash
dotnet run
```

Si tout est correctement configuré, la console affiche le texte extrait de `input.png` et l'écrit dans `output.txt`.

## Bonnes pratiques et dépannage

* **Image quality** – Visez au moins 300 dpi ; les images floues ou bruyantes réduisent le score de confiance.  
* **Language selection** – Correspond toujours à la langue du texte source. Une langue incorrecte entraîne une sortie illisible.  
* **Cache location** – Par défaut, Aspose stocke les modèles dans `%USERPROFILE%\.Aspose\Aspose.OCR`. Videz le dossier uniquement si vous devez forcer un nouveau téléchargement.  
* **Performance** – Pour le traitement par lots, réutilisez une seule instance de `OcrEngine` au lieu d'en créer une nouvelle pour chaque image.  
* **Error handling** – Enveloppez l'appel OCR dans un bloc try‑catch pour capturer les erreurs réseau lors du téléchargement du modèle.

## Conclusion

Vous savez maintenant comment **télécharger le modèle OCR**, **extraire du texte d'un PNG**, **convertir une image en texte**, **reconnaître le texte à partir d'une image**, et **lire le texte à partir d'une image** en utilisant Aspose.OCR en C#. L'exemple complet montre un flux prêt pour la production que vous pouvez étendre à la conversion PDF, au traitement multipage ou à l'intégration avec des pipelines d'analyse de texte en aval.

**Étapes suivantes**

* Explorez la **reconnaissance de texte manuscrit** en passant à `Language.EnglishHandwritten`.  
* Combinez l'OCR avec **Aspose.PDF** pour intégrer le texte extrait dans des PDF recherchables.  
* Expérimentez la **pré‑traitement d'image** (redressement, amélioration du contraste) pour améliorer la précision sur des scans de mauvaise qualité.

N'hésitez pas à adapter le code à vos propres projets, et bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image en C# – OCR hors ligne avec Aspose (Guide étape par étape)](/ocr/english/net/text-recognition/extract-text-from-image-in-c-offline-ocr-with-aspose-step-by/)
- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Comment extraire du texte d'une image en utilisant Aspose.OCR pour .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}