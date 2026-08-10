---
category: general
date: 2026-02-13
description: Comment lire rapidement un reçu avec Aspose OCR et extraire le montant
  à l’aide d’une expression régulière. Apprenez le traitement du reçu étape par étape
  avec l’OCR.
draft: false
keywords:
- how to read receipt
- extract amount using regex
- regex find total
- process receipt with ocr
language: fr
og_description: Comment lire un reçu en C# en utilisant Aspose OCR et les expressions
  régulières. Ce guide vous montre comment traiter le reçu avec l’OCR et extraire
  le montant total.
og_title: Comment lire un reçu en C# – Tutoriel complet sur l’OCR et les expressions
  régulières
tags:
- OCR
- C#
- Regex
- Aspose
title: Comment lire un reçu en C# – Guide OCR + Regex
url: /fr/net/text-recognition/how-to-read-receipt-in-c-ocr-regex-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment lire un reçu en C# – Guide OCR + Regex

Vous vous êtes déjà demandé **comment lire un reçu** à partir d'images sans taper manuellement chaque ligne ? Dans de nombreuses applications de petites entreprises, vous devez extraire le montant total d'une photo de reçu, et le faire à la main va à l'encontre de l'automatisation. Bonne nouvelle ? Avec Aspose OCR, vous pouvez laisser le moteur faire le gros du travail, puis une simple expression régulière localisera le total. Dans ce tutoriel, nous parcourrons **process receipt with OCR**, extrairons le montant à l'aide de regex, et obtiendrons une valeur totale prête à l'emploi.

Vous verrez un exemple complet et exécutable, découvrirez pourquoi le modèle linguistique du reçu est important, et obtiendrez des conseils pour gérer les cas limites comme différents symboles monétaires ou les libellés “Total” manquants. Aucun document externe n'est requis—tout ce dont vous avez besoin se trouve ici.

## Ce que vous apprendrez

- Comment configurer Aspose OCR pour la reconnaissance spécifique aux reçus (le modèle linguistique `Receipt` redresse et débruite automatiquement l'image).  
- Comment appliquer une expression régulière qui **extract amount using regex** fonctionne pour la plupart des reçus de style US.  
- Comment gérer les variations courantes telles que “TOTAL”, “Total :”, ou “Grand Total – $12.34”.  
- Comment afficher le résultat en toute sécurité et que faire lorsque le motif n'est pas trouvé.  

**Prerequisites** : .NET 6+ (ou .NET Framework 4.7+), une licence Aspose OCR valide ou un essai, et une image d’un reçu enregistrée localement. C’est tout—aucun paquet NuGet supplémentaire au‑delà d’Aspose.OCR.

---

## Étape 1 – Installer Aspose OCR et préparer le projet

### Pourquoi c’est important

Aspose OCR fournit un modèle **process receipt with OCR** spécialement conçu qui sait aplanir un papier froissé et ignorer le bruit de fond. Utiliser le modèle texte générique entraînerait davantage d’erreurs, surtout sur des numérisations basse résolution.

### Code

```csharp
// Install the package via NuGet first:
//   dotnet add package Aspose.OCR
using Aspose.OCR;
using Aspose.OCR.Enums;
using System.Text.RegularExpressions;

// If you have a license file, load it now (optional but removes trial watermark)
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

> **Astuce :** Conservez le fichier de licence en dehors de votre dossier de contrôle de version pour éviter les validations accidentelles.

---

## Étape 2 – Configurer le moteur OCR pour la reconnaissance de reçus

### Pourquoi c’est important

Le modèle linguistique `Receipt` inclut un redressement et un débruitage intégrés, ce qui améliore considérablement la précision sur les reçus réels souvent pliés ou froissés.

### Code

```csharp
// Step 2: Create and configure the OCR engine for receipt processing
var ocrEngine = new OcrEngine
{
    // Receipt model is optimized for invoices, grocery receipts, etc.
    Language = OcrLanguage.Receipt
};
```

---

## Étape 3 – Reconnaître le texte de l’image du reçu

### Pourquoi c’est important

Vous avez besoin du texte brut avant de pouvoir appliquer une regex. La méthode `RecognizeImage` renvoie un `OcrResult` contenant la chaîne complète, les scores de confiance, et plus encore si vous en avez besoin plus tard.

### Code

```csharp
// Step 3: Recognize text from the receipt image
// Replace the path with the actual location of your receipt file.
string receiptPath = @"C:\Receipts\sample-receipt.jpg";

OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

// Quick sanity check – print the whole OCR output (helps debugging)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(receiptResult.Text);
Console.WriteLine("===================\n");
```

**Sortie OCR attendue (exemple)**  
```
Walmart Supercenter
123 Main St.
Anytown, USA
Date: 02/12/2026
Item A   $3.45
Item B   $7.89
Subtotal $11.34
Tax      $0.91
Total:   $12.25
Thank you!
```

---

## Étape 4 – Construire une regex pour **Extract Amount Using Regex**

### Pourquoi c’est important

Les reçus existent sous de nombreux formats, mais le mot “Total” (ou une variante proche) suivi d’un montant en dollars est une ancre fiable. Le motif ci‑dessous tolère les espaces optionnels, les deux‑points, les tirets, et un signe `$` optionnel.

### Code

```csharp
// Step 4: Use a regular expression to locate the total amount in the recognized text
string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
RegexOptions options = RegexOptions.IgnoreCase;

Match totalMatch = Regex.Match(receiptResult.Text, pattern, options);
```

**Explication du motif**

| Partie | Signification |
|--------|----------------|
| `Total` | Recherche le mot “Total” (insensible à la casse). |
| `\s*[:\-]?` | Autorise tout espace blanc, suivi d’un deux‑points ou d’un tiret optionnel. |
| `\s*\$?` | Espace blanc optionnel et signe dollar optionnel. |
| `(\d+(\.\d{2})?)` | Capture un ou plusieurs chiffres, éventuellement suivis d’un décimal et de deux centimes. |

---

## Étape 5 – Afficher le total extrait ou gérer les données manquantes

### Pourquoi c’est important

Même le meilleur OCR peut manquer un mot, surtout sur des reçus flous. Fournir une solution de secours élégante évite les plantages et vous donne un point d’ancrage pour une logique personnalisée (par ex., demander à l'utilisateur de confirmer).

### Code

```csharp
// Step 5: Output the extracted total, or indicate it wasn't found
if (totalMatch.Success)
{
    string amount = totalMatch.Groups[1].Value;
    Console.WriteLine($"Total: ${amount}");
}
else
{
    Console.WriteLine("Total amount not found. Consider reviewing the OCR output manually.");
}
```

**Exemple de sortie console**

```
Total: $12.25
```

---

## Exemple complet fonctionnel – Toutes les étapes dans un seul fichier

Ci‑dessous se trouve un programme autonome que vous pouvez copier‑coller dans un projet console. Il comprend des commentaires, la gestion des erreurs, et le chargement optionnel de la licence.

```csharp
// ---------------------------------------------------------------
// How to Read Receipt in C# – OCR + Regex (Complete Example)
// ---------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Enums;
using System;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 0️⃣ Optional: Load your Aspose OCR license (remove trial watermark)
        try
        {
            var license = new Aspose.OCR.License();
            license.SetLicense("Aspose.OCR.lic"); // path to .lic file
        }
        catch (Exception ex)
        {
            Console.WriteLine("License not found – running in trial mode.");
        }

        // 1️⃣ Configure the OCR engine for receipt processing
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Receipt // receipt model = de‑skew + de‑noise
        };

        // 2️⃣ Path to the receipt image (change to your file)
        string receiptPath = @"YOUR_DIRECTORY/receipt.jpg";

        // 3️⃣ Perform OCR
        OcrResult receiptResult = ocrEngine.RecognizeImage(receiptPath);

        // 4️⃣ Debug: show full OCR text (helps when regex fails)
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(receiptResult.Text);
        Console.WriteLine("===================\n");

        // 5️⃣ Regex to **extract amount using regex** (find the total)
        string pattern = @"Total\s*[:\-]?\s*\$?(\d+(\.\d{2})?)";
        Match totalMatch = Regex.Match(receiptResult.Text, pattern,
                                        RegexOptions.IgnoreCase);

        // 6️⃣ Output
        if (totalMatch.Success)
        {
            string amount = totalMatch.Groups[1].Value;
            Console.WriteLine($"Total: ${amount}");
        }
        else
        {
            Console.WriteLine("Total amount not found. You might need to adjust the regex or improve image quality.");
        }
    }
}
```

**Exécution du programme**

1. Créez un nouveau projet console (`dotnet new console -n ReceiptReader`).  
2. Ajoutez le package NuGet Aspose.OCR (`dotnet add package Aspose.OCR`).  
3. Remplacez `YOUR_DIRECTORY/receipt.jpg` par le chemin réel vers une image de reçu.  
4. Construisez et exécutez (`dotnet run`).  

Vous devriez voir le dump OCR suivi de `Total: $xx.xx` si tout est correct.

---

## Gestion des cas limites & variations courantes

### 1. Différents symboles monétaires

Si vous traitez des euros (€) ou des livres (£), étendez le motif :

```csharp
string pattern = @"Total\s*[:\-]?\s*[$€£]?\s*(\d+(\.\d{2})?)";
```

### 2. Libellé “Total” manquant

Certains reçus n’affichent que “Grand Total”. Ajoutez une alternance :

```csharp
string pattern = @"(?:Total|Grand\s*Total)\s*[:\-]?\s*[$]?\s*(\d+(\.\d{2})?)";
```

### 3. Totaux multiples (p. ex., “Subtotal” et “Total”)

Si la regex correspond à la première occurrence, vous voudrez peut‑être la **dernière** correspondance :

```csharp
MatchCollection matches = Regex.Matches(receiptResult.Text, pattern,
                                         RegexOptions.IgnoreCase);
Match last = matches.Count > 0 ? matches[matches.Count - 1] : null;
```

### 4. Images basse résolution

- Augmentez le DPI lors de la numérisation (`300 DPI` est un bon compromis).  
- Pré‑traitez l’image avec un filtre simple de réduction du flou avant de la transmettre à Aspose (hors du cadre de ce guide, mais intéressant à explorer).

---

## Astuces pro pour les projets réels

- **Mettez en cache le résultat OCR** si vous devez extraire plusieurs champs (taxe, articles, etc.) – vous ne payez le coût OCR qu’une fois.  
- **Enregistrez le texte OCR brut** dans une base de données ; il devient une piste d’audit précieuse pour les dépenses contestées.  
- Lors de la création d’une API web, **exécutez l’OCR dans un worker en arrière‑plan** ; cela peut prendre quelques centaines de millisecondes, ce qui est acceptable de façon asynchrone mais pas idéal pour une requête synchrone.  
- **Validez le montant extrait** selon les règles métier (p. ex., le montant doit être > 0) avant de le persister.

---

## Conclusion

Nous avons couvert **how to read receipt** les images en C# avec Aspose OCR, puis **extract amount using regex** pour trouver de manière fiable la ligne du total. En exploitant le modèle linguistique `Receipt`, vous obtenez du texte redressé et débruité, et une expression régulière concise gère la majorité des particularités de formatage. L’extrait de code complet ci‑dessus est prêt à être intégré dans n’importe quel projet .NET console ou service, et les suggestions supplémentaires pour les cas limites vous offrent une base solide pour la production.

Prêt pour l’étape suivante ? Essayez d’étendre la solution pour extraire les lignes d’articles individuelles, calculer automatiquement la taxe, ou l’intégrer à une API de suivi des dépenses. Et si vous tombez sur un reçu qui casse le motif, rappelez‑vous que l’approche **regex find total** n’est qu’un point de départ—vous pouvez toujours ajuster le motif pour correspondre à votre locale spécifique.

Bon codage, et que votre traitement de reçus soit rapide, précis et totalement automatisé !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}