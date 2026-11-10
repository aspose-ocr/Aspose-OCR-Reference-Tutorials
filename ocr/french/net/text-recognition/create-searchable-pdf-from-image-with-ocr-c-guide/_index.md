---
category: general
date: 2026-03-18
description: Créez un PDF consultable avec Aspose OCR en C#. Convertissez l’image
  en PDF, ajoutez une couche de texte OCR et écrivez les octets du PDF dans un fichier
  en quelques étapes simples.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: fr
og_description: Créez rapidement un PDF recherchable avec Aspose OCR en C#. Apprenez
  comment convertir une image en PDF, ajouter une couche de texte OCR et écrire les
  octets du PDF dans un fichier.
og_title: Créer un PDF recherchable à partir d'une image – Guide rapide OCR en C#
tags:
- OCR
- PDF
- C#
- Aspose
title: Créer un PDF consultable à partir d'une image avec OCR – Guide C#
url: /fr/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable à partir d'une image avec OCR – Guide C#

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d'une image numérisée ? Avec Aspose OCR, vous pouvez le faire en quelques lignes, sans bibliothèques lourdes. Dans ce tutoriel, nous allons **convertir une image en PDF**, ajouter une **couche de texte OCR** au-dessus, et enfin **écrire les octets PDF dans un fichier** afin d’obtenir un document PDF/A‑2b conforme aux normes que vos utilisateurs pourront réellement rechercher.

Si vous vous demandez pourquoi vous embaucheriez un PDF consultable plutôt qu'un simple fichier image, pensez à l'expérience utilisateur : un PDF consultable permet aux gens de copier, sélectionner et indexer le texte—idéal pour les archives, les documents juridiques ou tout flux de travail nécessitant une extraction de texte ultérieure. Allons‑y.

## Ce dont vous avez besoin

- .NET 6 ou version ultérieure (le code fonctionne également sur .NET Framework 4.7+)
- Un package NuGet Aspose.OCR (`Aspose.OCR` version 23.10 ou plus récent)
- Une image raster (`.png`, `.jpg`, etc.) que vous souhaitez transformer en PDF consultable
- Une connaissance modeste de C#—rien de sophistiqué, juste les bases

C’est tout. Aucun outil externe, aucun convertisseur supplémentaire. Toute la lourde tâche est prise en charge par le moteur OCR d’Aspose.

## Créer un PDF consultable – Vue d'ensemble

Avant de plonger dans le code, décrivons le processus :

1. **Instancier** le moteur OCR – cet objet sait comment lire le texte à partir d'images.  
2. **Charger** l'image source – nous fournirons un `ImageStream` au moteur.  
3. **Configurer** les options d’enregistrement PDF/A‑2b – cela indique à Aspose d’intégrer le texte reconnu comme une couche cachée.  
4. **Exécuter** l'OCR et **capturer** les octets PDF résultants.  
5. **Écrire** ces octets sur le disque, produisant le fichier PDF consultable final.

Chacune de ces étapes correspond directement à une ou deux lignes de C#, ce qui fait que l’ensemble du flux de travail ressemble à un petit script plutôt qu’à un projet massif.

## Étape 1 : Convertir l'image en PDF – Charger l'image

Première chose à faire : nous devons fournir au moteur OCR quelque chose à lire. L’utilitaire `ImageStream.FromFile` charge le fichier dans un flux que Aspose peut traiter.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Astuce :** Gardez la résolution de votre image à 300 dpi ou plus ; la précision de l'OCR chute fortement avec des numérisations basse résolution.

## Étape 2 : Reconnaître le texte de l'image et ajouter une couche de texte OCR

Nous créons maintenant le moteur OCR et lui indiquons de reconnaître le texte. La magie se produit lorsque nous associons le résultat de la reconnaissance à `PdfSaveOptions` avec `IncludeTextLayer = true`. Ce drapeau force Aspose à intégrer les caractères extraits comme une couche de texte invisible, ce qui rend le PDF consultable.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Pourquoi PDF/A‑2b ? C’est un format d’archivage ISO qui garantit la préservation à long terme et, ce qui est important pour nous, oblige le PDF à contenir une couche de texte consultable. Si vous n’avez pas besoin de conformité archivistique, vous pouvez supprimer complètement `PdfCompliance`, mais le garder ne vous coûte rien.

## Étape 3 : Écrire les octets PDF dans un fichier – Enregistrer le résultat

Avec le moteur prêt et les options définies, nous exécutons la reconnaissance et demandons immédiatement à Aspose de nous fournir le PDF sous forme de `byte[]`. Ensuite nous écrivons ces octets sur le disque en utilisant `File.WriteAllBytes`. Simple, mais puissant.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Cette ligne `Console.WriteLine` est optionnelle, mais elle vous donne un retour instantané lorsque vous exécutez le programme depuis un terminal.

## Exemple complet fonctionnel

En réunissant tous les éléments, voici le programme complet, prêt à être exécuté. Copiez‑collez‑le dans un nouveau projet console, remplacez `YOUR_DIRECTORY` par un chemin réel, et appuyez sur **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Résultat attendu

- Un fichier nommé `output.pdf` apparaît dans le dossier que vous avez spécifié.  
- Ouvrez‑le dans Adobe Acrobat Reader ou tout lecteur PDF et essayez de sélectionner du texte—si vous pouvez copier des mots, vous avez réussi à **créer un PDF consultable**.  
- Le document passera également les outils de validation PDF/A‑2b car nous avons utilisé le drapeau de conformité approprié.

## Questions fréquentes & cas limites

**Et si mon image contient plusieurs pages ?**  
Enveloppez chaque page dans son propre `ImageStream` et alimentez‑les séquentiellement au `OcrEngine`. Aspose concaténera automatiquement les pages en un seul PDF.

**Puis‑je changer la langue de l'OCR ?**  
Absolument. Définissez `ocrEngine.Language = Language.English;` (ou toute langue prise en charge) avant d’appeler `Recognize`.

**Qu’en est‑il de l’utilisation de la mémoire pour les fichiers volumineux ?**  
Si vous traitez des numérisations de l’ordre du gigaoctet, envisagez de diffuser le résultat directement vers un `FileStream` au lieu de conserver l’ensemble du `byte[]` en mémoire :

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Ai‑je besoin d’une licence ?**  
Aspose propose un essai gratuit sans filigrane. Pour une utilisation en production, achetez une licence afin de supprimer la bannière d’évaluation et de débloquer toutes les fonctionnalités.

## Conseils pour améliorer la précision de l'OCR

- **Pré‑traitez** l'image : redressez, débruitez et augmentez le contraste.  
- **Utilisez des formats sans perte** comme PNG ; les artefacts de compression JPEG peuvent perturber le moteur.  
- **Évitez les arrière‑plans colorés** ; un fond blanc uni donne les meilleurs résultats.

## Prochaines étapes

Maintenant que vous pouvez **créer des PDF consultables**, vous pourriez vouloir :

- **Traiter par lots** un dossier d’images en utilisant `Directory.GetFiles`.  
- **Extraire le texte caché** plus tard avec les API `PdfDocument` pour l’indexation.  
- **Combiner l'OCR avec des signatures numériques** pour créer des archives à l’épreuve de la falsification.  

Tous ces éléments reposent sur le même schéma de base que nous avons couvert : charger, reconnaître, configurer, enregistrer.

---

*Prêt à transformer vos archives numérisées en PDF consultables ? Prenez le code, pointez‑le vers vos images, et laissez Aspose faire le gros du travail. Bon codage !*

![Create searchable PDF example](/images/create-searchable-pdf.png "Illustration of a searchable PDF generated from an image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}