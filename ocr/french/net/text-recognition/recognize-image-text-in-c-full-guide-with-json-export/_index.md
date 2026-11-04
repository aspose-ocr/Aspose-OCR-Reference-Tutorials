---
category: general
date: 2026-04-06
description: Reconnaître le texte d’une image avec Aspose OCR en C#. Apprenez comment
  extraire le texte, charger un fichier image en C# et écrire du JSON en C# avec un
  exemple simple étape par étape.
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: fr
og_description: reconnaître le texte d'image avec Aspose OCR en C#. Ce guide montre
  comment extraire du texte, charger un fichier image en C# et écrire du JSON en C#
  rapidement.
og_title: Reconnaître le texte d'image en C# – Guide complet étape par étape
tags:
- OCR
- C#
- Aspose
title: Reconnaître le texte d'image en C# – Guide complet avec export JSON
url: /fr/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître le texte d'image en C# – Guide complet étape par étape

Vous avez déjà eu besoin de **reconnaître le texte d'image** à partir d'un reçu numérisé mais vous ne saviez pas quelle bibliothèque choisir ? Vous n'êtes pas le seul. Dans de nombreuses applications réelles — suiveurs de dépenses, processeurs de factures, même outils d'accessibilité — extraire les mots d'une image est le premier obstacle.  

Dans ce tutoriel, nous allons parcourir une solution pratique qui **reconnaît le texte d'image** en utilisant la bibliothèque Aspose OCR, montre **comment extraire du texte**, démontre **comment charger un fichier image c#** correctement, et enfin **écrit du json en c#** afin que vous puissiez stocker ou transmettre les résultats. À la fin, vous disposerez d’une application console prête à l’emploi qui transforme n’importe quel PNG en une charge JSON bien structurée.

---

## Ce dont vous avez besoin

- **.NET 6+** (le code fonctionne également avec .NET Framework 4.8, mais .NET 6 est le meilleur choix).
- **Aspose.OCR for .NET** package NuGet. Installez‑le avec `dotnet add package Aspose.OCR`.
- Une image d'exemple (`input.png`) placée à un endroit accessible à votre application.  
- Visual Studio 2022 ou tout éditeur de votre choix — aucune astuce d'IDE sophistiquée requise.

> Astuce : Conservez vos fichiers image dans un dossier nommé `Resources` à l'intérieur du projet ; cela maintient les chemins propres et évite les maux de tête du type « fichier introuvable ».

---

## Étape 1 : reconnaître le texte d'image – Charger le fichier image

Avant que le moteur OCR ne fasse sa magie, vous devez **charger le fichier image c#** en toute sécurité. La méthode `Image.FromFile` lève une exception si le chemin est incorrect ou si le fichier n’est pas dans un format pris en charge, nous allons donc nous en prémunir.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*Pourquoi c’est important* : charger l’image à l’intérieur d’un bloc `using` garantit que les ressources GDI+ non gérées sont libérées rapidement, évitant les fuites de mémoire dans les services de longue durée.

---

## Étape 2 : comment extraire du texte avec Aspose OCR

Maintenant que le bitmap est en mémoire, nous le transmettons au moteur **reconnaître le texte d'image**. Le `OcrEngine` d’Aspose est simple : instancier, appeler `Recognize`, et vous obtenez un objet `OcrResult` qui contient le texte brut, les scores de confiance et même les boîtes englobantes.

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*Explication* : la méthode `Recognize` exécute le réseau neuronal intégré. Elle fonctionne mieux avec des images à fort contraste, 300 DPI. Si vous lui fournissez une photo floue, la confiance diminue — envisagez un pré‑traitement (redressement, binarisation) pour le code de production.

---

## Étape 3 : écrire du JSON en C# – Exporter le résultat OCR

La plupart des API attendent du JSON, nous allons donc **écrire du json en c#** en utilisant le `JsonExport` d’Aspose. La bibliothèque sérialise l’ensemble du `OcrResult`, en conservant les informations de ligne et les valeurs de confiance.

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### Sortie JSON attendue

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*Pourquoi le JSON ?* Il est indépendant du langage, facile à désérialiser, et conserve les métadonnées OCR détaillées dont vous pourriez avoir besoin pour la validation en aval.

---

## Étape 4 : programme complet et exécutable

En assemblant les pièces, voici l’application console complète. Copiez‑collez, restaurez les packages NuGet, et appuyez sur **F5**.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

Exécutez le programme et ouvrez `Resources/output.json` — vous devriez voir une représentation JSON bien structurée de tout ce que le moteur a reconnu.

---

## Gestion des cas limites courants

| Situation | Action | Pourquoi |
|-----------|--------|----------|
| **L'image est nulle ou corrompue** | Encapsulez `Image.FromFile` dans un try/catch et consignez l'exception. | Empêche l'application de planter et vous fournit un message d'erreur clair. |
| **Scores de confiance faibles** | Vérifiez `ocrResult.Words[i].Confidence`. Si inférieur à 0,75, envisagez un pré‑traitement (augmenter le DPI, affiner). | Améliore la fiabilité pour les processus en aval comme l'extraction de montants. |
| **Fichiers volumineux (>10 Mo)** | Réduisez l'échelle de l'image avant l'OCR (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`). | Réduit la pression mémoire et accélère la reconnaissance. |
| **Documents multilingues** | Définissez `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | Permet au moteur de détecter les caractères des deux langues. |

---

## Bonus : visualiser le résultat OCR (optionnel)

Si vous souhaitez voir où chaque mot se situe sur l’image, vous pouvez dessiner des boîtes englobantes :

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

Le `annotated.png` résultant affichera des rectangles rouges autour de chaque mot reconnu — pratique pour le débogage.

---

## Conclusion

Nous venons de **reconnaître le texte d'image** en C# du début à la fin : charger le fichier image, invoquer Aspose OCR pour **comment extraire du texte**, et enfin **écrire du json en c#** afin que les données puissent circuler partout. L’exemple complet fonctionne immédiatement, et les astuces supplémentaires vous aident à gérer les reçus flous, les fichiers volumineux ou les scans multilingues.

Et après ? Essayez de remplacer Aspose par un autre moteur (Tesseract, Microsoft OCR) et comparez les scores de confiance, ou injectez le JSON dans une base de données pour le reporting des dépenses. Vous pourriez également étendre l’application console en une API Web ASP .NET Core qui accepte les téléchargements d'images et renvoie du JSON instantanément.

Des questions sur la mise à l’échelle, la gestion des erreurs ou l’intégration avec Azure Functions ? Laissez un commentaire ou contactez‑moi sur GitHub. Bon codage, et que votre OCR reste toujours net !

---

![Capture d’écran de la sortie JSON OCR – exemple de reconnaissance de texte d'image](https://example.com/ocr-example.png "exemple de reconnaissance de texte d'image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}