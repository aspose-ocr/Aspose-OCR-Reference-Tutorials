---
category: general
date: 2026-04-08
description: Le OCR PDF par lots avec GPU permet d'extraire rapidement du texte à
  partir de fichiers PDF. Apprenez à définir la langue de l'OCR et à utiliser l'OCR
  accéléré par GPU en C#.
draft: false
keywords:
- batch pdf ocr
- extract text from pdf
- gpu accelerated ocr
- set ocr language
language: fr
og_description: Batch PDF OCR avec GPU vous permet d'extraire rapidement du texte
  à partir de fichiers PDF. Ce tutoriel montre comment définir la langue OCR et exploiter
  l'accélération GPU.
og_title: OCR de PDF en lot avec GPU – Guide d'extraction rapide de texte
tags:
- Aspose.OCR
- C#
- GPU
title: OCR de PDF par lots avec GPU – Guide d'extraction rapide de texte
url: /fr/net/ocr-optimization/batch-pdf-ocr-with-gpu-fast-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PDF par lot avec GPU – Guide d'extraction rapide de texte

Vous devez exécuter **OCR PDF par lot avec GPU** pour accélérer le traitement massif de documents ? Dans ce guide, nous vous montrons comment **extraire du texte à partir de fichiers PDF** en utilisant le moteur **OCR accéléré par GPU** d’Aspose.OCR. Que vous traitiez des milliers de factures ou que vous numérisiez des archives juridiques, la possibilité de définir la langue OCR et d’activer le GPU peut vous faire gagner des minutes — voire des heures — sur votre charge de travail.

Voici le constat : la plupart des développeurs utilisent par défaut l’OCR uniquement CPU et se demandent pourquoi c’est lent. À la fin de ce tutoriel, vous comprendrez pourquoi le GPU est important, comment configurer le moteur, et comment extraire du texte propre de chaque page PDF dans un travail par lot. Aucun outil externe, juste du C# pur et quelques lignes de code.

## Ce dont vous aurez besoin

- .NET 6.0 ou version ultérieure (le code se compile également avec .NET Core)  
- Aspose.OCR pour .NET 2024‑R3 (ou plus récent) – le package NuGet `Aspose.OCR`  
- Au moins un GPU NVIDIA avec prise en charge CUDA 11+ (ou AMD compatible si vous avez le bon pilote)  
- Familiarité de base avec C# async/await (optionnel mais utile)  

Si vous avez déjà ces éléments en place, super — plongeons‑y. Sinon, l’étape **définir la langue OCR** fonctionne aussi sur CPU, vous pouvez donc tester la logique avant de connecter le GPU.

---

## OCR PDF par lot – Initialiser le moteur GPU

La première étape consiste à créer un moteur OCR compatible GPU et à activer l’accélérateur. Aspose fournit la classe `GpuOcrEngine` qui hérite de la classe standard `OcrEngine`. Activer le GPU revient à basculer un drapeau.

```csharp
using Aspose.Ocr;
using System;
using System.Collections.Generic;

/// <summary>
/// Demonstrates batch PDF OCR using a GPU‑accelerated engine.
/// </summary>
public static class PdfBatchOcrDemo
{
    public static void BatchPdfWithGpu()
    {
        // 1️⃣ Create a GPU‑aware OCR engine and enable the GPU.
        var ocrEngine = new GpuOcrEngine
        {
            Options = { EnableGpu = true, GpuDeviceId = 0 } // 0 = first GPU in the system
        };
```

**Pourquoi c’est important :**  
- **EnableGpu = true** indique à Aspose de diriger les tâches lourdes de traitement d’image vers la carte graphique.  
- **GpuDeviceId = 0** sélectionne le premier GPU ; modifiez l’indice si vous avez plusieurs cartes.  
- Utiliser `GpuOcrEngine` au lieu de `OcrEngine` vous donne la même API avec un gain de performance.

> **Astuce pro :** Si vous exécutez sur un serveur sans affichage, assurez‑vous que le pilote NVIDIA et le runtime CUDA sont installés au niveau du système ; sinon le moteur reviendra silencieusement au CPU.

---

## Définir la langue OCR (set OCR language)

Ensuite, indiquez au moteur la langue à reconnaître. Aspose télécharge automatiquement les packs de langues la première fois que vous les demandez, vous n’avez donc pas besoin d’inclure de gros fichiers vous‑même.

```csharp
        // 2️⃣ Set the language for recognition – “en” for English.
        ocrEngine.Language = "en";
```

Vous pouvez remplacer `"en"` par n’importe quel code ISO‑639‑1 (`"fr"`, `"de"`, `"es"`, etc.). Si vous avez besoin d’un support multilingue, passez une liste séparée par des virgules comme `"en,fr"`.

**Pourquoi définir la langue :**  
- Le moteur OCR utilise des dictionnaires spécifiques à chaque langue pour améliorer la précision.  
- Ne pas la définir revient à utiliser l’anglais par défaut, ce qui peut mal interpréter les caractères d’autres alphabets.  
- Le téléchargement automatique garantit que vous avez toujours les derniers modèles sans mises à jour manuelles.

---

## Extraire du texte des pages PDF

Maintenant, nous listons les fichiers PDF que nous voulons traiter. Dans un scénario réel, vous pourriez lire les noms de fichiers depuis un répertoire ou une base de données ; ici nous coderons en dur une courte liste pour plus de clarté.

```csharp
        // 3️⃣ List the PDF pages to be processed.
        var pdfPagePaths = new List<string>
        {
            @"YOUR_DIRECTORY\page1.pdf",
            @"YOUR_DIRECTORY\page2.pdf",
            @"YOUR_DIRECTORY\page3.pdf"
        };
```

> **Remarque :** Utilisez des littéraux de chaîne verbatim (`@""`) pour éviter d’échapper les barres obliques inverses sous Windows.

Une fois la liste prête, nous parcourons chaque fichier, exécutons l’OCR et affichons le nombre de caractères — une vérification rapide que le moteur a bien lu quelque chose.

```csharp
        // 4️⃣ Recognize each page and output the character count.
        foreach (var pagePath in pdfPagePaths)
        {
            // RecognizePdf returns an OcrResult containing the extracted text.
            var ocrResult = ocrEngine.RecognizePdf(pagePath);
            Console.WriteLine($"Page {pagePath} → {ocrResult.Text.Length} characters");
        }
    }
}
```

**Sortie attendue (exemple) :**

```
Page YOUR_DIRECTORY\page1.pdf → 1284 characters
Page YOUR_DIRECTORY\page2.pdf → 1120 characters
Page YOUR_DIRECTORY\page3.pdf → 1439 characters
```

Si vous voyez `0 characters`, vérifiez que le PDF contient réellement du texte sélectionnable ou des images intégrées ; Aspose OCR fonctionne sur les pages rasterisées, donc les PDF scannés sont acceptés, mais les PDF natifs avec texte masqué peuvent nécessiter une approche différente.

---

## Vérifier les résultats et gérer les cas particuliers

Exécuter l’OCR dans un travail par lot n’est pas toujours sans accroc. Voici les problèmes courants et comment les atténuer.

| Problème | Symptom | Solution |
|----------|----------|----------|
| **Pilote GPU manquant** | `Aspose.Ocr.Exceptions.OcrException: GPU not available` | Installez le dernier pilote NVIDIA et le toolkit CUDA. |
| **Mémoire insuffisante sur de gros PDF** | Le processus plante après quelques pages | Augmentez `Options.MaxMemoryUsage` ou traitez les PDF page par page avec `RecognizePdfPage`. |
| **Pack de langue non téléchargé** | Le texte est illisible ou vide | Assurez‑vous que la machine a accès à Internet la première fois que vous définissez `ocrEngine.Language`. |
| **Fichier PDF corrompu** | `System.IO.IOException: Cannot read file` | Validez l’intégrité du fichier avant de le passer à l’OCR, éventuellement avec `PdfDocument.Load`. |

Vous pouvez également capturer le texte OCR brut pour un traitement en aval — enregistrement dans un fichier `.txt`, alimentation d’un index de recherche, ou passage à un modèle de langage pour la synthèse.

```csharp
        // Example: Save each OCR result to a .txt file.
        foreach (var pagePath in pdfPagePaths)
        {
            var ocrResult = ocrEngine.RecognizePdf(pagePath);
            var txtPath = System.IO.Path.ChangeExtension(pagePath, ".txt");
            System.IO.File.WriteAllText(txtPath, ocrResult.Text);
            Console.WriteLine($"Saved OCR text to {txtPath}");
        }
```

**Pourquoi la sauvegarde est utile :**  
- Elle découple l’étape lourde d’OCR des analyses ultérieures, vous permettant d’exécuter l’extraction une fois et de réutiliser les fichiers texte indéfiniment.  
- Les fichiers texte sont minuscules comparés aux PDF, ce qui les rend idéaux pour le contrôle de version ou le diff.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici une application console autonome que vous pouvez coller dans un nouveau projet `.csproj` et exécuter. Remplacez `YOUR_DIRECTORY` par le chemin réel contenant vos pages PDF.

```csharp
using Aspose.Ocr;
using System;
using System.Collections.Generic;

namespace BatchPdfOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            BatchPdfWithGpu();
        }

        /// <summary>
        /// Executes batch PDF OCR using a GPU‑accelerated engine.
        /// </summary>
        public static void BatchPdfWithGpu()
        {
            // Step 1 – Initialize GPU engine.
            var ocrEngine = new GpuOcrEngine
            {
                Options = { EnableGpu = true, GpuDeviceId = 0 }
            };

            // Step 2 – Set the OCR language (auto‑download enabled).
            ocrEngine.Language = "en";

            // Step 3 – Define the PDFs to process.
            var pdfPagePaths = new List<string>
            {
                @"YOUR_DIRECTORY\page1.pdf",
                @"YOUR_DIRECTORY\page2.pdf",
                @"YOUR_DIRECTORY\page3.pdf"
            };

            // Step 4 – Run OCR on each file and write results.
            foreach (var pagePath in pdfPagePaths)
            {
                var ocrResult = ocrEngine.RecognizePdf(pagePath);
                Console.WriteLine($"Page {pagePath} → {ocrResult.Text.Length} characters");

                // Optional: persist the extracted text.
                var txtPath = System.IO.Path.ChangeExtension(pagePath, ".txt");
                System.IO.File.WriteAllText(txtPath, ocrResult.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }
        }
    }
}
```

Compilez avec :

```bash
dotnet build
dotnet run
```

Vous devriez voir les comptes de caractères et les fichiers `.txt` générés apparaître à côté de chaque PDF.

---

![Diagramme de traitement OCR PDF par lot avec GPU](https://example.com/image.png "OCR PDF par lot avec GPU")

*Texte alternatif de l’image : **Diagramme de traitement OCR PDF par lot avec GPU** montrant PDF → OCR GPU → Sortie texte.*

---

## Prochaines étapes et sujets associés

- **Performance GPU‑accélérée vs CPU‑seule** : lancez un benchmark rapide (traitement de 100 pages) et comparez les temps. Attendez un gain de vitesse de 2‑5× sur les GPU modernes.  
- **Lots multilingues** : définissez `ocrEngine.Language = "en,fr,es"` pour gérer des documents multilingues en une seule passe.  
- **Streaming de gros PDF** : utilisez `RecognizePdfPage` pour OCRiser une page à la fois, réduisant la pression mémoire.  
- **Intégration avec Azure Functions ou AWS Lambda** : externalisez le travail par lot vers le cloud, en tirant parti d’instances GPU‑activées pour une mise à l’échelle à la demande.  
- **Indexation de recherche** : alimentez le texte extrait dans Elasticsearch ou Azure Cognitive Search pour une récupération rapide des documents.

---

## Conclusion

Vous venez de maîtriser **l’OCR PDF par lot avec GPU**, d’apprendre comment **extraire du texte à partir de fichiers PDF** de façon efficace, et découvert la bonne façon de **définir la langue OCR** pour une précision optimale. En activant l’accélération GPU, vous réduisez considérablement le temps de traitement, et grâce à l’API simple d’Aspose, vous évitez le code boilerplate habituel des pipelines OCR.

Testez-le sur votre propre jeu de données — ajustez la liste des langues, expérimentez avec différents appareils GPU, ou encapsulez la logique dans un service d’arrière‑plan. Le ciel est la limite lorsque vous combinez un OCR haute performance avec les outils .NET modernes.

Des questions, ou un cas particulier non couvert ici ? Laissez un commentaire ou ouvrez un ticket sur les forums Aspose. Bon codage, et que vos exécutions OCR soient rapides et sans erreur !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}