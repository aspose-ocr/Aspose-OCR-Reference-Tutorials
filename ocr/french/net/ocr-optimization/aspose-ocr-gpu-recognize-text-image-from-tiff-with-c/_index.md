---
category: general
date: 2026-05-21
description: Aspose OCR GPU vous permet de reconnaître rapidement le texte d’une image.
  Apprenez comment charger une image pour l’OCR, extraire le texte d’un TIFF et améliorer
  les performances.
draft: false
keywords:
- aspose ocr gpu
- recognize text image
- ocr tiff image
- load image for ocr
- extract text from tiff
language: fr
og_description: Aspose OCR GPU accélère l'extraction de texte. Ce guide montre comment
  charger une image pour l'OCR, reconnaître le texte de l'image et extraire le texte
  d'un TIFF efficacement.
og_title: Aspose OCR GPU – Reconnaître le texte d’une image TIFF en C#
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  headline: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  type: TechArticle
- description: Aspose OCR GPU lets you recognize text image quickly. Learn how to
    load image for OCR, extract text from TIFF and boost performance.
  name: 'Aspose OCR GPU: Recognize Text Image from TIFF with C#'
  steps:
  - name: Enables GPU acceleration (optional, with automatic CPU fallback).
    text: Enables GPU acceleration (optional, with automatic CPU fallback).
  - name: Creates an `OcrEngine` configured for English.
    text: Creates an `OcrEngine` configured for English.
  - name: Loads a large **OCR TIFF image** from disk.
    text: Loads a large **OCR TIFF image** from disk.
  - name: Runs the recognition and prints the result.
    text: Runs the recognition and prints the result.
  type: HowTo
tags:
- aspose
- ocr
- csharp
title: 'Aspose OCR GPU : Reconnaître le texte d’une image TIFF avec C#'
url: /fr/net/ocr-optimization/aspose-ocr-gpu-recognize-text-image-from-tiff-with-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU : Reconnaître une image texte à partir d'un TIFF avec C#

Vous vous êtes déjà demandé comment **reconnaître une image texte** à partir d'un fichier TIFF massif sans épuiser votre CPU ? Vous n'êtes pas le seul. Dans de nombreuses chaînes de traitement de documents, le goulot d'étranglement est l'étape OCR, surtout lorsque vous lancez des gigaoctets de pages numérisées sur un moteur basique.  

Bonne nouvelle ? **Aspose OCR GPU** peut turbo‑charger le processus, et l’exemple de code ci‑dessous montre exactement comment **charger une image pour l’OCR**, **extraire du texte d’un TIFF**, et revenir proprement à la CPU si aucun GPU n’est présent. Plongeons‑y.

## Ce que couvre ce tutoriel

Nous allons parcourir un programme C# complet, prêt à copier‑coller, qui :

1. Active l’accélération GPU (optionnelle, avec repli automatique sur le CPU).  
2. Crée un `OcrEngine` configuré pour l'anglais.  
3. Charge une grande **image OCR TIFF** depuis le disque.  
4. Exécute la reconnaissance et affiche le résultat.  

À la fin, vous comprendrez **pourquoi** chaque étape est importante, comment gérer les cas limites courants, et vous disposerez d’un exemple exécutable que vous pourrez adapter aux PDF, aux TIFF multi‑pages ou même aux flux vidéo en temps réel.

> **Prérequis** – .NET 6+ (ou .NET Framework 4.7+), le package NuGet Aspose.OCR, et une machine avec GPU si vous voulez voir le gain de vitesse. Aucun matériel spécial n’est requis ; le code utilisera simplement le CPU lorsqu’aucun GPU n’est détecté.

---

![Aspose OCR GPU processing diagram showing CPU fallback](/images/aspose-ocr-gpu-diagram.png){: .align-center alt="Diagramme de traitement Aspose OCR GPU montrant le repli sur le CPU"}

## Étape 1 : Activer l’accélération GPU (Optionnel)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

// Enable GPU if a compatible device is present.
// The call is safe – if no GPU is found Aspose falls back to CPU.
OcrEngine.EnableGpu(true);
```

**Pourquoi c’est important :**  
Les cœurs GPU excellent dans le parallélisme massif requis pour le pré‑traitement d’image (binarisation, suppression du bruit) et l’inférence de réseaux neuronaux. En activant `EnableGpu(true)`, vous donnez au moteur le feu vert pour déléguer ces tâches. Si la machine ne possède pas de carte compatible CUDA, Aspose repasse silencieusement au CPU, évitant ainsi tout plantage brutal.

**Astuce :** Sous Windows, il peut être nécessaire d’installer le dernier pilote NVIDIA ainsi que le toolkit CUDA. Sous Linux, assurez‑vous que le `nvidia‑driver` et `libcuda.so` se trouvent dans votre chemin de bibliothèques.

## Étape 2 : Créer et configurer le moteur OCR

```csharp
// Step 2: Instantiate the OCR engine and set the language.
var ocrEngine = new OcrEngine
{
    // English works for most scanned docs; you can pick other languages here.
    Language = OcrLanguage.English
};
```

**Pourquoi c’est important :**  
`OcrEngine` est le cœur de **Aspose OCR GPU**. Définir `Language` indique au modèle neuronal sous‑jacent quel jeu de caractères attendre, améliorant ainsi considérablement la précision. Vous pouvez également ajuster `Resolution`, `PreprocessOptions` ou `RecognitionMode` pour des documents plus difficiles.

## Étape 3 : Charger l’image pour l’OCR

```csharp
// Step 3: Load a large TIFF image from disk.
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/large_doc.tif");
```

**Pourquoi c’est important :**  
Un TIFF peut contenir plusieurs pages, une haute résolution et une compression sans perte — parfait pour les numérisations d’archives mais lourd en mémoire. `ImageStream.FromFile` diffuse le fichier, évitant un chargement complet en mémoire pour les images très volumineuses.

**Cas limite :** Si vous devez traiter un TIFF multi‑pages, appelez `ocrEngine.Image = ImageStream.FromFile(path, pageIndex);` dans une boucle, en incrémentant `pageIndex` jusqu’à ce que `ocrEngine.Image.IsNull` renvoie `true`.

## Étape 4 : Effectuer la reconnaissance

```csharp
// Step 4: Run the OCR process.
ocrEngine.Recognize();
```

**Pourquoi c’est important :**  
`Recognize()` effectue tout le travail lourd : pré‑traitement, analyse de mise en page, segmentation des caractères, et enfin l’inférence du réseau neuronal. Lorsque le GPU est actif, l’étape d’inférence s’exécute sur le GPU, réduisant souvent de 50‑80 % le temps de traitement pour les gros TIFF.

## Étape 5 : Produire les résultats

```csharp
// Step 5: Show how many characters were extracted and how long it took.
Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");

// Optional: print the extracted text (be careful with huge strings!)
Console.WriteLine("--- Extracted Text Start ---");
Console.WriteLine(ocrEngine.Text);
Console.WriteLine("--- Extracted Text End ---");
```

**Pourquoi c’est important :**  
`ocrEngine.Text` contient la chaîne entièrement concaténée provenant de l’image, tandis que `ProcessingTime` vous fournit un benchmark rapide pour comparer les exécutions CPU vs. GPU. La sortie console est pratique pour un débogage rapide ; en production, vous écririez probablement le texte dans une base de données ou un fichier.

**Sortie attendue (exemple pour une facture de 2 pages) :**

```
Recognized 1342 characters in 842 ms
--- Extracted Text Start ---
Invoice #12345
Date: 2026‑04‑30
...
Total: $1,234.56
--- Extracted Text End ---
```

Si le GPU n’est pas disponible, le temps peut grimper à ~1800 ms sur le même matériel, démontrant clairement le bénéfice de **aspose ocr gpu**.

---

## Gestion des problèmes courants

| Situation | À surveiller | Comment corriger |
|-----------|--------------|------------------|
| **GPU non détecté** | `EnableGpu(true)` repasse silencieusement, mais vous pourriez penser qu’il utilise toujours le GPU. | Vérifiez `OcrEngine.IsGpuEnabled` après l’appel ; consignez le résultat. |
| **Mémoire insuffisante sur un TIFF énorme** | Charger une image de 10 000 × 10 000 pixels peut dépasser la RAM. | Utilisez `ImageStream.FromFile(path, pageIndex, maxResolution: 300)` pour réduire la résolution lors du chargement. |
| **Langue incorrecte** | Le modèle anglais sur un document français produit une sortie illisible. | Définissez `Language = OcrLanguage.French` ou activez le mode multilingue. |
| **TIFF multi‑pages** | Seule la première page est traitée. | Parcourez les pages avec `ImageStream.FromFile(path, pageNumber)`. |

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez placer dans une application console. Il inclut la gestion des erreurs, le journal du statut GPU, et un minuteur simple pour vos propres benchmarks.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // adds GPU support

namespace AsposeOcrGpuDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Enable GPU acceleration (if available)
            OcrEngine.EnableGpu(true);
            Console.WriteLine($"GPU enabled: {OcrEngine.IsGpuEnabled}");

            // 2️⃣ Create the OCR engine and set language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English
            };

            // 3️⃣ Load the TIFF image (replace with your actual path)
            string imagePath = @"YOUR_DIRECTORY\large_doc.tif";
            try
            {
                ocrEngine.Image = ImageStream.FromFile(imagePath);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Failed to load image: {ex.Message}");
                return;
            }

            // 4️⃣ Perform recognition
            try
            {
                ocrEngine.Recognize();
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Recognition error: {ex.Message}");
                return;
            }

            // 5️⃣ Output results
            Console.WriteLine($"Recognized {ocrEngine.Text.Length} characters in {ocrEngine.ProcessingTime} ms");
            Console.WriteLine("--- Extracted Text Start ---");
            Console.WriteLine(ocrEngine.Text);
            Console.WriteLine("--- Extracted Text End ---");
        }
    }
}
```

Copiez, collez, appuyez sur **F5**, et observez la console afficher le nombre de caractères et le texte extrait. Remplacez `OcrLanguage.English` par toute autre langue prise en charge par Aspose si vous devez **reconnaître une image texte** en espagnol, allemand, etc.

## Récapitulatif & prochaines étapes

Nous venons de voir comment **aspose ocr gpu** pour **reconnaître une image texte** à partir d’une **image OCR TIFF**, comment **charger une image pour l’OCR**, et comment **extraire du texte d’un TIFF** efficacement. Les idées principales — activer le GPU, configurer la langue, diffuser le TIFF, et lire le résultat — sont applicables à d’autres formats comme JPEG ou PNG.

### Que tester ensuite

- **Traitement par lots** : Parcourez un dossier de TIFF, écrivez chaque `ocrEngine.Text` dans un fichier `.txt`.  
- **Gestion multi‑pages** : Utilisez `ImageStream.FromFile(path, pageIndex)` dans une boucle `while` pour traiter chaque page d’un document multi‑pages.  
- **Pré‑traitement personnalisé** : Ajustez `ocrEngine.PreprocessOptions` (par ex., `Denoise`, `Deskew`) pour les numérisations bruitées.  
- **Benchmark GPU** : Enregistrez `ProcessingTime` avec et sans `EnableGpu(true)` sur la même machine pour quantifier le gain de vitesse.  

N’hésitez pas à expérimenter — l’accélération GPU brille surtout sur les TIFF haute résolution et multi‑pages, mais même un 1080 Ti modeste réduira considérablement le temps de reconnaissance.

Vous avez des questions sur un type de document spécifique ou besoin d’aide pour intégrer la sortie dans une base de données ? Laissez un commentaire ci‑dessous, et bon codage !

## Tutoriels associés

- [Extraire du texte d’une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)
- [Comment extraire du texte d’une image en préparant des rectangles dans l’OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extraire du texte d’une image – Reconnaître la ligne avec Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}