---
category: general
date: 2026-04-04
description: Apprenez à extraire du texte à partir de fichiers TIFF en utilisant un
  moteur OCR, exemple en C#. Guide étape par étape avec sortie JSON et XML.
draft: false
keywords:
- extract text from tiff
- ocr engine example
- Aspose OCR C#
- multi‑page TIFF OCR
- JSON OCR result
language: fr
og_description: Extraire du texte à partir de fichiers TIFF en utilisant un moteur
  OCR, exemple en C#. Étapes détaillées, code complet et conseils pour la sortie JSON/XML.
og_title: Extraire du texte d’un TIFF avec le moteur OCR d’Aspose – Guide complet
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extraire du texte d’un TIFF avec le moteur OCR d’Aspose – Exemple complet
url: /fr/net/text-recognition/extract-text-from-tiff-with-aspose-ocr-engine-complete-examp/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir de TIFF – Exemple complet de moteur OCR en C#

Vous avez déjà eu besoin d'**extraire du texte à partir de TIFF** images mais vous n'étiez pas sûr quelle bibliothèque pouvait gérer les fichiers multi‑pages sans un cirque de solutions de contournement ? Vous n'êtes pas le seul. Dans de nombreux systèmes hérités, les documents arrivent sous forme de scans TIFF multi‑pages, et extraire le texte brut est une fonctionnalité indispensable pour la recherche, la conformité ou l'automatisation de la saisie de données.

Bonne nouvelle ? Avec Aspose OCR, vous pouvez le faire en quelques lignes — sans bricoler avec des tampons de pixels de bas niveau. Ce tutoriel vous guide à travers un **exemple complet de moteur OCR** qui charge un TIFF multi‑page, reconnaît chaque page, et génère à la fois du JSON joliment formaté et du XML optionnel. À la fin, vous disposerez d’une application console C# prête à l’emploi qui extrait du texte des fichiers TIFF en quelques secondes.

## Ce que vous allez apprendre

- Comment configurer le moteur Aspose OCR dans un projet .NET.  
- Le code exact nécessaire pour **extraire du texte à partir de TIFF** fichiers, y compris la gestion multi‑pages.  
- Pourquoi vous pourriez préférer une sortie JSON plutôt que XML et comment générer les deux.  
- Conseils pour dépanner les problèmes courants (par ex., DPI de l'image, utilisation de la mémoire).  

### Prérequis

- .NET 6.0 SDK ou version ultérieure (le code fonctionne avec .NET Core et .NET Framework).  
- Une licence Aspose OCR valide (ou une clé d’essai gratuite).  
- Visual Studio 2022 ou tout éditeur C# de votre choix.  
- Un fichier TIFF multi‑page d’exemple (nommé `multi-page.tiff` dans l’exemple).  

> **Astuce pro :** Si votre budget est serré, l’essai gratuit vous permet toujours d’extraire du texte jusqu’à 100 pages par mois — parfait pour les tests.

---

## Étape 1 – Initialiser le moteur OCR (exemple de moteur OCR)

Avant de pouvoir **extraire du texte à partir de TIFF**, nous avons besoin d’une instance du moteur OCR. Cet objet contient toute la configuration que vous pourrez ajuster plus tard (langue, résolution, etc.).

```csharp
using Aspose.OCR;
using System.IO;

// Create a new OCR engine – this is the core of our ocr engine example
var ocrEngine = new OcrEngine();

// Optional: set language if you know the document’s language
// ocrEngine.Language = Language.English;
```

*Pourquoi c’est important :* La classe `OcrEngine` masque le travail lourd. L’instancier une fois et le réutiliser pour plusieurs images est plus efficace en mémoire que de créer un nouveau moteur par page.

---

## Étape 2 – Charger le TIFF multi‑page (extraire du texte à partir de TIFF)

Nous pointons maintenant le moteur vers notre fichier source. `ImageStream.FromFile` prend en charge TIFF, JPEG, PNG et bien d’autres, mais pour ce tutoriel nous nous concentrons sur le TIFF.

```csharp
// Load the multi‑page TIFF you want to process
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi-page.tiff");
```

> **Note :** Remplacez `YOUR_DIRECTORY` par le chemin réel du dossier sur votre machine.  
> **Astuce :** Si votre TIFF a un DPI faible (inférieur à 150), envisagez de le pré‑traiter pour améliorer la précision de l’OCR.

---

## Étape 3 – Reconnaître toutes les pages

Appeler `Recognize()` exécute l’algorithme OCR sur **toutes les pages** du TIFF. L’objet résultat contient le texte brut, les scores de confiance et la segmentation page par page.

```csharp
// Run OCR on the loaded image – this extracts text from all pages
var ocrResult = ocrEngine.Recognize();
```

*Ce que vous obtenez :* `ocrResult` contient une collection d’objets `PageResult`. Le texte de chaque page est accessible via `ocrResult.Pages[i].Text`. Le moteur fournit également les niveaux de confiance, utiles pour les contrôles de qualité.

---

## Étape 4 – Enregistrer les résultats au format JSON (et XML optionnel)

La plupart des pipelines modernes préfèrent le JSON, mais les systèmes hérités utilisent encore le XML. Voici comment générer les deux, joliment formatés.

```csharp
// Convert the recognition result to pretty‑printed JSON
string jsonResult = ocrResult.ToJson(prettyPrint: true);
File.WriteAllText(@"YOUR_DIRECTORY/result.json", jsonResult);

// Optional: also output XML for older workflows
string xmlResult = ocrResult.ToXml();
File.WriteAllText(@"YOUR_DIRECTORY/result.xml", xmlResult);
```

### Exemple de sortie JSON (truncée)

```json
{
  "Pages": [
    {
      "PageNumber": 1,
      "Text": "Invoice #12345\nDate: 2024‑03‑15\nTotal: $1,250.00",
      "Confidence": 0.97
    },
    {
      "PageNumber": 2,
      "Text": "Itemized List\n1. Widget A – $500.00\n2. Widget B – $750.00",
      "Confidence": 0.95
    }
  ]
}
```

Le JSON est lisible par l’homme, ce qui facilite le débogage. Le XML reflète la même structure si vous en avez besoin.

---

## Étape 5 – Vérifier l’extraction (extraire du texte à partir de TIFF)

Après l’écriture des fichiers, une vérification rapide permet de s’assurer que tout s’est bien passé.

```csharp
// Load the JSON back just to confirm it was saved correctly
string loadedJson = File.ReadAllText(@"YOUR_DIRECTORY/result.json");
Console.WriteLine("First 200 characters of JSON output:");
Console.WriteLine(loadedJson.Substring(0, Math.Min(200, loadedJson.Length)));
```

Si vous voyez l’extrait affiché, vous avez réussi à **extraire du texte à partir de TIFF** et à le sauvegarder. Vous pouvez maintenant injecter le JSON dans un index de recherche, une base de données ou tout service en aval.

---

## Pourquoi utiliser Aspose OCR pour extraire du texte à partir de TIFF ?

- **Prise en charge multi‑pages prête à l’emploi** – pas besoin de découper le TIFF manuellement.  
- **Haute précision** grâce aux modèles de réseaux neuronaux propriétaires.  
- **Cross‑platform** – fonctionne sur les runtimes .NET Windows, Linux et macOS.  
- **Formats de sortie riches** (JSON, XML, texte brut) qui conviennent aux piles modernes et héritées.  

Si vous hésitez encore, essayez l’essai gratuit sur un document d’exemple. Vous remarquerez la rapidité et la simplicité comparées aux alternatives open‑source qui nécessitent souvent un pré‑traitement d’image supplémentaire.

---

## Problèmes courants & comment les éviter

| Issue | Symptom | Fix |
|-------|---------|-----|
| Low‑resolution TIFF | Missing characters, low confidence | Upscale the image to ≥150 DPI before OCR (`ocrEngine.Image = ImageStream.FromFile(...).Resize(150)` ) |
| Wrong language | Garbled words, especially for non‑English text | Set `ocrEngine.Language = Language.Spanish` (or appropriate) before `Recognize()` |
| Out‑of‑memory on huge files | `OutOfMemoryException` | Process pages in batches: loop through `ocrEngine.Image.Pages` and call `RecognizePage(i)` |
| License not applied | Watermark “Evaluation” in output | Register your license: `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet que vous pouvez insérer dans un nouveau projet console. Il inclut toutes les parties que nous avons abordées — initialisation, chargement, reconnaissance et sauvegarde.

```csharp
using Aspose.OCR;
using System;
using System.IO;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Initialize the OCR engine (ocr engine example)
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // Optional: set license if you have one
            // var license = new License();
            // license.SetLicense("Aspose.OCR.lic");

            // -------------------------------------------------
            // 2️⃣  Load the multi‑page TIFF (extract text from TIFF)
            // -------------------------------------------------
            string tiffPath = @"YOUR_DIRECTORY/multi-page.tiff";
            if (!File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -------------------------------------------------
            // 3️⃣  Recognize every page
            // -------------------------------------------------
            var ocrResult = ocrEngine.Recognize();

            // -------------------------------------------------
            // 4️⃣  Save JSON (pretty) and optional XML
            // -------------------------------------------------
            string jsonPath = @"YOUR_DIRECTORY/result.json";
            string jsonResult = ocrResult.ToJson(prettyPrint: true);
            File.WriteAllText(jsonPath, jsonResult);
            Console.WriteLine($"JSON saved to {jsonPath}");

            // Optional XML output
            string xmlPath = @"YOUR_DIRECTORY/result.xml";
            string xmlResult = ocrResult.ToXml();
            File.WriteAllText(xmlPath, xmlResult);
            Console.WriteLine($"XML saved to {xmlPath}");

            // -------------------------------------------------
            // 5️⃣  Quick verification (extract text from TIFF)
            // -------------------------------------------------
            string preview = jsonResult.Length > 200 ? jsonResult.Substring(0, 200) + "..." : jsonResult;
            Console.WriteLine("\nPreview of JSON output:");
            Console.WriteLine(preview);
        }
    }
}
```

Enregistrez le fichier sous `Program.cs`, exécutez `dotnet run`, et observez la console vous indiquer où le JSON et le XML ont été enregistrés. C’est tout — vous venez de terminer un **exemple de moteur OCR** qui extrait du texte à partir de TIFF.

---

## Prochaines étapes & sujets associés

- **Traitement par lots :** Enveloppez la logique ci‑dessus dans une boucle `foreach` pour gérer automatiquement des dizaines de fichiers TIFF.  
- **Intégration de recherche :** Envoyez le JSON vers Elasticsearch ou Azure Cognitive Search pour activer la recherche en texte intégral sur les documents numérisés.  
- **Pré‑traitement d’image :** Explorez l’API `ImageProcessing` d’Aspose pour redresser, débruiter ou ajuster le contraste avant l’OCR.  
- **Sortie alternative :** Utilisez `ocrResult.ToPlainText()` si vous avez seulement besoin de chaînes brutes sans métadonnées.  

Si vous êtes curieux concernant d’autres formats d’image, le même schéma fonctionne pour les PDF (il suffit de changer le fichier source) ou les PNG. L’essentiel est qu’une fois le moteur configuré, le reste constitue un pipeline réutilisable.

---

## Conclusion

Nous avons parcouru un **exemple complet de moteur OCR** qui vous permet d’**extraire du texte à partir de TIFF** avec Aspose OCR, en produisant du JSON propre et du XML optionnel pour tout flux de travail en aval. Le code est autonome, les explications couvrent le « pourquoi » de chaque étape

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}