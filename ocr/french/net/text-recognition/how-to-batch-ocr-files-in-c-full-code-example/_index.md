---
category: general
date: 2026-02-17
description: Comment effectuer une OCR en lot sur plusieurs PDF et images en C# avec
  Aspose OCR. Apprenez à extraire le texte d’un PDF, à convertir un PDF en texte et
  à reconnaître le texte à partir d’images.
draft: false
keywords:
- how to batch OCR
- extract text from pdf
- convert pdf to text
- recognize text from images
- extract text scanned pdf
language: fr
og_description: Comment effectuer une OCR par lots de plusieurs documents en C# avec
  Aspose OCR. Obtenez du code étape par étape pour extraire le texte d’un PDF, convertir
  le PDF en texte et reconnaître le texte à partir d’images.
og_title: Comment traiter par lots des fichiers OCR en C# – Guide complet
tags:
- OCR
- C#
- Aspose
- PDF
- Text Extraction
title: Comment traiter par lots des fichiers OCR en C# – Exemple complet de code
url: /fr/net/text-recognition/how-to-batch-ocr-files-in-c-full-code-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots de fichiers en C# – Guide complet

Vous êtes-vous déjà demandé **comment faire une OCR par lots** d’une pile de PDF et de scans d’images sans écrire une boucle séparée pour chaque fichier ? Vous n’êtes pas seul. La plupart des développeurs rencontrent ce problème lorsqu’ils doivent extraire du texte de dizaines de pages en une seule fois. Bonne nouvelle ? Avec Aspose OCR, vous pouvez fournir une collection de fichiers à un seul moteur et le laisser faire le travail lourd.  

Dans ce tutoriel, nous allons parcourir une solution pratique qui vous permet **d’extraire du texte d’un pdf**, **de convertir un pdf en texte**, et **de reconnaître du texte à partir d’images** en une exécution batch. À la fin, vous disposerez d’une application console prête à l’emploi qui affiche le résultat OCR pour chaque page, et vous comprendrez le pourquoi de chaque étape afin de pouvoir l’adapter à vos propres projets.

## Prérequis – Ce dont vous avez besoin avant de commencer

- **.NET 6.0 ou version ultérieure** (le code fonctionne également avec .NET Framework, mais .NET 6+ est recommandé)
- **Package NuGet Aspose.OCR** – installez‑le avec `dotnet add package Aspose.OCR`
- Quelques fichiers d’exemple : un PDF multipage (`doc1.pdf`) et un TIFF scanné (`doc2.tif`). Placez‑les dans un dossier que vous pouvez référencer, par ex. `C:\OCRSamples`.
- Connaissances de base en C# – vous devez être à l’aise avec les instructions `using` et les collections.

> Astuce : Si vous n’avez pas de licence, Aspose propose une clé temporaire gratuite qui supprime la limite de 100 pages pendant le développement.

## Étape 1 : Configurer le projet et importer les espaces de noms

Tout d’abord, créez un nouveau projet console (ou ajoutez‑le à un existant) et importez les espaces de noms requis.

```csharp
// Program.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;          // Aspose OCR core library
using Aspose.OCR.Image;   // ImageStream helper class
```

> **Pourquoi c’est important :** L’importation de `Aspose.OCR.Image` vous donne la méthode pratique `ImageStream.FromFile`, qui découpe automatiquement les pages PDF en flux d’images distincts. C’est la sauce secrète qui rend le traitement par lots indolore.

## Étape 2 : Initialiser le moteur OCR

Le moteur est le cheval de bataille qui communique avec le moteur OCR sous‑jacent. Vous n’avez besoin que d’une seule instance pour l’ensemble du batch.

```csharp
// Step 2: Create a single OcrEngine instance
OcrEngine ocrEngine = new OcrEngine();
```

> **Explication :** Réutiliser le même `OcrEngine` réduit le turnover mémoire et accélère le traitement parce que les bibliothèques natives restent chargées entre les pages.

## Étape 3 : Construire une liste de flux d’images

Ici nous rassemblons chaque document que nous voulons traiter. `ImageStream.FromFile` est assez intelligent pour découper un PDF en pages individuelles, de sorte qu’un PDF de trois pages devienne trois flux séparés en coulisses.

```csharp
// Step 3: Assemble the collection of image streams
List<ImageStream> imageStreams = new List<ImageStream>
{
    ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
    ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
};
```

> **Cas limite :** Si vous avez un mélange de PDF, TIFF, JPEG ou PNG, ajoutez‑les simplement à la même liste – Aspose gère automatiquement la détection du format.

## Étape 4 : Exécuter l’opération OCR par lots

Nous transmettons maintenant la liste au moteur. `RecognizeBatch` renvoie une collection d’objets `OcrResult`, un par page.

```csharp
// Step 4: Perform batch OCR on the supplied streams
IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

> **Pourquoi le batch ?** Exécuter l’OCR page par page dans une boucle manuelle oblige le moteur à se réinitialiser à chaque fois, ce qui peut doubler le temps de traitement. `RecognizeBatch` garde le moteur « chaud » et renvoie les résultats au fur et à mesure qu’ils sont disponibles.

## Étape 5 : Afficher le texte reconnu

Enfin, nous parcourons les résultats et écrivons le texte de chaque page dans la console. C’est à ce moment‑ci que vous pouvez remplacer `Console.WriteLine` par des écritures dans des fichiers, des insertions en base de données, ou toute autre action en aval.

```csharp
// Step 5: Display the OCR output for each page
for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResults[pageIndex].Text);
}
```

### Sortie console attendue

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore...
--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Si vous exécutez le programme avec les fichiers d’exemple, vous devriez voir un bloc de texte pour chaque page, prouvant que vous avez bien **extrait le texte d’un pdf scanné** en un seul passage.

## Gestion des problèmes courants

| Problème | Pourquoi cela se produit | Solution rapide |
|----------|--------------------------|-----------------|
| **Erreurs de mémoire insuffisante** | Les PDF volumineux génèrent de nombreuses images haute résolution. | Limitez le DPI lors du chargement des PDF : `ocrEngine.Settings.ImageDpi = 200;` |
| **Caractères parasites** | Le scan source est de mauvaise qualité ou utilise une langue non prise en charge. | Définissez explicitement la langue : `ocrEngine.Language = Language.English;` |
| **Résultats partiels** | La liste batch contient un fichier corrompu. | Enveloppez `RecognizeBatch` dans un try/catch et consignez `e.Message` pour le fichier fautif. |
| **Goulot d’étranglement de performance** | Exécution sur un seul thread alors que la machine possède plusieurs cœurs. | Utilisez `Parallel.ForEach` avec des instances séparées de `OcrEngine` par thread (avancé). |

## Bonus : Enregistrer les résultats OCR dans des fichiers texte

Si vous préférez conserver un fichier `.txt` séparé par page, ajoutez simplement un petit bloc d’écriture à l’intérieur de la boucle :

```csharp
string outputPath = @"C:\OCRResults";
System.IO.Directory.CreateDirectory(outputPath);

for (int i = 0; i < ocrResults.Count; i++)
{
    string fileName = System.IO.Path.Combine(outputPath, $"Page_{i + 1}.txt");
    System.IO.File.WriteAllText(fileName, ocrResults[i].Text);
}
```

Vous avez ainsi transformé **convert pdf to text** en un dossier ordonné de fichiers texte brut—parfait pour l’indexation ou la recherche en aval.

## Exemple complet fonctionnel

Voici le programme complet, prêt à copier‑coller. Aucun dépendance cachée, aucun script externe.

```csharp
// FullProgram.cs
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Image;

class Program
{
    static void Main()
    {
        // Initialise OCR engine (reuse for the whole batch)
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: tweak settings for speed or accuracy
        ocrEngine.Settings.ImageDpi = 200;          // lower memory usage
        ocrEngine.Language = Language.English;     // set language explicitly

        // Build the list of image streams (PDF pages auto‑split)
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"C:\OCRSamples\doc1.pdf"),
            ImageStream.FromFile(@"C:\OCRSamples\doc2.tif")
        };

        // Perform batch OCR
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Output each page's text to console
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
        }

        // (Optional) Save each page to a .txt file
        string outputFolder = @"C:\OCRResults";
        System.IO.Directory.CreateDirectory(outputFolder);
        for (int i = 0; i < ocrResults.Count; i++)
        {
            string txtPath = System.IO.Path.Combine(outputFolder, $"Page_{i + 1}.txt");
            System.IO.File.WriteAllText(txtPath, ocrResults[i].Text);
        }
    }
}
```

Exécutez `dotnet run` depuis le dossier du projet et observez la console se remplir du texte extrait. C’est **comment faire une OCR par lots** d’une collection de documents en quelques lignes de C#.

## Ce que nous avons couvert – Récapitulatif rapide

- Configuration d’une application console .NET et installation d’Aspose.OCR.  
- Création d’une seule instance `OcrEngine` pour garder le processus efficace.  
- Construction d’une liste d’objets `ImageStream` qui découpent automatiquement les PDF en pages.  
- Exécution de `RecognizeBatch` pour **extraire du texte d’un pdf** et d’autres formats d’image en une seule passe.  
- Affichage des résultats et sauvegarde optionnelle en fichiers `.txt` individuels, complétant le workflow **convert pdf to text**.  

## Prochaines étapes et sujets associés

- **Montée en échelle** : Utilisez `Parallel.ForEach` avec un pool d’objets `OcrEngine` pour traiter des centaines de fichiers en parallèle.  
- **Packs de langues** : Remplacez `Language.English` par `Language.French` ou chargez un dictionnaire personnalisé lorsque vous devez **reconnaître du texte à partir d’images** dans d’autres langues.  
- **Post‑traitement** : Faites passer la sortie OCR dans un correcteur orthographique ou un analyseur de langage naturel pour améliorer la précision des contrats scannés.  
- **Bibliothèques alternatives** : Comparez Aspose OCR avec Tesseract.NET si vous cherchez une option open‑source—les deux peuvent **extraire du texte d’un pdf scanné** mais diffèrent au niveau de la licence et de la précision prête à l’emploi.

---

![how to batch OCR example](alt="how to batch OCR example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}