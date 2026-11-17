---
category: general
date: 2026-05-25
description: Convertir les fichiers TIFF en texte avec Aspose.OCR en C#. Apprenez
  la conversion d’images en texte par lots et extrayez efficacement le texte des fichiers
  TIFF.
draft: false
keywords:
- convert tiff to text
- extract text from tiff
- batch image to text conversion
- convert scanned images txt
language: fr
og_description: Convertissez les TIFF en texte avec Aspose.OCR. Ce guide montre la
  conversion d’images en texte par lots et comment extraire le texte des fichiers
  TIFF en quelques lignes de C#.
og_title: Convertir TIFF en texte en C# – Guide complet d'OCR par lots
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  headline: Convert TIFF to Text in C# – Complete Batch OCR Guide
  type: TechArticle
- description: Convert TIFF to text using Aspose.OCR in C#. Learn batch image to text
    conversion and extract text from TIFF files efficiently.
  name: Convert TIFF to Text in C# – Complete Batch OCR Guide
  steps:
  - name: '**Create** an OCR engine set for English.'
    text: '**Create** an OCR engine set for English.'
  - name: '**Collect** every TIFF file from the target folder.'
    text: '**Collect** every TIFF file from the target folder.'
  - name: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
    text: '**Run** `BatchOcr.RecognizeAll` with four threads, turning each image into
      a string.'
  - name: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
    text: '**Loop** over the results, swapping the `.tif` extension for `.txt` and
      writing the string to disk.'
  type: HowTo
tags:
- C#
- OCR
- Aspose
- TIFF
title: Convertir TIFF en texte en C# – Guide complet d’OCR par lots
url: /fr/net/text-recognition/convert-tiff-to-text-in-c-complete-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir TIFF en texte en C# – Guide complet d'OCR par lots

Vous avez déjà eu besoin de **convertir TIFF en texte** sans savoir par où commencer ? Vous n'êtes pas seul — de nombreux développeurs rencontrent des difficultés avec l'OCR par lots lorsqu'ils traitent des documents numérisés. Dans ce tutoriel, nous allons parcourir une solution pratique qui **extrait le texte des fichiers TIFF** à l'aide d'Aspose.OCR, et nous le ferons en parallèle afin que les gros dossiers se terminent en quelques secondes.

Nous aborderons également les meilleures pratiques de **conversion d'image en texte par lots**, de sorte qu'à la fin vous disposerez d'un extrait réutilisable qui transforme un répertoire complet d'images numérisées en fichiers *.txt* propres — parfaits pour l'indexation, la recherche ou l'alimentation d'analyses en aval.

## Ce dont vous avez besoin

- **.NET 6.0** ou ultérieur (le code se compile également sur .NET Framework)  
- **Aspose.OCR for .NET** package NuGet (`Install-Package Aspose.OCR`)  
- Un dossier contenant un ou plusieurs fichiers *.tif* (le format de numérisation TIFF classique)  
- Votre IDE préféré (Visual Studio, VS Code, Rider—ce que vous préférez)

C’est tout. Aucun service externe, aucune clé API, juste du pur C# et Aspose.

![Capture d'écran d'un fichier TIFF en cours de traitement et du fichier texte résultant](/images/ocr-result.png "Résultat OCR montrant la sortie du TIFF converti en texte")

* (Texte alternatif : Capture d'écran montrant la sortie du TIFF converti en texte à l'écran)

## Étape 1 : Configurer le moteur OCR – Convertir TIFF en texte

Tout d'abord, nous avons besoin d'une instance `OcrEngine` qui sait qu'elle doit lire les caractères anglais. Le moteur est le cœur de la conversion ; le configurer correctement garantit des résultats fiables.

```csharp
using Aspose.OCR;
using System.IO;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // Create an OCR engine configured for English – this is the core of convert TIFF to text
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };
```

*Pourquoi c'est important :*  
Aspose.OCR prend en charge des dizaines de langues. Si vous traitez des numérisations multilingues, il suffit de remplacer `OcrLanguage.English` par la valeur d'énumération appropriée. Laisser la langue non définie force le moteur en mode détection automatique, ce qui peut être plus lent et moins précis.

## Étape 2 : Rassembler tous les fichiers TIFF – Extraire le texte du TIFF efficacement

Ensuite, nous récupérons chaque fichier *.tif* d'un dossier que vous spécifiez. L'utilisation de `Directory.GetFiles` nous fournit un tableau propre que nous pouvons transmettre au processeur par lots.

```csharp
        // Locate every TIFF in the input folder – adjust the path to your own directory
        string inputFolder = @"C:\Scans\Batch";
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif", SearchOption.TopDirectoryOnly);

        if (tiffFiles.Length == 0)
        {
            System.Console.WriteLine("No TIFF files found. Check the folder path.");
            return;
        }
```

*Astuce :* Le drapeau `SearchOption.AllDirectories` peut être utilisé si vos numérisations sont imbriquées dans des sous‑dossiers. N'oubliez pas que la récursion plus profonde peut augmenter l'utilisation de la mémoire pendant l'étape par lots.

## Étape 3 : Effectuer l'OCR en parallèle – Conversion d'image en texte par lots

Passons maintenant à la partie amusante. Aspose.OCR fournit un helper statique `BatchOcr.RecognizeAll` qui accepte un tableau de chemins de fichiers, un moteur, et un indice de `parallelism`. Nous lancerons quatre threads, ce qui, sur un ordinateur portable quad‑core moderne, donne un gain de vitesse quasi linéaire.

```csharp
        // Run OCR on all files in parallel (4 threads by default)
        // The result is a dictionary where Key = file path, Value = extracted text
        Dictionary<string, string> ocrResults = BatchOcr.RecognizeAll(tiffFiles, ocrEngine, parallelism: 4);
```

*Pourquoi le parallélisme ?*  
Analyser un lot de TIFF haute résolution peut être très gourmand en CPU. En répartissant le travail sur plusieurs threads, nous gardons tous les cœurs occupés, réduisant considérablement le temps d'exécution total. Si vous exécutez cela sur un serveur avec davantage de cœurs, augmentez la valeur de `parallelism` en conséquence.

## Étape 4 : Écrire la sortie – Convertir les images numérisées en fichiers TXT

Enfin, nous parcourons le dictionnaire et écrivons chaque morceau de texte dans un fichier *.txt* qui partage le même nom de base que l'original. C’est le moment où **convertir des images numérisées en txt** devient une réalité.

```csharp
        // Save each recognized text to a .txt file with the same base name as the source TIFF
        foreach (var kvp in ocrResults)
        {
            string sourcePath = kvp.Key;
            string extractedText = kvp.Value;

            // Change extension from .tif to .txt
            string txtPath = Path.ChangeExtension(sourcePath, ".txt");

            // Write the text – UTF‑8 ensures all characters are preserved
            File.WriteAllText(txtPath, extractedText);
            System.Console.WriteLine($"Saved: {txtPath}");
        }

        System.Console.WriteLine("Batch conversion complete!");
    }
}
```

### Ce que fait le code, en français simple

1. **Créer** un moteur OCR configuré pour l'anglais.  
2. **Collecter** chaque fichier TIFF du dossier cible.  
3. **Exécuter** `BatchOcr.RecognizeAll` avec quatre threads, transformant chaque image en chaîne de caractères.  
4. **Parcourir** les résultats, en remplaçant l'extension `.tif` par `.txt` et en écrivant la chaîne sur le disque.

C’est l’ensemble du flux de travail **convertir TIFF en texte** en moins de 50 lignes de code.

## Gestion des cas particuliers – Quand les choses ne se passent pas bien

- **TIFF manquants ou corrompus** – `BatchOcr` lèvera une `OcrException`. Enveloppez l’appel dans un `try / catch` si vous avez besoin d’une dégradation douce.  
- **Documents non anglais** – changez `OcrLanguage.English` en `OcrLanguage.Spanish`, `OcrLanguage.French`, etc., ou utilisez `OcrLanguage.AutoDetect`.  
- **Images très grandes** – envisagez de réduire le DPI avant l’OCR (`ocrEngine.ImagePreprocessing.Dpi = 200`) pour économiser de la mémoire, même si vous pouvez perdre un peu de précision.  
- **Encodage de sortie** – si vous avez besoin d’une page de code spécifique (par ex., Windows‑1252), passez‑la à `File.WriteAllText(txtPath, extractedText, Encoding.GetEncoding(1252))`.

## Astuces pro pour des conversions par lots robustes

- **Journaliser les échecs** : créez une `List<string> failedFiles` et ajoutez tout fichier qui lève une exception ; écrivez la liste dans un journal après la boucle.  
- **Réutiliser le moteur** : la même instance `OcrEngine` peut être réutilisée pour de nombreux fichiers ; ne l’instanciez pas à l’intérieur de la boucle.  
- **Valider le résultat** : un simple `if (string.IsNullOrWhiteSpace(extractedText))` peut signaler des numérisations vides ou illisibles.  
- **Combiner avec PDF** : si votre source est un PDF multipage, convertissez chaque page en TIFF d’abord (Aspose.PDF le fait) puis lancez ce lot.

## Prochaines étapes – Aller au-delà de la simple conversion

Maintenant que vous pouvez **extraire le texte des fichiers TIFF** en masse, vous pourriez vouloir :

- Alimenter les fichiers *.txt* dans un index de recherche (Elasticsearch, Azure Cognitive Search).  
- Exécuter une détection de langue sur chaque résultat pour orienter les documents vers des pipelines spécifiques à la locale.  
- Générer des PDF recherchables en superposant le texte OCR sur les images originales (Aspose.PDF à nouveau).  

Tous ces scénarios reposent sur la même idée centrale : **la conversion d'image en texte par lots** est un bloc de construction pour des systèmes de traitement de documents plus vastes.

---

### Conclusion

Vous venez d’apprendre comment **convertir TIFF en texte** avec Aspose.OCR, traiter un dossier complet en parallèle, et sauvegarder chaque résultat sous forme de fichier *.txt* propre. La solution est légère, entièrement configurable et prête pour la production—que vous numérisiez des factures anciennes, archiviez des contrats scannés ou alimentiez un moteur de recherche texte.  

Testez‑la, ajustez le parallélisme, et commencez à injecter ces nouveaux fichiers texte dans le workflow de votre choix. Bonne OCR !

---

## Tutoriels associés

- [Extraire du texte d'images à l'aide de l'opération OCR sur dossiers](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extraire du texte d'image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)
- [Extraire le texte d'image C# avec sélection de langue utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}