---
category: general
date: 2026-04-01
description: Apprenez à reconnaître rapidement le texte des fichiers PNG en définissant
  l’ID du dispositif GPU et en activant l’accélération GPU dans Aspose OCR. Guide
  C# étape par étape.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: fr
og_description: Reconnaissez rapidement le texte des fichiers PNG en définissant l’ID
  du dispositif GPU. Suivez ce guide complet en C# pour activer l’accélération GPU
  avec Aspose OCR.
og_title: Reconnaître du texte à partir d’un PNG – Tutoriel OCR Aspose accéléré par
  GPU
tags:
- C#
- OCR
- GPU
- Aspose
title: Reconnaître du texte à partir de PNG avec Aspose OCR – Démo par lots accélérée
  par GPU
url: /fr/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte à partir de png – Tutoriel complet C# avec accélération GPU par lots

Vous avez déjà eu besoin de **recognize text from png** images mais avez trouvé le processus douloureusement lent ? Vous n'êtes pas seul. La plupart des développeurs commencent par un appel OCR simple, puis regardent une console qui rame comme un escargot lorsqu'un dossier contient des dizaines de captures d'écran.  

Bonne nouvelle ? Aspose OCR peut déléguer le travail intensif à votre carte graphique, et en quelques lignes vous pouvez **set gpu device id** pour choisir le GPU exact que vous voulez. Dans ce guide, nous parcourrons un exemple complet et exécutable qui récupère chaque PNG d'un dossier, active l'accélération GPU, sélectionne le premier GPU et affiche le nombre de caractères pour chaque fichier.

À la fin, vous disposerez d'un programme autonome que vous pourrez intégrer à n'importe quel projet .NET, et vous comprendrez pourquoi activer le GPU est important, comment gérer les cas limites, et quoi ajuster pour encore meilleure performance.

## Ce dont vous avez besoin

- **.NET 6.0** ou ultérieur (le code se compile également avec .NET Core).  
- Le package NuGet **Aspose.OCR** – installez-le avec `dotnet add package Aspose.OCR`.  
- Une machine avec un GPU compatible CUDA (NVIDIA est le plus courant) et le pilote approprié.  
- Un dossier rempli d'images **PNG** que vous souhaitez traiter.  

Si l'un de ces éléments vous est inconnu, ne paniquez pas. Les étapes ci-dessous incluent les commandes exactes dont vous avez besoin, et nous discuterons également de ce qu'il faut faire lorsqu'un GPU n'est pas présent.

## Étape 1 : Initialiser le moteur OCR et activer l'accélération GPU

La première chose à faire est de créer une instance `OcrEngine` et d'activer le support GPU. Ce drapeau indique à Aspose d'utiliser les bibliothèques CUDA natives en interne.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Pourquoi c'est important :** Sans `UseGpuAcceleration`, chaque image est traitée par le CPU, ce qui peut être plusieurs ordres de grandeur plus lent, surtout pour les PNG haute résolution. Activer ce drapeau prépare également le moteur à accepter un dispositif GPU spécifique plus tard.

## Étape 2 : Définir l'ID du dispositif GPU (Optionnel mais recommandé)

Si votre poste de travail possède plusieurs GPU, vous pouvez choisir lequel utiliser. Les IDs de dispositif commencent à **0**, donc `0` sélectionne le premier GPU, `1` le deuxième, etc.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Astuce :** Lors de l'exécution sur un serveur partagé, définir explicitement l'ID du dispositif GPU peut empêcher votre tâche de voler des ressources aux autres processus. Si vous omettez cette ligne, Aspose choisira le dispositif par défaut, ce qui est généralement suffisant pour une configuration à GPU unique.

## Étape 3 : Rassembler tous les fichiers PNG de votre dossier de lot

Ensuite, nous devons localiser chaque PNG sur lequel vous souhaitez exécuter l'OCR. La méthode `Directory.GetFiles` fait le travail lourd.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Cas limite :** Si le dossier est vide, `imageFiles` sera un tableau vide. Nous gérerons cela plus tard avec un message convivial.

## Étape 4 : Traiter chaque image et afficher le nombre de caractères reconnus

Voici la boucle principale. Pour chaque PNG, nous appelons `Recognize`, puis affichons le nom du fichier et la longueur du texte extrait.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**What you’ll see:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Si une image ne contient aucun texte, le compte sera `0`. C'est tout à fait normal pour les captures d'écran purement graphiques.

## Étape 5 : Exécuter le programme et vérifier l'utilisation du GPU

Compilez le fichier (`dotnet build`) et exécutez-le (`dotnet run`). Pendant que la console défile, vous pouvez ouvrir votre outil de surveillance GPU (comme NVIDIA Smi) pour voir le pic d'utilisation du GPU brièvement pour chaque image. Si vous ne voyez aucune activité, revérifiez que :

1. Le pilote CUDA est installé.  
2. `UseGpuAcceleration` est réglé sur `true`.  
3. Le `GpuDeviceId` correct correspond à un GPU physique.

Si le GPU n'est pas disponible, Aspose reviendra automatiquement au CPU, mais vous perdrez l'avantage de vitesse.

## Variations courantes & astuces

| Situation | Ce qu'il faut changer |
|-----------|-----------------------|
| **Format d'image différent** (p. ex., JPEG) | Modifiez le motif de recherche en `*.jpg` ou `*.*` et Aspose reconnaîtra toujours le texte. |
| **Taille du lot très importante** (des milliers de fichiers) | Traitez par morceaux pour éviter la pression mémoire : divisez `imageFiles` en tableaux plus petits. |
| **Besoin du texte réel, pas seulement de la longueur** | Remplacez `ocrResult.Text.Length` par `ocrResult.Text` dans le `WriteLine`. |
| **Exécution sur un serveur sans interface** | Assurez-vous que le serveur possède un pilote GPU ; sinon, définissez `UseGpuAcceleration = false` pour éviter des erreurs inutiles. |
| **Plusieurs GPU, vouloir équilibrer la charge** | Bouclez sur `ocrEngine.GpuDeviceId = i % gpuCount` à l'intérieur du `foreach` pour faire tourner les dispositifs. |

## Sortie attendue & vérification

Lorsque tout fonctionne, la console affiche chaque nom de fichier suivi du nombre de caractères, comme montré précédemment. Pour revérifier la sortie OCR réelle, vous pouvez temporairement afficher le texte :

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

N'oubliez pas de supprimer ou de commenter cette ligne pour les gros lots ; imprimer des milliers de lignes peut submerger votre terminal.

## Exemple complet fonctionnel (prêt à copier‑coller)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

Enregistrez-le sous le nom `GpuBatchDemo.cs`, exécutez `dotnet add package Aspose.OCR`, puis `dotnet run`. Vous devriez voir les comptes de caractères apparaître presque instantanément pour chaque PNG, grâce à l'accélération GPU.

## Conclusion

Vous savez maintenant comment **recognize text from png** efficacement en activant l'accélération GPU et en définissant explicitement **set gpu device id** dans Aspose OCR. Le programme complet, prêt à copier‑coller, gère la découverte de dossiers, les vérifications de cas limites, et vous fournit un retour immédiat sur les performances OCR.

Prochaines étapes ? Essayez d'échanger l'appel `Recognize` contre `ocrEngine.RecognizeAsync` si vous avez besoin d'un traitement non bloquant, ou expérimentez différentes options de prétraitement d'image (p. ex., binarisation) que Aspose propose. Vous pourriez également acheminer les résultats OCR vers une base de données ou un index de recherche pour une solution de recherche en texte intégral.

Des questions sur la gestion des PDF multi‑pages, ou envie de comparer Aspose OCR avec Tesseract ? Laissez un commentaire ou explorez nos autres tutoriels sur **batch OCR C#**, **conseils de performance OCR**, et **traitement d'image piloté par GPU**. Bon codage !  

![Sortie console affichant les comptes de caractères reconnus pour les fichiers PNG – reconnaître du texte à partir de png avec accélération GPU](image-placeholder.png "exemple de sortie de reconnaissance de texte à partir de png")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}