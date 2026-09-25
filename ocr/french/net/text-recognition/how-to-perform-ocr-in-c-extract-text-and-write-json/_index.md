---
category: general
date: 2026-02-09
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) en
  C# pour extraire du texte d’une image, reconnaître le texte d’un PNG et écrire rapidement
  un fichier JSON en C#.
draft: false
keywords:
- how to perform OCR
- extract text from image
- recognize text from png
- write json file c#
language: fr
og_description: Comment effectuer la reconnaissance optique de caractères (OCR) en
  C# ? Suivez ce guide étape par étape pour extraire du texte d’une image, reconnaître
  le texte d’un PNG et écrire un fichier JSON en C# efficacement.
og_title: Comment réaliser l'OCR en C# – Extraire le texte et écrire du JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: Comment réaliser de l'OCR en C# – Extraire le texte et générer du JSON
url: /fr/net/text-recognition/how-to-perform-ocr-in-c-extract-text-and-write-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR en C# – Guide complet

Effectuer de l'OCR en C# est un obstacle fréquent lorsque vous devez **extraire du texte d'une image**. Dans ce guide, nous parcourrons la reconnaissance de texte à partir d'un PNG, l'exportation du résultat détaillé vers une chaîne JSON, et enfin **write JSON file C#**. Vous êtes-vous déjà retrouvé devant un formulaire numérisé en vous demandant comment transformer ces gribouillis en texte recherchable ? Vous n'êtes pas seul ; de nombreux développeurs rencontrent ce problème dès le début.

Nous utiliserons la bibliothèque Aspose.OCR car elle fournit la confiance par symbole dès le départ et s'intègre parfaitement aux projets .NET 6+. À la fin de ce tutoriel, vous disposerez d’une application console prête à l’emploi qui charge un PNG, extrait chaque caractère et enregistre un fichier JSON propre que vous pourrez injecter dans une base de données ou un modèle d'IA. Pas de raccourcis mystérieux « voir la documentation »—juste une solution autonome.

## Ce dont vous aurez besoin

- **.NET 6 SDK** (ou version ultérieure) – la version LTS actuelle au moment de la rédaction.
- **Aspose.OCR for .NET** package NuGet – `Install-Package Aspose.OCR`.
- Une image PNG que vous souhaitez analyser (par ex., `form.png`).  
- Un IDE ou éditeur – Visual Studio, VS Code, Rider – ce qui vous convient.

C’est tout. Si vous avez ces éléments, vous êtes prêt à démarrer.

![Illustration de la réalisation d'OCR montrant une application console C# traitant un PNG](ocr-example.png "Comment réaliser l'OCR en C#")

*Texte alternatif de l'image : illustration de la réalisation d'OCR montrant une application console C# traitant un PNG.*

## Étape 1 : Configurer le projet et ajouter les dépendances

Tout d'abord, créez un nouveau projet console et ajoutez la bibliothèque Aspose OCR.

```csharp
// Create a new console app (run in terminal)
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo

// Add Aspose.OCR NuGet package
dotnet add package Aspose.OCR
```

> **Astuce :** Utilisez le drapeau `--framework net6.0` si vous souhaitez verrouiller explicitement le framework cible.

Pourquoi cette étape est importante : le package NuGet contient les classes `OcrEngine`, `ImageStream` et `JsonExporter` dont nous dépendrons. Sans cela, le compilateur n'aurait aucune idée de ce que signifie « OCR ».

## Étape 2 : Écrire la logique OCR principale

Ouvrez `Program.cs` (ou créez un nouveau fichier) et remplacez son contenu par ce qui suit. Chaque section est commentée afin que vous puissiez comprendre pourquoi elle est présente.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Export;
using System;

namespace OcrJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialize the OCR engine – this prepares the
            //    internal models and allocates native resources.
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣ Load the image you want to process.
            //    Replace the path with your own PNG file.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/form.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR recognition – the heavy lifting.
            //    The result includes text, per‑symbol confidence,
            //    and layout information.
            // -------------------------------------------------
            RecognitionResult ocrResult = ocrEngine.Recognize(image);

            // -------------------------------------------------
            // 4️⃣ Export the result to a JSON string.
            //    JsonExporter respects the confidence values.
            // -------------------------------------------------
            JsonExporter jsonExporter = new JsonExporter();
            string jsonContent = jsonExporter.ExportToString(ocrResult);

            // -------------------------------------------------
            // 5️⃣ Write the JSON to disk – this is how we
            //    **write JSON file C#** style.
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/form.json";
            System.IO.File.WriteAllText(jsonPath, jsonContent);

            // -------------------------------------------------
            // 6️⃣ Let the user know we succeeded.
            // -------------------------------------------------
            Console.WriteLine($"JSON file saved successfully at {jsonPath}");
        }
    }
}
```

### Pourquoi chaque élément est important

- **OcrEngine** : Considérez-le comme le cerveau de l'opération. Il charge les modèles de langue et configure le pipeline d'inférence.
- **ImageStream.FromFile** : Gère tout PNG, JPEG, BMP, etc. Il abstrait les particularités de l'E/S de fichiers.
- **RecognitionResult** : Contient le texte brut ainsi que les scores de confiance. C’est ici que vous obtenez les données granulaires nécessaires à la validation en aval.
- **JsonExporter** : Convertit le riche `RecognitionResult` en une charge JSON propre, parfaite pour les API.
- **File.WriteAllText** : La méthode .NET directe pour **write JSON file C#** sans dépendances supplémentaires.

## Étape 3 : Exécuter l'application et vérifier la sortie

Compilez et exécutez le programme :

```bash
dotnet run
```

Vous devriez voir un message console similaire à :

```
JSON file saved successfully at YOUR_DIRECTORY/form.json
```

Ouvrez `form.json` – vous trouverez quelque chose comme :

```json
{
  "Text": "Sample Form\nName: John Doe\nDate: 2026-02-09",
  "Symbols": [
    { "Char": "S", "Confidence": 0.99, "X": 12, "Y": 8 },
    { "Char": "a", "Confidence": 0.98, "X": 22, "Y": 8 },
    // … more symbols …
  ]
}
```

L'étape **extract text from image** a réussi, et vous disposez maintenant d’une représentation JSON lisible par machine de chaque caractère.

## Étape 4 : Gérer les cas limites courants

### Fichiers manquants ou corrompus

Si le chemin du PNG est incorrect, `ImageStream.FromFile` lève une `FileNotFoundException`. Enveloppez le code de chargement dans un bloc try‑catch :

```csharp
try
{
    ImageStream image = ImageStream.FromFile(imagePath);
}
catch (FileNotFoundException ex)
{
    Console.Error.WriteLine($"Could not find image: {ex.Message}");
    return;
}
```

### Scores de confiance faibles

Parfois, l'OCR renvoie une faible confiance pour des numérisations bruyantes. Vous pouvez filtrer les symboles avant l'exportation :

```csharp
ocrResult.Symbols.RemoveAll(s => s.Confidence < 0.6);
```

Cela garantit que le JSON ne contient que des caractères raisonnablement fiables—utile lorsque vous alimentez les données dans des pipelines de validation en aval.

### Fichiers volumineux & mémoire

Le traitement d'un PNG de plusieurs mégaoctets peut augmenter l'utilisation de la mémoire. Envisagez de diffuser l'image par morceaux ou d'utiliser `OcrEngine.RecognizeAsync` (disponible dans les versions plus récentes d'Aspose) pour garder l'interface réactive.

## Étape 5 : Étendre la solution (optionnel)

- **Batch processing** : Parcourez un répertoire de PNG et générez un JSON correspondant pour chaque fichier.
- **Database storage** : Insérez le JSON dans une colonne SQL `NVARCHAR(MAX)` pour des analyses ultérieures.
- **Language selection** : Définissez `ocrEngine.Language = OcrLanguage.Spanish;` si vous avez besoin d'un support non anglais.

Toutes ces extensions suivent le même modèle **how to perform OCR** que nous avons établi—initialiser, reconnaître, exporter et persister.

## Questions fréquentes

**Q : Cela fonctionne-t-il avec JPG ou TIFF ?**  
R : Absolument. `ImageStream.FromFile` détecte automatiquement le format, vous pouvez donc remplacer le PNG par n'importe quelle image raster prise en charge.

**Q : Et si je dois extraire du texte d'un PDF ?**  
R : Convertissez d'abord chaque page PDF en image (par ex., avec `Aspose.PDF`) puis alimentez le PNG dans le flux OCR décrit ici.

**Q : Puis-je obtenir le résultat OCR au format XML au lieu de JSON ?**  
R : Oui. Aspose.OCR propose également un `XmlExporter`. Remplacez `JsonExporter` par `XmlExporter` et ajustez l'extension du fichier.

## Conclusion

Nous avons parcouru **how to perform OCR** en C# du début à la fin, en vous montrant comment **extract text from image**, **recognize text from PNG**, et **write JSON file C#** sans accroc. L'exemple complet et exécutable se trouve dans les extraits de code ci‑dessus, et vous comprenez maintenant les raisons de chaque étape — initialiser le moteur, gérer les cas limites et persister les résultats.

Ensuite, vous pourriez explorer des pipelines OCR par lots, intégrer la sortie JSON avec Azure Cognitive Search, ou expérimenter des modèles de langue personnalisés. Le ciel est la limite une fois que vous avez maîtrisé les bases de l'OCR en C#.

Si vous avez rencontré des problèmes ou avez des idées pour d'autres extensions, laissez un commentaire ci‑dessous. Bon codage, et profitez de transformer ces scans pixelisés en données propres et recherchables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}