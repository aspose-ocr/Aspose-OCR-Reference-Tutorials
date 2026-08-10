---
category: general
date: 2026-02-13
description: Apprenez à utiliser l'OCR en C# pour extraire du texte à partir de fichiers
  image, activer le traitement GPU et convertir rapidement les numérisations en texte.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: fr
og_description: Comment utiliser l'OCR en C# ? Ce guide vous montre comment extraire
  du texte à partir de fichiers image, activer le traitement GPU et convertir les
  numérisations en texte.
og_title: Comment utiliser l'OCR en C# – Extraire du texte d'images avec le GPU
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: Comment utiliser l'OCR en C# – Extraire du texte d'images avec le GPU
url: /fr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en C# – Extraire du texte d'images avec le GPU

Vous vous êtes déjà demandé **comment utiliser l'OCR** pour extraire du texte d’un document numérisé sans effort ? Vous n’êtes pas seul — les développeurs demandent constamment : « Comment extraire du texte d’un fichier image de façon efficace ? » Bonne nouvelle, avec Aspose.OCR vous pouvez faire exactement cela, et même **activer le traitement GPU** pour un gain de vitesse notable sur le matériel compatible.

Dans ce tutoriel, nous parcourrons un exemple complet, de bout en bout, qui vous montre **comment utiliser l'OCR**, comment **extraire du texte d’une image**, comment **convertir une numérisation en texte**, et que faire si le GPU n’est pas disponible. À la fin, vous disposerez d’une application console C# prête à l’emploi qui affiche le texte reconnu et indique si le GPU a réellement été utilisé.

## Ce dont vous avez besoin

- SDK .NET 6 ou version ultérieure (le code fonctionne également avec .NET Core)  
- Visual Studio 2022 ou tout autre éditeur de votre choix  
- Package Aspose.OCR pour .NET (disponible via NuGet)  
- Un fichier image haute résolution (par ex. `highres_scan.tif`) pour les tests  

Aucune configuration compliquée requise — juste quelques commandes NuGet et vous êtes prêt.

## Étape 1 : Installer Aspose.OCR et préparer le projet

Première chose à faire. Vous devez ajouter la bibliothèque OCR à votre projet. Ouvrez un terminal dans le dossier de votre solution et exécutez :

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Cela crée un nouveau projet console nommé **OcrDemo** et ajoute le package NuGet `Aspose.OCR`. La bibliothèque contient la classe `OcrEngine` que nous utiliserons.

> **Astuce :** Si vous êtes sur une machine disposant d’un GPU dédié, assurez‑vous que le pilote graphique le plus récent est installé ; sinon la bibliothèque reviendra automatiquement en mode CPU.

## Étape 2 : Écrire le code OCR complet

Ouvrez maintenant `Program.cs` et remplacez son contenu par ce qui suit. Chaque ligne est commentée afin que vous puissiez comprendre *pourquoi* nous faisons ce que nous faisons.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Pourquoi cela fonctionne

- **ProcessingMode = Gpu** indique au moteur d’essayer d’abord le GPU. La bibliothèque masque les appels bas‑niveau CUDA/OpenCL, vous n’avez donc pas besoin de gérer les contextes de périphérique vous‑même.  
- **IsGpuEnabled** est un booléen qui confirme si le chemin GPU a réussi. Si vous voyez `false`, le moteur est revenu automatiquement au CPU — pas de panique.  
- **RecognizeImage** fait tout le travail lourd : il charge l’image, exécute le modèle OCR et renvoie le résultat texte brut. Aucun pré‑traitement manuel du bitmap n’est nécessaire sauf si vous avez des exigences particulières (par ex. redressement).

## Étape 3 : Exécuter l’application et vérifier la sortie

Compilez et lancez :

```bash
dotnet run
```

Si tout est correctement configuré, vous verrez quelque chose comme :

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

Si le GPU n’est pas disponible, la première ligne affichera `GPU used: False`, mais le texte extrait apparaîtra quand même — grâce au basculement élégant.

> **Question fréquente :** *Et si mon image est un JPEG au lieu d’un TIFF ?*  
> La méthode `RecognizeImage` accepte tout format supporté par `System.Drawing` de .NET (JPEG, PNG, BMP, etc.). Il suffit de changer l’extension du fichier dans `imagePath`.

## Étape 4 : Optionnel – Ajuster les paramètres pour plus de précision

Aspose.OCR propose quelques réglages que vous pouvez modifier :

| Paramètre | Ce qu'il fait | Quand l'utiliser |
|-----------|---------------|------------------|
| `ocrEngine.Language` | Force une langue spécifique (ex. `OcrLanguage.English`) | Si vous connaissez la langue du document |
| `ocrEngine.PageSegMode` | Contrôle la façon dont le moteur divise les pages en blocs | Pour les mises en page à colonnes multiples |
| `ocrEngine.DetectOrientation` | Rotation automatique du texte qui n’est pas à l’endroit | Scans pouvant être à l’envers |

Vous pouvez définir ces propriétés avant d’appeler `RecognizeImage`. Par exemple :

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Étape 5 : Visualiser le flux (Image avec texte alternatif)

Voici un diagramme simple qui illustre **comment utiliser l'OCR** avec l’accélération GPU optionnelle. Ce n’est pas indispensable au fonctionnement du code, mais cela aide à voir la vue d’ensemble.

![Diagram showing how to use OCR with GPU processing](/images/ocr-gpu-flow.png)

*Texte alternatif :* *Diagramme montrant comment utiliser l'OCR avec le traitement GPU, en soulignant le basculement vers le CPU si nécessaire.*

## Cas limites et dépannage

1. **Out‑of‑Memory sur le GPU** – Les images très volumineuses peuvent dépasser la mémoire du GPU. Dans ce cas, la bibliothèque revient automatiquement au CPU. Vous pouvez pré‑redimensionner l’image pour limiter l’usage mémoire.  
2. **Format d’image non supporté** – Si `RecognizeImage` lève une *NotSupportedException*, vérifiez l’extension du fichier et assurez‑vous que l’image n’est pas corrompue. La conversion en PNG résout souvent le problème.  
3. **Scores de confiance faibles** – Lorsque le résultat OCR contient de nombreux caractères illisibles, envisagez un pré‑traitement (binarisation, suppression du bruit) ou passez à une numérisation de résolution supérieure.  

## Conclusion : Ce que nous avons accompli

Nous venons de couvrir **comment utiliser l'OCR** dans une application console C#, démontré comment **extraire du texte d’une image**, et montré comment **activer le traitement GPU** pour des résultats plus rapides. Vous savez maintenant comment **convertir une numérisation en texte**, vérifier si le GPU a réellement été employé, et ajuster quelques paramètres pour les scénarios limites.

### Prochaines étapes

- Essayez d’alimenter la sortie dans un **index de recherche** (par ex. Elasticsearch) afin que vos PDF numérisés deviennent recherchables.  
- Expérimentez avec le **traitement par lots** — bouclez sur un dossier d’images et écrivez chaque résultat dans un fichier `.txt`.  
- Combinez l’OCR avec des **API de traduction** pour traduire automatiquement des documents numérisés dans une langue étrangère.  

Vous avez d’autres questions ? Laissez un commentaire, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}