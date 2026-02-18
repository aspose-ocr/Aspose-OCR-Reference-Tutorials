---
category: general
date: 2026-02-17
description: Comment effectuer de l’OCR en C# et convertir rapidement une image en
  JSON. Suivez ce tutoriel C# OCR pour extraire le texte des images et enregistrer
  la mise en page au format JSON.
draft: false
keywords:
- how to perform OCR
- convert image to json
- c# ocr tutorial
- extract text image c#
- load image file c#
language: fr
og_description: Comment effectuer une OCR en C# ? Ce guide vous montre comment convertir
  une image en JSON, extraire le texte d’une image en C# et charger un fichier image
  pour l’OCR.
og_title: Comment réaliser l'OCR en C# – Convertir une image en JSON
tags:
- OCR
- C#
- Aspose
title: Comment réaliser l'OCR en C# – Guide de conversion d'image en JSON
url: /fr/net/text-recognition/how-to-perform-ocr-in-c-convert-image-to-json-guide/
---

file paths. We didn't.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR en C# – Guide de conversion d'image en JSON

Vous vous êtes déjà demandé **comment effectuer de l'OCR** sur un reçu, une facture ou tout document numérisé en utilisant C# ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsqu'ils doivent extraire du texte *et* préserver la mise en page sans passer des heures à écrire des analyseurs personnalisés.  

Dans ce tutoriel, nous parcourrons un **c# ocr tutorial** complet qui vous montre exactement comment effectuer de l'OCR, **convertir une image en json**, et enregistrer le résultat pour une analyse ultérieure. À la fin, vous disposerez d’une application console prête à l’emploi qui charge un fichier image en C#, extrait le texte et écrit un fichier JSON détaillé contenant les coordonnées, les scores de confiance et le texte brut.

## Prérequis — Ce dont vous avez besoin

- .NET 6 SDK ou version ultérieure (le code fonctionne également sur .NET Core)  
- Visual Studio 2022 ou tout éditeur de votre choix  
- Une licence Aspose OCR (vous pouvez commencer avec un essai gratuit)  
- Une image d'exemple, par ex., `receipt.png`, placée dans un dossier que vous pouvez référencer  

C’est tout—aucun package NuGet supplémentaire au-delà de `Aspose.OCR`. Si vous avez ces éléments, vous êtes prêt à commencer.

## Comment effectuer de l'OCR et obtenir la sortie JSON

Le cœur de **how to perform OCR** avec Aspose est simple : créez un `OcrEngine`, alimentez-le avec un flux d'image, appelez `Recognize`, puis sérialisez le `OcrResult` en JSON. Décomposons cela étape par étape.

### Étape 1 : Installer le package NuGet Aspose OCR

Ouvrez votre terminal dans le dossier du projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

> **Astuce :** Utilisez le drapeau `--version` pour verrouiller la dernière version stable (par ex., `23.9.0`). Cela rend votre build reproductible.

### Étape 2 : Créer la structure de base du projet console

Si vous n’avez pas encore de projet, créez‑en un :

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
```

Vous avez maintenant un fichier `Program.cs` prêt pour le code qui **load image file c#** et démarre le processus OCR.

### Étape 3 : Écrire le code complet OCR‑vers‑JSON

Ci-dessous se trouve le programme complet, prêt à l’exécution. Copiez‑collez‑le dans `Program.cs`. Chaque ligne est commentée afin que vous puissiez voir *pourquoi* chaque élément est important.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonOutput
{
    static void Main()
    {
        // ---------------------------------------------------------
        // 1️⃣  Initialize the OCR engine – this object holds
        //     language settings, recognition options, etc.
        // ---------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---------------------------------------------------------
        // 2️⃣  Load the image you want to analyze.
        //     This demonstrates **load image file c#** in a clean way.
        // ---------------------------------------------------------
        // Replace the path with the actual location of your receipt.png
        string imagePath = Path.Combine(
            Environment.CurrentDirectory, "receipt.png");
        ImageStream image = ImageStream.FromFile(imagePath);

        // ---------------------------------------------------------
        // 3️⃣  Perform the recognition.
        //     The engine returns an OcrResult containing text,
        //     confidence scores, and layout information.
        // ---------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ---------------------------------------------------------
        // 4️⃣  Convert the result to a detailed JSON string.
        //     This is the heart of **convert image to json**.
        // ---------------------------------------------------------
        string jsonResult = ocrResult.ToJson();

        // ---------------------------------------------------------
        // 5️⃣  Save the JSON to disk – you can later import this into
        //     databases, analytics pipelines, or UI components.
        // ---------------------------------------------------------
        string jsonPath = Path.Combine(
            Environment.CurrentDirectory, "receipt.json");
        File.WriteAllText(jsonPath, jsonResult);

        // ---------------------------------------------------------
        // 6️⃣  Let the user know we’re done.
        // ---------------------------------------------------------
        Console.WriteLine("JSON with layout saved to " + jsonPath);
    }
}
```

#### Ce que fait le code

| Étape | Pourquoi c'est important |
|------|---------------------------|
| **Initialize OcrEngine** | Configure la langue par défaut (anglais) et prépare les modèles internes. |
| **Load image file** | L’utilisation de `ImageStream.FromFile` garantit que l’image est lue dans un format attendu par Aspose. |
| **Recognize** | Le travail lourd—analyse des pixels, segmentation des caractères et recherche dans le dictionnaire. |
| **ToJson** | Produit une sortie structurée incluant les boîtes englobantes, la confiance et le texte brut. |
| **WriteAllText** | Enregistre le JSON afin que vous puissiez le partager avec d’autres services. |
| **Console.WriteLine** | Fournit un retour immédiat—pratique lors de l’exécution depuis un terminal. |

> **Attention :** Si votre image est grande, envisagez de la redimensionner d’abord pour améliorer la vitesse et l’utilisation de la mémoire. Aspose fournit des méthodes `Resize` que vous pouvez appeler sur `ImageStream`.

### Étape 4 : Exécuter l’application et vérifier la sortie

Depuis le terminal :

```bash
dotnet run
```

Vous devriez voir :

```
JSON with layout saved to C:\Path\To\OcrJsonDemo\receipt.json
```

Ouvrez `receipt.json` dans n’importe quel éditeur ; vous trouverez quelque chose comme :

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $12.34",
          "Confidence": 0.98,
          "BoundingBox": { "X": 120, "Y": 340, "Width": 150, "Height": 30 }
        }
      ]
    }
  ]
}
```

Ce JSON capture **extract text image c#** ainsi que les métadonnées de mise en page, parfait pour le traitement en aval.

## Convertir une image en JSON – Au‑delà des bases

Maintenant que vous savez **how to perform OCR**, explorons quelques variantes dont vous pourriez avoir besoin dans des projets réels.

### Gestion de plusieurs pages

Si votre source est un PDF ou TIFF multi‑pages, bouclez simplement sur chaque page :

```csharp
foreach (var pageStream in multiPageImageStreams)
{
    OcrResult result = ocrEngine.Recognize(pageStream);
    // Append each page's JSON to a master list
}
```

### Personnalisation de la langue et de la précision

Aspose prend en charge plus de 40 langues. Pour passer à l’espagnol :

```csharp
ocrEngine.Language = Language.Spanish;
```

Vous pouvez également ajuster `ocrEngine.Settings` pour activer **auto‑rotate**, **noise removal**, ou **dictionary‑based correction**—tout cela améliore la qualité du JSON que vous obtenez.

### Enregistrement du JSON au format lisible

Si vous préférez un JSON indenté pour la lisibilité :

```csharp
string prettyJson = ocrResult.ToJson(true); // true = formatted
File.WriteAllText(jsonPath, prettyJson);
```

## Charger un fichier image C# – Pièges courants et astuces

Lorsque vous **load image file c#**, vous pourriez rencontrer :

- **File not found** – Assurez‑vous que le chemin est absolu ou utilisez `Path.Combine` avec `Environment.CurrentDirectory`.  
- **Unsupported format** – Aspose gère PNG, JPEG, BMP, TIFF et PDF. Pour les formats RAW, convertissez‑les d’abord.  
- **Large file memory pressure** – Utilisez `ImageStream.FromFile(path, maxSizeInKB)` pour réduire la taille lors du chargement.  

Résoudre ces problèmes dès le départ vous évite des exceptions cryptiques plus tard dans le pipeline OCR.

## Extraire le texte d’une image C# – Vérification des résultats

Après avoir obtenu le JSON, vous pourriez ne vouloir que le texte brut :

```csharp
var ocrResult = ocrEngine.Recognize(image);
string plainText = ocrResult.Text; // Simple string with line breaks
Console.WriteLine(plainText);
```

![Diagramme montrant le flux de travail OCR – how to perform OCR, convert image to JSON, and extract text image c#](/images/ocr-workflow.png "flux de travail de l'OCR")

*Texte alternatif de l'image : "how to perform OCR workflow diagram illustrating convert image to JSON and extract text image c#"*  
*(L'image est un espace réservé ; remplacez‑la par un diagramme réel lors de la publication.)*

## Conclusion

Nous avons couvert **how to perform OCR** en C# du début à la fin, vous avons montré comment **convert image to JSON**, et expliqué les nuances de **load image file c#** et **extract text image c#**. L’exemple de code complet est prêt à être intégré dans n’importe quel projet .NET, et la sortie JSON vous fournit à la fois le texte brut et des données de mise en page précises pour l’analyse en aval.

Et après ? Essayez d’alimenter le JSON dans une base de données, de visualiser les boîtes englobantes sur une interface, ou d’enchaîner plusieurs exécutions OCR pour un traitement par lots. Vous pouvez également expérimenter d’autres fonctionnalités Aspose comme la reconnaissance d’écriture manuscrite ou la détection de codes‑barres—toutes deux s’intègrent naturellement dans le même pipeline.

Si vous rencontrez des problèmes, revenez aux conseils de dépannage dans la section « Load Image File C# », ou explorez la documentation exhaustive d’Aspose pour les paramètres avancés. Bon codage, et profitez de la transformation d’images en données structurées !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}