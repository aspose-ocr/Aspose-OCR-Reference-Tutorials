---
category: general
date: 2026-03-18
description: Comment redresser une image et réduire le bruit dans les fichiers numérisés.
  Apprenez à charger une image depuis un fichier, extraire le texte d’un TIFF et reconnaître
  le texte d’une image avec Aspose OCR.
draft: false
keywords:
- how to deskew image
- how to reduce noise
- recognize text from image
- load image from file
- extract text from tiff
language: fr
og_description: Comment redresser rapidement une image à l'aide d'Aspose OCR. Ce guide
  vous montre comment réduire le bruit, charger une image depuis un fichier et extraire
  du texte d'un TIFF en C#.
og_title: Comment redresser une image – Tutoriel complet OCR en C#
tags:
- OCR
- C#
- Image Processing
title: Comment redresser une image et nettoyer les numérisations – Guide complet C#
url: /fr/net/skew-angle-calculation/how-to-deskew-image-and-clean-up-scans-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image – Tutoriel complet OCR en C#

Vous vous êtes déjà demandé **comment redresser une image** qui ressemble à une photo prise avec un scanner bancal ? Vous n'êtes pas seul. La plupart des développeurs rencontrent ce problème lorsque le TIFF source est légèrement de travers, et les résultats OCR deviennent un désordre. Bonne nouvelle ? En quelques lignes de C#, vous pouvez redresser l'image, éliminer le fond granuleux et extraire du texte propre et consultable directement du fichier.

Dans ce guide, nous parcourrons **comment réduire le bruit**, **charger une image depuis un fichier**, et enfin **reconnaître le texte à partir d'une image** en utilisant Aspose OCR. À la fin, vous serez capable de **extraire du texte d'un TIFF** sans effort.

> **Astuce :** Si vous utilisez déjà Aspose OCR pour d’autres projets, vous pouvez ajouter ces filtres sans aucun problème de licence supplémentaire.

---

## Ce dont vous avez besoin

- .NET 6 ou supérieur (le code fonctionne également sur .NET Core)  
- Package NuGet Aspose.OCR (`Install-Package Aspose.OCR`)  
- Un TIFF numérisé légèrement tourné ou bruité (nous utiliserons `skewed_scanned_doc.tif` comme exemple)  
- Un éditeur de texte ou IDE (Visual Studio, VS Code, Rider – choisissez votre poison)

Aucune bibliothèque supplémentaire n'est requise ; les filtres que nous utiliserons sont intégrés à Aspose OCR.

---

## Étape 1 – Créer le moteur OCR (Comment redresser une image)

La première chose à faire est d'instancier un `OcrEngine`. Considérez-le comme le cerveau qui lira plus tard les caractères pour vous.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize the OCR engine – this object holds all settings
        var ocrEngine = new OcrEngine();
```

Pourquoi créer le moteur dès le départ ? Cela vous offre un endroit unique où attacher les filtres de prétraitement, les packs de langues et les options de sortie. Si vous sautez cette étape et appelez directement `OcrEngine.Recognize`, vous perdez la possibilité de nettoyer l'image au préalable, ce qui explique pourquoi nous nous soucions du redressement.

---

## Étape 2 – Ajouter les filtres de redressement et de réduction du bruit (Comment réduire le bruit)

Now we attach two filters:

| Filtre | Ce qu'il fait | Pourquoi c'est important |
|--------|--------------|---------------------------|
| `AutoDeskewFilter` | Détecte et corrige la rotation | Redresse les lignes de texte afin que le moteur OCR puisse les lire correctement |
| `NoiseReductionFilterV2` | Supprime les taches et le grain de fond | Des pixels plus propres signifient moins d’erreurs de reconnaissance |

```csharp
        // Add filters to improve OCR accuracy
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // corrects rotation
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduces background noise
```

Vous pourriez remplacer `NoiseReductionFilterV2` par la version antérieure, mais l'algorithme v2 gère mieux les scanners modernes. Si votre document est déjà parfaitement plat, le filtre de redressement transmettra simplement l'image sans modification — aucun dommage.

---

## Étape 3 – Charger l'image depuis un fichier (Load Image from File)

Aspose fournit un utilitaire pratique `ImageStream.FromFile` qui lit une variété de formats, y compris TIFF, JPEG, PNG et BMP. Voici comment nous chargeons le fichier en mémoire :

```csharp
        // Load the scanned image you want to preprocess
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");
```

Remplacez `YOUR_DIRECTORY` par le chemin réel sur votre machine. Si vous travaillez avec un chemin relatif, assurez-vous que le fichier se trouve à côté de votre exécutable ou définissez le répertoire de travail en conséquence.

---

## Étape 4 – Exécuter l'OCR sur l'image prétraitée (Recognize Text from Image)

Avec les filtres en place et l'image chargée, nous demandons enfin à Aspose de lire les caractères :

```csharp
        // Perform OCR – the engine will automatically apply the filters first
        var ocrResult = ocrEngine.Recognize(image);
```

En coulisses, le moteur exécute l'algorithme de redressement, lisse le bruit, puis utilise un reconnaisseur basé sur un réseau de neurones. Le résultat est encapsulé dans un objet `OcrResult` qui vous fournit le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard.

---

## Étape 5 – Afficher ou enregistrer le texte extrait (Extract Text from TIFF)

Pour une démonstration rapide, nous affichons simplement le texte dans la console, mais vous pourriez l'écrire dans un fichier, une base de données, ou le transmettre à un flux de travail en aval.

```csharp
        // Show the recognized text in the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Sortie attendue** (exemple, variera selon votre document) :

```
Invoice #12345
Date: 2023‑04‑01
Total: $1,250.00
Thank you for your business!
```

Si la sortie contient encore des caractères illisibles, vérifiez que le TIFF original n'est pas trop basse résolution (minimum 300 dpi recommandé) et que la langue est correctement définie dans `ocrEngine.Settings.Language`.

---

## Exemple complet fonctionnel (Toutes les étapes en un seul endroit)

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console et exécuter immédiatement.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add preprocessing filters
        ocrEngine.Settings.Filters.Add(new AutoDeskewFilter());          // deskew image
        ocrEngine.Settings.Filters.Add(new NoiseReductionFilterV2());   // reduce noise

        // 3️⃣ Load the image file (TIFF, JPEG, etc.)
        var image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_scanned_doc.tif");

        // 4️⃣ Recognize text – filters run automatically
        var ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted text
        Console.WriteLine(ocrResult.Text);
    }
}
```

Enregistrez le fichier sous `Program.cs`, exécutez `dotnet run`, et vous devriez voir le texte nettoyé apparaître dans votre terminal.

---

## Questions fréquentes & cas particuliers

### Et si mon TIFF possède plusieurs pages ?

Aspose OCR peut traiter les images multipages en bouclant sur `image.GetPages()` (ou en utilisant `image.Pages`). Chaque page renvoie son propre `OcrResult`. Combinez-les avec `StringBuilder` si vous avez besoin d'une chaîne unique.

### Le filtre de redressement fonctionne-t-il sur des images fortement tournées ?

Il gère les rotations jusqu'à environ ±15°. Au-delà, vous devrez peut-être pré‑tourner l'image manuellement à l'aide d'une bibliothèque graphique (par ex., `System.Drawing` ou `SkiaSharp`) avant de la transmettre à Aspose.

### Comment améliorer la précision pour du texte non‑anglais ?

Set the language explicitly:

```csharp
ocrEngine.Settings.Language = Language.English; // or Language.French, etc.
```

Vous pouvez également charger des packs de langues personnalisés si ceux fournis n'incluent pas votre alphabet.

### Puis-je exécuter cela sous Linux ?

Absolument. Aspose OCR est multiplateforme ; assurez‑vous simplement que les dépendances natives sont présentes (généralement aucune pour la version pure .NET). Utilisez `dotnet publish -r linux-x64` pour un binaire autonome.

---

## Bonus : Visualiser l'image redressée

Si vous souhaitez voir l'image corrigée avant l'OCR, vous pouvez la sauvegarder à nouveau sur le disque :

```csharp
// After OCR, the filtered image is stored in ocrEngine.Settings.FiltersResult
var corrected = ocrEngine.Settings.FiltersResult;
corrected.Save(@"output/deskewed_cleaned.tif");
```

![exemple de redressement d'image](https://example.com/deskew-demo.png "exemple de redressement d'image")

*Texte alternatif de l'image :* **exemple de redressement d'image** – montre un avant/après d'un TIFF tourné corrigé par AutoDeskewFilter.

---

## Conclusion

Nous avons couvert **comment redresser une image**, **comment réduire le bruit**, et l’ensemble du pipeline pour **reconnaître le texte à partir d'une image**, **charger une image depuis un fichier**, et **extraire du texte d'un TIFF** en utilisant Aspose OCR en C#. La leçon principale ? Ajouter seulement deux filtres de prétraitement peut transformer un scan tremblotant et granuleux en un document net et consultable sans aucun outil externe.

Prêt pour l'étape suivante ? Essayez de remplacer `AutoDeskewFilter` par `AutoRotateFilter` si vos documents sont à l'envers, ou expérimentez avec `ContrastEnhancementFilter` pour des impressions fanées. Le même schéma—moteur → filtres → chargement → reconnaissance—s'applique à tous les scénarios Aspose OCR, vous pouvez donc réutiliser cette structure de base pour les PDF, PNG ou même les photos prises avec un appareil.

Bon codage, et que votre OCR soit toujours précis !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}