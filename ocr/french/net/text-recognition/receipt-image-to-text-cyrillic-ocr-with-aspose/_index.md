---
category: general
date: 2026-04-01
description: Apprenez comment convertir une image de reçu en texte à l'aide d'Aspose
  OCR. Ce guide montre comment extraire du texte cyrillique, charger l'image pour
  l'OCR et reconnaître efficacement les caractères cyrilliques.
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: fr
og_description: Convertissez une image de reçu en texte avec Aspose OCR. Apprenez
  à extraire du texte cyrillique, charger une image pour l’OCR et reconnaître les
  caractères cyrilliques en C#.
og_title: image de reçu en texte – OCR cyrillique avec Aspose
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: Image de reçu en texte – OCR cyrillique avec Aspose
url: /fr/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# image de reçu en texte – OCR cyrillique avec Aspose

Vous avez déjà eu besoin de transformer une **image de reçu en texte** mais les caractères sont tous en cyrillique ? Vous n'êtes pas le seul à vous creuser la tête à ce sujet. Dans de nombreuses applications de vente au détail ou de comptabilité, les reçus sont rédigés en russe, bulgare ou serbe, et vous souhaitez tout de même obtenir une chaîne propre et consultable.  

Dans ce tutoriel, nous vous montrerons exactement comment **extraire du texte cyrillique** d’une photo de reçu, **charger l’image pour l’OCR**, et **reconnaître les caractères cyrilliques** à l’aide de la bibliothèque Aspose OCR. À la fin, vous disposerez d’un programme C# prêt à l’emploi qui écrit le résultat de l’OCR dans un fichier `.txt`.

## Ce dont vous avez besoin

- **.NET 6** (ou toute version récente de .NET) – le code fonctionne également sur .NET Framework 4.7+.
- **Aspose.OCR for .NET** package NuGet – `Install-Package Aspose.OCR`.
- Une image de reçu d’exemple contenant du texte cyrillique (par ex., `cyrillic_receipt.jpg`).
- Un environnement de développement – Visual Studio, VS Code ou Rider conviendra.  

Aucune dépendance native supplémentaire n’est requise ; Aspose fournit les modèles linguistiques et gère le traitement intensif en interne.

## image de reçu en texte – Configuration du moteur OCR

La première chose à faire est de **créer une instance du moteur OCR** et d’indiquer la langue qui nous intéresse. Aspose rend cela trivial :

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **Astuce :** Le pré‑chargement du modèle évite un appel réseau lors de la première exécution du programme, ce qui est pratique pour les scénarios de bureau ou embarqués.

## Comment extraire du texte cyrillique – Chargement de l’image du reçu

Maintenant que le moteur est prêt, nous devons **charger l’image pour l’OCR**. La classe `System.Drawing.Image` fonctionne parfaitement pour la plupart des formats bitmap.

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

Si le fichier n’est pas trouvé, `Image.FromFile` lève une `FileNotFoundException`. Vous voudrez peut‑être encapsuler le tout dans un bloc `try…catch` pour le code de production.

## Reconnaître les caractères cyrilliques – Récupérer le texte

L’objet `recognitionResult` contient le texte brut, les scores de confiance, et même les boîtes englobantes si vous en avez besoin plus tard. Pour une conversion simple « image de reçu en texte », nous écrivons simplement la propriété `Text` dans un fichier :

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

Lorsque vous exécutez le programme, vous devriez voir quelque chose comme :

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

C’est le résultat **image de reçu en texte** que vous recherchiez.

![exemple d'image de reçu convertie en texte](receipt-ocr-example.png "Exemple d'une image de reçu convertie en texte")

*Texte alternatif de l'image : conversion d'une image de reçu en texte montrant les caractères cyrilliques extraits par Aspose OCR.*

## Cas limites & Questions fréquentes

### Que faire si le modèle linguistique n’est pas encore téléchargé ?

Aspose télécharge automatiquement le modèle requis la première fois que vous définissez `ocrEngine.Language = Language.Cyrillic;`. Si la machine n’a pas d’accès à Internet, l’étape de pré‑chargement optionnelle échouera. Dans ce cas, fournissez le modèle manuellement (voir la documentation Aspose) ou assurez‑vous que l’appareil puisse accéder à `download.aspose.com`.

### Comment gérer plusieurs langues dans le même reçu ?

Vous pouvez passer une liste séparée par des virgules :

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

### Mon reçu est flou – puis‑je améliorer la précision ?

Aspose OCR propose un prétraitement d’image de base :

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

### Qu’en est‑il du traitement par lots de grande taille ?

Enveloppez la boucle de reconnaissance dans un `Parallel.ForEach` et réutilisez la même instance `OcrEngine` (elle est thread‑safe après le chargement du modèle). N’oubliez pas de verrouiller le moteur si vous rencontrez des problèmes de sécurité des threads.

## Exemple complet fonctionnel (Toutes les étapes combinées)

Voici le programme complet, prêt à copier‑coller, qui intègre le pré‑chargement optionnel et la gestion d’erreurs de base :

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

Exécutez le programme (`dotnet run` depuis le dossier du projet) et vous obtiendrez un fichier `.txt` contenant la sortie **image de reçu en texte**.

## Conclusion

Vous disposez maintenant d’une solution complète, de bout en bout, pour transformer une **image de reçu en texte** — spécifiquement pour les scripts cyrilliques — à l’aide d’Aspose OCR. Nous avons vu comment **créer le moteur OCR**, **charger l’image pour l’OCR**, **extraire du texte cyrillique**, et **reconnaître les caractères cyrilliques** en quelques lignes de C#.  

Prochaines étapes ? Essayez de traiter un dossier de reçus, expérimentez avec le `ImagePreprocessor` pour améliorer la précision, ou combinez la sortie OCR avec une base de données pour une comptabilité automatisée. Si vous devez gérer d’autres alphabets, remplacez `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}