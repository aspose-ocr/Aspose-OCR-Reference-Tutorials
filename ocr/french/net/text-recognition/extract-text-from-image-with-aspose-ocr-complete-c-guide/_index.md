---
category: general
date: 2026-03-04
description: Extraire du texte d’une image avec Aspose OCR en C#. Apprenez à charger
  une image pour l’OCR et à reconnaître efficacement le texte des fichiers TIFF.
draft: false
keywords:
- extract text from image
- load image for ocr
- recognize text from tiff
- Aspose OCR C#
- GPU OCR engine
language: fr
og_description: Extrayez du texte d’une image à l’aide d’Aspose OCR en C#. Ce guide
  montre comment charger une image pour l’OCR et reconnaître le texte des fichiers
  TIFF avec un moteur GPU.
og_title: Extraire du texte d’une image avec Aspose OCR – Tutoriel C#
tags:
- OCR
- C#
- Aspose
- GPU
title: Extraire du texte d’une image avec Aspose OCR – Guide complet C#
url: /fr/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image avec Aspose OCR – Guide complet C#

Vous avez déjà eu besoin d'**extraire du texte d'une image** sans savoir quelle bibliothèque offrirait à la fois rapidité et précision ? Vous n'êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu'ils traitent des PDF numérisés ou des archives TIFF. La bonne nouvelle, c'est qu'Aspose OCR, combiné à un moteur activé par GPU, rend tout le processus aussi simple qu'une brise.

Dans ce tutoriel, nous vous montrerons exactement comment **charger une image pour l'OCR**, configurer un moteur GPU, puis **reconnaître le texte d'un fichier TIFF** en quelques lignes seulement. À la fin, vous disposerez d’une application console exécutable qui affiche le texte extrait dans la console, et vous comprendrez le « pourquoi » de chaque étape.

## Ce que vous allez apprendre

- Comment installer et référencer le package NuGet Aspose.OCR.  
- Pourquoi un `GpuOcrEngine` accéléré par GPU peut réduire considérablement le temps de traitement.  
- La bonne façon de **charger une image pour l'OCR** avec `ImageInfo`.  
- Comment configurer les paramètres de langue et les limites de mémoire.  
- Comment **reconnaître le texte d'un TIFF** et gérer les pièges courants.

Aucune expérience préalable avec Aspose n'est requise ; une connaissance de base du C# et de .NET suffit. Allons-y.

---

## Étape 1 : Extraire du texte d'une image – Initialiser le moteur OCR GPU

La première chose dont nous avons besoin est un moteur OCR capable de lire les pixels. Aspose propose un `GpuOcrEngine` qui délègue le travail intensif à votre carte graphique. C’est particulièrement utile lorsque vous avez des dizaines de TIFF haute résolution en attente dans une file.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Create a GPU‑enabled OCR engine.
// Setting GpuMemoryLimit helps avoid out‑of‑memory crashes on modest GPUs.
GpuOcrEngine ocrEngine = new GpuOcrEngine
{
    GpuMemoryLimit = 1024 // limit to 1024 MB
};
```

**Pourquoi c’est important :**  
Un moteur fonctionnant uniquement sur CPU scannerait chaque pixel séquentiellement, ce qui peut être très lent pour les grandes images. En limitant la mémoire GPU, vous gardez le processus léger tout en bénéficiant d’un gain de performance.

> **Astuce :** Si vous exécutez le code sur un serveur sans GPU, revenez à `OcrEngine` — l’API est identique, il suffit de changer le nom de la classe.

---

## Étape 2 : Charger l'image pour l'OCR – Préparer le fichier TIFF

Maintenant que le moteur est prêt, nous devons **charger l'image pour l'OCR**. `ImageInfo.Load` d’Aspose comprend un large éventail de formats, y compris les TIFF multi‑pages. Pointez‑le simplement vers votre fichier et laissez la bibliothèque gérer le reste.

```csharp
// Replace the path with the location of your TIFF file.
string imagePath = @"YOUR_DIRECTORY/english_page.tif";

// Load the image into an ImageInfo object.
// ImageInfo abstracts away format specifics, giving you a uniform API.
ImageInfo image = ImageInfo.Load(imagePath);
```

**Cas particulier :**  
Si votre TIFF contient plusieurs pages, vous pouvez itérer sur `image.Pages` et traiter chaque page individuellement. Pour la plupart des scans à page unique, la ligne ci‑dessus suffit.

---

## Étape 3 : Reconnaître le texte d'un TIFF – Effectuer l'OCR

Avec l'image en mémoire et le moteur prêt, nous pouvons enfin **reconnaître le texte d'un TIFF**. La méthode `Recognize` renvoie un objet `OcrResult` contenant la chaîne extraite, les scores de confiance et même les boîtes englobantes si vous en avez besoin plus tard.

```csharp
// Set the language you expect in the image.
// English is the default, but you can combine languages like Language.English | Language.Spanish.
ocrEngine.Language = Language.English;

// Run the OCR process.
OcrResult ocrResult = ocrEngine.Recognize(image);
```

**Pourquoi la langue est importante :**  
Spécifier la langue correcte améliore considérablement la précision, car le moteur peut appliquer des dictionnaires et des modèles de caractères propres à la langue.

---

## Étape 4 : Afficher le texte extrait

La dernière étape est triviale — il suffit d’écrire le résultat dans la console, un fichier ou une base de données. Ici, nous restons simples et affichons le texte à l’écran.

```csharp
// Print the recognized text.
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(ocrResult.Text);
```

**Sortie attendue :**  
Si `english_page.tif` contient un paragraphe imprimé, vous verrez quelque chose comme :

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
```

Si l’OCR rencontre des difficultés, le texte peut contenir des caractères étranges ; ajuster `GpuMemoryLimit` ou fournir une image source de résolution supérieure résout généralement le problème.

---

## Exemple complet fonctionnel

Voici le programme complet, autonome, que vous pouvez copier‑coller dans un nouveau projet Console App. Il compile avec .NET 6 ou version ultérieure.

```csharp
// ------------------------------------------------------------
// Complete C# program to extract text from image using Aspose OCR.
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize GPU OCR engine with a memory cap.
        GpuOcrEngine ocrEngine = new GpuOcrEngine
        {
            GpuMemoryLimit = 1024 // MB
        };

        // 2️⃣ Choose the language for recognition.
        ocrEngine.Language = Language.English;

        // 3️⃣ Load the image you want to process.
        // Make sure the path points to a valid TIFF file.
        string imagePath = @"YOUR_DIRECTORY/english_page.tif";
        ImageInfo image = ImageInfo.Load(imagePath);

        // 4️⃣ Perform OCR – this returns the recognized text.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Display the result.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);

        // Keep the console window open when debugging.
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

Enregistrez le fichier, exécutez `dotnet run` et observez la console afficher le contenu extrait. Simple, non ?

---

## Questions fréquentes & cas particuliers

**Et si mon image est un PNG ou JPEG au lieu d’un TIFF ?**  
`ImageInfo.Load` fonctionne avec pratiquement n’importe quel format raster, vous pouvez donc changer l’extension et le reste du code reste identique. Aucun changement supplémentaire n’est requis.

**Mon OCR renvoie des caractères illisibles—que vérifier ?**  
1. Vérifiez la résolution de l’image (300 dpi ou plus est idéal).  
2. Assurez‑vous que la bonne `Language` est définie ; une langue inadéquate réduit le support du dictionnaire.  
3. Augmentez `GpuMemoryLimit` si l’image est très grande ; le moteur peut se throttler.

**Puis‑je traiter plusieurs fichiers en lot ?**  
Absolument. Enveloppez les étapes de chargement et de reconnaissance dans une boucle `foreach (var file in Directory.GetFiles(...))`. Pensez à libérer chaque `ImageInfo` si vous traitez des centaines de fichiers afin de libérer les ressources natives.

**Ai‑je besoin d’un GPU pour exécuter ce code ?**  
Non. Si aucun GPU compatible n’est présent, remplacez `GpuOcrEngine` par le `OcrEngine` classique. Les appels d’API (`Recognize`, `Language`, etc.) restent les mêmes.

---

## Conseils de performance – Optimiser l’OCR GPU

- **Réutiliser le moteur :** Créer un nouveau `GpuOcrEngine` pour chaque image ajoute du sur‑coût. Instanciez‑le une fois et réutilisez‑le pour de nombreux fichiers.  
- **Traitement par lots :** Chargez plusieurs images en mémoire, puis appelez `Recognize` séquentiellement ; le GPU reste « chaud » et travaille plus vite.  
- **Ajuster la limite de mémoire :** Sur une machine avec 4 Go de VRAM, une limite de 1024 Mo est sûre. Sur des stations de travail haut de gamme, vous pouvez l’augmenter à 4096 Mo pour des lots plus volumineux.

---

## Conclusion

Vous venez d’apprendre comment **extraire du texte d’une image** avec le moteur GPU d’Aspose OCR, comment **charger correctement une image pour l’OCR**, et comment **reconnaître le texte d’un TIFF** dans une application console C# propre et prête pour la production. Le code est entièrement exécutable, les explications couvrent le « comment » et le « pourquoi », et vous disposez maintenant d’une base solide pour aborder des scénarios OCR plus complexes—comme les documents multilingues ou les flux vidéo en temps réel.

Prêt pour le prochain défi ? Essayez d’étendre l’exemple pour écrire la sortie dans un CSV, ou expérimentez les données `BoundingBox` pour mettre en évidence les mots reconnus sur l’image d’origine. Les possibilités sont infinies, et les gains de performance grâce à l’accélération GPU rendront vos pipelines ultra‑rapides.

Si ce guide vous a été utile, laissez une étoile sur GitHub, partagez‑le avec un collègue, ou commentez ci‑dessous avec vos propres astuces. Bon codage !  

![extract text from image using Aspose OCR](placeholder.png){alt="extraction de texte à partir d'une image avec Aspose OCR"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}