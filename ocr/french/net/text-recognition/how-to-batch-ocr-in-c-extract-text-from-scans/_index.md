---
category: general
date: 2026-05-06
description: Apprenez à réaliser la reconnaissance optique de caractères (OCR) en
  lot avec C# et à extraire rapidement le texte des numérisations en utilisant Aspose
  OCR Batch. Suivez un guide complet étape par étape avec du code, des astuces et
  la gestion des cas limites.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: fr
og_description: Comment faire de l'OCR par lots en C# ? Ce guide vous montre comment
  extraire du texte à partir de numérisations efficacement avec Aspose OCR, le support
  GPU et le traitement parallèle.
og_title: Comment réaliser une OCR par lots en C# – Extraire le texte des numérisations
tags:
- C#
- OCR
- Aspose
title: Comment réaliser une OCR par lots en C# – Extraire le texte des numérisations
url: /fr/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment faire du OCR par lots en C# – Extraire du texte à partir de numérisations

Vous vous êtes déjà demandé **comment faire du OCR par lots** lorsque vous avez un dossier rempli de PDF ou JPEG numérisés ? Vous n'êtes pas le seul à regarder une montagne d'images et à penser « Il doit exister un moyen plus rapide d'extraire le texte ». Dans ce tutoriel, nous allons parcourir une solution pratique qui non seulement vous permet **d'extraire du texte à partir de numérisations**, mais accélère également le processus grâce à l'accélération GPU et au parallélisme.

Voici le problème : faire du OCR fichier par fichier prend énormément de temps, surtout si vous traitez des dizaines ou des centaines de pages. À la fin de ce guide, vous disposerez d'une application console C# prête à l'emploi qui traite un répertoire entier en une seule commande, vous fournissant des fichiers texte propres prêts à être indexés, recherchés, ou tout autre usage.

## Prérequis

- **.NET 6.0 ou version ultérieure** (le code utilise les fonctionnalités modernes de C#).
- Une **licence pour Aspose.OCR** (l'essai gratuit fonctionne pour les tests).
- Une machine compatible GPU **si vous souhaitez activer `UseGpu`** ; sinon la bibliothèque reviendra au CPU.
- Une connaissance de base des **applications console C#**.

Pas de services externes, pas de fichiers de configuration cachés — seulement le SDK et un dossier d'images.

## Étape 1 : Installer le package NuGet Aspose.OCR

Tout d'abord, ajoutez la bibliothèque Aspose OCR à votre projet. Ouvrez un terminal dans le dossier de votre solution et exécutez :

```bash
dotnet add package Aspose.OCR
```

> **Astuce :** Si vous utilisez Visual Studio, vous pouvez également ajouter le package via l'interface du Gestionnaire de packages NuGet.

## Étape 2 : Créer le squelette de l'application console

Configurons une application console minimale qui hébergera notre processeur par lots. Créez un nouveau fichier nommé `Program.cs` et collez le squelette suivant :

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // We'll configure and run the OCR batch processor here.
        }
    }
}
```

Pourquoi encapsuler la logique dans `Main` ? Parce qu'une application console nous donne un retour instantané via `Console.WriteLine`, parfait pour vérifier rapidement que le travail de **OCR par lots** s'est réellement terminé.

## Étape 3 : Configurer l'OcrBatchProcessor

Voici le cœur de la solution. Nous allons instancier `OcrBatchProcessor`, le pointer vers notre dossier d'entrée, indiquer où déposer les résultats, et ajuster quelques paramètres de performance.

```csharp
// Step 3: Configure the OCR batch processor
var batch = new OcrBatchProcessor
{
    // Folder that contains the source images to be processed
    InputFolder = @"YOUR_DIRECTORY/Scans",

    // Folder where the OCR results will be saved
    OutputFolder = @"YOUR_DIRECTORY/OcrResults",

    // Specify the language of the documents (Spanish in this example)
    Language = OcrLanguage.Spanish,

    // Enable GPU acceleration for faster processing (if available)
    UseGpu = true,

    // Limit the number of concurrent OCR operations
    MaxDegreeOfParallelism = 4
};
```

### Pourquoi ces paramètres sont importants

| Paramètre | Ce que ça fait | Quand vous pourriez le changer |
|-----------|----------------|--------------------------------|
| `InputFolder` | Chemin vers les numérisations que vous souhaitez traiter. | Utilisez un chemin relatif pour la portabilité. |
| `OutputFolder` | Emplacement où le texte extrait de chaque image sera enregistré sous forme de fichier `.txt`. | Pointez vers un partage réseau si vous avez besoin d'un stockage central. |
| `Language` | Modèle de langue OCR ; nous avons choisi l'espagnol pour illustrer la prise en charge multilingue. | Changez pour `OcrLanguage.English` ou toute langue prise en charge. |
| `UseGpu` | Décharge les calculs matriciels lourds vers le GPU. | Réglez sur `false` sur des serveurs sans GPU. |
| `MaxDegreeOfParallelism` | Contrôle le nombre d'images traitées simultanément. | Réduisez sur des machines à faible CPU pour éviter la saturation. |

## Étape 4 : Exécuter l'opération par lots avec gestion des erreurs

Exécuter le lot est aussi simple que d'appeler `Execute()`, mais nous l'envelopperons dans un bloc try‑catch afin que vous receviez un message utile si quelque chose ne va pas (par ex., dossier manquant, format d'image non pris en charge).

```csharp
try
{
    // Step 4: Run the batch OCR operation
    batch.Execute();

    // Step 5: Inform the user that processing has finished
    Console.WriteLine("Batch completed.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
}
```

Lorsque le processeur termine, vous verrez **Batch completed.** dans la console, et chaque image source aura un fichier `.txt` correspondant dans `OcrResults`. Les noms de fichiers reflètent les originaux, ce qui facilite le rapprochement avec la numérisation d'origine.

## Étape 5 : Vérifier la sortie – À quoi s'attendre

Après l'exécution du programme, ouvrez n'importe quel fichier dans `YOUR_DIRECTORY/OcrResults`. Vous devriez voir le contenu texte brut extrait de l'image correspondante, par exemple :

```
Este es un documento de prueba.
Contiene varias líneas de texto.
```

Si la sortie apparaît illisible, vérifiez que le `Language` correspond à la langue de vos numérisations. Aspose OCR prend en charge plus de 100 langues, vous pouvez donc remplacer `OcrLanguage.Spanish` par celle dont vous avez besoin.

## Gestion des cas limites et des pièges courants

### 1. GPU non disponible

Si votre machine ne possède pas de GPU compatible, `UseGpu = true` reviendra silencieusement en mode CPU, mais vous perdrez le gain de vitesse. Pour être explicite, vous pouvez détecter la capacité du GPU :

```csharp
if (!OcrBatchProcessor.IsGpuSupported)
{
    batch.UseGpu = false;
    Console.WriteLine("GPU not detected – falling back to CPU processing.");
}
```

### 2. Fichiers volumineux dépassant la mémoire

Lorsque vous traitez des TIFF ou PDF très volumineux, envisagez de les découper préalablement en images plus petites. Aspose OCR peut gérer les PDF multi‑pages, mais la consommation de mémoire augmente avec le nombre de pages. Une étape de pré‑traitement simple avec `Aspose.Imaging` peut découper le document en morceaux gérables.

### 3. Fichiers non‑image dans le dossier d'entrée

Le processeur par lots ignore les fichiers qu'il ne peut pas analyser, mais il est recommandé de garder le dossier propre. Vous pouvez filtrer par extension :

```csharp
batch.InputFolder = @"YOUR_DIRECTORY/Scans";
batch.FileFilter = file => file.EndsWith(".png", StringComparison.OrdinalIgnoreCase)
                         || file.EndsWith(".jpg", StringComparison.OrdinalIgnoreCase);
```

*(Note : `FileFilter` est une propriété hypothétique ; remplacez‑la par l'API réelle si disponible.)*

## Exemple complet fonctionnel

Ci-dessous le programme complet, prêt à copier‑coller. Remplacez `YOUR_DIRECTORY` par le chemin absolu sur votre machine.

```csharp
using System;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Configure the batch processor
            var batch = new OcrBatchProcessor
            {
                InputFolder = @"C:\MyScans",          // <-- change this
                OutputFolder = @"C:\OcrResults",     // <-- change this
                Language = OcrLanguage.Spanish,
                UseGpu = true,
                MaxDegreeOfParallelism = 4
            };

            // Optional: fall back to CPU if no GPU is found
            if (!OcrBatchProcessor.IsGpuSupported)
            {
                batch.UseGpu = false;
                Console.WriteLine("GPU not detected – using CPU.");
            }

            try
            {
                // Run the batch job
                batch.Execute();

                Console.WriteLine("Batch completed.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Error during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Sortie console attendue

```
Batch completed.
```

Et dans `C:\OcrResults` vous trouverez un fichier `.txt` pour chaque image dans `C:\MyScans`.

## Conclusion

Vous disposez maintenant d'une méthode solide et prête pour la production pour **faire du OCR par lots** en C# et **extraire du texte à partir de numérisations** sans ouvrir manuellement chaque fichier. En tirant parti de l'API batch d'Aspose, de l'accélération GPU et du parallélisme configurable, la solution passe de quelques pages à des milliers.

Et après ? Essayez ces idées :

- **Intégrer avec un index de recherche** (par ex., Elasticsearch) pour rendre le texte extrait interrogeable.
- **Ajouter un post‑traitement** tel que la correction orthographique ou la détection de langue.
- **Envelopper l'application console dans un service Windows** pour une surveillance continue d'un dossier de dépôt.

N'hésitez pas à expérimenter, ajuster le niveau de parallélisme, ou changer le modèle de langue. Si vous rencontrez des problèmes, laissez un commentaire ci‑dessous—bon OCR !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}