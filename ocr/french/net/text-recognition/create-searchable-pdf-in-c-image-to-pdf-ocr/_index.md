---
category: general
date: 2026-02-28
description: Créer un PDF consultable à partir d'un TIFF multipage en C#. Ce guide
  montre comment convertir une image en PDF consultable avec un exemple complet d’OCR
  en C#.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- convert tiff to pdf
- c# ocr example
- c# image to pdf
language: fr
og_description: Créez un PDF consultable à partir d’un TIFF avec Aspose.OCR. Suivez
  cet exemple OCR C# étape par étape pour transformer les images en PDF consultables.
og_title: Créer un PDF consultable en C# – Image vers PDF OCR
tags:
- OCR
- PDF
- C#
- Aspose
title: Créer un PDF recherchable en C# – Image vers PDF OCR
url: /fr/net/text-recognition/create-searchable-pdf-in-c-image-to-pdf-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable en C# – Image vers PDF OCR

Vous avez déjà eu besoin de **créer un PDF consultable** à partir d'un document numérisé mais vous ne saviez pas par où commencer ? Vous n'êtes pas le seul. Dans de nombreux flux de travail de bureau, un PDF consultable fait la différence entre un fichier sans issue et une archive consultable.  

Dans ce tutoriel, nous parcourrons un **exemple c# ocr** complet qui transforme un TIFF multipage en PDF consultable, le tout avec Aspose.OCR. À la fin, vous saurez exactement comment **convertir une image en PDF consultable**, comment **convertir un tiff en pdf**, et vous disposerez d’un extrait de code prêt à l’emploi que vous pourrez insérer dans n’importe quel projet .NET.

## Ce que vous apprendrez

* Comment installer et référencer Aspose.OCR dans un projet C#.
* Les étapes exactes pour charger un TIFF, définir la langue et appeler `RecognizeToPdf`.
* Pourquoi chaque étape est importante – de la gestion de la mémoire à la sélection de la langue.
* Conseils pour gérer les gros documents, dépanner les problèmes courants d’OCR, et étendre la solution à d’autres formats d’image.

**Prérequis** – un SDK .NET récent (4.6+ ou .NET Core 3.1+), Visual Studio (ou votre IDE préféré), et une licence Aspose.OCR (l’essai gratuit suffit pour les tests). Aucune autre bibliothèque externe n’est requise.

---

## Créer un PDF consultable – Vue d’ensemble

À un niveau élevé, le processus ressemble à ceci :

1. **Initialiser** le `OcrEngine`.  
2. **Charger** l’image source (un TIFF dans notre cas).  
3. **Configurer** les paramètres de langue pour une meilleure précision.  
4. **Exécuter** l’OCR et **enregistrer** le résultat directement en PDF consultable.  

C’est tout. L’API Aspose fait le travail lourd, vous n’avez donc pas besoin d’assembler séparément des bibliothèques OCR et PDF.

---

## Étape 1 : Installer Aspose.OCR et configurer votre projet

Tout d’abord, ajoutez le package NuGet Aspose.OCR :

```bash
dotnet add package Aspose.OCR
```

Ou, si vous préférez la console du Gestionnaire de packages dans Visual Studio :

```powershell
Install-Package Aspose.OCR
```

Après la restauration du package, ouvrez votre fichier de projet et vérifiez la référence :

```xml
<ItemGroup>
  <PackageReference Include="Aspose.OCR" Version="23.10.0" />
</ItemGroup>
```

> **Astuce :** Utilisez la dernière version stable (vérifiez le site Aspose) pour obtenir les corrections de bugs et les derniers packs de langues.

---

## Étape 2 : Convertir TIFF en PDF – Chargement de l’image

Nous allons maintenant charger le TIFF que vous souhaitez rendre consultable. La méthode `Image.Load` d’Aspose prend en charge les TIFF multipages dès le départ.

```csharp
using Aspose.OCR;
using System.Drawing;

// Load the multi‑page TIFF. Replace the path with your actual file.
using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");
```

> **Pourquoi c’est important :** Charger l’image à l’intérieur d’un bloc `using` garantit que les ressources non gérées sont libérées rapidement—crucial lors du traitement de gros documents.

---

## Étape 3 : Image vers PDF consultable – Configuration du moteur OCR

Avant d’exécuter l’OCR, nous indiquerons au moteur quelle langue attendre. L’anglais fonctionne dans la plupart des cas, mais vous pouvez remplacer par n’importe quelle valeur de l’énumération `OcrLanguage`.

```csharp
// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// (Optional) Specify language for better accuracy
ocrEngine.Language = OcrLanguage.English;
```

> **Note d’expert :** Sélectionner la bonne langue réduit considérablement les erreurs de reconnaissance. Si vous avez des langues mixtes, vous pouvez les combiner avec l’opérateur `|`, par ex., `OcrLanguage.English | OcrLanguage.French`.

---

## Étape 4 : Exemple OCR C# – Reconnaître et enregistrer

Avec le moteur prêt, appelez `RecognizeToPdf`. La méthode écrit le PDF consultable directement sur le disque, en intégrant une couche de texte invisible derrière l’image originale.

```csharp
// Define the output path for the searchable PDF
string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";

// Perform OCR and write the searchable PDF
ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);
```

Après l’exécution de cette ligne, `output.pdf` contiendra les pages TIFF originales ainsi qu’une superposition de texte cachée que n’importe quel lecteur PDF pourra rechercher.

---

## Étape 5 : Image C# vers PDF – Vérifier le résultat

Confirmons que tout a fonctionné. Ouvrez le PDF généré dans Adobe Reader (ou tout autre lecteur) et essayez de rechercher un mot que vous savez présent dans le TIFF source.

```csharp
Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
```

Si la recherche renvoie des résultats, vous avez réussi à **créer un PDF consultable** à partir d’une image. Sinon, revérifiez le paramètre de langue ou la qualité du TIFF source.

---

## Exemple complet fonctionnel

En assemblant toutes les pièces, voici une application console autonome que vous pouvez compiler et exécuter :

```csharp
using Aspose.OCR;
using System.Drawing;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Load the multi‑page TIFF
        using var tiffImage = Image.Load(@"YOUR_DIRECTORY/input.tif");

        // Step 3: (Optional) Set language for better accuracy
        ocrEngine.Language = OcrLanguage.English;

        // Step 4: Convert the image to a searchable PDF
        string outputPdfPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.RecognizeToPdf(tiffImage, outputPdfPath);

        // Step 5: Inform the user
        System.Console.WriteLine("Searchable PDF created at: " + outputPdfPath);
    }
}
```

**Sortie attendue** (dans la console) :

```
Searchable PDF created at: C:\MyFolder\output.pdf
```

Ouvrez `output.pdf` et vous devriez pouvoir taper n’importe quel mot du TIFF original dans la zone de recherche du lecteur et voir les correspondances mises en évidence.

---

![Create searchable PDF example](placeholder-image.png){: .align-center alt="exemple de création de PDF consultable"}

*La capture d’écran ci‑dessus montre un PDF consultable ouvert dans un lecteur avec la couche de texte cachée activée.*

---

## Questions fréquentes & cas particuliers

### Et si mon TIFF est énorme (des centaines de pages) ?

Aspose.OCR diffuse les pages une à une, mais vous pourriez tout de même atteindre les limites de mémoire. Envisagez de traiter le TIFF par lots :

```csharp
for (int i = 0; i < tiffImage.PageCount; i++)
{
    using var singlePage = tiffImage.ExtractPage(i);
    ocrEngine.RecognizeToPdf(singlePage, $"page_{i}.pdf");
}
```

Ensuite, fusionnez les PDF par page avec une bibliothèque PDF (par ex., Aspose.PDF).

### Puis-je exporter vers un format différent, comme un DOCX consultable ?

Oui—utilisez `RecognizeToDocument` au lieu de `RecognizeToPdf`. L’API reflète la méthode PDF, il suffit de changer l’extension du fichier cible.

### Comment gérer les langues autres que l’anglais ?

Remplacez `OcrLanguage.English` par l’énumération appropriée, par exemple `OcrLanguage.Spanish`. Vous pouvez également combiner les langues :

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.German;
```

### Qu’en est‑il des PDF protégés par mot de passe ?

Après l’étape OCR, vous pouvez ouvrir le PDF généré avec Aspose.PDF et appliquer le chiffrement :

```csharp
var pdfDoc = new Aspose.Pdf.Document(outputPdfPath);
pdfDoc.Encrypt("ownerPassword", "userPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save(outputPdfPath);
```

---

## Récapitulatif

Nous avons couvert tout ce dont vous avez besoin pour **créer des fichiers PDF consultables** à partir d’images TIFF en utilisant C#. En partant de l’installation d’Aspose.OCR, du chargement de l’image, de la configuration de la langue, de l’exécution de l’OCR, et enfin de la vérification du résultat consultable, vous disposez maintenant d’un solide **exemple c# ocr** que vous pouvez adapter à d’autres formats.  

Si vous êtes prêt à aller plus loin, essayez :

* **Convertir TIFF en PDF** pour des archives non consultables (il suffit d’ignorer l’étape OCR).  
* Expérimenter avec **image vers PDF consultable**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}