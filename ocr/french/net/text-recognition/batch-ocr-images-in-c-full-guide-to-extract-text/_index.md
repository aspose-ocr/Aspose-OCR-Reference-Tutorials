---
category: general
date: 2026-02-24
description: Effectuez rapidement la reconnaissance OCR par lots d'images avec Aspose.OCR
  en C#. Apprenez à lire les fichiers d’un répertoire, à reconnaître le texte d’une
  image et à convertir l’image en texte en quelques étapes.
draft: false
keywords:
- batch OCR images
- extract text from images
- read files from directory
- recognize text from image
- convert image to text
language: fr
og_description: Effectuez une reconnaissance OCR par lots d'images en C# avec Aspose.OCR.
  Ce tutoriel montre comment lire les fichiers d'un répertoire, reconnaître le texte
  d'une image et convertir l'image en texte de manière efficace.
og_title: OCR d'images en lot avec C# – Guide complet étape par étape
tags:
- C#
- OCR
- Aspose
title: OCR d'images par lots en C# – Guide complet pour extraire le texte
url: /fr/net/text-recognition/batch-ocr-images-in-c-full-guide-to-extract-text/
---

Check that we didn't translate variable names.

Check that we kept markdown formatting.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Traitement par lots d'images OCR en C# – Guide complet pour extraire du texte

Vous avez déjà eu besoin de **traitement par lots d'images OCR** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul—de nombreux développeurs rencontrent le même obstacle lorsqu'ils essaient pour la première fois de **extraire du texte d'images** en masse. La bonne nouvelle, c'est qu'avec quelques lignes de C# et Aspose.OCR, vous pouvez transformer un dossier rempli d'images en fichiers `.txt` bien organisés en un rien de temps.

Dans ce tutoriel, nous parcourrons l'ensemble du processus : lire les fichiers d'un répertoire, alimenter chaque image dans le moteur OCR, et enfin **convertir l'image en texte** dans des fichiers que vous pouvez indexer, rechercher ou injecter dans des pipelines en aval. À la fin, vous disposerez d'une application console autonome que vous pourrez intégrer à n'importe quelle solution .NET.

## Ce dont vous avez besoin

- **.NET 6+** (l'exemple se compile avec .NET 6, mais toute version récente fonctionne)
- **Aspose.OCR** package NuGet (`Install-Package Aspose.OCR`)
- Un dossier de fichiers image (`.png`, `.jpg`, etc.) que vous souhaitez traiter
- Visual Studio, Rider ou votre éditeur préféré

Aucun fichier de configuration supplémentaire, aucun service externe—juste du code C# pur qui s'exécute localement.

## Traitement par lots d'images OCR – Configuration du projet

Tout d'abord, créez un nouveau projet console :

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Cette commande crée un projet minimal et récupère la bibliothèque OCR. Une fois la restauration terminée, vous êtes prêt à ajouter la logique principale.

### Lire les fichiers d'un répertoire

Nous devons indiquer à notre application où se trouvent les images sources et où placer les fichiers texte résultants. L'utilisation de `System.IO` rend cela très simple.

```csharp
using System;
using System.IO;
using Aspose.OCR;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Define input and output folders
        string inputFolder  = @"C:\Images\ToProcess";   // <-- change to your source folder
        string outputFolder = @"C:\Images\OcrResults"; // <-- change to your target folder

        // 2️⃣ Ensure the output folder exists
        Directory.CreateDirectory(outputFolder);
```

> **Pourquoi cette étape est importante :** Si le répertoire de sortie n'existe pas, le programme lèvera une exception lorsqu'il tentera d'écrire un fichier `.txt`. `CreateDirectory` est idempotent — il ne fait rien si le dossier existe déjà, il est donc sûr de l'appeler à chaque exécution.

### Reconnaître le texte d'une image et convertir l'image en texte

Nous lançons maintenant le moteur OCR et parcourons chaque fichier trouvé. La boucle utilise `Directory.GetFiles` avec un joker (`*.*`) afin de récupérer *tous* les fichiers, mais vous pouvez restreindre le filtre à `*.png` ou `*.jpg` si vous le souhaitez.

```csharp
        // 3️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 4️⃣ Process each image file in the input folder
        foreach (var imagePath in Directory.GetFiles(inputFolder, "*.*", SearchOption.TopDirectoryOnly))
        {
            // 5️⃣ Recognise text from the current image
            var ocrResult = ocrEngine.RecognizeImage(imagePath);

            // 6️⃣ Save the recognised text to a .txt file in the output folder
            string textFilePath = Path.Combine(
                outputFolder,
                Path.GetFileNameWithoutExtension(imagePath) + ".txt");

            File.WriteAllText(textFilePath, ocrResult.Text);
        }

        Console.WriteLine("✅ All images processed. Check the output folder!");
    }
}
```

**Que se passe-t-il ici ?**  
- `ocrEngine.RecognizeImage(imagePath)` lit le bitmap, exécute l'algorithme OCR et renvoie un objet `OcrResult`.  
- `ocrResult.Text` contient la représentation en texte brut de tout ce que le moteur a pu lire.  
- `File.WriteAllText` crée un nouveau fichier (ou écrase un existant) avec le texte extrait.

C’est l’ensemble du pipeline **batch OCR images** en moins de 30 lignes de code.

## Astuces pro et cas limites

| Situation | Recommandation |
|-----------|----------------|
| Les images sont volumineuses ( > 5 Mo ) | Réduisez-les à une largeur d’environ 1500 px pour accélérer la reconnaissance sans perdre en précision. |
| Vous devez prendre en charge les PDF | Convertissez chaque page PDF en image d'abord (par ex., avec `Aspose.PDF`), puis alimentez‑la dans la même boucle. |
| Certains fichiers ne sont pas des images (ex. `.txt`) | Ajoutez un filtre simple : `if (!imagePath.EndsWith(".png") && !imagePath.EndsWith(".jpg")) continue;` |
| Vous souhaitez une prise en charge multilingue | Définissez `ocrEngine.Language = Language.English | Language.Spanish;` avant la boucle. |
| Vous avez besoin d'un rapport de progression | Écrivez `Console.WriteLine($"Processing {Path.GetFileName(imagePath)}...");` à l'intérieur du foreach. |

> **Astuce pro :** Enveloppez l’appel OCR dans un `try/catch`. Occasionnellement, une image corrompue provoquera une exception `RecognizeImage` ; la gérer empêche l'arrêt complet du lot.

## Résultat attendu

Après l'exécution du programme, le `outputFolder` contiendra un fichier `.txt` pour chaque image originale :

```
C:\Images\OcrResults\invoice1.txt
C:\Images\OcrResults\receipt_2024-01-15.txt
C:\Images\OcrResults\signage.png.txt   <-- note the .txt extension
```

Chaque fichier contient le texte brut extrait par le moteur, par exemple :

```
Invoice #12345
Date: 01/15/2024
Total: $1,250.00
Thank you for your business!
```

Vous pouvez maintenant injecter ces fichiers dans un index de recherche, exécuter une analyse de sentiment, ou simplement les archiver pour la conformité.

## Questions fréquentes

**Q : Cela fonctionne-t-il sous Linux ?**  
R : Absolument. Aspose.OCR est multiplateforme, et les API `System.IO` utilisées ici sont indépendantes du système d'exploitation. Il suffit d'ajuster les chemins de dossiers (`/home/user/images`).

**Q : Et si je dois **read files from directory** de façon récursive ?**  
R : Changez `SearchOption.TopDirectoryOnly` en `SearchOption.AllDirectories`. Soyez attentif aux problèmes d'autorisations dans les dossiers plus profonds.

**Q : Quelle est la précision de l'OCR ?**  
R : La précision dépend de la qualité de l'image, de la police et de la langue. Pour de meilleurs résultats, utilisez des scans haute résolution et des arrière‑plans propres. Vous pouvez également ajuster `ocrEngine.Config` pour activer la correction d'inclinaison ou la réduction du bruit.

## Conclusion

Vous venez d'apprendre comment **batch OCR images** en C# avec Aspose.OCR, depuis la lecture des fichiers d'un répertoire jusqu'à **recognize text from image** et enfin **convert image to text**, des fichiers que vous pouvez stocker ou traiter davantage. L'exemple complet et exécutable ci‑dessus devrait fonctionner immédiatement, et la section des astuces vous fournit une feuille de route pour mettre à l'échelle ou personnaliser la solution.

Prochaines étapes ? Essayez d'ajouter une interface simple avec WinForms ou WPF, intégrez la sortie à Azure Cognitive Search, ou expérimentez d'autres langues prises en charge par Aspose.OCR. Le ciel est la limite une fois que vous avez maîtrisé la boucle principale.

Bon codage, et que vos lots OCR soient sans erreur !  

![Diagram of batch OCR images process](batch-ocr-images-diagram.png "Batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}