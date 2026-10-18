---
category: general
date: 2026-03-21
description: Apprenez à redresser les fichiers image et à reconnaître le texte d’une
  image avec Aspose OCR. Convertissez un JPG en texte et corrigez la rotation de l’image
  en quelques lignes de code C#.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: fr
og_description: Comment redresser une image et extraire du texte à partir de JPEGs
  en utilisant Aspose OCR. Suivez ce guide étape par étape pour convertir un jpg en
  texte et corriger la rotation de l'image.
og_title: Comment redresser une image en C# – Tutoriel rapide Aspose OCR
tags:
- OCR
- C#
- Aspose
title: Comment redresser une image en C# – Guide complet utilisant Aspose OCR
url: /fr/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image en C# – Guide complet avec Aspose OCR

Vous vous êtes déjà demandé **comment redresser une image** provenant d’un scanner incliné à un angle étrange ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils essaient d’extraire du texte de reçus, factures ou notes manuscrites. La bonne nouvelle, c’est qu’avec Aspose OCR vous pouvez corriger la rotation de l’image et obtenir du texte propre et recherchable en quelques lignes seulement.

Dans ce tutoriel, nous parcourrons l’ensemble du processus : de l’installation de la bibliothèque, à l’activation du redressement automatique, en passant par la reconnaissance du texte d’image, jusqu’à la conversion d’un JPG en texte. À la fin, vous disposerez d’une application console prête à l’emploi qui **reconnaît les fichiers jpg** sans avoir à les faire pivoter manuellement au préalable.

## Ce dont vous avez besoin

- **.NET 6.0** ou version ultérieure (le code fonctionne aussi bien sur .NET Core que sur .NET Framework)  
- **Aspose.OCR for .NET** package NuGet – la version 23.12 ou plus récente est recommandée  
- Un **JPEG incliné** d’exemple (par ex., `skewed_receipt.jpg`) placé à un endroit accessible par votre application  
- Visual Studio, VS Code ou tout autre éditeur C# de votre choix  

Aucun autre outil tiers n’est requis. La bibliothèque gère le redressement, l’OCR et même la détection de langue en interne.

![exemple de désalignement d'image](/images/deskew-example.png "comment redresser une image avec Aspose OCR")

## Étape 1 : Configurer le projet et installer Aspose.OCR

Pour garder les choses propres, créez un nouveau projet console :

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

La ligne `dotnet add package` récupère les binaires **Aspose.OCR** ainsi que toutes les dépendances natives. Sous Windows, les DLL natives sont installées automatiquement ; sous Linux/macOS, il peut être nécessaire d’installer le paquet `libgdiplus`, mais cela ne se fait qu’une fois.

## Étape 2 : Activer le redressement automatique (corriger la rotation de l’image)

Ouvrez maintenant `Program.cs` et remplacez son contenu par le code ci‑dessous. La ligne clé est `ocrEngine.Settings.Deskew = true;` — c’est le drapeau qui indique au moteur **comment redresser une image** automatiquement.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Pourquoi activer le redressement ?

Lorsqu’un scanner alimente une page sous un angle, la ligne de base du texte est inclinée. Les moteurs OCR traditionnels liraient chaque caractère comme une version inclinée, ce qui réduit fortement la précision. En définissant `Deskew = true`, Aspose OCR exécute rapidement une transformée de Hough en arrière‑plan, fait pivoter le bitmap pour le rendre horizontal, puis effectue la reconnaissance. Le résultat est équivalent à une rotation manuelle dans Photoshop — mais plus rapide et entièrement automatisé.

## Étape 3 : Reconnaître le texte d’image et convertir le JPG en texte

L’appel `Recognize` fait deux choses à la fois :

1. **Redresse** l’image (parce que nous avons activé le drapeau).  
2. **Extrait** le contenu textuel, le renvoyant dans un objet `OcrResult`.

Vous pouvez traiter `ocrResult.Text` comme une simple chaîne, l’écrire dans un fichier ou l’alimenter à des pipelines de traitement en aval. Si vous avez besoin des scores de confiance bruts par mot, `ocrResult.Words` vous fournit une collection avec les valeurs `Confidence`.

### Exemple de sortie

En supposant que `skewed_receipt.jpg` contienne un simple reçu, vous pourriez obtenir quelque chose comme :

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Remarquez comment les chiffres s’alignent correctement malgré une rotation d’environ 7° de l’image d’origine. C’est la magie de **la rotation correcte de l’image** intégrée à la bibliothèque.

## Étape 4 : Exécuter l’exemple et vérifier les résultats

Compilez et lancez :

```bash
dotnet run
```

Si tout est correctement configuré, le texte extrait s’affichera dans la console. Si vous obtenez une exception telle que `FileNotFoundException`, revérifiez le chemin vers votre JPEG et assurez‑vous que le fichier est lisible.

### Pièges courants & astuces pro

- **Images volumineuses** – La consommation mémoire de l’OCR augmente avec les dimensions de l’image. Redimensionnez les fichiers trop grands (par ex., > 3000 px de largeur) avant de les passer au moteur.  
- **Scripts non latins** – Par défaut, le moteur suppose l’anglais. Définissez `ocrEngine.Settings.Language = OcrLanguage.French;` (ou toute langue prise en charge) si vous devez **reconnaître le texte d’image** dans d’autres alphabets.  
- **Traitement par lots** – Pour de nombreux fichiers, réutilisez la même instance `OcrEngine` ; créer un nouveau moteur pour chaque fichier engendre un surcoût inutile.  
- **Vérification de la qualité** – Après le redressement, vous pouvez exporter le bitmap corrigé via `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` pour vérifier visuellement la correction de rotation.

## Exemple complet fonctionnel (tout en un)

Voici le programme complet, autonome, que vous pouvez copier‑coller dans `Program.cs`. Il comprend des commentaires, la gestion des erreurs et une étape optionnelle pour enregistrer l’image redressée.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

L’exécution du programme **reconnaît les fichiers jpg**, corrige automatiquement toute inclinaison et affiche du texte propre et recherchable dans la console.

## Conclusion

Vous disposez maintenant d’un extrait de code solide, prêt pour la production, qui montre **comment redresser une image** et extraire son contenu avec Aspose OCR. Cette approche fonctionne pour les reçus, factures, contrats numérisés ou tout JPEG dont le texte n’est pas parfaitement horizontal.

Prochaines étapes possibles :

- **Traitement par lots** d’un dossier de JPEG et écriture de chaque résultat dans un fichier `.txt` (relié à *convertir jpg en texte*).  
- Intégrer l’étape OCR dans une API ASP.NET Core afin que les clients puissent télécharger des images et recevoir du texte au format JSON.  
- Expérimenter avec différents paramètres OCR comme `ocrEngine.Settings.Language` ou `ocrEngine.Settings.RecognitionMode` pour améliorer la précision sur des documents non anglais.  

Essayez, ajustez les paramètres et laissez le moteur faire le gros du travail. Comme toujours, si vous rencontrez un problème ou avez une optimisation à partager, laissez un commentaire ci‑dessous. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}