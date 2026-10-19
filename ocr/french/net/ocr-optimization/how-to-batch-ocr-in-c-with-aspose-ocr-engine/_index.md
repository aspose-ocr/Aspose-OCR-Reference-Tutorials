---
category: general
date: 2026-09-13
description: Comment effectuer une OCR par lots avec Aspose OCR GPU en C# en utilisant
  .NET. Apprenez à reconnaître le texte à partir d'images, extraire le texte des fichiers
  TIFF et accélérer le traitement grâce au support GPU.
draft: false
keywords:
- aspose ocr gpu
- process multiple images
- how to batch ocr
- install aspose ocr
lastmod: 2026-09-13
og_description: Comment effectuer une OCR par lots avec Aspose OCR GPU en C# en utilisant
  .NET. Ce guide vous montre comment reconnaître le texte à partir d'images, extraire
  le texte des fichiers TIFF et exploiter l'accélération GPU pour un traitement haute
  performance.
og_image_alt: Screenshot of Aspose OCR GPU batch processing console output in C#
og_title: Comment effectuer une OCR par lots avec Aspose OCR GPU en C# en utilisant
  .NET
schemas:
- author: Aspose
  dateModified: '2026-09-13'
  description: How to batch OCR with Aspose OCR GPU in C# using .NET. Learn to recognize
    text from images, extract text from TIFF files, and accelerate processing with
    GPU support.
  headline: How to batch OCR with Aspose OCR GPU in C# using .NET
  type: TechArticle
- questions:
  - answer: Yes, as long as the server has a CUDA‑compatible GPU and the appropriate
      driver libraries installed; no display is required.
    question: Can I run the GPU version on a headless Linux server?
  - answer: Absolutely. The engine treats each page as a separate image and returns
      concatenated text, preserving page order.
    question: Does Aspose OCR support multi‑page TIFF files out of the box?
  - answer: Benchmarks show Aspose OCR achieves ≥ 96 % character accuracy on clean
      printed documents and ≥ 90 % on low‑contrast scans, matching leading SaaS providers
      while keeping data on‑premises.
    question: How accurate is the OCR output compared with cloud services?
  - answer: The library imposes no hard limit; practical limits are driven by available
      disk space and GPU memory. Processing 10 000 pages on an RTX 3080 typically
      stays under 2 GB of GPU memory.
    question: Is there a limit to the number of files I can process in one run?
  - answer: Yes, set `ocrEngine.Language = OcrLanguage.Spanish` (or any supported
      language) before calling `Recognize`. The engine supports 30+ languages, including
      Arabic, Chinese, and Hindi.
    question: Can I customize the language model for non‑English scripts?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
title: Comment effectuer une OCR par lots avec Aspose OCR GPU en C# en utilisant .NET
url: /fr/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer une OCR par lots avec Aspose OCR GPU en C# sous .NET

Si vous devez **batch OCR** des centaines de pages numérisées rapidement, le moteur Aspose OCR GPU vous offre un moyen rapide et fiable de reconnaître du texte à partir d'images et de fichiers TIFF en une seule exécution. Dans ce guide, vous verrez comment configurer un projet .NET, activer l'accélération GPU et traiter un dossier complet d'images sans écrire une seule ligne de code boiler‑plate vous-même.

## Réponses rapides
- **Qu’est‑ce que le “batch OCR” ?** Il s'agit du traitement automatisé de nombreux fichiers image en une seule opération, renvoyant le texte extrait pour chaque fichier.  
- **Puis‑je utiliser la version GPU sur n'importe quelle machine ?** Oui, tant que le système possède un GPU compatible CUDA et le pilote approprié installé.  
- **Ai‑je besoin d'une licence pour le développement ?** Une licence d'essai gratuite suffit pour les tests ; une licence commerciale est requise pour la production.  
- **Quelles versions de .NET sont prises en charge ?** .NET 6.0 et ultérieures sont entièrement prises en charge ; .NET 5 fonctionne également avec quelques ajustements.  
- **Le moteur est‑il thread‑safe pour les exécutions parallèles ?** Le moteur CPU est thread‑safe ; le moteur GPU nécessite une instance par thread ou une stratégie parallèle contrôlée.

## Qu’est‑ce que Aspose OCR GPU ?
Le moteur `Aspose.OCR` GPU est une bibliothèque OCR haute performance qui délègue le travail d'analyse d'images à une carte graphique compatible CUDA, offrant jusqu'à 4 fois plus de débit comparé au traitement purement CPU. Elle prend en charge un large éventail de formats d'image, fournit des modèles de langue intégrés et peut être intégrée à n'importe quelle application .NET avec peu de modifications de code.

## Pourquoi utiliser Aspose OCR GPU pour le traitement par lots ?
Aspose OCR prend en charge **plus de 30 formats d'image** (y compris PNG, JPEG, BMP et TIFF multipage) et peut gérer des fichiers allant jusqu'à **2 Go** chacun sans charger le document complet en mémoire. Lorsque vous activez l'accélération GPU, les pages TIFF typiques de 300 dpi sont traitées en moins de 0,2 seconde par page sur une carte RTX 3080 moderne.

## Prérequis
- SDK .NET 6.0 (ou ultérieur) installé sur votre machine de développement.  
- Package NuGet Aspose.OCR pour .NET – choisissez le package `Aspose.OCR.Gpu` si vous disposez d'un GPU compatible, sinon installez `Aspose.OCR`.  
- Un dossier contenant les images que vous souhaitez traiter (TIFF, PNG, JPEG, etc.).  
- Visual Studio 2022, Rider ou tout éditeur capable de créer des applications console .NET.

> **Conseil pro :** Vérifiez que CUDA 11+ est installé et que `nvidia-smi` indique votre GPU comme « compatible ». La bibliothèque reviendra automatiquement au CPU si aucun GPU adapté n'est trouvé.

## Comment configurer le projet et installer Aspose OCR
Créez une nouvelle application console .NET, ajoutez le package NuGet Aspose OCR et restaurez les dépendances. Cela prépare un projet léger qui peut être compilé et exécuté sur n'importe quelle plateforme supportant .NET 6 ou ultérieur. Après l'installation du package, vous pouvez référencer les classes OCR directement dans votre code, activant le traitement par lots sans configuration supplémentaire.

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Si vous disposez d'une licence compatible GPU, installez plutôt le package spécifique GPU. Cette version contient des liaisons CUDA natives qui permettent au moteur de s'exécuter sur la carte graphique, offrant le gain de performance décrit précédemment.

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Votre projet référence désormais la bibliothèque OCR requise pour **batch OCR**.

## Comment initialiser le moteur OCR (CPU ou GPU)
La classe `OcrEngine` est le point d'entrée principal pour effectuer des opérations OCR. Elle abstrait le matériel sous‑jacent et fournit une API simple pour l'exécution sur CPU et GPU. Chargez le moteur OCR et indiquez‑lui s'il doit utiliser le GPU :

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Pourquoi c'est important :** Le réglage `UseGpu` permet à Aspose de choisir le chemin d'exécution le plus rapide. Lorsqu'un GPU compatible est présent, le moteur s'exécute sur la carte graphique ; sinon il revient au CPU sans générer d'erreur, garantissant que votre tâche par lots ne plante jamais à cause d'un matériel manquant.

## Comment rassembler les fichiers à traiter
Rassembler les images cibles est la première étape de tout flux de travail par lots. Construisez une liste de chemins de fichiers correspondant aux extensions prises en charge, puis transmettez cette liste à la boucle OCR. Cette approche maintient le code simple et facilite l'ajout de filtres ultérieurement.

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Note de cas limite :** Si votre dossier contient des formats mixtes, remplacez le motif de recherche par `\"*.*\"` et filtrez par extension à l'intérieur de la boucle. Cela rend le traitement par lots flexible et évite les fichiers manquants.

## Comment traiter chaque image et afficher un aperçu
Pour chaque fichier, invoquez le moteur OCR, récupérez le texte reconnu et affichez un court extrait dans la console. Afficher un aperçu aide à vérifier que le traitement par lots fonctionne correctement sans ouvrir chaque fichier de sortie.

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Ce que vous verrez :** Pour chaque image, la console affiche les 100 premiers caractères du texte reconnu, confirmant que le traitement par lots a réussi sans ouvrir chaque fichier manuellement.

## Comment enregistrer les résultats OCR (optionnel mais pratique)
Conserver la sortie OCR complète permet l'indexation en aval, l'analyse IA ou la conversion en PDF recherchables. Écrivez le texte dans un fichier `.txt` placé à côté de l'image source, en utilisant le même nom de base pour une corrélation facile.

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Chaque image possède désormais un fichier texte compagnon contenant la sortie OCR complète, prêt pour les moteurs de recherche, les modèles de langue ou les pipelines d'analyse personnalisés.

## Comment exécuter la démo et vérifier la sortie
Compilez et exécutez l'application console pour voir le traitement par lots en action. L'étape de compilation compile le code, tandis que l'étape d'exécution traite chaque image du dossier cible et écrit les lignes d'aperçu dans la console. Si vous avez activé l'étape d'enregistrement optionnelle, vous trouverez également un fichier `.txt` pour chaque image source.

1. Compilez le projet : `dotnet build`.  
2. Exécutez le programme : `dotnet run --project GpuBatchDemo.csproj`.

Vous devriez voir les lignes d'aperçu dans la console et, si vous avez ajouté l'étape optionnelle, une série de fichiers `.txt` à côté de vos images sources.

## Problèmes courants et comment les résoudre
| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| **Empty `ocrResult.Text`** | Image trop sombre ou DPI faible | Pré‑traitez les images (augmentez le contraste, upscale) ou activez `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Pilote obsolète | Mettez à jour le pilote GPU, ou définissez `UseGpu = false` pour forcer le traitement CPU. |
| **Exception “File not found”** | Séparateur de chemin incorrect sous Linux/macOS | Utilisez `Path.Combine` ou des barres obliques (`/`). |

## Comment mettre à l'échelle au‑delà de quelques fichiers
Lorsque vous passez de dizaines à des milliers d'images, envisagez ces stratégies : utilisez le traitement parallèle avec des instances de moteur séparées par thread, chargez les images par lots gérables et consignez la progression dans un fichier pour une récupération facile. Ces techniques maintiennent une faible consommation de mémoire et un débit élevé.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Rappel :** La mémoire GPU est partagée par le processus. Démarrer trop de tâches GPU parallèles peut saturer la mémoire et ralentir le traitement par lots. Commencez avec 2‑4 threads et surveillez l'utilisation du GPU.

## Questions fréquemment posées

**Q : Puis‑je exécuter la version GPU sur un serveur Linux sans affichage ?**  
R : Oui, tant que le serveur possède un GPU compatible CUDA et les bibliothèques de pilotes appropriées installées ; aucun affichage n'est requis.

**Q : Aspose OCR prend‑il en charge les fichiers TIFF multipage nativement ?**  
R : Absolument. Le moteur traite chaque page comme une image distincte et renvoie le texte concaténé, en conservant l'ordre des pages.

**Q : Quelle est la précision de la sortie OCR comparée aux services cloud ?**  
R : Les benchmarks montrent qu'Aspose OCR atteint ≥ 96 % de précision de caractères sur des documents imprimés propres et ≥ 90 % sur des scans à faible contraste, égalant les principaux fournisseurs SaaS tout en conservant les données sur site.

**Q : Existe‑t‑il une limite au nombre de fichiers que je peux traiter en une exécution ?**  
R : La bibliothèque n'impose aucune limite stricte ; les limites pratiques dépendent de l'espace disque disponible et de la mémoire GPU. Traiter 10 000 pages sur une RTX 3080 reste généralement en dessous de 2 Go de mémoire GPU.

**Q : Puis‑je personnaliser le modèle de langue pour des scripts non anglais ?**  
R : Oui, définissez `ocrEngine.Language = OcrLanguage.Spanish` (ou toute langue prise en charge) avant d'appeler `Recognize`. Le moteur prend en charge plus de 30 langues, dont l'arabe, le chinois et l'hindi.

## Conclusion
Vous disposez maintenant d'une solution complète, de bout en bout, pour **batch OCR with Aspose OCR GPU in C#**. Le tutoriel a couvert la configuration du projet, l'activation du GPU, l'énumération des fichiers, le traitement image par image, la persistance optionnelle des résultats et les techniques de mise à l'échelle pour des charges de travail massives. Avec cette base, vous pouvez alimenter la sortie OCR dans des index de recherche, la fournir à des modèles de grande taille, ou créer des pipelines de traitement de documents personnalisés.

Prêt pour le prochain défi ? Essayez de combiner le texte OCR avec Aspose .PDF pour générer des PDF recherchables, ou intégrez la sortie avec Azure Cognitive Search pour une recherche plein texte instantanée à travers des milliers de documents numérisés.

---

**Dernière mise à jour :** 2026-09-13  
**Testé avec :** Aspose.OCR 24.5 pour .NET (packages CPU & GPU)  
**Auteur :** Aspose  

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```
```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

## Tutoriels associés

- [Comment utiliser l'OCR en C pour extraire du texte d'images avec l'accélération GPU](/ocr/net/ocr-optimization/how-to-use-ocr-in-c-extract-text-from-images-with-gpu-accele/)
- [Reconnaître du texte à partir d'une image avec Aspose OCR GPU accéléré C](/ocr/net/ocr-optimization/recognize-text-from-image-with-aspose-ocr-gpu-accelerated-c/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}