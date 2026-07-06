---
category: general
date: 2026-02-14
description: Apprenez comment éliminer la distorsion d’une image, prétraiter l’image
  pour l’OCR, réduire le bruit dans l’image et extraire le texte d’une image en utilisant
  Aspose OCR en C#.
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: fr
og_description: Supprimer l'inclinaison de l'image, prétraiter l'image pour l'OCR
  et extraire le texte de l'image avec un tutoriel C# pas à pas utilisant Aspose OCR.
og_title: Supprimer l’inclinaison de l’image – Guide complet de prétraitement OCR
tags:
- OCR
- CSharp
- ImageProcessing
title: Supprimer l’inclinaison de l’image – Guide complet de prétraitement OCR
url: /fr/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Supprimer l’inclinaison d’une image – Guide complet de pré‑traitement OCR

Vous avez déjà eu besoin de **supprimer l’inclinaison d’une image** avant de l’alimenter à un moteur OCR ? Vous n’êtes pas le seul—les documents numérisés, les photos de reçus ou les captures d’écran arrivent souvent inclinés, et ce petit angle peut saboter la reconnaissance de texte.  

Bonne nouvelle ? Avec une poignée de filtres Aspose OCR, vous pouvez redresser, débruiter, augmenter le contraste, puis **extraire le texte d’une image** dans un pipeline unique et fluide. Dans ce guide, nous parcourrons l’ensemble du processus, du chargement d’une image inclinée à **reconnaître le texte d’un document** et afficher le résultat.

---

## Ce que vous allez créer

À la fin de ce tutoriel, vous disposerez d’une application console C# prête à l’emploi qui :

1. **Supprime l’inclinaison d’une image** à l’aide de `DeskewFilter`.
2. **Réduit le bruit dans l’image** avec `DenoiseFilter`.
3. **Prétraite l’image pour l’OCR** en augmentant le contraste.
4. **Reconnaît le texte d’un document** via le `Engine` d’Aspose OCR.
5. **Extrait le texte d’une image** et l’affiche dans la console.

Aucun service externe, seulement le package NuGet Aspose OCR et quelques lignes de code.

---

## Prérequis

- .NET 6.0 SDK ou version ultérieure (le code fonctionne également avec .NET Core et .NET Framework).  
- Visual Studio 2022 ou tout éditeur de votre choix.  
- Aspose.OCR pour .NET installé (`dotnet add package Aspose.OCR`).  
- Une image d’exemple (`skewed_noisy.jpg`) placée dans un dossier que vous pouvez référencer.

Si vous avez tout cela, lançons‑nous.

---

## Étape 1 : Charger l’image source

La première chose dont nous avons besoin est un `ImageStream` qui pointe vers le fichier que nous voulons nettoyer.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Pourquoi c’est important :** `ImageStream` abstrait le bitmap sous‑jacent, permettant aux filtres Aspose de fonctionner sans que vous ayez à gérer les données brutes des pixels.

---

## Étape 2 : Construire un pipeline de pré‑traitement (Supprimer l’inclinaison & Réduire le bruit)

Au lieu d’appeler chaque filtre séparément, Aspose vous permet de les chaîner dans un `ImageProcessingPipeline`. Cela garde le code propre et garantit que les opérations s’exécutent dans le bon ordre.

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### Pourquoi l’ordre est important

1. **Deskew d’abord** – Redresser l’image avant le débruitage empêche le filtre de bruit de traiter les bords inclinés comme des artefacts.  
2. **Denoise ensuite** – Une fois l’image nivelée, l’algorithme peut mieux différencier le signal du grain.  
3. **Boost du contraste en dernier** – Améliorer le contraste après que l’image soit propre maximise la lisibilité pour l’OCR sans amplifier le bruit.

---

## Étape 3 : Appliquer le pipeline et obtenir une image nettoyée

Nous exécutons maintenant le pipeline sur le flux original.

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

À ce stade, l’image est redressée, débruitée et possède un contraste plus élevé—parfait pour l’OCR.

---

## Étape 4 : Initialiser le moteur OCR et reconnaître le texte

Avec une image impeccable en main, nous pouvons enfin la transmettre à Aspose OCR.

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **Astuce :** Si vous avez besoin d’un réglage spécifique à une langue, `Engine` accepte une propriété `Language` (par ex., `ocrEngine.Language = Language.English;`). Pour la plupart des documents basés sur l’alphabet latin, la valeur par défaut fonctionne bien.

---

## Étape 5 : Afficher le texte extrait

Un simple `Console.WriteLine` affiche le résultat.

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

Lorsque vous exécutez le programme, vous devriez voir le contenu textuel de `skewed_noisy.jpg` affiché dans le terminal—propre, lisible et prêt pour le traitement en aval.

---

## Exemple complet fonctionnel

Ci‑dessous se trouve le programme complet, prêt à copier‑coller. Enregistrez‑le sous `Program.cs`, remplacez `YOUR_DIRECTORY` par le chemin réel, et exécutez `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Sortie attendue** (exemple pour un reçu simple) :

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

Si la sortie apparaît brouillée, vérifiez que le chemin de l’image est correct et que le fichier source contient réellement du texte lisible.

---

## Questions fréquentes & cas particuliers

### Et si l’image est tournée de 90° au lieu d’une légère inclinaison ?

`DeskewFilter` gère les angles mineurs (±15°). Pour des rotations complètes, appelez `new RotateFilter { Angle = 90 }` avant l’étape de deskew.

### Mon image est au format PNG—cela change‑t‑il quelque chose ?

Non. `ImageStream.FromFile` détecte automatiquement le format, donc PNG, JPEG, BMP ou TIFF fonctionnent tous de la même façon.

### Comment puis‑je ajuster la force de réduction du bruit ?

`DenoiseFilter` expose une propriété `Strength` (0‑100). Des valeurs plus élevées suppriment davantage le grain mais peuvent flouter les détails fins. Expérimentez avec des valeurs autour de 30‑50 pour les documents riches en texte.

### J’ai besoin de traiter un lot de fichiers—puis‑je réutiliser le pipeline ?

Absolument. Créez le `processingPipeline` une fois, puis bouclez sur chaque fichier :

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

Réutiliser la même instance `Engine` améliore également les performances.

---

## Astuces pro pour un OCR prêt pour la production

- **Mettez en cache le pipeline** : Instancier les filtres à plusieurs reprises peut être coûteux dans les scénarios à haut débit.  
- **Définissez la langue OCR** : `ocrEngine.Language = Language.Spanish;` pour les documents non anglais.  
- **Gérez les résultats vides** : Vérifiez toujours `ocrResult.Text?.Length > 0` avant de poursuivre.  
- **Enregistrez les images intermédiaires** : Sauvegarder `cleanedImage` sur disque (`cleanedImage.Save("debug.png");`) vous aide à affiner les paramètres des filtres.

---

## Conclusion

Nous avons montré comment **supprimer l’inclinaison d’une image**, **réduire le bruit dans l’image**, et **prétraiter l’image pour l’OCR** en utilisant le puissant pipeline de filtres d’Aspose OCR, puis **reconnaître le texte d’un document** et enfin **extraire le texte d’une image**. L’ensemble du flux de travail tient en moins de 50 lignes de C# et est facile à étendre pour le traitement par lots, les modèles de langue personnalisés ou des filtres supplémentaires.

Prêt pour l’étape suivante ? Essayez d’ajouter un `BinarizeFilter` pour forcer la sortie en noir et blanc, ou expérimentez différents niveaux de `ContrastBoostFilter` pour voir comment ils affectent la précision de la reconnaissance. Plus vous jouerez avec le pipeline, mieux vous comprendrez comment chaque filtre contribue à un résultat OCR propre.

Bon codage, et que vos images restent toujours droites !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}