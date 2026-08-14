---
category: general
date: 2026-02-20
description: Reconnaissez rapidement le texte d’une image grâce à l’accélération GPU
  d’Aspose OCR. Apprenez comment extraire le texte d’un scan en C# avec un exemple
  complet et exécutable.
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: fr
og_description: Reconnaître du texte à partir d'une image avec accélération GPU. Ce
  tutoriel vous montre comment extraire du texte d'un scan en C# à l'aide d'Aspose
  OCR, avec le code complet et des astuces.
og_title: Reconnaître le texte à partir d'une image avec Aspose OCR GPU – Guide C#
tags:
- Aspose
- OCR
- C#
- GPU
title: Reconnaître le texte d’une image en utilisant Aspose OCR GPU en C#
url: /fr/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

content.

Be careful with French punctuation: use spaces before colon? Not necessary.

Let's translate.

Start with shortcodes unchanged.

Proceed.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir d'une image avec Aspose OCR GPU en C#

Vous avez déjà eu besoin de **reconnaître du texte à partir d'une image** mais le fichier était énorme et votre CPU n’en pouvait plus ? Peut‑être avez‑vous essayé une bibliothèque OCR basique et cela a pris une éternité, ou les résultats étaient médiocres. La bonne nouvelle ? Avec l’accélération GPU d’Aspose OCR, vous pouvez transformer un TIFF numérisé massif en texte propre et interrogeable en quelques secondes.

Dans ce guide, nous allons parcourir un exemple complet, prêt à copier‑coller, qui montre comment **extraire du texte d’un fichier scanné** sur une machine équipée de GPU. Pas de références vagues, juste le code dont vous avez besoin, pourquoi chaque ligne est importante, et quelques pièges à éviter pour ne pas perdre vos cheveux.

## Ce dont vous aurez besoin

- **.NET 6+** (ou .NET Framework 4.7+ – l’API fonctionne de la même façon)
- **Aspose.OCR for .NET** package NuGet (version 23.12 ou supérieure)
- Un **GPU** avec support CUDA (optionnel, mais nettement plus rapide)
- Une image scannée haute résolution (par ex., `large_doc.tif`)

Si vous n’avez pas de GPU, le moteur reviendra automatiquement sur le CPU — vous pourrez donc toujours exécuter l’exemple, simplement un peu plus lentement.

## Étape 1 – Installer le package Aspose.OCR

Ouvrez votre terminal ou la console du Gestionnaire de packages et exécutez :

```bash
dotnet add package Aspose.OCR
```

Ou, dans l’interface NuGet de Visual Studio, recherchez **Aspose.OCR** et cliquez sur *Install*. Cela récupère la bibliothèque OCR principale ainsi que l’assembly d’accélération GPU optionnel.

> **Astuce pro :** Après l’installation, vérifiez le dossier `packages` pour `Aspose.OCR.Acceleration.dll`. Il est requis pour le support GPU ; si vous êtes sur un serveur sans affichage, vous pouvez l’ignorer et le code compilera quand même.

## Étape 2 – Initialiser le moteur OCR accéléré par GPU

La classe `GpuOcrEngine` détecte automatiquement tout GPU compatible. Si vous avez plusieurs appareils, vous pouvez en choisir un spécifique, mais la plupart des développeurs laissent le moteur choisir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**Pourquoi c’est important :** Initialiser le moteur GPU une seule fois réduit la surcharge. Si vous créez et détruisez le moteur à chaque itération d’une boucle, vous perdrez les gains de performance.

## Étape 3 – Charger votre image scannée haute résolution

Aspose OCR travaille avec `System.Drawing.Image`. Assurez‑vous que le chemin du fichier pointe vers une vraie image ; sinon vous obtiendrez une `FileNotFoundException`.

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **Cas limite :** Si l’image dépasse 10 000 × 10 000 px, pensez à la réduire d’abord. La mémoire du GPU est limitée, et charger un bitmap massif peut provoquer une `OutOfMemoryException`.

## Étape 4 – Effectuer l’OCR avec les paramètres de langue par défaut (Latin)

La méthode `Recognize` renvoie une chaîne brute. Vous pouvez passer un objet `OcrOptions` si vous avez besoin d’une autre langue ou d’un pré‑traitement personnalisé.

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**Pourquoi le réglage par défaut fonctionne :** La plupart des documents scannés — contrats, factures, rapports—utilisent des alphabets basés sur le latin. Si vous avez besoin du cyrillique, de l’arabe ou du chinois, définissez `ocrEngine.Language = "ru"` (ou le code ISO approprié) avant d’appeler `Recognize`.

## Étape 5 – Afficher ou persister le texte extrait

Pour une vérification rapide, nous allons simplement écrire le résultat dans la console. Dans une vraie application, vous pourriez enregistrer dans une base de données, un fichier `.txt`, ou l’alimenter à un index de recherche.

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### Résultat attendu

Si `large_doc.tif` contient un paragraphe simple comme « Hello, world! », vous verrez :

```
Hello, world!
```

Pour des scans multi‑pages, le moteur concatène le texte dans l’ordre de lecture. Vous pouvez le scinder plus tard en utilisant les sauts de ligne (`\n`) si vous avez besoin de délimiter les pages.

## Gestion des pièges courants

| Problème | Symptom | Solution |
|----------|---------|----------|
| **Aucun GPU détecté** | `ocrEngine.Device` est `null` et le traitement est lent. | Installez le dernier pilote NVIDIA et le CUDA Toolkit (v11+). Vérifiez avec `nvidia-smi`. |
| **Retards du ramasse‑miettes** | Pics de mémoire après le traitement de nombreuses images. | Appelez `scannedImage.Dispose()` après l’OCR, ou encapsulez l’image dans un bloc `using`. |
| **Mauvaise langue** | Caractères illisibles pour du texte non latin. | Définissez `ocrEngine.Language` au bon code ISO 639‑1 avant `Recognize`. |
| **Fichiers très volumineux** | `OutOfMemoryException`. | Réduisez avec `Image.GetThumbnailImage` ou découpez le scan en tuiles. |

## Exemple complet, prêt à l’emploi

Voici le programme complet — incluant les directives `using`, la gestion des erreurs, et un bloc `using` propre pour l’image :

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### Ce que fait ce code

1. **Crée** un `GpuOcrEngine` qui sélectionne automatiquement le meilleur GPU.  
2. **Charge** le TIFF cible dans un bloc `using` afin de garantir sa libération.  
3. **Appelle** `Recognize` pour convertir le bitmap en chaîne de caractères.  
4. **Écrit** le résultat à la fois dans la console et dans un fichier `.txt` à côté de l’image source.  
5. **Capture** toute exception et affiche un message d’erreur convivial.

## Aller plus loin – De « reconnaître du texte à partir d’une image » à des pipelines documentaires complets

Maintenant que vous pouvez **extraire du texte d’un fichier scanné**, pensez aux étapes suivantes :

- **Traitement par lots** : parcourez un dossier de TIFF et agrégerez les résultats dans un index interrogeable unique.  
- **Détection de langue** : utilisez `ocrEngine.DetectLanguage()` (si disponible) pour basculer automatiquement de langue.  
- **Post‑traitement** : passez la sortie dans un correcteur orthographique ou un filtre regex pour nettoyer les artefacts OCR.  
- **Intégration avec Azure Cognitive Search** : poussez le texte extrait dans un index cloud searchable pour une recherche instantanée.

Chacune de ces étapes s’appuie sur le même modèle de base que vous venez de voir — initialiser une fois, fournir les images, récupérer le texte.

## Conclusion

Vous venez d’apprendre comment **reconnaître du texte à partir d’une image** en utilisant le moteur GPU‑accéléré d’Aspose OCR en C#. L’exemple complet et exécutable montre comment configurer le moteur, charger un scan haute résolution, exécuter l’OCR et gérer la sortie. En suivant les conseils et la gestion des cas limites présentés, vous éviterez les pièges courants et obtiendrez des résultats fiables, que vous soyez sur un ordinateur de développeur ou sur un serveur de production.

Prêt à transformer davantage de scans en données interrogeables ? Essayez de traiter tout un dossier, expérimentez avec des langues non latines, ou alimentez les résultats dans un moteur de recherche plein texte. Le ciel est la limite, et le code que vous venez d’écrire constitue la base solide dont vous avez besoin.

Bon codage ! 🚀

![recognize text from image example](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}