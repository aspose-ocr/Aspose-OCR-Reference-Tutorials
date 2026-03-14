---
category: general
date: 2026-03-13
description: Comment utiliser l'OCR en C# pour extraire du texte à partir de numérisations.
  Apprenez à convertir des fichiers TIFF en texte avec Aspose OCR, l'accélération
  GPU et du code étape par étape.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: fr
og_description: Comment utiliser l'OCR en C# pour extraire du texte à partir de numérisations.
  Ce guide vous montre comment convertir des fichiers TIFF en texte avec Aspose OCR
  et l'accélération GPU.
og_title: Comment utiliser l'OCR en C# – Extraire rapidement du texte à partir de
  numérisations
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Comment utiliser l'OCR en C# – Extraire rapidement le texte des numérisations
url: /fr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en C# – Extraire du texte des numérisations rapidement

Vous êtes-vous déjà demandé **comment utiliser l'OCR** pour extraire du texte lisible d’une pile de fichiers TIFF numérisés ? Vous n’êtes pas le seul. Dans de nombreux projets réels—pensons à la numérisation de factures, à l’archivage de documents historiques, ou simplement à rendre les PDF recherchables—les développeurs ont besoin d’une méthode fiable pour **extraire du texte des numérisations** sans se compliquer la vie.

Bonne nouvelle ? Avec Aspose OCR et quelques lignes de C# vous pouvez convertir du TIFF en texte en quelques secondes, même sur une station de travail modeste. Vous trouverez ci‑dessous un exemple complet, prêt à l’emploi, ainsi que le raisonnement derrière chaque choix afin que vous puissiez l’adapter à votre propre flux de travail.

## Ce dont vous aurez besoin

Avant de commencer, assurez‑vous d’avoir les éléments suivants à portée de main :

| Prérequis | Pourquoi c’est important |
|--------------|----------------|
| .NET 6+ (ou .NET Framework 4.7+) | Le package NuGet Aspose OCR cible les runtimes .NET modernes. |
| Visual Studio 2022 (ou tout IDE de votre choix) | Vous offre IntelliSense et un débogage facile. |
| Un GPU compatible CUDA & driver (optionnel) | Permet `ocrEngine.UseGpu = true` pour un gain de vitesse notable sur de gros lots. |
| Un dossier d’images TIFF à traiter | Ce tutoriel utilise les fichiers `*.tif`, mais vous pouvez adapter le motif. |
| Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`) | La bibliothèque principale qui fait le travail lourd. |

Si l’un de ces éléments vous manque, procurez‑le‑vous maintenant—inutile de lire plus loin pour se retrouver bloqué par une dépendance manquante.

## Vue d'ensemble de la solution

À haut niveau, le programme réalise trois actions :

1. **Créer un moteur OCR** et activer éventuellement l’accélération GPU.  
2. **Parcourir chaque fichier TIFF** d’un répertoire, lancer la reconnaissance et récupérer le texte brut résultant.  
3. **Écrire le texte** dans un fichier `.txt` placé à côté de l’image originale.

C’est tout. Le code est volontairement minimal, tout en illustrant les bonnes pratiques : sélection explicite de la langue, libération correcte des ressources et gestion des erreurs pour les cas limites les plus courants.

![Exemple d'utilisation de l'OCR en C#](/images/how-to-use-ocr-csharp.png "Illustration de comment utiliser l'OCR en C# pour extraire du texte des numérisations")

## Étape 1 : Initialiser le moteur OCR (Comment utiliser l'OCR)

La première chose dont vous avez besoin est une instance de `OcrEngine`. Cet objet est la porte d’entrée à toutes les fonctionnalités d’Aspose OCR. Par défaut il fonctionne sur le CPU, mais définir `UseGpu = true` indique à la bibliothèque de déléguer les calculs matriciels lourds à votre carte graphique—à condition d’avoir un driver compatible CUDA installé.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Pourquoi c’est important :**  
- **L’accélération GPU** peut réduire le temps de traitement jusqu’à 70 % pour des numérisations haute résolution.  
- **La sélection explicite de la langue** évite que le moteur ne devine et améliore la précision, surtout pour les scripts non latins.

## Étape 2 : Pointer le moteur vers vos numérisations (Convertir TIFF en texte)

Ensuite, nous indiquons au programme où chercher les images. Utiliser `Directory.GetFiles` avec un filtre `*.tif` garde la logique simple et évite d’inclure des fichiers non pertinents comme `.jpg` ou `.png`.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Note de cas limite :** Si le répertoire est vide, la boucle ci‑dessous ne s’exécutera jamais, ce qui est parfaitement acceptable. Vous verrez plus tard un message amical « No files found ».

## Étape 3 : Traiter chaque fichier TIFF (Extraire le texte des numérisations)

Voici le cœur du programme : charger chaque image, exécuter l’OCR et enregistrer le résultat. L’assistant `ImageStream.FromFile` diffuse le fichier directement en mémoire, ce qui est plus efficace que de charger d’abord un `Bitmap`.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Pourquoi nous enveloppons chaque itération dans un `try/catch` :**  
Traiter un lot de documents est parfois chaotique ; un TIFF corrompu ou un manque de mémoire ne doit pas interrompre l’ensemble du processus. Le bloc `catch` consigne le problème et passe à la suite, gardant la chaîne de traitement robuste.

### Sortie attendue

Pour chaque `example.tif` vous trouverez un fichier frère `example.txt` contenant quelque chose comme :

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

Si le moteur OCR ne peut pas lire une ligne, il laissera simplement une ligne vide ou un caractère illisible—aucun plantage.

## Étape 4 : Nettoyage et libération (Bonne pratique)

`OcrEngine` implémente `IDisposable`, il est donc poli de libérer les ressources natives lorsque vous avez fini. Dans une petite application console, le GC pourrait suffire, mais la libération explicite est une habitude qui vaut la peine d’être prise.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Exemple complet fonctionnel (Prêt à copier‑coller)

Voici le programme complet que vous pouvez coller dans un nouveau projet Console App. Il compile tel quel, à condition d’avoir ajouté le package NuGet Aspose.OCR.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Checklist rapide

- **Drapeau GPU** – supprimez‑le ou réglez‑le sur `false` si vous n’avez pas de driver CUDA.  
- **Langue** – remplacez `Language.English` par toute autre langue prise en charge.  
- **Motif de fichier** – changez `"*.tif"` en `"*.png"` ou `"*.*"` si vos numérisations sont dans un autre format.  

## Pièges courants & astuces pro (tutoriel OCR c#)

| Piège | Comment l’éviter |
|---------|-----------------|
| **Erreurs de dépassement de mémoire** sur de très gros lots | Traitez les fichiers par petits groupes ou appelez `GC.Collect()` après chaque 50 fichiers (rarement nécessaire). |
| **GPU non détecté** alors que `UseGpu = true` | Le moteur revient silencieusement au CPU, mais vous pouvez vérifier `ocrEngine.IsGpuAvailable` après construction. |
| **Pack de langue incorrect** entraînant une sortie illisible | Toujours définir explicitement `ocrEngine.Language` ; la valeur par défaut peut être `Language.Unknown`. |
| **Le chemin du fichier contient des caractères Unicode** | Utilisez `Path.GetFullPath` pour normaliser, ou préfixez avec `@"\\?\"` sous Windows si les chemins dépassent |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}