---
category: general
date: 2025-12-29
description: Créer un PDF consultable à partir d'images numérisées en utilisant le
  traitement par lots d'Aspose OCR. Apprenez à convertir des images en PDF, à prétraiter
  les images pour l'OCR et à redresser les documents numérisés.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- convert images to pdf
- preprocess images for ocr
- deskew scanned documents
language: fr
og_description: Créer un PDF consultable à partir d'images numérisées en utilisant
  le traitement par lots d'Aspose OCR. Apprenez à convertir des images en PDF, à prétraiter
  les images pour l'OCR et à redresser les documents numérisés.
og_title: Créer un PDF consultable avec OCR par lots – Guide C#
tags:
- OCR
- C#
- PDF/A
- Aspose
title: Créer un PDF consultable avec OCR par lots – Guide C#
url: /fr/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un PDF consultable avec OCR par lots – Guide C#

Vous avez déjà eu besoin de **créer des fichiers PDF consultables** à partir d’une montagne d’images numérisées mais vous êtes bloqué dès la première étape ? Vous n’êtes pas seul — la plupart des développeurs rencontrent le même mur lorsqu’ils traitent des scans désordonnés, des pages irrégulières ou simplement une conversion massive.  

La bonne nouvelle ? Avec Aspose OCR, vous pouvez mettre en place un pipeline **de traitement OCR par lots** qui non seulement **convertit les images en PDF** mais aussi **prétraite les images pour l’OCR** et même **redresse automatiquement les documents numérisés**. Dans ce tutoriel, nous parcourrons l’ensemble du processus, de la configuration du moteur à la finition du résultat, afin que vous puissiez l’exécuter sur un dossier de fichiers et obtenir des PDF/A‑2b consultables.

> **Ce que vous obtiendrez :** une application console C# unique et exécutable qui prend un répertoire d’images (ou de PDF), nettoie chaque page, exécute l’OCR et génère un fichier PDF/A‑2b consultable à côté de la source. Pas de fragments de code épars, juste une solution cohérente.

---

## Prérequis

- SDK .NET 6 ou version ultérieure (le code compile également avec .NET Core).  
- Un package NuGet Aspose OCR (`Aspose.OCR`).  
- Un dossier d’images numérisées (TIFF, JPEG, PNG) ou de PDF que vous souhaitez transformer en PDF consultables.  
- (Facultatif) Une vraie clé de licence — sinon le mode d’essai ajoutera un filigrane, mais cela fonctionne pour les tests.

Si vous avez tout cela, plongeons‑y.

---

## Vue d’ensemble – Comment le pipeline complet crée un PDF consultable

1. **Activer le mode d’essai** (ou charger votre licence).  
2. **Configurer `OcrBatchProcessor`** – indiquez où lire les fichiers, où écrire les PDF, quel format utiliser et combien de threads exécuter en parallèle.  
3. **Pré‑traiter chaque image** – redresser, débruiter et supprimer les arrière‑plans afin que le moteur OCR voie une page propre.  
4. **Exécuter le lot** – Aspose traite chaque fichier, lance l’OCR et écrit un PDF/A‑2b consultable.  
5. **Notifier la fin** – un simple message console, mais vous pourriez brancher un logger ou un webhook.

C’est le flux de haut niveau. Le code ci‑dessous implémente chaque étape avec de nombreux commentaires, afin que vous puissiez ajuster n’importe quelle partie sans casser l’ensemble.

---

## Étape 1 – Activer le mode d’essai (ou charger votre licence)

Avant de pouvoir appeler une classe Aspose, vous devez informer la bibliothèque que vous êtes licencié. Pour des expériences rapides, le mode d’essai suffit.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

// Activate trial mode – replace with OcrEngine.SetLicense("YourLicenseFile.lic") for production
OcrEngine.EnableTrialMode();
```

> **Astuce pro :** placez l’activation de la licence tout en haut de `Program.cs`. Si vous l’oubliez, le moteur lèvera une exception dès le premier appel à `Process()`.

---

## Étape 2 – Configurer le moteur de traitement OCR par lots

Voici où nous configurons l’objet **de traitement OCR par lots**. Notez que `InputFolder` et `OutputFolder` sont identiques dans cet exemple, mais vous pouvez les séparer si vous le souhaitez.

```csharp
// Define where your source images live and where the searchable PDFs should be saved
var ocrBatch = new OcrBatchProcessor
{
    // Folder that contains the images or PDFs to be processed
    InputFolder = @"C:\Scans\Incoming",

    // Folder where searchable PDF/A‑2b files will be saved
    OutputFolder = @"C:\Scans\Processed",

    // Choose the output format – searchable PDF/A‑2b (perfect for archiving)
    OutputFormat = SaveFormat.SearchablePdf,

    // Limit the number of concurrent OCR operations to avoid CPU spikes
    MaxDegreeOfParallelism = 3,

    // Pre‑process each image: deskew, denoise, and remove background
    Preprocess = img => ImageFilters
                            .Deskew(img)          // fixes rotated pages
                            .Denoise()            // reduces speckles
                            .RemoveBackground()   // clears colored backgrounds
};
```

### Pourquoi ces paramètres sont importants

- **`MaxDegreeOfParallelism`** : lancer trop de threads OCR peut saturer votre CPU, surtout sur une station de travail modeste. Trois threads constituent un bon compromis pour la plupart des ordinateurs portables quad‑core.  
- **Pipeline `Preprocess`** : les trois filtres combinés améliorent considérablement la précision de l’OCR. Le redressement corrige le problème fréquent de « scan incliné », le débruitage élimine le bruit aléatoire, et la suppression de l’arrière‑plan garantit que le moteur ne voit que du texte noir sur fond blanc.  
- **`SaveFormat.SearchablePdf`** : cela crée des fichiers PDF/A‑2b à la fois archivables et consultables—une exigence pour de nombreuses normes de conformité.

---

## Étape 3 – Exécuter le lot et voir la magie opérer

Lancer le lot est aussi simple que d’appeler `Process()`. La méthode bloque jusqu’à ce que chaque fichier soit traité, puis retourne. Si vous avez besoin d’un suivi de progression, vous pouvez brancher l’événement `ProgressChanged` (non montré ici).

```csharp
// Start processing – this will walk through every file in InputFolder
ocrBatch.Process();

// Let the user (or calling script) know we’re finished
Console.WriteLine("All files processed. Searchable PDFs are ready.");
```

Lorsque la console affiche la ligne finale, vous trouverez un PDF consultable pour chaque image d’entrée dans `C:\Scans\Processed`. Ouvrez‑en un dans Adobe Reader, appuyez sur **Ctrl+F**, et vous pourrez rechercher le texte qui vient d’être extrait du scan.

---

## Étape 4 – Programme complet exécutable (prêt à copier‑coller)

Ci‑dessous se trouve le programme **complet et autonome** que vous pouvez placer dans un nouveau projet console (`dotnet new console`). Assurez‑vous d’avoir ajouté le package NuGet Aspose.OCR au préalable (`dotnet add package Aspose.OCR`).

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

namespace CreateSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Activate trial mode (replace with real license for production)
            OcrEngine.EnableTrialMode();

            // 2️⃣ Configure batch OCR processing
            var ocrBatch = new OcrBatchProcessor
            {
                InputFolder = @"C:\Scans\Incoming",   // 👉 change to your source folder
                OutputFolder = @"C:\Scans\Processed", // 👉 change to your target folder
                OutputFormat = SaveFormat.SearchablePdf,
                MaxDegreeOfParallelism = 3,
                Preprocess = img => ImageFilters
                                        .Deskew(img)          // fixes rotated pages
                                        .Denoise()            // cleans up noise
                                        .RemoveBackground()   // strips colored backgrounds
            };

            // 3️⃣ Run the batch
            ocrBatch.Process();

            // 4️⃣ Notify completion
            Console.WriteLine("All files processed. Searchable PDFs are ready.");
        }
    }
}
```

### Sortie attendue

```
All files processed. Searchable PDFs are ready.
```

Après l’exécution, en vous rendant dans `C:\Scans\Processed` vous verrez un ensemble de fichiers `.pdf` — chacun consultable, chacun conforme à PDF/A‑2b. Ouvrez n’importe quel fichier, tapez un mot que vous savez présent dans le scan original, et voilà, le texte est mis en évidence.

---

## Questions fréquentes & gestion des cas particuliers

### Et si mon dossier source contient déjà des PDF ?

Aspose OCR peut ingérer les PDF directement ; il rasterisera chaque page, appliquera les mêmes filtres **de prétraitement**, et intégrera la couche OCR. Aucun code supplémentaire n’est nécessaire.

### Comment changer le format de sortie en PDF simple (non consultable) ?

Remplacez `SaveFormat.SearchablePdf` par `SaveFormat.Pdf`. Vous perdrez la couche de texte consultable, mais la fidélité visuelle restera identique.

### Mes scans sont en couleur—la suppression de l’arrière‑plan affecte‑t‑elle cela ?

`RemoveBackground()` cible les arrière‑plans non blancs tout en préservant le texte principal. Si vous devez conserver des graphiques en couleur, vous pouvez omettre ce filtre :

```csharp
.Preprocess = img => ImageFilters.Deskew(img).Denoise()
```

### Je tourne sur un serveur avec peu de RAM—puis‑je réduire le nombre de threads ?

Absolument. Réglez `MaxDegreeOfParallelism` à `1` ou `2`. Le lot prendra plus de temps, mais la consommation de mémoire restera faible.

---

## Résumé visuel (optionnel)

Si vous aimez un diagramme rapide, imaginez ce flux :

![Create searchable pdf workflow – shows input folder → preprocessing → OCR → searchable PDF output](/images/ocr-workflow.png)

*Texte alternatif :* **Diagramme du flux de création de PDF consultable** – illustre le traitement OCR par lots, la conversion et les étapes de redressement.

---

## Conclusion

Vous disposez maintenant d’une solution **complète et prête pour la production** afin de **créer des fichiers PDF consultables** à partir de n’importe quel lot d’images numérisées. En tirant parti du **traitement OCR par lots**, vous pouvez **convertir des images en PDF**, **prétraiter les images pour l’OCR**, et **redresser automatiquement les documents numérisés**—le tout avec quelques lignes de C#.

Prochaines étapes ? Essayez d’ajouter un schéma de nommage personnalisé, intégrez un framework de journalisation pour capturer les scores de confiance de l’OCR, ou expérimentez d’autres `ImageFilters` comme `Sharpen()` pour du texte pâle. L’API Aspose OCR est suffisamment flexible pour évoluer avec vos besoins.

Bon codage, et que vos PDF restent toujours consultables !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}