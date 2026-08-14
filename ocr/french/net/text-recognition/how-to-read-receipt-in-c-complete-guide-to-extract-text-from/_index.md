---
category: general
date: 2026-02-20
description: Apprenez à lire un reçu en C# en extrayant le texte d’une image et en
  le convertissant en JSON. Code étape par étape utilisant Aspose OCR.
draft: false
keywords:
- how to read receipt
- extract text from image
- convert image to json
- load image file c#
- OCR receipt C#
- Aspose OCR tutorial
language: fr
og_description: Découvrez comment lire un reçu en C# en chargeant un fichier image,
  en extrayant le texte avec Aspose OCR et en convertissant le résultat en JSON. Exemple
  complet de code.
og_title: Comment lire un reçu en C# – Extraire le texte, convertir en JSON
tags:
- C#
- OCR
- Image Processing
- JSON
title: Comment lire un reçu en C# – Guide complet pour extraire le texte d’une image
url: /fr/net/text-recognition/how-to-read-receipt-in-c-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment lire un reçu en C# – Guide complet

Vous vous êtes déjà demandé **comment lire un reçu** à partir d’images de façon programmatique ? Peut‑être que vous développez une application de suivi des dépenses et que vous devez extraire les lignes d’un reçu de supermarché à partir d’une photo. D’après mon expérience, le principal point de douleur est de transformer ce JPEG flou en données structurées réellement exploitables. Bonne nouvelle : avec quelques lignes de C# et Aspose OCR, vous pouvez **extraire du texte d’une image**, puis **convertir l’image en JSON** d’une manière presque magique.

Dans ce tutoriel, vous repartirez avec une solution prête à l’emploi qui **charge un fichier image C#**, exécute l’OCR et génère une charge JSON détaillée. Aucun service externe, aucun appel REST compliqué — juste du code .NET pur que vous pouvez intégrer dans n’importe quel projet console ou ASP.NET. À la fin, vous comprendrez pourquoi chaque étape est importante, comment gérer les cas limites courants (comme les tailles de reçu non standard), et à quoi ressemble réellement la sortie JSON.

## Ce dont vous aurez besoin

- **.NET 6.0 ou version ultérieure** – le code utilise `System.Drawing.Common` qui est pris en charge sous Windows, Linux et macOS.  
- **Aspose.OCR for .NET** – vous pouvez récupérer le package NuGet d’essai gratuit (`Aspose.OCR`) ou utiliser une copie sous licence si vous en avez une.  
- Une **image de reçu d’exemple** (`receipt.jpg`) placée quelque part où votre application peut la lire.  
- L’IDE de votre choix (Visual Studio, Rider, VS Code).  

C’est tout. Pas de configuration supplémentaire, pas de clés API.

---

## Étape 1 – Charger le fichier image C# (Mot‑clé principal en action)

Avant que le moteur OCR ne fasse sa magie, il faut charger l’image en mémoire. C’est l’étape classique « load image file C# » que de nombreux développeurs négligent.

```csharp
using System.Drawing;          // Required for Image
using Aspose.OCR;
using Aspose.OCR.Models;

// Path to your receipt image – adjust as needed
string imagePath = @"C:\Receipts\receipt.jpg";

// Load the image into a System.Drawing.Image object
Image receiptImage = Image.FromFile(imagePath);
```

**Pourquoi c’est important :**  
`Image.FromFile` lit le fichier *une fois* et garde un handle ouvert, ce qui est parfait pour un passage OCR rapide. Si vous traitez de nombreux reçus dans une boucle, envisagez d’utiliser `Image.FromStream` pour éviter de verrouiller le fichier.

> **Astuce pro :** Si vous rencontrez une *FileNotFoundException*, revérifiez le chemin et assurez‑vous que l’image est bien présente. Les chemins relatifs fonctionnent aussi (`"./receipt.jpg"`), mais les chemins absolus sont plus sûrs en production.

---

## Étape 2 – Créer et configurer le moteur OCR

Aspose OCR fournit un `OcrEngine` prêt à l’emploi. Vous n’avez pas besoin d’entraîner un modèle ; la bibliothèque sait déjà lire le texte imprimé, exactement ce que la plupart des reçus utilisent.

```csharp
// Instantiate the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Optional: tweak recognition settings if your receipts are low‑contrast
ocrEngine.Config.Language = OcrLanguage.English;
ocrEngine.Config.DetectOrientation = true;   // Handles rotated receipts
```

**Pourquoi nous définissons ces options :**  
`DetectOrientation` indique au moteur de faire pivoter automatiquement l’image si le reçu a été scanné à l’envers. Définir la langue restreint l’ensemble de caractères, ce qui peut améliorer la précision—surtout quand vous ne avez besoin que de données alphanumériques en anglais.

---

## Étape 3 – Reconnaître l’image et convertir en JSON

Place maintenant la partie amusante : **extraire du texte d’une image** et **convertir l’image en JSON** en un seul appel.

```csharp
// Perform OCR and get the result as a JSON string
string jsonResult = ocrEngine.RecognizeToJson(receiptImage);
```

La méthode `RecognizeToJson` renvoie une structure JSON riche qui comprend :

- `Text` : le texte brut concaténé.  
- `Lines` : un tableau d’objets ligne avec leurs coordonnées.  
- `Words` : chaque mot avec son score de confiance.  
- `Regions` : les boîtes englobantes des blocs de texte détectés.

Vous pouvez désérialiser ce JSON en un objet C# si vous avez besoin d’un accès typé, mais dans de nombreux scénarios, afficher le JSON brut suffit.

---

## Étape 4 – Afficher le JSON (ou le stocker)

Voyons la sortie et discutons de ce qu’on peut en faire.

```csharp
// Write the JSON to the console – perfect for quick debugging
Console.WriteLine(jsonResult);

// Bonus: Save the JSON to a file for later processing
File.WriteAllText("receipt_output.json", jsonResult);
```

### Exemple de sortie

```json
{
  "Text":"Walmart\n123 Main St\nItem A  $2.99\nItem B  $5.49\nTotal   $8.48",
  "Lines":[
    {"Text":"Walmart","BoundingBox":{"X":10,"Y":15,"Width":200,"Height":30}},
    {"Text":"123 Main St","BoundingBox":{"X":10,"Y":50,"Width":180,"Height":25}},
    {"Text":"Item A  $2.99","BoundingBox":{"X":10,"Y":85,"Width":210,"Height":28}},
    {"Text":"Item B  $5.49","BoundingBox":{"X":10,"Y":120,"Width":210,"Height":28}},
    {"Text":"Total   $8.48","BoundingBox":{"X":10,"Y":155,"Width":210,"Height":30}}
  ],
  "Words":[
    {"Text":"Walmart","Confidence":0.99,"BoundingBox":{...}},
    …
  ]
}
```

**Et après ?**  
Analysez le tableau `Lines` pour extraire le montant `Total`, ou transmettez le JSON à un service en aval qui enregistre les écritures de dépenses. Comme le résultat est déjà du JSON, vous pouvez le brancher directement à n’importe quelle base NoSQL, Azure Function ou flux Power Automate.

---

## Étape 5 – Gestion des cas limites courants

Même les meilleurs moteurs OCR ont leurs faiblesses. Voici quelques scénarios que vous pourriez rencontrer en apprenant **comment lire un reçu** à partir d’images.

| Situation | Solution / Recommandation |
|-----------|---------------------------|
| **Reçu à basse résolution (≤ 150 dpi)** | Agrandir d’abord l’image avec `Bitmap` et `Graphics` (`InterpolationMode.HighQualityBicubic`). |
| **Reçu tourné ou incliné** | Conserver `DetectOrientation = true`. Pour une inclinaison sévère, pré‑traiter avec `Image.RotateFlip` ou une bibliothèque tierce comme OpenCV. |
| **Fond coloré (ex. : reçu posé sur une table)** | Convertir en niveaux de gris et augmenter le contraste avant l’OCR (`ImageAttributes`). |
| **Plusieurs reçus sur une même photo** | Rogner chaque région de reçu manuellement ou activer `ocrEngine.Config.RecognizeMultipleRegions = true`. |
| **Fichiers volumineux provoquant OutOfMemory** | Utiliser des blocs `using` pour libérer rapidement les objets `Image`, ou traiter par morceaux. |

```csharp
// Example: simple grayscale conversion
using (Bitmap bmp = new Bitmap(receiptImage))
{
    for (int y = 0; y < bmp.Height; y++)
        for (int x = 0; x < bmp.Width; x++)
        {
            Color c = bmp.GetPixel(x, y);
            int gray = (int)(c.R * 0.3 + c.G * 0.59 + c.B * 0.11);
            bmp.SetPixel(x, y, Color.FromArgb(gray, gray, gray));
        }
    receiptImage = (Image)bmp.Clone();
}
```

---

## Étape 6 – Exemple complet (prêt à copier‑coller)

Voici le programme *complet* que vous pouvez compiler immédiatement. Il inclut toutes les étapes, les directives `using` appropriées et une gestion d’erreurs élégante.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ReceiptReaderDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Load the image file C#
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY\receipt.jpg";

            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"❌ Image not found: {imagePath}");
                return;
            }

            Image receiptImage;
            try
            {
                receiptImage = Image.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"⚠️ Failed to load image: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Create and configure OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine
            {
                Config =
                {
                    Language = OcrLanguage.English,
                    DetectOrientation = true
                }
            };

            // -------------------------------------------------
            // 3️⃣ Recognize and convert to JSON
            // -------------------------------------------------
            string jsonResult;
            try
            {
                jsonResult = ocrEngine.RecognizeToJson(receiptImage);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"🛑 OCR failed: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 4️⃣ Output results
            // -------------------------------------------------
            Console.WriteLine("🗂️ OCR JSON Result:");
            Console.WriteLine(jsonResult);

            // Optionally persist the JSON
            string outputPath = Path.Combine(
                Path.GetDirectoryName(imagePath) ?? ".", "receipt_output.json");
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"✅ JSON saved to {outputPath}");
        }
    }
}
```

**Exécutez‑le :**  
`dotnet run` depuis le dossier du projet. Si tout est correctement configuré, vous verrez le JSON affiché dans la console et enregistré à côté de votre image de reçu.

---

## Conclusion

Nous venons de couvrir **comment lire un reçu** en C# de bout en bout. En chargeant l’image, en configurant Aspose OCR et en appelant `RecognizeToJson`, vous pouvez **extraire du texte d’une image** et **convertir l’image en JSON** sans quasiment aucun code boilerplate. Cette approche passe d’une démonstration d’un seul reçu à un processeur par lots capable de gérer des centaines de reçus chaque nuit.

Prochaines étapes possibles :

- **Analyser le JSON** pour extraire dates, totaux et lignes d’articles (avec `System.Text.Json` ou `Newtonsoft.Json`).  
- **Intégrer à une base de données** (SQL, Cosmos DB) pour stocker automatiquement les enregistrements de dépenses.  
- **Ajouter une interface** (WinForms, WPF ou Blazor) afin que les utilisateurs puissent glisser‑déposer leurs reçus.  
- **Remplacer Aspose OCR** par un autre moteur (Tesseract, Microsoft Azure OCR) si la licence pose problème—tout en conservant le même modèle « load image file C# ».

N’hésitez pas à expérimenter, à casser des choses, puis à revenir ici pour un rappel. Si vous rencontrez un obstacle, la communauté (et les forums Aspose) sont d’excellents endroits où poser vos questions. Bon codage, et profitez de la transformation de ces reçus papier en données propres et recherchables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}