---
category: general
date: 2026-04-06
description: Extrayez du texte d’une image en utilisant Aspose OCR GPU en C#. Apprenez
  à charger une image depuis un fichier et à définir la limite de mémoire GPU dans
  ce guide étape par étape.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: fr
og_description: Extraire du texte d’une image en utilisant Aspose OCR GPU en C#. Apprenez
  à charger une image depuis un fichier et à définir la limite de mémoire GPU dans
  ce guide étape par étape.
og_title: Extraire du texte d’une image avec Aspose OCR GPU – Guide complet C#
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Extraire du texte d’une image avec Aspose OCR GPU – Guide complet C#
url: /fr/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image avec Aspose OCR GPU – Guide complet C#

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais vous êtes resté bloqué au moment où les performances comptaient ? Vous n'êtes pas seul — de nombreux développeurs rencontrent le même obstacle lorsque l'OCR devient un goulot d'étranglement. Dans ce tutoriel, nous vous montrerons exactement comment extraire du texte d'une image en utilisant le runtime GPU d'Aspose OCR, charger une image depuis un fichier, et même définir une limite de mémoire GPU pour un contrôle plus strict des ressources.

Nous parcourrons un exemple complet, prêt à l'exécution en C#, expliquerons pourquoi chaque ligne est importante et soulignerons les pièges courants que vous pourriez rencontrer. À la fin, vous disposerez d'une base solide pour créer des pipelines OCR rapides et évolutifs qui s'exécutent sur le GPU.

## Ce que couvre ce guide

- **Prerequisites** : .NET 6+ (ou .NET Framework 4.6+), package NuGet Aspose.OCR, un pilote GPU compatible.
- **Step‑by‑step code** qui charge une image depuis un fichier, configure le moteur GPU d'Aspose OCR, et extrait le texte.
- **Why** vous pourriez vouloir définir une limite de mémoire GPU et comment le faire en toute sécurité.
- **Edge‑case handling** : images basse résolution, GPU manquant, et dépannage des scores de confiance.
- **Next steps** : traitement par lots, intégration avec ASP.NET Core, et retour au CPU si nécessaire.

> **Conseil pro** : Si vous n'êtes pas sûr que votre GPU soit utilisé, vérifiez le moniteur d'activité GPU (par ex., NVIDIA‑SMI) pendant l'exécution de l'OCR. Vous verrez une pointe d'utilisation de la mémoire qui correspond à la limite que vous avez définie.

![Diagramme montrant le flux d'extraction de texte d'une image à l'aide du moteur Aspose OCR GPU](extract-text-from-image-aspose-ocr-gpu.png "extraction de texte d'une image avec Aspose OCR GPU")

## Étape 1 : Initialiser le moteur Aspose OCR pour le traitement GPU

La première chose dont vous avez besoin est une instance `OcrEngine` qui sait qu'elle doit s'exécuter sur le GPU. Aspose fournit un objet `OcrEngineSettings` propre où vous pouvez spécifier le runtime.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Pourquoi c'est important** : Par défaut, Aspose OCR revient au CPU, ce qui suffit pour les petites images mais peut être extrêmement lent pour les photos haute résolution. Définir explicitement `Runtime = OcrRuntime.Gpu` décharge le travail lourd sur la carte graphique, vous offrant un gain de vitesse notable.

## Étape 2 : (Optionnel) Définir une limite de mémoire GPU

Si vous exécutez sur une station de travail partagée ou un conteneur avec des ressources GPU limitées, vous pouvez plafonner la quantité de mémoire que le moteur OCR consomme. Cela empêche les plantages hors mémoire et garde les autres processus satisfaits.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**Quand l'utiliser** :  
- **Environnements multi‑locataires** où plusieurs services partagent le même GPU.  
- **Pipelines CI/CD** qui allouent une quantité fixe de mémoire GPU par job.  

Si vous omettez cette ligne, Aspose utilisera autant de mémoire que nécessaire, ce qui convient sur une station de travail dédiée.

## Étape 3 : Charger l'image depuis un fichier

Nous devons maintenant charger l'image en mémoire. Aspose OCR travaille avec `System.Drawing.Image`, nous utiliserons donc `Image.FromFile`. Assurez‑vous que le chemin pointe vers un fichier réel ; sinon une exception sera levée.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Pourquoi le chargement depuis un fichier est important** : De nombreux développeurs essaient d'alimenter directement un tableau d'octets, ce qui fonctionne mais ajoute une étape de conversion inutile. Utiliser `Image.FromFile` est simple, et l'instruction `using` garantit que le handle du fichier est libéré rapidement.

## Étape 4 : Exécuter l'OCR et récupérer le résultat

Avec le moteur configuré et l'image chargée, nous pouvons enfin extraire le texte. La méthode `Recognize` renvoie un `OcrResult` contenant à la fois le texte brut et un score de confiance.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Comprendre la sortie** :  
- `Confidence` est une valeur comprise entre 0 et 1. Une confiance de 0,95 (ou 95 %) signifie généralement que l'OCR est précis.  
- `Text` contient les sauts de ligne tels qu'ils apparaissent dans l'image, ce qui est pratique pour un traitement ultérieur.

## Étape 5 : Vérifier la sortie et gérer les cas limites

### Vérification des niveaux de confiance

Si la confiance descend en dessous, disons, de 80 %, vous pourriez vouloir revenir au traitement CPU ou appliquer un prétraitement d'image (par ex., binarisation).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Gestion d'un GPU manquant

Toutes les machines ne disposent pas d'un GPU compatible. Aspose lèvera une `OcrException` s'il ne peut pas initialiser le runtime GPU.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Images haute résolution

Les images très grandes (par ex., > 4000 px de largeur) peuvent consommer beaucoup de mémoire GPU. Si vous atteignez la limite que vous avez définie précédemment, Aspose tronquera le traitement. Dans de tels cas, réduisez d'abord la taille de l'image :

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console. Il inclut toutes les étapes, la gestion des erreurs et la logique de repli optionnelle.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Sortie attendue

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Si la confiance chute en dessous du seuil, vous verrez les messages supplémentaires de repli sur le CPU.

---

## Conclusion

Vous savez maintenant **comment extraire du texte d'une image** en utilisant le moteur GPU d'Aspose OCR, comment **charger une image depuis un fichier**, et pourquoi vous pourriez vouloir **définir une limite de mémoire GPU** pour les charges de travail en production. L'exemple ci‑dessus est une solution entièrement fonctionnelle, digne d'être citée, que vous pouvez intégrer à n'importe quel projet .NET.

Et après ? Envisagez :

- **Traitement par lots** : parcourir un dossier d'images et écrire les résultats dans un CSV.  
- **Intégration ASP.NET Core** : exposer un point d'API qui accepte une image téléchargée et renvoie le texte OCR.  
- **Optimisation des performances** : expérimenter différentes valeurs de `GpuMemoryLimit` et surveiller l'utilisation du GPU pour trouver le point optimal.

N'hésitez pas à adapter le code à votre propre scénario—que vous construisiez un pipeline de numérisation de documents, une application de traduction en temps réel, ou un service de numérisation de reçus. Les principes restent les mêmes : initialiser le moteur GPU, gérer la mémoire judicieusement, et toujours vérifier la confiance.

Des questions ou un problème ? Laissez un commentaire ci‑dessous, et résolvons-le ensemble. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}