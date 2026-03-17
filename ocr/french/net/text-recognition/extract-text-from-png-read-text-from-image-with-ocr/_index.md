---
category: general
date: 2026-03-17
description: Extraire du texte d’un PNG à l’aide d’Aspose OCR en C#. Apprenez à lire
  le texte d’une image, à traiter l’OCR de reçus et à créer un moteur OCR avec accélération
  GPU.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: fr
og_description: Extraire du texte d’un PNG à l’aide d’Aspose OCR. Ce guide montre
  comment lire le texte d’une image, traiter l’OCR de reçus et créer un moteur OCR
  efficacement.
og_title: Extraire le texte d’un PNG – Lire le texte d’une image avec OCR
tags:
- OCR
- CSharp
- Aspose
title: Extraire le texte d’un PNG – Lire le texte d’une image avec OCR
url: /fr/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'un PNG – Lire du texte à partir d'une image avec OCR

Vous avez déjà eu besoin d'**extraire du texte d'un PNG** sans savoir quelle bibliothèque vous donnerait des résultats fiables ? Vous n'êtes pas seul — les développeurs demandent constamment : « Comment lire du texte à partir de fichiers image comme des reçus sans écrire un réseau neuronal personnalisé ? » La bonne nouvelle, c’est qu’Aspose OCR fait le gros du travail pour vous, et vous pouvez même activer le GPU pour gagner en vitesse.

Dans ce tutoriel, nous passerons en revue tout ce dont vous avez besoin pour **traiter l'OCR de reçus**, depuis l'installation du package NuGet jusqu'à la création d'un moteur OCR qui comprend votre fichier PNG. À la fin, vous disposerez d’une application console autonome qui lit une image de reçu, affiche le texte reconnu et vous montre comment ajuster le moteur pour différents scénarios. Aucun document externe, juste du code pur et des explications claires.

## Prérequis

- SDK .NET 6.0 (ou toute version .NET récente)  
- Visual Studio 2022 ou VS Code avec les extensions C#  
- Un GPU NVIDIA compatible avec le dernier driver (facultatif, mais recommandé pour le mode GPU)  
- Le package NuGet **Aspose.OCR** (`dotnet add package Aspose.OCR`)  

Si vous n’avez pas de GPU, vous pouvez toujours exécuter l’exemple en mode CPU — il suffit d’ignorer les lignes de configuration du GPU.

## Étape 1 : Installer Aspose.OCR et configurer le projet

Tout d’abord, créez un nouveau projet console et ajoutez la bibliothèque Aspose OCR.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Pourquoi c’est important : le package `Aspose.OCR` regroupe le moteur OCR, les chargeurs d’images et le support GPU optionnel. L’ajouter via NuGet garantit que vous obtenez la dernière version stable (en mars 2026, c’est la 23.10).

## Étape 2 : Importer les espaces de noms et créer le moteur OCR

Ouvrez maintenant **Program.cs** et ajoutez les directives `using` requises. Puis, instanciez le moteur.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Astuce :** Si vous rencontrez une `System.DllNotFoundException` sur des machines sans GPU, commentez simplement les deux lignes qui définissent `EngineMode` et `GpuDeviceId`. Le moteur repassera automatiquement en CPU.

## Étape 3 : Charger l'image PNG dont vous voulez extraire le texte

Aspose OCR peut lire les images directement depuis un chemin de fichier, un flux ou même un tableau d’octets. Pour cette démonstration, nous chargerons une image de reçu locale.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Remarquez comment nous protégeons le code contre un fichier manquant. Dans une application réelle, vous afficheriez probablement un message d’interface convivial au lieu de simplement quitter.

## Étape 4 : Effectuer la reconnaissance OCR

L’extraction réelle du texte se fait avec un seul appel de méthode. Le moteur renvoie un objet `OcrResult` contenant la chaîne brute, les scores de confiance et les informations de mise en page.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

Pourquoi nous vérifions `ocrResult.Text` : parfois un PNG de mauvaise qualité renvoie une chaîne vide, et il vaut mieux informer l’utilisateur que de ne rien afficher silencieusement.

## Étape 5 : Afficher le texte reconnu

Enfin, imprimez la chaîne extraite dans la console. Vous pouvez également l’écrire dans un fichier, une base de données ou la transmettre à un autre service.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Lorsque vous exécutez le programme (`dotnet run`), vous devriez voir quelque chose comme :

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

C’est la **solution complète pour extraire du texte d’un fichier PNG** avec Aspose OCR, et vous venez d’apprendre comment **lire du texte à partir d’une image** qui ressemble à un reçu.

## Optionnel : Affiner le moteur OCR (avancé)

Si vous avez besoin d’une précision supérieure pour des polices spécifiques ou des arrière‑plans bruyants, envisagez d’ajuster ces paramètres :

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Ces réglages sont particulièrement utiles lorsque vous **traitez l'OCR de reçus** dans des travaux batch où certaines numérisations sont loin d’être parfaites.

## Problèmes courants & comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Pilote GPU manquant** | Le moteur tente de charger CUDA mais ne trouve pas la DLL. | Installez le dernier pilote NVIDIA ou passez en mode CPU en supprimant la ligne `EngineMode.Gpu`. |
| **Chemin d'image incorrect** | `ImageStream.FromFile` lève une exception si le fichier est introuvable. | Validez toujours le chemin (voir Étape 3) ou utilisez `Path.Combine` pour la sécurité multiplateforme. |
| **Faible confiance sur des reçus flous** | Le moteur OCR ne parvient pas à différencier les caractères. | Activez `EnableImagePreprocessing` et augmentez éventuellement le DPI de l’image avant de la transmettre au moteur. |
| **Fuite de mémoire dans des services de longue durée** | Chaque `OcrEngine` conserve des ressources non gérées. | Disposez du moteur après usage : `using var ocrEngine = new OcrEngine();` |

## Exemple complet fonctionnel (copier‑coller)

Voici le **programme entier** que vous pouvez coller dans `Program.cs`. Il inclut tous les ajustements optionnels commentés pour une activation facile.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Enregistrez, lancez `dotnet run`, et vous verrez le contenu du reçu affiché dans la console.

![exemple d'extraction de texte à partir d'un PNG](receipt.png "exemple d'extraction de texte à partir d'un PNG")

*L'image ci‑dessus montre un exemple de reçu PNG que le code peut traiter.*

## Récapitulatif

Nous avons vu comment **extraire du texte d'un PNG** avec Aspose OCR, démontré comment **lire du texte à partir d’une image**, et parcouru une chaîne complète de **traitement d’OCR de reçus** incluant l’accélération GPU optionnelle. En **créant votre propre moteur OCR**, vous obtenez un contrôle total sur la configuration, les performances et la gestion des erreurs.

## Que faire ensuite ?

- **Traitement par lots** : parcourez un répertoire de reçus PNG et écrivez chaque résultat dans un fichier CSV.  
- **Intégration avec Azure Functions** : transformez cette application console en point de terminaison serverless qui accepte des téléchargements d’images.  
- **Support multilingue** : remplacez `Language.English` par `Language.Spanish` ou ajoutez des dictionnaires personnalisés.  
- **Post‑traitement** : utilisez des expressions régulières pour extraire des champs comme le total, la date ou le numéro de TVA à partir de la chaîne OCR brute.

N’hésitez pas à expérimenter — l’OCR est un outil étonnamment flexible une fois que vous connaissez les bons paramètres. Si vous rencontrez des difficultés, laissez un commentaire ci‑dessous ou consultez la référence API Aspose OCR pour approfondir.

Bon codage, et profitez de transformer ces reçus PNG récalcitrants en texte consultable !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}