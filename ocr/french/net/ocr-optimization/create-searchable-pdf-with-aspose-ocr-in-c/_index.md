---
category: general
date: 2026-04-01
description: Créer un PDF consultable en C# avec Aspose OCR – apprenez à convertir
  un PDF numérisé, ajouter l’OCR au PDF et activer l’accélération GPU pour des résultats
  rapides.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: fr
og_description: Créez rapidement un PDF consultable en C# — convertissez un PDF numérisé,
  ajoutez l’OCR au PDF et activez l’accélération GPU pour un traitement haute performance.
og_title: Créer un PDF interrogeable avec Aspose OCR en C#
tags:
- Aspose OCR
- C#
- PDF processing
title: Créer un PDF interrogeable avec Aspose OCR en C#
url: /fr/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable avec Aspose OCR en C#

Vous avez déjà eu besoin de **créer des PDF consultables** à partir d’une pile de documents numérisés ? Vous n’êtes pas le seul — de nombreuses équipes luttent pour transformer des PDF uniquement image en ressources recherchables par texte. La bonne nouvelle ? Avec Aspose OCR, vous pouvez **convertir un PDF numérisé** en une version entièrement consultable en quelques lignes de code C#. Dans ce guide, nous parcourrons tout le processus, de l’ajout d’OCR au PDF à l’**activation de l’accélération GPU** pour un gain de vitesse.

Nous vous montrerons également comment **convertir un pdf en format consultable**, expliquerons pourquoi vous pourriez vouloir **ajouter de l’OCR à un PDF**, et vous donnerons des astuces pratiques pour gérer de gros lots. À la fin, vous disposerez d’une application console prête à l’emploi qui produit un PDF consultable que vous pourrez intégrer à n’importe quel système de gestion de documents.

---

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d’avoir les éléments suivants :

- **.NET 6.0** ou version ultérieure (l’API fonctionne également avec le .NET Framework, mais .NET 6+ est le meilleur choix).
- **Aspose.OCR for .NET** package NuGet (`Install-Package Aspose.OCR`).
- Un fichier PDF numérisé (uniquement image) à utiliser comme entrée.
- Optionnel : une machine compatible GPU avec CUDA® installé si vous souhaitez **activer l’accélération GPU**.

C’est tout—pas de moteurs OCR lourds, pas de services externes. Tout s’exécute localement.

---

## Créer un PDF consultable – Vue d’ensemble étape par étape

Voici le flux de haut niveau que nous allons suivre :

1. **Initialiser le moteur OCR** – indiquez à Aspose la langue à rechercher et si vous utilisez le GPU.
2. **Pointer le moteur vers votre PDF numérisé** – définissez les chemins d’entrée et de sortie.
3. **Lancer la conversion** – Aspose effectue le travail lourd et écrit un PDF consultable.
4. **Vérifier le résultat** – ouvrez le fichier de sortie et effectuez une recherche de texte.

Chaque étape est détaillée dans sa propre section, afin que vous puissiez choisir les parties qui vous intéressent le plus.

---

## Convertir un PDF numérisé en PDF consultable

La première chose à faire est de créer une instance de `OcrEngine`. Cet objet est le cheval de bataille qui lit les images raster à l’intérieur de votre PDF et extrait le texte.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Pourquoi cela fonctionne :** `ConvertToSearchablePdf` lit chaque page, exécute l’OCR sur le contenu raster, puis intègre une couche de texte invisible derrière l’image originale. Le résultat ressemble exactement au document numérisé d’origine, mais vous pouvez maintenant copier, sélectionner et rechercher le texte.

---

## Ajouter de l’OCR à un PDF avec Aspose

Si vous avez déjà un PDF et que vous souhaitez simplement **ajouter de l’OCR à un PDF** sans convertir l’ensemble du fichier, vous pouvez appeler la même méthode — Aspose traite l’opération comme « ajout d’OCR ». Le code ci‑dessus le fait déjà, mais voici une variante rapide qui montre comment traiter plusieurs fichiers dans une boucle :

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Astuce :** Conservez la même instance de `OcrEngine` pour tout le lot. La recréer à chaque fois ajoute une surcharge inutile, surtout lorsque vous **activez l’accélération GPU**.

---

## Activer l’accélération GPU pour un OCR plus rapide

L’accélération GPU peut faire gagner des minutes sur un gros lot. Aspose OCR exploite NVIDIA CUDA en interne, il suffit donc de basculer un drapeau booléen :

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Quand l’utiliser :** Si vous traitez des PDF de plus de 10 Mo ou plus d’une dizaine de fichiers, le GPU vous offrira généralement un gain de vitesse de 2‑3×. Sur un ordinateur portable modeste sans GPU compatible CUDA, laissez‑le à `false` — la bibliothèque reviendra automatiquement au CPU.

**Piège fréquent :** Oublier d’installer la bonne version du driver CUDA peut provoquer une exception d’exécution (`CudaException`). Assurez‑vous que votre driver correspond à la version attendue par Aspose (voir les notes de version sur la page NuGet).

---

## Exemple complet fonctionnel (toutes les étapes combinées)

Voici une application console autonome que vous pouvez copier‑coller dans un nouveau projet .NET. Elle inclut des commentaires utiles, la gestion des erreurs, et une étape finale de vérification qui affiche le nombre de pages traitées.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Sortie attendue**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

Ouvrez `output.pdf` avec n’importe quel lecteur PDF et essayez de taper un mot présent dans les images numérisées. Si le texte est mis en surbrillance, vous avez réussi à **créer un pdf consultable**.

---

## Problèmes courants et astuces professionnelles

| Problème | Pourquoi cela se produit | Comment corriger / éviter |
|----------|--------------------------|---------------------------|
| **GPU non détecté** | Driver CUDA manquant ou incompatible. | Installez la version de driver indiquée dans les notes de version d’Aspose ; définissez `UseGpuAcceleration = false` comme solution de secours. |
| **Langue incorrecte** | L’OCR utilise l’anglais par défaut ; d’autres langues nécessitent une configuration explicite. | Définissez `Language = Language.Spanish` (ou tout autre enum supporté) avant la conversion. |
| **PDF volumineux provoquant OutOfMemory** | Le moteur charge des pages entières en mémoire. | Traitez le PDF par morceaux avec `ocrEngine.PageRange = new PageRange(1, 5)` pour chaque lot. |
| **Fichier de sortie corrompu** | Le dossier de destination n’a pas les droits d’écriture. | Exécutez l’application avec des droits élevés ou choisissez un chemin accessible en écriture. |
| **Couche de texte non consultable** | Le visualiseur met en cache une ancienne version. | Rafraîchissez le visualiseur PDF ou rouvrez le fichier. |

**Astuce pro :** Lorsque vous avez un mélange de PDF numérisés et natifs, vérifiez le drapeau `HasText` de chaque page (`PdfPageInfo.HasText`) avant d’exécuter l’OCR. Cela économise des cycles CPU et évite un double OCR sur les pages déjà consultables.

---

## Vérifier le résultat par programme (optionnel)

Si vous souhaitez automatiser la vérification, Aspose.PDF peut extraire le texte caché :

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Cet extrait montre que vous avez réellement **converti un pdf en format consultable**, et pas seulement superposé une image.

---

## Exemple d’image

![Create searchable PDF output example](https://example.com/images/searchable-pdf.png "Create searchable PDF using Aspose OCR")

*Texte alternatif :* **exemple de création de pdf consultable** montrant la vue avant (numérisée) et après (consultable).

---

## Prochaines étapes & sujets associés

- **Traitement par lots :** Enveloppez la boucle de la section « Ajouter de l’OCR à un PDF » dans un service Windows ou une Azure Function pour des travaux nocturnes.
- **Support linguistique avancé :** Explorez `ocrEngine.Language = Language.Multilingual` pour les documents contenant des scripts mixtes.
- **Nettoyage post‑OCR :** Utilisez `TextFragmentAbsorber` d’Aspose.PDF pour corriger les erreurs d’OCR courantes (ex. : « 0 » vs « O »).
- **Sécurité**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}