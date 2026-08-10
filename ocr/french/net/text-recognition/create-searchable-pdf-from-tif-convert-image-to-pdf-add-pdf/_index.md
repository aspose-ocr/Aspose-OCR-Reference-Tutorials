---
category: general
date: 2026-04-04
description: Créer un PDF consultable à partir d’une image TIF en C# – apprenez comment
  convertir une image en PDF, ajouter des métadonnées PDF et générer un document consultable
  à l’aide d’Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: fr
og_description: Créer un PDF consultable à partir d'un fichier TIF avec C#. Convertir
  l'image en PDF, ajouter des métadonnées PDF et produire un document consultable
  en utilisant Aspose.OCR.
og_title: Créer un PDF interrogeable à partir de TIF – Guide étape par étape
tags:
- Aspose.OCR
- C#
- PDF generation
title: Créer un PDF consultable à partir de TIF – Convertir l'image en PDF, ajouter
  des métadonnées PDF
url: /fr/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir de TIF – Guide complet C# Walkthrough

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d'une facture numérisée mais vous ne saviez pas comment garder le texte consultable et les métadonnées du fichier bien organisées ? Vous n'êtes pas seul. Dans de nombreux projets d'automatisation, le PDF doit être à la fois lisible par machine et correctement balisé avec des informations telles que le titre, l'auteur et les seuils de confiance.  

Dans ce guide, nous parcourrons une solution complète qui **convertit une image en PDF**, injecte des **métadonnées PDF**, et filtre les résultats OCR à faible confiance — le tout avec la bibliothèque Aspose.OCR. À la fin, vous disposerez d’un extrait prêt à l’emploi que vous pourrez intégrer dans n’importe quel projet .NET, ainsi que de quelques astuces pour gérer les cas particuliers.

## Prérequis

- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.6+)  
- Aspose.OCR NuGet package (`Install-Package Aspose.OCR`)  
- Une image TIF que vous souhaitez transformer en PDF consultable (par ex., `input.tif`)  
- Une connaissance de base du C# et de Visual Studio (ou de votre IDE préféré)

Aucun autre service externe n’est requis — le processus s’exécute entièrement en local.

## Étape 1 – Configurer le moteur OCR (Noyau du PDF consultable)

La première chose dont nous avons besoin est d’une instance `OcrEngine` qui sait quelle langue reconnaître. Dans la plupart des scénarios d’entreprise, l’anglais suffit, mais vous pouvez remplacer `Language.English` par n’importe quelle langue prise en charge.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Pourquoi c’est important :** Le moteur OCR effectue le travail lourd de conversion des pixels raster en texte Unicode. Définir correctement la langue améliore la précision et réduit le nombre de mots à faible confiance qui seront ensuite filtrés.

> **Astuce :** Si vous traitez des documents multilingues, créez plusieurs moteurs ou utilisez `Language.Multilingual` pour laisser Aspose gérer automatiquement la détection de la langue.

## Étape 2 – Charger l'image TIF (Créer un PDF à partir du TIF)

Nous pointons maintenant le moteur vers le fichier source. L’utilitaire `ImageStream.FromFile` lit l’image dans un flux que le moteur OCR peut consommer.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Vous vous demandez peut‑être, *« Puis‑je fournir un JPEG ou un PNG à la place ? »* Absolument — Aspose.OCR prend en charge la plupart des formats raster. Il suffit de changer l’extension du fichier et le tour est joué.

## Étape 3 – Configurer les options PDF (Ajouter des métadonnées au PDF)

Avant la conversion, nous définissons un objet `PdfOptions`. C’est ici que nous **ajoutons des métadonnées PDF** comme le titre et l’auteur, et où nous indiquons également au moteur de supprimer les mots dont la confiance est inférieure à un seuil.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Que se passe-t-il ici ?**  
- `Title` et `Author` deviennent partie du dictionnaire d’informations du document PDF, facilitant l’indexation du fichier dans les systèmes de gestion documentaire.  
- `MinConfidence` agit comme une barrière de sécurité : l’OCR lit souvent mal les caractères pâles ; les filtrer maintient la couche consultable propre et améliore l’extraction de texte en aval.

Si vous avez besoin de métadonnées personnalisées (par ex., `Subject`, `Keywords`), vous pouvez les définir via `PdfOptions.CustomProperties`.

## Étape 4 – Convertir l'image en PDF consultable (Convertir l'image en PDF)

Avec le moteur prêt et les options configurées, l’appel final effectue la conversion. Il écrit un PDF consultable sur le disque, en intégrant la couche de texte OCR sous l’image originale.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Après l’exécution de cette ligne, `output.pdf` contient :
- L’image TIF originale comme arrière‑plan visuel  
- Une couche de texte invisible que les moteurs de recherche et les opérations copier‑coller peuvent lire  
- Les métadonnées que nous avons définies précédemment (titre, auteur, etc.)

### Résultat attendu

Ouvrez le PDF généré dans Adobe Reader ou tout autre visualiseur PDF et essayez de sélectionner du texte. Vous devriez pouvoir copier des phrases qui correspondent à la numérisation originale. La boîte de dialogue **Propriétés** du document affichera le titre « Invoice #12345 » et l’auteur « MyCompany ».

## Étape 5 – Vérifier le filtrage par confiance (Pourquoi MinConfidence aide)

Il est utile de confirmer que les mots à faible confiance ont bien été supprimés. Vous pouvez inspecter le texte caché du PDF à l’aide d’un outil comme `pdftotext` :

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Si le mot n’apparaît jamais, le filtre `MinConfidence` a fonctionné comme prévu. Ajustez le seuil (par ex., `0.7f`) si vous avez besoin d’un filtre plus agressif ou plus permissif.

## Étape 6 – Gérer plusieurs pages (Créer un PDF consultable à partir d’un TIF multi‑pages)

De nombreuses factures sont des TIFF multi‑pages. Aspose.OCR traite chaque trame comme une page distincte automatiquement. Il suffit de pointer le moteur vers le fichier multi‑pages ; le même appel `ConvertToSearchablePdf` générera un PDF consultable multi‑pages.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Cas particulier :** Si une page est vide, l’OCR peut quand même générer une couche de texte vide, ce qui est sans danger. Cependant, vous pouvez ignorer les pages vides en vérifiant `ocrEngine.HasText` avant la conversion.

## Étape 7 – Regrouper l’exemple complet (Toutes les étapes ensemble)

Ci‑dessous se trouve un programme unique, prêt à l’exécution, qui réunit tous les éléments. Remplacez `YOUR_DIRECTORY` par le chemin réel du dossier sur votre machine.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Exécutez le programme (`dotnet run` ou appuyez sur **F5** dans Visual Studio) et vous verrez le message de confirmation. Le PDF généré se trouve à côté de votre image source, prêt pour l’indexation ou l’archivage.

## Questions fréquentes & pièges

| Question | Réponse |
|----------|--------|
| **Puis‑je ajouter une police personnalisée à la couche consultable ?** | La couche OCR utilise Unicode ; l’apparence visuelle est déterminée par l’image sous‑jacente, donc aucun embarquement de police supplémentaire n’est requis. |
| **Et si mon TIF est en couleur ?** | Aspose.OCR convertit automatiquement les images couleur en niveaux de gris pour l’OCR, mais vous pouvez conserver les couleurs originales dans le PDF en définissant `PdfOptions.PreserveColor = true`. |
| **La bibliothèque est‑elle thread‑safe ?** | Chaque instance `OcrEngine` doit être utilisée par un seul thread. Pour le traitement parallèle, créez un moteur distinct par thread. |
| **Comment chiffrer le PDF ?** | Utilisez `PdfOptions.Security` pour définir un mot de passe et des permissions après la conversion OCR. |

## Prochaines étapes (Développez votre boîte à outils PDF)

- **Traitement par lots :** Parcourez un dossier de TIFF et générez un PDF consultable pour chaque fichier.  
- **Post‑traitement :** Utilisez Aspose.PDF pour fusionner les PDF générés en un seul document maître.  
- **Métadonnées avancées :** Remplissez des champs XMP personnalisés pour une meilleure intégration avec SharePoint ou les systèmes ECM.  

Toutes ces extensions s’appuient sur le modèle de base que nous venons de couvrir : **créer un PDF consultable**, **convertir une image en PDF**, et **ajouter des métadonnées PDF**.

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous ou consultez la documentation Aspose.OCR pour les dernières mises à jour de l’API.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}