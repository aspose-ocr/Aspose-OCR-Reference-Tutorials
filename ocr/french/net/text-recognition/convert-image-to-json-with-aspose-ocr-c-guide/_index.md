---
category: general
date: 2026-01-15
description: Convertir une image en JSON avec Aspose OCR en C#. Apprenez à extraire
  le texte d’une image, obtenir les boîtes englobantes au format JSON et reconnaître
  l’image d’un reçu.
draft: false
keywords:
- convert image to json
- extract text from image
- aspose ocr c# example
- recognize receipt image
- json bounding boxes
language: fr
og_description: Convertir une image en JSON à l'aide d'Aspose OCR en C#. Guide étape
  par étape pour extraire le texte d’une image, reconnaître une image de reçu et obtenir
  les boîtes englobantes au format JSON.
og_title: Convertir une image en JSON avec le guide Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSON
- Image Processing
title: Convertir une image en JSON avec le guide Aspose OCR C#
url: /fr/net/text-recognition/convert-image-to-json-with-aspose-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir une image en JSON avec le guide Aspose OCR C# 

Vous avez déjà eu besoin de **convertir une image en JSON** mais vous ne saviez pas quelle bibliothèque pouvait vous fournir à la fois le texte brut et les coordonnées exactes des mots ? Vous n'êtes pas seul. De nombreux développeurs rencontrent cet obstacle lorsqu'ils essaient d'extraire du texte à partir de fichiers image—en particulier des reçus—tout en ayant besoin d'une charge utile JSON lisible par machine pour le traitement en aval.

Dans ce tutoriel, nous parcourrons un **exemple Aspose OCR C#** complet qui vous montre comment extraire du texte d’une image, reconnaître une image de reçu, et générer des **boîtes englobantes JSON** pour chaque mot. À la fin, vous disposerez d’une application console prête à l’emploi qui affiche une chaîne JSON correctement formatée que vous pourrez injecter dans n’importe quelle API, base de données ou pipeline d’analyse.

> **Ce que vous en retirerez**  
> • Un projet C# entièrement fonctionnel qui **convertit une image en JSON**  
> • Un aperçu de la raison pour laquelle nous activons `IncludeBoundingBoxes` (c’est la clé des `json bounding boxes`)  
> • Des astuces pour gérer différents formats d’image et langues  

Commençons.

---

## Ce dont vous avez besoin

Avant de plonger dans le code, assurez‑vous d’avoir les prérequis suivants installés :

- **.NET 6.0 SDK** (ou toute version ultérieure) – le code cible .NET 6 mais fonctionne également avec .NET Framework 4.7+.
- **Aspose.OCR for .NET** package NuGet – vous pouvez l’ajouter via `dotnet add package Aspose.OCR`.
- Une image de reçu d’exemple (`receipt.jpg`) placée dans un dossier que vous pouvez référencer depuis votre projet.
- Visual Studio 2022, VS Code, ou tout IDE de votre choix.

Aucun autre service externe n’est requis ; tout s’exécute localement.

---

## Convertir une image en JSON – Vue d’ensemble

L’idée principale est simple : charger une image, demander à Aspose OCR de reconnaître l’anglais (ou toute langue prise en charge), lui demander d’inclure les boîtes englobantes, puis demander le résultat au format **JSON**. La bibliothèque effectue tout le travail lourd — OCR, analyse de mise en page et sérialisation JSON.

Voici un diagramme de haut niveau du flux (imaginez une petite illustration) :

```
[Image File] → Aspose OCR Engine → Recognition Options (JSON + Bounding Boxes) → JSON Output
```

Ce petit diagramme capture l’ensemble du pipeline que nous allons implémenter.

---

## Étape 1 : Configurer le projet et installer Aspose OCR

Tout d’abord, créez un nouveau projet console et ajoutez le package Aspose OCR.

```bash
dotnet new console -n JsonOutputDemo
cd JsonOutputDemo
dotnet add package Aspose.OCR
```

> **Astuce pro :** Si vous utilisez Visual Studio, faites un clic droit sur le projet → *Manage NuGet Packages* → recherchez **Aspose.OCR** et installez la dernière version stable (actuellement 23.12).

---

## Étape 2 : Charger l’image que vous souhaitez reconnaître

Nous utiliserons la méthode `OcrImage.FromFile` pour lire l’image du reçu. Assurez‑vous que le chemin pointe vers un fichier réel ; sinon vous rencontrerez une `FileNotFoundException`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // Step 2: Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

Si votre image se trouve à côté du fichier `.csproj`, vous pouvez simplement utiliser `"receipt.jpg"`.

---

## Étape 3 : Configurer les options OCR pour les boîtes englobantes JSON

La magie opère lorsque nous activons `OutputFormat = OutputFormat.Json` **et** `IncludeBoundingBoxes = true`. Le premier indique à Aspose de sérialiser le résultat en JSON, tandis que le second ajoute `x`, `y`, `width` et `height` pour chaque mot—exactement ce dont vous avez besoin pour les `json bounding boxes`.

```csharp
        // Step 3: Configure OCR options
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };
```

Vous pouvez également ajuster `ocrOptions.Dpi` ou `ocrOptions.Language` si vous avez besoin d’une résolution supérieure ou d’une langue différente.

---

## Étape 4 : Effectuer la reconnaissance – Extraire le texte de l’image

Nous appelons maintenant `Recognize`. La méthode renvoie un objet `OcrResult` qui contient la chaîne JSON, le texte brut, et plus encore.

```csharp
        // Step 4: Perform recognition using English language and the configured options
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);
```

Si vous devez gérer d’autres langues, remplacez `Language.English` par `Language.Spanish`, `Language.French`, etc. Aspose prend en charge plus de 30 langues dès le départ.

---

## Étape 5 : Sortir le résultat – Votre charge utile JSON

Enfin, nous affichons le JSON dans la console. Dans une application réelle, vous l’écririez probablement dans un fichier ou l’enverriez à un service.

```csharp
        // Step 5: Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

L’exécution du programme devrait produire un document JSON similaire à l’extrait ci‑dessous.

```json
{
  "Text": "Total $12.34\nDate 01/01/2024",
  "Words": [
    {
      "Text": "Total",
      "BoundingBox": { "X": 45, "Y": 112, "Width": 60, "Height": 20 }
    },
    {
      "Text": "$12.34",
      "BoundingBox": { "X": 110, "Y": 112, "Width": 70, "Height": 20 }
    },
    {
      "Text": "Date",
      "BoundingBox": { "X": 45, "Y": 140, "Width": 50, "Height": 20 }
    },
    {
      "Text": "01/01/2024",
      "BoundingBox": { "X": 100, "Y": 140, "Width": 120, "Height": 20 }
    }
  ]
}
```

Remarquez comment chaque mot possède maintenant sa **boîte englobante JSON**—parfait pour l’alimenter dans une superposition UI ou un analyseur en aval.

---

## Exemple complet fonctionnel

Voici le programme complet, prêt à copier‑coller. Aucun élément caché, aucun appel externe—juste du C# pur.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Output;

class JsonOutputDemo
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load the image you want to recognize
        var receiptImage = OcrImage.FromFile("YOUR_DIRECTORY/receipt.jpg");

        // 3️⃣ Configure OCR options to get detailed JSON output with word positions
        var ocrOptions = new OcrOptions
        {
            OutputFormat = OutputFormat.Json,
            IncludeBoundingBoxes = true   // include coordinates for each recognized word
        };

        // 4️⃣ Perform recognition using English language and the configured options
        var ocrResult = ocrEngine.Recognize(receiptImage, Language.English, ocrOptions);

        // 5️⃣ Output the resulting JSON string
        System.Console.WriteLine(ocrResult.Json);
    }
}
```

> **Attention à :**  
> • **Erreurs de chemin de fichier** – vérifiez à nouveau l’emplacement de l’image.  
> • **Package NuGet manquant** – assurez‑vous que `Aspose.OCR` est référencé.  
> • **Formats d’image non pris en charge** – privilégiez JPEG, PNG, BMP ou TIFF pour de meilleurs résultats.

---

## Questions fréquentes et cas particuliers

### Puis‑je convertir une **page PDF** en JSON au lieu d’un JPEG ?

Oui. Convertissez d’abord la page PDF en image (par exemple, en utilisant `Aspose.PDF`), puis injectez cette image dans le même pipeline OCR. Le résultat JSON sera identique car l’étape OCR ne s’intéresse qu’aux données raster.

### Que faire si le reçu est flou ?

Augmentez le DPI dans `ocrOptions`. Par exemple :

```csharp
ocrOptions.Dpi = 300; // higher DPI improves accuracy on low‑quality scans
```

Un DPI plus élevé peut augmenter l’utilisation de la mémoire, il faut donc équilibrer qualité et performances.

### J’ai besoin de **plusieurs langues** sur le même reçu (par ex., anglais + espagnol).

Vous pouvez passer un tableau de langues :

```csharp
var ocrResult = ocrEngine.Recognize(receiptImage, new[] { Language.English, Language.Spanish }, ocrOptions);
```

Aspose tentera de reconnaître chaque langue dans l’ordre spécifié.

### Comment écrire le JSON dans un fichier ?

Il suffit de remplacer la ligne `Console.WriteLine` par :

```csharp
System.IO.File.WriteAllText("receipt.json", ocrResult.Json);
```

Vous avez maintenant un fichier persistant que vous pouvez envoyer à d’autres services.

---

## Résumé visuel

![convert image to json example](convert-image-to-json.png "convert image to json example")

*La capture d’écran montre la sortie console du payload JSON après l’exécution de la démo.*

---

## Conclusion

Nous venons de vous montrer comment **convertir une image en JSON** en utilisant Aspose OCR en C#. En configurant `OutputFormat` et `IncludeBoundingBoxes`, vous pouvez **extraire du texte d’une image**, **reconnaître une image de reçu**, et obtenir des **boîtes englobantes JSON** précises pour chaque mot. Le code complet et exécutable se trouve dans l’extrait ci‑dessus, vous pouvez donc l’intégrer immédiatement dans n’importe quel projet .NET.

Et ensuite ? Essayez d’alimenter le JSON dans un visualiseur front‑end qui met en surbrillance chaque mot, ou envoyez les données à un modèle d’apprentissage automatique qui classe les lignes d’articles sur les reçus. Vous pouvez également expérimenter d’autres langues, des réglages DPI plus élevés, ou le traitement par lots de plusieurs images dans une boucle.

Si vous rencontrez des problèmes, rappelez‑vous les astuces concernant les chemins de fichiers, le DPI et les tableaux de langues. N’hésitez pas à laisser un commentaire ou à ouvrir une issue sur le dépôt GitHub que vous créerez pour cette démo. Bon codage, et profitez de la transformation d’images en JSON structuré !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}