---
category: general
date: 2026-02-24
description: Comment activer le GPU dans l'exemple Aspose OCR C# – convertir rapidement
  une image en texte brut. Inclut la définition de l'ID du dispositif GPU et le guide
  C# pour lire le texte d'une image.
draft: false
keywords:
- how to enable gpu
- image to plain text
- aspose ocr example
- set gpu device id
- read image text c#
language: fr
og_description: Comment activer le GPU dans l’exemple Aspose OCR C#. Apprenez à définir
  l’ID du dispositif GPU et à lire le texte d’une image en C# de manière efficace.
og_title: Comment activer le GPU pour Aspose OCR en C# – Conversion rapide d’image
  en texte brut
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Comment activer le GPU pour Aspose OCR en C# – Conversion rapide d’image en
  texte brut
url: /fr/net/ocr-optimization/how-to-enable-gpu-for-aspose-ocr-in-c-fast-image-to-plain-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment activer le GPU pour Aspose OCR en C# – Conversion rapide d'image en texte brut

Vous vous êtes déjà demandé **comment activer le GPU** lors de l'utilisation d'Aspose OCR pour transformer une image en texte modifiable ? Vous n'êtes pas seul—de nombreux développeurs rencontrent une barrière de performance lorsqu'ils traitent de grosses factures ou des contrats numérisés. Bonne nouvelle ? Convertir une image en texte brut peut être ultra‑rapide dès que vous exploitez votre carte graphique.

Dans ce guide, nous passerons en revue un **exemple complet d'Aspose OCR** qui vous montre exactement comment activer le GPU, définir l'ID du dispositif GPU, et **lire le texte d'une image en C#**. À la fin, vous disposerez d'un programme exécutable qui extrait le texte de n'importe quelle image prise en charge en une fraction du temps nécessaire avec une approche uniquement CPU.

## Ce dont vous avez besoin

- .NET 6.0 ou ultérieur (l'API fonctionne avec .NET Core et .NET Framework)
- Un GPU compatible CUDA avec le dernier pilote installé
- Une licence Aspose.OCR pour .NET (ou un essai gratuit, qui fonctionne pour le développement)
- Visual Studio 2022 (ou tout éditeur C# de votre choix)

Aucun package NuGet supplémentaire au-delà de `Aspose.OCR` n'est requis—seulement la bibliothèque elle‑-même.

---

## Étape 1 – Installer le package NuGet Aspose OCR

Tout d'abord, ajoutez la bibliothèque officielle Aspose OCR à votre projet. Ouvrez la console du gestionnaire de packages et exécutez :

```powershell
Install-Package Aspose.OCR
```

Cela récupère `Aspose.OCR.dll` ainsi que toutes ses dépendances. Si vous préférez l'interface graphique, faites un clic droit sur votre projet → **Manage NuGet Packages** → recherchez *Aspose.OCR* et cliquez sur **Install**.  

*Astuce :* Après l'installation, vérifiez que le dossier `Aspose.OCR` apparaît sous **Dependencies** dans l'Explorateur de solutions.

---

## Étape 2 – Créer une structure d'application console simple

Nous allons créer une petite application console qui montre le flux complet. Créez un nouveau projet :

```bash
dotnet new console -n GpuOcrDemo
cd GpuOcrDemo
```

Remplacez le `Program.cs` généré par le code complet présenté plus loin. Cette structure nous fournit un point d'entrée propre et nous permet de nous concentrer sur la logique OCR.

---

## Étape 3 – Comment activer le GPU et définir l'ID du dispositif GPU

Passons maintenant à la star du spectacle : **comment activer le GPU** dans Aspose OCR. La bibliothèque expose un objet `OcrSettings` où vous pouvez activer `UseGpu` et éventuellement choisir un dispositif CUDA spécifique via `GpuDeviceId`. Voici l'extrait exact que vous intégrerez dans votre programme :

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Enable GPU acceleration – this is the crucial “how to enable gpu” step
        ocrEngine.Settings = new OcrSettings()
        {
            UseGpu = true,          // Turn on GPU processing
            GpuDeviceId = 0         // Optional: select the first CUDA‑compatible device
        };

        // 3️⃣ Recognise text from an image (any supported format)
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/large_invoice.png");

        // 4️⃣ Output the plain‑text result to the console
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Pourquoi activer le GPU ?

Activer le GPU décharge le travail intensif—prétraitement des pixels, segmentation des caractères et inférence du réseau neuronal—vers la carte graphique. Sur une GTX 1650 modeste, vous pouvez observer un **gain de vitesse de 2‑3×** par rapport au mode uniquement CPU, surtout avec des documents haute résolution.

### Choisir un ID de dispositif

Si votre machine possède plusieurs GPU, `GpuDeviceId` vous permet de cibler un GPU spécifique. `0` sélectionne le premier dispositif ; `1` choisirait le second, etc. Vous pouvez découvrir les ID disponibles en utilisant l'outil NVIDIA `nvidia-smi` ou en interrogeant la classe `GpuInfo` d'Aspose (non montré ici pour plus de concision).

---

## Étape 4 – Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être exécuté. Collez-le dans `Program.cs`, remplacez le chemin de l'image par un fichier réel sur votre disque, et appuyez sur **F5**.

```csharp
// Program.cs – Complete Aspose OCR GPU example
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Validate the input argument (optional but handy)
            if (args.Length == 0)
            {
                Console.WriteLine("Usage: dotnet run <image_path>");
                return;
            }

            string imagePath = args[0];

            // Initialise the OCR engine
            var ocrEngine = new OcrEngine();

            // -------------------- How to Enable GPU --------------------
            // Turn on GPU acceleration and optionally pick a device
            ocrEngine.Settings = new OcrSettings()
            {
                UseGpu = true,          // Enables GPU processing
                GpuDeviceId = 0         // Selects the first CUDA‑compatible GPU
            };
            // ---------------------------------------------------------

            try
            {
                // Recognise the image – this is the “image to plain text” core
                var ocrResult = ocrEngine.RecognizeImage(imagePath);

                // Display the extracted text
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrResult.Text);
            }
            catch (Exception ex)
            {
                // Graceful error handling – helpful when the GPU is unavailable
                Console.WriteLine($"Error during OCR: {ex.Message}");
            }
        }
    }
}
```

### Sortie attendue

Si l'image fournie contient la ligne *« Invoice #12345 – Total $1,250.00 »*, la console affichera :

```
=== Extracted Text ===
Invoice #12345 – Total $1,250.00
```

Le résultat est du texte brut, prêt pour un traitement ultérieur (par ex., alimentation d'une base de données ou d'un analyseur de langage naturel).

---

## Étape 5 – Vérifier l'utilisation du GPU (optionnel)

Pour vous assurer que le GPU est réellement utilisé, ouvrez votre outil de surveillance GPU (comme **NVIDIA‑Smi** ou **GPU‑Z**) pendant l'exécution du programme. Vous devriez voir un pic d'utilisation du calcul sur le dispositif sélectionné. Si vous ne voyez que de l'activité CPU, revérifiez que :

- Le pilote du GPU est à jour.
- Le drapeau `UseGpu` est défini sur `true`.
- Votre format d'image est pris en charge (PNG, JPEG, TIFF, etc.).

---

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution rapide |
|----------|--------------------------|-----------------|
| **GPU non détecté** | Pilote obsolète ou runtime CUDA manquant | Installez le dernier pilote NVIDIA et le toolkit CUDA |
| **`Aspose.OCR` throws “GPU not supported”** | Exécution sur un GPU non‑CUDA (par ex., AMD plus ancien) | Définissez `UseGpu = false` ou passez à un GPU compatible |
| **Chemin d'image incorrect** | Le chemin relatif pointe vers le mauvais dossier | Utilisez un chemin absolu ou passez le chemin en argument de ligne de commande |
| **Licence non appliquée** | Le mode d'évaluation peut limiter l'utilisation du GPU | Register a license with `License license = new License(); license.SetLicense("Aspose.OCR.lic");` |

---

## Extension de l'exemple : traitement par lots avec le GPU

Si vous devez traiter des dizaines de factures, encapsulez l'appel de reconnaissance dans une boucle. Comme le GPU reste chaud, les images suivantes bénéficient du **cache de préchauffage**, réduisant encore davantage le temps d'exécution de quelques millisecondes.

```csharp
string[] files = Directory.GetFiles(@"C:\Invoices\", "*.png");
foreach (var file in files)
{
    var result = ocrEngine.RecognizeImage(file);
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Trim()}");
}
```

N'oubliez pas de conserver la même instance `OcrEngine`—créer un nouveau moteur par fichier réinitialiserait le contexte GPU et nuirait aux performances.

---

## Conclusion

Vous disposez maintenant d'un **exemple complet d'Aspose OCR** qui montre **comment activer le GPU**, comment **définir l'ID du dispositif GPU**, et comment **lire le texte d'une image en C#**. En basculant `UseGpu` et en pointant vers le bon dispositif, vous transformez une tâche OCR lente liée au CPU en un pipeline à haut débit capable de gérer de grandes factures, reçus ou tout document numérisé.

N'hésitez pas à expérimenter : essayez différents formats d'image, ajustez `GpuDeviceId` sur des configurations multi‑GPU, ou combinez cela avec d'autres bibliothèques Aspose pour la génération de PDF. Le ciel est la limite une fois le GPU en jeu.

<img src="gpu-ocr.png" alt="comment activer le GPU avec Aspose OCR en C# – convertir rapidement une image en texte brut">

*Bon codage ! Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous ou consultez les forums officiels d'Aspose pour des approfondissements.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}