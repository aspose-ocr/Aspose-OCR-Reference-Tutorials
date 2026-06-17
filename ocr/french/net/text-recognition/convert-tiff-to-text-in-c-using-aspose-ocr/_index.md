---
category: general
date: 2026-03-05
description: Convertissez les TIFF en texte en C# rapidement avec Aspose OCR. Apprenez
  à afficher le texte OCR des fichiers TIFF multipages en quelques minutes.
draft: false
keywords:
- convert tiff to text
- aspose ocr c#
- display ocr text
language: fr
og_description: Convertissez les TIFF en texte en C# avec Aspose OCR. Ce guide vous
  montre comment afficher le texte OCR à partir d’images TIFF multipages, étape par
  étape.
og_title: Convertir TIFF en texte avec C# – Guide complet d’Aspose OCR
tags:
- Aspose
- OCR
- C#
- TIFF
title: Convertir TIFF en texte en C# à l'aide d'Aspose OCR
url: /fr/net/text-recognition/convert-tiff-to-text-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir TIFF en texte en C# avec Aspose OCR

Besoin de **convertir TIFF en texte** en C# ? Vous n'êtes pas seul — de nombreux développeurs peinent à extraire des chaînes lisibles à partir de fichiers TIFF multi‑pages. La bonne nouvelle, c’est que Aspose OCR C# rend la tâche presque indolore, et vous pouvez **afficher le texte OCR** sur la console ou le transmettre à un autre système en quelques secondes.

Dans ce tutoriel, nous allons parcourir un exemple complet, prêt à être exécuté, qui montre exactement comment charger un TIFF multi‑pages, exécuter l’OCR et imprimer le texte de chaque page. Aucun pas caché, aucune astuce du type « voir la documentation ». À la fin, vous disposerez d’un programme autonome que vous pourrez intégrer à n’importe quel projet .NET.

## Ce dont vous avez besoin

- .NET 6.0 ou supérieur (l’exemple cible .NET 6, mais .NET 5 fonctionne également)  
- Un fichier de licence Aspose OCR valide (`Aspose.OCR.lic`). La bibliothèque fonctionne sans licence, mais vous verrez un filigrane d’essai de 20 secondes.  
- Un fichier TIFF multi‑pages que vous souhaitez traiter (nous l’appellerons `multipage.tif`).  
- Visual Studio 2022 ou tout éditeur de votre choix — rien d’exotique.

Si ces points sont cochés, plongeons‑y.

## Étape 1 : Installer le package NuGet Aspose OCR

Avant que le code ne s’exécute, vous avez besoin de la bibliothèque elle‑même. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Cette ligne unique récupère la dernière version stable (en mars 2026, c’est la 23.9).  

> **Astuce pro :** Gardez vos packages à jour ; les nouvelles versions incluent souvent des améliorations de performances pour les gros TIFF.

## Étape 2 : Configurer la licence Aspose OCR C# (Optionnel mais recommandé)

Faire fonctionner le moteur OCR sans licence est possible, mais la sortie sera préfixée d’un avertissement d’essai. Pour éviter cela, pointez le moteur vers votre fichier `.lic` :

```csharp
using Aspose.OCR;

// ...

// Step 2: Apply your Aspose OCR license (optional but recommended)
var ocrEngine = new OcrEngine();
ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
```

Si vous sautez cette étape, le code fonctionnera toujours — il suffit de retenir le texte supplémentaire dans les résultats.

## Étape 3 : Charger et reconnaître le TIFF multi‑pages

Nous allons maintenant réellement **convertir TIFF en texte**. L’assistant `ImageStream.FromFile` lit le fichier dans un format que le moteur comprend. Ensuite, nous appelons `Recognize()` qui renvoie un objet `OcrResult` contenant le texte de chaque page.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 3: Load the multi‑page TIFF image to be processed
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\multipage.tif");

// Step 4: Perform OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize();
```

> **Pourquoi c’est important :** `Recognize()` effectue le travail lourd — analyse des pixels, détection de la langue et reconstruction des lignes de texte—tout en code C# natif. L’objet résultat vous donne un accès page par page, idéal pour **afficher le texte OCR** plus tard.

## Étape 4 : Parcourir les pages et **afficher le texte OCR**

Avec le résultat en main, nous parcourons simplement les pages et imprimons chacune d’elles. C’est la partie où vous voyez réellement la conversion d’image en texte brut.

```csharp
// Step 5: Iterate through each page of the result and display the recognized text
for (int pageIndex = 0; pageIndex < ocrResult.PageCount; pageIndex++)
{
    Console.WriteLine($"--- Page {pageIndex + 1} ---");
    Console.WriteLine(ocrResult.GetPageText(pageIndex));
    Console.WriteLine(); // Blank line for readability
}
```

L’exécution du programme produit une sortie similaire à celle‑ci-dessous (votre texte réel variera selon le contenu du TIFF) :

```
--- Page 1 ---
Hello, world!
This is the first page of our multi‑page TIFF.

--- Page 2 ---
Second page starts here.
More sample text follows.
```

Voilà — vous avez **converti TIFF en texte** et **affiché le texte OCR** pour chaque page.

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console (`dotnet new console`). Il inclut toutes les directives `using`, la gestion de la licence et la vérification des erreurs.

```csharp
// ConvertTiffToText.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace ConvertTiffToText
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -----------------------------------------------------------------
            // Step 2: Apply your Aspose OCR license (optional but recommended)
            // -----------------------------------------------------------------
            try
            {
                ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");
            }
            catch (Exception ex)
            {
                Console.WriteLine("License file not found or invalid. Running in trial mode.");
                Console.WriteLine($"Details: {ex.Message}");
            }

            // -----------------------------------------------------------------
            // Step 3: Load the multi‑page TIFF image to be processed
            // -----------------------------------------------------------------
            const string tiffPath = @"C:\Images\multipage.tif";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"Error: TIFF file not found at {tiffPath}");
                return;
            }

            ocrEngine.Image = ImageStream.FromFile(tiffPath);

            // -----------------------------------------------------------------
            // Step 4: Perform OCR – this is where we convert TIFF to text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize();

            // -----------------------------------------------------------------
            // Step 5: Iterate through each page and display OCR text
            // -----------------------------------------------------------------
            Console.WriteLine($"Successfully processed {ocrResult.PageCount} page(s).");
            for (int i = 0; i < ocrResult.PageCount; i++)
            {
                Console.WriteLine($"--- Page {i + 1} ---");
                Console.WriteLine(ocrResult.GetPageText(i));
                Console.WriteLine(); // Add spacing between pages
            }

            // Keep the console window open when debugging
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Sortie attendue** (truncée pour la brièveté) est montrée plus haut. Si vous voyez le filigrane d’essai, revérifiez que le chemin de la licence est correct.

## Pièges courants lors de la conversion de TIFF en texte

| Problème | Pourquoi cela se produit | Comment corriger |
|----------|--------------------------|------------------|
| **Manque de mémoire sur de très gros TIFF** | Le moteur charge l’image entière en RAM. | Utilisez `ImageStream.FromFile(..., loadOnlyFirstPage: false)` et traitez les pages par lots, ou augmentez la limite de mémoire du processus. |
| **Caractères parasites** | Les images source à basse résolution déconcertent le moteur OCR. | Pré‑traitez le TIFF (par ex., augmentez le DPI à 300) avant de le passer à Aspose OCR. |
| **Licence non appliquée** | `SetLicense` lève une exception que vous ignorez. | Enveloppez l’appel dans un try/catch (comme montré) et consignez l’erreur. |
| **Données de langue manquantes** | Par défaut, l’OCR suppose l’anglais. | Définissez `ocrEngine.Language = OcrLanguage.French;` (ou toute langue prise en charge) avant `Recognize()`. |

Traiter ces cas limites garantit que votre conversion fonctionne sans accroc en production.

## Prochaines étapes : Aller au-delà de l’affichage simple

Maintenant que vous pouvez **convertir TIFF en texte** et **afficher le texte OCR**, vous pourriez vouloir :

- **Enregistrer le texte extrait** dans un fichier `.txt` ou une base de données pour une analyse ultérieure.  
- **Combiner plusieurs TIFF** en un seul PDF consultable à l’aide d’Aspose.PDF.  
- **Appliquer un post‑traitement** (vérification orthographique, nettoyage par expressions régulières) pour améliorer la précision.  

Toutes ces extensions s’appuient sur le même schéma de base que nous venons de couvrir.

---

### TL;DR

Nous avons parcouru une solution C# complète qui **convertit TIFF en texte** avec Aspose OCR C#. Le code crée un `OcrEngine`, charge éventuellement une licence, lit un TIFF multi‑pages, exécute l’OCR et **affiche le texte OCR** page par page. Avec l’exemple complet fourni, vous pouvez l’insérer dans n’importe quel projet .NET et commencer à extraire du texte immédiatement.

Des questions sur les performances, la prise en charge des langues ou l’intégration avec d’autres produits Aspose ? Laissez un commentaire ci‑dessous—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}