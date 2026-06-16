---
category: general
date: 2026-05-21
description: Effectuer la reconnaissance optique de caractères (OCR) sur une image
  avec C#. Apprenez comment charger une image pour l’OCR, extraire du texte d’un PNG
  et reconnaître le texte d’une image avec un petit exemple de code.
draft: false
keywords:
- perform OCR on image
- extract text from PNG
- recognize text from image
- load image for OCR
language: fr
og_description: Effectuez rapidement la reconnaissance OCR d’une image en C#. Ce guide
  montre comment charger une image pour l’OCR, extraire le texte d’un PNG et reconnaître
  le texte d’une image avec une sortie HTML respectant la mise en page.
og_title: Effectuer la reconnaissance optique de caractères sur une image avec C#
  – Tutoriel complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  headline: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Perform OCR on image using C#. Learn how to load image for OCR, extract
    text from PNG, and recognize text from image with a tiny code sample.
  name: Perform OCR on Image with C# – Complete Step‑by‑Step Guide
  steps:
  - name: Load Image for OCR
    text: The line `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");`
      is where we **load image for OCR**. The `ImageStream` helper abstracts away
      file‑format details, so you can feed JPEG, BMP, or TIFF without changing code.
  - name: Extract Text from PNG
    text: 'Once `engine.Recognize()` finishes, the OCR engine holds the recognized
      text internally. You can pull it out as a string if you only need raw text:'
  - name: Recognize Text from Image
    text: 'The `Recognize()` call does the heavy lifting. Under the hood the engine:'
  - name: Handling Layout‑Aware HTML Output
    text: 'Most developers stop at plain text, but the `HtmlSaveOptions` we used let
      you **perform OCR on image** and keep the visual structure intact. Two flags
      matter:'
  - name: Scaling to Multiple Files
    text: 'If you need to **perform OCR on image** files in a folder, wrap the core
      logic in a simple loop:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Aspose.OCR
title: Effectuer la reconnaissance optique de caractères (OCR) sur une image avec
  C# – Guide complet étape par étape
url: /fr/net/text-recognition/perform-ocr-on-image-with-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image avec C# – Guide complet étape par étape

Vous êtes-vous déjà demandé comment **effectuer une OCR sur des fichiers image** sans vous embourber dans des interfaces lourdes ? Vous n'êtes pas seul. Que vous numérisiez des reçus, extrayiez des données de formulaires scannés, ou que vous ayez simplement besoin de transformer un PNG en texte recherchable, quelques lignes de C# suffisent.

Dans ce tutoriel, nous allons parcourir le chargement d’une image pour l’OCR, la reconnaissance du texte à partir de l’image, puis l’extraction du texte du PNG sous forme de HTML propre. À la fin, vous disposerez d’une application console prête à l’emploi qui **effectue une OCR sur des fichiers image** et préserve la mise en page d’origine.

## Ce que vous allez créer

- Un programme console minimal qui lit un PNG (ou toute image prise en charge)  
- Utilise un moteur OCR pour **reconnaître le texte à partir de l’image**  
- Enregistre le résultat sous forme de HTML sensible à la mise en page, en incorporant l’image originale  
- Montre comment **charger une image pour l’OCR**, **extraire le texte d’un PNG**, et gérer les cas limites courants  

> **Prérequis**  
> - SDK .NET 6.0 ou ultérieur (vous pouvez aussi cibler .NET Framework 4.7+)  
> - Une bibliothèque OCR compatible NuGet – l’exemple utilise *Aspose.OCR* mais toute bibliothèque avec une API similaire fonctionnera  
> - Connaissances de base en C# (rien de compliqué)  

Vous avez tout ça ? Parfait—plongeons‑y.

## Effectuer une OCR sur une image – Parcours complet du code

Voici le programme **complet et exécutable**. Copiez‑collez‑le dans un nouveau projet console (`dotnet new console`) et appuyez sur **F5**.

```csharp
using System;
using Aspose.OCR;               // OCR engine namespace
using Aspose.OCR.Models;        // Save options namespace
using Aspose.OCR.ImageProcessing; // Image loading helpers

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine and set the language
            // -------------------------------------------------
            var engine = new OcrEngine
            {
                Language = OcrLanguage.English   // You can change to French, German, etc.
            };

            // -------------------------------------------------
            // Step 2: Load the image for OCR
            // -------------------------------------------------
            // Replace the path with your actual PNG/JPEG/TIFF file.
            engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");

            // -------------------------------------------------
            // Step 3: Perform OCR recognition
            // -------------------------------------------------
            engine.Recognize();

            // -------------------------------------------------
            // Step 4: Configure HTML save options – keep layout
            // -------------------------------------------------
            var htmlOptions = new HtmlSaveOptions
            {
                PreserveLayout = true,   // Keep columns, tables, and spacing
                EmbedImages = true       // Embed the original PNG inside the HTML
            };

            // -------------------------------------------------
            // Step 5: Save the recognized content as layout‑aware HTML
            // -------------------------------------------------
            engine.Save("YOUR_DIRECTORY/form.html", htmlOptions);

            Console.WriteLine("HTML with layout saved.");
        }
    }
}
```

> **Sortie attendue**  
> ```
> HTML with layout saved.
> ```  
> Après l’exécution, vous trouverez `form.html` à côté de votre PNG. Ouvrez‑le dans un navigateur et vous verrez exactement la même mise en page, mais le texte sera désormais sélectionnable et recherchable.

### Charger une image pour l’OCR

La ligne `engine.Image = ImageStream.FromFile("YOUR_DIRECTORY/form.png");` est celle où nous **chargeons l’image pour l’OCR**. L’assistant `ImageStream` masque les détails du format de fichier, vous permettant d’alimenter JPEG, BMP ou TIFF sans modifier le code.  

**Pourquoi ne pas simplement passer un `Bitmap` ?**  
Parce que de nombreux SDK OCR attendent un flux qui transporte également les métadonnées DPI. Utiliser le chargeur intégré de la bibliothèque garantit que le moteur voit l’image exactement comme elle apparaît à l’écran, ce qui améliore la précision.

#### Astuce pro
Si vous traitez un lot de fichiers, encapsulez l’étape de chargement dans un `try/catch` et journalisez toute `FileNotFoundException`. Cela empêche le plantage du lot entier lorsqu’un fichier est manquant.

### Extraire le texte d’un PNG

Une fois que `engine.Recognize()` a terminé, le moteur OCR conserve le texte reconnu en interne. Vous pouvez le récupérer sous forme de chaîne si vous ne avez besoin que du texte brut :

```csharp
string plainText = engine.Text;   // Returns the whole document as plain text
Console.WriteLine(plainText);
```

C’est la façon la plus rapide d’**extraire le texte d’un PNG** lorsque la mise en page ne vous intéresse pas. Pour la plupart des tâches de saisie de données, le texte brut suffit—n’oubliez pas de supprimer les sauts de ligne si vous prévoyez d’importer dans un CSV.

### Reconnaître le texte à partir de l’image

L’appel `Recognize()` fait le gros du travail. En interne, le moteur :

1. Normalise l’image (redresse, supprime le bruit)  
2. La segmente en lignes et mots  
3. Exécute un classificateur de réseau neuronal entraîné sur des millions de glyphes  

Comme nous avons défini `Language = OcrLanguage.English`, le moteur applique les dictionnaires spécifiques à l’anglais, ce qui réduit considérablement les faux positifs. Si vous avez besoin d’un support multilingue, passez simplement un tableau de langues :

```csharp
engine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

### Gestion de la sortie HTML sensible à la mise en page

La plupart des développeurs s’arrêtent au texte brut, mais le `HtmlSaveOptions` que nous utilisons vous permet d’**effectuer une OCR sur une image** tout en conservant la structure visuelle. Deux indicateurs sont importants :

- `PreserveLayout = true` – conserve les colonnes, tableaux et espaces.  
- `EmbedImages = true` – insère le PNG original sous forme d’élément `<img>` encodé en Base64, rendant le HTML autonome.

Si vous préférez un fichier plus léger, définissez `EmbedImages = false` et le HTML référencera le PNG original sur le disque.

#### Cas limite : fichiers volumineux

Pour les images supérieures à 5 Mo, l’incorporation peut gonfler la taille du HTML. Dans ce cas, utilisez des références d’image externes et envisagez de compresser le PNG au préalable avec `ImageProcessor.Compress`.

## Pièges courants et astuces pro

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Caractères illisibles | Langue incorrecte ou pack linguistique manquant | Installez les fichiers de données linguistiques appropriés et définissez correctement `engine.Language` |
| Aucun texte dans la sortie | Image trop sombre ou basse résolution | Pré‑traitez avec `engine.Image = ImageProcessor.AdjustContrast(engine.Image, 1.2)` |
| Mise en page cassée dans le HTML | `PreserveLayout` laissé à la valeur par défaut `false` | Définissez `PreserveLayout = true` dans `HtmlSaveOptions` |
| Traitement lent sur de nombreuses pages | Le moteur se réinitialise à chaque fichier | Réutilisez la même instance `OcrEngine` et ne changez que `engine.Image` à chaque itération |

### Mise à l’échelle vers plusieurs fichiers

Si vous devez **effectuer une OCR sur des fichiers image** dans un dossier, encapsulez la logique principale dans une boucle simple :

```csharp
foreach (var file in Directory.GetFiles("YOUR_DIRECTORY", "*.png"))
{
    engine.Image = ImageStream.FromFile(file);
    engine.Recognize();
    var htmlPath = Path.ChangeExtension(file, ".html");
    engine.Save(htmlPath, htmlOptions);
    Console.WriteLine($"Processed {Path.GetFileName(file)}");
}
```

Notez que nous **chargeons l’image pour l’OCR** à l’intérieur de la boucle, mais nous conservons les mêmes objets `engine` et `htmlOptions`. Cela réduit le turnover mémoire et accélère les traitements par lots.

## Aller plus loin : exportation vers PDF ou DOCX

Le même `engine` peut enregistrer dans d’autres formats :

```csharp
engine.Save("output.pdf", new PdfSaveOptions { PreserveLayout = true });
engine.Save("output.docx", new WordSaveOptions { PreserveLayout = true });
```

Si votre système en aval attend des PDF recherchables, il suffit d’une ligne de changement—pas besoin de créer une chaîne de conversion séparée.

## Conclusion

Nous venons de vous montrer comment **effectuer une OCR sur des fichiers image** avec C#, du chargement de la photo à **extraire le texte d’un PNG** puis **reconnaître le texte à partir de l’image** dans un fichier HTML sensible à la mise en page. L’exemple complet est prêt à être exécuté, et vous comprenez maintenant pourquoi chaque étape est importante, comment l’ajuster pour différentes langues, et quels pièges éviter.

Ensuite, essayez de remplacer la langue anglaise par une autre locale, expérimentez `PreserveLayout = false` pour obtenir un HTML plus léger, ou canalisez la sortie texte brute vers une base de données pour des archives recherchables. Le ciel est la limite lorsqu’on combine un moteur OCR solide avec quelques lignes de C#.

Des questions sur la gestion des TIFF multi‑pages, ou envie de savoir comment intégrer cela dans une API ASP.NET Core ? Laissez un commentaire ci‑dessous, et bon codage !


## Tutoriels associés

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}