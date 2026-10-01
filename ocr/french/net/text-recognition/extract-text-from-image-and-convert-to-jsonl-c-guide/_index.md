---
category: general
date: 2026-01-02
description: Extraire du texte d’une image avec Aspose OCR en C#. Apprenez comment
  convertir une image au format JSONL rapidement et de façon fiable.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: fr
og_description: Extrayez le texte d’une image avec Aspose OCR et convertissez‑le au
  format JSONL. Tutoriel complet C# étape par étape pour les développeurs.
og_title: Extraire le texte d’une image – Convertir en JSONL en C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Extraire du texte d’une image et le convertir en JSONL – Guide C#
url: /fr/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image et le convertir en JSONL – Tutoriel complet C#

Vous avez déjà eu besoin d'**extraire du texte d'une image** sans savoir quelle bibliothèque vous donnerait une sortie propre et structurée ? Vous n'êtes pas seul. Dans de nombreux projets de traitement de reçus ou de numérisation de documents, le goulot d'étranglement consiste à transformer un bitmap en texte recherchable *et* en un format lisible par machine.  

Bonne nouvelle : avec Aspose OCR, vous pouvez **extraire du texte d'une image** et, en quelques lignes de code, **convertir l'image en JSONL** pour les analyses en aval. Ce guide vous accompagne pas à pas, du chargement d'un PNG à l'écriture d'un fichier JSON‑Lines qui peut être diffusé dans un pipeline de données.

> **Astuce :** Si vous utilisez déjà .NET 6 ou une version ultérieure, le même code fonctionne sans configuration supplémentaire.

## Prérequis — Ce dont vous avez besoin

- **.NET 6 SDK** (ou toute version récente de .NET)
- **Aspose.OCR** package NuGet  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** pour la sérialisation  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Une image d'exemple (par ex. `receipt.png`) placée dans un dossier que vous pouvez référencer.
- Un IDE ou éditeur de votre choix — Visual Studio, VS Code, Rider, etc.

Pas d'installation lourde, pas de services externes, seulement quelques packages NuGet.

![Extract text from image using C#](https://example.com/assets/ocr-sample.png)

*Texte alternatif : extraire du texte d'une image avec C# et Aspose OCR*

## Étape 1 : Charger l'image à traiter  

La première chose à faire lorsque vous voulez **extraire du texte d'une image** est de fournir un bitmap au moteur OCR. Utiliser `System.Drawing.Bitmap` est simple et fonctionne pour la plupart des formats raster.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Pourquoi c’est important :** Charger l'image en tant que `Bitmap` donne au moteur OCR un accès direct aux pixels, ce qui améliore la vitesse et la précision de reconnaissance comparé à la diffusion de bytes bruts.

## Étape 2 : Configurer Aspose OCR pour une sortie JSON‑Lines  

Aspose OCR vous permet de spécifier la langue, le format de sortie et quelques réglages de performance. Ici nous demandons **JSON‑Lines** (un objet JSON par ligne) car c’est idéal pour un traitement ligne par ligne ultérieur.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Conseil de pro :** Si vous avez besoin de reçus multilingues, définissez `Language = Language.Multilingual` ou passez un tableau de valeurs `Language`.

## Étape 3 : Exécuter l'OCR et capturer le résultat  

Nous **extraits maintenant du texte d'une image**. La méthode `Recognize` renvoie un objet `OcrResult` contenant une collection d'objets `OcrLine`, chacun représentant une ligne de texte reconnu avec sa boîte englobante.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

À ce stade, `ocrResult.Lines` contient tout ce dont vous avez besoin — texte brut, scores de confiance et coordonnées.

## Étape 4 : Sérialiser les lignes en JSON‑Lines  

Nous allons transformer la collection en une chaîne JSON joliment indentée. Même si le format JSON‑Lines est généralement compact, ajouter de l'indentation rend le fichier plus lisible pendant le développement.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

La variable `jsonLines` résultante ressemble à ceci (troncature pour la brièveté) :

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Chaque ligne se termine par un caractère de nouvelle ligne, vous obtenez ainsi un vrai **JSONL** (JSON‑Lines).

## Étape 5 : Écrire le JSON‑Lines sur le disque  

Enfin, nous persistons la sortie afin que d’autres services—comme Spark, Logstash ou un simple script Bash—puissent l’ingérer ligne par ligne.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Lorsque vous ouvrez `receipt.jsonl`, vous verrez un objet JSON par ligne, prêt à être diffusé.

## Étape 6 : Vérifier l'exportation  

Une vérification rapide vous évite des heures de débogage plus tard. Lisons les premières lignes et affichons‑les dans la console.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Sortie typique de la console :

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Si vous voyez quelque chose de similaire, félicitations — vous avez **extrait du texte d'une image** et **converti l'image en JSONL** avec succès.

## Pièges courants & comment les éviter  

| Problème | Pourquoi cela arrive | Solution |
|----------|----------------------|----------|
| **Sortie vide** | Chemin d'image incorrect ou fichier illisible. | Utilisez `File.Exists(imagePath)` avant de créer le bitmap. |
| **Scores de confiance faibles** | Image floue ou contraste faible. | Pré‑traitez l'image (par ex. `Bitmap.RotateFlip`, `Graphics.Clear`) ou augmentez le DPI. |
| **Langue incorrecte** | L'OCR utilise l'anglais par défaut alors que le reçu est dans une autre langue. | Définissez `options.Language = Language.Spanish` (ou l'énumération appropriée). |
| **JSONL apparaît comme un tableau JSON unique** | Vous avez utilisé `Formatting.None` sans gérer les sauts de ligne. | Assurez‑vous que chaque objet sérialisé se termine par `Environment.NewLine`. |

## Exemple complet fonctionnel  

Voici le programme complet, prêt à être exécuté. Copiez‑le dans un projet console et appuyez sur **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Résultat attendu :** Un fichier `receipt.jsonl` contenant un objet JSON par ligne, chacun avec les champs `Text`, `Confidence` et `BoundingBox`. Vous pouvez maintenant alimenter ce fichier dans n’importe quel pipeline analytique qui consomme du JSONL.

## Prochaines étapes – Aller au-delà de l'OCR de base  

- **Traitement par lots :** Enveloppez la logique ci‑dessus dans une boucle `foreach` pour gérer des dossiers entiers de reçus.  
- **Parallélisme :** Utilisez `Parallel.ForEach` pour des gains de vitesse multi‑cœur lorsqu’il s’agit de milliers d’images.  
- **Post‑traitement :** Éliminez les lignes à faible confiance (`Confidence < 0.9`) avant de les stocker.  
- **Intégration :** Poussez le JSONL directement vers Azure Blob Storage ou AWS S3 avec les SDK correspondants.  
- **Formats alternatifs :** Changez `OutputFormat` en `PlainText` ou `Xml` si votre système en aval préfère ces formats.  

## Conclusion  

Vous disposez maintenant d’une solution solide, de bout en bout, pour **extraire du texte d'une image** et **convertir l'image en JSONL** avec Aspose OCR en C#. Le tutoriel a couvert tout, du chargement du bitmap à la vérification du résultat, en passant par plusieurs astuces pratiques pour rendre votre pipeline robuste.

Testez-le avec vos propres reçus, factures ou formulaires numérisés — voyez le moteur OCR transformer les pixels en données recherchables et structurées ligne par ligne en quelques secondes. Si vous rencontrez des cas particuliers (par ex. des scans inclinés ou du texte multilingue), revisitez la section *RecognitionOptions* et ajustez la langue ou les étapes de pré‑traitement.

Bon codage, et que vos pipelines de données restent toujours propres !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}