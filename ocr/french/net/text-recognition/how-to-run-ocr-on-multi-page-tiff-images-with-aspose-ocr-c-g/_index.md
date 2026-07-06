---
category: general
date: 2026-02-11
description: Apprenez à exécuter l’OCR sur un TIFF multipage en C# avec Aspose OCR.
  Convertissez le TIFF en texte, extrayez le texte du TIFF et reconnaissez rapidement
  le texte à partir d’une image.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: fr
og_description: Comment exécuter la reconnaissance OCR sur un TIFF multipage avec
  Aspose OCR en C#. Guide étape par étape pour convertir un TIFF en texte, extraire
  le texte d’un TIFF et reconnaître le texte à partir d’une image.
og_title: Comment exécuter l’OCR sur des images TIFF multipages – Tutoriel complet
  C#
tags:
- OCR
- C#
- Aspose
- TIFF
title: Comment exécuter l’OCR sur des images TIFF multipages avec Aspose OCR – Guide
  C#
url: /fr/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

none.

Check for any code block placeholders: CODE_BLOCK_0-7. Keep.

Check for any inline code: already fine.

Make sure we keep headings with same number of #.

Now produce final output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exécuter l'OCR sur des images TIFF multi‑pages avec Aspose OCR

Vous vous êtes déjà demandé **comment exécuter l'OCR** sur un TIFF numérisé contenant plusieurs pages ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils doivent extraire du texte interrogeable à partir d'anciens documents. La bonne nouvelle ? Avec Aspose OCR, vous pouvez reconnaître du texte à partir de fichiers image en quelques lignes de code C#, et vous obtiendrez du texte brut concaténé prêt à être indexé ou traité davantage.

Dans ce tutoriel, nous parcourrons l’ensemble du flux de travail : de l’installation du package Aspose OCR, au chargement d’un TIFF multi‑pages, en passant par la conversion du TIFF en texte et enfin l’affichage du contenu extrait. À la fin, vous serez capable d’**extraire du texte à partir de fichiers TIFF**, d’**reconnaître du texte à partir d’images**, et même d’automatiser le processus pour des dizaines de fichiers dans un travail par lots. Pas de magie, juste des étapes claires et pratiques.

## Ce que vous apprendrez

- Comment configurer le moteur Aspose OCR pour la reconnaissance de la langue anglaise.  
- Le code exact nécessaire pour **convertir le TIFF en texte** en utilisant la classe `OcrEngine`.  
- Astuces pour gérer les images multi‑pages et garantir que chaque page soit correctement séparée.  
- Pièges courants (comme les dépendances natives manquantes) et comment les éviter.  

**Prérequis** – vous aurez besoin de .NET 6 ou supérieur, Visual Studio (ou tout éditeur C#), et d’une connexion Internet pour la fonction de téléchargement automatique des ressources. C’est tout ; aucune bibliothèque native supplémentaire à gérer.

---

## Étape 1 – Installer le package NuGet Aspose OCR

Avant de pouvoir **effectuer l'OCR sur des fichiers image**, vous devez ajouter la bibliothèque à votre projet.

```bash
dotnet add package Aspose.OCR
```

> **Astuce pro :** Si vous travaillez dans Visual Studio, vous pouvez également faire un clic droit sur le projet → *Manage NuGet Packages* → rechercher “Aspose.OCR” et cliquer sur *Install*.

Le package comprend tout ce dont vous avez besoin, et avec `AutomaticResourceDownload = true` le moteur téléchargera les packs de langues à la volée.

---

## Étape 2 – Initialiser le moteur OCR (Comment exécuter l'OCR)

Maintenant que le package est en place, nous créons et configurons une instance `OcrEngine`. C’est le cœur de **comment exécuter l'OCR** dans notre scénario.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Pourquoi c’est important :** Le paramètre `Language` indique au moteur quel jeu de caractères attendre, tandis que `AutomaticResourceDownload` vous évite de placer manuellement les fichiers de langue sur le serveur. `OutputFormat` à `Text` nous fournit une chaîne simple—parfait pour les pipelines de **conversion du TIFF en texte**.

---

## Étape 3 – Charger le TIFF multi‑pages (Reconnaître le texte à partir d’une image)

Un TIFF peut contenir de nombreuses trames, chacune représentant une page. La classe `System.Drawing.Image` abstrait cela pour nous.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Et si le fichier n’est pas dans le même dossier ?** Fournissez simplement un chemin absolu complet ou utilisez `Path.Combine` avec `AppContext.BaseDirectory`.  
> **Qu’en est‑il de l’utilisation de la mémoire ?** L’instruction `using` libère l’image après le traitement, évitant les fuites—crucial lorsque vous traitez par lots des dizaines de gros TIFF.

L’appel `Recognize` parcourt automatiquement chaque page du TIFF, concaténant les résultats avec des sauts de ligne. C’est pourquoi vous verrez chaque page séparée lorsque vous afficherez `ocrResult.Text`.

---

## Étape 4 – Exemple complet fonctionnel (Toutes les étapes dans un seul fichier)

Ci-dessous se trouve une application console complète, prête à être exécutée. Copiez‑collez‑la dans un nouveau projet console .NET et appuyez sur **F5**.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Sortie attendue** (troncature pour la brièveté) :

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Chaque page apparaît sur sa propre ligne car `OcrOutputFormat.Text` insère un saut de ligne entre les trames. Si vous avez besoin d’un séparateur différent, vous pouvez post‑traiter `result.Text` avec `String.Replace`.

---

## Étape 5 – Gestion des cas limites courants

### 5.1 Fichiers TIFF volumineux  
Lorsqu’on travaille avec des TIFF de plusieurs gigaoctets, charger le fichier entier en mémoire peut poser problème. Une solution de contournement consiste à traiter chaque trame individuellement :

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Documents non‑anglais  
Si vous devez **reconnaître du texte à partir d’une image** en espagnol ou en français, il suffit de modifier la propriété `Language` :

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose téléchargera automatiquement les ressources linguistiques appropriées.

### 5. Enregistrement du résultat  
Souvent vous voudrez **convertir le TIFF en texte** et enregistrer le résultat dans un fichier `.txt` :

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Vous pouvez également diviser la sortie par page en utilisant `String.Split(Environment.NewLine)` et écrire chaque tranche dans un fichier séparé.

---

## Astuces pro & pièges

- **AutomaticResourceDownload** fonctionne la première fois que vous lancez l’application ; les exécutions suivantes sont hors ligne.  
- Si vous voyez des caractères illisibles, revérifiez le paramètre `Language` ; des packs de langues incompatibles entraînent une mauvaise reconnaissance.  
- Pour les PDF rasterisés en TIFF, vous pouvez augmenter `ocrEngine.Dpi` (la valeur par défaut est 300) pour une meilleure précision.  
- Enveloppez toujours `Image.FromFile` dans un bloc `using` ; sinon le fichier sera verrouillé et vous ne pourrez pas le supprimer ou le déplacer plus tard.

---

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec des TIFF à page unique ?**  
R : Absolument. Le moteur traite un TIFF à trame unique de la même façon ; vous obtiendrez simplement une ligne de texte.

**Q : Puis‑je traiter des fichiers PNG ou JPEG de la même manière ?**  
R : Oui—il suffit de changer l’extension du fichier. La méthode `Recognize` accepte tout format `System.Drawing.Image`.

**Q : Que faire si j’ai besoin du résultat OCR au format PDF plutôt qu’en texte brut ?**  
R : Définissez `OutputFormat = OcrOutputFormat.Pdf` et `ocrResult` contiendra un tableau d’octets PDF que vous pourrez écrire sur le disque.

---

## Conclusion

Vous disposez maintenant d’une solution complète, de bout en bout, pour **comment exécuter l'OCR** sur des fichiers TIFF multi‑pages en utilisant Aspose OCR en C#. En configurant le moteur, en chargeant l’image et en appelant `Recognize`, vous pouvez **extraire du texte à partir de TIFF**, **convertir le TIFF en texte**, et **reconnaître du texte à partir d’une image** avec seulement quelques lignes de code. N’hésitez pas à ajuster la langue, le format de sortie ou le traitement trame par trame pour répondre à vos besoins de traitement par lots.

Prêt pour l’étape suivante ? Essayez de combiner cette approche avec un service de surveillance de dossiers pour **effectuer automatiquement l'OCR sur des fichiers image** dès qu’ils arrivent dans un dossier de dépôt, ou intégrez la sortie dans un index de recherche pour une recherche plein texte instantanée. Les possibilités sont infinies, et le code que vous venez de voir constitue une base solide.

Si vous avez rencontré le moindre problème, laissez un commentaire ci‑dessous ou contactez‑moi sur GitHub. Bon codage, et profitez de la transformation de ces TIFF récalcitrants en texte interrogeable !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}