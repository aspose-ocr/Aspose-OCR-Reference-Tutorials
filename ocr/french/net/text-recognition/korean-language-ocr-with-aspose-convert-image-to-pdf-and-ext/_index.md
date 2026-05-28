---
category: general
date: 2026-05-28
description: Tutoriel OCR de la langue coréenne avec Aspose en C#. Apprenez comment
  charger une image depuis un flux, extraire le texte brut, convertir l'image en PDF
  et exporter un PDF consultable.
draft: false
keywords:
- korean language ocr
- convert image to pdf
- load image from stream
- extract plain text
- export searchable pdf
language: fr
og_description: OCR de la langue coréenne en C# avec Aspose. Guide pas à pas pour
  charger une image depuis un flux, extraire le texte brut, convertir l'image en PDF
  et exporter un PDF consultable.
og_title: OCR de la langue coréenne – Convertir une image en PDF et extraire le texte
  (Guide C#)
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Korean Language OCR tutorial using Aspose in C#. Learn how to load
    image from stream, extract plain text, convert image to PDF and export searchable
    PDF.
  headline: 'Korean Language OCR with Aspose: Convert Image to PDF and Extract Text
    in C#'
  type: TechArticle
tags:
- Aspose OCR
- C#
- Image Processing
title: 'OCR coréen avec Aspose : convertir une image en PDF et extraire le texte en
  C#'
url: /fr/net/text-recognition/korean-language-ocr-with-aspose-convert-image-to-pdf-and-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR de langue coréenne avec Aspose : Convertir une image en PDF et extraire le texte en C#

Vous vous êtes déjà demandé comment exécuter **Korean Language OCR** sur une image sans envoyer quoi que ce soit dans le cloud ? Vous n'êtes pas le seul. Que vous numérisiez des panneaux de rue, traitiez des reçus ou construisiez un index de recherche multilingue, pouvoir reconnaître les caractères coréens localement peut vous faire gagner du temps, de l'argent et éviter des problèmes de confidentialité.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre comment **load image from stream**, **extract plain text**, **convert image to PDF**, et enfin **export searchable PDF** — le tout avec Aspose.OCR et quelques lignes de C#. Aucun service externe, aucune magie cachée — juste du code .NET pur que vous pouvez intégrer dans n'importe quelle application console.

## Ce que vous en retirerez

- Un programme console fonctionnel qui lit un fichier JPEG via un flux de fichier.  
- Texte coréen extrait sous forme de chaînes Unicode simples.  
- Un rapport JSON détaillé de l'exécution OCR pour le débogage ou l'analyse.  
- Un PDF consultable que vous pouvez ouvrir dans n'importe quel lecteur PDF et sélectionner réellement les mots coréens.  

**Prerequisites**  
- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.7+).  
- Package NuGet Aspose.OCR pour .NET installé (`Install-Package Aspose.OCR`).  
- Un dossier contenant `korean_sign.jpg` et un emplacement accessible en écriture pour les fichiers de sortie.  

Si vous avez déjà ces éléments en place, super — mettons-nous au travail.

## Étape 1 : Initialiser le moteur OCR pour la reconnaissance de langue coréenne

La première chose dont vous avez besoin est une instance `OcrEngine`. Activer le GPU (si vous en avez un) accélère considérablement la reconnaissance, et désactiver le téléchargement automatique des ressources oblige la bibliothèque à utiliser les packs de langues hors ligne que vous fournissez.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

// Create the OCR engine
var ocrEngine = new OcrEngine();

// Enable GPU acceleration – optional but fast
ocrEngine.Configuration.EnableGpu = true;

// We’ll supply the Korean language pack ourselves
ocrEngine.Configuration.AutomaticResourceDownload = false;
ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";
```

> **Pourquoi cela importe :**  
> *GPU acceleration* peut réduire le temps de traitement de secondes à millisecondes pour de gros lots.  
> Définir `AutomaticResourceDownload` à `false` garantit que la démo fonctionne hors ligne — une exigence cruciale pour de nombreux environnements d'entreprise.

## Étape 2 : Charger l'image depuis un flux

Lire l'image via un flux vous offre de la flexibilité : vous pouvez récupérer des fichiers depuis le disque, des partages réseau ou même des blobs mis en cache en mémoire. Ici, nous ouvrons un fichier JPEG local, mais le même modèle fonctionne avec n'importe quel `Stream`.

```csharp
using System.IO;

// Open the image file as a read‑only stream
using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");

// Feed the stream to the OCR engine
ocrEngine.Image = ImageStream.FromStream(imageStream);
```

> **Pro tip:** Si vous devez un jour traiter des images téléchargées via une API web, remplacez simplement `File.OpenRead` par le `IFormFile.OpenReadStream()` entrant — le reste reste identique.

## Étape 3 : Choisir la langue coréenne et appliquer les filtres de pré‑traitement

Aspose.OCR prend en charge quelques étapes de prétraitement qui nettoient l'image avant la reconnaissance. Pour les panneaux coréens, le redressement et la réduction du bruit sont généralement suffisants.

```csharp
using Aspose.OCR.Enums;

// Tell the engine we’re dealing with Korean text
ocrEngine.Configuration.Language = Language.Korean;

// Apply deskew and denoise filters
ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                            PreprocessFilter.Denoise;
```

> **Que se passe-t-il en coulisses ?**  
> Le filtre `Deskew` redresse le texte incliné, tandis que `Denoise` élimine le grain qui peut perturber le classificateur de caractères. Ignorer ces étapes conduit souvent à une sortie brouillée, surtout sur des photos à basse résolution.

## Étape 4 : Extraire le texte brut de façon asynchrone

Voici le moment de vérité — demander au moteur de reconnaître les caractères et de nous fournir une chaîne propre. Utiliser `RecognizeAsync` maintient l'interface réactive si vous intégrez cela dans une application de bureau ou web.

```csharp
// Run OCR and get the plain text result
string plainText = await ocrEngine.RecognizeAsync();
```

Lorsque vous exécutez le programme, vous devriez voir quelque chose comme :

```
OCR complete. Extracted text:
서울시청
```

> **Pourquoi asynchrone ?**  
> L'OCR peut être intensif en CPU. L'exécution asynchrone empêche votre thread de se bloquer, ce qui est particulièrement utile dans ASP.NET Core où la famine de threads est un vrai problème.

## Étape 5 : Obtenir un résultat de reconnaissance détaillé et l'enregistrer au format JSON

Parfois vous avez besoin de plus que la simple chaîne brute — peut-être des scores de confiance, des boîtes englobantes ou les données d'image originales. La méthode `RecognizeDetailed` renvoie un objet `RecognitionResult` qui peut être sérialisé en JSON pour une analyse ultérieure.

```csharp
// Detailed result includes confidence, coordinates, etc.
RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();

// Convert to nicely indented JSON
string jsonResult = detailedResult.ToJson(indent: true);

// Persist the JSON to disk
File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);
```

L'ouverture de `korean_ocr.json` révélera une structure similaire à :

```json
{
  "Pages": [
    {
      "Text": "서울시청",
      "Confidence": 0.98,
      "Words": [
        {
          "Text": "서울시청",
          "BoundingBox": [12,34,56,78],
          "Confidence": 0.98
        }
      ]
    }
  ]
}
```

> **Quand l'utiliser ?**  
> Si vous construisez un index de recherche, les valeurs de confiance vous permettent de filtrer les résultats de mauvaise qualité. Si vous devez mettre en surbrillance du texte dans une interface, les boîtes englobantes sont votre carte.

## Étape 6 : Convertir l'image en PDF et exporter un PDF consultable

Aspose rend la transition du raster au vecteur sans effort. En définissant `OutputFormat` sur `SearchablePdf`, la bibliothèque intègre l'image originale et superpose une couche de texte invisible contenant le résultat de l'OCR. Le PDF résultant peut être recherché, copié et indexé comme n'importe quel PDF natif.

```csharp
using Aspose.OCR.Enums;

// Tell the engine to produce a searchable PDF
ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;

// Save the PDF to the target folder
ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");
```

Ouvrez `korean_searchable.pdf` dans Adobe Reader ou tout autre lecteur PDF, appuyez sur **Ctrl+F**, tapez un mot coréen, et voyez-le se positionner exactement à l'endroit correspondant sur la page. C’est la puissance d’un PDF consultable.

> **Astuce supplémentaire :**  
> Si vous avez seulement besoin d'un PDF visuel sans la couche de texte cachée, changez `OutputFormat` en `Pdf`.

## Exemple complet fonctionnel

Voici le programme complet — copiez‑collez, remplacez `YOUR_DIRECTORY` par un chemin réel, et appuyez sur **F5**.

```csharp
using System;
using System.IO;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Enums;

class OcrDemo
{
    static async Task Main()
    {
        // Step 1: Create the OCR engine and enable GPU with offline resources
        var ocrEngine = new OcrEngine();
        ocrEngine.Configuration.EnableGpu = true;
        ocrEngine.Configuration.AutomaticResourceDownload = false;
        ocrEngine.Configuration.ResourcesFolder = @"YOUR_DIRECTORY/Resources";

        // Step 2: Select the language and apply preprocessing filters
        ocrEngine.Configuration.Language = Language.Korean;
        ocrEngine.Configuration.PreprocessFilters = PreprocessFilter.Deskew |
                                                    PreprocessFilter.Denoise;

        // Step 3: Load the image to be recognized from a file stream
        using var imageStream = File.OpenRead(@"YOUR_DIRECTORY/korean_sign.jpg");
        ocrEngine.Image = ImageStream.FromStream(imageStream);

        // Step 4: Run OCR asynchronously and obtain the plain text result
        string plainText = await ocrEngine.RecognizeAsync();

        // Step 5: Get a detailed recognition result, convert it to JSON, and save it
        RecognitionResult detailedResult = ocrEngine.RecognizeDetailed();
        string jsonResult = detailedResult.ToJson(indent: true);
        File.WriteAllText(@"YOUR_DIRECTORY/korean_ocr.json", jsonResult);

        // Step 6: Export the recognized page as a searchable PDF
        ocrEngine.Configuration.OutputFormat = OutputFormat.SearchablePdf;
        ocrEngine.Save(@"YOUR_DIRECTORY/korean_searchable.pdf");

        Console.WriteLine("OCR complete. Extracted text:");
        Console.WriteLine(plainText);
    }
}
```

### Sortie console attendue

```
OCR complete. Extracted text:
서울시청
```

Et vous trouverez trois nouveaux fichiers à côté de votre image source :

- `korean_ocr.json` – données de reconnaissance complètes.  
- `korean_searchable.pdf` – un PDF que vous pouvez rechercher.  
- (optional) tout journal intermédiaire que vous choisissez d'ajouter.

## Questions fréquentes et cas particuliers

**Et si je n’ai pas de GPU ?**  
Définissez `EnableGpu = false` ; le repli sur le CPU est parfaitement adéquat pour de petits lots.

**Puis‑je traiter plusieurs images en une seule exécution ?**  
Absolument. Enveloppez la logique principale dans une boucle `foreach (var file in Directory.GetFiles(...))` et ré‑attribuez `ocrEngine.Image` à chaque itération.

**Comment gérer d’autres langues avec le coréen ?**  
Aspose.OCR vous permet de définir `Language = Language.AutoDetect` ou de combiner des langues avec l'opérateur OU bit à bit (par ex., `Language.Korean | Language.English`).

**Et si la confiance de l'OCR est faible ?**  
Inspectez `detailedResult.Pages[0].Words` et filtrez les entrées avec `Confidence < 0.7`. Vous pouvez également ajuster les filtres de prétraitement — essayez d'ajouter `PreprocessFilter.ContrastEnhancement`.

## Conclusion

Vous venez de voir comment réaliser **Korean Language OCR** de bout en bout, depuis **loading image from stream** jusqu'à **extract plain text**, puis **convert image to PDF** et enfin **export searchable PDF**. L'approche est modulaire, vous pouvez donc remplacer la source d'image, changer le format de sortie ou intégrer le JSON dans n'importe quel pipeline en aval.

Quelles sont les prochaines étapes

## Tutoriels associés

- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Reconnaître du texte sur une image avec Aspose OCR pour plusieurs langues](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extraire du texte d'une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}