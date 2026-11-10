---
category: general
date: 2026-03-07
description: Extrayez du texte à partir de fichiers PNG en utilisant C#. Apprenez
  comment convertir une image en texte avec C# et lire rapidement le texte des images
  numérisées.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: fr
og_description: Extraire du texte à partir de fichiers PNG avec C#. Ce guide montre
  comment convertir une image en texte en C# et lire le texte à partir d'images numérisées
  avec Aspose OCR.
og_title: Extraire du texte d’un PNG en C# – Guide complet d’OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extraire du texte d’un PNG en C# – Guide complet d’OCR
url: /fr/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'un PNG en C# – Guide complet d'OCR

Vous avez déjà eu besoin d'**extract text from PNG** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul — la plupart des développeurs rencontrent ce problème lorsqu'ils sont confrontés à des graphiques numérisés ou à des captures d'écran qu'il faut rendre recherchables. Bonne nouvelle : avec quelques lignes de C# et Aspose OCR, vous pouvez transformer n'importe quel PNG en chaînes éditables en un clin d'œil.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : de la localisation des PNG sur le disque, au lancement de tâches OCR en parallèle, jusqu'à l’affichage d’un aperçu propre de chaque résultat. À la fin, vous saurez comment **convert image to text C#**, vous pourrez **read text from scanned images** efficacement, et vous verrez la meilleure façon de **run OCR on images** sans bloquer votre thread UI.

## Ce dont vous avez besoin

- .NET 6.0 ou version ultérieure (le code fonctionne aussi avec .NET Core et .NET Framework)  
- Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un dossier rempli de fichiers *.png* que vous souhaitez traiter  
- L'IDE de votre choix (Visual Studio, VS Code, Rider…)

Aucune configuration supplémentaire n’est requise ; la bibliothèque inclut tout le nécessaire pour décoder PNG, JPEG, TIFF, etc.

## Étape 1 : Localiser tous les fichiers PNG – le début de “Extract Text from PNG”

Tout d’abord, nous devons trouver chaque PNG sur lequel nous allons exécuter l’OCR. `Directory.GetFiles` est rapide et fiable.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Pourquoi c’est important :* Balayer le répertoire une seule fois simplifie le reste du pipeline, et la vérification précoce évite une situation silencieuse de « no‑output » difficile à déboguer plus tard.

## Étape 2 : Lancer des tâches OCR parallèles – **run OCR on images** efficacement

Exécuter l’OCR séquentiellement suffit pour quelques fichiers, mais les projets réels traitent souvent des dizaines ou des centaines d’images. En lançant une `Task` par image, on garde le CPU occupé pendant que la bibliothèque effectue le travail lourd.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Astuce :* `Task.Run` délègue le travail au pool de threads, ce qui signifie que votre UI (si vous en avez une) reste réactive. Sur un serveur, le même schéma se met à l’échelle facilement sur plusieurs cœurs.

## Étape 3 : Attendre toutes les tâches – Rassembler les résultats

Nous attendons maintenant que chaque opération OCR se termine. `Task.WhenAll` renvoie un tableau aligné avec l’ordre original des fichiers, ce qui facilite l’association des résultats aux noms de fichiers.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Note sur les cas limites :* Si une image lève une exception (fichier corrompu, format non supporté), le `WhenAll` entier propagera l’exception. Vous pouvez envelopper le `Task.Run` interne dans un try/catch et renvoyer une chaîne vide ou un message diagnostique si vous avez besoin de tolérance aux fautes.

## Étape 4 : Afficher un aperçu – Vérifier la sortie de **convert image to text C#**

Un aperçu rapide vous aide à confirmer que l’OCR a fonctionné avant d’enregistrer les données ailleurs.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Un affichage typique dans la console ressemble à :

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Si l’aperçu montre du charabia, revérifiez la qualité de l’image ou envisagez un pré‑traitement (par ex., binarisation) – mais pour la plupart des PNG propres, Aspose OCR obtient le bon résultat du premier coup.

## Optionnel : Enregistrer les résultats dans un CSV – Cas d’utilisation réel

La plupart des projets ont besoin du texte extrait sous forme structurée. Voici un petit helper qui écrit le nom de fichier et le texte OCR complet dans un fichier CSV.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Vous pouvez maintenant importer le CSV dans Excel, Power BI ou tout autre système en aval qui attend **read text from scanned images**.

## FAQ

**Et si mes PNG sont volumineux (plus de 5 Mo) ?**  
Aspose OCR redimensionne automatiquement les grandes images pour garder la consommation mémoire raisonnable, mais vous pouvez redimensionner manuellement avec `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` pour limiter la largeur à 2000 px tout en conservant le ratio.

**Puis‑je exécuter cela sous Linux ?**  
Oui. Aspose OCR est multiplateforme ; assurez‑vous simplement que les dépendances natives (`libgdiplus` sur certaines distributions) sont installées.

**La langue OCR est‑elle anglaise par défaut ?**  
Exactement. Si vous avez besoin d’une autre langue, définissez `engine.Language = OcrLanguage.French;` (ou tout autre enum supporté) avant d’appeler `Recognize()`.

**Comment gérer les PDF protégés par mot de passe contenant des PNG ?**  
Convertissez d’abord les pages PDF en images (avec Aspose PDF ou une autre bibliothèque), puis alimentez ces PNG dans le même pipeline. Le principe de **how to run OCR on images** reste identique.

## Exemple complet (Async Main)

Voici un programme autonome que vous pouvez copier‑coller dans un projet console. Il inclut toutes les pièces présentées plus haut, ainsi qu’un petit helper pour valider le dossier d’entrée.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Sortie attendue** (exemple pour deux PNG) :

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Conclusion

Nous venons de couvrir tout ce qu’il faut pour **extract text from PNG** avec C#. De la localisation des fichiers, au lancement de jobs OCR parallèles, en passant par l’aperçu des chaînes et leur persistance dans un CSV — ce guide fournit un modèle prêt pour la production dans les scénarios **convert image to text C#**.  

Si vous êtes prêt pour l’étape suivante, essayez d’alimenter le même pipeline avec des fichiers JPEG ou TIFF, expérimentez différentes langues OCR, ou intégrez les résultats à un index de recherche afin de **read text from scanned images** instantanément.  

Des questions sur les cas limites, l’optimisation des performances ou la licence ? Laissez un commentaire ou contactez la communauté Aspose—bon codage !  

![Exemple d'extraction de texte à partir de PNG](extract-text-png.png "Extraction de texte à partir de PNG avec Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}