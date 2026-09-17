---
category: general
date: 2026-02-09
description: Extraire du texte d’une image avec OCR hors ligne en C#. Un exemple complet
  d’OCR en C# montre comment charger une image pour l’OCR, reconnaître le texte cyrillique
  et extraire le texte d’un passeport.
draft: false
keywords:
- extract text from image
- c# ocr example
- load image for ocr
- recognize cyrillic text
- recognize text from passport
language: fr
og_description: Extrayez du texte d'une image avec OCR hors ligne en C#. Découvrez
  un exemple d'OCR en C# étape par étape qui charge une image pour l'OCR, reconnaît
  le texte cyrillique et extrait le texte d'un passeport.
og_title: Extraire du texte d’une image en C# – Guide OCR hors ligne
tags:
- OCR
- C#
- Aspose
title: Extraire du texte d’une image en C# – Exemple d’OCR hors ligne
url: /fr/net/text-recognition/extract-text-from-image-in-c-offline-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image en C# – Exemple d'OCR hors ligne

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais vous êtes bloqué par des API dépendantes du réseau ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur lorsque le service OCR tente de télécharger des packs de langues à l'exécution, surtout dans des environnements restreints.

Dans ce guide, nous parcourrons un **exemple c# ocr** qui fonctionne entièrement hors ligne, charge une image pour l'OCR et reconnaît le texte cyrillique d'un passeport. À la fin, vous disposerez d'un programme prêt à l'emploi qui affiche le contenu texte brut de toute image prise en charge directement dans la console.

## Ce que vous allez apprendre

- Comment configurer Aspose.OCR pour le traitement hors ligne.  
- Le code exact pour **charger une image pour l'OCR** depuis le disque.  
- Comment configurer le moteur pour **reconnaître le texte cyrillique**.  
- Un **exemple c# ocr** complet, prêt à copier‑coller, qui extrait le texte d'une photo de type passeport.  

Aucune expérience préalable avec Aspose n'est requise ; un SDK .NET 6 (ou supérieur) et Visual Studio 2022 (ou VS Code) suffisent.

---

![Extraire du texte d'une image avec Aspose OCR sur une photo de passeport](/images/ocr-passport.jpg "extraire du texte d'une image")

## Étape 1 : Configurer le projet pour extraire du texte d'une image

Avant d'écrire du code, assurez-vous que le package NuGet Aspose.OCR est ajouté à votre projet :

```bash
dotnet add package Aspose.OCR
```

> **Astuce :** Utilisez le drapeau `--version` pour verrouiller la dernière version stable (par ex., `13.9.0`). Cela garantit la compatibilité avec .NET 6.

Créer une nouvelle application console est aussi simple que :

```bash
dotnet new console -n OfflineOcrDemo
cd OfflineOcrDemo
```

Vous avez maintenant une base vierge où nous allons **extraire du texte d'une image** sans jamais toucher à Internet.

## Étape 2 : Charger l'image pour l'OCR – Lecture de la photo de passeport

La première chose dont le moteur OCR a besoin est un bitmap ou un flux représentant l'image. Dans notre scénario, nous allons **charger une image pour l'OCR** depuis un fichier local nommé `cyrillic_passport.jpg`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

// Step 2: Load the image file (this is the “load image for ocr” part)
var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

// Validate the file exists – helpful when the path is wrong.
if (!System.IO.File.Exists(imagePath))
{
    Console.WriteLine($"❌ Image not found at {imagePath}");
    return;
}

// ImageStream abstracts the underlying format; it works with JPEG, PNG, etc.
var image = ImageStream.FromFile(imagePath);
```

> **Pourquoi c'est important :** Fournir un flux plutôt qu'un `Bitmap` brut permet à Aspose de gérer la détection du format en interne, réduisant le code boilerplate et les bugs potentiels.

## Étape 3 : Configurer le mode hors ligne et choisir la langue cyrillique

Aspose.OCR peut télécharger des modèles de langue à la volée, mais cela va à l'encontre de l'objectif d'une solution hors ligne. Désactivez les appels réseau et indiquez explicitement au moteur la langue à utiliser.

```csharp
// Step 3: Create the OCR engine and switch to offline mode
var ocrEngine = new OcrEngine
{
    Configuration =
    {
        OfflineMode = true,               // No network traffic – perfect for secure environments
        Language = new[] { OcrLanguage.Cyrillic } // We want to **recognize cyrillic text**
    }
};
```

> **Cas particulier :** Si vous devez plus tard reconnaître des caractères latins dans le même document, ajoutez simplement `OcrLanguage.English` au tableau. Le moteur gérera automatiquement la détection multilingue.

## Étape 4 : Exécuter le moteur OCR et reconnaître le texte cyrillique

Nous allons maintenant réellement **reconnaître le texte d'images de type passeport**. La méthode `Recognize` renvoie un objet résultat riche contenant le texte brut, les scores de confiance et les boîtes englobantes.

```csharp
// Step 4: Perform the OCR operation
OcrResult result = ocrEngine.Recognize(image);

// Step 5: Output the plain text – this is where we finally **extract text from image**
Console.WriteLine("📝 Extracted Text:");
Console.WriteLine("-------------------");
Console.WriteLine(result.PlainText);
```

### Sortie console attendue

```
📝 Extracted Text:
-------------------
ПАСПОРТ РФ
Иванов Иван Иванович
01.01.1990
...
```

Si le résultat apparaît brouillé, vérifiez que l'image source est claire et que le pack de langue `OfflineMode` pour le cyrillique est présent dans le dossier d'installation d'Aspose (généralement `\Aspose.OCR\resources\languages`).

## Exemple complet C# OCR – Code source complet

Voici le **exemple c# ocr** dans son intégralité. Copiez‑collez‑le dans `Program.cs` et exécutez `dotnet run`. Tout ce dont vous avez besoin pour **extraire du texte d'une image** se trouve ici.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class OfflineExample
{
    static void Main()
    {
        // --------------------------------------------------------------
        // Step 1: Create the OCR engine (offline mode)
        // --------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Configuration =
            {
                OfflineMode = true,                     // No network calls
                Language = new[] { OcrLanguage.Cyrillic } // Recognize Cyrillic text
            }
        };

        // --------------------------------------------------------------
        // Step 2: Load the image for OCR (passport photo)
        // --------------------------------------------------------------
        var imagePath = @"YOUR_DIRECTORY\cyrillic_passport.jpg";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"❌ Image not found at {imagePath}");
            return;
        }

        var image = ImageStream.FromFile(imagePath);

        // --------------------------------------------------------------
        // Step 3: Recognize the text
        // --------------------------------------------------------------
        var result = ocrEngine.Recognize(image);

        // --------------------------------------------------------------
        // Step 4: Output the plain text (the final extraction)
        // --------------------------------------------------------------
        Console.WriteLine("📝 Extracted Text:");
        Console.WriteLine("-------------------");
        Console.WriteLine(result.PlainText);
    }
}
```

### Exécution de l'exemple

```bash
dotnet run
```

Vous devriez voir la console afficher les détails du passeport en cyrillique. C'est le moment où vous savez que votre pipeline d'**extraction de texte d'image** fonctionne.

## Problèmes courants et comment les résoudre

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `PlainText` vide | Modèle de langue incorrect ou image trop sombre | Assurez-vous que le pack de langue `OfflineMode` inclut `Cyrillic` et augmentez le contraste de l'image |
| `System.DllNotFoundException` | Binaires natifs Aspose OCR manquants | Réinstallez le package NuGet ou copiez le `Aspose.OCR.Native.dll` dans le dossier de sortie |
| Performance lente sur les grandes images | Le moteur traite la résolution complète | Redimensionnez l'image à ≤ 1500 px de largeur avant de la fournir à `ImageStream` |
| Caractères brouillés | Image mal orientée | Utilisez `Image.RotateFlip(RotateFlipType.Rotate90FlipNone)` avant de créer le flux |

## Prochaines étapes – Étendre le flux de travail OCR hors ligne

- **Charger une image pour l'OCR** depuis un `MemoryStream` lors du traitement de fichiers téléchargés dans ASP.NET Core.  
- Passer à **reconnaître le texte d'un passeport** en mode batch en parcourant un dossier de scans de passeports.  
- Combiner le résultat avec des **expressions régulières** pour extraire des champs comme le numéro de passeport ou la date de naissance.  
- Expérimentez avec `ocrEngine.Configuration.UseParallelProcessing = true` pour des gains de vitesse multi‑cœurs.

---

### Conclusion

Nous venons de vous montrer comment **extraire du texte d'une image** en utilisant un pipeline OCR C# entièrement hors ligne. Le **exemple c# ocr** court et autonome charge une image, configure le moteur pour **reconnaître le texte cyrillique**, et imprime les données du passeport extraites — le tout sans aucune requête réseau.

N'hésitez pas à ajuster le code, ajouter d'autres langues, ou connecter la sortie à une base de données. Le ciel est la limite une fois que vous avez maîtrisé les bases du chargement d'une image pour l'OCR et de la reconnaissance de texte d'une photo de type passeport.

Des questions ou envie de partager vos propres ajustements ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}