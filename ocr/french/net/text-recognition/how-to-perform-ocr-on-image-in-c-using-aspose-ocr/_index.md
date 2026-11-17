---
category: general
date: 2026-10-11
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) sur
  une image en C# avec Aspose.OCR, y compris l'installation de System.Drawing.Common
  et l'extraction du texte à partir de fichiers JPG.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- recognize text from picture
- load image for OCR
- install System.Drawing.Common package
language: fr
lastmod: 2026-10-11
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  en C# avec Aspose.OCR. Ce guide vous montre comment installer System.Drawing.Common,
  charger une image pour l'OCR et extraire le texte d'un JPG.
og_image_alt: Screenshot of C# console output displaying recognized text after performing
  OCR on image
og_title: Effectuer la reconnaissance optique de caractères (OCR) sur une image en
  C# – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on image in C# with Aspose.OCR, including
    installing System.Drawing.Common and extracting text from JPG files.
  headline: How to perform OCR on image in C# using Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose
title: Comment effectuer l'OCR sur une image en C# avec Aspose.OCR
url: /fr/net/text-recognition/how-to-perform-ocr-on-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR sur une image en C# avec Aspose.OCR

Si vous devez **effectuer une OCR sur une image** dans une application .NET, ce guide vous présente une solution complète. En utilisant Aspose.OCR, vous pouvez rapidement **reconnaître du texte à partir d'une image** tels que les fichiers JPG et afficher le résultat dans une fenêtre de console.

Vous apprendrez comment :

* **install System.Drawing.Common package** – la bibliothèque qui fournit la classe `Image`,
* **load image for OCR** – lire un JPEG ou PNG en mémoire,
* configurer le modèle de langue,
* **perform OCR on image** et enfin,
* **extract text from JPG** et l'afficher.

Les étapes sont rédigées pour .NET 6+, mais elles fonctionnent également avec .NET Framework 4.6.1 ou ultérieur.

---

## Prérequis

| Exigence | Pourquoi c'est important |
|-------------|----------------|
| .NET 6 SDK (or .NET Framework 4.6.1+) | Fournit le runtime pour l'application console C#. |
| Visual Studio 2022 (or any IDE) | Facilite l'ajout de packages NuGet et l'exécution du programme. |
| Internet connection (first run only) | Aspose.OCR télécharge automatiquement le module de langue. |
| A sample image containing Cyrillic or Latin text (e.g., `sample_cyrillic.jpg`) | Utilisée pour démontrer **extraire du texte d'un JPG**. |

---

## Étape 1 : Installer le package System.Drawing.Common

Le package NuGet `System.Drawing.Common` fournit la classe `Image` que vous utiliserez pour **charger une image pour l'OCR**. Ouvrez la console du gestionnaire de packages et exécutez :

```powershell
Install-Package System.Drawing.Common
```

> **Conseil :** Ciblez `net6.0-windows` ou ajoutez `<UseWindowsForms>true</UseWindowsForms>` au fichier de projet si vous rencontrez des avertissements spécifiques à la plateforme sous Linux/macOS.

---

## Étape 2 : Ajouter le package NuGet Aspose.OCR

Aspose.OCR contient le moteur OCR et les modèles de langue. Installez-le avec :

```powershell
Install-Package Aspose.OCR
```

Le package est léger ; les données de langue requises (par ex., le cyrillique) sont téléchargées la première fois que vous définissez `OcrEngine.Language`.

---

## Étape 3 : Comment charger une image pour l'OCR

Charger l'image est la première étape concrète avant de pouvoir **effectuer une OCR sur une image**. La méthode `Image.FromFile` lit tout format pris en charge par GDI+, y compris JPG, PNG, BMP et TIFF.

```csharp
using System.Drawing; // Requires System.Drawing.Common

// Replace the path with the location of your test picture.
string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
Image ocrImage = Image.FromFile(imagePath);
```

*Si le fichier n'existe pas, une `FileNotFoundException` est levée – encapsulez l'appel dans un bloc try/catch pour le code de production.*

---

## Étape 4 : Configurer le moteur et **effectuer une OCR sur une image**

Créez une instance `OcrEngine`, sélectionnez le modèle de langue, assignez l'image chargée, puis appelez `Recognize()`.

```csharp
using Aspose.OCR;

// Step 4: Initialize OCR engine and set language
var ocrEngine = new OcrEngine
{
    // Choose the language you need; Cyrillic is used in this example.
    Language = OcrLanguage.Cyrillic,
    Image = ocrImage
};

// Execute the OCR operation
OcrResult ocrResult = ocrEngine.Recognize();
```

La méthode `Recognize()` renvoie un objet `OcrResult` qui contient le texte extrait, les scores de confiance et les boîtes englobantes. Le module de langue est téléchargé automatiquement lors de la première utilisation, aucune fichier supplémentaire n'est requis.

---

## Étape 5 : **Extraire du texte d'un JPG** et l'afficher

Vous pouvez maintenant **reconnaître du texte à partir d'une image** et afficher le résultat. La propriété `Text` de `OcrResult` contient la chaîne brute.

```csharp
// Step 5: Output recognized text
Console.WriteLine("Recognized text:");
Console.WriteLine(ocrResult.Text);
```

### Sortie console attendue

```
Recognized text:
Пример текста на кириллице
```

Si l'image source contient du texte anglais, la sortie sera la phrase anglaise que vous avez placée dans l'image.

---

## Cas limites et conseils de bonnes pratiques

| Situation | Recommendation |
|-----------|----------------|
| **Large images ( > 5 MB )** | Redimensionnez l'image à ≤ 2000 px sur le côté le plus long avant l'OCR pour réduire la consommation de mémoire et améliorer la vitesse. |
| **Multiple languages in one picture** | Appelez `ocrEngine.AddLanguage(OcrLanguage.English)` en plus du cyrillique, puis définissez `ocrEngine.Language = OcrLanguage.Multilingual`. |
| **Low‑contrast scans** | Augmentez le contraste avec `System.Drawing.Graphics` avant de transmettre le bitmap au moteur. |
| **Running on Linux/macOS** | Assurez‑vous que la dépendance native `libgdiplus` est installée (`sudo apt-get install -y libgdiplus`). |
| **Repeated OCR calls** | Réutilisez la même instance `OcrEngine` et ne remplacez que `ocrEngine.Image` afin d'éviter le rechargement répété du module. |

---

## Programme complet, exécutable

Voici l'application console complète qui intègre toutes les étapes précédentes. Copiez le code dans un nouveau projet console C#, remplacez le chemin de l'image, puis exécutez‑le.

```csharp
using System;
using System.Drawing;                 // Install System.Drawing.Common if needed
using Aspose.OCR;                     // NuGet package: Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Install System.Drawing.Common (handled via NuGet)
        // Step 2: Install Aspose.OCR (handled via NuGet)

        // Step 3: Load the image that contains the text to be recognized
        // Replace the placeholder with the actual path to your JPG or PNG file.
        string imagePath = @"YOUR_DIRECTORY/sample_cyrillic.jpg";
        Image ocrImage;
        try
        {
            ocrImage = Image.FromFile(imagePath);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Failed to load image: {ex.Message}");
            return;
        }

        // Step 4: Create the OCR engine and choose the language model
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.Cyrillic, // Change to OcrLanguage.English for Latin scripts
            Image = ocrImage
        };

        // Step 5: Perform OCR on the loaded picture
        OcrResult ocrResult = ocrEngine.Recognize();

        // Step 6: Display the extracted text
        Console.WriteLine("Recognized text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Exécuter le programme** affiche la chaîne reconnue dans la console, confirmant que vous avez réussi à **effectuer une OCR sur une image** et à **extraire du texte d'un JPG**.

---

## Conclusion

Vous savez maintenant comment **effectuer une OCR sur des fichiers image** en C# avec Aspose.OCR, depuis l'installation du **package System.Drawing.Common** requis jusqu'à **charger une image pour l'OCR**, sélectionner la langue appropriée, et enfin **extraire du texte d'un JPG**. Cet exemple complet vous fournit une base solide pour créer des pipelines de traitement de documents plus avancés, comme le traitement par lots de dossiers d'images ou l'intégration de l'OCR dans une API web.

### Et après ?

* Explorez **reconnaître du texte à partir d'une image** dans les PDF en convertissant chaque page en image d'abord.
* Expérimentez avec les propriétés `Resolution`, `Threshold` et `MaxProcessingTime` de `OcrEngine` pour affiner la précision sur des scans bruités.
* Combinez la sortie OCR avec une bibliothèque de traitement du langage naturel pour catégoriser automatiquement le contenu extrait.

N'hésitez pas à adapter le code à d'autres formats d'image, ajouter la gestion des erreurs, ou l'intégrer à des applications plus importantes. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire du texte d'une image en C# – Guide complet Aspose OCR](/ocr/english/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/)
- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Comment extraire du texte d'image depuis un flux avec Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}