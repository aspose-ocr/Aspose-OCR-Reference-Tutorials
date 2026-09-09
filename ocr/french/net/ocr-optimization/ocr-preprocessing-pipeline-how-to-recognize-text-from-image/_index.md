---
category: general
date: 2026-01-02
description: Apprenez à créer un pipeline de prétraitement OCR qui redresse automatiquement
  l'image, prétraite l'image pour l'OCR et lit le texte d'un JPG avec Aspose.OCR –
  guide étape par étape.
draft: false
keywords:
- ocr preprocessing pipeline
- recognize text from image
- auto deskew image
- preprocess image for ocr
- read text from jpg
language: fr
og_description: Découvrez le pipeline de prétraitement OCR qui redresse automatiquement
  les images et vous permet de reconnaître le texte à partir de fichiers image tels
  que jpg. Code complet, explications et astuces.
og_title: Pipeline de prétraitement OCR – Guide complet C#
tags:
- OCR
- C#
- Image Processing
title: pipeline de prétraitement OCR – Comment reconnaître du texte à partir d’une
  image en C#
url: /fr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# pipeline de prétraitement OCR – Guide complet C#

Avez‑vous déjà eu du mal à **reconnaître du texte à partir d'images** qui sont de travers, bruyantes ou simplement difficiles à lire ? Vous n'êtes pas seul. Dans de nombreux projets réels, la photo brute obtenue d'un scanner ou d'un appareil photo de téléphone a besoin d'un peu de soins avant que le moteur OCR puisse faire son travail.  

C'est là qu'intervient un **pipeline de prétraitement OCR**. En redressant automatiquement l'image, en réduisant les taches de fond et en la nettoyant, vous augmentez considérablement la précision. Dans ce tutoriel, nous passerons en revue un exemple complet qui **prétraite l'image pour l'OCR**, redresse automatiquement l'image, et enfin **lit le texte d'un jpg** en utilisant Aspose.OCR.

> **Ce que vous en retirerez :** une application console C# prête à l'emploi qui charge un JPG incliné et bruyant, le fait passer à travers un pipeline de prétraitement intelligent, et affiche le texte extrait dans la console.

## Prérequis

- .NET 6 SDK ou version ultérieure (le code se compile également avec .NET Core)
- Visual Studio 2022 ou tout IDE de votre choix
- Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`)
- Une image d'exemple telle que `skewed_noisy.jpg` placée dans un dossier que vous pouvez référencer

Aucune autre bibliothèque externe n'est requise ; tout le reste se trouve dans Aspose.OCR.

---

## Étape 1 – Configurer le projet et charger votre image

Tout d'abord, créez un nouveau projet console et ajoutez la référence Aspose.OCR. Puis chargez l'image que vous souhaitez traiter.

```csharp
using Aspose.OCR;
using System.Drawing;

class PreprocessExample
{
    static void Main()
    {
        // Load the image that needs OCR
        var imagePath = "YOUR_DIRECTORY/skewed_noisy.jpg";
        var image = new Bitmap(imagePath);
```

> **Pourquoi c'est important :** La classe `Bitmap` nous donne un accès direct aux pixels, ce dont le moteur OCR a besoin pour son étape de prétraitement. Si le chemin est incorrect, vous obtiendrez une `FileNotFoundException`, alors vérifiez bien l'emplacement.

---

## Étape 2 – Créer l'instance du moteur OCR

Ensuite, instanciez le `OcrEngine`. Cet objet pilotera l'ensemble du **pipeline de prétraitement OCR**.

```csharp
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Astuce :** Vous pouvez réutiliser le même `OcrEngine` pour plusieurs images ; il suffit de réinitialiser les `RecognitionOptions` à chaque fois.

---

## Étape 3 – Configurer les paramètres de prétraitement (le cœur du pipeline)

Ici, nous activons les deux fonctionnalités les plus puissantes : **auto redressement d'image** et **réduction du bruit**. Les deux font partie du pipeline qui prépare l'image pour une extraction de texte précise.

```csharp
        // Configure recognition options with the new preprocessing pipeline
        var recognitionOptions = new RecognitionOptions
        {
            Preprocess = new PreprocessSettings
            {
                EnableSmartDeskew = true,          // Auto‑detect and correct rotation
                EnableNoiseReduction = true,      // Apply AI‑based denoising
                NoiseReductionLevel = NoiseLevel.Medium
            },
            Language = Language.English
        };
```

> **Comment ça fonctionne :**  
> - `EnableSmartDeskew` examine les angles de base de l'image et la fait pivoter à 0°, ce qui est crucial pour les scans inclinés.  
> - `EnableNoiseReduction` exécute un filtre IA léger qui supprime les taches sans effacer les caractères faibles.  
> - `NoiseReductionLevel` vous permet d'échanger vitesse contre qualité ; `Medium` est un bon compromis pour la plupart des JPG.

---

## Étape 4 – Exécuter l'OCR et capturer le résultat

Nous transmettons maintenant l'image et les options au moteur. La méthode renvoie un objet `OcrResult` contenant la chaîne extraite et les scores de confiance.

```csharp
        // Perform OCR on the image using the configured options
        var ocrResult = ocrEngine.Recognize(image, recognitionOptions);
```

> **Cas limite :** Si l'image est complètement vide, `ocrResult.Text` sera une chaîne vide. Vous pourriez vouloir vérifier `ocrResult.HasText` avant de poursuivre dans du code de production.

---

## Étape 5 – Afficher le texte reconnu

Enfin, imprimez le résultat dans la console. Cela montre que nous pouvons **reconnaître du texte à partir d'images** en seulement quelques lignes de code.

```csharp
        // Output the recognized text
        System.Console.WriteLine("=== Extracted Text ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

**Sortie attendue (exemple) :**

```
=== Extracted Text ===
Invoice #12345
Date: 01/01/2024
Total: $1,250.00
Thank you for your business!
```

Si l'image était bruyante ou mal orientée, vous remarqueriez des caractères illisibles. Grâce au **pipeline de prétraitement OCR**, ces problèmes sont considérablement réduits.

---

## Étape 6 – Exemple complet fonctionnel (prêt à copier‑coller)

Voici le fichier source complet, prêt à être compilé. Remplacez `YOUR_DIRECTORY` par le chemin réel vers votre JPG.

```csharp
using Aspose.OCR;
using System.Drawing;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Load the image that needs OCR
        var imagePath = "YOUR_DIRECTORY/skewed_noisy.jpg";
        var image = new Bitmap(imagePath);

        // 2️⃣ Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // 3️⃣ Configure the preprocessing pipeline (auto deskew + noise reduction)
        var recognitionOptions = new RecognitionOptions
        {
            Preprocess = new PreprocessSettings
            {
                EnableSmartDeskew = true,          // Auto‑detect and correct rotation
                EnableNoiseReduction = true,      // AI‑based denoising
                NoiseReductionLevel = NoiseLevel.Medium
            },
            Language = Language.English
        };

        // 4️⃣ Run OCR with the configured pipeline
        var ocrResult = ocrEngine.Recognize(image, recognitionOptions);

        // 5️⃣ Print the extracted text
        System.Console.WriteLine("=== Extracted Text ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Enregistrez-le sous `Program.cs`, exécutez `dotnet run`, et observez la console se remplir du texte nettoyé.

---

## Étape 7 – Aller plus loin – Ajuster le pipeline

Le **pipeline de prétraitement OCR** est flexible. Voici quelques variations courantes que vous pourriez explorer :

| Variation | Quand l'utiliser | Extrait de code |
|-----------|------------------|-----------------|
| **Réduction du bruit plus élevée** (p. ex., `NoiseLevel.High`) | Scans très granuleux provenant de caméras basse résolution | `NoiseReductionLevel = NoiseLevel.High` |
| **Désactiver le redressement** | Les images sont déjà parfaitement alignées | `EnableSmartDeskew = false` |
| **Support multilingue** | Les documents contiennent à la fois de l'anglais et de l'espagnol | `Language = Language.English | Language.Spanish` |
| **Mise à l'échelle DPI personnalisée** | Des polices très petites nécessitent un suréchantillonnage | `recognitionOptions.Dpi = 300;` |

---

## Conclusion

Nous venons de créer un **pipeline de prétraitement OCR** en C# qui **redresse automatiquement l'image**, réduit le bruit, et enfin **reconnaît du texte à partir d'images** comme les JPG. En configurant `PreprocessSettings` dans les `RecognitionOptions` d'Aspose.OCR, nous avons transformé une image tremblotante et tachetée en texte propre et interrogeable avec seulement quelques lignes.

> **Points clés :**  
> - Nettoyez toujours l'image d'abord – le moteur OCR fonctionne mieux sur des entrées droites et à faible bruit.  
> - Le pipeline est entièrement configurable ; ajustez le redressement et la réduction du bruit selon vos besoins.  
> - Le même schéma fonctionne pour les PDF, TIFF ou toute source bitmap que vous fournissez à Aspose.OCR.

Prêt pour l'étape suivante ? Essayez de faire passer un lot de fichiers par le pipeline, ou intégrez le code dans une API web afin que les utilisateurs puissent télécharger des images et obtenir du texte instantanément. Vous pouvez également explorer les fonctionnalités de conversion de documents d'Aspose pour transformer le texte extrait en PDF interrogeable.

Bon codage, et que vos résultats OCR soient toujours précis ! 🚀

![Diagramme d'un pipeline de prétraitement OCR montrant les étapes : charger l'image → redressement intelligent → réduction du bruit → OCR → texte de sortie](ocr-preprocessing-pipeline.png "diagramme du pipeline de prétraitement OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}