---
category: general
date: 2026-03-18
description: Comment faire de l'OCR d'un PDF en C# – apprenez à convertir un PDF numérisé,
  créer un PDF interrogeable, ajouter un filigrane à un PDF et extraire le texte d'un
  PDF avec un workflow simple OcrEngine.
draft: false
keywords:
- how to ocr pdf
- convert scanned pdf
- create searchable pdf
- add watermark pdf
- extract text from pdf
language: fr
og_description: Comment faire de l'OCR sur un PDF en C# ? Ce guide vous montre comment
  convertir un PDF numérisé, créer un PDF interrogeable, ajouter un filigrane à un
  PDF et extraire le texte d’un PDF à l’aide d’OcrEngine.
og_title: Comment faire de l'OCR d'un PDF en C# – Guide rapide et complet
tags:
- OCR
- PDF
- C#
- Document Processing
title: Comment faire de l’OCR d’un PDF en C# – Convertir les PDF numérisés
url: /fr/python-java/general/how-to-ocr-pdf-in-c-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR sur un PDF en C# – Convertir les PDF numérisés

Vous avez déjà eu besoin de **how to OCR PDF** mais vous êtes bloqué par un fichier numérisé qui refuse de coopérer ? Vous n'êtes pas le seul. Dans de nombreux projets réels—pensez à la numérisation de factures ou à l'archivage de rapports historiques—vous vous retrouvez avec une pile d'images intégrées dans un PDF, et la seule façon de les rendre recherchables est d'exécuter l'OCR dessus.  

Bonne nouvelle ? Avec seulement quelques lignes de C# vous pouvez **convert scanned PDF** en un **create searchable PDF**, ajouter un léger filigrane, et même extraire le texte brut pour un traitement ultérieur. Vous verrez ci‑dessous un exemple complet, prêt à l'exécution, qui fait exactement cela.

## Ce que couvre ce tutoriel

* Comment **how to OCR PDF** en utilisant la classe `OcrEngine`.  
* Transformer un PDF numérisé en un **create searchable PDF**.  
* Ajouter un filigrane sur la première page (**add watermark pdf**).  
* Extraire les chaînes de texte brut du résultat (**extract text from pdf**).  
* Pièges courants—comme la gestion de documents multi‑pages ou de scans à basse résolution.  

Pas de liens vers une documentation externe, pas de fragments de code à moitié terminés. Tout ce dont vous avez besoin est ici.

## Prérequis

* .NET 6.0 ou ultérieur (le code se compile également avec .NET 5).  
* Une référence à la bibliothèque OCR qui fournit `OcrEngine` et `ImageFormats` (par ex., `Aspose.OCR` ou un package similaire).  
* Un PDF d'entrée nommé `input.pdf` placé dans un dossier que vous contrôlez.  
* Une connaissance de base des applications console C#.  

Si vous avez déjà tout cela, super—passons à l'action.

## Étape 1 : Configurer le projet et importer les dépendances

Créez un nouveau projet console et ajoutez le package OCR via NuGet :

```bash
dotnet new console -n OcrPdfDemo
cd OcrPdfDemo
dotnet add package Aspose.OCR
```

Ouvrez maintenant `Program.cs`. En haut, importez les espaces de noms dont vous aurez besoin :

```csharp
using System;
using Aspose.OCR;          // OcrEngine lives here
using Aspose.OCR.Image;   // ImageFormats enum
```

*Pourquoi c'est important* : Importer les bons espaces de noms permet au compilateur de localiser `OcrEngine`. Ignorer cette étape déclenchera une erreur `CS0246` et arrêtera votre compilation.

## Étape 2 : Initialiser le moteur OCR

Le moteur est le cœur du processus. Vous l’instanciez une fois et le réutilisez pour chaque page.

```csharp
// Step 2: Initialize the OCR engine
OcrEngine engine = new OcrEngine();
```

*Astuce* : Si vous prévoyez de traiter de nombreux PDF consécutivement, envisagez de réutiliser la même instance `engine` afin d'éviter des vérifications de licence répétées.

## Étape 3 : Charger le PDF source

Indiquez au moteur quel fichier traiter. La méthode `SetImageFromFile` accepte toute source image‑ou‑PDF.

```csharp
// Step 3: Load the scanned PDF you want to OCR
engine.SetImageFromFile(@"YOUR_DIRECTORY\input.pdf");
```

> **Pourquoi cette étape est cruciale** – Le moteur a besoin d’une représentation bitmap de chaque page. Lorsque vous lui fournissez un PDF, il rasterise chaque page en interne selon le DPI par défaut (généralement 300). Si le PDF source est déjà basé sur du texte, le moteur le transmet simplement tel quel, vous faisant gagner du temps.

## Étape 4 : Exécuter la reconnaissance OCR

C’est maintenant le travail lourd qui s’effectue. La méthode `Recognize` analyse chaque page, extrait les glyphes et crée une couche recherchable.

```csharp
// Step 4: Perform OCR on the loaded document
engine.Recognize();
```

*Question fréquente* : *Et si le PDF comporte 50 pages ?*  
`Recognize` traite l’ensemble du document par défaut. Dans des environnements à mémoire limitée, vous pouvez définir `engine.PageIndex` et `engine.PageCount` pour travailler page par page.

## Étape 5 : Enregistrer le PDF recherchable (Filigrane sur la page 1)

Nous enregistrerons le résultat en tant que PDF. La première page recevra automatiquement un filigrane car la bibliothèque OCR ajoute par défaut une superposition « Generated by Aspose.OCR ». Si vous avez besoin d’un filigrane personnalisé, vous pouvez modifier la propriété `engine.Watermark` avant d’enregistrer.

```csharp
// Step 5: Save the OCR‑processed PDF with a watermark on page 1
engine.Save(@"YOUR_DIRECTORY\output.pdf", ImageFormats.Pdf);
```

Après cet appel, vous disposerez d’un **create searchable PDF** où vous pourrez sélectionner, copier et rechercher le texte comme dans n’importe quel PDF natif.

## Étape 6 : Extraire le texte brut (Optionnel mais pratique)

Si vous souhaitez également **extract text from pdf** pour l’indexation ou une analyse supplémentaire, le moteur vous donne accès à la chaîne brute.

```csharp
// Step 6: Pull the recognized text into a string
string extractedText = engine.Text;
Console.WriteLine("=== Extracted Text Start ===");
Console.WriteLine(extractedText);
Console.WriteLine("=== Extracted Text End ===");
```

La propriété `engine.Text` concatène le texte de toutes les pages, en conservant les sauts de ligne. Vous pouvez la scinder avec `\f` (form feed) si vous avez besoin d’une granularité par page.

## Exemple complet fonctionnel

Voici le programme complet. Copiez‑collez‑le dans `Program.cs`, remplacez `YOUR_DIRECTORY` par un chemin absolu ou relatif, puis exécutez `dotnet run`.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine
            OcrEngine engine = new OcrEngine();

            // 2️⃣ Load the source PDF to be processed
            // Make sure the file exists; otherwise you'll get a FileNotFoundException.
            string inputPath = @"YOUR_DIRECTORY\input.pdf";
            engine.SetImageFromFile(inputPath);

            // 3️⃣ Perform OCR recognition on the loaded document
            engine.Recognize();

            // 4️⃣ Save the recognized document as a PDF (watermark appears on page 1)
            string outputPath = @"YOUR_DIRECTORY\output.pdf";
            engine.Save(outputPath, ImageFormats.Pdf);

            // 5️⃣ (Optional) Extract plain text for further use
            string extractedText = engine.Text;
            Console.WriteLine("=== Extracted Text Start ===");
            Console.WriteLine(extractedText);
            Console.WriteLine("=== Extracted Text End ===");

            Console.WriteLine($"OCR complete! Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Sortie attendue

L’exécution du programme affiche le texte extrait dans la console et crée `output.pdf`. Ouvrez le PDF avec n’importe quel lecteur (Adobe Acrobat, Edge, etc.) et essayez de rechercher un mot présent dans le scan original —vous verrez qu’il est maintenant recherchable. La première page montre le filigrane par défaut, confirmant que l’étape **add watermark pdf** a réussi.

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|--------|
| **Et si le scan est de basse résolution ?** | Augmentez le DPI avant la reconnaissance : `engine.ImageInfo.DpiX = engine.ImageInfo.DpiY = 600;` Cela fournit au moteur OCR plus de détails à traiter. |
| **Puis-je choisir un filigrane personnalisé ?** | Oui. Définissez `engine.Watermark = "Confidential – Processed on " + DateTime.Now.ToShortDateString();` avant `Save`. |
| **Comment gérer les PDF protégés par mot de passe ?** | Utilisez `engine.LoadPassword = "yourPassword";` avant `SetImageFromFile`. |
| **Existe‑t‑il un moyen de limiter l'OCR à des pages spécifiques ?** | Définissez `engine.PageIndex = 2;` et `engine.PageCount = 5;` pour ne traiter que les pages 3 à 7. |
| **Et si je dois garder les images originales intactes ?** | Après l'OCR, vous pouvez fusionner le PDF original avec la couche OCR à l'aide d'une bibliothèque PDF (par ex., `Aspose.PDF`) afin de préserver la fidélité des images. |

## Astuces & bonnes pratiques

* **Astuce** : Exécutez l'OCR sur un thread d'arrière‑plan si vous intégrez cela dans une application UI—sinon l'interface se bloquera.  
* **Attention à** : les PDF contenant du contenu raster et vectoriel mixte. Le moteur ne fera l'OCR que sur les pages raster ; le texte vectoriel reste sélectionnable automatiquement.  
* **Optimisation de performance** : Mettez en cache les données de langue OCR (`engine.Language = OcrLanguage.English;`) pour éviter de les recharger à chaque document.  

## Conclusion

Vous disposez maintenant d’une solution complète, de bout en bout, pour **how to OCR PDF** en C#. En initialisant le `OcrEngine`, en chargeant un fichier numérisé, en reconnaissant le texte, en enregistrant un **create searchable pdf**, en ajoutant un filigrane, et éventuellement en **extracting text from pdf**, vous pouvez transformer n’importe quel PDF basé sur des images en un actif recherchable et indexable.

Prochaines étapes ? Essayez d’enchaîner ce flux de travail avec un système de gestion documentaire, ou expérimentez avec différentes langues (`engine.Language = OcrLanguage.French;`). Vous pouvez également explorer le traitement par lots de plusieurs fichiers dans un dossier—il suffit de boucler sur les étapes avec une nouvelle instance `engine` à chaque fois.

Bon codage, et que vos PDF soient toujours recherchables ! 

![How to OCR PDF example showing input and output files](https://example.com/ocr-pdf-demo.png "how to ocr pdf")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}