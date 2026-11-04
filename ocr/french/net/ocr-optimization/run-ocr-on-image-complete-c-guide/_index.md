---
category: general
date: 2026-05-28
description: Exécutez l'OCR sur une image en utilisant C# pour lire le texte de l'image
  et extraire rapidement le texte d’un reçu. Découvrez les options GPU et les techniques
  de chargement.
draft: false
keywords:
- run ocr on image
- read text from image
- extract text from receipt
- load image for ocr
language: fr
og_description: Exécutez l'OCR sur une image avec C#. Ce tutoriel vous montre comment
  lire du texte à partir d’une image, extraire le texte d’un reçu et optimiser l’utilisation
  du GPU.
og_title: Exécuter l'OCR sur une image – Guide complet C#
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  headline: Run OCR on Image – Complete C# Guide
  type: TechArticle
- description: Run OCR on image using C# to read text from image and extract text
    from receipt fast. Learn GPU options and loading techniques.
  name: Run OCR on Image – Complete C# Guide
  steps:
  - name: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
    text: '**Batch processing:** Re‑use a single `OcrEngine` instance for a batch
      of images; it caches language models and reduces latency.'
  - name: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
    text: '**Pre‑filtering:** Apply a simple grayscale conversion and contrast boost
      before handing the image to the engine—many libraries expose a `Preprocess`
      method.'
  - name: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
    text: '**Error logging:** Capture `ocrEngine.LastError` (if available) after each
      `Recognize()` call to diagnose failures without crashing your service.'
  - name: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
    text: '**Thread safety:** Most OCR engines are **not** thread‑safe. If you need
      parallelism, create a separate engine per thread or use a concurrency queue.'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
- Computer Vision
title: Exécuter l'OCR sur une image – Guide complet C#
url: /fr/net/ocr-optimization/run-ocr-on-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécuter l'OCR sur une image – Guide complet C#

Vous avez déjà eu besoin de **exécuter l'OCR sur une image** mais vous ne saviez pas par où commencer ? Vous n'êtes pas seul ; de nombreux développeurs rencontrent ce mur lorsqu'ils essaient pour la première fois de lire du texte à partir de données d'image. La bonne nouvelle, c’est qu’avec quelques lignes de C# vous pouvez extraire du texte de scans de reçus, de PDF ou de n’importe quelle photo que vous leur lancez. Dans ce guide, nous parcourrons un exemple complet, prêt à l’emploi, qui montre également comment **load image for OCR**, exploiter l’accélération GPU et limiter la consommation de mémoire en toute sécurité.

À la fin de ce tutoriel, vous serez capable de :

* Initialiser un moteur OCR en C#
* **Load image for OCR** depuis le disque ou un flux
* **Read text from image** avec prise en charge optionnelle du GPU
* **Extract text from receipt** et afficher le résultat dans la console

Aucun service externe requis — seulement une bibliothèque locale et une image de reçu d’exemple.

---

## Ce dont vous avez besoin

| Prérequis | Raison |
|--------------|--------|
| .NET 6.0 SDK ou version ultérieure | Runtime moderne, prend en charge les dernières fonctionnalités du langage |
| Une bibliothèque OCR exposant une classe `OcrEngine` (par ex., IronOCR, wrapper .NET de Tesseract) | Fournit les méthodes `Configuration` et `Recognize` utilisées ci‑dessous |
| Un GPU compatible CUDA (optionnel) | Active le drapeau `EnableGpu` pour un traitement plus rapide |
| Une image de reçu d’exemple (`receipt.jpg`) | Illustre l’étape **extract text from receipt** |
| Tout IDE C# (Visual Studio, Rider, VS Code) | Pour une compilation et un débogage rapides |

Si vous n’avez pas de GPU, le code reviendra simplement en mode CPU — pas de souci.

---

![Exemple de sortie d'OCR sur image](https://example.com/ocr-output.png "Exécution de l'OCR sur une image – exemple de sortie console")

*Texte alternatif : Exemple de sortie d'OCR sur image montrant le texte du reçu reconnu.*

---

## Étape 1 : Exécuter l'OCR sur une image – Configuration du moteur

Tout d’abord, créez une instance du moteur OCR. Cet objet est le cœur du processus ; il conserve tous les paramètres de configuration et effectue le travail lourd.

```csharp
using System;
using OcrLibrary;   // Replace with the actual namespace of your OCR package

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

*Pourquoi c’est important :* La classe `OcrEngine` encapsule le moteur OCR natif (Tesseract, IronOCR, etc.). L’instancier une seule fois et le réutiliser pour plusieurs images réduit la surcharge et vous offre un point unique où ajuster les paramètres.

---

## Étape 2 : Load Image for OCR

Avant que le moteur puisse lire quoi que ce soit, vous devez lui fournir une image. La propriété `Image` de la bibliothèque attend un flux ou un chemin de fichier, selon l’implémentation.

```csharp
// Step 2: Load the image to be processed
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/receipt.jpg");
```

*Astuce :* Si vous gérez des téléchargements d’utilisateurs, encapsulez cela dans un `try/catch` et validez d’abord le type de fichier. Les formats non pris en charge lanceront une exception qui pourra être gérée proprement.

---

## Étape 3 : Enable GPU Acceleration (Optional)

Si votre machine possède un runtime CUDA ou OpenCL compatible, activer le mode GPU peut faire gagner quelques secondes à chaque passe de reconnaissance.

```csharp
// Step 3: Enable GPU acceleration (requires CUDA/OpenCL runtime)
ocrEngine.Configuration.EnableGpu = true;
```

*Conseil de pro :* Tous les GPU ne sont pas créés égaux. Sur les cartes plus anciennes, vous pourriez observer un léger ralentissement dû à la surcharge du pilote. Testez les deux chemins (`EnableGpu = true/false`) pour voir ce qui fonctionne le mieux avec votre matériel.

---

## Étape 4 : Limit GPU Memory Usage (Optional)

Parfois, vous ne voulez pas que le processus OCR engloutisse toute la mémoire GPU, surtout si vous partagez le GPU avec d’autres charges de travail comme l’inférence deep‑learning.

```csharp
// Step 4: (Optional) Limit the amount of GPU memory the engine can use (in MB)
ocrEngine.Configuration.GpuMemoryLimit = 1024; // 1 GB limit
```

*Quand l’utiliser :* Si vous exécutez un service web qui traite de nombreuses images en parallèle, plafonner la mémoire évite les plantages « out‑of‑memory ».

---

## Étape 5 : Recognize Text and Read Text from Image

Le moteur est maintenant prêt à faire son travail. L’appel à `Recognize()` lance le pipeline OCR et renvoie la chaîne extraite.

```csharp
// Step 5: Perform OCR and retrieve the recognized text
string recognizedText = ocrEngine.Recognize();
```

*Pourquoi c’est le cœur du processus :* Cette ligne unique masque une cascade de prétraitements (binarisation, redressement) et la classification réelle des caractères. Le `recognizedText` retourné est du texte Unicode brut, prêt pour un traitement ultérieur.

---

## Étape 6 : Extract Text from Receipt – Output

Enfin, écrivez le résultat dans la console ou stockez‑le où vous le souhaitez. Pour un reçu, vous pourrez plus tard analyser les lignes d’articles, les totaux ou les dates.

```csharp
// Step 6: Output the result
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(recognizedText);
```

**Sortie console attendue (troncature pour la brièveté) :**

```
=== OCR Result ===
Store Name
123 Main St.
Date: 04/27/2026
Item   Qty   Price
Apple   2    1.20
Bread   1    2.50
Total          3.70
Thank you!
```

Si l’OCR a du mal avec une mise en page de reçu particulière, envisagez d’ajuster les options de prétraitement (par ex., `ocrEngine.Configuration.Deskew = true`) ou d’utiliser une image de résolution supérieure.

---

## Cas limites courants & comment les gérer

| Situation | Solution proposée |
|-----------|-------------------|
| **Image nulle** – `ocrEngine.Image` est `null` | Validez le chemin du fichier avant l’affectation ; lancez une `ArgumentException` claire si manquant. |
| **GPU non disponible** – `EnableGpu = true` lève `PlatformNotSupportedException` | Enveloppez l’appel d’activation du GPU dans un `try/catch` et revenez en mode CPU. |
| **Grands reçus (> 10 Mo)** provoquant une pression mémoire | Utilisez `GpuMemoryLimit` ou traitez l’image en tuiles (`ocrEngine.Configuration.TileSize`). |
| **Détection de langue incorrecte** – la sortie contient du charabia | Définissez `ocrEngine.Configuration.Language = "eng"` (ou le code ISO approprié) pour forcer l’anglais. |

---

## Conseils de pro pour un OCR prêt pour la production

1. **Traitement par lots :** Réutilisez une seule instance `OcrEngine` pour un lot d’images ; elle met en cache les modèles linguistiques et réduit la latence.  
2. **Pré‑filtrage :** Appliquez une conversion simple en niveaux de gris et un renforcement du contraste avant de transmettre l’image au moteur — de nombreuses bibliothèques exposent une méthode `Preprocess`.  
3. **Journalisation des erreurs :** Capturez `ocrEngine.LastError` (si disponible) après chaque appel à `Recognize()` pour diagnostiquer les échecs sans faire planter votre service.  
4. **Sécurité des threads :** La plupart des moteurs OCR **ne sont pas** thread‑safe. Si vous avez besoin de parallélisme, créez un moteur distinct par thread ou utilisez une file d’attente de concurrence.  

---

## Conclusion

Nous venons de parcourir un flux complet **run OCR on image** en C#. En partant de la création du moteur, **loading image for OCR**, en activant l’accélération GPU, puis en **extracting text from receipt**, vous disposez maintenant d’une base solide pour construire des pipelines de traitement de documents plus sophistiqués.

Les prochaines étapes pourraient inclure :

* Analyser le texte du reçu en JSON structuré (avec des expressions régulières ou une bibliothèque de traitement du langage naturel) – idéal pour l’automatisation **read text from image**.  
* Intégrer l’étape OCR dans une API ASP .NET Core afin que les utilisateurs puissent télécharger des reçus via HTTP.  
* Expérimenter avec différents back‑ends OCR (Tesseract vs. SDK commerciaux) pour comparer la précision.

Essayez avec plusieurs mises en page de reçus, ajustez la configuration, et vous verrez à quel point il est rapide de transformer une photo floue en données exploitables. Bon codage, et que vos images soient toujours nettes !

## Tutoriels associés

- [Extraire le texte d’une image C# avec sélection de langue en utilisant Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extraire le texte d’une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)
- [Comment extraire le texte d’une image en préparant des rectangles dans l’OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}