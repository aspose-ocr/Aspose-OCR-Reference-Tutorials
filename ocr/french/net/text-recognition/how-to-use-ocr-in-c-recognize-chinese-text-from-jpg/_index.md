---
category: general
date: 2026-05-25
description: Comment utiliser l'OCR en C# pour extraire du texte à partir de fichiers
  image. Apprenez à reconnaître les caractères chinois à partir d'un JPG en utilisant
  Aspose.OCR en quelques étapes simples.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from jpg
- recognize chinese characters
- ocr chinese simplified
language: fr
og_description: Comment utiliser l'OCR en C# pour extraire du texte à partir de fichiers
  image. Ce guide vous montre comment reconnaître les caractères chinois à partir
  d'un JPG en utilisant Aspose.OCR.
og_title: Comment utiliser l'OCR en C# – Reconnaître le texte chinois à partir d'un
  JPG
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  headline: How to Use OCR in C# – Recognize Chinese Text from JPG
  type: TechArticle
- description: How to use OCR in C# to extract text from image files. Learn to recognize
    Chinese characters from a JPG using Aspose.OCR in a few simple steps.
  name: How to Use OCR in C# – Recognize Chinese Text from JPG
  steps:
  - name: What’s happening under the hood?
    text: '- **`OcrEngine.Language`** tells Aspose which dictionary to use. By picking
      `ChineseSimplified`, we instruct the engine to look for the Simplified Chinese
      language pack. - **First‑time download**: When `Recognize` runs, the SDK reaches
      out to Aspose’s CDN, pulls the ≈6 MB language file, caches it lo'
  - name: 5.1 Dealing with Low‑Quality Images
    text: 'OCR accuracy drops when the source image is blurry, noisy, or has poor
      lighting. A quick fix is to pre‑process the image:'
  - name: 5.2 Running in a Headless Environment
    text: 'If you’re deploying to a Linux container without a GUI, make sure the `libgdiplus`
      library (required for `System.Drawing`) is installed:'
  - name: 5.3 Caching the Language Pack Manually
    text: You can download the language file once and point Aspose to it via the `License`
      API, which eliminates the one‑time network call. This is handy for offline scenarios.
  - name: Expected Output
    text: 'If the JPG contains the phrase “欢迎光临”, the console will print:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Comment utiliser l'OCR en C# – Reconnaître le texte chinois à partir d’un JPG
url: /fr/net/text-recognition/how-to-use-ocr-in-c-recognize-chinese-text-from-jpg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l’OCR en C# – Reconnaître du texte chinois depuis un JPG

Vous êtes-vous déjà demandé **comment utiliser l’OCR** pour extraire des mots d’une photo que vous avez prise avec votre téléphone ? Vous n’êtes pas seul. Dans de nombreux projets réels—pensez aux scanners de reçus, aux applications de traduction ou à la saisie automatisée de données—vous aurez besoin d’**extraire du texte depuis une image** rapidement et de manière fiable.

Dans ce tutoriel, nous allons parcourir un exemple complet et exécutable qui **reconnaît le texte depuis des fichiers JPG** et gère même le cas délicat de **reconnaître des caractères chinois** en utilisant le pack linguistique **OCR Chinese Simplified**. À la fin, vous disposerez d’une application console autonome qui affiche la chaîne détectée dans la console, sans téléchargements manuels supplémentaires.

> **Note rapide :** Le code fonctionne avec Aspose.OCR ≥ 23.7, qui télécharge automatiquement les ressources linguistiques lors de la première utilisation. Si vous utilisez une version antérieure, vous devrez ajouter la langue manuellement.

## Prérequis

Avant de commencer, assurez-vous d’avoir :

- Le SDK .NET 6.0 ou une version ultérieure (l’exemple cible .NET 6, mais .NET 5 fonctionne également)
- Une version récente de Visual Studio 2022 ou VS Code avec l’extension C#
- Une connexion Internet pour le premier téléchargement de la langue
- Une image JPG contenant du texte chinois simplifié (nous l’appellerons `chinese_sign.jpg`)

C’est tout—pas de moteurs OCR lourds, pas de manipulation de DLL natives. Juste quelques commandes NuGet et quelques lignes de code.

## Étape 1 : Installer Aspose.OCR via NuGet

Première chose à faire : nous avons besoin de la bibliothèque OCR. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Ou, si vous préférez l’interface Visual Studio, faites un clic droit sur **Dependencies → Manage NuGet Packages**, recherchez “Aspose.OCR”, puis cliquez sur **Install**.

> **Astuce :** Gardez vos packages à jour. De nouveaux packs linguistiques et des améliorations de performances arrivent à chaque version mineure.

## Étape 2 : Créer un nouveau projet console (si vous ne l’avez pas encore fait)

Si vous partez de zéro, créez une nouvelle application console :

```bash
dotnet new console -n OcrChineseDemo
cd OcrChineseDemo
```

Vous avez maintenant un fichier `Program.cs` prêt pour le code OCR.

## Étape 3 : Écrire le code OCR – Reconnaître le chinois simplifié depuis un JPG

Ouvrez `Program.cs` et remplacez son contenu par ce qui suit. Chaque ligne est commentée afin que vous puissiez voir *pourquoi* nous faisons chaque étape, pas seulement *quoi* nous faisons.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;   // Required for Image.FromFile

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // --------------------------------------------------------------
            // 1️⃣  Initialise the OCR engine and request the Simplified Chinese
            //     language. This language isn’t bundled in the core package,
            //     so Aspose.OCR will download it the first time you call
            //     Recognize().
            // --------------------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                // The enum value maps to the language pack name.
                Language = OcrLanguage.ChineseSimplified
            };

            // --------------------------------------------------------------
            // 2️⃣  Load the image you want to process. Replace the path with
            //     the actual location of your JPG file.
            // --------------------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";
            using var image = Image.FromFile(imagePath);

            // --------------------------------------------------------------
            // 3️⃣  Perform the recognition. The first call may take a few
            //     seconds because the language resources are being fetched.
            // --------------------------------------------------------------
            string recognizedText = ocrEngine.Recognize(image);

            // --------------------------------------------------------------
            // 4️⃣  Output the result to the console.
            // --------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Que se passe-t-il en coulisses ?

- **`OcrEngine.Language`** indique à Aspose quel dictionnaire utiliser. En choisissant `ChineseSimplified`, nous demandons au moteur de charger le pack linguistique chinois simplifié.
- **Téléchargement initial** : lorsque `Recognize` s’exécute, le SDK contacte le CDN d’Aspose, télécharge le fichier linguistique d’environ 6 Mo, le met en cache localement, puis poursuit l’OCR. Les appels suivants sont instantanés.
- **`Image.FromFile`** fonctionne avec n’importe quel format raster que .NET peut décoder—JPG, PNG, BMP—vous permettant ainsi d’**extraire du texte depuis une image** de nombreux types, pas seulement JPG.

## Étape 4 : Exécuter l’application et vérifier la sortie

Compilez et lancez :

```bash
dotnet run
```

Vous devriez voir quelque chose comme :

```
=== Recognized Text ===
欢迎光临
```

Si la console affiche du texte illisible ou une chaîne vide, revérifiez :

1. L’image contient bien des caractères chinois clairs et à fort contraste.
2. Le chemin du fichier est correct (pas d’espaces superflus ou d’extensions manquantes).
3. Votre machine peut accéder à `https://download.aspose.com` pour le pack linguistique.

## Étape 5 : Gestion des cas limites et des pièges courants

### 5.1 Traiter des images de mauvaise qualité

La précision de l’OCR diminue lorsque l’image source est floue, bruitée ou mal éclairée. Une solution rapide consiste à pré‑traiter l’image :

```csharp
using System.Drawing.Imaging;

// Convert to grayscale
var gray = new Bitmap(image.Width, image.Height);
using (var g = Graphics.FromImage(gray))
{
    var colorMatrix = new ColorMatrix(
        new float[][]{
            new float[]{0.3f,0.3f,0.3f,0,0},
            new float[]{0.59f,0.59f,0.59f,0,0},
            new float[]{0.11f,0.11f,0.11f,0,0},
            new float[]{0,0,0,1,0},
            new float[]{0,0,0,0,1}
        });
    var attributes = new ImageAttributes();
    attributes.SetColorMatrix(colorMatrix);
    g.DrawImage(image, new Rectangle(0,0,image.Width,image.Height),
                0,0,image.Width,image.Height, GraphicsUnit.Pixel, attributes);
}

// Use the processed bitmap for OCR
string recognizedText = ocrEngine.Recognize(gray);
```

### 5.2 Exécution dans un environnement sans interface graphique

Si vous déployez dans un conteneur Linux sans GUI, assurez‑vous que la bibliothèque `libgdiplus` (requise par `System.Drawing`) est installée :

```bash
apt-get update && apt-get install -y libgdiplus
```

### 5.3 Mettre en cache le pack linguistique manuellement

Vous pouvez télécharger le fichier linguistique une fois et indiquer à Aspose son emplacement via l’API `License`, ce qui élimine l’appel réseau unique. Cela est pratique pour les scénarios hors ligne.

```csharp
// Assuming you have the .dat file downloaded to /opt/ocr/langs/
ocrEngine.SetLicense("Aspose.OCR.lic"); // optional if you have a paid license
ocrEngine.LoadLanguage(@" /opt/ocr/langs/ChineseSimplified.dat");
```

## Exemple complet (tout‑en‑un)

Voici le programme *complet* que vous pouvez copier‑coller dans `Program.cs`. Aucun morceau caché, aucun script externe.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

namespace OcrChineseDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialise OCR engine with Simplified Chinese language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified
            };

            // Path to the JPG image containing Chinese text
            string imagePath = @"YOUR_DIRECTORY/chinese_sign.jpg";

            // Load the image (ensure the file exists)
            using var image = Image.FromFile(imagePath);

            // Recognize text – first call may download the language pack
            string recognizedText = ocrEngine.Recognize(image);

            // Display the result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### Sortie attendue

Si le JPG contient la phrase « 欢迎光临 », la console affichera :

```
=== Recognized Text ===
欢迎光临
```

N’hésitez pas à remplacer l’image par tout autre signe, nom de rue ou étiquette produit en chinois simplifié — le moteur fera de son mieux.

## Conclusion

Nous venons de voir **comment utiliser l’OCR** en C# pour **extraire du texte depuis une image**, en abordant spécifiquement le défi de **reconnaître des caractères chinois** dans un **JPG**. En tirant parti du téléchargement à la volée du pack linguistique d’Aspose.OCR, vous pouvez garder votre déploiement léger tout en supportant **OCR Chinese Simplified** dès le départ.

Et après ? Essayez ces idées :

- **Traitement par lots** : parcourez un dossier d’images et écrivez chaque résultat dans un CSV.
- **Combinaison avec des API de traduction** : transmettez la chaîne reconnue à Azure Translator pour des applications multilingues en temps réel.
- **Explorer d’autres langues** : remplacez `OcrLanguage.ChineseSimplified` par `Japanese` ou `Arabic` et voyez comment le même code s’adapte.

Des questions sur l’optimisation des performances, la licence ou l’intégration de l’OCR dans un service web ? Laissez un commentaire ci‑dessous—bon codage ! 

---

![Capture d’écran de la sortie console montrant comment utiliser l’OCR en C# pour reconnaître du texte chinois depuis une image JPG](ocr-chinese-demo.png "sortie console de l’utilisation de l’OCR")


## Tutoriels associés

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}