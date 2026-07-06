---
category: general
date: 2026-03-26
description: Comment réaliser une OCR par lots en C# facilite l'extraction de texte
  à partir de fichiers PNG. Suivez ce tutoriel pas à pas en C# OCR pour l'extraction
  de texte en lot avec Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: fr
og_description: Comment faire de l’OCR par lots en C# vous permet d’extraire rapidement
  du texte à partir de fichiers PNG. Ce guide vous accompagne à travers un tutoriel
  complet d’OCR en C# avec extraction de texte par lots.
og_title: Comment faire de l'OCR par lots en C# – Extraire le texte d'un PNG
tags:
- OCR
- C#
- Aspose
title: Comment effectuer une OCR par lots en C# – Extraire le texte d’un PNG
url: /fr/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR par lots en C# – Extraire du texte à partir de PNG

Vous vous êtes déjà demandé **comment faire de l'OCR par lots** sur une pile de captures d'écran sans écrire un programme séparé pour chaque fichier ? Vous n'êtes pas seul. Dans de nombreux projets, nous nous retrouvons avec des dizaines de PNG dont il faut extraire le texte, et le faire un par un est fastidieux.  

La bonne nouvelle ? Avec Aspose OCR, vous pouvez créer une petite application console C# qui traite toutes ces images en parallèle, vous offrant une **extraction de texte par lots** rapide et un jeu de résultats propre. Dans ce guide, nous parcourrons un **tutoriel OCR C#** complet, expliquerons pourquoi chaque élément est important, et vous montrerons exactement à quoi ressemble la sortie.

À la fin de cet article, vous serez capable de :

* Charger une liste de fichiers PNG (ou toute image prise en charge) en une seule fois.  
* Configurer un `OcrEngine` partagé afin que les paramètres restent cohérents sur l’ensemble du lot.  
* Exécuter la file de reconnaissance avec jusqu’à quatre travailleurs parallèles.  
* Récupérer le texte reconnu pour chaque page et l’imprimer dans la console.

Pas de magie, juste du code solide que vous pouvez intégrer dès aujourd’hui à votre solution.

## Ce dont vous aurez besoin

Avant de plonger, assurez-vous d'avoir :

* .NET 6 SDK (ou toute version récente de .NET).  
* Une licence Aspose OCR valide ou une clé d’évaluation temporaire.  
* Un dossier contenant les fichiers PNG que vous souhaitez traiter.  
* Visual Studio 2022 ou votre éditeur préféré.

C’est tout—aucun package NuGet supplémentaire au‑delà de `Aspose.OCR` et du standard `System.Collections.Generic`.

## Comment faire de l'OCR par lots – Configurer le projet

Tout d’abord, créez un nouveau projet console et ajoutez la bibliothèque Aspose OCR.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Une fois la restauration terminée, ouvrez **Program.cs** (ou créez un nouveau fichier) et ajoutez les directives `using` habituelles :

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Cette simple structure nous donne accès à `OcrEngine`, `RecognitionQueue` et aux classes d’assistance dont nous aurons besoin plus tard.

## Extraire du texte à partir de PNG – Préparer la liste d'images

Nous devons maintenant indiquer au programme **quels PNG** passer en OCR. La façon la plus directe est de construire une `List<string>` contenant des chemins absolus ou relatifs.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

Remplacez `YOUR_DIRECTORY` par le chemin réel du dossier. Si vous avez un ensemble dynamique, vous pouvez également utiliser `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` et alimenter la liste avec le résultat. L’essentiel est que **extraire du texte à partir de PNG** ne consiste qu’à fournir les bons noms de fichiers à la file.

![Flux d'OCR par lots](https://example.com/placeholder.png "Diagramme illustrant comment faire de l'OCR par lots sur une collection de fichiers PNG")

*Texte alternatif de l'image : diagramme du flux d'OCR par lots*

## Tutoriel OCR C# – Configurer la file de reconnaissance

Le cœur de l’opération par lots est le `RecognitionQueue`. Pensez‑y comme à un tapis roulant qui transmet chaque image à un `OcrEngine` partagé. En partageant le moteur, nous maintenons une faible consommation de mémoire et garantissons des paramètres identiques pour chaque page.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

Pourquoi définir `MaxDegreeOfParallelism` à 4 ? Sur un ordinateur portable quad‑core typique, cela offre le meilleur débit sans affamer le système d’exploitation. Si vous exécutez sur un serveur avec plus de cœurs, augmentez le nombre en conséquence.

### Astuce pro

Si vous avez besoin de packs de langues personnalisés, de réglages DPI ou de recadrage de région d’intérêt, faites‑le **une seule fois** sur le `Engine` partagé avant d’enfiler les images. Par exemple :

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Toutes les reconnaissances suivantes héritent automatiquement de ces options—c’est l’essence de **comment créer l'OCR** de pipelines qui restent cohérents.

## Extraction de texte par lots – Enfiler les images et exécuter la file

Avec la file prête, l’étape suivante consiste à pousser chaque image dedans. La méthode `Enqueue` accepte une instance `OcrImage`, que nous créons à partir d’un chemin de fichier.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Une fois chaque fichier ajouté à la file, nous lançons le traitement :

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` bloque jusqu’à ce que chaque image soit terminée, puis renvoie une liste où chaque élément correspond à l’ordre d’entrée. Cela garantit que le résultat de la page 1 se trouve à l’index 0, celui de la page 2 à l’index 1, etc.—pratique lorsque vous devez faire correspondre les résultats aux fichiers sources.

## Comment créer l'OCR – Afficher les résultats

Enfin, affichons le texte reconnu dans la console. C’est ici que vous voyez réellement la **extraction de texte par lots** en action.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Lorsque vous exécutez le programme (`dotnet run`), vous devriez voir quelque chose comme :

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Si une image échoue (par ex., fichier corrompu), le `OcrResult` correspondant aura une propriété `Text` vide et vous pourrez inspecter `ocrResults[i].Exception` pour le diagnostic.

## Comment créer l'OCR – Conseils, cas limites et bonnes pratiques

### Gestion de gros lots

Traiter des centaines de PNG peut encore consommer de la mémoire si vous conservez tous les objets `OcrResult` en vie. Dans ce cas, diffusez la sortie vers un fichier ou une base de données dès que chaque résultat arrive :

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### Gestion des formats non PNG

Aspose OCR prend également en charge JPEG, BMP et TIFF dès le départ. Il suffit de changer l’extension de fichier dans votre liste ou d’utiliser une recherche générique. Les mêmes étapes du **tutoriel OCR C#** s’appliquent—aucune modification de code n’est nécessaire.

### Ignorer les pages blanches

Si vous avez des PDF numérisés contenant parfois des pages blanches, vous pouvez filtrer les résultats :

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Considérations de licence

La version d’évaluation appose un filigrane sur chaque page. Pour une utilisation en production, assurez‑vous d’intégrer votre fichier de licence au début de `Main` :

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Ajustement du parallélisme

`MaxDegreeOfParallelism` vaut par défaut `Environment.ProcessorCount`. Si vous constatez une utilisation élevée du CPU ou une pression mémoire, réduisez la valeur. Inversement, sur une VM cloud avec de nombreux cœurs, augmentez‑la pour exploiter pleinement le matériel.

## Résumé

Vous disposez maintenant d’une solution complète **comment faire de l'OCR par lots** en C# qui peut **extraire du texte à partir de PNG**, les exécuter en parallèle et vous fournir des résultats propres et ordonnés. En partageant un seul `OcrEngine`, vous avez appris **comment créer l'OCR** de pipelines à la fois économes en mémoire et faciles à maintenir. Ce **tutoriel OCR C#** vous montre également comment passer à l’**extraction de texte par lots** pour des centaines d’images avec seulement quelques lignes supplémentaires.

---

### Et après ?

* Essayez d’ajouter la détection de langue (`Engine.Language = Language.AutoDetect`).  
* Expérimentez avec les formats de sortie — écrivez les résultats en JSON ou CSV pour des analyses en aval.  
* Combinez cet OCR par lots avec une étape de conversion PDF‑vers‑image pour traiter des documents numérisés entiers.

N’hésitez pas à ajuster le parallélisme, à remplacer vos propres sources d’images, ou à brancher les résultats dans un index de recherche. Le ciel est la limite quand vous maîtrisez **comment faire de l'OCR par lots** en C#.

Bon codage, et que vos exécutions OCR soient rapides et sans erreur !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}