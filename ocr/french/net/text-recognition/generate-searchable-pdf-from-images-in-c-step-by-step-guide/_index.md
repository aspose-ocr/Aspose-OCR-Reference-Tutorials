---
category: general
date: 2026-02-22
description: Générez un PDF consultable et extrayez le texte d’une image à l’aide
  d’Aspose OCR. Apprenez comment convertir une image en PDF et obtenir du texte brut
  dans un seul tutoriel.
draft: false
keywords:
- generate searchable pdf
- extract text from image
- convert image to pdf
- output plain text
- convert scanned image pdf
language: fr
og_description: Générez un PDF consultable à partir d'images numérisées avec Aspose
  OCR. Ce guide montre comment extraire le texte d’une image, produire du texte brut
  et convertir l’image en PDF.
og_title: Générer un PDF interrogeable à partir d'images – Tutoriel complet C#
tags:
- C#
- OCR
- PDF generation
- Aspose
title: Générer un PDF interrogeable à partir d'images en C# – Guide étape par étape
url: /fr/net/text-recognition/generate-searchable-pdf-from-images-in-c-step-by-step-guide/
---

.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Générer un PDF consultable à partir d'images en C# – Tutoriel complet

Vous avez déjà eu besoin de **générer un PDF consultable** à partir d'une image numérisée mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul—la plupart des développeurs rencontrent ce problème lorsqu'ils découvrent l'OCR. La bonne nouvelle ? Avec Aspose OCR vous pouvez **extraire du texte d'une image**, **produire du texte brut**, et **convertir une image en PDF** en quelques lignes de C#.

Dans ce guide, nous parcourrons l’ensemble du processus, du chargement d’un fichier PNG à l’enregistrement d’un PDF consultable et d’un fichier texte brut. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel projet .NET. Pas de superflu, juste ce qui fait le travail.

## Ce que vous apprendrez

- Comment configurer **Aspose.OCR** dans une application console .NET.  
- La différence entre les modes **output plain text** et **searchable PDF**.  
- Comment **extract text from image** et l’écrire dans un fichier `.txt`.  
- Comment **convert image to PDF** tout en conservant le bitmap original et en ajoutant une couche de texte cachée.  
- Conseils pour gérer de gros lots, les pièges courants, et où ajuster les paramètres pour une meilleure précision.

> **Prérequis** – Vous avez besoin de .NET 6+ (ou .NET Framework 4.7+), Visual Studio 2022 (ou tout autre éditeur), et d’une licence Aspose OCR (ou d’un essai gratuit). Aucune autre bibliothèque tierce n’est requise.

![exemple de PDF consultable généré](image-placeholder.png "Exemple d'un PDF consultable généré")

## Étape 1 : Installer Aspose OCR et créer le moteur

Tout d’abord, ajoutez le package NuGet à votre projet :

```bash
dotnet add package Aspose.OCR
```

Nous pouvons maintenant initialiser le moteur OCR et indiquer la langue à traiter. L'anglais est la langue par défaut, mais vous pouvez passer au français, à l'espagnol, etc., en modifiant l'énumération `Language`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.IO;

class Program
{
    static void Main()
    {
        // Initialize the OCR engine for English
        OcrEngine ocrEngine = new OcrEngine { Language = Language.English };
```

**Pourquoi c’est important :** Le moteur contient toute la configuration — langue, format de sortie et indicateurs de prétraitement optionnels. Le configurer une fois et le réutiliser évite le surcoût de création d’une nouvelle instance pour chaque fichier.

## Étape 2 : Extraire le texte et l’enregistrer en texte brut

Si vous avez seulement besoin des caractères bruts, passez le moteur à `OutputFormat.Text`. Cela indique à Aspose OCR d’ignorer complètement la génération du PDF et de vous renvoyer une chaîne.

```csharp
        // Tell the engine to return plain text
        ocrEngine.OutputFormat = OutputFormat.Text;

        // Path to your source image (PNG, JPEG, BMP, etc.)
        string inputImagePath = @"YOUR_DIRECTORY/input.png";

        // Perform recognition – the result contains the extracted string
        OcrResult plainTextResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Write the text to a .txt file
        string textOutputPath = @"YOUR_DIRECTORY/output.txt";
        File.WriteAllText(textOutputPath, plainTextResult.Text);
```

**Astuce :** `plainTextResult.Text` supprime déjà les sauts de ligne qui appartiennent à la mise en page OCR. Si vous avez besoin de l’espacement original, inspectez `plainTextResult.TextBlocks` à la place.

### Résultat attendu

Ouvrez `output.txt` et vous devriez voir quelque chose comme :

```
Hello, world!
This is a sample scanned document.
```

C’est la partie **output plain text** du tutoriel — rapide, légère, et parfaite pour le traitement en aval (par ex., l’indexation).

## Étape 3 : Passer en mode PDF consultable

Créons maintenant un **PDF consultable**. Le moteur intégrera le bitmap original et superposera le texte généré par l’OCR en dessous, rendant le document consultable dans n’importe quel lecteur PDF.

```csharp
        // Change the output format to searchable PDF
        ocrEngine.OutputFormat = OutputFormat.SearchablePdf;

        // Recognize the same image again – this time we get PDF bytes
        OcrResult pdfResult = ocrEngine.Recognize(Image.Load(inputImagePath));

        // Save the PDF bytes to a file
        string pdfOutputPath = @"YOUR_DIRECTORY/output.pdf";
        File.WriteAllBytes(pdfOutputPath, pdfResult.RawData);
    }
}
```

**Pourquoi nous re‑reconnaissons :** Le moteur OCR met en cache la dernière image, mais le format de sortie détermine les données retournées. Changer de format force une nouvelle passe qui inclut la couche de texte cachée.

### À quoi ressemble le PDF

Ouvrez `output.pdf` dans Adobe Reader ou tout autre lecteur et essayez de sélectionner du texte. Vous verrez que vous pouvez copier, rechercher et mettre en surbrillance le contenu—même si l’apparence visuelle reste le bitmap original. C’est la caractéristique d’un **convert scanned image pdf**.

## Étape 4 : Gestion de plusieurs fichiers (optionnel)

Les projets du monde réel traitent rarement une seule image. Ci‑dessus, une boucle rapide qui traite chaque PNG d’un dossier, en produisant les fichiers correspondants `.txt` et `.pdf`.

```csharp
        string folder = @"YOUR_DIRECTORY";
        foreach (var file in Directory.GetFiles(folder, "*.png"))
        {
            // Plain‑text extraction
            ocrEngine.OutputFormat = OutputFormat.Text;
            var txtResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllText(Path.ChangeExtension(file, ".txt"), txtResult.Text);

            // Searchable PDF generation
            ocrEngine.OutputFormat = OutputFormat.SearchablePdf;
            var pdfResult = ocrEngine.Recognize(Image.Load(file));
            File.WriteAllBytes(Path.ChangeExtension(file, ".pdf"), pdfResult.RawData);
        }
```

**Note de cas limite :** Les grandes images peuvent épuiser la mémoire. Si vous rencontrez `OutOfMemoryException`, envisagez de réduire la taille avec `Image.Resize` avant la reconnaissance, ou traitez les fichiers par lots plus petits.

## Étape 5 : Affiner la précision de l’OCR

Aspose OCR propose quelques réglages que vous pouvez ajuster :

| Setting | Ce qu’il fait | Quand l’utiliser |
|---------|----------------|-------------------|
| `ocrEngine.PageSegmentationMode` | Contrôle la façon dont le moteur divise l’image en blocs de texte. | Utile pour les mises en page à colonnes multiples. |
| `ocrEngine.Deskew` | Corrige automatiquement les pages légèrement inclinées. | Documents numérisés qui ne sont pas parfaitement alignés. |
| `ocrEngine.RemoveNoise` | Tente de nettoyer les taches et les artefacts de fond. | Scans de mauvaise qualité ou pages faxées. |

```csharp
ocrEngine.Deskew = true;
ocrEngine.RemoveNoise = true;
```

Activer ces options peut augmenter le temps de traitement, mais le gain en qualité de **extract text from image** en vaut souvent la peine.

## Étape 6 : Vérifier la sortie programmatiquement

Parfois, vous devez vérifier que le PDF contient réellement du texte consultable (par ex., dans des tests automatisés). La vérification la plus simple consiste à s’assurer que le tableau d’octets du PDF n’est pas vide et que la longueur de `RawData` dépasse la taille de l’image.

```csharp
if (pdfResult.RawData.Length > Image.Load(inputImagePath).Data.Length)
{
    Console.WriteLine("Searchable PDF generated successfully!");
}
else
{
    Console.WriteLine("Warning: PDF may not contain hidden text.");
}
```

Pour une validation plus approfondie, vous pourriez utiliser une bibliothèque PDF (comme iTextSharp) pour extraire le flux de texte et le comparer à `plainTextResult.Text`.

## Pièges courants et comment les éviter

- **Licence manquante** – Sans une licence Aspose valide, la bibliothèque fonctionne en mode d’évaluation, ajoutant un filigrane aux PDF. Enregistrez votre licence tôt (`License license = new License(); license.SetLicense("Aspose.OCR.lic");`).  
- **Chemin incorrect** – Codifier en dur des chemins absolus fonctionne sur votre machine mais échoue ailleurs. Utilisez `Path.Combine` avec `AppDomain.CurrentDomain.BaseDirectory` pour la portabilité.  
- **Formats d’image non pris en charge** – Les GIF et TIFF avec plusieurs images nécessitent une gestion spéciale (`Image.LoadMultiPage`). Convertissez-les en PNG/JPEG d’abord si vous ne avez besoin que de la première page.  
- **Goulots d’étranglement de performance** – Re‑créer `OcrEngine` dans une boucle est coûteux. Conservez une seule instance et ne changez que `OutputFormat` comme indiqué.

## Récapitulatif

Nous avons couvert l’ensemble du flux de travail pour **generate searchable PDF** à partir d’une image numérisée en utilisant Aspose OCR :

1. Installez le package NuGet et créez un `OcrEngine`.  
2. Définissez `OutputFormat.Text` pour **output plain text** et écrivez-le dans un fichier `.txt`.  
3. Passez à `OutputFormat.SearchablePdf` pour **convert image to PDF** avec une couche de texte invisible.  
4. Enregistrez les octets du PDF et, éventuellement, parcourez un répertoire pour un traitement par lots.  
5. Affinez la précision avec les options de deskew, de suppression du bruit et de segmentation de page.  

Tout cela tient dans un programme compact et autonome que vous pouvez copier‑coller dans Visual Studio.

## Que tester ensuite ?

- **Traitement par lots** avec une interface UI (WinForms ou WPF) afin que les utilisateurs puissent glisser‑déposer des fichiers.  
- **Détection de langue** – Aspose OCR peut détecter automatiquement la langue ; essayez `ocrEngine.Language = Language.AutoDetect`.  
- **Post‑traitement** – Alimenter le texte extrait dans un index de recherche (ElasticSearch, Azure Cognitive Search) pour une récupération instantanée des documents.  
- **Sorties alternatives** – Utilisez `OutputFormat.Hocr` pour des résultats OCR basés sur HTML, utiles pour les aperçus web.  

N’hésitez pas à expérimenter différentes résolutions d’image, modes couleur et paramètres OCR. Plus vous jouez, mieux vous comprendrez les compromis entre vitesse et précision.

---

**Bon codage !** Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous ou consultez la documentation Aspose OCR pour des approfondissements. Votre prochain projet—qu’il s’agisse de facturation, d’archivage ou de création d’une base de connaissances consultable—est maintenant beaucoup plus simple.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}