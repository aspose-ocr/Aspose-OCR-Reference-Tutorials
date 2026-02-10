---
category: general
date: 2026-02-09
description: Extrait rapidement du texte d'images avec C# en définissant le parallélisme
  maximal pour l'OCR par lots – apprenez à convertir des pages numérisées, à gérer
  l'OCR de plusieurs images et à lire efficacement le texte des PNG.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: fr
og_description: extraire du texte d'images en C# en définissant le parallélisme maximal.
  Ce tutoriel montre comment convertir des pages numérisées, exécuter plusieurs OCR
  d'images et lire le texte PNG avec Aspose OCR.
og_title: Extraire le texte des images PNG avec C# – Guide complet d’OCR par lots
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: extraire le texte des images PNG avec C# – OCR par lots avec Aspose OCR
url: /fr/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extraire du texte d'images à partir de PNG avec C# – OCR par lot avec Aspose OCR

Vous avez déjà eu besoin d'**extraire du texte d'images** d'un dossier de PNG numérisés mais vous êtes resté bloqué sur la question « comment le rendre rapide ? »? Vous n'êtes pas seul. Dans de nombreux projets réels, les développeurs doivent **définir le parallélisme maximal** afin que des dizaines de pages soient traitées en quelques secondes au lieu de minutes.  

Dans ce guide, nous parcourrons un exemple complet et exécutable qui **convertit des pages numérisées**, exécute **un OCR sur plusieurs images**, et enfin **lit le texte des PNG** sans effort. Pas de liens vagues « voir la documentation » — seulement du code que vous pouvez copier‑coller, des explications sur l'importance de chaque ligne, et des astuces pour éviter les pièges habituels.

> **Astuce :** Si vous utilisez déjà Aspose OCR ailleurs, vous remarquerez que la même classe `OcrEngine` apparaît ici, mais nous ajusterons sa configuration pour un véritable traitement parallèle.

---

## Ce dont vous avez besoin

- **.NET 6+** (ou .NET Framework 4.6+). L'API fonctionne de la même façon, mais les runtimes plus récents offrent une meilleure gestion des threads.  
- **Aspose.OCR for .NET** – à installer via NuGet : `Install-Package Aspose.OCR`.  
- Un dossier contenant quelques scans PNG (`page1.png`, `page2.png`, …).  
- Un IDE ou éditeur avec lequel vous êtes à l'aise (Visual Studio, Rider, VS Code…).

C’est tout. Aucun service supplémentaire, aucune clé cloud, juste un traitement local pur.

---

## extraire du texte d'images – Définir le parallélisme maximal pour l'OCR par lot

Lorsque vous lancez l'OCR sur plusieurs fichiers, le moteur utilise, par défaut, un seul thread. C’est sûr mais extrêmement lent. En configurant `MaxDegreeOfParallelism`, vous indiquez au moteur combien de threads il peut créer simultanément.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Pourquoi 4 ?**  
Quatre est un bon compromis sur la plupart des ordinateurs portables modernes — assez de cœurs pour occuper le CPU, mais pas tant que vous affamez les autres processus. Si vous exécutez cela sur un serveur avec 16 cœurs, augmentez le nombre à 12 ou 14 pour un gain de vitesse notable.

---

## Convertir des pages numérisées – Construire la collection de flux d'images

Aspose attend chaque image sous forme d'`ImageStream`. L'utilitaire `FromFile` lit le fichier, le garde en mémoire, et le transmet au moteur OCR. Vous pouvez également fournir un `MemoryStream` si vos images proviennent d'une base de données ou d'une réponse HTTP.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Cas limite :** Si un fichier est manquant ou corrompu, `FromFile` lèvera une `FileNotFoundException`. Enveloppez la construction dans un `try/catch` si vous prévoyez des entrées peu fiables.

---

## OCR multiple images – Exécuter l'OCR par lot

C’est maintenant le travail lourd qui commence. `RecognizeBatch` crée jusqu'au nombre de threads que vous avez défini précédemment, traite chaque image, et renvoie une liste d'objets `OcrResult`.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

En coulisses, chaque thread charge son image, exécute le réseau neuronal, et extrait le texte brut. L'ordre des résultats correspond à l'ordre de la liste d'entrée, vous pouvez donc mapper en toute sécurité page 1 → résultat 0, etc.

---

## lire le texte PNG – Afficher le contenu extrait

Enfin, nous parcourons les résultats et affichons le texte brut dans la console. C’est ici que vous pouvez rediriger la sortie vers un fichier, une base de données, ou même un service NLP en aval.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Sortie console attendue

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Si vous voyez des sections vides, vérifiez que les PNG ne sont pas des images entièrement blanches — l'OCR a besoin de contraste.

---

## Conseils pratiques & pièges courants

| Situation | Que faire |
|-----------|-----------|
| **Pression mémoire** sur de gros lots | Traitez les images par blocs de 10‑20 fichiers, puis appelez `GC.Collect()` si vous remarquez des pics. |
| **Détection de langue incorrecte** | Définissez `ocrEngine.Configuration.Language = OcrLanguage.English;` (ou votre langue cible) avant d’appeler `RecognizeBatch`. |
| **Performance lente malgré le parallélisme** | Vérifiez que votre SSD ne limite pas les I/O ; lisez d'abord tous les fichiers en mémoire (comme nous le faisons avec `ImageStream.FromFile`). |
| **Caractères manquants** | Augmentez `ocrEngine.Configuration.DPI = 300;` pour un traitement à plus haute résolution. |

---

## Étendre l'exemple – De PNG à PDF ou DOCX

Si vous devez finalement **convertir des pages numérisées** en PDF recherchables, il suffit d’alimenter la même `ocrResults[i].PlainText` dans une bibliothèque PDF (par ex., Aspose.PDF) et de superposer le texte comme une couche invisible. La même astuce de parallélisme fonctionne également là‑bas.

---

## Code source complet (prêt à copier‑coller)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Enregistrez ceci sous le nom `BatchExample.cs`, exécutez `dotnet run`, et observez votre console se remplir du texte qui était auparavant caché dans ces scans PNG.

---

## Résumé visuel

![extract text images example](images/ocr-batch.png){alt="exemple d'extraction d'images texte"}

Le diagramme montre le flux : **Fichiers PNG → collection ImageStream → OcrEngine (parallélisme maximal) → résultats OCR → Console / stockage en aval**.

---

## Conclusion

Vous disposez maintenant d’une recette solide, de bout en bout, pour **extraire du texte d'images** en C# tout en **définissant le parallélisme maximal**, **convertissant des pages numérisées**, gérant **l'OCR sur plusieurs images**, et **lisant le texte PNG** efficacement. Le code est autonome, les explications couvrent à la fois le « comment » et le « pourquoi », et les astuces vous évitent les maux de tête courants.

Et après ? Essayez de remplacer la liste de PNG par une boucle dynamique `Directory.GetFiles`, expérimentez différents nombres de threads, ou alimentez la sortie dans un PDF recherchable. Le même schéma s’étend à des centaines de pages avec à peine une ligne de code supplémentaire.

Des questions ou un cas limite difficile ? Laissez un commentaire ci‑dessous, et bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}