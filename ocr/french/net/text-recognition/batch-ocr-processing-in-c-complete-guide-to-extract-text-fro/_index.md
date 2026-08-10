---
category: general
date: 2026-06-16
description: Le traitement OCR par lots en C# vous permet de convertir rapidement
  des images en texte. Apprenez comment extraire le texte des images en utilisant
  Aspose.OCR avec du code étape par étape.
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: fr
og_description: Le traitement OCR par lots en C# convertit les images en texte. Suivez
  ce guide pour extraire le texte des images à l'aide d'Aspose.OCR.
og_title: Traitement OCR par lots en C# – Extraire le texte des images
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: Traitement OCR par lots en C# – Guide complet pour extraire du texte à partir
  d'images
url: /fr/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Traitement OCR par lots en C# – Guide complet pour extraire du texte à partir d'images

Vous êtes-vous déjà demandé comment **traiter l'OCR par lots** en C# sans écrire une boucle séparée pour chaque image ? Vous n'êtes pas le seul. Lorsque vous avez des dizaines – voire des centaines – de reçus, factures ou notes manuscrites numérisées, alimenter manuellement chaque fichier dans un moteur OCR devient rapidement un cauchemar.  

Bonne nouvelle : avec Aspose.OCR, vous pouvez *convertir des images en texte* en une seule opération propre. Dans ce tutoriel, nous parcourrons l’ensemble du flux de travail, de l’installation de la bibliothèque à l’exécution d’un job de production capable d’**extraire du texte à partir d'images** et d’enregistrer les résultats dans le format dont vous avez besoin.

> **Ce que vous obtiendrez :** une application console prête à l’emploi qui traite un dossier complet, écrit des fichiers texte brut (ou JSON, XML, HTML, PDF) côte à côte avec les originaux, et vous montre comment ajuster le parallélisme pour un débit maximal.

## Prérequis

- SDK .NET 6.0 ou version ultérieure (le code fonctionne aussi avec .NET Core et .NET Framework)
- Visual Studio 2022, VS Code ou tout éditeur C# de votre choix
- Une licence Aspose.OCR NuGet (une version d’essai gratuite suffit pour l’évaluation)
- Un dossier contenant des fichiers image (`.png`, `.jpg`, `.tif`, etc.) que vous souhaitez **convertir des images en texte**

Si vous avez coché toutes ces cases, plongeons‑y.

![Diagram illustrating batch OCR processing flow](batch-ocr-workflow.png "Batch OCR processing flow")

## Étape 1 : Installer Aspose.OCR via NuGet

Tout d’abord, ajoutez le package Aspose.OCR à votre projet. Ouvrez un terminal dans le répertoire du projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Ou, si vous êtes dans Visual Studio, faites un clic droit sur *Dependencies → Manage NuGet Packages*, recherchez **Aspose.OCR**, puis cliquez sur *Install*. Cette ligne unique récupère tout ce dont vous avez besoin pour le **traitement OCR par lots**.

> **Astuce pro :** maintenez la version du package à jour ; la dernière version (en juin 2026) ajoute la prise en charge de nouveaux formats d’image et améliore la précision multilingue.

## Étape 2 : Créer le squelette de la console

Créez une nouvelle application console C# (si ce n’est pas déjà fait) et remplacez le `Program.cs` généré par le squelette suivant. Notez la directive `using Aspose.OCR;` en haut – c’est l’espace de noms qui nous fournit la classe `OcrBatchProcessor`.

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

À ce stade, le fichier n’est qu’un placeholder, mais c’est un point de départ propre pour notre logique de **traitement OCR par lots**.

## Étape 3 : Initialiser le OcrBatchProcessor

Le `OcrBatchProcessor` est le moteur qui parcourt un dossier, exécute l’OCR sur chaque image prise en charge et écrit la sortie. L’instancier est aussi simple que :

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

Pourquoi utiliser un processeur par lots plutôt qu’une API image unique ? La classe batch gère automatiquement l’énumération des fichiers, la journalisation des erreurs et même l’exécution parallèle, ce qui signifie que vous passez moins de temps à écrire des boucles et plus de temps à affiner la précision.

## Étape 4 : Indiquer vos dossiers d’entrée et de sortie

Dites au processeur où lire les images et où déposer les résultats. Remplacez les chemins factices par les répertoires réels de votre machine.

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

Les deux dossiers doivent exister avant d’exécuter l’application ; sinon vous obtiendrez une `DirectoryNotFoundException`. Les créer programmatique­ment est simple, mais pour plus de clarté nous gardons l’exemple basique.

## Étape 5 : Choisir le format de sortie

Aspose.OCR peut générer du texte brut, du JSON, du XML, du HTML ou même du PDF. Pour la plupart des scénarios **extraire du texte à partir d'images**, le texte brut suffit, mais n’hésitez pas à changer.

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

Si vous avez besoin de données structurées pour un traitement en aval, `ResultFormat.Json` est un bon choix. La bibliothèque encapsulera automatiquement le texte de chaque page dans un objet JSON, en conservant les informations de mise en page.

## Étape 6 : Définir la langue et le parallélisme

La précision de l’OCR dépend du bon modèle de langue. L’anglais convient à la plupart des documents occidentaux, mais vous pouvez choisir n’importe quelle langue prise en charge (arabe, chinois, etc.). De plus, vous pouvez indiquer au processeur combien de threads lancer – jusqu’à quatre par défaut.

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**Pourquoi le parallélisme est important :** si vous avez un CPU quad‑core, régler `MaxDegreeOfParallelism` à `4` peut réduire le temps de traitement d’environ 75 %. Sur un ordinateur portable à deux cœurs, `2` est plus sûr. Expérimentez pour trouver le meilleur compromis pour votre matériel.

## Étape 7 : Exécuter le job par lots

Maintenant le vrai travail commence. Une seule ligne lance tout le pipeline, traite chaque image du dossier d’entrée et écrit les résultats dans le dossier de sortie.

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

Lorsque la console affiche *Batch OCR completed.*, vous trouverez un fichier `.txt` (ou le format que vous avez choisi) à côté de chaque image d’origine. Les noms de fichiers correspondent à la source, ce qui rend la corrélation entre la sortie OCR et l’image très simple.

## Exemple complet fonctionnel

En rassemblant le tout, voici le programme complet que vous pouvez copier‑coller dans `Program.cs` et exécuter immédiatement :

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### Résultat attendu

En supposant que vous avez trois images (`invoice1.png`, `receipt2.jpg`, `form3.tif`) dans le dossier d’entrée, le dossier de sortie contiendra :

```
invoice1.txt
receipt2.txt
form3.txt
```

Chaque fichier `.txt` contient les caractères bruts extraits de l’image correspondante. Ouvrez n’importe quel fichier avec Notepad, et vous verrez la représentation texte du scan original.

## Questions fréquentes & cas particuliers

### Que faire si certaines images échouent à être traitées ?

`OcrBatchProcessor` journalise les erreurs dans la console par défaut et continue avec le fichier suivant. En production, vous pouvez vous abonner à l’événement `OnError` pour collecter les noms de fichiers en échec et les retenter plus tard.

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### Puis‑je traiter directement des PDF ?

Oui. Aspose.OCR traite chaque page d’un PDF comme une image en interne. Il suffit de pointer `InputFolder` vers un répertoire contenant des PDF, et le processeur extraira le texte de chaque page – ce qui **convertit des images en texte** même lorsque la source est un PDF.

### Comment gérer les documents multilingues ?

Définissez `Language` sur `OcrLanguage.Multilingual` ou spécifiez une liste de langues si la version de la bibliothèque le permet. Le moteur tentera de reconnaître les caractères de toutes les langues fournies, ce qui est pratique pour les factures internationales.

### Qu’en est‑il de la consommation mémoire ?

Le processeur par lots diffuse chaque image, donc l’utilisation mémoire reste faible même avec des milliers de fichiers. Cependant, activer un `MaxDegreeOfParallelism` élevé sur une machine à mémoire limitée peut provoquer des pics. Surveillez votre RAM et ajustez le nombre de threads en conséquence.

## Conseils pour une meilleure précision

- **Pré‑traiter les images** : éliminez le bruit, redressez et convertissez en niveaux de gris avant l’OCR. Aspose.OCR propose `ImagePreprocessOptions` que vous pouvez associer à `ocrBatchProcessor`.
- **Choisir le bon format** : si vous avez besoin de conserver la mise en page, `ResultFormat.Html` ou `Pdf` maintiennent les sauts de ligne et le style de base.
- **Valider les résultats** : implémentez une étape de post‑traitement simple qui vérifie les fichiers de sortie vides – ils indiquent souvent une reconnaissance échouée.

## Prochaines étapes

Maintenant que vous avez maîtrisé le **traitement OCR par lots** pour **extraire du texte à partir d'images**, vous pourriez vouloir :

- **Intégrer à une base de données** – stocker chaque résultat OCR avec des métadonnées pour la recherche.
- **Ajouter une interface** – créer un petit front‑end WPF ou WinForms permettant aux utilisateurs de glisser‑déposer des dossiers.
- **Faire évoluer** – exécuter le job par lots sur Azure Functions ou AWS Lambda pour un traitement natif cloud.

Chacune de ces thématiques s’appuie sur les concepts de base que nous avons couverts, vous plaçant ainsi en bonne position pour étendre votre solution.

---

**Bon codage !** Si vous rencontrez un problème ou avez des idées d’amélioration, laissez un commentaire ci‑dessous. Continuons la discussion et rendons l’automatisation OCR encore plus fluide.


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}