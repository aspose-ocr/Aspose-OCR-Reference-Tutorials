---
category: general
date: 2026-02-11
description: Convertir une image OCR en JSON en C#. Apprenez à extraire le texte d’une
  image, lire un fichier image en C#, formater la sortie JSON et afficher joliment
  le JSON en C# avec Aspose.OCR.
draft: false
keywords:
- ocr image to json
- extract text from image
- read image file c#
- format json output
- pretty print json c#
language: fr
og_description: Convertir une image OCR en JSON en C#. Ce guide montre comment extraire
  le texte d’une image, lire le fichier image en C#, formater la sortie JSON et afficher
  joliment le JSON en C# à l’aide d’Aspose.OCR.
og_title: OCR d'image vers JSON en C# – Guide complet étape par étape
tags:
- OCR
- C#
- JSON
title: OCR d'image vers JSON en C# – Guide complet étape par étape
url: /fr/net/text-recognition/ocr-image-to-json-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr image to json en C# – Guide complet étape par étape

Vous avez déjà eu besoin de **ocr image to json** mais vous ne saviez pas quelle bibliothèque choisir ou comment obtenir un résultat bien formaté ? Vous n'êtes pas seul. Dans de nombreuses applications réelles — numérisation de reçus, vérification d'identité ou archivage simple de documents — vous voudrez extraire le texte d'une image et obtenir une charge utile JSON propre que les services en aval peuvent consommer.

Dans ce tutoriel, nous parcourrons l’ensemble du pipeline : de la lecture d’un fichier image en C# à l’extraction du texte avec Aspose.OCR, en demandant ensuite au moteur une sortie JSON structurée, puis en affichant joliment ce JSON pour le rendre lisible par l’homme. À la fin, vous disposerez d’un extrait autonome, prêt pour la production, que vous pourrez intégrer à n’importe quel projet .NET.  

Nous aborderons également les pièges courants (comme les packs de langues manquants) et montrerons quelques variations rapides — par exemple, passer à une sortie XML ou gérer des PDF multi‑pages. Aucun document externe requis ; tout ce dont vous avez besoin se trouve ici.

## Ce dont vous avez besoin

- **.NET 6+** (le code fonctionne également avec .NET Framework 4.7+)
- **Aspose.OCR for .NET** – installer via NuGet (`Install-Package Aspose.OCR`)
- Une image d’exemple (par ex. `receipt.png`) placée à un endroit accessible
- Une connaissance de base de la syntaxe C# (si vous avez déjà écrit un « Hello World », vous êtes prêt)

> *Astuce :* Si vous êtes sur un serveur CI, définissez `AutomaticResourceDownload = true` afin qu’Aspose télécharge les données de langue à la volée—pas de manipulation manuelle de DLL.

## Étape 1 : Lire le fichier image en C# et créer le moteur OCR  

La première chose que nous faisons est de charger l’image depuis le disque. L’utilisation de `System.Drawing.Image` garde le code court et fonctionne pour PNG, JPEG, BMP et même les TIFF multi‑pages (le moteur sélectionne la première page par défaut).

```csharp
using System.Drawing;          // For Image
using Aspose.OCR;              // Core OCR classes
using Aspose.OCR.Models;       // Language and output enums
using System.Text.Json;        // JSON parsing & pretty‑print

// 1️⃣ Configure the OCR engine – this is where we tell Aspose what language we expect
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // extract text from image in English
    AutomaticResourceDownload = true,        // auto‑download language packs if missing
    OutputFormat = OcrOutputFormat.Json      // ask for JSON rather than plain text
};
```

**Pourquoi c’est important :**  
- `AutomaticResourceDownload` empêche les plantages à l’exécution lorsque le fichier de langue anglaise n’est pas présent localement.  
- Définir `OutputFormat` sur `Json` signifie que le moteur effectue déjà le travail lourd de conversion des résultats OCR bruts en un objet structuré—aucune analyse manuelle de chaîne n’est requise.

## Étape 2 : Exécuter l’OCR et obtenir la sortie JSON  

Nous injectons maintenant le bitmap chargé dans le moteur. La méthode `Recognize` renvoie un `OcrResult` qui contient une propriété `Text` contenant la chaîne JSON.

```csharp
// 2️⃣ Load the image you want to process
using (var receiptImage = Image.FromFile(@"C:\Images\receipt.png"))
{
    // 3️⃣ Perform OCR – this call blocks until the engine finishes
    var ocrResult = ocrEngine.Recognize(receiptImage);

    // 4️⃣ The OCR engine gave us JSON straight away
    string rawJson = ocrResult.Text;
    
    // Optional: write the raw JSON to a file for debugging
    System.IO.File.WriteAllText(@"C:\Temp\ocr_raw.json", rawJson);
}
```

**Cas limite :** Si l’image est corrompue ou que le chemin est incorrect, `Image.FromFile` lève une `FileNotFoundException`. Enveloppez le bloc dans un `try/catch` si vous prévoyez des entrées peu fiables.

## Étape 3 : Analyser et formater le JSON – pretty‑print JSON en C#  

Le JSON brut provenant du moteur OCR est compact et difficile à lire. En utilisant `System.Text.Json`, nous pouvons le désérialiser dans un `JsonDocument`, puis le re‑sérialiser avec indentation.

```csharp
// 5️⃣ Parse the JSON string into a DOM-like structure
using var jsonDoc = JsonDocument.Parse(rawJson);

// 6️⃣ Pretty‑print with indentation (2 spaces by default)
string prettyJson = JsonSerializer.Serialize(
    jsonDoc.RootElement,
    new JsonSerializerOptions { WriteIndented = true });

// 7️⃣ Output to console – you could also send this to an API or a file
Console.WriteLine(prettyJson);

// 8️⃣ Save the pretty JSON for later use
System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
```

**Ce que vous verrez :**  

```json
{
  "Lines": [
    {
      "Text": "Store Name",
      "BoundingBox": { "X": 12, "Y": 5, "Width": 150, "Height": 20 }
    },
    {
      "Text": "Total: $23.45",
      "BoundingBox": { "X": 12, "Y": 200, "Width": 100, "Height": 20 }
    }
  ],
  "Language": "English",
  "Confidence": 0.96
}
```

Le JSON inclut désormais le texte ligne par ligne, les boîtes englobantes, la langue détectée et un score de confiance—parfait pour l’alimenter à des analyses en aval ou à un composant UI.

## Étape 4 : Bonus – Changer le format de sortie ou la langue  

Si vous avez besoin de **format json output** en XML ou de faire de l’OCR sur un reçu espagnol, il suffit d’ajuster la configuration du moteur :

```csharp
ocrEngine.Language = OcrLanguage.Spanish;          // extract text from image in Spanish
ocrEngine.OutputFormat = OcrOutputFormat.Xml;     // ask for XML instead of JSON
```

Le reste du code reste identique ; vous ne changez que l’étape de désérialisation (utilisez `XmlDocument` pour XML).

## Exemple complet fonctionnel  

En rassemblant le tout, voici un fichier unique que vous pouvez copier‑coller dans une application console :

```csharp
// ---------------------------------------------------------------
// ocr_image_to_json_demo.cs
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Text.Json;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Configure OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            AutomaticResourceDownload = true,
            OutputFormat = OcrOutputFormat.Json
        };

        // Path to your image – adjust as needed
        string imagePath = @"C:\Images\receipt.png";

        try
        {
            using (var receiptImage = Image.FromFile(imagePath))
            {
                var ocrResult = ocrEngine.Recognize(receiptImage);
                string rawJson = ocrResult.Text;

                // Parse & pretty‑print
                using var jsonDoc = JsonDocument.Parse(rawJson);
                string prettyJson = JsonSerializer.Serialize(
                    jsonDoc.RootElement,
                    new JsonSerializerOptions { WriteIndented = true });

                Console.WriteLine("=== Pretty‑Printed OCR JSON ===");
                Console.WriteLine(prettyJson);

                // Optional: write to file
                System.IO.File.WriteAllText(@"C:\Temp\ocr_pretty.json", prettyJson);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Error processing image: {ex.Message}");
        }
    }
}
```

L’exécution de ce programme affiche une charge JSON joliment indentée dans la console et l’enregistre dans `C:\Temp\ocr_pretty.json`. Le bloc `try/catch` garantit que même si l’image ne peut pas être lue, vous obtiendrez un message d’erreur clair au lieu d’un plantage silencieux.

## Questions fréquentes et pièges  

- **Que faire si l’OCR renvoie du texte vide ?**  
  En général, cela signifie que l’image est trop bruitée ou que la langue ne correspond pas. Essayez d’augmenter le contraste de l’image ou de changer `Language` en `AutoDetect`.  

- **Puis‑je traiter plusieurs images dans une boucle ?**  
  Absolument. Enveloppez le bloc `using (var img = Image.FromFile(...))` dans une boucle `foreach (var file in Directory.GetFiles(...))` et collectez chaque `prettyJson` dans une liste ou écrivez‑les dans des fichiers séparés.  

- **Le schéma JSON est‑il stable ?**  
  Aspose garantit la compatibilité ascendante pour le format de sortie `Json`, mais vérifiez toujours l’attribut `Version` dans la réponse si vous ciblez une version d’API spécifique.  

- **Ai‑je besoin d’une licence pour Aspose.OCR ?**  
  Une clé d’évaluation gratuite fonctionne jusqu’à 100 pages. En production, achetez une licence et configurez‑la avec `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.  

## Conclusion  

Vous disposez maintenant d’une **solution complète, autonome pour ocr image to json** en C#. En lisant le fichier image, en configurant le moteur OCR, en demandant la sortie JSON et en l’affichant joliment, vous pouvez intégrer l’extraction de texte à n’importe quel service .NET sans vous battre avec des astuces de chaînes.  

À partir d’ici, vous pouvez explorer **extract text from image** pour d’autres types de fichiers (PDF, TIFF multi‑pages), expérimenter avec différentes langues, ou acheminer le JSON vers un magasin NoSQL pour l’analyse. Le ciel est la limite—n’oubliez pas de gérer les erreurs avec grâce et de surveiller la licence si vous montez en échelle.

Bon codage, et que vos pipelines OCR soient toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}