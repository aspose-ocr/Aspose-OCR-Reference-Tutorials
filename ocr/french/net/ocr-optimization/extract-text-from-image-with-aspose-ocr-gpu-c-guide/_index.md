---
category: general
date: 2026-01-06
description: extraire du texte d’une image en utilisant l’accélération GPU d’Aspose
  OCR en C#. OCR rapide pour le texte chinois, les fichiers haute résolution et plus.
draft: false
keywords:
- extract text from image
- Aspose OCR
- GPU acceleration
- C# OCR tutorial
- Chinese OCR
language: fr
og_description: extraire du texte d’une image en utilisant Aspose OCR avec accélération
  GPU en C#. Découvrez une méthode rapide et fiable pour OCR des pages chinoises haute
  résolution.
og_title: Extraire du texte d’une image avec Aspose OCR & GPU – Guide C#
tags:
- OCR
- C#
- Aspose
- Image Processing
title: extraire du texte d'une image avec Aspose OCR & GPU – Guide C#
url: /fr/net/ocr-optimization/extract-text-from-image-with-aspose-ocr-gpu-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# extraire du texte d'une image avec Aspose OCR & GPU – Tutoriel complet C#

Vous avez déjà eu besoin d'**extraire du texte d'une image** mais le fichier est énorme et le CPU rame ? Vous n'êtes pas seul—de nombreux développeurs rencontrent ce problème lorsqu'ils traitent des numérisations haute résolution ou des documents multilingues. La bonne nouvelle, c'est qu'Aspose OCR propose une solution accélérée par GPU, transformant une tâche lente en une opération quasi instantanée.

Dans ce guide, nous vous montrerons exactement comment configurer Aspose OCR en C#, activer l'accélération GPU basée sur CUDA, et **extraire du texte d'une image** comme un pro. Nous parcourrons également un scénario réel — reconnaître du texte chinois simplifié sur un TIFF de plusieurs mégaoctets—afin que vous puissiez copier‑coller le code directement dans votre projet.

## Ce que vous apprendrez

À la fin de ce tutoriel, vous serez capable de :

* Installer et référencer le package NuGet Aspose.OCR.  
* Passer le moteur OCR à **l'accélération GPU** pour des gains de vitesse massifs.  
* Choisir la langue optimale (par ex. **Chinese OCR**) qui bénéficie du pipeline GPU.  
* Charger des images haute résolution et **extraire du texte d'une image** de façon fiable.  
* Gérer les pièges courants tels que la sélection du dispositif GPU et les limites de mémoire.

Aucune expérience préalable en programmation GPU n'est requise—juste une configuration C# de base et une carte graphique compatible.

## Prérequis

* .NET 6.0 ou ultérieur (le code fonctionne également sur .NET Core et .NET Framework).  
* Un GPU compatible CUDA (NVIDIA GeForce, Quadro ou Tesla).  
* Visual Studio 2022 (ou tout autre éditeur de votre choix).  
* Le package NuGet Aspose.OCR : `Install-Package Aspose.OCR`.  

Si l'un de ces éléments vous manque, résolvez‑le d'abord—en particulier le pilote GPU, sinon le drapeau `UseGpu` reviendra silencieusement au CPU.

---

## Étape 1 : Configurer le moteur OCR pour **extraire du texte d'une image**

Tout d'abord, créez une instance de `OcrEngine`, activez le mode GPU, et choisissez éventuellement l'index du dispositif GPU (0 correspond à la première carte).

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;

// Initialize OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable CUDA‑based GPU acceleration
    UseGpu = true,

    // Optional: select a specific GPU device (0 = first GPU)
    GpuDeviceId = 0
};
```

**Pourquoi c’est important :** Activer `UseGpu` déplace le pré‑traitement d’image lourd et l’inférence du réseau neuronal sur la carte graphique, ce qui peut être 5‑10× plus rapide que le CPU pour les grandes images. Si vous sautez cette étape, vous obtiendrez toujours des résultats précis, mais la perte de performance sera perceptible sur les gros fichiers.

> **Astuce pro :** Vérifiez que votre GPU est reconnu en affichant `OcrEngine.IsGpuSupported`. S’il renvoie `false`, revérifiez la version de votre pilote.

## Étape 2 : Choisir une langue qui bénéficie du traitement GPU

Aspose OCR prend en charge de nombreuses langues, mais certaines (comme **Chinese OCR**) possèdent des jeux de caractères plus vastes et profitent donc davantage de l’exécution parallèle sur GPU.

```csharp
// Select Chinese Simplified for this example
ocrEngine.Language = OcrLanguage.ChineseSimplified;
```

Vous pouvez remplacer cela par `OcrLanguage.English` ou toute autre langue prise en charge—souvenez‑vous simplement que la langue doit être installée dans le package Aspose OCR que vous utilisez.

## Étape 3 : Charger une image haute résolution

Le moteur travaille avec `ImageStream`, qui abstrait la gestion des fichiers. Pointez‑le vers votre fichier TIFF, PNG ou JPEG.

```csharp
// Load a high‑resolution TIFF image
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\big_chinese_page.tif");
```

**Cas particulier :** Si votre image dépasse 8 KB en mémoire, envisagez de la sous‑échantillonner d’abord afin d’éviter les erreurs de dépassement de mémoire sur les GPU plus anciens. Un redimensionnement rapide avec `Bitmap` (en conservant le DPI) peut garder la précision tout en s’insérant dans la VRAM.

## Étape 4 : Exécuter la reconnaissance et obtenir le **texte extrait**

Appelez maintenant `Recognize()`. Si cela renvoie `true`, le résultat OCR est stocké dans `ocrEngine.Text`.

```csharp
if (ocrEngine.Recognize())
{
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.Error.WriteLine("OCR failed. Check the image format and GPU settings.");
}
```

Le résultat sera une chaîne Unicode plain contenant tous les caractères reconnus. Pour le chinois, vous verrez les glyphes réels, pas des octets corrompus—Aspose gère Unicode en interne.

### Résultat attendu

En supposant que le TIFF source contienne un paragraphe de chinois simplifié, vous pourriez obtenir quelque chose comme :

```
=== Extracted Text ===
在这个示例中，我们演示如何使用Aspose OCR与GPU加速来提取图像中的文本。
```

Si l’image est en anglais, le même code renverra la transcription anglaise.

## Exemple complet fonctionnel

Voici le programme complet, autonome, que vous pouvez copier‑coller dans un nouveau projet console.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with GPU support
            OcrEngine ocrEngine = new OcrEngine
            {
                UseGpu = true,          // Switch pipelines to CUDA
                GpuDeviceId = 0         // Optional: select the first GPU
            };

            // Verify GPU availability (optional but helpful)
            if (!ocrEngine.IsGpuSupported)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
            }

            // 2️⃣ Choose language (Chinese Simplified for this demo)
            ocrEngine.Language = OcrLanguage.ChineseSimplified;

            // 3️⃣ Load a high‑resolution image
            string imagePath = @"C:\Images\big_chinese_page.tif";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // 4️⃣ Perform recognition
            if (ocrEngine.Recognize())
            {
                Console.WriteLine("=== Extracted Text ===");
                Console.WriteLine(ocrEngine.Text);
            }
            else
            {
                Console.Error.WriteLine("Recognition failed – check the image and GPU settings.");
            }
        }
    }
}
```

Enregistrez‑le sous le nom `Program.cs`, exécutez `dotnet run`, et observez la console afficher le résultat OCR. C’est tout—vous venez d'**extraire du texte d'une image** en utilisant Aspose OCR avec l'accélération GPU.

## Questions fréquentes & pièges

| Question | Réponse |
|----------|---------|
| **Et si je n’ai pas de GPU compatible CUDA ?** | Définissez `UseGpu = false` ; le moteur utilisera automatiquement le chemin CPU. |
| **Puis-je traiter plusieurs images dans une boucle ?** | Oui—réutilisez la même instance `OcrEngine`, il suffit d’assigner un nouveau `ImageStream` à chaque itération. |
| **Comment gérer les fuites de mémoire ?** | Appelez `ocrEngine.Dispose()` lorsque vous avez terminé, surtout dans les services de longue durée. |
| **Y a‑t‑il une limite de taille d’image ?** | La limite pratique est la VRAM de votre GPU. Pour des images > 4 Go, envisagez de diviser l’image en morceaux plus petits. |
| **Où obtenir la licence Aspose OCR ?** | Demandez un essai gratuit sur Aspose.com, puis définissez `ocrEngine.License = new License("Aspose.OCR.lic");`. |

## Prochaines étapes & sujets liés

Maintenant que vous pouvez **extraire du texte d'une image** efficacement, vous pourriez explorer :

* **Pipelines OCR par lots** – combinez ce code avec `Parallel.ForEach` pour des ensembles de documents massifs.  
* **Post‑traitement** – utilisez des expressions régulières pour nettoyer les artefacts OCR courants.  
* **Intégration avec Azure Cognitive Services** – comparez l’OCR local GPU avec l’OCR cloud pour les compromis coût/précision.  
* **Prise en charge d’autres langues** – changez simplement `OcrLanguage` en japonais, arabe, etc.  

Chacune de ces options s’appuie sur les bases que nous avons posées ici, en tirant parti du même moteur Aspose OCR et de l’accélération GPU.

---

### Conclusion

Vous venez d’apprendre comment **extraire du texte d'une image** en utilisant le moteur OCR accéléré par GPU d’Aspose OCR en C#. En initialisant le moteur, en activant CUDA, en choisissant la bonne langue, en chargeant une image haute résolution et en appelant `Recognize()`, vous obtenez des résultats OCR rapides et fiables—même pour des scripts complexes comme le chinois.  

Testez‑le avec vos propres documents, expérimentez différentes langues, et constatez le gain de performance. En cas de problème, consultez le tableau « Questions fréquentes » ou laissez un commentaire—bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}