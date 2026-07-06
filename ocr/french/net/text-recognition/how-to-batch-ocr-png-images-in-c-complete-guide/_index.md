---
category: general
date: 2026-03-17
description: Comment effectuer une OCR par lots d'images PNG en C# rapidement. Apprenez
  à extraire le texte des fichiers PNG, à convertir les PNG en texte et à lire les
  images d'un répertoire avec un script simple.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: fr
og_description: Comment effectuer une OCR par lots d'images PNG en C# avec du code
  pas à pas. Extraire le texte des fichiers PNG, convertir les PNG en texte et lire
  les images d'un répertoire sans effort.
og_title: Comment faire de l'OCR par lots d'images PNG en C# – Guide complet
tags:
- OCR
- C#
- Image Processing
title: Comment effectuer une OCR par lots d'images PNG en C# – Guide complet
url: /fr/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

markdown formatting, code blocks placeholders unchanged.

Also need to preserve the horizontal rules as "---". Already.

Check for any other links: none.

Now produce final output with translated content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer un OCR par lots d'images PNG en C# – Guide complet

Vous vous êtes déjà demandé **how to batch OCR** sur un dossier rempli de captures d'écran sans ouvrir chaque fichier manuellement ? Vous n'êtes pas le seul—les développeurs demandent constamment comment faire de l'OCR par lots sur de grandes collections de PNG, surtout lorsque le but est d'extraire du texte PNG files pour une analyse en aval.  

Dans ce tutoriel, nous parcourrons un exemple C# prêt à l’emploi qui **extracts text PNG** files, **converts PNG to text**, et vous montre la meilleure façon de **read images from directory**. À la fin, vous disposerez d’un script unique qui crée un fichier `.txt` à côté de chaque image, vous faisant gagner des heures de copier‑pasting manuel.

## Ce que vous allez accomplir

- Initialiser un moteur OCR une fois et le réutiliser pour tout le lot.  
- Analyser chaque `*.png` dans un dossier donné sans écrire vous‑même de boucle.  
- Écrire chaque résultat OCR dans son propre fichier texte, en conservant le nom de fichier original.  
- Gérer les cas limites courants comme les dossiers vides ou les fichiers non‑image de manière élégante.

### Prérequis

- .NET 6.0 ou supérieur (le code fonctionne également sur .NET Core et .NET Framework).  
- Une bibliothèque OCR qui expose les types `OcrEngine`, `ImageStream` et `OcrResult` (par exemple, le fictif SDK **FastOCR** utilisé dans les extraits).  
- Connaissances de base en C#—aucun motif avancé requis.

---

## Comment faire de l'OCR par lots d'images PNG – Vue d'ensemble

Voici le **programme complet, runnable**. N'hésitez pas à le copier‑paste dans un nouveau projet console, à remplacer les chemins factices, et à appuyer sur **F5**.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Sortie attendue :** Pour chaque `image01.png`, vous trouverez un `image01.txt` contenant les caractères reconnus. La console affichera chaque fichier au fur et à mesure de son écriture.

![Diagramme de traitement OCR par lots](how-to-batch-ocr-diagram.png "Diagramme illustrant comment effectuer un OCR par lots d'images PNG avec C#")

---

## Explication étape par étape

### 1. Initialiser le moteur OCR – le cœur du processus  

La ligne `var ocrEngine = new OcrEngine();` crée une instance unique du moteur qui sera réutilisée pour tout le lot. Réutiliser le moteur est **crucial** car la plupart des bibliothèques OCR allouent des ressources lourdes (comme les modèles de langue) lors de la construction. Initialiser une seule fois améliore considérablement les performances—surtout lorsque vous avez des dizaines ou des centaines de PNG.

> **Astuce pro :** Si vous avez besoin d’une langue autre que l’anglais, définissez `ocrEngine.Config.Language = Language.Spanish;` (ou tout autre enum pris en charge).  

### 2. Lire les images depuis le répertoire – localiser chaque PNG  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` fait exactement ce que promet le mot‑clé secondaire *read images from directory*. Il renvoie un tableau de chemins absolus, que nous transmettons ensuite au moteur OCR.  

> **Pourquoi ne pas utiliser `SearchOption.AllDirectories` ?** Si vos images sont imbriquées, vous pouvez passer à `GetFiles(path, "*.png", SearchOption.AllDirectories)`. N'oubliez pas que des analyses plus profondes peuvent ramener des fichiers indésirables, donc filtrez en conséquence.

### 3. Convertir les chemins de fichiers en objets ImageStream  

La plupart des SDK OCR attendent un flux plutôt qu’un chemin brut. L’expression LINQ `Select(path => ImageStream.FromFile(path)).ToList()` crée une **list of streams** que le batch recognizer peut consommer en un seul appel. Cette étape garantit également que les descripteurs de fichiers ne sont ouverts qu’une seule fois, réduisant la surcharge d’I/O.

> **Cas limite :** Si un fichier est corrompu, `ImageStream.FromFile` peut lever une exception. Enveloppez la conversion dans un `try/catch` si vous avez besoin de résilience.

### 4. Reconnaître le texte dans le lot complet  

`ocrEngine.RecognizeBatch(imageStreams)` est le point idéal pour *how to batch OCR*. Au lieu de boucler sur chaque image et d’appeler une méthode mono‑image, nous transmettons l’ensemble de la collection au moteur. En interne, la bibliothèque peut paralléliser le travail, vous offrant un gain de vitesse sur les machines multi‑cœurs.

> **Conseil :** Si votre bibliothèque OCR n’expose pas de méthode batch, vous pouvez tout de même obtenir des performances similaires en utilisant `Parallel.ForEach` autour de l’appel `Recognize` mono‑image.

### 5. Écrire chaque résultat OCR – conversion PNG en texte  

La boucle `for` finale écrit `ocrResults[i].Text` dans un fichier `.txt` dont le nom reflète le PNG original. C’est exactement ce que décrit le mot‑clé secondaire *convert PNG to text*. L’appel `Path.Combine` garantit que le dossier de sortie existe et empêche les bugs de traversée de chemin.

> **Erreur courante :** Oublier de créer d’abord le répertoire de sortie provoquera une `DirectoryNotFoundException`. La ligne `Directory.CreateDirectory(outputFolder);` résout cela de façon préventive.

---

## Gestion des variations du monde réel

| Situation | What to Change | Why |
|-----------|----------------|-----|
| **Dossier d'entrée vide** | Conserver la garde précoce `if (imagePaths.Length == 0)` | Empêche un appel OCR inutile et fournit un message convivial |
| **Types de fichiers mixtes** | Use `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` | Garantit que vous ne traitez que des PNG, satisfaisant *extract text png* sans erreurs |
| **Images volumineuses ( > 5 Mo )** | Downscale before feeding to OCR: `ImageStream.FromFile(path).Resize(1920, 1080)` (if API supports) | Réduit la pression mémoire et améliore souvent la précision de reconnaissance |
| **Langue OCR différente** | Set `ocrEngine.Config.Language = Language.French;` | Aligne le moteur avec la langue des images sources |

---

## Questions fréquentes (FAQ)

**Q : Cette solution fonctionne-t-elle avec des fichiers JPEG ou TIFF ?**  
R : La logique principale reste la même ; il suffit de changer le motif de recherche en `"*.jpg"` ou `"*.tif"` et de s’assurer que la bibliothèque OCR peut décoder ces formats.

**Q : Comment puis‑je traiter des milliers d'images sans épuiser la mémoire ?**  
R : Remplacez l’appel batch par une approche de streaming—traitez un lot d’environ 50 images à la fois, puis libérez les flux avant de charger le lot suivant.

**Q : J’ai besoin du score de confiance OCR. Où le trouver ?**  
R : La plupart des objets `OcrResult` exposent une propriété `Confidence`. Vous pouvez étendre l’étape d’écriture :

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Conclusion

Nous venons de couvrir **how to batch OCR** des images PNG en C# du début à la fin. En initialisant un seul moteur, en lisant les images depuis le répertoire, en les convertissant en flux, en reconnaissant tout le lot, et enfin en écrivant chaque résultat dans un fichier texte, vous disposez maintenant d’un modèle solide et prêt pour la production pour les tâches **extract text PNG**, **convert PNG to text**, et **read images from directory**.

Et ensuite ? Essayez de remplacer le fournisseur OCR, ajoutez un post‑traitement multithread (par ex., la correction orthographique), ou alimentez les fichiers `.txt` dans un index de recherche. Le ciel est la limite une fois que vous avez maîtrisé le flux de travail par lots.

Vous avez une variante à partager ? Laissez un commentaire, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}