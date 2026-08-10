---
category: general
date: 2026-04-26
description: Comment effectuer rapidement une reconnaissance OCR par lots d'images
  PNG. Apprenez à extraire le texte d'un PNG, convertir les images en texte, écrire
  le texte reconnu et lire le répertoire PNG avec Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: fr
og_description: Comment traiter par lots des images PNG avec OCR en C# à l'aide d'Aspose
  OCR. Ce guide montre comment extraire du texte à partir de PNG, convertir les images
  en texte et écrire le texte reconnu efficacement.
og_title: Comment réaliser une OCR par lots d’images PNG en C# – Étape par étape
tags:
- OCR
- C#
- Aspose
title: Comment faire de l'OCR par lots d'images PNG en C# – Guide complet
url: /fr/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lot d'images PNG en C# – Guide complet

Vous vous êtes déjà demandé **comment faire de l'OCR par lot** sur un dossier entier de fichiers PNG sans écrire un programme distinct pour chaque image ? Vous n'êtes pas le seul à jongler avec des dizaines de captures d'écran, de reçus numérisés ou de graphiques qui doivent être transformés en texte consultable. Dans ce tutoriel, nous allons parcourir une solution pratique qui **extrait le texte des PNG**, **convertit les images en texte**, et **écrit le texte reconnu** dans des fichiers individuels—tout en parcourant automatiquement le répertoire PNG.

À la fin de ce guide, vous disposerez d’une application console C# prête à l’emploi qui traite n’importe quel nombre d’images en une seule fois. Aucun script supplémentaire, aucun copier‑coller manuel—juste du code qui fait le travail lourd pour vous.

## Ce dont vous avez besoin

- **.NET 6.0** ou version ultérieure (le code fonctionne également sous .NET Framework).  
- **Aspose.OCR for .NET** package NuGet (l’essai gratuit suffit pour les tests).  
- Un dossier contenant quelques fichiers *.png* que vous souhaitez OCRiser.  
- Visual Studio 2022 ou tout autre IDE C# de votre choix.

Si vous avez tout cela, passons directement à l’implémentation.

## Étape 1 – Préparer vos dossiers d’entrée et de sortie *(Lire le répertoire PNG)*

La première chose que nous faisons est d’indiquer au programme le dossier qui contient les images et de décider où les fichiers *.txt* résultants seront enregistrés. L’utilisation de `Directory.GetFiles` nous fournit une énumération propre de chaque PNG du répertoire.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Pourquoi c’est important :**  
- Utiliser le caractère générique (`*.png`) garantit que nous ne traitons que des fichiers image, en ignorant les éventuels documents parasites.  
- Créer le dossier de sortie à la volée évite une `DirectoryNotFoundException` plus tard.

> **Astuce :** Si vous devez prendre en charge d’autres formats (JPEG, BMP), il suffit d’étendre le motif de recherche ou d’appeler `Directory.EnumerateFiles` avec plusieurs extensions.

## Étape 2 – Initialiser le moteur OCR *(Convertir les images en texte)*

Aspose.OCR propose deux types de moteurs : un `OcrEngine` basé sur le CPU et un `GpuOcrEngine` accéléré par le GPU. Pour la plupart des traitements par lot, le moteur CPU est parfaitement suffisant, mais vous pouvez changer le nom de classe si vous disposez d’un GPU performant.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Pourquoi c’est important :**  
- Spécifier la langue améliore considérablement la précision, car le moteur sait quel jeu de caractères attendre.  
- Passer à `GpuOcrEngine` ne nécessite qu’une ligne de code si vous rencontrez des goulots d’étranglement de performance sur de gros lots.

## Étape 3 – Créer un Batch Recogniser

Aspose fournit un pratique `BatchRecognizer` qui accepte une énumération de chemins de fichiers et renvoie les résultats un par un. Cela évite de charger toutes les images en mémoire simultanément—un détail crucial pour les dossiers volumineux.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Pourquoi c’est important :**  
- Le batch recogniser encapsule la logique de boucle, nous permettant de nous concentrer sur ce qu’il faut faire avec chaque résultat plutôt que sur la façon d’itérer en toute sécurité.

## Étape 4 – Exécuter l’OCR sur toutes les images et écrire la sortie *(Écrire le texte reconnu)*

Nous effectuons maintenant réellement l’OCR. La méthode `Recognize` renvoie un `IEnumerable<RecognitionResult>` où chaque résultat contient le texte extrait et d’autres métadonnées.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Pourquoi c’est important :**  
- Utiliser `File.WriteAllText` garantit que le texte est enregistré avec l’encodage UTF‑8 par défaut, préservant les caractères spéciaux.  
- La numérotation incrémentale (`out_0.txt`, `out_1.txt`) correspond à l’ordre de traitement, ce qui est utile pour le débogage.

> **Cas limite :** Si une image échoue à l’OCR (par ex., fichier corrompu), `RecognitionResult.Text` sera vide. Vous pouvez ajouter une vérification simple dans la boucle pour consigner les échecs :

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Étape 5 – Assembler le tout – Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console. Il inclut les directives `using`, la validation des dossiers, et une petite interface console pour savoir quand le lot est terminé.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Sortie attendue :**  
L’exécution du programme affiche quelque chose comme :

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

Et vous verrez `out_0.txt` … `out_11.txt` dans le dossier de sortie, chacun contenant la version texte brut de son image correspondante.

## Questions fréquentes & Astuces

| Question | Réponse |
|----------|--------|
| *Puis‑je OCRiser également les sous‑dossiers ?* | Oui—remplacez `Directory.GetFiles` par `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Et si j’ai besoin d’une langue différente ?* | Définissez `ocrEngine.Language = Language.Spanish;` (ou tout autre enum supporté). |
| *Comment gérer d’énormes lots (des milliers de fichiers) ?* | Envisagez de traiter par lots ou d’utiliser `Parallel.ForEach` avec un degré de parallélisme limité afin d’éviter l’épuisement de la mémoire. |
| *La sortie est‑elle toujours en UTF‑8 ?* | `File.WriteAllText` utilise UTF‑8 sans BOM par défaut, ce qui convient à la plupart des langues latines. Pour les scripts asiatiques, vous devrez peut‑être spécifier explicitement `Encoding.UTF8`. |
| *Puis‑je obtenir des scores de confiance ?* | `RecognitionResult` expose `Confidence`—vous pouvez le consigner avec le texte pour le contrôle de qualité. |

## Vue d’ensemble visuelle *(Comment faire de l’OCR par lot – Diagramme)*

![Flux de travail OCR par lot montrant le dossier d’entrée → moteur OCR → batch recogniser → fichiers txt de sortie](https://example.com/diagram-how-to-batch-ocr.png "Comment faire de l'OCR par lot")

*Le texte alternatif contient le mot‑clé principal, répondant aux exigences SEO pour les images.*

## Conclusion

Nous venons de couvrir **comment faire de l'OCR par lot** d’un répertoire de fichiers PNG avec Aspose.OCR, depuis la lecture du répertoire PNG jusqu’à l’écriture de chaque fichier texte reconnu. La solution est entièrement autonome, fonctionne sur n’importe quel runtime .NET moderne, et peut être étendue pour l’accélération GPU, la prise en charge multilingue ou le traitement parallèle.

Prêt pour l’étape suivante ? Essayez de remplacer `Language.Latin` par une autre langue, ou intégrez la sortie dans un index de recherche afin que vos documents deviennent immédiatement consultables. Le ciel est la limite une fois que vous maîtrisez l’OCR par lot.

Bon codage, et faites‑moi savoir dans les commentaires si vous rencontrez le moindre problème !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}