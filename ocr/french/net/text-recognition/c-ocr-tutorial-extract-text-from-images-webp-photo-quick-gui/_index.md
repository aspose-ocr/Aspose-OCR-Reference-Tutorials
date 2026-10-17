---
category: general
date: 2026-03-17
description: c# tutoriel OCR – découvrez comment extraire du texte à partir de fichiers
  image, lire le texte des photos WebP et convertir une image en texte à l'aide d'un
  OcrEngine simple.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- read text from webp
- recognize text from photo
- convert image to text
language: fr
og_description: Le tutoriel OCR en C# vous montre comment extraire du texte à partir
  de fichiers image, lire le texte des photos WebP et convertir une image en texte
  en quelques lignes de code.
og_title: Tutoriel OCR C# – Extraire du texte d'images en quelques minutes
tags:
- C#
- OCR
- Image Processing
title: 'Tutoriel OCR C# : Extraire du texte à partir d''images (WebP, Photo) – Guide
  rapide'
url: /fr/net/text-recognition/c-ocr-tutorial-extract-text-from-images-webp-photo-quick-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Extraire du texte à partir d'images (WebP, Photo)

Vous avez déjà eu besoin d'**extraire du texte d'un fichier image** sans savoir par où commencer en C# ? Peut‑être avez‑vous un screenshot WebP, un JPEG de reçu, ou une page PDF scannée et vous voulez simplement récupérer les mots qu'elle contient. Dans ce **c# OCR tutorial** nous allons parcourir un exemple complet, prêt à l'emploi, qui lit le texte d'une photo, gère le WebP et d'autres formats modernes, et convertit l'image en texte brut — le tout en quelques lignes de code.

**Quel est le bénéfice ?** Vous pourrez transformer n'importe quelle image contenant du texte en chaînes recherchables, les injecter dans des bases de données, ou les transmettre à des pipelines d'IA en aval. Pas de magie, juste un moteur OCR solide, quelques API .NET, et des explications claires du « pourquoi » derrière chaque étape.

## Ce dont vous avez besoin

Avant de commencer, assurez‑vous d'avoir :

- **.NET 6 SDK** (ou plus récent). Le code ci‑dessous compile avec .NET 6+ et fonctionne sous Windows, Linux ou macOS.
- **Visual Studio 2022** ou tout éditeur de votre choix (VS Code fonctionne très bien).
- Le package NuGet **`Microsoft.Windows.SDK.Contracts`** (qui fournit `Windows.Media.Ocr`). Installez‑le avec :

```bash
dotnet add package Microsoft.Windows.SDK.Contracts
```

- Un fichier image que vous souhaitez traiter – pour ce tutoriel nous utiliserons une photo **WebP** nommée `photo.webp` placée dans un dossier appelé `YOUR_DIRECTORY`.

> Astuce : Si vous êtes sur une plateforme non‑Windows, vous pouvez remplacer le `OcrEngine` par une bibliothèque multiplateforme comme **Tesseract**. Le reste du code reste pratiquement identique.

## Étape 1 : Créer un projet C# OCR Tutorial

Tout d'abord, créez une nouvelle application console. Ouvrez un terminal et exécutez :

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Ajoutez le package requis (comme indiqué ci‑dessus) et ouvrez le projet dans votre IDE. Cette structure de base nous donne une toile vierge pour le **c# OCR tutorial**.

## Étape 2 : Importer les espaces de noms et préparer l'image

Nous avons besoin de quelques directives `using` afin que le compilateur sache où trouver `OcrEngine`, `SoftwareBitmap` et les aides de chargement d'images.

```csharp
using System;
using System.IO;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;
```

> **Pourquoi ces espaces de noms ?**  
> `Windows.Media.Ocr` contient la classe `OcrEngine` qui effectue réellement la reconnaissance. `Windows.Graphics.Imaging` nous permet de décoder l'image (y compris le WebP) en un `SoftwareBitmap` compréhensible par le moteur. Les aides `System.IO` et `Windows.Storage.Streams` simplifient le chargement des fichiers.

Ensuite, chargez l'image. Le décodeur intégré peut gérer WebP, HEIF, PNG, JPEG, et plus, vous permettant ainsi d'**extraire du texte d'un WebP** sans plugins supplémentaires.

```csharp
// Step 2: Load the image file into a SoftwareBitmap
string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

// Open the file as a random access stream
using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
{
    // Decode the image (auto-detects format)
    BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
    SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();
    
    // Optional: Convert to grayscale for better OCR accuracy
    SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);
    
    // Pass the bitmap to the next step
    await RecognizeTextAsync(grayBitmap);
}
```

> **Cas particulier :** Si votre image est déjà en noir et blanc, vous pouvez ignorer l'étape de conversion. La conversion en niveaux de gris apporte un petit gain de performance et améliore souvent la reconnaissance sur des photos bruitées.

## Étape 3 : Exécuter le moteur OCR – Reconnaître le texte de la photo

Voici le cœur du **c# OCR tutorial**. Nous créons une instance de `OcrEngine`, lui fournissons le bitmap, puis récupérons le texte reconnu.

```csharp
static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
{
    // Step 3: Create the OCR engine instance – it automatically picks the best language
    OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

    if (ocrEngine == null)
    {
        Console.WriteLine("❌ No OCR engine available for the current language.");
        return;
    }

    // Perform recognition
    OcrResult ocrResult = await ocrEngine.RecognizeAsync(bitmap);

    // Step 4: Display the extracted text – this is the “convert image to text” part
    Console.WriteLine("📝 Recognized text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Que se passe‑t‑il ?**  
- `TryCreateFromUserProfileLanguages()` sélectionne la ou les langues configurées dans le profil Windows de l'utilisateur, ce qui couvre généralement l'anglais, l'espagnol, etc. Si vous avez besoin d'une langue spécifique, utilisez `OcrEngine.TryCreateFromLanguage(new Language("fr-FR"))`.
- `RecognizeAsync` effectue le travail lourd sur un thread d'arrière‑plan, renvoyant un `OcrResult` contenant la chaîne brute, les boîtes englobantes des mots et les scores de confiance.
- Enfin, nous affichons `ocrResult.Text`, vous donnant le résultat du **convert image to text** que vous pouvez transmettre ailleurs.

## Étape 4 : Exemple complet, exécutable

En rassemblant le tout, voici un programme autonome que vous pouvez copier‑coller dans `Program.cs`. Il compile, s'exécute, et affiche le texte extrait de `photo.webp`.

```csharp
// Program.cs – Complete c# OCR tutorial example
using System;
using System.IO;
using System.Threading.Tasks;
using Windows.Graphics.Imaging;
using Windows.Media.Ocr;
using Windows.Storage.Streams;

class Program
{
    static async Task Main(string[] args)
    {
        // Replace with your actual directory and file name
        string imagePath = Path.Combine("YOUR_DIRECTORY", "photo.webp");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"❗ Image not found: {imagePath}");
            return;
        }

        // Load and optionally preprocess the image
        using (IRandomAccessStream stream = File.OpenRead(imagePath).AsRandomAccessStream())
        {
            BitmapDecoder decoder = await BitmapDecoder.CreateAsync(stream);
            SoftwareBitmap bitmap = await decoder.GetSoftwareBitmapAsync();

            // Convert to grayscale – improves OCR accuracy on many photos
            SoftwareBitmap grayBitmap = SoftwareBitmap.Convert(bitmap, BitmapPixelFormat.Gray8);

            // Run OCR
            await RecognizeTextAsync(grayBitmap);
        }
    }

    static async Task RecognizeTextAsync(SoftwareBitmap bitmap)
    {
        // Create OCR engine (auto‑detect language)
        OcrEngine ocrEngine = OcrEngine.TryCreateFromUserProfileLanguages();

        if (ocrEngine == null)
        {
            Console.WriteLine("❌ Unable to create OCR engine. Ensure language packs are installed.");
            return;
        }

        // Perform recognition
        OcrResult result = await ocrEngine.RecognizeAsync(bitmap);

        // Output the extracted text
        Console.WriteLine("\n--- OCR Output ---");
        Console.WriteLine(result.Text);
        Console.WriteLine("--- End of Output ---\n");
    }
}
```

### Résultat attendu

Si `photo.webp` contient la phrase « Hello, world! This is a test. », vous verrez quelque chose comme :

```
--- OCR Output ---
Hello, world!
This is a test.
--- End of Output ---
```

Les sauts de ligne exacts dépendent de la mise en page de l'image source, mais le résultat de **extract text from image** sera toujours une chaîne brute que vous pourrez manipuler davantage.

## Questions fréquentes & cas particuliers

### Cela fonctionne‑t‑il avec d'autres formats d'image ?

Absolument. Le décodeur utilisé (`BitmapDecoder`) détecte automatiquement JPEG, PNG, BMP, GIF, **WebP**, HEIF, et plus. Vous pouvez donc **read text from WebP**, JPEG, ou même un TIFF sans modifier le code.

### Et si le moteur OCR renvoie une faible confiance ?

Vous pouvez inspecter `ocrResult.Lines` et chaque `OcrWord` pour obtenir un `ConfidenceScore`. Si le score est en dessous d'un seuil (par ex. 0,6), envisagez :

- Un pré‑traitement de l'image (augmenter le contraste, affiner, redresser).
- Utiliser une image source de résolution plus élevée.
- Passer à une bibliothèque dédiée comme **Tesseract** pour le support multilingue.

### Comment gérer plusieurs langues dans la même image ?

Créez des instances séparées de `OcrEngine` pour chaque langue et exécutez‑les séquentiellement, ou utilisez une bibliothèque qui supporte la détection de langues mixtes. Pour le moteur intégré, vous pouvez passer un objet `Language` :

```csharp
var spanishEngine = OcrEngine.TryCreateFromLanguage(new Language("es-ES"));
```

### Puis‑je exécuter cela sous Linux/macOS ?

L'API `Windows.Media.Ocr` est exclusive à Windows. Sur des plateformes non‑Windows, remplacez la section OCR par **Tesseract** (via `Tesseract.Net.SDK`). Le code de chargement et de pré‑traitement reste identique, de sorte que le reste de ce **c# OCR tutorial** s'applique toujours.

## Astuces pro pour une meilleure précision

- **Redimensionnez** les grandes images à un maximum de 2000 px sur le côté le plus long – les moteurs OCR sont plus rapides sur des tailles modérées.
- **Débruitez** avec un simple flou gaussien si la photo est granuleuse.
- **Redressez** le bitmap si le texte n'est pas parfaitement horizontal ; `SoftwareBitmap` peut être tourné avant d'être passé à `OcrEngine`.
- **Mettez en cache** l'instance `OcrEngine` si vous traitez de nombreuses images en lot ; la recréer à chaque fois ajoute une surcharge.

## Sujets connexes à explorer

- **Convert image to text** avec **Tesseract** pour des projets multiplateformes.
- **Extract text from PDF** en rendant chaque page sous forme d'image d'abord.
- **Batch OCR**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}