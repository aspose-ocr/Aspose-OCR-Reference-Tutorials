---
category: general
date: 2026-09-06
description: Conversion d'image OCR en JSON en C# avec Aspose.OCR – guide étape par
  étape pour extraire le texte d’une image et obtenir une sortie JSON.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- ocr image to json
- extract text from image
- convert image to text
- recognize text from photo
- load image for ocr
language: fr
lastmod: 2026-09-06
og_description: OCR d'image en JSON en C# avec Aspose.OCR. Apprenez comment charger
  une image pour l'OCR, reconnaître le texte d'une photo et convertir le résultat
  en JSON.
og_image_alt: Screenshot of C# code that converts an OCR image to JSON using Aspose.OCR
og_title: Convertir une image OCR en JSON en C# – guide complet d'Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-09-06'
  description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  headline: How to convert an OCR image to JSON in C# with Aspose.OCR
  type: TechArticle
- description: ocr image to json conversion in C# using Aspose.OCR – step‑by‑step
    guide to extract text from image and get JSON output.
  name: How to convert an OCR image to JSON in C# with Aspose.OCR
  steps:
  - name: Place an image named `input.jpg` in the project root.
    text: Place an image named `input.jpg` in the project root.
  - name: Execute `dotnet run`.
    text: Execute `dotnet run`.
  - name: Observe the console output and open `output.json` to see the structured
      data.
    text: Observe the console output and open `output.json` to see the structured
      data.
  type: HowTo
- questions:
  - answer: Yes. Use `ocrEngine.SaveJson(Stream)` to write directly to a `MemoryStream`,
      then call `stream.ToArray()`.
    question: Can I get the OCR result as a byte array instead of a file?
  - answer: Aspose.OCR can accept PDF pages converted to images via Aspose.PDF, but
      the OCR engine itself works on raster images. Convert PDFs to images first,
      then **load image for ocr**.
    question: Does the engine support PDF input?
  - answer: 'Set `ocrEngine.Language = OcrLanguage.Arabic`. The JSON includes the
      correct text direction, which you can render in UI frameworks that support RTL.
      ## Conclusion You now have a complete solution for **ocr image to json** in
      C#. By loading an image, configuring the language, running the OCR engine, '
    question: How do I handle right‑to‑left scripts like Arabic?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- JSON
- Image processing
title: Comment convertir une image OCR en JSON en C# avec Aspose.OCR
url: /fr/net/text-recognition/how-to-convert-an-ocr-image-to-json-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment convertir une image OCR en JSON en C# avec Aspose.OCR

Si vous devez **ocr image to json** dans une application .NET, ce guide vous montre comment le faire avec Aspose.OCR. Nous parcourrons le chargement d’une image pour l’OCR, la reconnaissance de texte à partir d’une photo, et la conversion du résultat en JSON afin que vous puissiez consommer les données dans des API ou des bases de données.

Extraire du texte à partir de fichiers image est une exigence courante pour le traitement de factures, la numérisation de reçus et les projets d’archivage. À la fin de ce tutoriel, vous serez capable de **convert image to text**, récupérer le résultat en texte brut, et générer une charge JSON structurée qui préserve les informations de mise en page.

## Prérequis

- SDK .NET 6.0 ou version ultérieure installé  
- Visual Studio 2022 (ou tout éditeur supportant .NET)  
- Un package NuGet Aspose.OCR (`Aspose.OCR`) ajouté à votre projet  
- Une image d’exemple (`input.jpg`) placée dans un dossier que vous pouvez référencer depuis le code  

Vous n’avez besoin d’aucun moteur OCR supplémentaire ; Aspose.OCR gère la lourde tâche en interne.

## Étape 1 : Installer le package NuGet Aspose.OCR

Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Le package inclut la classe `Aspose.OCR.OcrEngine`, qui fournit des méthodes pour **load image for ocr**, la sélection de la langue et l’exportation du résultat.

## Étape 2 : Créer un nouveau projet console C#

Si vous n’avez pas encore de projet, créez‑en un :

```bash
dotnet new console -n OcrToJsonDemo
cd OcrToJsonDemo
```

Ajoutez les directives `using` dont vous aurez besoin :

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;
```

## Étape 3 : Charger l’image et configurer le moteur OCR

Le code suivant montre comment **load image for ocr**, définir la langue et préparer le moteur pour le traitement. Dans cet exemple nous utilisons le cyrillique, mais vous pouvez passer à `OcrLanguage.English`, `OcrLanguage.French`, etc., selon la langue source.

```csharp
// Step 3: Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Choose the language that matches the text in the image.
// Replace OcrLanguage.Cyrillic with the language you need.
ocrEngine.Language = OcrLanguage.Cyrillic;

// Load the image file. The ImageStream class abstracts file, stream, or byte[] sources.
string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
ocrEngine.Image = ImageStream.FromFile(imagePath);
```

> **Pourquoi c’est important :** Définir la langue correcte améliore considérablement la précision lorsque vous **recognize text from photo**. Le moteur utilise des dictionnaires et jeux de caractères spécifiques à chaque langue.

## Étape 4 : Exécuter le processus OCR et récupérer les résultats

Exécutez maintenant le moteur OCR. Si le processus réussit, vous pouvez **extract text from image** en texte brut, HTML ou JSON. Aspose.OCR fournit une méthode `SaveJson` qui écrit le résultat structuré dans un fichier.

```csharp
// Step 4: Execute the OCR process
if (ocrEngine.Process())
{
    // Plain‑text output
    string plainText = ocrEngine.Text;
    Console.WriteLine("=== Plain Text ===");
    Console.WriteLine(plainText);

    // JSON output – includes bounding boxes, confidence scores, and line information
    string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
    ocrEngine.SaveJson(jsonPath);
    Console.WriteLine($"\nJSON result saved to: {jsonPath}");
}
else
{
    Console.WriteLine("OCR processing failed. Check the image path and format.");
}
```

### Structure JSON attendue

Un fichier `output.json` typique ressemble à ceci (formaté pour la lisibilité) :

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Text": "Пример текста",
          "Confidence": 0.96,
          "Rect": { "X": 45, "Y": 120, "Width": 210, "Height": 30 }
        },
        {
          "Text": "Еще одна строка",
          "Confidence": 0.93,
          "Rect": { "X": 45, "Y": 160, "Width": 230, "Height": 28 }
        }
      ]
    }
  ]
}
```

La charge JSON contient le texte de chaque ligne, un score de confiance, et le rectangle qui englobe la ligne dans la photo originale. Cela facilite le mappage du résultat OCR aux éléments d’interface utilisateur ou aux champs de base de données.

## Étape 5 : Code source complet pour la démo

Ci‑dessous se trouve le programme complet, prêt à l’exécution, qui réalise le flux de travail **ocr image to json**. Copiez‑le dans `Program.cs` et exécutez `dotnet run`.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrToJsonDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Select the language (Cyrillic in this example)
            ocrEngine.Language = OcrLanguage.Cyrillic;

            // 3️⃣ Load the image you want to process
            string imagePath = Path.Combine(Environment.CurrentDirectory, "input.jpg");
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found: {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Run the OCR process
            if (ocrEngine.Process())
            {
                // 5️⃣ Retrieve plain text (optional)
                string plainText = ocrEngine.Text;
                Console.WriteLine("=== Plain Text ===");
                Console.WriteLine(plainText);

                // 6️⃣ Save the result as JSON
                string jsonPath = Path.Combine(Environment.CurrentDirectory, "output.json");
                ocrEngine.SaveJson(jsonPath);
                Console.WriteLine($"\nJSON result saved to: {jsonPath}");
            }
            else
            {
                Console.WriteLine("OCR processing failed. Verify the image format and language settings.");
            }
        }
    }
}
```

### Exécution de l’exemple

1. Placez une image nommée `input.jpg` à la racine du projet.  
2. Exécutez `dotnet run`.  
3. Observez la sortie console et ouvrez `output.json` pour voir les données structurées.

## Astuces professionnelles et pièges courants

| Situation | Recommendation |
|-----------|----------------|
| **Photos basse résolution** | Augmentez le DPI avant le traitement ou utilisez `ocrEngine.Image = ImageStream.FromFile(path, 300)` pour forcer 300 DPI. |
| **Langues mixtes** | Définissez `ocrEngine.Language = OcrLanguage.Multilingual` et, éventuellement, fournissez une liste de langues via `ocrEngine.Language = new[] { OcrLanguage.English, OcrLanguage.Cyrillic }`. |
| **Documents volumineux** | Traitez une page à la fois pour limiter l’utilisation de la mémoire ; le moteur prend en charge les TIFF multi‑pages. |
| **Caractères incorrects** | Vérifiez que le `OcrLanguage` correct est sélectionné ; utiliser la mauvaise langue réduit la précision lorsque vous **convert image to text**. |
| **Champs JSON manquants** | Assurez‑vous d’utiliser la version 23.6 ou ultérieure d’Aspose.OCR ; les versions antérieures n’exposaient pas la méthode `SaveJson`. |

## Questions fréquentes

**Q : Puis‑je obtenir le résultat OCR sous forme de tableau d’octets au lieu d’un fichier ?**  
R : Oui. Utilisez `ocrEngine.SaveJson(Stream)` pour écrire directement dans un `MemoryStream`, puis appelez `stream.ToArray()`.

**Q : Le moteur prend‑il en charge les entrées PDF ?**  
R : Aspose.OCR peut accepter des pages PDF converties en images via Aspose.PDF, mais le moteur OCR lui‑même fonctionne sur des images raster. Convertissez d’abord les PDF en images, puis **load image for ocr**.

**Q : Comment gérer les scripts de droite à gauche comme l’arabe ?**  
R : Définissez `ocrEngine.Language = OcrLanguage.Arabic`. Le JSON inclut la bonne direction du texte, que vous pouvez rendre dans les frameworks UI qui supportent le RTL.

## Conclusion

Vous disposez maintenant d’une solution complète pour **ocr image to json** en C#. En chargeant une image, en configurant la langue, en exécutant le moteur OCR et en exportant le résultat en JSON, vous pouvez **extract text from image**, **convert image to text**, et **recognize text from photo** dans un flux de travail unique et simplifié.  

À partir d’ici, vous pourriez explorer :

- Intégrer la sortie JSON à une API Web (`ASP.NET Core`)  
- Stocker le résultat dans une base de données NoSQL comme MongoDB  
- Ajouter un post‑traitement pour corriger les erreurs OCR courantes  

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d’API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [reconnaître du texte à partir d’une image en C# – Guide complet de l’OCR et du JSON](/ocr/english/net/text-recognition/recognize-text-from-image-in-c-complete-guide-to-ocr-and-jso/)
- [Convertir une image en texte en C# avec Aspose OCR – Guide étape par étape](/ocr/english/net/text-recognition/convert-image-to-text-in-c-with-aspose-ocr-step-by-step-guid/)
- [Comment extraire du texte d’une image avec Aspose.OCR pour .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}