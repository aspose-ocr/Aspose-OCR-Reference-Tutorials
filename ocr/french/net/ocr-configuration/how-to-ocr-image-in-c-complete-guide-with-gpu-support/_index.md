---
category: general
date: 2026-01-09
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) sur
  une image et à extraire le texte de l'image avec Aspose.OCR. Comprend les étapes
  pour convertir un document numérisé, activer le GPU et lire l'image avec l'OCR.
draft: false
keywords:
- how to ocr image
- extract image text
- convert scanned document
- how to enable gpu
- read image with ocr
language: fr
og_description: Comment effectuer rapidement la reconnaissance OCR d’une image avec
  Aspose.OCR. Suivez ce tutoriel étape par étape pour extraire le texte d’une image,
  convertir un document numérisé et activer le GPU.
og_title: Comment faire de l'OCR d'image en C# – Guide accéléré par GPU
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Comment faire de l’OCR d’image en C# – Guide complet avec prise en charge du
  GPU
url: /fr/net/ocr-configuration/how-to-ocr-image-in-c-complete-guide-with-gpu-support/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire de l'OCR d'image en C# – Guide complet avec prise en charge GPU

Vous vous êtes déjà demandé **comment faire de l'OCR d'image** directement depuis votre application .NET ? Vous n'êtes pas le seul—les développeurs ont constamment besoin d'extraire du texte à partir de PDFs, TIFF et photos, surtout lorsqu'ils traitent de gros documents numérisés. Bonne nouvelle ? Avec Aspose.OCR vous pouvez **extraire le texte d'une image** en quelques lignes seulement, et vous pouvez même **activer l'accélération GPU** pour un traitement plus rapide.

Dans ce tutoriel, nous passerons en revue tout ce que vous devez savoir : de l'installation de la bibliothèque, à l'initialisation du moteur OCR avec repli GPU, jusqu'à **lire l'image avec OCR** et afficher le résultat. À la fin, vous serez capable de **convertir des images de documents numérisés** en chaînes éditables—sans services externes requis.

---

## Ce dont vous aurez besoin

- **.NET 6.0** ou version ultérieure (le code fonctionne également sur .NET Core et .NET Framework).
- Une **licence** pour Aspose.OCR ou une clé d'évaluation temporaire (l'essai gratuit fonctionne pour les tests).
- Un fichier image que vous souhaitez traiter—de préférence un TIFF ou PNG haute résolution.
- (Optionnel) Une machine avec GPU activé si vous voulez voir le gain de vitesse ; sinon le moteur reviendra gracieusement au CPU.

Avoir ces prérequis couverts signifie que vous pouvez vous concentrer sur le flux de travail OCR réel sans rencontrer d'obstacle plus tard.

---

## Étape 1 : Installer le package NuGet Aspose.OCR

Tout d'abord, ajoutez la bibliothèque Aspose.OCR à votre projet. Ouvrez un terminal dans le dossier de votre solution et exécutez :

```bash
dotnet add package Aspose.OCR
```

Ou, si vous utilisez l'interface NuGet de Visual Studio, recherchez simplement **Aspose.OCR** et cliquez sur installer. Cette commande unique récupère toutes les DLL nécessaires, y compris les binaires GPU natifs lorsqu'ils sont disponibles.

> **Astuce :** Gardez le package à jour. Les nouvelles versions incluent souvent des améliorations des modèles de langue et un meilleur support GPU.

---

## Étape 2 : Importer les espaces de noms requis  

Maintenant que le package est installé, importez les espaces de noms pertinents. Cette étape est où nous commençons **comment faire de l'OCR d'image** dans le code.

```csharp
// Step 2: Import required namespaces
using Aspose.OCR;
using Aspose.OCR.Settings;
```

Ces deux lignes vous donnent accès à la classe `OcrEngine` et à l'objet de paramètres qui vous permet d'activer ou désactiver l'utilisation du GPU. Sans elles, le compilateur ne saurait pas ce que signifie `OcrEngine`.

---

## Étape 3 : Initialiser le moteur OCR et activer le GPU  

Si vous vous êtes déjà demandé **comment activer le GPU** pour l'OCR, voici la réponse. Nous créons une instance `OcrEngineSettings`, activons le drapeau `UseGpu`, et la transmettons au constructeur du moteur. Le moteur détecte automatiquement si un GPU compatible est présent ; sinon, il revient au CPU—vous n'avez donc pas besoin de gestion d'erreur supplémentaire.

```csharp
// Step 3: Initialize the OCR engine with GPU support (falls back to CPU if unavailable)
var ocrSettings = new OcrEngineSettings { UseGpu = true };
var ocrEngine   = new OcrEngine(ocrSettings);
```

Pourquoi activer le GPU du tout ? Pour les grandes images—pensez aux TIFF multi‑pages ou aux scans haute résolution—le temps de traitement peut passer de plusieurs secondes à une fraction de seconde. Si vous construisez un pipeline de traitement par lots, ce gain de vitesse s'accumule rapidement.

---

## Étape 4 : Effectuer l'OCR sur votre image cible  

C'est ici que nous **lisons réellement l'image avec OCR**. Fournissez le chemin de votre fichier, et le moteur renvoie le texte reconnu sous forme de chaîne. Cela fonctionne pour tout format raster pris en charge par Aspose (PNG, JPEG, TIFF, BMP, etc.).

```csharp
// Step 4: Perform OCR on the target image file
string imagePath = @"C:\Images\large-document.tif";
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

Si vous devez **convertir des documents numérisés** page par page, bouclez simplement sur les noms de fichiers et appelez `RecognizeImage` pour chacun. La méthode est thread‑safe, vous pouvez donc même paralléliser la charge de travail sur un CPU multi‑cœur.

---

## Étape 5 : Afficher ou persister le texte extrait  

Enfin, nous affichons le résultat. Dans une application console, `Console.WriteLine` fait l'affaire. Dans un scénario réel, vous pourriez écrire le texte dans une base de données, un fichier JSON, ou le transmettre à un index de recherche.

```csharp
// Step 5: Display the extracted text
Console.WriteLine(recognizedText);
```

La ligne ci‑dessus imprime la sortie OCR brute. Vous remarquerez des sauts de ligne, des erreurs de reconnaissance occasionnelles, et peut‑être quelques caractères errants—rien d'inhabituel pour l'OCR. Un post‑traitement (par ex., nettoyage avec regex) peut remettre de l'ordre si nécessaire.

> **Note :** Aspose.OCR prend également en charge les dictionnaires spécifiques à chaque langue. Si vous traitez des textes non anglais, définissez `ocrEngine.Settings.Language` en conséquence avant d'appeler `RecognizeImage`.

---

## Exemple complet fonctionnel  

En rassemblant le tout, voici un programme autonome que vous pouvez copier‑coller dans un nouveau projet console :

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with GPU support
        var ocrSettings = new OcrEngineSettings { UseGpu = true };
        var ocrEngine   = new OcrEngine(ocrSettings);

        // Path to the image you want to process
        string imagePath = @"C:\Images\large-document.tif";

        // Perform OCR
        string recognizedText = ocrEngine.RecognizeImage(imagePath);

        // Output the result
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(recognizedText);
    }
}
```

**Sortie attendue** (troncature pour la brièveté) :

```
=== OCR Result ===
This is a sample scanned document.
It contains several lines of text that have been
converted from image to editable characters.
...
```

Exécutez le programme, et vous devriez voir le texte extrait apparaître dans votre fenêtre console. Si le GPU est disponible, le temps de traitement sera nettement plus court que sur des machines uniquement CPU.

---

## Pièges courants & comment les éviter  

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Garbage characters** | Source à basse résolution ou fond bruité. | Pré‑traitez l'image (augmentez le DPI, appliquez une binarisation) avant l'OCR. |
| **GPU not used** | Aucun pilote CUDA compatible installé. | Vérifiez la version du pilote, ou définissez `UseGpu = false` pour forcer le CPU. |
| **Out‑of‑memory on large TIFFs** | Chargement du fichier complet en une fois. | Utilisez `OcrEngineSettings.MaxMemoryUsage` pour limiter l'empreinte, ou traitez les pages individuellement. |
| **Incorrect language detection** | La langue par défaut est l'anglais. | Définissez `ocrEngine.Settings.Language = Language.YourLanguage;` avant d'appeler `RecognizeImage`. |

Traiter ces cas limites garantit que votre implémentation **comment faire de l'OCR d'image** reste robuste sur différents environnements.

---

## Étendre la solution  

Maintenant que vous pouvez **extraire le texte d'une image**, vous pourriez vouloir :

- **Convertir des documents numérisés** PDFs en PDFs recherchables en intégrant la couche OCR.
- Stocker les résultats dans un index **Azure Cognitive Search** pour une récupération rapide.
- Chaîner la sortie OCR à une **API de traduction** si vous avez besoin d'un support multilingue.
- Utiliser la méthode `GetBoundingBoxes` d'**Aspose.OCR** pour localiser où chaque mot apparaît sur l'image—pratique pour les outils de rédaction.

Toutes ces extensions reposent sur le même principe de base que nous avons couvert : initialiser le moteur, lui fournir une image, et lire le texte.

---

## Conclusion  

Nous avons parcouru un exemple complet, de bout en bout, de **comment faire de l'OCR d'image** avec Aspose.OCR en C#. En installant le package NuGet, en important les bons espaces de noms, en activant le GPU (ou en revenant au CPU), et en appelant `RecognizeImage`, vous pouvez de manière fiable **extraire le texte d'une image**, **convertir des pages de documents numérisés**, et **lire l'image avec OCR** dans n'importe quelle application .NET.

Essayez-le sur quelques-unes de vos propres numérisations—expérimentez différents formats d'image, activez ou désactivez le drapeau GPU, et observez comment les performances changent. Lorsque vous serez prêt, explorez les fonctionnalités avancées comme les dictionnaires de langues ou l'extraction de boîtes englobantes pour rendre votre solution encore plus intelligente.

Bon codage, et que vos pipelines OCR soient rapides, précis et sans tracas !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}