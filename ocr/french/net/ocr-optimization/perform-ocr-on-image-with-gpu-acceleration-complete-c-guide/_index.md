---
category: general
date: 2026-02-11
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) sur
  une image en utilisant le GPU OCR en C#. Ce tutoriel étape par étape couvre la configuration,
  le code et les meilleures pratiques.
draft: false
keywords:
- perform OCR on image
- use GPU OCR
- Aspose OCR C#
- GPU acceleration OCR
- OCR performance tuning
language: fr
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  en utilisant le GPU OCR en C#. Suivez ce guide pour une solution rapide et fiable
  avec Aspose OCR.
og_title: Effectuer la reconnaissance optique de caractères sur une image avec GPU
  – Implémentation complète en C#
tags:
- OCR
- C#
- Aspose
- GPU Computing
title: Effectuer la reconnaissance optique de caractères sur une image avec accélération
  GPU – Guide complet C#
url: /fr/net/ocr-optimization/perform-ocr-on-image-with-gpu-acceleration-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer l'OCR sur une image avec accélération GPU – Guide complet C#

Vous avez déjà eu besoin d'**effectuer l'OCR sur une image** mais votre CPU était submergé par d'énormes fichiers TIFF ? Vous n'êtes pas seul. Dans de nombreux projets réels, le traitement de gros documents peut transformer quelques secondes en minutes, et ce ralentissement pénalise à la fois les utilisateurs et les budgets.  

La bonne nouvelle ? En tirant parti d’un GPU, vous pouvez réduire ces temps de traitement de façon spectaculaire. Dans ce tutoriel, nous parcourrons un exemple pratique qui montre exactement **comment effectuer l'OCR sur une image** en utilisant le moteur accéléré par GPU d’Aspose, ainsi qu’une poignée de conseils pratiques que vous ne trouverez pas dans la documentation générique.

> **Ce que vous obtiendrez :** une application console C# prête à l’emploi, des explications ligne par ligne, et des conseils de dépannage pour les problèmes courants. Aucun référentiel externe requis — tout ce dont vous avez besoin se trouve ici.

## Ce qu’il vous faut

Avant de commencer, assurez‑vous d’avoir les éléments suivants installés sur votre machine de développement :

| Prérequis | Version minimale |
|--------------|-----------------|
| .NET 6.0 SDK ou ultérieur | 6.0 |
| Visual Studio 2022 (ou tout autre IDE) | 17.0 |
| Aspose.OCR for .NET (package NuGet) | 23.11 ou plus récent |
| Un GPU compatible CUDA (NVIDIA) | Compute Capability 3.5+ |
| Une image d’exemple – par ex. `large_document.tif` | n’importe quelle taille |

Si l’un de ces points vous est inconnu, ne paniquez pas. La fonctionnalité **use GPU OCR** fonctionne même sur des GPU modestes, et le package NuGet récupérera automatiquement tous les binaires natifs nécessaires.

## Étape 1 : Effectuer l'OCR sur une image avec accélération GPU

La première chose dont nous avons besoin est une instance du moteur OCR activé GPU. Cet objet effectue le travail lourd sur la carte graphique, tout en exposant une API propre et synchrone.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System.Drawing;

// Create a GPU‑accelerated OCR engine and configure it
var ocrEngine = new GpuOcrEngine
{
    // Select the first GPU in the system (device index 0)
    DeviceId = 0,
    // Let the engine download language packs automatically if they’re missing
    AutomaticResourceDownload = true,
    // Specify the language you want to recognize – English in this case
    Language = OcrLanguage.English
};
```

**Pourquoi c’est important :**  
- `DeviceId = 0` indique à la bibliothèque d’utiliser le GPU principal ; vous pouvez le modifier si vous avez plusieurs cartes.  
- `AutomaticResourceDownload = true` empêche une erreur d’exécution lorsque les données linguistiques anglaises ne sont pas présentes localement.  
- Définir explicitement `Language` évite le recours par défaut du moteur à un modèle générique plus lent.

> **Astuce pro :** Si vous exécutez sur un serveur sans affichage, assurez‑vous que le pilote NVIDIA est installé et que la commande `nvidia-smi` indique le GPU comme « Online ». Sinon le moteur reviendra silencieusement au CPU.

## Étape 2 : Charger votre fichier image

Ensuite, chargez l’image sur laquelle vous souhaitez lancer l’OCR. Aspose fonctionne avec n’importe quel `System.Drawing.Image`, vous pouvez donc fournir du JPEG, PNG, TIFF, ou même des PDF multi‑pages (après conversion).

```csharp
// Load the image from disk – replace the path with your own file location
using var image = Image.FromFile(@"C:\OCR\Samples\large_document.tif");
```

**Pourquoi c’est important :**  
- Utiliser une instruction `using` garantit que les ressources non gérées de l’image sont libérées rapidement, ce qui est crucial lorsque vous traitez de nombreux fichiers dans une boucle.  
- Si votre image est exceptionnellement grande (par ex. > 500 Mo), envisagez de la sous‑échantillonner d’abord afin de garder la consommation de mémoire GPU sous contrôle.

## Étape 3 : Reconnaître le texte avec le moteur OCR GPU

Nous transmettons maintenant l’image au moteur GPU et attendons le résultat. La méthode `Recognize` renvoie un objet `OcrResult` contenant le texte extrait et les métriques de performance.

```csharp
// Perform OCR – this call runs on the GPU
var ocrResult = ocrEngine.Recognize(image);
```

**Pourquoi c’est important :**  
- L’appel est synchrone, ce qui signifie que le thread se bloque jusqu’à ce que le GPU ait fini. Dans une application UI, vous voudrez exécuter cela sur un thread d’arrière‑plan pour garder l’interface réactive.  
- `ocrResult.ProcessingTime` vous donne le temps écoulé en millisecondes, idéal pour comparer **use GPU OCR** aux alternatives CPU‑only.

## Étape 4 : Afficher les résultats et les statistiques

Enfin, nous affichons la longueur du texte reconnu et la durée de l’opération. Dans une vraie application, vous écririez probablement `ocrResult.Text` dans un fichier ou une base de données.

```csharp
// Show a quick summary on the console
Console.WriteLine($"Recognized {ocrResult.Text.Length} characters in {ocrResult.ProcessingTime} ms");

// Optionally, dump the full text (commented out for brevity)
// Console.WriteLine(ocrResult.Text);
```

**Sortie attendue (exemple) :**

```
Recognized 12457 characters in 312 ms
```

Remarquez que le temps de traitement est mesuré en quelques centaines de millisecondes pour un TIFF de plusieurs mégaoctets — exactement l’accélération attendue lorsque vous **use GPU OCR**.

![exemple d'exécution d'OCR sur image](/images/perform-ocr-on-image.png "Capture d'écran montrant la sortie console après l'exécution de l'OCR sur image")

*La capture d'écran ci‑dessus illustre la sortie console après l'exécution de l'OCR sur image avec accélération GPU.*

## Utiliser GPU OCR efficacement

Même si le code ci‑dessus fonctionne immédiatement, les déploiements en production rencontrent souvent quelques obstacles. Voici les problèmes les plus courants et leurs solutions.

| Problème | Cause | Solution |
|-------|-------|----------|
| **Out‑of‑memory (GPU)** | Image trop grande pour la VRAM du GPU | Réduire l’échelle de l’image (`Bitmap` resize) avant d’appeler `Recognize`. |
| **Language pack not found** | `AutomaticResourceDownload` désactivé ou pas d’accès Internet | Pré‑télécharger le pack linguistique via `ocrEngine.DownloadResources(OcrLanguage.English)`. |
| **Slow first run** | Compilation JIT du pilote GPU | Réchauffer le moteur en exécutant une petite image factice au démarrage. |
| **Incorrect character set** | Propriété `Language` incorrecte | Définir `Language` sur l’énumération correcte (par ex. `OcrLanguage.French`). |

**Astuce pro :** Lorsque vous traitez des dizaines de fichiers en lot, réutilisez la même instance de `GpuOcrEngine`. Créer un nouveau moteur pour chaque fichier entraîne un coûteux basculement de contexte GPU.

## Exemple complet fonctionnel

Voici le programme complet, rassemblé en un seul fichier que vous pouvez copier‑coller dans un nouveau projet console.

```csharp
// File: Program.cs
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.Drawing;

namespace GpuOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize GPU OCR engine
            var ocrEngine = new GpuOcrEngine
            {
                DeviceId = 0,
                AutomaticResourceDownload = true,
                Language = OcrLanguage.English
            };

            // 2️⃣ Load the image (adjust the path to your file)
            using var image = Image.FromFile(@"C:\OCR\Samples\large_document.tif");

            // 3️⃣ Run recognition on the GPU
            var ocrResult = ocrEngine.Recognize(image);

            // 4️⃣ Output statistics
            Console.WriteLine($"Recognized {ocrResult.Text.Length} characters in {ocrResult.ProcessingTime} ms");

            // Optional: write the extracted text to a file
            // System.IO.File.WriteAllText("output.txt", ocrResult.Text);
        }
    }
}
```

Enregistrez le fichier, exécutez `dotnet run`, et vous devriez voir le nombre de caractères et le temps de traitement affichés dans la console. Si vous ouvrez `output.txt` (décommentez la ligne), vous verrez le texte OCR brut prêt pour un traitement en aval.

## Conclusion

Nous venons de vous montrer **comment effectuer l'OCR sur une image** en utilisant le moteur accéléré GPU d’Aspose, depuis la configuration du `GpuOcrEngine` jusqu’au traitement du résultat et au dépannage des problèmes courants. En déléguant le travail lourd à la carte graphique, vous obtenez des améliorations de vitesse d’un ordre de grandeur — exactement ce qu’il faut lorsqu’on travaille avec de gros documents ou des scénarios de numérisation en temps réel.

> **À retenir :** La combinaison de `GpuOcrEngine`, de la gestion automatique des ressources et d’une taille d’image adaptée vous fournit une chaîne robuste et haute performance pour tout projet C# qui doit **use GPU OCR**.

### Et après ?

- **Traitement par lots :** Enveloppez la logique principale dans une boucle `foreach` pour gérer des dossiers d’images.  
- **Parallélisme :** Combinez GPU OCR avec `Parallel.ForEach` pour les serveurs multi‑GPU.  
- **Post‑traitement :** Alimentez `ocrResult.Text` dans un correcteur orthographique ou un extracteur d’entités pour des analyses en aval plus intelligentes.  

N’hésitez pas à expérimenter — remplacez `OcrLanguage.English` par une autre langue, testez différents formats d’image, ou intégrez le moteur dans une API ASP.NET. Le ciel est la limite lorsque vous **use GPU OCR** de manière responsable.

Bon codage, et que vos tâches OCR s’exécutent à la vitesse de l’éclair !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}