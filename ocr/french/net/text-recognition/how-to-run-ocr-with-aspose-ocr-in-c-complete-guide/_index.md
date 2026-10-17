---
category: general
date: 2026-02-28
description: Comment exécuter l'OCR en C# avec Aspose OCR – apprenez comment extraire
  du texte d'une image, convertir l'image en JSON ou XML en quelques étapes seulement.
draft: false
keywords:
- how to run OCR
- extract text from image
- convert image to json
- convert image to xml
- how to extract text
language: fr
og_description: Comment exécuter l’OCR en C# avec Aspose OCR – découvrez comment extraire
  du texte d’une image et convertir l’image en JSON ou XML avec un exemple prêt à
  l’emploi.
og_title: Comment exécuter l'OCR avec Aspose OCR en C# – Guide complet
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Comment exécuter l'OCR avec Aspose OCR en C# – Guide complet
url: /fr/net/text-recognition/how-to-run-ocr-with-aspose-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# comment exécuter OCR avec Aspose OCR en C# – Guide complet

Si vous vous demandez **comment exécuter OCR** sur une image de reçu en utilisant C#, vous êtes au bon endroit. Dans ce tutoriel, nous allons parcourir **extraction de texte depuis l'image** puis **conversion de l'image en JSON** ou **conversion de l'image en XML** avec Aspose OCR — le tout dans un programme autonome.

Imaginez que vous développez une application de suivi des dépenses et que vous devez extraire les lignes d'articles à partir de reçus photographiés. Saisir manuellement chaque entrée est fastidieux, n'est‑ce pas ? À la fin de ce guide, vous disposerez d'un extrait réutilisable qui lit n'importe quelle image, renvoie du texte structuré, et vous fournit à la fois les représentations JSON et XML prêtes pour le traitement en aval.

## Prérequis

- .NET 6.0 SDK ou version ultérieure (le code fonctionne également avec .NET Framework 4.8)
- Visual Studio 2022 (ou tout éditeur de votre choix)
- Un package NuGet **Aspose.OCR** actif (`Install-Package Aspose.OCR`)
- Une image d'exemple (par ex., `receipt.png`) placée dans un dossier que vous pouvez référencer

Aucune configuration supplémentaire n'est requise ; la bibliothèque inclut tous les modèles OCR nécessaires.

![Image de reçu pour le traitement OCR – comment exécuter OCR](receipt.png)

> *Texte alternatif : Image de reçu pour le traitement OCR – comment exécuter OCR*

## Implémentation étape par étape

Ci-dessous, nous décomposons la solution en parties logiques. Chaque étape explique **pourquoi** nous la faisons, et pas seulement **ce que** le code fait.

### 1️⃣ Initialiser le moteur OCR – la base de **comment exécuter OCR**

La classe `OcrEngine` est le point d'entrée. L'instancier charge les modèles de langue internes et prépare le moteur pour la reconnaissance.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        // This object holds the OCR model and settings.
        var ocrEngine = new OcrEngine();
```

> **Astuce :** Réutiliser le même `OcrEngine` sur plusieurs images réduit la consommation de mémoire et accélère le traitement par lots.

### 2️⃣ Charger l'image – le cœur de **extraction de texte depuis l'image**

Aspose OCR fonctionne avec son propre wrapper `Image`. Utiliser une instruction `using` garantit que le handle du fichier est libéré rapidement.

```csharp
        // Step 2: Load the image you want to analyze
        // Replace YOUR_DIRECTORY with the actual path on your machine.
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");
```

Si l'image est dans un format différent (BMP, TIFF, PDF), la même méthode `Load` la gère — aucune conversion supplémentaire n'est nécessaire.

### 3️⃣ Exécuter la reconnaissance OCR – le cœur de **comment exécuter OCR**

Appeler `Recognize` effectue le travail lourd : analyse de la mise en page, segmentation des caractères et classification spécifique à la langue.

```csharp
        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);
```

Le `OcrResult` retourné contient le texte brut, les scores de confiance, et un arbre de mise en page détaillé qui peut être sérialisé.

### 4️⃣ Convertir l'image en JSON – la façon directe de **conversion de l'image en JSON**

JSON est parfait pour les API web ou les bases NoSQL. La méthode `ToJson` vous fournit une chaîne formatée, facilitant le débogage.

```csharp
        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);
```

Un exemple typique de sortie JSON ressemble à ceci (truncaté pour plus de concision) :

```json
{
  "Text": "Total 12.34",
  "Blocks": [
    {
      "Text": "Total",
      "Confidence": 0.98,
      "Bounds": { "X": 10, "Y": 150, "Width": 45, "Height": 15 }
    },
    {
      "Text": "12.34",
      "Confidence": 0.97,
      "Bounds": { "X": 60, "Y": 150, "Width": 30, "Height": 15 }
    }
  ]
}
```

Vous pouvez maintenant envoyer ce JSON directement à un point d'accès REST ou le stocker dans Azure Cosmos DB.

### 5️⃣ Convertir l'image en XML – lorsque la **conversion de l'image en XML** est requise

Certains systèmes hérités consomment encore du XML. Aspose fournit `ToXml` pour une représentation propre et compatible avec le schéma.

```csharp
        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

Exemple d'extrait XML :

```xml
<OcrResult>
  <Text>Total 12.34</Text>
  <Blocks>
    <Block>
      <Text>Total</Text>
      <Confidence>0.98</Confidence>
      <Bounds X="10" Y="150" Width="45" Height="15" />
    </Block>
    <Block>
      <Text>12.34</Text>
      <Confidence>0.97</Confidence>
      <Bounds X="60" Y="150" Width="30" Height="15" />
    </Block>
  </Blocks>
</OcrResult>
```

Les deux formats conservent les mêmes données hiérarchiques, vous pouvez donc choisir celui qui convient à votre pipeline en aval.

## Pièges courants et comment extraire le texte de manière fiable

Même avec une bibliothèque robuste, les images du monde réel posent des problèmes. Voici trois problèmes que vous pourriez rencontrer ainsi que leurs solutions correspondantes.

### 📏 Images à basse résolution

**Pourquoi c'est important :** Les petites polices se fusionnent, réduisant les scores de confiance.  
**Solution :** Pré‑traiter l'image — agrandir avec `Image.Resize` ou appliquer un filtre de netteté avant de la passer à `Recognize`.

```csharp
using var highRes = image.Resize(2.0, InterpolationMode.HighQualityBicubic);
var result = ocrEngine.Recognize(highRes);
```

### 🌈 Faible contraste

**Pourquoi c'est important :** Le texte clair sur fond sombre perturbe l'algorithme de segmentation.  
**Solution :** Inverser les couleurs ou ajuster la luminosité/contraste via `Image.AdjustBrightnessContrast`.

```csharp
image.AdjustBrightnessContrast(brightness: 30, contrast: 40);
```

### 📄 Documents multilingues

**Pourquoi c'est important :** Le modèle de langue par défaut est l'anglais ; les langues mixtes entraînent une sortie illisible.  
**Solution :** Définissez `ocrEngine.Language = OcrLanguage.Multilingual;` avant la reconnaissance.

```csharp
ocrEngine.Language = OcrLanguage.Multilingual;
```

Aborder ces cas limites garantit que **extraction de texte** depuis n'importe quelle image devienne une routine fiable plutôt qu'un pari.

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être compilé et exécuté. Remplacez simplement `YOUR_DIRECTORY` par le chemin de votre image et appuyez sur F5.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class StructuredOutputDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Optional: improve accuracy for low‑contrast images
        // ocrEngine.Language = OcrLanguage.Multilingual;

        // Step 2: Load the image you want to analyze
        using var image = Image.Load(@"YOUR_DIRECTORY/receipt.png");

        // Step 3: Run OCR recognition on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Retrieve the detailed layout as pretty‑printed JSON
        string jsonOutput = ocrResult.ToJson(prettyPrint: true);
        Console.WriteLine("=== JSON Output ===");
        Console.WriteLine(jsonOutput);

        // Step 5: Retrieve the same information in XML format (optional)
        string xmlOutput = ocrResult.ToXml();
        Console.WriteLine("\n=== XML Output ===");
        Console.WriteLine(xmlOutput);
    }
}
```

**Sortie console attendue** (formatée pour la lisibilité) montre les structures JSON et XML contenant le texte extrait et les boîtes englobantes.

## Récapitulatif – Ce que nous avons couvert

- **comment exécuter OCR** avec Aspose OCR en C#
- Le processus étape par étape pour **extraction de texte depuis l'image**
- Deux options de sérialisation : **conversion de l'image en JSON** et **conversion de l'image en XML**
- Astuces pour gérer les scénarios à basse résolution, faible contraste et multilingues
- Un exemple complet, prêt à copier‑coller, que vous pouvez intégrer à n'importe quel projet .NET

## Et après ?

Maintenant que vous pouvez **extraction de texte** et obtenir des données structurées, envisagez ces idées complémentaires :

- Alimenter le JSON dans une Azure Function qui stocke les reçus dans Cosmos DB.
- Utiliser la sortie XML pour alimenter un système comptable existant basé sur SOAP.
- Combiner Aspose OCR avec un modèle d'apprentissage automatique pour catégoriser automatiquement les types de dépenses.

N'hésitez pas à expérimenter — remplacez `receipt.png` par des factures, cartes de visite ou notes manuscrites. Le même schéma fonctionne à travers

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}