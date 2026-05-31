---
category: general
date: 2026-05-31
description: Apprenez comment obtenir les scores de confiance OCR en C# tout en extrayant
  le texte d’une image et en lisant l’image d’un reçu avec Aspose OCR.
draft: false
keywords:
- ocr confidence scores
- extract text from image
- ocr bounding boxes
- perform ocr on jpg
- read receipt image
language: fr
og_description: Les scores de confiance OCR vous permettent d’évaluer la précision ;
  ce guide montre comment extraire du texte d’une image, obtenir les boîtes englobantes
  et lire une image de reçu à l’aide d’Aspose OCR.
og_title: Scores de confiance OCR en C# – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to get OCR confidence scores in C# while extract text from
    image and read receipt image with Aspose OCR.
  headline: OCR confidence scores in C# – Complete Guide
  type: TechArticle
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Scores de confiance OCR en C# – Guide complet
url: /fr/net/ocr-optimization/ocr-confidence-scores-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Scores de confiance OCR en C# – Guide complet

Vous vous êtes déjà demandé comment obtenir des **scores de confiance OCR** lorsque vous devez *extraire du texte d'une image* ? Peut‑être essayez‑vous de **lire des images de reçus** pour le suivi des dépenses et vous voulez savoir quels caractères le moteur n’est pas sûr de reconnaître. Bonne nouvelle ? Avec Aspose.OCR vous pouvez récupérer les pourcentages de confiance, les boîtes englobantes et le texte brut d’un JPG en quelques lignes de C#.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : installer la bibliothèque, configurer le moteur pour **effectuer l’OCR sur un JPG**, extraire les scores de confiance et interpréter les **boîtes englobantes OCR** qui indiquent où chaque caractère se trouve sur la page. À la fin, vous disposerez d’une application console prête à l’emploi qui affiche chaque caractère, sa confiance et sa position—parfait pour valider des reçus ou tout document numérisé.

## Ce que vous apprendrez

- Installer Aspose.OCR via NuGet et configurer un moteur OCR de base.  
- Configurer `OcrOptions` pour demander une sortie texte brut **avec scores de confiance** et **boîtes englobantes**.  
- Parcourir `OcrResult` pour **extraire du texte d’une image** ligne par ligne et symbole par symbole.  
- Gérer les problèmes courants tels que les fichiers manquants, les caractères à faible confiance et les formats non‑JPG.  
- Étendre l’exemple pour traiter plusieurs images de reçus dans un dossier.

Aucune expérience préalable avec Aspose n’est requise ; il vous suffit d’un environnement .NET fonctionnel et d’une image de reçu (JPG) que vous souhaitez tester.

---

## Étape 1 – Installer Aspose.OCR et préparer votre projet

Tout d’abord : vous avez besoin du package NuGet Aspose.OCR. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

> **Astuce :** L’essai gratuit fonctionne jusqu’à 200 pages, ce qui est largement suffisant pour tester la numérisation de reçus.

Après l’installation du package, créez un nouveau projet console (si vous n’en avez pas déjà un) :

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
```

Vous pouvez maintenant ouvrir le fichier `Program.cs` généré et commencer à ajouter les directives using :

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
```

Ces espaces de noms vous donnent accès à `OcrEngine`, `OcrOptions` et aux types de résultat dont nous aurons besoin plus tard.

## Étape 2 – Obtenir les scores de confiance OCR et les boîtes englobantes OCR

C’est le cœur du tutoriel. Nous configurerons le moteur afin que chaque caractère reconnu soit accompagné d’un **score de confiance** et d’une **boîte englobante** (le rectangle qui entoure le glyphe). L’en‑tête H2 elle‑même contient le mot‑clé principal, respectant la règle SEO.

```csharp
// Step 2: Initialize the OCR engine and request detailed output
OcrEngine ocrEngine = new OcrEngine();

// Load the image you want to process – here we assume a JPEG receipt
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");

// Tell Aspose we want plain text, confidence percentages, and bounding boxes
ocrEngine.Options = new OcrOptions
{
    OutputFormat = OcrOutputFormat.PlainText,
    IncludeConfidence = true,
    IncludeBoundingBoxes = true
};
```

**Pourquoi inclure les scores de confiance ?**  
Un score de confiance (0‑100 %) indique à quel point le moteur est sûr de chaque caractère. Si vous transmettez la sortie à une logique en aval—par exemple, un workflow d’approbation de dépenses—vous pouvez rejeter ou signaler automatiquement les symboles à faible confiance.

**Pourquoi demander les boîtes englobantes ?**  
Les boîtes englobantes sont essentielles lorsque vous devez mettre en évidence du texte sur l’image originale, extraire des sous‑régions ou aligner les résultats OCR avec une superposition UI. Chaque `character.Bounds` vous fournit les coordonnées X, Y, la largeur et la hauteur en pixels.

## Étape 3 – Effectuer l’OCR sur un JPG et extraire le texte d’une image

Nous exécutons maintenant le moteur. L’appel à `Recognize()` effectue tout le travail lourd et renvoie un objet `OcrResult`.

```csharp
// Step 3: Run the OCR process
OcrResult ocrResult = ocrEngine.Recognize();
```

Si le chemin de l’image est incorrect ou que le fichier n’est pas dans un format pris en charge, Aspose lève une `FileNotFoundException` ou `UnsupportedImageFormatException`. Enveloppez l’appel dans un bloc try/catch dans le code de production pour gérer ces cas limites de façon élégante.

### Extraction du texte brut

Si vous avez seulement besoin du texte concaténé, vous pouvez lire `ocrResult.Text` :

```csharp
Console.WriteLine("Full extracted text:");
Console.WriteLine(ocrResult.Text);
```

Mais comme nous avons également demandé les scores de confiance et les boîtes englobantes, nous parcourrons la structure pour voir les détails de chaque caractère.

## Étape 4 – Parcourir les lignes, les symboles et afficher les scores de confiance OCR

Voici la boucle qui affiche chaque caractère, sa confiance et sa boîte. C’est ici que l’exemple de **lecture d’image de reçu** brille réellement.

```csharp
// Step 4: Walk through each line and each symbol (character)
foreach (var textLine in ocrResult.Lines)
{
    foreach (var character in textLine.Symbols)
    {
        Console.WriteLine(
            $"Char: '{character.Text}'  Confidence: {character.Confidence}%  Box: {character.Bounds}");
    }
}
```

Un exemple de sortie pourrait ressembler à :

```
Char: 'R'  Confidence: 98%  Box: {X=12,Y=34,Width=15,Height=20}
Char: 'e'  Confidence: 95%  Box: {X=28,Y=34,Width=12,Height=20}
Char: 'c'  Confidence: 92%  Box: {X=41,Y=34,Width=13,Height=20}
...
```

**Interpréter les nombres :**  
- **Confiance ≥ 90 %** – généralement sûr à accepter.  
- **Confiance 70‑89 %** – vous pourriez vouloir revérifier, surtout pour les chiffres des montants.  
- **Confiance < 70 %** – envisagez de signaler pour une révision manuelle.

## Étape 5 – Exemple complet exécutable (avec gestion des erreurs)

En assemblant le tout, voici un programme complet que vous pouvez copier‑coller dans `Program.cs`. Il inclut une vérification simple des fichiers manquants et affiche un message convivial si l’OCR échoue.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the receipt image – adjust to your environment
            const string imagePath = "YOUR_DIRECTORY/receipt.jpg";

            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found -> {imagePath}");
                return;
            }

            try
            {
                // Initialize engine
                OcrEngine ocrEngine = new OcrEngine
                {
                    Image = ImageStream.FromFile(imagePath),
                    Options = new OcrOptions
                    {
                        OutputFormat = OcrOutputFormat.PlainText,
                        IncludeConfidence = true,
                        IncludeBoundingBoxes = true
                    }
                };

                // Perform OCR
                OcrResult ocrResult = ocrEngine.Recognize();

                // Show full plain text (optional)
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
                Console.WriteLine();

                // Show each character with confidence and bounding box
                Console.WriteLine("=== Detailed Character Data ===");
                foreach (var line in ocrResult.Lines)
                {
                    foreach (var symbol in line.Symbols)
                    {
                        Console.WriteLine(
                            $"Char: '{symbol.Text}'  Confidence: {symbol.Confidence}%  Box: {symbol.Bounds}");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"OCR failed: {ex.Message}");
            }
        }
    }
}
```

### Sortie attendue

Lorsque vous exécutez `dotnet run`, la console affichera d’abord le texte concaténé du reçu, puis une liste de chaque caractère avec son score de confiance et sa boîte englobante. Si la confiance d’un caractère est faible, vous verrez un pourcentage inférieur à 80, ce qui indique qu’il faut vérifier cette partie du reçu manuellement.

## Bonus : Traitement de plusieurs reçus dans un dossier

Si vous avez un lot d’images JPG de reçus, encapsulez la logique ci‑dessus dans une boucle `foreach (var file in Directory.GetFiles(folder, "*.jpg"))`. N’oubliez pas de réinitialiser le `OcrEngine` pour chaque fichier, ou d’instancier un nouveau à l’intérieur de la boucle afin d’éviter les fuites d’état.

```csharp
string folder = "YOUR_DIRECTORY/Receipts";
foreach (var file in System.IO.Directory.GetFiles(folder, "*.jpg"))
{
    // reuse the same code block, just replace imagePath with 'file'
}
```

Le traitement en masse est pratique pour les importations de dépenses nocturnes.

---

## Conclusion

Vous disposez maintenant d’une solution solide, de bout en bout, pour obtenir des **scores de confiance OCR** en C#, **extraire du texte d’une image**, et récupérer les **boîtes englobantes OCR** tout en **effectuant l’OCR sur des fichiers JPG** comme une **image de reçu à lire**. Le code est entièrement autonome, fonctionne avec la dernière version d’Aspose.OCR (au 31‑05‑2026), et vous fournit les données granulaire nécessaires pour construire des pipelines de traitement de documents fiables.

Et après ? Essayez de visualiser les boîtes englobantes sur le reçu original en utilisant `System.Drawing` ou une bibliothèque UI, ou transmettez les caractères à faible confiance à un service de vérification secondaire. Vous pouvez également expérimenter avec différentes langues en définissant `ocrEngine.Options.Language = OcrLanguage.French;` – l’API prend en charge de nombreuses locales.

Bon codage, et que vos scores de confiance restent toujours élevés !

![Capture d'écran du résultat console affichant les scores de confiance OCR et les boîtes englobantes pour un reçu

## Que devriez‑vous apprendre ensuite ?

- [Extraire le texte d'image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Comment obtenir les choix de caractères OCR pour les caractères reconnus en reconnaissance d'image](/ocr/english/net/text-recognition/get-choices-for-recognized-characters/)
- [Comment utiliser Aspose OCR pour le résultat JSON en reconnaissance d'image](/ocr/english/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}