---
category: general
date: 2026-04-08
description: Extraire du texte d’une image avec Aspose OCR en C#. Apprenez à prétraiter
  l’image pour l’OCR et à prétraiter l’image afin d’améliorer la précision.
draft: false
keywords:
- extract text from image
- preprocess image for ocr
- how to preprocess image
- Aspose OCR C#
- image preprocessing techniques
language: fr
og_description: Extraire du texte d’une image à l’aide d’Aspose OCR en C#. Ce guide
  montre comment prétraiter l’image pour l’OCR et comment la prétraiter pour obtenir
  les meilleurs résultats.
og_title: Extraire du texte d’une image avec Aspose OCR – Guide complet C#
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Extraire du texte d’une image avec Aspose OCR – Guide complet C#
url: /fr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image avec Aspose OCR – Guide complet C#  

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais les résultats étaient truffés d'erreurs ? Vous n'êtes pas seul—la plupart des développeurs rencontrent ce problème lorsque l'image source est inclinée, bruitée ou à faible contraste. La bonne nouvelle, c'est qu'une courte routine de prétraitement peut transformer une capture tremblotante en une source propre pour l'OCR, et Aspose OCR rend le tout très simple.

Dans ce tutoriel, nous parcourrons un exemple concret qui montre **comment prétraiter une image pour l'OCR** à l'aide des filtres intégrés d'Aspose OCR, puis **extraire du texte d'une image** avec seulement quelques lignes de C#. À la fin, vous disposerez d'un programme prêt à l'emploi, comprendrez pourquoi chaque filtre est important et saurez comment ajuster le pipeline pour vos propres cas particuliers.

## Ce dont vous avez besoin

- .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Framework 4.7+)
- Le package NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Une image d'exemple qui est inclinée, bruitée ou à faible contraste (par ex., `skewed_noisy.jpg`)
- Tout IDE de votre choix—Visual Studio, Rider ou VS Code convient  

Pas de bibliothèques natives supplémentaires, pas de services web, juste du C# pur.

## Étape 1 : Configurer le moteur OCR – Le point de départ pour extraire du texte

Première chose à faire : créer une instance `OcrEngine` et indiquer la langue à rechercher. L'anglais est le plus courant, mais vous pouvez remplacer `"en"` par `"fr"`, `"de"` etc.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void PreprocessAndOcr()
    {
        // 1️⃣ Initialize the OCR engine – this is where we define the language.
        var ocrEngine = new OcrEngine { Language = "en" };
```

**Pourquoi c'est important :** Le moteur possède des dictionnaires internes et des heuristiques spécifiques à chaque langue. Si vous omettez de définir la langue, Aspose utilise l'anglais par défaut, mais être explicite évite les surprises lorsque vous changez de locale plus tard.

## Étape 2 : Construire un pipeline de prétraitement – Comment prétraiter une image pour de meilleurs résultats

Nous ajoutons maintenant des filtres. Considérez-les comme une petite suite de retouche photo qui s'exécute automatiquement avant l'étape OCR. Les trois filtres ci‑dessous couvrent les problèmes les plus courants :

| Filtre | Ce qu'il corrige | Quand l'utiliser |
|--------|------------------|------------------|
| `DeskewFilter` | Fait pivoter l'image pour la rendre horizontale | Images prises sous un angle |
| `DenoiseFilter` | Réduit les taches aléatoires et le grain | Photos en faible lumière ou documents numérisés |
| `ContrastStretchFilter` | Augmente le contraste, faisant ressortir le texte sombre | Impressions fanées ou captures d'écran délavées |

```csharp
        // 2️⃣ Add preprocessing steps – this is the core of “how to preprocess image”.
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast
```

**Astuce :** L'ordre est important. D'abord le Deskew, puis le Denoise, et enfin le contraste. Si vous les inversez, vous risquez d'amplifier le bruit au lieu de le supprimer.

## Étape 3 : Exécuter l'OCR – Extraire enfin le texte d'une image

Une fois le pipeline prêt, transmettez au moteur le chemin de votre image. Aspose appliquera automatiquement les filtres, puis exécutera l'algorithme de reconnaissance.

```csharp
        // 3️⃣ Recognize text from the pre‑processed image.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");
```

Si le fichier n'est pas trouvé, vous obtiendrez une `FileNotFoundException` claire. C’est pourquoi nous recommandons d'utiliser des chemins absolus pendant le développement, puis de passer à des chemins relatifs ou à des valeurs de configuration en production.

## Étape 4 : Afficher le résultat – Voir ce que vous avez obtenu

L'objet `OcrResult` contient le texte brut, les scores de confiance, et même les boîtes englobantes de chaque mot. Pour une démonstration rapide, nous allons simplement afficher le texte dans la console.

```csharp
        // 4️⃣ Output the extracted text.
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Lorsque vous exécutez le programme, vous devriez voir quelque chose comme :

```
=== OCR Output ===
Invoice Number: 2023-0456
Date: 03/15/2024
Total: $1,234.56
```

Si la sortie apparaît brouillée, vérifiez la qualité de l'image ou expérimentez avec des filtres supplémentaires (par ex., `BinarizationFilter` pour les images binaires).

## Exemple complet fonctionnel – Copier‑coller et exécuter

Voici le programme complet et autonome. Remplacez simplement `YOUR_DIRECTORY/skewed_noisy.jpg` par le chemin réel de votre image de test.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Filters;
using System;

public static class ImageOcrDemo
{
    public static void Main()
    {
        PreprocessAndOcr();
    }

    public static void PreprocessAndOcr()
    {
        // Step 1: Create OCR engine and set language
        var ocrEngine = new OcrEngine { Language = "en" };

        // Step 2: Build preprocessing pipeline
        ocrEngine.Preprocess.Add(new DeskewFilter());               // correct skew
        ocrEngine.Preprocess.Add(new DenoiseFilter());             // reduce noise
        ocrEngine.Preprocess.Add(new ContrastStretchFilter());     // enhance contrast

        // Step 3: Recognize text from the pre‑processed image
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed_noisy.jpg");

        // Step 4: Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Sortie attendue** – La console affichera la représentation en texte brut de ce qui se trouve dans l'image. Si l'image contient un simple panneau indiquant « OpenAI », vous verrez exactement ce mot, sans symboles supplémentaires.

## Cas limites et comment ajuster le pipeline

### 1️⃣ Images très sombres

Si le filtre de contraste n'est pas suffisant, ajoutez en préfixe un `BrightnessCorrectionFilter` :

```csharp
ocrEngine.Preprocess.Add(new BrightnessCorrectionFilter(30)); // increase brightness by 30%
```

### 2️⃣ Documents multilingues

Définissez `Language = "en+fr"` (Aspose prend en charge les codes de langue séparés par des virgules) et ajoutez un `LanguageDetectionFilter` si vous souhaitez que le moteur détecte automatiquement.

### 3️⃣ Gros PDF convertis en images

Traiter un PDF de mille pages image par image peut être lent. Utilisez `Parallel.ForEach` pour exécuter l'OCR sur plusieurs images en parallèle, mais rappelez‑vous que le `OcrEngine` n'est pas thread‑safe — créez une instance distincte par thread.

```csharp
Parallel.ForEach(imagePaths, path =>
{
    var engine = new OcrEngine { Language = "en" };
    // add same filters...
    var result = engine.RecognizeImage(path);
    // store result...
});
```

### 4️⃣ Obtenir les boîtes englobantes

Si vous avez besoin de la localisation de chaque mot (par ex., pour les mettre en évidence), inspectez `ocrResult.Regions`. Chaque région contient des coordonnées `Rectangle` que vous pouvez utiliser dans une superposition UI.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

## Pièges courants (et comment les éviter)

- **Ignorer l'étape Deskew** – Même une inclinaison de 2 degrés peut faire chuter la confiance de 20 %. Ajoutez toujours `DeskewFilter` lorsque la source n'est pas parfaitement alignée.
- **Utiliser du JPEG avec une compression élevée** – Les artefacts de compression ressemblent à du bruit ; passez à PNG ou TIFF pour un meilleur OCR.
- **Coder en dur les chemins** – Les chemins relatifs fonctionnent localement, mais dans les pipelines CI/CD vous voudrez lire l'emplacement de l'image depuis la configuration ou les variables d'environnement.

## Tester votre configuration

1. Exécutez le programme avec une image nette et à fort contraste. Vous devriez obtenir un texte quasi parfait.  
2. Remplacez par une photo bruitée et inclinée. Vérifiez que la sortie s'améliore après l'ajout des trois filtres.  
3. Expérimentez en supprimant un filtre à la fois pour voir son impact — cela vous aide à comprendre *pourquoi* chaque étape est importante.

## Conclusion

Nous venons de démontrer comment **extraire du texte d'une image** avec Aspose OCR, et nous avons montré une méthode pratique pour **prétraiter une image pour l'OCR** qui fonctionne dans la plupart des scénarios réels. En enchaînant `DeskewFilter`, `DenoiseFilter` et `ContrastStretchFilter`, vous fournissez au moteur une toile propre, ce qui améliore considérablement la précision.

À partir de là, vous pouvez explorer des filtres plus avancés, gérer des documents multipages, ou intégrer les résultats OCR dans un index de recherche. Quoi que vous choisissiez, le schéma de base—initialiser, prétraiter, reconnaître et consommer—reste le même.

Prêt à passer au niveau supérieur ? Essayez d'ajouter un `BinarizationFilter` pour les numérisations noir et blanc, ou connectez la sortie à une base de données pour des PDF consultables. Bon codage, et que chaque image que vous soumettez à Aspose renvoie un texte net et lisible !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}