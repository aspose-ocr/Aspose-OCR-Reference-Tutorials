---
category: general
date: 2026-02-19
description: Apprenez à effectuer la reconnaissance optique de caractères en lot avec
  Aspose.OCR en C#. Ce guide vous montre comment extraire du texte à partir d'images
  et convertir des images en txt efficacement.
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: fr
og_description: Comment réaliser une OCR par lots avec Aspose.OCR en C#. Extraire
  le texte des images et convertir les images en txt en quelques étapes simples.
og_title: Comment faire de l'OCR par lots en C# – Conversion rapide d'image en texte
tags:
- OCR
- C#
- Aspose
title: Comment réaliser une OCR par lots en C# – Extraire rapidement du texte à partir
  d'images
url: /fr/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots en C# – Guide complet étape par étape

Vous vous êtes déjà demandé **comment faire de l'OCR par lots** sur un dossier complet d'images sans écrire un programme distinct pour chaque fichier ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent extraire du texte de dizaines — voire de milliers — de pages numérisées, de reçus ou de captures d'écran. La bonne nouvelle ? Avec Aspose.OCR, vous pouvez automatiser toute la chaîne, **extraire du texte à partir d'images**, et **convertir des images en txt** en quelques lignes seulement.

Dans ce tutoriel, nous allons parcourir un exemple complet, prêt à l’emploi, qui montre exactement comment configurer un processeur OCR par lots, ajuster le pré‑traitement, gérer le parallélisme et écrire chaque résultat dans un fichier `.txt`. À la fin, vous disposerez d’une application console autonome que vous pourrez intégrer à n’importe quel projet .NET.

## Ce dont vous avez besoin

- .NET 6.0 ou version ultérieure (le code fonctionne également sur .NET Core et .NET Framework)
- Aspose.OCR for .NET package NuGet (`Aspose.OCR`)  
- Un dossier rempli de fichiers image (`.png`, `.jpg`, etc.) que vous souhaitez traiter
- Une quantité modeste de RAM ; la démo utilise 4 threads parallèles mais vous pouvez l’ajuster

Aucun service externe, aucun fichier de configuration caché — juste du code C# pur que vous pouvez compiler et exécuter dès aujourd’hui.

![Diagramme illustrant le flux de traitement OCR par lots](/images/how-to-batch-ocr-flow.png "diagramme du flux OCR par lots")

## Étape 1 : Installer Aspose.OCR et configurer le projet

Tout d’abord, ajoutez le package Aspose.OCR à votre projet :

```bash
dotnet add package Aspose.OCR
```

**Pourquoi c’est important :** Aspose.OCR regroupe le moteur OCR, les données linguistiques et les utilitaires de pré‑traitement, vous n’aurez donc besoin d’aucun binaire tiers. Une fois le package installé, créez une nouvelle application console (ou ajoutez le code à une existante) et importez les espaces de noms requis :

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

Ces instructions `using` vous donnent accès aux classes du processeur par lots et aux utiles I/O pratiques.

## Étape 2 : Configurer le processeur OCR par lots

Nous allons maintenant instancier `OcrBatchProcessor` et lui indiquer quelle langue rechercher, comment nettoyer les images et combien de threads exécuter en parallèle. C’est le cœur de **comment faire de l'OCR par lots** efficacement.

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**Pourquoi activer le redressement ?** De nombreux documents numérisés ne sont pas parfaitement alignés ; l’algorithme de redressement les fait pivoter pour retrouver une ligne de base droite, ce qui augmente souvent les taux de reconnaissance de 10‑15 %.

## Étape 3 : Brancher un rappel de résultat pour enregistrer les fichiers texte

Le processeur par lots déclenche un événement pour chaque image terminée. Nous allons nous abonner à `ResultProcessed` afin d’écrire chaque résultat OCR dans un fichier `.txt` — **convertir des images en txt** à la volée.

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

Astuce rapide : si vous devez préserver la structure de dossiers d’origine, vous pouvez modifier `txtPath` pour inclure des sous‑dossiers ou un répertoire de sortie séparé.

## Étape 4 : Exécuter le lot sur votre dossier d’images

Il ne reste plus qu’à pointer le processeur vers le dossier contenant les images que vous voulez **extraire du texte à partir d'images**. La méthode `ProcessFolder` parcourt récursivement les sous‑dossiers, vous pouvez donc déposer tout un arbre de scans et laisser la bibliothèque gérer le reste.

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

Lorsque vous lancez le programme, vous verrez une sortie console similaire à :

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

Chaque image possède désormais un fichier `.txt` frère contenant le texte extrait.

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet que vous pouvez copier‑coller dans `Program.cs` :

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### Résultat attendu

- Pour chaque `*.png` ou `*.jpg` dans le répertoire source, un fichier `*.txt` correspondant apparaît à côté.
- La console affiche une ligne par fichier, vous offrant un retour en temps réel.
- Si une image ne peut pas être lue (fichier corrompu, format non pris en charge), Aspose.OCR consigne une erreur mais continue le traitement du reste — grâce à la robustesse intégrée du moteur par lots.

## Questions fréquentes & cas particuliers

### Et si je dois traiter des PDF au lieu d’images ?

Aspose.OCR peut accepter les pages PDF comme images en interne, mais vous devrez d’abord convertir le PDF en images raster (par ex., avec Aspose.PDF). Une fois les PNG obtenus, le même code de lot fonctionne sans modification.

### Puis‑je changer la langue à la volée ?

Oui. La propriété `Language` accepte n’importe quelle valeur de l’énumération `Language` (Spanish, French, Chinese, etc.). Si vous avez des documents multilingues, envisagez d’exécuter deux passes — une par langue — ou utilisez `Language.AutoDetect`.

### Comment limiter le lot à des types de fichiers spécifiques ?

`ProcessFolder` accepte un `SearchOption` optionnel et un tableau `string[] extensions`. Exemple :

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### Qu’en est‑il de l’accélération GPU ?

Aspose.OCR prend en charge le GPU via la configuration `OcrEngine`, mais le paramètre `MaxDegreeOfParallelism` du processeur par lots reste le principal levier de concurrence. Si vous disposez d’un GPU compatible, activez‑le dans les paramètres du moteur avant de créer `OcrBatchProcessor`.

### Comment gérer des dossiers très volumineux (des dizaines de milliers de fichiers) ?

- Augmentez `MaxDegreeOfParallelism` avec prudence ; trop de threads peuvent épuiser la mémoire.
- Utilisez un répertoire de sortie dédié pour éviter l’encombrement.
- Videz périodiquement les journaux sur le disque afin de prévenir l’engorgement de la mémoire.

## Conseils pro pour un OCR de haute qualité

- **Le DPI compte** : les images à 300 DPI ou plus offrent la meilleure précision. Si vos scans sont inférieurs, envisagez un agrandissement avec un filtre bicubique avant le traitement.
- **Réduction du bruit** : activez `Preprocessing.NoiseRemoval` si les images sources sont granuleuses.
- **Nom des fichiers** : gardez les noms courts et alphanumériques ; les caractères spéciaux peuvent perturber la logique du chemin de rappel.
- **Journalisation** : remplacez `Console.WriteLine` par un logger approprié (par ex., `Serilog`) pour les charges de travail en production.

## Prochaines étapes

Maintenant que vous avez maîtrisé **comment faire de l'OCR par lots**, vous pourriez vouloir :

- **Extraire du texte à partir d'images** et alimenter la sortie dans un index de recherche (par ex., Elasticsearch) pour la recherche en texte intégral.
- **Convertir des images en txt** puis exécuter du traitement du langage naturel (NLP) pour classer automatiquement les documents.
- Expérimenter avec **différents packs de langues** ou des dictionnaires personnalisés pour une terminologie spécifique à votre secteur.

Si vous êtes curieux du post‑traitement, consultez les tutoriels sur « Parsing OCR output with regular expressions » ou « Storing OCR results in a SQL database ».

---

**Bon codage !** N’hésitez pas à ajuster le parallélisme, ajouter d’autres étapes de pré‑traitement, ou encapsuler le tout dans un service Windows pour une surveillance continue. Le ciel est la limite lorsque vous combinez les capacités de lot d’Aspose.OCR avec un peu d’ingéniosité .NET.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}