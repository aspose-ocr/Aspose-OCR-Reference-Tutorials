---
category: general
date: 2026-04-04
description: Comment activer rapidement le GPU dans Aspose OCR. Apprenez à extraire
  du texte d’une image, charger l’image pour l’OCR et reconnaître le texte en utilisant
  C#.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: fr
og_description: Comment activer rapidement le GPU dans Aspose OCR. Suivez ce tutoriel
  pour extraire du texte d’une image, charger l’image pour l’OCR et reconnaître le
  texte avec C#.
og_title: Comment activer le GPU pour l'OCR en C# – Guide complet
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Comment activer le GPU pour l'OCR en C# – Guide étape par étape
url: /fr/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer le GPU pour l'OCR en C# – Guide complet

Vous vous êtes déjà demandé **comment activer le GPU** lors de l'utilisation d'Aspose OCR ? Peut-être avez‑vous atteint une limite de performance en traitant des centaines de reçus, et le CPU ne suit plus. La bonne nouvelle, c’est que activer l’accélération GPU est un jeu d’enfant, et une fois activée vous verrez le moteur OCR parcourir les images à toute vitesse.

Dans ce tutoriel, nous allons non seulement activer le commutateur GPU, mais aussi vous montrer comment **charger une image pour l'OCR**, **reconnaître du texte**, et finalement **extraire du texte d'une image** à l'aide d'un exemple C# clair. À la fin, vous disposerez d’un programme prêt à l’emploi qui extrait le texte brut de n’importe quelle image prise en charge — sans services externes requis.

## Ce dont vous avez besoin

- .NET 6+ (ou .NET Framework 4.7.2 et versions ultérieures).  
- Aspose.OCR for .NET, version 24.2.0 ou plus récente (le drapeau GPU a été ajouté dans cette version).  
- Une machine avec GPU et les pilotes appropriés (NVIDIA CUDA 11+ fonctionne très bien).  
- Un fichier image que vous souhaitez traiter — pensez à un reçu numérisé, une facture photographiée ou une note manuscrite.

Si vous avez déjà tout cela, super — plongeons‑y.

## Étape 1 : Comment activer le GPU – Configurer le moteur OCR

La première chose à faire est d’indiquer à Aspose OCR d’utiliser le GPU. Cela se fait en définissant la propriété `UseGpu` sur l’instance `OcrEngine`. La propriété est `false` par défaut, nous l’activons donc explicitement.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Pourquoi c’est important :** Lorsque `UseGpu` est `true`, la bibliothèque décharge les calculs matriciels lourds vers le processeur graphique. Sur un RTX 3060 modeste, vous remarquerez que la latence passe de plusieurs secondes par image à une fraction de seconde.

> **Astuce :** Si vous exécutez dans un environnement CI sans interface, assurez‑vous que le pilote GPU est installé et que le compte de service a la permission d’accéder au dispositif. Sinon le moteur reviendra silencieusement en mode CPU.

## Étape 2 : Charger l'image pour l'OCR – Pointer le moteur vers votre fichier

Ensuite, nous devons **charger une image pour l'OCR**. Aspose OCR accepte tout format d’image pris en charge par System.Drawing (PNG, JPEG, BMP, TIFF, etc.). L’utilitaire `ImageStream.FromFile` enveloppe le fichier dans l’objet flux requis.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Si vous préférez charger depuis un `byte[]` (par exemple lorsque l’image provient d’une base de données), vous pouvez utiliser `ImageStream.FromBytes(byteArray)` à la place — même résultat, juste une source différente.

## Étape 3 : Reconnaître du texte – Exécuter le processus OCR

Maintenant que le moteur est configuré et que l’image est chargée, il est temps de **reconnaître du texte**. La méthode `Recognize` effectue tout le travail lourd et renvoie un objet `OcrResult` qui contient le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

Vous pouvez également changer la langue en définissant `ocrEngine.Language = OcrLanguage.French;` avant d’appeler `Recognize()`. L’accélération GPU fonctionne quel que soit le pack de langue chargé.

## Étape 4 : Extraire du texte d’une image – Produire le résultat

Enfin nous **extrayons du texte d’une image** en lisant la propriété `Text` de l’objet résultat. À des fins de démonstration, nous l’afficherons simplement dans la console, mais vous pourriez l’écrire dans un fichier, une base de données, ou le transmettre à un autre service.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Sortie attendue** (votre texte réel différera selon l’image) :

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Si vous avez besoin des valeurs de confiance brutes, vous pouvez parcourir `ocrResult.Regions` et inspecter chaque `Region.Confidence`.

## Exemple complet fonctionnel – Un fichier, prêt à exécuter

Voici le programme complet. Copiez‑collez‑le dans un nouveau projet console, restaurez le package NuGet Aspose.OCR, et appuyez sur **F5**.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Note :** Remplacez `YOUR_DIRECTORY/receipt.jpg` par le chemin réel vers votre image. Si le programme lève une `FileNotFoundException`, vérifiez à nouveau le chemin et les permissions du fichier.

## Questions fréquentes & cas particuliers

### Et si le GPU n’est pas détecté ?

Aspose OCR reviendra automatiquement en mode CPU et enregistrera un avertissement. Pour vérifier quel mode est actif, inspectez `ocrEngine.IsGpuEnabled` après la construction — il renvoie `true` uniquement lorsque le pilote GPU est chargé avec succès.

### Puis‑je traiter plusieurs images dans une boucle ?

Absolument. Déplacez simplement la ligne `ocrEngine.Image = …` à l’intérieur d’une boucle `foreach (var file in files)`. Conservez la même instance `OcrEngine ; la réutiliser évite le surcoût d’allocation répétée des ressources GPU.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### Comment gérer les langues non‑anglais ?

Définissez la langue avant d’appeler `Recognize()` :

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

L’accélération GPU fonctionne de la même manière ; seul le modèle de langue change.

### Et les photos grandes et haute résolution ?

Si vous rencontrez des erreurs de dépassement de mémoire, réduisez d’abord l’image. Aspose OCR fournit `ImageHelper.Resize` – une méthode rapide pour réduire la taille sans perdre trop de détails.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Conclusion

Nous avons couvert **comment activer le GPU** pour Aspose OCR, vous montré comment **charger une image pour l'OCR**, parcouru **comment reconnaître du texte**, et démontré **comment extraire du texte d’une image** avec un programme C# concis et prêt pour la production. En basculant le drapeau `UseGpu`, vous débloquez un gain de vitesse notable, surtout lors du traitement de lots de reçus, factures ou tout flux de documents à haut volume.

Prêt pour l’étape suivante ? Essayez d’associer ce pipeline OCR à une base de données pour stocker les reçus extraits, ou d’alimenter le texte brut dans un modèle de traitement du langage naturel pour la catégorisation des dépenses. Vous pouvez également explorer la collection `OcrResult.Regions` pour obtenir les coordonnées des boîtes englobantes et créer une interface qui met en évidence chaque mot sur l’image originale.

Bonne programmation, et profitez de la puissance supplémentaire que l’accélération GPU apporte à vos charges de travail OCR ! 

---

![illustration de comment activer le gpu](gpu-ocr-diagram.png "illustration de comment activer le gpu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}