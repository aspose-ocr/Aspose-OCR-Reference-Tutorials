---
category: general
date: 2026-02-28
description: Extraire du texte d’une image avec Aspose.OCR sans Internet. Apprenez
  à reconnaître le texte à partir d’un PNG, à lire le texte d’un scan, à convertir
  une image en texte et à charger une image pour l’OCR.
draft: false
keywords:
- extract text from image
- recognize text from png
- read text from scan
- convert image to text
- load image for OCR
language: fr
og_description: Extraire du texte d’une image hors ligne avec Aspose.OCR. Ce tutoriel
  montre comment reconnaître le texte à partir d’un PNG, lire le texte d’un scan,
  convertir une image en texte et charger une image pour l’OCR.
og_title: Extraire du texte d'une image en C# – Guide OCR hors ligne
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extraire du texte d’une image en C# – Guide pas à pas de l’OCR hors ligne
url: /fr/net/text-recognition/extract-text-from-image-in-c-offline-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en C# – Guide pas à pas de l'OCR hors ligne

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais votre application ne peut pas dépendre d'une connexion Internet ? Peut‑être construisez‑vous un scanner sécurisé qui fonctionne sur un appareil sandboxé, ou vous voulez simplement éviter les pics de latence. Dans les deux cas, la bonne nouvelle est qu'Aspose.OCR vous permet d'**reconnaître du texte à partir de fichiers png** entièrement hors ligne.  

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui vous montre comment **lire du texte à partir de fichiers numérisés**, **convertir une image en texte**, et **charger une image pour l'OCR** en utilisant la bibliothèque Aspose.OCR. À la fin, vous disposerez d’une application console autonome qui affiche le texte extrait dans la console — aucun service cloud requis.

## Ce dont vous avez besoin

- **.NET 6.0** (ou toute version récente de .NET). La syntaxe présentée fonctionne avec .NET 6+ mais les mêmes concepts s’appliquent à .NET Framework 4.7+.
- **Aspose.OCR for .NET** package NuGet. Installez‑le avec `dotnet add package Aspose.OCR`.
- Un fichier image (png, jpg, bmp, etc.) contenant du texte clair et lisible. Pour ce guide, nous l’appellerons `offline_test.png` et le placerons dans un dossier nommé `YOUR_DIRECTORY`.
- Un IDE préféré (Visual Studio, VS Code, Rider — ce qui vous convient).

> **Astuce :** Conservez le pack de langue dont vous avez besoin (l'anglais dans l'exemple) sur la même machine que l'application ; cela garantit un fonctionnement réellement hors ligne.

## Étape 1 – Configurer le projet et installer Aspose.OCR

Créez un nouveau projet console et ajoutez la bibliothèque OCR.

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
dotnet add package Aspose.OCR
```

> **Pourquoi c’est important :** L’ajout du package NuGet restaure toutes les DLL nécessaires, vous n’obtiendrez donc pas d’erreur « référence manquante » lors de la compilation.

## Étape 2 – Configurer le moteur OCR pour une utilisation hors ligne

Le cœur de la solution est la classe `OcrEngine`. En définissant `OfflineMode` à `true`, vous garantissez que le moteur ne fera jamais d’appel réseau. Vous spécifiez également le pack de langue qui réside localement.

```csharp
using Aspose.OCR;
using System.Drawing;   // For Image.Load

// Initialize the OCR engine
var ocrEngine = new OcrEngine
{
    OfflineMode = true,               // Prevent any network calls
    Language = OcrLanguage.English    // Use the locally‑installed English pack
};
```

> **Explication :** `OfflineMode` est une mesure de sécurité. Si vous oubliez de le définir, Aspose peut silencieusement contacter son service cloud pour télécharger les données de langue manquantes, ce qui annule l’objectif d’un scanner hors ligne.

## Étape 3 – Charger l'image à traiter

Charger l'image est simple, mais notez l’utilisation de `using var` qui garantit que le bitmap est automatiquement libéré.

```csharp
// Adjust the path to point at your image file
using var image = Image.Load(@"YOUR_DIRECTORY/offline_test.png");

// Quick sanity check – you can inspect image.Width / image.Height if needed
Console.WriteLine($"Loaded image with dimensions: {image.Width}x{image.Height}");
```

> **Cas particulier :** Si le fichier n’est pas trouvé, `Image.Load` lève une `FileNotFoundException`. Enveloppez l’appel dans un bloc try‑catch pour le code de production.

## Étape 4 – Exécuter l'OCR et récupérer le texte

Nous effectuons maintenant la reconnaissance. La méthode `Recognize` renvoie un objet `OcrResult` qui contient la chaîne extraite et les scores de confiance.

```csharp
// Perform OCR
var ocrResult = ocrEngine.Recognize(image);

// The Text property holds the plain‑text extraction
string extractedText = ocrResult.Text;

// Show the result
Console.WriteLine("\n--- OCR Output ---");
Console.WriteLine(extractedText);
```

> **Ce que vous voyez :** `ocrResult.Text` est déjà une chaîne propre — pas besoin de supprimer les sauts de ligne sauf si votre logique en aval l’exige.

## Étape 5 – Exemple complet fonctionnel

En rassemblant le tout, voici le fichier complet `Program.cs` que vous pouvez copier‑coller dans votre projet. Il compile et s’exécute tel quel (remplacez simplement le chemin de l’image).

```csharp
using Aspose.OCR;
using System.Drawing;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine for offline use
        var ocrEngine = new OcrEngine
        {
            OfflineMode = true,               // Prevent any network calls
            Language = OcrLanguage.English    // Use a locally‑available language pack
        };

        // Step 2: Load the image you want to process
        using var image = Image.Load(@"YOUR_DIRECTORY/offline_test.png");

        // Step 3: Run OCR on the loaded image
        var ocrResult = ocrEngine.Recognize(image);

        // Step 4: Display the extracted text
        System.Console.WriteLine("\n--- Extracted Text ---");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Sortie attendue

Si `offline_test.png` contient la phrase « Hello, world! », la console affichera :

```
--- Extracted Text ---
Hello, world!
```

Pour des documents plus longs, vous verrez le paragraphe complet, les sauts de ligne et la ponctuation préservés tels que le moteur OCR les interprète.

## Questions fréquentes & pièges

### 1. *Puis‑je reconnaître du texte à partir de fichiers png avec un arrière‑plan coloré ?*  
Oui. Aspose.OCR applique automatiquement une étape de prétraitement qui normalise le contraste. Si l’arrière‑plan est trop bruité, envisagez de convertir d’abord l’image en niveaux de gris :

```csharp
image = image.ConvertToGrayscale();
```

### 2. *Et si je dois lire du texte à partir de PDF numérisés au lieu de PNG ?*  
Extrayez chaque page sous forme d’image (en utilisant une bibliothèque PDF comme Aspose.PDF) et alimentez ces images dans le même pipeline OCR. Le flux de travail reste identique une fois que vous avez un bitmap.

### 3. *Comment gérer les résultats à faible confiance ?*  
`OcrResult` inclut une propriété `Confidence` par caractère. Vous pouvez parcourir `ocrResult.Characters` et signaler tout caractère dont la confiance est < 0,75 pour une révision manuelle.

### 4. *Le pack de langue anglais est‑il le seul à fonctionner hors ligne ?*  
Non. Tout pack de langue installé localement (par ex., `OcrLanguage.Spanish`) fonctionne de la même façon — il suffit de définir `Language = OcrLanguage.Spanish`.

### 5. *Puis‑je traiter un dossier d’images en lot ?*  
Absolument. Enveloppez la logique de chargement et de reconnaissance dans une boucle `foreach (var file in Directory.GetFiles(folder, "*.png"))`. N’oubliez pas de libérer chaque image après le traitement.

## Conseils de performance

- **Réutilisez l’instance `OcrEngine`** pour plusieurs images. Créer un nouveau moteur pour chaque fichier ajoute une surcharge.
- **Redimensionnez les grandes images** à un maximum de 2000 px sur le côté le plus long ; des dimensions plus grandes n’améliorent pas la précision mais ralentissent le traitement.
- **Activez le multithreading** si vous avez de nombreuses images — assurez‑vous simplement que chaque thread possède son propre `OcrEngine` ou protégez le partagé avec un verrou.

## Vue d’ensemble visuelle

![Diagramme montrant le flux OCR hors ligne – extraire du texte d'une image → charger l'image pour l'OCR → reconnaître le texte à partir de png → texte de sortie](https://example.com/ocr-flow.png "Flux de travail d'extraction de texte d'image")

*L'illustration met en évidence les quatre étapes principales couvertes dans ce guide.*

## Conclusion

Vous savez maintenant comment **extraire du texte d'une image** entièrement hors ligne en utilisant Aspose.OCR. Le tutoriel a couvert tout, depuis la configuration du projet, la configuration du moteur en mode hors ligne, le chargement d’une image, jusqu’à **reconnaître du texte à partir de png** et **lire du texte à partir de documents numérisés**. Avec le code source complet à portée de main, vous pouvez rapidement adapter la solution pour **convertir une image en texte** dans des travaux par lots, l’intégrer à des utilitaires de bureau, ou l’incorporer dans des services côté serveur qui doivent rester sur site.

Et après ? Essayez de remplacer le pack de langue anglais par une autre langue, expérimentez le prétraitement d’image (seuillage, redressement), ou alimentez la sortie OCR dans un pipeline de traitement du langage naturel pour l’analyse de sentiment. Le ciel est la limite lorsque vous combinez l’OCR hors ligne avec les outils .NET modernes.

Bon codage, et que vos numérisations soient toujours d’une clarté cristalline !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}