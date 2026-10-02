---
category: general
date: 2026-01-01
description: Tutoriel C# OCR montrant comment extraire du texte, charger une image
  pour l'OCR et écrire du JSON dans un fichier en utilisant Aspose.OCR – guide étape
  par étape.
draft: false
keywords:
- c# OCR tutorial
- how to extract text
- write json to file
- load image for OCR
- OCR image to JSON
language: fr
og_description: Tutoriel C# OCR qui vous guide pour extraire du texte d’images, charger
  une image pour l’OCR et écrire du JSON dans un fichier en utilisant Aspose.OCR.
og_title: Tutoriel OCR C# – Extraire le texte et exporter en JSON
tags:
- Aspose.OCR
- C#
- Text Extraction
title: Tutoriel OCR en C# – Extraire du texte d'images et exporter en JSON
url: /fr/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tutoriel c# OCR – Extraire du texte d'images et exporter en JSON

Vous vous êtes déjà demandé comment extraire du texte d'une facture numérisée sans passer des heures à écrire des analyseurs personnalisés ? Vous n'êtes pas seul. Dans ce **c# OCR tutorial** nous vous montrerons exactement comment charger une image pour l'OCR, exécuter le moteur de reconnaissance, puis **écrire le JSON dans un fichier** afin que vous puissiez alimenter les systèmes en aval.

Imaginez que vous avez un dossier de reçus, chacun nommé `receipt1.png`, `receipt2.png`, et que vous avez besoin d'une méthode rapide pour les transformer en enregistrements JSON interrogeables. C'est le problème que nous allons résoudre, et à la fin vous disposerez d'une application console prête à l'emploi qui fait exactement cela. Aucune dépendance supplémentaire au-delà d'Aspose.OCR, et aucune magie — juste des étapes claires et reproductibles.

> **Ce que vous apprendrez**
> - Comment **charger une image pour l'OCR** en utilisant Aspose.OCR.
> - La meilleure façon d'**extraire du texte** et d'obtenir les scores de confiance.
> - Convertir le résultat OCR en une charge utile **OCR image to JSON** bien structurée.
> - **Écrire le JSON dans un fichier** en toute sécurité et vérifier la sortie.

## Prérequis

- .NET 6 SDK ou version ultérieure (le code fonctionne également sur .NET Core).  
- Visual Studio 2022 ou tout éditeur de votre choix.  
- Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`).  
- Un fichier image (PNG, JPG, BMP) que vous souhaitez traiter – pour la démo nous utiliserons `invoice.png`.

Si vous n'avez pas l'un d'eux, téléchargez le SDK depuis le site de Microsoft et ajoutez le package NuGet via la console du gestionnaire de packages :

```powershell
Install-Package Aspose.OCR
```

Maintenant que les bases sont posées, plongeons dans l'implémentation réelle.

## Étape 1 : c# OCR tutorial – Initialiser le moteur OCR

Avant de pouvoir **charger une image pour l'OCR**, nous avons besoin d'une instance du moteur qui pilotera le processus de reconnaissance. La classe `OcrEngine` est légère, mais il est recommandé de l'encapsuler dans un bloc `using` afin que les ressources soient libérées rapidement.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine – this is the heart of the c# OCR tutorial
        var ocrEngine = new OcrEngine();

        // The rest of the steps follow…
```

*Astuce :* Si vous prévoyez de traiter de nombreuses images en lot, réutilisez la même instance `OcrEngine` au lieu d'en créer une nouvelle à chaque fois. Cela réduit la consommation de mémoire et accélère le traitement.

## Étape 2 : Charger une image pour l'OCR

Nous allons maintenant réellement **charger une image pour l'OCR**. Aspose.OCR prend en charge une variété de formats, vous pouvez donc le pointer vers un PNG, JPEG ou même un TIFF multi‑pages. La méthode `OcrImage.FromFile` lit le fichier et le prépare pour la reconnaissance.

```csharp
        // Step 2: Load the image you want to recognize
        // Replace YOUR_DIRECTORY with the folder that holds your invoice.png
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);
```

> **Pourquoi c'est important :** Charger l'image séparément vous permet d'inspecter ses dimensions, DPI, ou même de la pré‑traiter (par ex., binarisation) avant de l'envoyer au moteur. Si l'image est corrompue, `FromFile` lèvera une exception claire, que vous pouvez attraper et consigner.

## Étape 3 : Comment extraire du texte – Exécuter la reconnaissance

Avec l'image en main, nous pouvons enfin **extraire du texte**. La méthode `Recognize` renvoie un objet `OcrResult` qui contient non seulement le texte brut mais aussi les données de position et les scores de confiance pour chaque mot.

```csharp
        // Step 3: Perform OCR – this is the core of how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);
```

*Cas particulier :* Certains PDF contiennent des calques de texte invisibles. Si vous alimentez une page PDF rendue en image, le moteur peut ne rien voir. Dans ces cas, envisagez d'utiliser Aspose.PDF pour extraire le calque caché d'abord, puis de recourir à l'OCR uniquement si nécessaire.

## Étape 4 : OCR image to JSON – Convertir le résultat

La classe `OcrResult` propose une fonction d'aide pratique `ToJson()` qui sérialise l'ensemble du résultat — y compris la boîte englobante et la confiance de chaque mot — en une chaîne JSON. C'est la façon la plus propre d'obtenir **OCR image to JSON** sans écrire votre propre sérialiseur.

```csharp
        // Step 4: Convert the OCR result to JSON (includes words, confidence, locations)
        string jsonResult = ocrResult.ToJson();
```

Si vous préférez un schéma personnalisé, vous pouvez parcourir `ocrResult.Words` et construire votre propre objet, mais pour la plupart des scénarios le JSON intégré est suffisant et déjà bien structuré.

## Étape 5 : Écrire le JSON dans un fichier

Voici la dernière pièce du puzzle : persister la charge utile JSON. La méthode `File.WriteAllText` garantit que le fichier est créé (ou écrasé) de manière atomique. Assurez‑vous que le répertoire cible existe, sinon vous rencontrerez une `DirectoryNotFoundException`.

```csharp
        // Step 5: Save the JSON output – this demonstrates write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);
```

*Conseil :* Si vous avez besoin de UTF‑8 avec BOM ou d'un autre encodage, utilisez la surcharge qui accepte un argument `Encoding`.

## Étape 6 : Vérifier la sortie

Un simple `Console.WriteLine` nous indique que le processus s'est terminé avec succès. Vous pouvez également ouvrir le fichier JSON dans un visualiseur pour confirmer la structure.

```csharp
        // Step 6: Inform the user that the JSON file has been saved
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

### Extrait JSON attendu

```json
{
  "Text": "Invoice #12345\nDate: 2025-12-31\nTotal: $250.00",
  "Words": [
    { "Text": "Invoice", "Confidence": 0.98, "Location": { "X": 10, "Y": 15, "Width": 80, "Height": 20 } },
    { "Text": "#12345", "Confidence": 0.96, "Location": { "X": 95, "Y": 15, "Width": 60, "Height": 20 } }
    // … more words …
  ]
}
```

Le JSON inclut la position de chaque mot, ce qui est pratique si vous souhaitez plus tard mettre en surbrillance le texte dans une interface.

## Exemple complet fonctionnel

Ci-dessous le programme complet, prêt à copier‑coller. Remplacez `YOUR_DIRECTORY` par le chemin réel où se trouve votre image.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonExportDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to recognize
        var imagePath = @"YOUR_DIRECTORY/invoice.png";
        var ocrImage = OcrImage.FromFile(imagePath);

        // Step 3: Perform OCR – how to extract text
        var ocrResult = ocrEngine.Recognize(ocrImage);

        // Step 4: Convert the result to JSON (OCR image to JSON)
        string jsonResult = ocrResult.ToJson();

        // Step 5: Write JSON to file – write JSON to file
        var jsonPath = @"YOUR_DIRECTORY/invoice.json";
        File.WriteAllText(jsonPath, jsonResult);

        // Step 6: Verify
        Console.WriteLine($"JSON saved to {jsonPath}");
    }
}
```

Exécutez le programme (`dotnet run` depuis le dossier du projet) et vous trouverez `invoice.json` à côté de votre PNG original.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **FileNotFoundException** lors du chargement de l'image | Erreur de frappe dans le chemin ou fichier manquant | Utilisez `Path.Combine` et vérifiez `File.Exists` avant d'appeler `FromFile`. |
| **Scores de confiance faibles** | Qualité d'image médiocre, DPI faible | Pré‑traitez avec `ocrImage.AdjustContrast` ou augmentez la résolution de l'image à 300 DPI. |
| **Fichier JSON vide** | `ocrResult` a renvoyé null (échec du moteur) | Vérifiez que le format de l'image est supporté et que la licence (le cas échéant) est correctement appliquée. |
| **Goulot d'étranglement de performance sur de gros lots** | Re‑création de `OcrEngine` à chaque itération | Réutilisez une seule instance `OcrEngine` pendant le lot, en la libérant uniquement à la fin. |

## Prochaines étapes

Maintenant que vous avez maîtrisé le **c# OCR tutorial**, vous pourriez vouloir :

- **Batch process** un dossier complet et agréger les fichiers JSON dans une base de données unique.  
- **Integrate** la sortie avec Azure Cognitive Search pour des PDF interrogeables.  
- **Add language support** en définissant `ocrEngine.Language = OcrLanguage.Spanish` (ou toute langue supportée).  
- **Post‑process** le JSON pour extraire des tableaux ou des paires clé‑valeur à l'aide d'expressions régulières.  

Chacune de ces extensions s'appuie sur les concepts de base que nous avons couverts : charger des images pour l'OCR, extraire du texte, convertir en JSON et écrire ce JSON sur le disque.

### Conclusion

Dans ce **c# OCR tutorial** nous avons parcouru chaque étape nécessaire pour **charger une image pour l'OCR**, **extraire du texte**, transformer le résultat en une charge utile **OCR image to JSON**, et enfin **écrire le JSON dans un fichier**. L'exemple de code complet est prêt à être intégré dans n'importe quel projet .NET, et les explications vous donnent le contexte nécessaire pour adapter la solution à des scénarios réels.

Essayez-le avec votre propre jeu de reçus ou factures — ajustez le pré‑traitement des images, expérimentez avec différentes langues, et observez la croissance du JSON produit. Si vous rencontrez des problèmes, consultez à nouveau le tableau des pièges ou laissez un commentaire ci‑dessous. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}