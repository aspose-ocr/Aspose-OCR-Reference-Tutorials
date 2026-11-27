---
category: general
date: 2026-11-26
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) sur
  des fichiers PNG, à convertir les PNG en texte et à extraire du texte cyrillique
  à l’aide d’Aspose.OCR – guide étape par étape pour les développeurs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- convert PNG to text
- recognize text from PNG
- extract Cyrillic text
- load image for OCR
language: fr
lastmod: 2026-11-26
og_description: Comment effectuer la reconnaissance optique de caractères (OCR) sur
  des fichiers PNG et extraire du texte cyrillique à l'aide d'Aspose.OCR en C#. Suivez
  ce tutoriel complet pour convertir un PNG en texte.
og_image_alt: how to perform OCR on a PNG image using Aspose.OCR
og_title: Comment effectuer la reconnaissance optique de caractères (OCR) sur des
  images PNG avec Aspose.OCR – Guide C#
schemas:
- author: Aspose
  dateModified: '2026-11-26'
  description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  headline: How to perform OCR on PNG images with Aspose.OCR in C#
  type: TechArticle
- description: Learn how to perform OCR on PNG files, convert PNG to text, and extract
    Cyrillic text using Aspose.OCR – step‑by‑step guide for developers.
  name: How to perform OCR on PNG images with Aspose.OCR in C#
  steps:
  - name: Handling large images
    text: 'If the PNG is larger than 2 MB, consider down‑scaling it before recognition
      to speed up processing:'
  - name: 'Edge case: Missing language module'
    text: 'If the download fails (e.g., offline environment), the engine throws an
      `OcrException`. Catch it to provide a graceful fallback:'
  - name: Expected output
    text: 'If `sample_image.png` contains the Cyrillic phrase “Привет мир”, the console
      will display:'
  - name: How it works
    text: 1. **Engine creation** – prepares the OCR pipeline. 2. **Image loading**
      – supports both raw PNG and down‑scaled versions for performance. 3. **Language
      selection** – demonstrates **extract Cyrillic text** while handling missing
      modules. 4. **Recognition** – the core **recognize text from PNG** call
  type: HowTo
tags:
- OCR
- C#
- Aspose.OCR
title: Comment effectuer l'OCR sur des images PNG avec Aspose.OCR en C#
url: /fr/net/text-recognition/how-to-perform-ocr-on-png-images-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR sur des images PNG avec Aspose.OCR en C#

Si vous devez **how to perform OCR** sur un fichier PNG, ce guide vous montre les étapes exactes pour convertir PNG en texte à l'aide d'Aspose.OCR. Que vous extrayiez du texte cyrillique à partir de documents numérisés ou que vous reconnaissiez simplement du texte à partir de captures d'écran PNG, la solution fonctionne immédiatement et ne nécessite que quelques lignes de code C#.

Dans ce tutoriel, vous apprendrez à :

* **load image for OCR** depuis un dossier local,
* configurer le moteur pour **extract Cyrillic text**,
* **recognize text from PNG** et obtenir une chaîne propre,
* gérer les problèmes courants tels que les modules de langue manquants et les images volumineuses.

Aucune expérience préalable avec Aspose.OCR n'est requise — il suffit d'un environnement de développement .NET et d'une image PNG que vous souhaitez traiter.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

* .NET 6.0 (ou version ultérieure) installé.
* Une copie sous licence ou d'essai d'**Aspose.OCR for .NET**. Vous pouvez obtenir un essai gratuit sur le site d'Aspose.
* Visual Studio 2022 (ou tout IDE supportant .NET).
* Un fichier PNG contenant le texte que vous voulez extraire (l'exemple utilise `sample_image.png`).

## Étape 1 : Installer le package NuGet Aspose.OCR

Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Le package comprend le moteur OCR principal et tous les modules de langue. Lorsque vous demandez une langue qui n'est pas présente localement, Aspose.OCR télécharge automatiquement le module requis.

## Étape 2 : Créer une instance du moteur OCR (how to perform OCR)

La première action concrète dans tout flux de travail OCR consiste à instancier le moteur. Cet objet gère toutes les opérations suivantes, comme le chargement de l'image et la reconnaissance.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

**Pourquoi c'est important :** La classe `OcrEngine` encapsule la chaîne de traitement OCR. Créer une seule instance et la réutiliser pour plusieurs images réduit la consommation de mémoire et améliore les performances.

## Étape 3 : Charger l'image pour l'OCR – spécifier le fichier PNG source

Le chargement de l'image est le moment où vous **load image for OCR**. Aspose.OCR accepte plusieurs types d'entrée ; le plus simple est `ImageStream.FromFile`.

```csharp
// Load the PNG image from disk
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_image.png");
```

> **Astuce :** Utilisez un chemin absolu ou `Path.Combine` pour éviter les erreurs d'exécution sur différents environnements.

### Gestion des images volumineuses

Si le PNG dépasse 2 Mo, envisagez de le réduire avant la reconnaissance afin d'accélérer le traitement :

```csharp
using System.Drawing;

// Downscale large images to a maximum width of 1200 pixels
Bitmap original = new Bitmap(@"YOUR_DIRECTORY/sample_image.png");
int maxWidth = 1200;
int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

using (var ms = new MemoryStream())
{
    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
    ocrEngine.Image = ImageStream.FromStream(ms);
}
```

## Étape 4 : Configurer la langue – extract Cyrillic text

Par défaut, Aspose.OCR suppose l'anglais. Pour **extract Cyrillic text**, définissez la propriété `Language` sur `Language.Cyrillic`. Le module requis sera téléchargé automatiquement lors de la première exécution du code.

```csharp
// Set the OCR language to Cyrillic
ocrEngine.Language = Language.Cyrillic;
```

Si vous devez reconnaître plusieurs langues (par ex., anglais et cyrillique), vous pouvez les combiner :

```csharp
ocrEngine.Language = Language.English | Language.Cyrillic;
```

### Cas particulier : module de langue manquant

Si le téléchargement échoue (par ex., environnement hors ligne), le moteur lève une `OcrException`. Capturez‑la pour fournir une solution de secours élégante :

```csharp
try
{
    ocrEngine.Language = Language.Cyrillic;
}
catch (OcrException ex)
{
    Console.WriteLine($"Language module could not be loaded: {ex.Message}");
    // Optionally, fall back to English or abort the process
}
```

## Étape 5 : Effectuer l'opération de reconnaissance (recognize text from PNG)

Maintenant que l'image et la langue sont définies, vous pouvez **recognize text from PNG**. La méthode `Recognize` exécute la chaîne OCR de façon synchrone.

```csharp
// Run OCR
ocrEngine.Recognize();
```

**Pourquoi cela fonctionne :** En interne, Aspose.OCR applique un pré‑traitement (binarisation, suppression du bruit) avant d'alimenter l'image dans un reconnaisseur basé sur un réseau neuronal adapté à la langue sélectionnée.

## Étape 6 : Récupérer et afficher le texte reconnu (convert PNG to text)

Après la reconnaissance, la chaîne extraite est disponible via la propriété `Text`. C'est l'étape finale de **convert PNG to text**.

```csharp
// Get the recognized text
string recognizedText = ocrEngine.Text;

// Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

### Résultat attendu

Si `sample_image.png` contient la phrase cyrillique « Привет мир », la console affichera :

```
=== OCR Result ===
Привет мир
```

La sortie peut inclure des sauts de ligne et de la ponctuation exactement comme ils apparaissent dans l'image. Vous pouvez post‑traiter la chaîne avec `String.Trim()`, `Regex` ou d'autres utilitaires de nettoyage de texte si nécessaire.

## Étape 7 : Optionnel – Enregistrer le résultat dans un fichier

Stocker le résultat OCR permet un traitement en aval (par ex., indexation, traduction). Voici une façon rapide d'écrire le texte dans un fichier UTF‑8 :

```csharp
File.WriteAllText(@"YOUR_DIRECTORY/ocr_output.txt", recognizedText, Encoding.UTF8);
Console.WriteLine("OCR text saved to ocr_output.txt");
```

## Problèmes courants et comment les éviter

| Problème | Symptom | Solution |
|----------|----------|----------|
| **Module de langue manquant** | `OcrException` sur `Language = Language.Cyrillic` | Assurez‑vous d'avoir une connexion Internet lors de la première exécution ou pré‑téléchargez les modules via le package hors ligne d'Aspose. |
| **Image floue ou à faible contraste** | Précision médiocre, nombreux caractères « ? » | Pré‑traitez l'image : augmentez le contraste, appliquez un affûtage, ou convertissez en niveaux de gris avant de la transmettre au moteur. |
| **PNG très volumineux** | Temps de traitement long, possible `OutOfMemoryException` | Réduisez la taille comme indiqué à l'étape 3, ou découpez une image multi‑pages en tuiles séparées. |
| **Caractères non UTF‑8** | Sortie corrompue | Vérifiez que la console ou l'écrivain de fichier utilise l'encodage UTF‑8 (`Encoding.UTF8`). |

## Exemple complet, exécutable

Voici le programme complet qui intègre toutes les étapes ci‑dessus. Copiez‑le dans un nouveau projet console et exécutez‑le après avoir ajusté les chemins de fichiers.

```csharp
using System;
using System.Drawing;
using System.IO;
using System.Text;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1. Create OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 2. Load PNG image (with optional down‑scaling for large files)
            string imagePath = @"YOUR_DIRECTORY/sample_image.png";
            Bitmap original = new Bitmap(imagePath);
            const int maxWidth = 1200;

            if (original.Width > maxWidth)
            {
                int newHeight = (int)(original.Height * (maxWidth / (double)original.Width));
                Bitmap resized = new Bitmap(original, new Size(maxWidth, newHeight));

                using (var ms = new MemoryStream())
                {
                    resized.Save(ms, System.Drawing.Imaging.ImageFormat.Png);
                    ocrEngine.Image = ImageStream.FromStream(ms);
                }
            }
            else
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }

            // 3. Set language to Cyrillic (fallback to English if needed)
            try
            {
                ocrEngine.Language = Language.Cyrillic;
            }
            catch (OcrException ex)
            {
                Console.WriteLine($"Failed to load Cyrillic module: {ex.Message}");
                Console.WriteLine("Falling back to English.");
                ocrEngine.Language = Language.English;
            }

            // 4. Recognize text
            ocrEngine.Recognize();

            // 5. Retrieve and display the text (convert PNG to text)
            string recognizedText = ocrEngine.Text;
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(recognizedText);

            // 6. Save result to a UTF‑8 file
            string outputPath = @"YOUR_DIRECTORY/ocr_output.txt";
            File.WriteAllText(outputPath, recognizedText, Encoding.UTF8);
            Console.WriteLine($"OCR text saved to {outputPath}");
        }
    }
}
```

### Comment cela fonctionne

1. **Engine creation** – prépare la chaîne de traitement OCR.  
2. **Image loading** – prend en charge les PNG bruts et les versions réduites pour la performance.  
3. **Language selection** – montre comment **extract Cyrillic text** tout en gérant les modules manquants.  
4. **Recognition** – l'appel principal **recognize text from PNG**.  
5. **Result handling** – montre **convert PNG to text** et écrit le résultat dans un fichier.

Exécutez le programme avec `dotnet run`. Si tout est correctement configuré, le texte reconnu s'affichera dans la console et sera enregistré dans `ocr_output.txt`.

## Conclusion

Dans ce tutoriel, vous avez appris **how to perform OCR** sur des fichiers PNG en utilisant Aspose.OCR pour .NET, couvrant tout, de **load image for OCR** à **extract Cyrillic text** et **convert PNG to text**. L'exemple complet et exécutable démontre le flux de travail standard, les cas limites courants et des astuces pratiques pour garder votre pipeline OCR fiable.

**Next steps**

* Explorez **recognize text from PNG** avec des langues supplémentaires (arabe, chinois) en combinant les drapeaux `Language`.  
* Intégrez le résultat OCR avec Azure Cognitive Search pour des archives de documents consultables.  
* Expérimentez les paramètres du `OcrEngine` d'Aspose.OCR tels que `Resolution

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment télécharger le modèle Aspose.OCR et extraire du texte d'un PNG en C#](/ocr/english/net/text-recognition/how-to-download-ocr-model-and-extract-text-from-png-using-as/)
- [Comment effectuer de l'OCR en C# – Reconnaître du texte cyrillique avec Aspose](/ocr/english/net/text-recognition/how-to-perform-ocr-in-c-recognize-cyrillic-text-with-aspose/)
- [Comment faire de l'OCR par lots en C# – Méthode rapide pour extraire du texte de fichiers PNG](/ocr/english/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}