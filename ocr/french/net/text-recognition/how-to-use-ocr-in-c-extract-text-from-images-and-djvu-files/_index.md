---
category: general
date: 2026-04-04
description: Comment utiliser l’OCR rapidement et en toute sécurité. Apprenez à extraire
  du texte d’une image, à convertir un DJVU en texte et à charger une image pour l’OCR
  avec Aspose.OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: fr
og_description: Comment utiliser l'OCR en C# pour extraire du texte à partir de fichiers
  image et de documents DJVU. Tutoriel étape par étape avec le code complet.
og_title: Comment utiliser l'OCR en C# – Guide complet
tags:
- OCR
- C#
- Aspose
title: Comment utiliser l’OCR en C# – Extraire du texte à partir d’images et de fichiers
  DJVU
url: /fr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser l'OCR en C# – Extraire du texte à partir d'images et de fichiers DJVU

Vous vous êtes déjà demandé **comment utiliser l'OCR** pour extraire des mots d'une page numérisée sans les taper manuellement ? Vous n'êtes pas le seul. Dans de nombreux projets—que vous numérisiez de vieux livres ou extrayiez des données de reçus—obtenir du texte à partir d'une image est un problème quotidien. La bonne nouvelle ? Avec Aspose.OCR, vous pouvez le faire en quelques lignes, même lorsque la source est un fichier DJVU.

Dans ce guide, nous passerons en revue tout ce dont vous avez besoin pour **extraire du texte d'une image**, **charger une image pour l'OCR**, et même **convertir DJVU en texte** en utilisant C#. À la fin, vous disposerez d'une application console prête à l'emploi qui affiche le texte reconnu directement dans la console. Pas de mystère, pas de dépendances supplémentaires, juste du C# pur et Aspose.

## Ce que vous apprendrez

- Comment installer et référencer la bibliothèque Aspose.OCR.
- Le code exact nécessaire pour **charger une image pour l'OCR**, qu'il s'agisse d'un PNG, JPEG ou d'une page DJVU.
- Comment appeler le moteur et récupérer le résultat.
- Conseils pour gérer les gros documents et les pièges courants.
- Un exemple complet et exécutable que vous pouvez copier‑coller dans Visual Studio.

> **Prérequis :** .NET 6.0 ou ultérieur et une licence valide Aspose.OCR (ou un essai gratuit). Si vous n'avez pas encore la bibliothèque, récupérez‑la depuis NuGet avec `dotnet add package Aspose.OCR`.

## Comment utiliser l'OCR avec Aspose en C#

C'est l'étape principale où nous répondons réellement à la question **comment utiliser l'OCR** dans un projet C#. Le code ci‑dessous est un programme complet ; vous pouvez le coller dans une nouvelle application console et appuyer sur F5.

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Pourquoi cela fonctionne :**  
- `OcrEngine` est le point d'entrée ; il abstrait le travail lourd de prétraitement d'image, de détection de langue et de classification des caractères.  
- `ImageStream.FromFile` peut gérer de nombreux formats, y compris DJVU, ce qui signifie que vous pouvez **convertir DJVU en texte** sans étape de conversion supplémentaire.  
- `Recognize()` renvoie un objet `OcrResult` qui contient le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

L'exécution du programme affiche quelque chose comme :

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

C’est tout—votre première opération réussie d'**extraction de texte à partir de DJVU**.

![exemple d'utilisation de l'OCR](/images/ocr-demo.png "Capture d'écran montrant comment utiliser l'OCR dans une application console C#")

*Texte alternatif : « comment utiliser l'OCR » capture d'écran de la sortie console.*

## Charger une image pour l'OCR

Avant que le moteur puisse lire quoi que ce soit, vous devez **charger une image pour l'OCR** correctement. Aspose prend en charge la plupart des formats raster dès le départ, mais quelques astuces peuvent rendre la reconnaissance plus fluide :

- **Redimensionner les grandes images** à un maximum de 2000 px sur le côté le plus long. Les fichiers surdimensionnés augmentent l'utilisation de la mémoire et peuvent ralentir le moteur.
- **Convertir les images couleur en niveaux de gris** si vous remarquez des arrière‑plans bruyants. Utilisez `ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();`.
- **Définir le DPI manuellement** pour les numérisations à basse résolution (`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`).

Ces ajustements sont optionnels mais améliorent souvent la précision lorsque vous **extrayez du texte d'une image** comme des reçus numérisés.

## Extraire du texte d'une image – Bonnes pratiques

Lorsque vous travaillez avec des formats d'image typiques (PNG, JPEG, BMP), les étapes restent les mêmes, mais vous pouvez affiner le moteur :

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **La sélection de la langue** est importante. Si vous traitez des documents multilingues, définissez `ocrEngine.Language = Language.Multilingual;`.
- **RecognitionMode** peut être `Auto`, `Fast` ou `Accurate`. `Accurate` offre une meilleure qualité au prix de la vitesse—utilisez‑le pour les tâches d'archivage.

## Convertir DJVU en texte – Gestion des fichiers multi‑pages

Les fichiers DJVU contiennent souvent plusieurs pages. Aspose traite chaque page comme un flux d'image distinct, vous pouvez donc les parcourir en boucle :

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**Pourquoi boucler ?**  
Les fichiers DJVU sont essentiellement une pile d'images. En itérant sur chaque page, vous **extrayez du texte à partir de DJVU** dans l'ordre, en préservant le flux du document original.

## Pièges courants et astuces pro

| Problème | Pourquoi cela se produit | Solution |
|------|----------------|-----|
| **Caractères indésirables** | DPI faible ou compression importante | Agrandir l'image, définir `ocrEngine.Image.DpiX/Y = 300` |
| **Traitement lent** | Utilisation du mode `Accurate` sur de très gros fichiers | Passer au mode `Fast` pour les traitements en masse |
| **Support de langue manquant** | La langue par défaut est uniquement l'anglais | Charger des packs de langues supplémentaires (`ocrEngine.Language = Language.Spanish;`) |
| **Erreurs de mémoire insuffisante** | Chargement de nombreuses pages haute résolution en même temps | Traiter les pages une par une et libérer les ressources (`ocrEngine.Dispose();`) |

Une **astuce pro** rapide : appelez toujours `ocrEngine.Dispose()` après avoir terminé avec une page. Cela libère les ressources natives et empêche les fuites de mémoire subtiles qui peuvent faire planter les services de longue durée.

## Tester votre pipeline OCR

Pour vérifier que tout fonctionne, essayez ces vérifications simples :

1. **Afficher la longueur** de la chaîne reconnue : `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`
2. **Comparer avec le texte connu** en utilisant une bibliothèque de diff simple si vous avez une vérité de référence.
3. **Enregistrer les scores de confiance** (`ocrResult.Confidence`) pour détecter automatiquement les pages de mauvaise qualité.

Si la confiance est constamment inférieure à 0,7, revisitez les étapes de prétraitement d'image mentionnées précédemment.

## Prochaines étapes

Maintenant que vous savez **comment utiliser l'OCR**, envisagez d'étendre votre flux de travail :

- **Traitement par lots** : encapsulez la boucle dans un `Parallel.ForEach` pour accélérer les grandes collections.
- **Exporter en PDF** : utilisez Aspose.PDF pour intégrer le texte reconnu comme couche cachée pour des PDF recherchables.
- **Intégrer avec l'IA** : injectez les chaînes extraites dans un modèle de langage pour la synthèse ou l'extraction d'entités.

Toutes ces options s'appuient sur la même base que vous venez de mettre en place, et chaque étape bénéficie des mêmes principes d'**extraction de texte d'une image** que nous avons abordés.

Essayez, ajustez les paramètres pour vos documents spécifiques, et vous transformerez des pages numérisées en texte consultable en un rien de temps. Vous avez des questions ou un fichier récalcitrant ? Laissez un commentaire—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}