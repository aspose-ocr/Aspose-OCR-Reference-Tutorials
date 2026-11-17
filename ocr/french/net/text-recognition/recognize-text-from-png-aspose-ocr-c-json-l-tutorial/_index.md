---
category: general
date: 2026-03-26
description: Reconnaître le texte d’un PNG et extraire les données du reçu à l’aide
  d’Aspose OCR en C#. Convertir l’image en JSON‑L et traiter le reçu avec OCR dans
  un exemple complet.
draft: false
keywords:
- recognize text from png
- extract text from receipt
- convert image to jsonl
- process receipt with ocr
- aspose ocr example c#
language: fr
og_description: reconnaître le texte d’un PNG et transformer les reçus en JSON‑L avec
  Aspose OCR en C#. Code complet étape par étape et astuces.
og_title: reconnaître du texte à partir de png – Guide Aspose OCR C#
tags:
- Aspose OCR
- C#
- JSONL
- Receipt Processing
title: reconnaître le texte à partir de PNG – tutoriel Aspose OCR C# JSON‑L
url: /fr/net/text-recognition/recognize-text-from-png-aspose-ocr-c-json-l-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir de png – Guide complet Aspose OCR C#

Vous avez déjà eu besoin de **reconnaître du texte à partir de fichiers png** sans savoir quelle bibliothèque vous donnerait des résultats propres, ligne par ligne ? Vous n'êtes pas seul. Dans de nombreuses petites applications, le reçu est stocké sous forme d'image PNG, et extraire le montant, la date ou le nom du commerçant est un point de douleur quotidien.  

La bonne nouvelle ? En quelques lignes de C# et avec la bibliothèque **Aspose OCR**, vous pouvez **extraire le texte d'un reçu**, puis **convertir l'image en jsonl** pour des analyses en aval. Dans ce tutoriel, nous parcourrons toute la chaîne — chargement d’un PNG, exécution de l’OCR et écriture de chaque ligne dans un fichier JSON‑L — pour que vous puissiez **traiter un reçu avec l’OCR** immédiatement.

Nous couvrirons tout ce dont vous avez besoin : les packages NuGet requis, un programme complet et exécutable, les explications de chaque étape, ainsi que quelques astuces pratiques que vous apprécierez lorsque les reçus deviendront désordonnés. Aucun document externe n’est nécessaire ; copiez‑collez, exécutez et adaptez.

---

## Ce que vous allez apprendre

- Comment **reconnaître du texte à partir de png** avec `Aspose.OCR`.
- Comment **extraire le texte d’un reçu** sous forme d’objets ligne et récupérer les scores de confiance.
- Comment **convertir l’image en jsonl** afin que chaque ligne OCR devienne un objet JSON distinct.
- Comment **traiter un reçu avec l’OCR** de bout en bout, en gérant les cas limites comme les images vides ou les lignes à faible confiance.
- Astuces pour dépanner les problèmes courants d’OCR et améliorer la précision.

### Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également avec .NET Core et .NET Framework).
- Visual Studio 2022 ou tout autre IDE de votre choix.
- Une licence valide Aspose OCR (vous pouvez commencer avec une licence temporaire gratuite depuis Aspose.com).
- Un reçu d’exemple enregistré sous `receipt.png` dans un dossier que vous contrôlez.

---

## Étape 1 : Reconnaître du texte à partir de png avec Aspose OCR

La première chose dont nous avons besoin est un `OcrEngine` initialisé. Cet objet contient les paramètres du moteur OCR (langue, mode de détection, etc.). Par défaut, il utilise l’anglais et détecte automatiquement la mise en page, ce qui convient à la plupart des reçus.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is where Aspose loads its models.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the PNG image that contains the receipt.
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // Run OCR and get the result object.
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);
```

**Pourquoi c’est important :**  
`OcrEngine` est le composant qui fait le gros du travail ; le créer une fois et le réutiliser pour de nombreuses images réduit la consommation de mémoire. Si vous avez besoin d’une autre langue (par ex., des reçus en espagnol), vous pouvez définir `ocrEngine.Language = OcrLanguage.Spanish;` avant d’appeler `Recognize`.

---

## Étape 2 : Extraire le texte des lignes du reçu

`OcrResult` contient une collection appelée `Lines`. Chaque ligne possède le texte brut et un score de confiance (0‑100). Les extraire vous donne un contrôle granulaire — vous pouvez éliminer les lignes à faible confiance ou les marquer pour une révision manuelle.

```csharp
        // Prepare to write each line as a JSON‑L record.
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";

        using (StreamWriter jsonLineWriter = new StreamWriter(jsonlPath))
        {
            foreach (var line in ocrResult.Lines)
            {
                // Build a simple JSON object for the line.
                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                jsonLineWriter.WriteLine(json);
            }
        }

        Console.WriteLine("JSON‑L file written to " + jsonlPath);
    }

    // Helper to escape quotes and backslashes in JSON strings.
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Pourquoi nous échappons le JSON :**  
Le texte d’un reçu peut contenir des guillemets (`"`) ou des antislashs (`\`) qui casseraient une chaîne JSON naïve. La méthode `EscapeJson` garantit une ligne JSON valide.

**À quoi ressemble la sortie :**  

```
{"text":"Store XYZ","confidence":98.5}
{"text":"Date: 2024-07-15","confidence":97.2}
{"text":"Total $23.45","confidence":99.1}
```

Chaque ligne est un enregistrement séparé, idéal pour le streaming vers un data lake ou l’alimentation d’un modèle d’apprentissage automatique.

---

## Étape 3 : Convertir l’image en JSONL – gestion des cas limites

Lorsque vous traitez un lot de reçus, certaines images peuvent être vides, corrompues ou présenter des scores de confiance très faibles. Rendons le pipeline un peu plus robuste.

```csharp
        // After OCR, check if any lines were detected.
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("Warning: No text detected. Verify the image path and quality.");
            return;
        }

        // Optional: filter out lines with confidence below a threshold.
        const double minConfidence = 80.0;
        foreach (var line in ocrResult.Lines)
        {
            if (line.Confidence < minConfidence)
                continue; // skip noisy line
            // write as before...
        }
```

**Pourquoi filtrer :**  
Les reçus imprimés sur du papier fané peuvent générer des caractères parasites avec une faible confiance. Supprimer tout ce qui est en dessous de 80 % élimine généralement le bruit tout en conservant les données utiles.

---

## Étape 4 : Traiter un reçu avec l’OCR – exemple de bout en bout

En assemblant le tout, voici le programme **complet, prêt à l’exécution**. Remplacez `YOUR_DIRECTORY` par le dossier contenant votre fichier PNG.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;
using System.IO;

class JsonLExample
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load receipt PNG
        string imagePath = @"YOUR_DIRECTORY\receipt.png";
        OcrImage receiptImage = OcrImage.FromFile(imagePath);

        // 3️⃣ Perform OCR
        OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

        // 4️⃣ Verify we got something back
        if (ocrResult.Lines.Count == 0)
        {
            Console.WriteLine("❗ No text found – check the image quality.");
            return;
        }

        // 5️⃣ Write each line to a JSON‑L file
        string jsonlPath = @"YOUR_DIRECTORY\receipt.jsonl";
        using (StreamWriter writer = new StreamWriter(jsonlPath))
        {
            const double minConfidence = 80.0;
            foreach (var line in ocrResult.Lines)
            {
                if (line.Confidence < minConfidence) continue; // skip low‑confidence

                string json = $"{{\"text\":\"{EscapeJson(line.Text)}\",\"confidence\":{line.Confidence}}}";
                writer.WriteLine(json);
            }
        }

        Console.WriteLine($"✅ JSON‑L written to: {jsonlPath}");
    }

    // Helper to make JSON safe
    private static string EscapeJson(string s) => s.Replace("\\", "\\\\").Replace("\"", "\\\"");
}
```

**Exécution du code :**  
1. Ouvrez un terminal dans le dossier du projet.  
2. `dotnet add package Aspose.OCR` – installe la bibliothèque.  
3. `dotnet run` – vous devriez voir le message de succès et un fichier `receipt.jsonl` apparaître.

**Résultat attendu :** Un fichier JSON délimité par des lignes où chaque ligne reflète une ligne du reçu, avec les scores de confiance. Vous pouvez maintenant acheminer ce fichier vers Power BI, Elastic ou tout autre outil d’analyse qui comprend le format JSON‑L.

---

## Pièges courants & Astuces pro

| Problème | Pourquoi cela arrive | Solution rapide |
|----------|----------------------|-----------------|
| **Sortie vide** | Chemin d’image incorrect ou fichier non PNG. | Vérifiez le chemin, utilisez `File.Exists(imagePath)`. |
| **Caractères parasites** | DPI trop bas ou PNG fortement compressé. | Utilisez des scans d’au moins 300 dpi ; évitez la compression JPEG agressive. |
| **Trop de lignes à faible confiance** | Reçu imprimé sur papier thermique fané. | Augmentez le seuil `minConfidence` ou pré‑traitez l’image (contraste/threshold). |
| **Erreurs d’analyse JSON** | Guillemets non échappés dans le texte du reçu. | Conservez la fonction d’aide `EscapeJson` ou passez à `System.Text.Json` pour une sérialisation robuste. |

**Astuce pro :** Si vous devez extraire des champs spécifiques (par ex., le montant total), exécutez une simple expression régulière sur chaque `line.Text` après avoir obtenu le fichier JSON‑L. Cela sépare l’OCR de la logique métier et facilite le débogage.

---

## Étendre la solution

- **Traitement par lots** : Enveloppez la logique `Main` dans un `foreach` parcourant tous les fichiers PNG d’un répertoire.
- **Support multilingue** : Définissez `ocrEngine.Language = OcrLanguage.Spanish;` (ou toute langue prise en charge) avant `Recognize`.
- **Sortie structurée** : Au lieu d’un JSON ligne par ligne, créez un objet `Receipt` avec les propriétés `Date`, `Merchant`, `Total`, puis sérialisez‑le en une fois.

Toutes ces variantes continuent de **convertir l’image en jsonl** au cœur du processus, vous permettant de changer le consommateur en aval sans toucher à la partie OCR.

---

## Conclusion

Nous venons de vous montrer comment **reconnaître du texte à partir de png** avec Aspose OCR, **extraire le texte d’un reçu**, et **convertir l’image en jsonl** pour un traitement en aval simplifié. Le programme C# complet et autonome illustre le flux complet — du chargement d’un PNG, à la gestion des cas limites, jusqu’à l’écriture d’un fichier JSON‑L propre — pour que vous puissiez immédiatement **traiter un reçu avec l’OCR** dans vos projets.

Essayez avec quelques reçus d’exemple, ajustez le seuil de confiance, et vous verrez à quel point une pile d’images bruyantes se transforme rapidement en données structurées prêtes pour l’analyse. Une fois à l’aise, explorez le traitement par lots ou ajoutez un petit modèle ML pour classer automatiquement les catégories de dépenses.

Des questions ou une astuce à partager ? Laissez un commentaire ci‑dessous—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}