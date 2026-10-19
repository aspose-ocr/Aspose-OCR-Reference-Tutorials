---
category: general
date: 2026-03-18
description: Configurez le dispositif GPU dans Aspose OCR pour extraire rapidement
  le texte d’une image. Apprenez comment charger une image pour l’OCR, reconnaître
  une image de reçu et obtenir des résultats précis.
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: fr
og_description: Définissez le dispositif GPU dans Aspose OCR pour extraire rapidement
  le texte d’une image. Suivez ce guide étape par étape pour charger l’image pour
  l’OCR et reconnaître l’image d’un reçu.
og_title: Définir le périphérique GPU pour l'OCR en C# – Guide complet de programmation
tags:
- OCR
- C#
- GPU
- Aspose
title: Définir le périphérique GPU pour l'OCR en C# – Guide complet de programmation
url: /fr/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir le périphérique GPU pour l'OCR en C# – Guide de programmation complet

Besoin de **définir le périphérique GPU** pour un traitement OCR plus rapide ? Dans ce guide, nous vous montrerons exactement comment définir le périphérique GPU avec Aspose OCR, puis extraire le texte d’une image de reçu en quelques lignes de code.  

Si vous avez déjà eu du mal à **charger l’image pour l'OCR** ou vous vous êtes demandé *comment extraire du texte* à partir de scans haute résolution, vous êtes au bon endroit. À la fin, vous disposerez d’un programme exécutable qui reconnaît une image de reçu, affiche le texte brut et revient gracieusement à la CPU si le GPU n’est pas disponible.

## Ce que couvre ce tutoriel

Nous aborderons tout ce que vous devez savoir :

* Installation du package NuGet Aspose OCR (la seule dépendance externe).  
* Définition du périphérique GPU (`set GPU device`) et, éventuellement, choix d’un autre indice GPU.  
* Chargement d’un fichier image pour l'OCR – oui, cela inclut l’étape redoutée « charger l’image pour l'OCR » qui bloque de nombreux débutants.  
* Exécution du moteur de reconnaissance pour **reconnaître l’image du reçu**.  
* Extraction de la chaîne résultante afin que vous puissiez **extraire du texte à partir de l’image** et l’utiliser dans votre application.  

Pas de magie, pas de liens cachés – juste une solution complète et autonome que vous pouvez copier‑coller dans Visual Studio et exécuter dès aujourd’hui.

## Prérequis

* .NET 6.0 ou supérieur (le code fonctionne également sur .NET Core et .NET Framework).  
* Une machine équipée d’un GPU avec les pilotes appropriés installés – sinon la bibliothèque basculera automatiquement en mode CPU.  
* Une image de reçu d’exemple (par ex., `receipt_highres.png`) placée quelque part où vous pouvez la référencer avec un chemin complet.  

C’est tout. Si le package NuGet vous manque, exécutez `dotnet add package Aspose.OCR` dans le dossier de votre projet.

---

## Étape 1 – Définir le périphérique GPU dans Aspose OCR

La première chose à faire est de **définir le périphérique GPU** sur le moteur OCR. Cela indique à Aspose de déléguer le travail lourd à la carte graphique plutôt qu’au processeur.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**Pourquoi c’est important :**  
Lorsque le moteur fonctionne en `ProcessingMode.Gpu`, les noyaux CUDA sous‑jacents peuvent accélérer la segmentation des caractères et l’inférence du réseau de neurones de façon spectaculaire. Sur un RTX 3080 moderne, vous verrez les temps d’OCR passer de plusieurs secondes à moins d’une seconde pour des reçus haute résolution.

> **Astuce :** Si vous ne savez pas quel indice GPU utiliser, appelez `OcrEngine.GetAvailableGpuDevices()` (disponible dans les versions récentes) et choisissez celui qui possède le plus de mémoire libre.

---

## Étape 2 – Charger l’image pour l'OCR

Maintenant que le moteur est configuré, nous devons **charger l’image pour l'OCR**. Aspose fournit un wrapper pratique `ImageStream` qui abstrait les I/O de fichiers et prend en charge les flux depuis la mémoire, le réseau ou le disque.

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**Que pourrait mal se passer ?**  
Si le chemin du fichier est incorrect ou que l’image est corrompue, `FromFile` lèvera une `FileNotFoundException`. Un rapide contrôle `File.Exists(imagePath)` avant de créer le flux vous évite un plantage désagréable.

---

## Étape 3 – Reconnaître l’image du reçu

Avec l’image en main, nous appelons `Recognize`. C’est l’étape qui **reconnaît l’image du reçu** en utilisant le pipeline accéléré par GPU que nous avons configuré précédemment.

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**Dans les coulisses :**  
Le moteur convertit d’abord l’image en un bitmap en niveaux de gris normalisé, puis exécute un modèle d’apprentissage profond qui prédit les probabilités des caractères. Parce que nous sommes sur GPU, le modèle traite l’ensemble du bitmap en parallèle, ce qui explique pourquoi les gros reçus sont traités rapidement.

---

## Étape 4 – Extraire le texte de l’image et vérifier la sortie

Enfin, nous récupérons le résultat texte brut du `OcrResult` et l’écrivons dans la console. C’est le moment où vous **extrayez du texte à partir de l’image** et pouvez le transmettre à une logique en aval (par ex., l’analyse des lignes d’articles).

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**Sortie attendue :**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

Si le texte apparaît illisible, revérifiez que l’image est en haute résolution et que le pilote GPU est à jour. Vous pouvez également basculer `ocrEngine.Settings.PreprocessMode` pour améliorer le contraste des reçus mal éclairés.

---

## Étape 5 – Repli sur la CPU (Gestion des cas limites)

Que se passe-t-il si la machine cible ne possède pas de GPU compatible ? Au lieu de planter, vous pouvez détecter la situation et basculer vers le traitement CPU.

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**Pourquoi inclure cela ?**  
Dans les pipelines CI ou les conteneurs cloud, vous exécutez souvent sur des serveurs sans tête dépourvus de GPU. Une dégradation gracieuse garantit que le même code fonctionne partout.

---

## Pièges courants et conseils pratiques

| Piège | Comment l’éviter |
|-------|-------------------|
| Oublier de définir `ProcessingMode` avant de charger l’image. | Toujours configurer le moteur d’abord (Étape 1). |
| Utiliser le mauvais indice GPU (`GpuDeviceId`). | Interroger les appareils disponibles ou rester avec la valeur par défaut `0`. |
| Charger une image basse résolution, ce qui réduit la précision de l’OCR. | Viser au moins 300 DPI pour les reçus. |
| Ne pas disposer `ImageStream` – entraîne des verrous de fichiers. | Envelopper le flux dans un bloc `using` ou appeler `Dispose()` manuellement. |
| Ignorer le drapeau `IsGpuAvailable` sur les machines sans CUDA. | Ajouter la logique de repli de l’Étape 5. |

---

## Exemple complet fonctionnel (prêt à copier‑coller)

Voici le programme complet, prêt à être compilé. Enregistrez‑le sous `Program.cs`, ajoutez le package NuGet Aspose OCR, puis exécutez.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

L’exécution du programme affiche le texte du reçu extrait dans la console, exactement comme montré précédemment. Vous pouvez maintenant acheminer cette chaîne vers un analyseur, une base de données ou toute autre logique métier dont vous avez besoin.

---

## Conclusion

Nous vous avons montré comment **définir le périphérique GPU** dans Aspose OCR, **charger l’image pour l'OCR**, et **reconnaître l’image du reçu** afin que vous puissiez **extraire du texte à partir de l’image** avec une vitesse fulgurante. L’exemple complet et exécutable démontre à la fois le *comment* et le *pourquoi*, vous offrant une base solide pour tout projet C# OCR nécessitant une accélération GPU.

Prêt pour l’étape suivante ? Essayez d’expérimenter avec :

* Le traitement de plusieurs images en parallèle grâce à `Parallel.ForEach`.  
* L’ajustement de `ocrEngine.Settings.PreprocessMode` pour améliorer les résultats sur des scans à faible contraste.  
* L’exportation de la sortie OCR au format JSON pour des analyses en aval.  

N’hésitez pas à laisser un commentaire si vous rencontrez des difficultés, et bon codage !

![Diagramme montrant comment définir le périphérique GPU pour le traitement OCR](set-gpu-device.png "définir le périphérique GPU")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}