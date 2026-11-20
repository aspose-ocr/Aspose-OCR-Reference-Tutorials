---
category: general
date: 2026-04-26
description: Créer un PDF consultable à partir d’une image numérisée avec Aspose OCR
  en C#. Apprenez à convertir l’image numérisée, extraire le texte et générer rapidement
  un PDF consultable.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: fr
og_description: Créer un PDF consultable à partir d’une image numérisée avec Aspose
  OCR. Code C# étape par étape pour convertir, extraire le texte et générer un PDF
  consultable.
og_title: Créer un PDF consultable à partir d'une image numérisée – Guide C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Créer un PDF consultable à partir d'une image numérisée – Guide C#
url: /fr/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir d’une image numérisée – Guide C#

Vous avez déjà eu besoin de **créer des fichiers PDF consultables** à partir de contrats papier, de reçus ou d’archives anciennes ? Vous n’êtes pas seul — la plupart des développeurs rencontrent ce problème lorsqu’un client remet une pile de scans TIFF et attend un PDF consultable en livrable final.  

Dans ce tutoriel, nous vous montrons exactement **comment OCRiser un document** et transformer une image numérisée en **PDF consultable** avec Aspose OCR pour .NET. À la fin, vous pourrez **convertir des fichiers d’image numérisée**, **extraire du texte d’une image**, et même gérer des TIFF multi‑pages sans effort.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir :

* .NET 6.0 ou supérieur (l’API fonctionne avec .NET Core, .NET Framework et .NET 5+).  
* Une licence valide Aspose OCR ou accepter le filigrane d’évaluation.  
* Le package NuGet `Aspose.OCR` installé (`dotnet add package Aspose.OCR`).  
* Un fichier TIFF d’exemple (par ex., `contract_scan.tif`) que vous souhaitez transformer en PDF consultable.

C’est tout — pas de bibliothèques supplémentaires, pas de configuration compliquée. Prêt ? C’est parti.

![Exemple de PDF consultable](create-searchable-pdf.png "exemple de pdf consultable")

## Étape 1 – Initialiser le moteur OCR (Créer un PDF consultable)

Première chose à faire : créer une instance d’`OcrEngine`. Cet objet est le cheval de bataille qui lit le bitmap, identifie les caractères et vous renvoie le texte.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Pourquoi définir la langue ?**  
Si vous laissez la valeur par défaut, Aspose essaiera tous les packs de langues, ce qui ralentit le processus. Spécifier `Language.Latin` indique au moteur de se concentrer sur l’alphabet latin, offrant ainsi un gain de vitesse et des résultats plus précis pour les contrats en anglais.

## Étape 2 – Charger votre image numérisée (Convertir l’image numérisée)

Nous fournissons maintenant au moteur l’image à traiter. Aspose peut lire un chemin de fichier, un flux, ou même un `byte[]`. Pour la simplicité, nous utiliserons `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Si vous devez plus tard **convertir un TIFF en PDF**, gardez à l’esprit que les TIFF multi‑pages sont gérés automatiquement — chaque trame devient une page PDF distincte.

## Étape 3 – Exécuter l’OCR et récupérer le texte (Extraire du texte d’une image)

Lancer l’OCR est aussi simple que d’appeler `Recognize`. Le moteur renvoie un `RecognitionResult` contenant le texte brut, les scores de confiance et les informations de mise en page.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Astuce :** Si vous avez seulement besoin du texte (pas de PDF), vous pouvez vous arrêter ici et écrire `extractedText` dans un fichier `.txt`. Mais la plupart du temps, notre objectif est un PDF consultable, nous continuons donc.

## Étape 4 – Enregistrer en PDF consultable (Créer un PDF consultable)

Aspose rend l’étape finale triviale : il suffit d’appeler `Save` avec `SaveFormat.PdfSearchable`. En interne, la bibliothèque intègre le texte extrait comme couche invisible tout en conservant l’apparence de l’image d’origine.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Lorsque vous ouvrirez `contract_searchable.pdf` dans n’importe quel lecteur PDF, vous pourrez sélectionner, copier et rechercher le texte — exactement ce qu’attend un client d’un « PDF consultable ».

## Gestion des TIFF multi‑pages (Convertir TIFF en PDF)

Si votre fichier source comporte plusieurs pages, Aspose traitera chaque trame comme une page distincte automatiquement. Aucun boucle supplémentaire n’est nécessaire. Vous pouvez toutefois contrôler le DPI ou la qualité d’image pour chaque page :

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Après avoir configuré ces options, répétez **l’Étape 2** pour chaque trame, ou pointez simplement `ImageStream.FromFile` vers le TIFF multi‑pages et laissez Aspose faire le travail lourd.

## Pièges courants et solutions

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Le texte est illisible ou manquant | Mauvaise langue définie | Définissez `ocrEngine.Language` sur le pack de langue correct (par ex., `Language.German`). |
| Le PDF est volumineux (10 Mo pour un scan d’une page) | Compression d’image par défaut trop faible | Ajustez `ocrEngine.ImageProcessingOptions.Compression` à `Jpeg` et choisissez une valeur `Quality` raisonnable (0‑100). |
| L’OCR est très lent | Utilisation de la détection de langue `Auto` par défaut | Spécifiez explicitement la langue attendue. |
| Aucun calque consultable n’apparaît | Enregistrement avec `SaveFormat.Pdf` au lieu de `PdfSearchable` | Utilisez `PdfSearchable`. |

## Exemple complet de bout en bout

En rassemblant le tout, voici une application console prête à être exécutée que vous pouvez copier‑coller dans Visual Studio :

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Ce que vous verrez :**  
* Une fenêtre console affichant un extrait du texte OCRisé.  
* Un fichier `contract_searchable.pdf` placé à côté de votre TIFF d’origine. Ouvrez‑le, appuyez sur **Ctrl + F**, et recherchez n’importe quel mot présent dans le scan original — voilà, ça fonctionne.

## Prochaines étapes & Sujets connexes

* **Comment OCRiser des lots de documents** – encapsulez le code ci‑dessus dans une boucle `foreach` et traitez un dossier complet.  
* **Convertir d’autres formats d’image numérisée** (PNG, JPEG) – la même API fonctionne ; il suffit de changer l’extension du fichier.  
* **Extraire du texte d’une image** pour une analyse ultérieure – alimentez `result.Text` dans une chaîne de traitement de langage naturel.  
* **Optimiser la taille du PDF** – explorez `PdfSaveOptions` pour compresser davantage les images ou n’incorporer les polices que si nécessaire.  

Expérimentez avec ces idées, et vous deviendrez rapidement la référence pour toute demande « transformer ce scan en PDF consultable ».

---

### TL;DR

Vous savez maintenant comment **créer des fichiers PDF consultables** à partir d’images numérisées en utilisant Aspose OCR en C#. Le processus est : initialiser le moteur, charger l’image, exécuter l’OCR, et enregistrer avec `PdfSearchable`. Ajustez les paramètres de langue, DPI et compression pour gérer les cas particuliers, et vous êtes prêt à **convertir des images numérisées**, **extraire du texte d’une image**, et même **convertir des TIFF en PDF** à grande échelle. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}