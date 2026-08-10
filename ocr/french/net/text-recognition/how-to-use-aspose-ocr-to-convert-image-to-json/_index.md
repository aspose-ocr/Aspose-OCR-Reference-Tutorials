---
category: general
date: 2026-03-15
description: Comment utiliser Aspose OCR pour extraire du texte à partir d'images
  et convertir une image en JSON en C#. Apprenez à reconnaître le texte à partir de
  PNG et à obtenir rapidement une sortie structurée.
draft: false
keywords:
- how to use aspose
- convert image to json
- extract text from image
- recognize text from png
- how to extract ocr
language: fr
og_description: Comment utiliser Aspose OCR pour extraire du texte d'images et convertir
  une image en JSON en C#. Ce guide vous accompagne dans la reconnaissance de texte
  à partir de PNG et l'obtention d'une sortie structurée.
og_title: Comment utiliser Aspose OCR pour convertir une image en JSON
tags:
- Aspose
- OCR
- C#
- JSON
title: Comment utiliser Aspose OCR pour convertir une image en JSON
url: /fr/net/text-recognition/how-to-use-aspose-ocr-to-convert-image-to-json/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser Aspose OCR pour convertir une image en JSON

Comment utiliser Aspose OCR est une question fréquente lorsque les développeurs doivent extraire du texte à partir d’images. Si vous cherchez à **convertir une image en JSON** ou à **reconnaître du texte depuis un PNG**, ce guide vous couvre — pas de blabla, juste une solution pratique de bout en bout.

Dans les quelques minutes qui suivent, nous passerons en revue tout ce dont vous avez besoin : installer la bibliothèque, configurer le moteur pour une sortie JSON, charger un reçu PNG, exécuter l’OCR, puis écrire le résultat dans un fichier `.json`. À la fin, vous pourrez **extraire du texte d’une image** avec un seul appel de méthode, et vous comprendrez pourquoi chaque étape est importante.

> **Astuce :** Aspose OCR fonctionne avec une large gamme de formats d’image (PNG, JPEG, BMP, TIFF). Le même code ci‑dessous les gère tous, vous n’avez donc pas à écrire de logique spécifique à chaque format.

## Ce dont vous aurez besoin

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Framework 4.6+)  
- Un package NuGet Aspose.OCR valide (essai gratuit ou licence)  
- Un fichier image que vous souhaitez traiter (par ex. `receipt.png`)  
- Visual Studio, VS Code ou tout éditeur C# de votre choix  

C’est tout — aucune dépendance supplémentaire, aucun service externe. Prêt ? C’est parti.

![comment utiliser le moteur OCR Aspose](image-placeholder.png "comment utiliser le moteur OCR Aspose")

## Comment utiliser Aspose OCR – Configurer la sortie JSON

La première chose à faire lorsque vous **comment utilisez aspose** pour l’OCR est de créer une instance `OcrEngine` et de lui indiquer d’émettre du JSON. Ce petit commutateur de configuration vous évite d’avoir à sérialiser manuellement le résultat plus tard.

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine – this is the core object that does the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell Aspose to give us JSON instead of plain text.
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Load the image you want to recognize.
        var inputImage = Image.FromFile(@"YOUR_DIRECTORY/receipt.png");

        // 4️⃣ Run the OCR process.
        var ocrResult = ocrEngine.Recognize(inputImage);

        // 5️⃣ Save the JSON payload to disk.
        File.WriteAllText(@"YOUR_DIRECTORY/receipt.json", ocrResult.Text);

        // 6️⃣ Let the developer know we’re done.
        Console.WriteLine("JSON saved.");
    }
}
```

**Pourquoi c’est important :** Définir `OutputFormat` sur `Json` signifie que le moteur OCR structure déjà le texte en une hiérarchie de pages, de lignes et de mots. Vous n’avez plus besoin d’analyser des chaînes brutes par la suite, ce qui rend le traitement en aval — comme l’alimentation d’une base de données — beaucoup plus propre.

## Convertir une image en JSON avec Aspose OCR

Maintenant que le moteur est configuré, parlons plus en détail de la partie **convertir une image en JSON**.

1. **Charger l’image** – `Image.FromFile` fonctionne pour tout format supporté. Si vous travaillez avec un flux (par ex. un fichier téléchargé), vous pouvez utiliser `Image.FromStream` à la place.  
2. **Exécuter `Recognize`** – cette méthode renvoie un objet `OcrResult`. Parce que nous avons défini la sortie en JSON, `ocrResult.Text` contient déjà une chaîne JSON.  
3. **Écrire le fichier** – `File.WriteAllText` est la façon la plus simple de persister le JSON. Si vous devez le stocker dans un bucket cloud, remplacez simplement cette ligne par l’appel SDK approprié.

### Exemple de sortie JSON attendue

Une charge JSON typique ressemble à ceci (truncée pour la brièveté) :

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Lines": [
        {
          "Words": [
            { "Text": "Total", "Confidence": 0.99 },
            { "Text": "$12.34", "Confidence": 0.98 }
          ]
        }
      ]
    }
  ]
}
```

Vous pouvez maintenant injecter cette structure dans n’importe quel système en aval — qu’il s’agisse d’un outil de reporting, d’un modèle d’apprentissage automatique ou d’un simple fichier de journal.

## Extraire du texte d’une image avec Aspose OCR

Si vous avez seulement besoin de la chaîne brute (c’est‑à‑dire que le JSON ne vous intéresse pas), basculez simplement le format de sortie vers du texte simple :

```csharp
ocrEngine.Configuration.OutputFormat = OutputFormat.PlainText;
var plainResult = ocrEngine.Recognize(inputImage);
Console.WriteLine(plainResult.Text);
```

**Quand choisir le texte simple ?**  
- Débogage rapide ou affichage console.  
- Scénarios où vous appliquerez un post‑traitement personnalisé (par ex. extraction par expression régulière).  

Mais rappelez‑vous, **extraire du texte d’une image** en utilisant le JSON vous fournit des données de position — utiles pour mettre en évidence le texte dans une UI ou aligner avec des champs de formulaire.

## Reconnaître du texte depuis des fichiers PNG

Le PNG est un format sans perte, ce qui donne souvent une meilleure précision OCR comparé aux JPEG fortement compressés. Voici une petite checklist pour vous assurer d’obtenir les meilleurs résultats lorsque vous **reconnaissez du texte depuis un PNG** :

| Élément de checklist | Pourquoi cela aide |
|----------------------|--------------------|
| Utiliser un DPI de 300+ | Une résolution plus élevée donne au moteur plus de pixels à analyser. |
| Garder l’image en niveaux de gris | Réduit le bruit ; Aspose OCR convertit automatiquement, mais le pré‑traitement peut accélérer les choses. |
| Supprimer le bruit de fond | Un fond propre améliore les scores de confiance. |

Si vous rencontrez de faibles scores de confiance, essayez d’augmenter le DPI ou d’appliquer un filtre de seuillage simple avant de transmettre l’image à Aspose.

## Comment extraire les résultats OCR de façon programmatique

Au‑delà de la simple sauvegarde du JSON, vous pourriez vouloir lire programmatique­ment des champs spécifiques — par exemple le montant total sur un reçu. Parce que le JSON contient une hiérarchie, vous pouvez le désérialiser dans un objet C# :

```csharp
using System.Text.Json;

// Assuming ocrResult.Text contains the JSON string
var ocrData = JsonSerializer.Deserialize<OcrResponse>(ocrResult.Text);

// Example class definitions (simplified)
public class OcrResponse
{
    public Page[] Pages { get; set; }
}
public class Page
{
    public int PageNumber { get; set; }
    public Line[] Lines { get; set; }
}
public class Line
{
    public Word[] Words { get; set; }
}
public class Word
{
    public string Text { get; set; }
    public double Confidence { get; set; }
}
```

Vous pouvez alors interroger `ocrData` avec LINQ :

```csharp
var totalLine = ocrData.Pages
    .SelectMany(p => p.Lines)
    .FirstOrDefault(l => l.Words.Any(w => w.Text.Equals("Total", StringComparison.OrdinalIgnoreCase)));

if (totalLine != null)
{
    var amount = totalLine.Words
        .FirstOrDefault(w => w.Text.StartsWith("$"))
        ?.Text;
    Console.WriteLine($"Extracted amount: {amount}");
}
```

**Pourquoi cela fonctionne :** Le JSON indique déjà où chaque mot se trouve sur la page, vous permettant de localiser de façon fiable les champs même si la mise en page change légèrement.

## Cas limites et pièges courants

- **Résultat nul** : Si `ocrEngine.Recognize` renvoie `null`, l’image est peut‑être non supportée ou corrompue. Protégez toujours contre cela :

  ```csharp
  var ocrResult = ocrEngine.Recognize(inputImage);
  if (ocrResult == null) throw new InvalidOperationException("OCR failed – check the image path.");
  ```

- **Fichiers volumineux** : Pour des images de plusieurs mégaoctets, envisagez de diffuser l’image ou de la redimensionner avant l’OCR afin d’éviter une consommation excessive de mémoire.

- **Problèmes de licence** : La version d’essai ajoute un filigrane à la sortie. Assurez‑vous de charger votre licence tôt dans le programme :

  ```csharp
  Aspose.OCR.License license = new Aspose.OCR.License();
  license.SetLicense("Aspose.OCR.lic");
  ```

- **Scripts non latins** : Aspose OCR prend en charge de nombreuses langues, mais vous devez définir la propriété `Language` en conséquence (par ex. `ocrEngine.Configuration.Language = Language.English;`).

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.OCR;
using Aspose.OCR.Config;
using System;
using System.IO;

class JsonOutputExample
{
    static void Main()
    {
        // Load your Aspose license (optional for trial)
        // var license = new Aspose.OCR.License();
        // license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Set output to JSON – this is the key step for convert image to JSON
        ocrEngine.Configuration.OutputFormat = OutputFormat.Json;

        // 3️⃣ Optional: improve accuracy for PNG files
        ocrEngine.Configuration.Dpi = 300; // higher DPI = better results

        // 4️⃣ Load the image you want to process
        var inputImagePath = @"YOUR_DIRECTORY/receipt.png";
        if (!File.Exists(inputImagePath))
            throw new FileNotFoundException($"Image not found: {inputImagePath}");

        var inputImage = Image.FromFile(inputImagePath);

        // 5️⃣ Run OCR – this is where we actually extract text from image
        var ocrResult = ocrEngine.Recognize(inputImage);
        if (ocrResult == null)
            throw new InvalidOperationException("OCR

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}