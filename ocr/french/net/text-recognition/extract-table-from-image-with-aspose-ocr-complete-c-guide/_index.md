---
category: general
date: 2026-03-18
description: Extraire un tableau à partir d’une image en utilisant Aspose OCR en C#.
  Apprenez comment convertir le tableau en JSON, obtenir le JSON du tableau et extraire
  le texte de l’image en quelques minutes.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: fr
og_description: Extrayez un tableau d’une image avec Aspose OCR en C#. Apprenez à
  convertir le tableau en JSON, obtenir le JSON du tableau et extraire rapidement
  le texte d’une image.
og_title: Extraire un tableau d’une image avec Aspose OCR – Guide complet C#
tags:
- Aspose OCR
- C#
- Table Extraction
title: Extraire un tableau d’une image avec Aspose OCR – Guide complet C#
url: /fr/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire un tableau à partir d'une image – Guide complet C#  

Vous avez déjà eu besoin d'**extraire un tableau à partir d'une image** mais vous n'étiez pas sûr de la bibliothèque qui pouvait le faire sans une montagne de parsing manuel ? Vous n'êtes pas seul. Dans de nombreux projets de traitement de factures ou de numérisation de reçus, le vrai point douloureux est de transformer un bitmap bruité en un tableau structuré que votre système en aval peut consommer.  

La bonne nouvelle ? Avec Aspose OCR vous pouvez **convertir un tableau en JSON** en quelques lignes, et vous obtenez également le texte brut de l'image entière, donc **extraire du texte à partir d'une image** est un bonus. Dans ce tutoriel, nous parcourrons tout le flux – du chargement d'une image à l'obtention d'une représentation JSON propre du tableau détecté.

> **Gain rapide :** À la fin, vous disposerez d'une application console C# exécutable qui affiche à la fois le texte OCR brut et une chaîne JSON que vous pouvez injecter directement dans une base de données ou une API.

## Prérequis

- .NET 6.0 SDK (ou toute version récente de .NET) installé.  
- Une licence valide Aspose OCR ou un essai gratuit (la bibliothèque fonctionne sans licence mais ajoute un filigrane).  
- Une image contenant réellement un tableau – par exemple `invoice_table.png`.  
- Visual Studio 2022, VS Code, ou tout éditeur de votre choix.  

Aucun package NuGet supplémentaire au-delà de `Aspose.OCR` n'est requis.

## Étape 1 : Configurer le projet et installer Aspose OCR

Tout d'abord, créez un nouveau projet console et ajoutez la bibliothèque OCR.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Astuce pro :** Si vous utilisez un proxy d'entreprise, ajoutez le drapeau `--no-restore` et exécutez `dotnet restore` plus tard avec les variables d'environnement appropriées.

## Étape 2 : Initialiser le moteur OCR et activer la reconnaissance de tableau

Le cœur de la solution est le `OcrEngine`. En activant `EnableTableRecognition`, nous indiquons à Aspose OCR de rechercher des structures en forme de grille plutôt que de traiter tout comme du texte brut.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Pourquoi cette étape est-elle cruciale ? Sans la reconnaissance de tableau, le moteur aplatirait l'image en une seule chaîne, rendant impossible la reconstruction des lignes et colonnes ultérieurement. L'activer ajoute une phase d'analyse de mise en page légère qui ne coûte presque rien en performances mais apporte d'énormes bénéfices en aval.

## Étape 3 : Charger votre image et lancer la reconnaissance

Nous pointons maintenant le moteur vers le fichier contenant le tableau. `ImageStream.FromFile` prend en charge la plupart des formats courants (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Si l'image est grande, envisagez de la redimensionner d'abord pour accélérer le traitement. Aspose OCR détecte automatiquement le DPI, mais un scan à 300 DPI est un bon compromis pour la plupart des tableaux.

## Étape 4 : Extraire le texte brut – « extract text from image »

Même si notre objectif principal est le tableau, vous avez souvent encore besoin du texte brut pour la journalisation ou un traitement de secours.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

La propriété `Text` concatène tout ce que le moteur voit, en conservant les sauts de ligne. Cela est pratique lorsque vous devez vérifier que l'OCR a correctement lu les en-têtes ou pieds de page en dehors de la zone du tableau.

## Étape 5 : Obtenir le tableau détecté en JSON – « convert table to json » & « get table json »

C’est ici que la magie opère. `GetTableAsJson()` sérialise les lignes, colonnes et contenus de cellules détectés en une chaîne JSON propre.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

Le JSON résultant ressemble à ceci (formaté pour la lisibilité) :

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

Pourquoi le JSON est-il le format préféré ? Il est indépendant du langage, facile à désérialiser en objets, et fonctionne très bien avec les API web modernes. Si vous avez besoin d’un CSV à la place, il suffit d’itérer sur les lignes et de joindre les textes des cellules avec des virgules.

## Étape 6 : (Optionnel) Convertir le JSON en objet .NET – « convert image to json »

Si vous préférez travailler avec des types forts, désérialisez le JSON en utilisant `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Vous définiriez `TableModel`, `RowModel` et `CellModel` pour correspondre au schéma JSON. Cette étape montre comment passer de **convert image to json** jusqu’à un objet typé, facilitant la validation en aval.

## Exemple complet fonctionnel

En rassemblant tout, voici le programme complet, prêt à être exécuté. Enregistrez-le sous `Program.cs` dans le dossier du projet créé précédemment.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Sortie attendue

Lorsque vous exécutez `dotnet run`, vous devriez voir quelque chose de similaire :

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Si la sortie semble vide, vérifiez que `EnableTableRecognition` est bien réglé sur `true` et que l'image contient réellement des lignes de grille nettes.

## Pièges courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Aucun JSON retourné** | Détection du tableau désactivée ou image à faible contraste. | Assurez-vous que `ocrEngine.Settings.EnableTableRecognition = true` et améliorez la qualité de l'image (augmentez le contraste, binarisez). |
| **Lignes partielles** | L'OCR est confus par des cellules fusionnées ou du texte pivoté. | Pré‑traitez l'image : redressez (`ImageProcessor.Rotate`) ou séparez manuellement les cellules fusionnées. |
| **Brouillage Unicode** | Police non reconnue (par ex., écriture manuscrite). | Changez les packs de langue via `ocrEngine.Language = Language.English;` ou utilisez un autre moteur OCR pour l'écriture manuscrite. |
| **Ralentissement des performances** | Image très grande (>5 MP). | Redimensionnez à environ 1500 px de largeur tout en conservant le DPI. |

## Prochaines étapes : aller au-delà des bases

Maintenant que vous pouvez **extraire un tableau à partir d'une image** et **convertir le tableau en JSON**, envisagez ces extensions :

- **Persist the JSON** dans une base de données avec Entity Framework.  
- **Post‑process** le JSON pour normaliser les formats de devise (par ex., supprimer `$`).  
- **Batch process** un dossier de factures en utilisant `Directory.GetFiles` et parallélisez avec `Parallel.ForEach`.  
- **Integrate** avec Azure Functions ou AWS Lambda pour des pipelines OCR serverless.  

Chacun de ces sujets introduit naturellement les autres mots-clés secondaires comme **convert image to json** (lorsque vous envoyez le résultat complet de l'OCR à un point de terminaison cloud) et **get table json** pour l'analyse en aval.

---

### Conclusion

Nous venons de vous montrer comment **extraire un tableau à partir d'une image** avec Aspose OCR, transformer ce tableau en JSON propre, et même le désérialiser en objets C#. Le même modèle

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}