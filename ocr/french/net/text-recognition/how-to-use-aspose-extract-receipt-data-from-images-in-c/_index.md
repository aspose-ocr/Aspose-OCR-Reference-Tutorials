---
category: general
date: 2026-04-04
description: Apprenez à utiliser Aspose pour extraire les données d’un reçu, charger
  l’image du reçu et effectuer la reconnaissance OCR de l’image du reçu avec un exemple
  complet en C#. Guide étape par étape pour les développeurs.
draft: false
keywords:
- how to use aspose
- extract receipt data
- how to extract receipt
- load receipt image
- ocr receipt image
language: fr
og_description: Comment utiliser Aspose pour extraire les données d’un reçu à partir
  d’une image de reçu numérisée. Code C# complet, explications et conseils pour le
  traitement OCR d’images de reçus.
og_title: Comment utiliser Aspose – Extraire les données de reçus à partir d'images
tags:
- Aspose
- OCR
- C#
- Receipt Processing
title: Comment utiliser Aspose – Extraire les données de reçus à partir d’images en
  C#
url: /fr/net/text-recognition/how-to-use-aspose-extract-receipt-data-from-images-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use Aspose – Extract Receipt Data from Images in C#

Vous êtes-vous déjà demandé **comment utiliser Aspose** pour extraire des informations structurées à partir d’une photo de reçu ? Vous n’êtes pas le seul. Que vous construisiez une application de suivi des dépenses ou que vous automatisiez la saisie de factures, le problème est le même : vous avez un PNG ou JPEG, et vous avez besoin du nom du commerçant, de la date et du montant total sans saisie manuelle.

Voici le point essentiel — Aspose.OCR rend toute cette chaîne de traitement un jeu d’enfant. Dans ce tutoriel, nous allons charger une image de reçu, exécuter l’OCR, puis extraire les données du reçu en quelques lignes de C#. À la fin, vous disposerez d’un programme console exécutable qui affiche le commerçant, la date et le montant total directement dans la console.

> **Quick win :** Si vous avez juste besoin du code, passez directement à la section « Exemple complet fonctionnel » en bas et copiez‑collez.

## What You’ll Need

- **.NET 6.0 ou version ultérieure** (l’API fonctionne avec .NET Core et .NET Framework)
- **Aspose.OCR for .NET** package NuGet (`Install-Package Aspose.OCR`)
- Une image de reçu d’exemple (PNG, JPG ou BMP) enregistrée localement
- Visual Studio 2022 ou tout éditeur supportant les projets C#

Aucune autre bibliothèque tierce n’est requise. La seule condition préalable est une compréhension de base des applications console C# — si vous avez déjà écrit « Hello World », vous êtes prêt.

## Step 1 – Install and Reference Aspose.OCR

Pour **how to use Aspose**, vous devez d’abord ajouter la bibliothèque à votre projet. Ouvrez la console du gestionnaire de packages et exécutez :

```powershell
Install-Package Aspose.OCR
```

Vous pouvez également utiliser l’interface NuGet et rechercher « Aspose.OCR ». Une fois installé, ajoutez les espaces de noms requis en haut de votre fichier :

```csharp
using Aspose.OCR;
using Aspose.OCR.Structured;
```

> **Pro tip :** Gardez vos packages NuGet à jour. À ce jour (avril 2026), la dernière version stable est la 23.11.0, qui inclut des améliorations de performances pour l’OCR sur les reçus haute résolution.

## Step 2 – Load the Receipt Image

Lorsque vous **load receipt image** des fichiers, vous avez deux sources courantes : un chemin local ou un flux provenant d’une requête web. Pour ce tutoriel, nous resterons simples et lirons depuis le disque :

```csharp
// Step 2: Load the receipt image to be processed
var ocrEngine = new OcrEngine
{
    Language = Language.English // set language for better accuracy
};

ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.png");
```

Remplacez `YOUR_DIRECTORY/receipt.png` par le chemin réel de votre fichier de reçu. Si vous gérez des téléchargements d’utilisateurs, vous pouvez fournir un `MemoryStream` à `ImageStream.FromStream`.

> **Why this matters :** Spécifier la langue (English) indique au moteur OCR quel jeu de caractères attendre, réduisant les fausses reconnaissances — particulièrement important lorsque vous **ocr receipt image** contenant des chiffres et des symboles.

## Step 3 – Run OCR and Capture Layout Information

L’étape OCR fait plus que simplement renvoyer du texte brut ; elle capture également la mise en page, ce qui est crucial pour l’extraction structurée ultérieure.

```csharp
// Step 3: Run OCR to generate text and layout information (required for structured extraction)
ocrEngine.Recognize();
```

Après que `Recognize()` soit terminé, le `ocrEngine` possède à la fois le texte simple et les données positionnelles de chaque mot. C’est la base de l’étape suivante où nous demanderons à Aspose « **how to extract receipt** » automatiquement.

## Step 4 – Initialize the Layout Recognizer

Aspose fournit une classe `LayoutRecognizer` qui sait comment les reçus sont généralement organisés (commerçant en haut, ligne de date, total en bas). Vous transmettez simplement le moteur OCR configuré :

```csharp
// Step 4: Initialize the layout recognizer with the OCR engine
var layoutRecognizer = new LayoutRecognizer(ocrEngine);
```

En interne, le reconnaisseur applique un ensemble d’heuristiques — comme la recherche de symboles monétaires ou de motifs de date—pour mapper le texte brut aux champs sémantiques.

## Step 5 – Extract Structured Receipt Data

Voici la partie agréable : **extract receipt data**. Un seul appel de méthode fait le gros du travail :

```csharp
// Step 5: Extract structured receipt data (merchant, date, total amount)
var receiptData = layoutRecognizer.ExtractReceiptData();
```

`receiptData` est un objet de type `ReceiptData` (défini dans `Aspose.OCR.Structured`). Il contient trois propriétés principales :

- `Merchant` – le nom du magasin
- `Date` – la date d’achat sous forme de `DateTime` (si détectée)
- `TotalAmount` – le montant total sous forme de `decimal`

Si le moteur ne trouve pas un champ particulier, la propriété sera `null` ou `0`. Vous pouvez ajouter une logique de secours si nécessaire (par ex., demander à l’utilisateur de confirmer).

## Step 6 – Display the Extracted Information

Enfin, affichez les résultats dans la console. C’est ici que vous voyez le fruit de votre travail :

```csharp
// Step 6: Display the extracted information
Console.WriteLine($"Merchant: {receiptData.Merchant}");
Console.WriteLine($"Date:     {receiptData.Date:d}");
Console.WriteLine($"Total:    {receiptData.TotalAmount:C}");
```

Les chaînes de format (`:d` et `:C`) produisent respectivement une date courte et une chaîne monétaire, rendant la sortie lisible par l’humain.

### Expected Output

En supposant que le reçu provienne de « Coffee Corner », daté du 2025‑12‑01, avec un total de $4.75, la console affichera :

```
Merchant: Coffee Corner
Date:     12/1/2025
Total:    $4.75
```

Si un champ manque, vous verrez une ligne vide ou une valeur par défaut — parfait pour le débogage.

## Edge Cases & Common Pitfalls

### 1. Low‑Resolution Images
Si l’image du reçu est floue ou inférieure à 150 dpi, la précision de l’OCR chute drastiquement. Redimensionner l’image avec un simple filtre bilinéaire avant de la transmettre à Aspose peut améliorer les résultats.

```csharp
ocrEngine.Image = ImageStream.FromFile("receipt.png")
    .Resize(2.0, InterpolationMode.Bilinear);
```

### 2. Non‑English Receipts
L’exemple principal utilise `Language.English`. Pour des reçus multilingues, définissez `Language` sur l’énumération appropriée (par ex., `Language.French`) ou utilisez `Language.AutoDetect` si vous n’êtes pas sûr.

### 3. Multiple Receipts in One Image
Le reconnaisseur de mise en page d’Aspose attend un seul reçu par image. Si vous avez une photo contenant plusieurs reçus côte à côte, vous devrez pré‑traiter l’image — recadrer chaque reçu dans son propre fichier avant d’exécuter l’OCR.

### 4. Missing Currency Symbol
Parfois le montant total apparaît sans le symbole `$`. Le reconnaisseur capte tout de même les nombres, mais vous devrez peut‑être post‑traiter la chaîne pour garantir le bon placement décimal.

```csharp
if (receiptData.TotalAmount == 0 && rawText.Contains("Total"))
{
    // fallback parsing logic here
}
```

## Pro Tips for Production

- **Cache the OCR engine** si vous traitez de nombreux reçus en lot ; réutiliser la même instance réduit la surcharge d’allocation.
- **Log the raw OCR text** (`ocrEngine.Text`) pour les traces d’audit. C’est utile lorsqu’un champ échoue à être extrait.
- **Wrap the entire flow in a try/catch** et affichez un message d’erreur convivial (par ex., « Impossible de lire le reçu, veuillez télécharger une image plus claire »).

## Complete Working Example

Voici une application console autonome que vous pouvez compiler et exécuter telle quelle. Remplacez simplement le chemin de l’image et vous êtes prêt.

```csharp
// ------------------------------------------------------------
// How to Use Aspose – Extract Receipt Data from Images (C#)
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Structured;

namespace ReceiptExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create and configure the OCR engine for English language
            var ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Load the receipt image you want to process
            // 👉 Make sure the file exists; otherwise an exception will be thrown.
            const string imagePath = "YOUR_DIRECTORY/receipt.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 3️⃣ Run OCR – this also captures layout information
            ocrEngine.Recognize();

            // 4️⃣ Initialize the layout recognizer with the OCR engine
            var layoutRecognizer = new LayoutRecognizer(ocrEngine);

            // 5️⃣ Extract structured receipt data (merchant, date, total amount)
            var receiptData = layoutRecognizer.ExtractReceiptData();

            // 6️⃣ Display the extracted information
            Console.WriteLine($"Merchant: {receiptData.Merchant ?? "Not detected"}");
            Console.WriteLine($"Date:     {(receiptData.Date == DateTime.MinValue ? "Not detected" : receiptData.Date.ToShortDateString())}");
            Console.WriteLine($"Total:    {(receiptData.TotalAmount == 0 ? "Not detected" : receiptData.TotalAmount.ToString("C"))}");

            // Keep the console window open when debugging
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Running the code**

1. Créez un nouveau projet console .NET (`dotnet new console -n ReceiptExtractor`).
2. Ajoutez le package Aspose.OCR (`dotnet add package Aspose.OCR`).
3. Remplacez le `Program.cs` généré par l’extrait ci‑dessus.
4. Placez une image de reçu au chemin que vous avez spécifié.
5. Compilez et exécutez (`dotnet run`).

Vous devriez voir le commerçant, la date et le total affichés exactement comme indiqué précédemment.

## Wrapping Up

Dans ce guide, nous avons couvert **how to use Aspose** pour **load receipt image**, exécuter **ocr receipt image**, puis **extract receipt data** avec seulement quelques lignes. L’essentiel est qu’Aspose.OCR effectue le travail lourd — une fois le moteur OCR configuré, le `LayoutRecognizer` transforme le texte brut en un objet structuré fiable.

Prochaines étapes ? Essayez d’insérer les valeurs extraites dans une base de données, générez un résumé PDF du reçu, ou alimentez‑les dans un modèle d’apprentissage automatique pour la classification des dépenses. Vous pouvez également expérimenter avec d’autres types de documents structurés comme les factures ou les étiquettes d’expédition — `ExtractInvoiceData` d’Aspose fonctionne de façon très similaire.

Des questions sur les cas limites ou envie de voir comment gérer des PDF multi‑pages ? Laissez un commentaire ou consultez la documentation officielle d’Aspose.OCR pour des scénarios avancés. Bon codage, et profitez de la simplicité de **how to use Aspose** pour l’automatisation des reçus !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}