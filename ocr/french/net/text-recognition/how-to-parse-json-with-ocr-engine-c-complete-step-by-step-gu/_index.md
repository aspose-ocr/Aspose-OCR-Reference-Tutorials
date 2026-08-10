---
category: general
date: 2026-03-17
description: Apprenez à analyser le JSON des résultats OCR en C#. Ce tutoriel couvre
  comment extraire le texte, charger l'image pour l'OCR, exécuter la reconnaissance
  OCR et utiliser le moteur OCR en C# efficacement.
draft: false
keywords:
- how to parse json
- how to extract text
- load image for OCR
- run OCR recognition
- use OCR engine C#
language: fr
og_description: Comment analyser le JSON issu de la sortie OCR en C#. Suivez notre
  guide pour extraire le texte, charger l’image pour l’OCR, lancer la reconnaissance
  OCR et utiliser le moteur OCR en C#.
og_title: Comment analyser JSON avec le moteur OCR C# – Tutoriel complet
tags:
- C#
- OCR
- JSON
- Image Processing
title: Comment analyser le JSON avec le moteur OCR C# – Guide complet étape par étape
url: /fr/net/text-recognition/how-to-parse-json-with-ocr-engine-c-complete-step-by-step-gu/
---

code block placeholders.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment analyser le JSON avec le moteur OCR C# – Guide complet étape par étape

Vous vous êtes déjà demandé **comment analyser le json** qui provient directement d’un moteur OCR ? Vous n’êtes pas seul. La plupart des développeurs rencontrent le même problème : obtenir du JSON brut, puis déterminer la meilleure façon d’extraire les éléments utiles comme les scores de confiance ou le texte réel. Dans ce guide, nous verrons comment charger une image pour l’OCR, exécuter la reconnaissance OCR, et enfin **comment analyser le json** de manière propre et maintenable.

À la fin du tutoriel, vous serez capable de :

* Charger une image pour l’OCR en quelques lignes de code.  
* Exécuter la reconnaissance OCR avec un moteur OCR C#.  
* **Comment extraire le texte** et d’autres métadonnées du payload JSON.  
* Gérer les cas limites courants (champs manquants, formats inattendus) sans plantage.

Aucune documentation externe requise — tout ce dont vous avez besoin se trouve ici.

## Pré‑requis

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou supérieur (le code compile également sous .NET Framework 4.7+).  
* Une référence à la bibliothèque OCR que vous utilisez (l’exemple utilise une classe hypothétique `OcrEngine`).  
* Le package NuGet `Newtonsoft.Json` pour la gestion du JSON (`Install-Package Newtonsoft.Json`).  
* Un fichier image (par ex., `passport.png`) placé quelque part où votre application peut le lire.

> **Astuce pro :** Si vous utilisez un SDK OCR commercial, vérifiez que le format de sortie JSON est activé — la plupart des fournisseurs l’exposent via une propriété de configuration comme `ocrEngine.Config.OutputFormat`.

## Étape 1 – Créer et configurer le moteur OCR (Mot‑clé principal en action)

La première chose à faire est d’instancier le moteur OCR et de lui indiquer de renvoyer du JSON. C’est ici que la phrase **how to parse json** apparaît pour la première fois dans notre code, car le moteur nous fournira une chaîne JSON que nous analyserons ensuite.

```csharp
using System;
using Newtonsoft.Json.Linq;   // For JSON parsing
// Assume OcrEngine, OutputFormat, and ImageStream live in the OCR SDK namespace
using OcrSdk;                  // <-- replace with the real namespace

// Step 1: Create an OCR engine instance and set JSON output
var ocrEngine = new OcrEngine();
ocrEngine.Config.OutputFormat = OutputFormat.Json;
```

**Pourquoi c’est important :** Définir `OutputFormat` à `Json` garantit que la réponse contient à la fois le texte reconnu **et** des métadonnées utiles comme les scores de confiance. Si vous oubliez cette étape, vous obtiendrez du texte brut à la place, et **how to parse json** devient un point sans intérêt.

## Étape 2 – Charger l’image pour l’OCR

Nous chargeons maintenant l’image que nous voulons analyser. C’est l’endroit exact où le mot‑clé secondaire **load image for OCR** brille.

```csharp
// Step 2: Load the image you want to recognize
// Make sure the path points to a real file; otherwise an exception is thrown.
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY\passport.png");
```

> **Et si le fichier n’est pas présent ?** Enveloppez l’appel dans un `try/catch` et affichez un message convivial — votre application ne plantera pas et les utilisateurs sauront ce qui s’est mal passé.

## Étape 3 – Exécuter la reconnaissance OCR

Avec le moteur prêt et l’image chargée, l’étape logique suivante est d’exécuter le processus de reconnaissance. Cela satisfait le mot‑clé secondaire **run OCR recognition**.

```csharp
// Step 3: Execute OCR and get the raw result object
var ocrResult = ocrEngine.Recognize();
```

La propriété `ocrResult.Text` contient maintenant une chaîne JSON. Si vous l’imprimez dans la console, vous verrez quelque chose comme :

```json
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}
```

## Étape 4 – Comment extraire le texte (et d’autres champs) du JSON

Voici le cœur du tutoriel : **how to parse json** et **how to extract text** du payload OCR. Nous utiliserons `Newtonsoft.Json.Linq.JObject` pour sa flexibilité.

```csharp
// Step 4: Output the raw JSON (optional, helps debugging)
Console.WriteLine("Raw OCR JSON:");
Console.WriteLine(ocrResult.Text);
Console.WriteLine();

// Step 5: Parse the JSON into a JObject
JObject jsonObject = JObject.Parse(ocrResult.Text);

// Extract the overall confidence score
var overallConfidence = jsonObject["OverallConfidence"]?.Value<double>() ?? 0.0;
Console.WriteLine($"Overall confidence: {overallConfidence:P0}");

// Extract the text from the first page (how to extract text)
string pageText = jsonObject["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
Console.WriteLine("Extracted text:");
Console.WriteLine(pageText);
```

**Pourquoi utiliser `JObject` ?** Il vous permet de naviguer en toute sécurité dans l’arbre JSON sans définir une classe modèle C# complète. Les opérateurs conditionnels null (`?.`) vous protègent des `NullReferenceException` si le moteur OCR omet un champ.

### Gestion des cas limites

* **Champs manquants :** Le motif `?.Value<T>() ?? default` renvoie une valeur de secours sensée.  
* **Pages multiples :** Parcourez `jsonObject["Pages"]` si vous attendez plus d’une page.  
* **Confiance non numérique :** Utilisez `double.TryParse` si le SDK renvoie parfois une chaîne.

## Étape 5 – Regrouper le tout dans une méthode réutilisable

Pour éviter de copier‑coller le même code boilerplate, encapsulez le flux complet dans une méthode d’aide. Cela montre également **use OCR engine C#** de façon propre et réutilisable.

```csharp
public static void RunOcrAndParseJson(string imagePath)
{
    // 1️⃣ Create engine & set JSON output
    var engine = new OcrEngine();
    engine.Config.OutputFormat = OutputFormat.Json;

    // 2️⃣ Load image (load image for OCR)
    engine.Image = ImageStream.FromFile(imagePath);

    // 3️⃣ Run OCR (run OCR recognition)
    var result = engine.Recognize();

    // 4️⃣ Show raw JSON (optional)
    Console.WriteLine("=== Raw JSON ===");
    Console.WriteLine(result.Text);
    Console.WriteLine();

    // 5️⃣ Parse JSON (how to parse json)
    JObject obj = JObject.Parse(result.Text);

    // 6️⃣ Extract useful data (how to extract text)
    double confidence = obj["OverallConfidence"]?.Value<double>() ?? 0.0;
    string text = obj["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;

    Console.WriteLine($"Overall confidence: {confidence:P0}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(text);
}
```

Vous pouvez maintenant appeler `RunOcrAndParseJson(@"C:\Images\passport.png");` depuis `Main` ou n’importe quelle autre partie de votre application.

## Exemple complet fonctionnel

Voici un programme console complet et autonome que vous pouvez copier‑coller dans un nouveau `.csproj`. Il inclut toutes les pièces dont nous avons parlé, ainsi qu’un peu de gestion d’erreurs.

```csharp
// File: Program.cs
using System;
using Newtonsoft.Json.Linq;
using OcrSdk;               // Replace with the actual namespace of your OCR library

class Program
{
    static void Main()
    {
        try
        {
            // Adjust the path to point at a real image on your machine
            string imagePath = @"YOUR_DIRECTORY\passport.png";

            RunOcrAndParseJson(imagePath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Unexpected error: {ex.Message}");
        }
    }

    /// <summary>
    /// Demonstrates how to parse JSON returned by an OCR engine,
    /// and how to extract text, confidence, and other metadata.
    /// </summary>
    /// <param name="imagePath">Full path to the image file.</param>
    public static void RunOcrAndParseJson(string imagePath)
    {
        // 1️⃣ Initialize OCR engine (use OCR engine C#)
        var engine = new OcrEngine();
        engine.Config.OutputFormat = OutputFormat.Json;

        // 2️⃣ Load image for OCR
        engine.Image = ImageStream.FromFile(imagePath);

        // 3️⃣ Run OCR recognition
        var result = engine.Recognize();

        // 4️⃣ Print raw JSON (helps debugging)
        Console.WriteLine("=== Raw OCR JSON ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // 5️⃣ Parse JSON (how to parse json)
        JObject json = JObject.Parse(result.Text);

        // 6️⃣ Extract overall confidence
        double overallConf = json["OverallConfidence"]?.Value<double>() ?? 0.0;
        Console.WriteLine($"Overall confidence: {overallConf:P0}");

        // 7️⃣ Extract text from first page (how to extract text)
        string firstPageText = json["Pages"]?[0]?["Text"]?.Value<string>() ?? string.Empty;
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(firstPageText);
    }
}
```

**Sortie attendue** (en supposant que l’OCR a réussi) :

```
=== Raw OCR JSON ===
{
  "OverallConfidence": 0.92,
  "Pages": [
    {
      "Text": "John Doe\nPassport No: 123456789",
      "Confidence": 0.95
    }
  ]
}

Overall confidence: 92%
=== Extracted Text ===
John Doe
Passport No: 123456789
```

Si l’image ne peut pas être lue, le SDK lèvera une exception que nous attrapons dans `Main`, affichant une erreur conviviale au lieu de planter.

## Questions fréquentes (FAQ)

**Q : Et si le moteur OCR renvoie un tableau de pages ?**  
R : Parcourez `json["Pages"]` et concaténez chaque valeur `["Text"]`, ou traitez‑les individuellement selon votre cas d’usage.

**Q : Puis‑je désérialiser le JSON dans une classe C# typée ?**  
R : Absolument. Définissez une structure de classe correspondant au schéma JSON et utilisez `JsonConvert.DeserializeObject<YourRootClass>(result.Text)`. Cela vous donne une sécurité à la compilation mais nécessite de garder le modèle synchronisé avec la sortie du SDK.

**Q : Cela fonctionne‑t‑il avec des API OCR asynchrones ?**  
R : Oui. Remplacez `engine.Recognize()` par `await engine.RecognizeAsync()` et faites de `RunOcrAndParseJson` une méthode `async Task`. La partie parsing JSON reste identique.

**Q : Comment enregistrer le JSON dans un fichier pour une analyse ultérieure ?**  
R : Après avoir récupéré `result.Text`, appelez `File.WriteAllText(@"output.json", result.Text);`. Vous pouvez ensuite le recharger avec `JObject.Parse(File.ReadAllText(...))`.

## Suivant

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}