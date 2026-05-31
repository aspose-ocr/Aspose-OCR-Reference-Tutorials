---
category: general
date: 2026-05-31
description: Comment effectuer une reconnaissance optique de caractères (OCR) par
  lots en C# avec Aspose OCR. Apprenez à convertir des images en texte, à extraire
  le texte des images et à traiter plusieurs fichiers efficacement.
draft: false
keywords:
- how to batch OCR
- convert images to text
- extract text from images
- OCR multiple files
- batch OCR processing
language: fr
og_description: Comment effectuer une OCR par lots en C# avec Aspose OCR. Convertissez
  des images en texte, extrayez le texte des images et gérez facilement l’OCR de plusieurs
  fichiers.
og_title: Comment faire de l'OCR par lots en C# – Guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  headline: How to Batch OCR in C# – Complete Programming Guide
  type: TechArticle
- description: How to batch OCR in C# with Aspose OCR. Learn to convert images to
    text, extract text from images, and process multiple files efficiently.
  name: How to Batch OCR in C# – Complete Programming Guide
  steps:
  - name: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
    text: '**.NET 6 SDK** (or later) installed – the latest runtime gives you better
      performance and native support for async I/O.'
  - name: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
    text: '**Visual Studio 2022** (Community Edition works fine) or any editor you
      like.'
  - name: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
    text: 'The **Aspose.OCR** NuGet package. Install it via the Package Manager Console:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- batch-processing
title: Comment réaliser une OCR par lots en C# – Guide complet de programmation
url: /fr/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment réaliser une OCR par lots en C# – Guide complet de programmation

Vous vous êtes déjà demandé **comment faire de l’OCR par lots** sur un dossier entier d’images numérisées sans ouvrir chaque fichier manuellement ? Vous n’êtes pas seul. Dans de nombreux projets réels—pensez à l’automatisation de factures ou à l’archivage de photos historiques—vous devez **convertir des images en texte** en masse, et le faire fichier par fichier est une perte de temps considérable.

Dans ce tutoriel, nous parcourrons une application console C# prête à l’emploi qui prend chaque PNG, JPG ou TIFF d’un répertoire source, exécute Aspose OCR sur chacun, puis crée un fichier *.txt* correspondant dans un dossier de sortie. À la fin, vous serez à l’aise avec **l’extraction de texte à partir d’images**, la gestion de **l’OCR de plusieurs fichiers**, et vous disposerez d’une base solide pour tout **traitement OCR par lots** dont vous pourriez avoir besoin plus tard.

## Ce que vous allez apprendre

- Configurer un projet .NET avec le package NuGet Aspose OCR.  
- Définir les dossiers source et destination pour une exécution **OCR par lots**.  
- Énumérer les types d’images pris en charge et les transmettre au moteur OCR.  
- Écrire le texte reconnu dans des fichiers *.txt* individuels, convertissant ainsi **les images en texte**.  
- Gérer les problèmes courants comme les dossiers manquants, les formats non supportés et les optimisations de performances.

Aucune expérience préalable avec Aspose n’est requise ; une compréhension de base du C# et de Visual Studio suffit.

---

![Diagram showing the flow of batch OCR processing from image folder to text output – how to batch OCR](/images/batch-ocr-flow.png){alt="diagramme du flux d’OCR par lots"}

## Comment réaliser une OCR par lots – Configuration du projet

Avant de plonger dans le code, assurez‑vous d’avoir :

1. **.NET 6 SDK** (ou version ultérieure) installé – la dernière runtime offre de meilleures performances et une prise en charge native des I/O asynchrones.  
2. **Visual Studio 2022** (l’édition Community convient parfaitement) ou tout autre éditeur de votre choix.  
3. Le package **Aspose.OCR** via NuGet. Installez‑le avec la console du gestionnaire de packages :

   ```powershell
   Install-Package Aspose.OCR
   ```

C’est tout. Le reste du tutoriel part du principe que le package est correctement référencé.

## Étape 2 : Préparer les dossiers source et destination (convertir des images en texte)

Nous avons besoin de deux dossiers : l’un contenant les images brutes et l’autre où les fichiers *.txt* générés seront placés. Le code ci‑dessous crée le dossier de destination s’il n’existe pas déjà—aucune manipulation manuelle requise.

```csharp
// Define where the images live and where the text files will go
string sourceFolder = @"C:\OCR\Batch";
string outputFolder = @"C:\OCR\BatchTxt";

// Ensure the output directory exists; CreateDirectory is idempotent
Directory.CreateDirectory(outputFolder);
```

> **Pourquoi c’est important :** Si vous omettez l’appel `CreateDirectory`, le programme lèvera une `DirectoryNotFoundException` dès la première tentative d’écriture d’un fichier texte. En le gérant dès le départ, vous rendez le processus d’OCR par lots plus robuste.

## Étape 3 : Énumérer les fichiers image pour l’OCR de plusieurs fichiers

Ensuite, nous récupérons chaque fichier correspondant aux formats que nous supportons. L’utilisation de LINQ rend le code concis tout en restant lisible.

```csharp
// Grab all PNG, JPG, and TIFF files from the source folder (non‑recursive)
var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
    .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));
```

> **Astuce :** Si vous devez plus tard gérer des PDF ou des BMP, il suffit d’étendre la clause `Where`. Garder le filtre à un seul endroit rend les ajustements futurs simples.

## Étape 4 : Exécuter le moteur OCR sur chaque image (comment faire de l’OCR par lots)

Voici le cœur du sujet : fournir chaque image à Aspose OCR et extraire le texte reconnu. La boucle ci‑dessous crée une nouvelle instance `OcrEngine` pour chaque fichier—cela garantit que la mémoire occupée par l’image précédente est libérée avant de passer à la suivante.

```csharp
foreach (var imagePath in imageFiles)
{
    // Initialize the OCR engine with the current image
    OcrEngine ocrEngine = new OcrEngine
    {
        Image = ImageStream.FromFile(imagePath)
    };

    // Perform recognition; Recognize() returns an OcrResult object
    OcrResult ocrResult = ocrEngine.Recognize();

    // Build the output .txt file path (same base name, .txt extension)
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    // Persist the extracted text
    File.WriteAllText(textFilePath, ocrResult.Text);

    Console.WriteLine($"Processed {Path.GetFileName(imagePath)} → {Path.GetFileName(textFilePath)}");
}
```

**Que se passe‑t‑il ?**  

- `ImageStream.FromFile` charge l’image dans un flux lisible par Aspose.  
- `ocrEngine.Recognize()` exécute l’algorithme OCR et renvoie une chaîne dans `ocrResult.Text`.  
- `File.WriteAllText` écrit cette chaîne sur le disque, réalisant ainsi **l’extraction de texte à partir d’images**.

### Gestion des cas limites

- **Images corrompues** – encapsulez l’appel de reconnaissance dans un `try/catch`, consignez l’échec, puis poursuivez avec le fichier suivant.  
- **Lots volumineux** – envisagez de traiter les fichiers de façon asynchrone avec `Parallel.ForEach` si vous disposez d’une machine multi‑cœur.  
- **Langues différentes** – définissez `ocrEngine.Language = Language.English;` ou toute autre langue prise en charge avant d’appeler `Recognize()`.

## Étape 5 : Enregistrer le texte extrait (extraire du texte à partir d’images)

Le fragment précédent enregistre déjà la sortie OCR, mais isolons cette logique dans une méthode d’assistance. Cela rend la boucle principale plus claire et encourage la réutilisation.

```csharp
static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
{
    string textFilePath = Path.Combine(outputFolder,
        Path.GetFileNameWithoutExtension(imagePath) + ".txt");

    File.WriteAllText(textFilePath, recognizedText);
}
```

Vous remplacerez alors l’appel inline `File.WriteAllText` par :

```csharp
SaveOcrResult(outputFolder, imagePath, ocrResult.Text);
```

> **Pourquoi extraire cela dans une méthode ?** Cela sépare les préoccupations — reconnaissance vs persistance—et vous offre un point unique pour ajouter du post‑traitement (comme le retrait des espaces superflus ou l’ajout d’un horodatage).

## Exemple complet fonctionnel – Traitement OCR par lots en C#

En rassemblant tous les morceaux, voici un programme autonome que vous pouvez copier‑coller dans un nouveau projet Console App et exécuter immédiatement.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Define source & destination folders
            string sourceFolder = @"C:\OCR\Batch";
            string outputFolder = @"C:\OCR\BatchTxt";

            // 2️⃣ Make sure the output folder exists
            Directory.CreateDirectory(outputFolder);

            // 3️⃣ Get all supported image files (convert images to text)
            var imageFiles = Directory.EnumerateFiles(sourceFolder, "*.*", SearchOption.TopDirectoryOnly)
                .Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase) ||
                            f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase));

            // 4️⃣ Process each image (how to batch OCR)
            foreach (var imagePath in imageFiles)
            {
                try
                {
                    // Initialise OCR engine for the current file
                    OcrEngine ocrEngine = new OcrEngine
                    {
                        Image = ImageStream.FromFile(imagePath)
                    };

                    // Run OCR – this extracts text from images
                    OcrResult result = ocrEngine.Recognize();

                    // 5️⃣ Save the result (extract text from images)
                    SaveOcrResult(outputFolder, imagePath, result.Text);

                    Console.WriteLine($"✅ {Path.GetFileName(imagePath)} processed.");
                }
                catch (Exception ex)
                {
                    // Gracefully handle problematic files
                    Console.WriteLine($"⚠️ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }

            Console.WriteLine("🎉 Batch OCR processing complete!");
        }

        // Helper to write the OCR output to a .txt file
        static void SaveOcrResult(string outputFolder, string imagePath, string recognizedText)
        {
            string textFilePath = Path.Combine(outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, recognizedText);
        }
    }
}
```

### Résultat attendu

Lorsque vous lancez le programme, la console affichera des lignes similaires à :

```
✅ invoice001.png processed.
✅ receipt123.jpg processed.
✅ map.tif processed.
🎉 Batch OCR processing complete!
```

Pendant ce temps, le dossier `C:\OCR\BatchTxt` contiendra :

- `invoice001.txt`
- `receipt123.txt`
- `map.txt`

Chaque fichier renferme la représentation texte brute de son image source, prête à être indexée, recherchée ou analysée en aval.

## Astuces pro & pièges courants (traitement OCR par lots)

- **Gestion de la mémoire :** Aspose OCR libère les tampons d’image après chaque appel `Recognize()`, mais si vous traitez des milliers de fichiers, pensez à invoquer `GC.Collect()` avec parcimonie pour garder l’empreinte mémoire faible.  
- **Accélération :** Utilisez `OcrEngine.RecognizeAsync()` sous .NET 6+ et lancez plusieurs tâches avec `Task

## Que devez‑vous apprendre ensuite ?

- [Comment réaliser une OCR par lots d’images avec List dans Aspose.OCR pour .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extraire du texte à partir d’images en utilisant l’opération OCR sur des dossiers](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Comment effectuer une OCR sur des images d’archives avec Aspose.OCR pour .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}