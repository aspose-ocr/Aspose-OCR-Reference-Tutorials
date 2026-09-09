---
category: general
date: 2026-01-02
description: Apprenez à reconnaître le texte chinois et à extraire le texte des fichiers
  PNG avec la reconnaissance de texte hors ligne en utilisant Aspose.OCR. Aucun internet
  requis – effectuez la reconnaissance OCR sur l'image en quelques étapes seulement.
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: fr
og_description: Reconnaître du texte chinois sans Internet. Ce tutoriel montre comment
  extraire du texte d’un PNG en utilisant la reconnaissance de texte hors ligne et
  effectuer une OCR sur l’image en C#.
og_title: reconnaître le texte chinois hors ligne – Guide C# étape par étape
tags:
- OCR
- C#
- Aspose
title: reconnaître le texte chinois hors ligne – Tutoriel complet OCR en C#
url: /fr/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# reconnaître du texte chinois hors ligne – Tutoriel complet C# OCR

Vous avez déjà eu besoin de **reconnaître du texte chinois** à partir d’un PNG numérisé mais votre application s’exécute sur une machine sans internet ? Vous n’êtes pas seul. Dans de nombreux scénarios d’entreprise—pensez aux serveurs isolés ou aux appareils sur le terrain—compter sur des services cloud n’est tout simplement pas une option.  

Dans ce guide, nous parcourrons une solution autonome qui vous permet **d’extraire du texte à partir de fichiers png**, d’exécuter une **reconnaissance de texte hors ligne**, et de **faire de l’OCR sur des images** à l’aide d’Aspose.OCR. À la fin, vous disposerez d’un programme console C# prêt à l’emploi qui affiche les caractères chinois directement dans la console.

## Prérequis

- .NET 6 SDK (ou toute version récente de .NET) installé localement.  
- Visual Studio 2022 ou VS Code – selon votre préférence.  
- Une copie du package NuGet Aspose.OCR pour .NET (`Aspose.OCR`).  
- Les fichiers de ressources linguistiques pour l’anglais et le chinois simplifié (le tutoriel montre comment les télécharger automatiquement).  
- Une image nommée `chinese_doc.png` placée dans un dossier que vous pouvez référencer (espace réservé `YOUR_DIRECTORY`).  
- Aucun service supplémentaire, aucune clé API—juste une DLL locale et quelques fichiers de ressources.

---

## Étape 1 – Télécharger les ressources linguistiques requises (une fois)

Aspose.OCR stocke les packs de langues sur le disque. La première fois que vous lancez l’application, vous devez les télécharger. L’appel `ResourceManager.DownloadResources` fait exactement cela, et comme nous transmettons à la fois l’anglais et le chinois simplifié, le moteur pourra ensuite basculer entre eux sans aucun trafic réseau supplémentaire.

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **Astuce :** Conservez le dossier téléchargé (`Aspose.OCR.Resources`) sous contrôle de version si vous avez besoin de builds reproductibles sur plusieurs machines.

## Étape 2 – Initialiser le moteur OCR en mode hors ligne

Définir `OfflineMode = true` indique à la bibliothèque d’éviter tout appel HTTP. C’est la clé d’une véritable **reconnaissance de texte hors ligne**.

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **Pourquoi c’est important :** Certaines bibliothèques OCR reviennent aux services cloud lorsqu’un pack de langue est manquant. En imposant le mode hors ligne, nous garantissons des performances déterministes et la conformité aux politiques de confidentialité des données.

## Étape 3 – Charger le PNG à traiter

Nous utiliserons `System.Drawing.Bitmap` pour lire l’image. Si votre projet cible .NET 6+ sur des plateformes non Windows, envisagez `SkiaSharp` comme alternative, mais pour la plupart des déploiements centrés sur Windows, `Bitmap` fonctionne très bien.

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **Cas particulier :** Si le PNG est très volumineux (plus de 5 MP), vous pourriez vouloir le réduire d’abord pour accélérer la reconnaissance et diminuer l’utilisation de la mémoire :

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## Étape 4 – Exécuter la reconnaissance avec la langue chinois simplifié

Ici, nous indiquons au moteur exactement quelle langue utiliser. L’objet `RecognitionOptions` vous permet également d’ajuster des paramètres comme `DetectOrientation` ou `PreserveFormatting`, mais les valeurs par défaut fonctionnent bien pour la plupart des documents imprimés.

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## Étape 5 – Afficher (ou traiter davantage) le texte extrait

La propriété `OcrResult.Text` contient la représentation en texte brut. Vous pouvez l’écrire dans la console, dans un fichier, ou la transmettre à un pipeline NLP en aval.

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### Résultat attendu

Si `chinese_doc.png` contient la phrase « 你好，世界！ », la console affichera :

```
=== Recognized Chinese Text ===
你好，世界！
```

> **Note :** La précision de l’OCR dépend de la qualité de l’image, de la clarté de la police et du contraste. Pour de meilleurs résultats, utilisez des numérisations haute résolution (300 dpi ou plus) et assurez‑vous que le texte n’est pas incliné.

---

## Exemple complet fonctionnel

Ci‑dessous se trouve le programme complet, prêt à copier‑coller. Enregistrez‑le sous le nom `Program.cs` dans un nouveau projet console et exécutez `dotnet run`. Toutes les étapes sont regroupées, vous pouvez ainsi voir le flux du téléchargement des ressources jusqu’au résultat final.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Conseil :** Enveloppez l’appel `ResourceManager.DownloadResources` dans un bloc `try/catch` si vous souhaitez gérer gracieusement le cas où internet est réellement indisponible. La méthode lèvera une `NetworkException` sinon.

---

## Questions fréquemment posées (FAQ)

| Question | Réponse |
|----------|--------|
| **Puis‑je reconnaître le chinois traditionnel ?** | Oui—remplacez `Language.ChineseSimplified` par `Language.ChineseTraditional` et téléchargez le pack correspondant. |
| **Et si je dois extraire du texte d’un JPEG au lieu d’un PNG ?** | Le même code fonctionne ; il suffit de changer l’extension du fichier. `Bitmap` prend en charge la plupart des formats raster courants. |
| **Existe‑t‑il un moyen d’obtenir les boîtes englobantes pour chaque caractère ?** | Définissez `RecognitionOptions.DetectRegions = true`. Le `OcrResult` contiendra alors des objets `Region` avec leurs coordonnées. |
| **Comment exécuter cela sous Linux ?** | Utilisez le package `System.Drawing.Common` (1.0+). Sur un Linux sans interface graphique, vous pourriez avoir besoin de la dépendance native `libgdiplus`. |
| **Puis‑je traiter un dossier d’images par lots ?** | Absolument—encapsulez la logique de reconnaissance dans une boucle `foreach (var file in Directory.GetFiles(folder, "*.png"))`. |

## Prochaines étapes et sujets associés

- **Améliorer la précision** : expérimentez `RecognitionOptions.PreprocessImage = true` pour laisser le moteur améliorer automatiquement le contraste.  
- **Combiner les langues** : vous pouvez passer un tableau de langues à `ResourceManager.DownloadResources` et laisser le moteur détecter automatiquement.  
- **Intégrer à une UI** : intégrez le code console dans une application WinForms ou WPF et affichez le résultat OCR dans une zone de texte.  
- **Explorer d’autres bibliothèques Aspose** : `Aspose.PDF` pour la génération de PDF, `Aspose.Slides` pour l’automatisation de présentations, etc.  

Si vous souhaitez extraire du texte d’autres formats d’image, le même schéma s’applique—il suffit d’échanger le chemin du fichier et éventuellement d’ajuster les options de prétraitement. Bon codage !

---

![exemple de reconnaissance de texte chinois](/images/recognize-chinese-text.png "Capture d’écran montrant la sortie de la reconnaissance de texte chinois dans la console")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}