---
category: general
date: 2026-10-18
description: Effectuez rapidement la reconnaissance optique de caractères (OCR) sur
  une image en C#. Apprenez à extraire du texte à partir d’un JPG, à convertir une
  image en texte et à lire le texte d’une image en utilisant Aspose.OCR.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- perform OCR on image
- extract text from JPG
- convert image to text
- read text from image
- load image for OCR
language: fr
lastmod: 2026-10-18
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  en C# avec Aspose.OCR. Ce tutoriel montre comment extraire du texte d’un JPG, convertir
  une image en texte et lire le texte d’une image en quelques minutes.
og_image_alt: Console output displaying recognized Cyrillic text after performing
  OCR on an image
og_title: Effectuer l'OCR sur une image en C# – guide complet
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Perform OCR on an image in C# quickly. Learn to extract text from JPG,
    convert image to text and read text from image using Aspose.OCR.
  headline: How to perform OCR on an image in C# with Aspose.OCR
  type: TechArticle
tags:
- OCR
- C#
- Aspose.OCR
title: Comment effectuer l'OCR sur une image en C# avec Aspose.OCR
url: /fr/net/text-recognition/how-to-perform-ocr-on-an-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR sur une image en C# avec Aspose.OCR

Si vous devez **effectuer une OCR sur une image** dans une application .NET, ce guide vous montre une solution complète, prête à l’emploi. Vous verrez comment **charger une image pour l'OCR**, reconnaître les caractères cyrilliques, et **extraire du texte d'un JPG** sans écrire de code de traitement d'image de bas niveau.

Dans ce tutoriel vous allez :

* Installer le package NuGet Aspose.OCR.  
* Charger un fichier image (JPG, PNG, BMP, etc.).  
* Exécuter le moteur OCR pour **convertir l'image en texte**.  
* **Lire le texte de l'image** dans la console.  

Les étapes fonctionnent avec n'importe quelle image compatible .NET, vous pouvez donc les adapter aux PDF, aux reçus numérisés ou aux captures d'écran.

## Prérequis

* .NET 6.0 SDK ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+).  
* Visual Studio 2022 ou tout éditeur C# de votre choix.  
* Accès à Internet lors du premier lancement – Aspose.OCR télécharge automatiquement le module de langue cyrillique.  

> **Astuce :** Gardez le package NuGet à jour ; les versions plus récentes améliorent la précision de reconnaissance et ajoutent des packs de langues.

## Étape 1 : Installer Aspose.OCR

Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Le package contient la classe `OcrEngine` utilisée pour **effectuer une OCR sur des fichiers image**. Après l'exécution de la commande, la référence du package apparaît dans votre fichier *.csproj*.

## Étape 2 : Créer une structure de programme console

Créez un nouveau projet console si vous n'en avez pas déjà un :

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

Remplacez le *Program.cs* généré par le code présenté dans les sections suivantes. La structure comprend les directives `using` requises et une méthode `Main` qui pilote le processus OCR.

## Étape 3 : Charger une image pour l'OCR

La première ligne fonctionnelle du code **charge l'image** que vous souhaitez analyser. Aspose.OCR accepte n'importe quel flux, vous pouvez donc charger un fichier depuis le disque, une URL web ou une ressource intégrée.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Step 3: Load the image containing Cyrillic text
        // Replace the path with the location of your JPG file.
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);
```

*Pourquoi c'est important* : L'utilisation de `ImageStream.FromFile` abstrait la gestion des formats, garantissant que le moteur OCR reçoit un bitmap cohérent quel que soit le type de fichier d'origine. Elle libère également le flux automatiquement grâce à l'instruction `using`.

## Étape 4 : Initialiser le moteur OCR et définir la langue (optionnel)

Par défaut, Aspose.OCR tente de détecter la langue automatiquement. Pour du texte cyrillique, vous pouvez demander explicitement le module `Language.Cyrillic`, ce qui accélère le téléchargement initial.

```csharp
        // Step 4: Initialize the OCR engine
        var engine = new OcrEngine();

        // Optional: force Cyrillic language to avoid auto‑detection overhead
        engine.Language = Language.Cyrillic;
```

Si vous omettez l'affectation de la langue, le moteur téléchargera le module nécessaire la première fois que vous appellerez `Recognize`. Le téléchargement s'effectue via HTTPS et est mis en cache localement pour les exécutions suivantes.

## Étape 5 : Effectuer l'OCR et convertir l'image en texte

Vous **effectuez maintenant l'OCR sur l'image** et obtenez une chaîne de texte brut. La méthode `Recognize` effectue tout le travail lourd : prétraitement, analyse de mise en page et classification des caractères.

```csharp
        // Step 5: Perform OCR – convert image to text
        engine.Image = image;
        string recognizedText = engine.Recognize();
```

Le `recognizedText` retourné contient des sauts de ligne qui correspondent à la mise en page originale, facilitant le post‑traitement ou le stockage dans une base de données.

## Étape 6 : Afficher le résultat – lire le texte de l'image

Enfin, **lisez le texte de l'image** en écrivant le résultat dans la console. Cette étape vérifie que l'OCR a réussi et vous montre exactement ce qui a été extrait.

```csharp
        // Step 6: Display the recognized text – read text from image
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

Lorsque vous exécutez le programme (`dotnet run`), vous devriez voir une sortie similaire à :

```
=== OCR Result ===
Пример текста на кириллице
```

> **Remarque :** La sortie exacte dépend de la qualité du JPG source. Des images claires et haute résolution donnent les meilleurs résultats.

## Code source complet et exécutable

Ci-dessous le programme complet que vous pouvez copier‑coller dans *Program.cs* et exécuter sans modifications (à l'exception du chemin de l'image).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

class Program
{
    static void Main()
    {
        // Load the image containing Cyrillic text
        string imagePath = @"YOUR_DIRECTORY\cyrillic-sample.jpg";
        using var image = ImageStream.FromFile(imagePath);

        // Initialize the OCR engine
        var engine = new OcrEngine
        {
            // Force Cyrillic language; optional but speeds up first run
            Language = Language.Cyrillic,
            Image = image
        };

        // Recognize the text – this converts the image to text
        string recognizedText = engine.Recognize();

        // Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

L'exécution du programme affiche les caractères extraits dans la console, prouvant que vous avez réussi à **extraire du texte d'un JPG** et à **convertir l'image en texte**.

## Gestion des variations courantes

| Scénario | Ajustement |
|----------|------------|
| **Langue différente** | Définissez `engine.Language = Language.English;` ou un autre enum pris en charge. |
| **PDF multi‑pages** | Convertissez chaque page en image (par ex., avec `Aspose.PDF`) et appelez la boucle OCR pour chaque image. |
| **Lot important** | Enveloppez l'appel OCR dans une boucle `Parallel.ForEach` ; réutilisez une seule instance `OcrEngine` pour réduire la consommation de mémoire. |
| **Image basse résolution** | Pré‑traitez avec `engine.Image = ImageProcessing.Filters.GaussianBlur(image, 1.5);` pour réduire le bruit avant la reconnaissance. |

Ces variations vous permettent de **extraire du texte d'un JPG** quel que soit la langue, la taille ou la qualité.

## Conseils de performance

* **Mettre en cache les modules de langue** – le premier téléchargement peut prendre quelques secondes ; les exécutions suivantes sont instantanées. |
* **Réutiliser l'instance `OcrEngine`** pour plusieurs images afin d'éviter les coûts d'initialisation répétés. |
* **Limiter la taille de l'image** – les photos extrêmement grandes augmentent l'utilisation de mémoire. Redimensionnez à un maximum de 2000 px en largeur avant de les fournir au moteur.

## Conclusion

Vous savez maintenant comment **effectuer une OCR sur des fichiers image** en C# avec Aspose.OCR. En chargeant une image, en configurant le moteur et en appelant `Recognize`, vous pouvez **extraire du texte d'un JPG**, **convertir l'image en texte**, et **lire le texte de l'image** avec seulement quelques lignes de code.  

À partir d'ici, vous pourriez explorer :

* Stocker les résultats OCR dans une base de données pour des archives consultables.  
* Intégrer le flux de travail dans une API web qui accepte les images téléchargées.  
* Utiliser d'autres modules de langue (arabe, hindi, etc.) pour élargir la portée de votre application.

N'hésitez pas à expérimenter avec différents formats d'image, langues et stratégies de traitement par lots. Le modèle de base — **charger une image pour l'OCR → reconnaître → gérer la sortie texte brut** — reste le même, vous offrant une base solide pour tout projet d'extraction de texte.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et à explorer des approches d'implémentation alternatives dans vos propres projets.

- [Extraire le texte d'une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Convertir une image en texte – Effectuer l'OCR sur une image depuis une URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)
- [Comment extraire du texte d'une image en utilisant Aspose.OCR pour .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}