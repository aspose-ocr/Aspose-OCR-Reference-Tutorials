---
category: general
date: 2026-03-29
description: Comment utiliser l’OCR avec Aspose pour extraire du texte à partir de
  fichiers PNG et convertir les images en texte. Apprenez l’OCR asynchrone étape par
  étape en C#.
draft: false
keywords:
- how to use OCR
- extract text from png
- convert images to text
- extract text from images
language: fr
og_description: Comment utiliser l’OCR avec Aspose en C# pour extraire du texte de
  fichiers PNG. Ce guide vous accompagne à travers l’OCR asynchrone, le code et les
  astuces.
og_title: Comment utiliser l'OCR en C# – Extraire du texte à partir d'images PNG
tags:
- OCR
- C#
- Aspose
title: Comment utiliser l'OCR en C# – Extraire rapidement du texte d'images PNG
url: /fr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-png-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en C# – Extraire rapidement du texte d'images PNG

Vous vous êtes déjà demandé **comment utiliser l'OCR** pour extraire du texte d'une poignée de captures d'écran PNG ? Peut‑être avez‑vous des reçus numérisés, des factures ou des maquettes d'interface et vous avez besoin de ce texte dans un format interrogeable. Bonne nouvelle ? Avec Aspose.OCR vous pouvez convertir des images en texte en seulement quelques lignes de code C# asynchrone.  

Dans ce tutoriel, nous vous montrerons exactement comment extraire du texte de fichiers PNG, expliquerons pourquoi chaque étape est importante, et vous fournirons un programme prêt à l'emploi qui affiche le texte reconnu pour chaque page. À la fin, vous serez capable de **extraire du texte d'images** sans devoir fouiller dans la documentation.

## Ce que vous apprendrez

- Installer et référencer le package NuGet Aspose.OCR.  
- Initialiser le moteur OCR et définir la langue (anglais dans cet exemple).  
- Fournir un tableau de fichiers PNG à `RecognizeImagesAsync` pour un traitement rapide et non bloquant.  
- Parcourir les objets `OcrResult` et afficher les chaînes extraites.  

Pas de services externes, pas de rappels compliqués—juste du C# propre et asynchrone qui fonctionne sur .NET 6+.

---

## Prérequis

| Exigence | Raison |
|----------|--------|
| .NET 6 SDK (or later) | Fonctionnalités modernes du langage comme `async Main`. |
| Visual Studio 2022 or VS Code | IDE pour compiler et exécuter le code. |
| Aspose.OCR NuGet package (`Aspose.OCR`) | Fournit la classe `OcrEngine` utilisée dans l'exemple. |
| A few PNG images (`page1.png`, `page2.png`, …) | Fichiers d'entrée pour le processus OCR. |

Si vous avez déjà un projet .NET, exécutez simplement `dotnet add package Aspose.OCR`. Sinon, créez une nouvelle application console avec `dotnet new console -n OcrDemo`.

## Étape 1 : Installer Aspose.OCR et configurer le projet

Tout d'abord, ajoutez la bibliothèque OCR à votre projet :

```bash
dotnet add package Aspose.OCR
```

Pourquoi c'est important : Aspose.OCR regroupe le moteur OCR natif, les packs de langues et une API simple. En l'obtenant via NuGet, vous assurez la compatibilité des versions et les mises à jour automatiques.

## Étape 2 : Initialiser le moteur OCR et choisir une langue

Le moteur doit savoir quelle langue rechercher. L'anglais est le plus courant, mais vous pouvez remplacer par `Language.Spanish`, `Language.French`, etc.

```csharp
using Aspose.OCR;

// ...

// Step 2: Create the engine and set the language to English
var ocrEngine = new OcrEngine
{
    Language = Language.English   // Change this if you need a different language
};
```

> **Astuce :** Toujours définir explicitement la langue ; laisser la valeur par défaut peut réduire la précision et augmenter le temps de traitement.

## Étape 3 : Préparer la liste des fichiers PNG

Vous pouvez fournir un seul fichier ou un tableau. Fournir un tableau permet au moteur de les traiter par lots de façon asynchrone, ce qui est idéal pour une poignée de pages.

```csharp
// Step 3: Define the image files you want to process
string[] imagePaths = { "page1.png", "page2.png", "page3.png" };
```

Si vos images se trouvent dans un sous‑dossier, préfixez simplement le chemin relatif (`"images/page1.png"`). Le moteur lèvera une `FileNotFoundException` claire si un chemin est incorrect—vérifiez donc les noms de fichiers.

## Étape 4 : Exécuter l'OCR asynchrone sur toutes les images

La méthode `RecognizeImagesAsync` renvoie un tableau de `OcrResult`. Comme elle est asynchrone, votre interface (ou console) reste réactive pendant que l'OCR s'exécute en arrière‑plan.

```csharp
// Step 4: Perform async OCR on every image
OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);
```

**Pourquoi asynchrone ?**  
Si vous intégrez l'OCR dans une API web ou une application de bureau, vous ne voulez pas que le thread se bloque pendant que le moteur analyse chaque pixel. `await` libère le thread dans le pool de threads, améliorant la scalabilité.

## Étape 5 : Afficher le texte extrait pour chaque page

Maintenant que nous avons les résultats, parcourez-les et affichez le texte reconnu. La propriété `Text` contient la sortie en texte brut, prête pour un traitement ultérieur (par ex., sauvegarde dans une base de données).

```csharp
// Step 5: Output the recognized text for every page
for (int i = 0; i < ocrResults.Length; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

### Sortie attendue

En supposant que `page1.png` contienne « Invoice #12345 » et que `page2.png` contienne « Total : $89.99 », vous verrez quelque chose comme :

```
--- Page 1 ---
Invoice #12345
Date: 03/28/2026
--- Page 2 ---
Total: $89.99
Paid by: Credit Card
```

Si l'OCR ne trouve aucun texte, la propriété `Text` sera une chaîne vide—gérez ce cas dans le code de production en vérifiant `string.IsNullOrWhiteSpace`.

## Exemple complet fonctionnel

Ci‑dessus se trouve le programme complet que vous pouvez copier‑coller dans `Program.cs`. Il inclut toutes les directives `using`, le `Main` asynchrone, et des commentaires qui clarifient chaque étape.

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    // Async Main is supported from C# 7.1 onward
    static async Task Main()
    {
        // Step 1: Initialize the OCR engine and set the language to English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Step 2: Define the image files to be processed
        string[] imagePaths = { "page1.png", "page2.png", "page3.png" };

        // Step 3: Perform asynchronous OCR on all images
        OcrResult[] ocrResults = await ocrEngine.RecognizeImagesAsync(imagePaths);

        // Step 4: Output the recognized text for each page
        for (int i = 0; i < ocrResults.Length; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].Text);
        }
    }
}
```

Enregistrez le fichier, placez vos PNG à côté de l'exécutable (ou ajustez les chemins), puis exécutez :

```bash
dotnet run
```

Vous devriez voir le texte extrait affiché dans la console, confirmant que vous avez réussi à **convertir des images en texte**.

## Gestion des cas limites courants

| Situation | Action |
|-----------|--------|
| **Low‑resolution PNG** | Augmenter `ocrEngine.ImageProcessingOptions.Dpi` avant la reconnaissance. |
| **Multiple languages** | Définir `ocrEngine.Language = Language.English | Language.Spanish;` (OU bitwise). |
| **Large batch (hundreds of files)** | Traiter par lots (par ex., 20 fichiers par appel `RecognizeImagesAsync`) pour éviter les pics de mémoire. |
| **Need the confidence score** | Utiliser `ocrResults[i].Confidence` (un float entre 0 et 1) pour filtrer les résultats de faible qualité. |

Ces ajustements maintiennent votre pipeline OCR robuste, surtout lorsque vous passez d'une démonstration à la production.

## Bonus : Enregistrer les résultats dans un fichier texte

Si vous préférez une copie persistante plutôt que la sortie console, ajoutez un petit utilitaire :

```csharp
using System.IO;

// After the for‑loop:
File.WriteAllLines("OcrOutput.txt", ocrResults.Select(r => r.Text));
Console.WriteLine("All pages saved to OcrOutput.txt");
```

Vous avez maintenant un fichier unique qui **extrait du texte d'images** pour le traitement en aval—parfait pour l'indexation, la recherche ou l'alimentation d'un modèle de langage.

## Conclusion

Nous avons parcouru **comment utiliser l'OCR** en C# avec Aspose pour **extraire du texte de fichiers PNG** et **convertir des images en texte** efficacement. L'approche asynchrone garantit que votre application reste réactive, tandis que l'API simple rend le code lisible et maintenable.  

Testez-le avec vos propres documents, expérimentez différentes langues, et peut‑être même enchaînez la sortie dans un index de recherche ou un service de résumé. Le ciel est la limite quand vous pouvez transformer de façon fiable des images en chaînes interrogeables.

### Prochaines étapes et sujets associés

- **Extraire du texte d'images** dans d'autres formats (JPEG, TIFF) – il suffit de changer les extensions de fichier.  
- **Traitement par lots avec Parallel.ForEach** pour des charges de travail massives.  
- **Nettoyage post‑OCR** à l'aide d'expressions régulières pour normaliser les dates, montants ou identifiants.  
- **Intégrer avec Azure Cognitive Services** si vous avez besoin d'un OCR basé sur le cloud avec des fonctionnalités supplémentaires.  

N'hésitez pas à laisser un commentaire si vous rencontrez des problèmes, ou à partager comment vous avez étendu ce flux de base. Bon codage !   (Image: ![Capture d'écran du résultat OCR montrant le texte extrait](/images/ocr-result.png){.align-center alt="exemple de sortie d'utilisation de l'OCR"} )

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}