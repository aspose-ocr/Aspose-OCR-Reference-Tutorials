---
category: general
date: 2026-03-23
description: Extraire du texte d’une image à l’aide d’Aspose OCR en C# et apprendre
  à ajouter un journal console pour un retour en temps réel.
draft: false
keywords:
- extract text from image
- add console logger
language: fr
og_description: Extraire le texte d’une image avec Aspose OCR et ajouter un journal
  console pour surveiller le processus. Tutoriel C# étape par étape.
og_title: Extraire du texte d’une image en C# – Guide complet de programmation
tags:
- OCR
- C#
- logging
title: Extraire du texte d’une image en C# – Guide complet
url: /fr/net/text-recognition/extract-text-from-image-in-c-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'une image en C# – Guide complet

Vous devez **extraire du texte à partir d'une image** rapidement et de manière fiable ? Avec Aspose OCR, vous pouvez le faire en quelques lignes de C#.  
Nous vous montrerons également comment **ajouter un logger console** afin de pouvoir suivre le progrès du moteur OCR directement dans votre terminal.

Imaginez que vous avez un reçu numérisé, une note manuscrite ou une page PDF enregistrée en PNG. Vous voulez les caractères bruts sans ouvrir d'interface lourde. Ce tutoriel vous guide à travers une solution complète, prête à copier‑coller, qui fonctionne aujourd'hui avec .NET 6+ et la dernière bibliothèque Aspose OCR.

À la fin de ce guide, vous serez capable de :

* Charger un fichier image et exécuter l'OCR pour **extraire du texte à partir d'une image**.  
* Brancher un logger console dans Aspose AI afin de voir ce que la bibliothèque fait en arrière‑plan.  
* Appliquer le post‑processeur de correction orthographique intégré pour nettoyer les erreurs d'OCR.  

> **Pré-requis** – Un environnement de développement .NET fonctionnel (Visual Studio 2022, VS Code ou Rider), le SDK .NET 6 ou plus récent, et une licence Aspose OCR (ou un essai gratuit). Aucun autre paquet tiers n'est requis.

---

## Ce dont vous aurez besoin

| Élément | Pourquoi c'est important |
|------|----------------|
| **Aspose.OCR** NuGet package | Fournit la classe `OcrEngine` qui lit réellement l'image. |
| **Aspose.OCR.AI** NuGet package | Vous fournit le cadre du post‑processeur `AsposeAI`, y compris la correction orthographique. |
| **Microsoft.Extensions.Logging** (optional) | Fournit l'interface `ILogger` pour l'étape **add console logger**. |
| **An input image** (`input.png`) | Le fichier source à partir duquel nous allons **extraire du texte à partir d'une image**. |

Vous pouvez installer les packages via le terminal :

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.AI
dotnet add package Microsoft.Extensions.Logging.Abstractions
```

---

## Étape 1 – Extraire du texte à partir d'une image avec Aspose OCR

La première chose que nous faisons est de transmettre l'image au moteur OCR. Ce bloc effectue le travail lourd et renvoie une chaîne brute qui peut encore contenir des fautes d'orthographe.

```csharp
using Aspose.OCR;
using System;

class OcrDemo
{
    static string PerformOcr(string imagePath)
    {
        // Initialise the OCR engine
        using (OcrEngine ocr = new OcrEngine())
        {
            // Load the image – replace with your own path if needed
            ocr.Image = ImageStream.FromFile(imagePath);

            // Run recognition; if it fails we return an empty string
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }

            // The engine populates the Text property with the recognised characters
            string rawText = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + rawText);
            return rawText;
        }
    }
}
```

**Pourquoi cela fonctionne :** `OcrEngine` abstrait tout le prétraitement d'image de bas niveau (binarisation, correction d'inclinaison, etc.). Lorsque `Recognize()` renvoie `true`, la propriété `Text` contient déjà les caractères les plus probables.  

> **Astuce :** Si votre image est grande, envisagez de la redimensionner à ≤ 2000 px sur le côté le plus long avant de la fournir au moteur. Cela accélère le traitement sans nuire à la précision.

---

## Étape 2 – Ajouter un logger console pour un aperçu en temps réel

Nous introduisons maintenant la partie **add console logger**. La journalisation n'est pas seulement pour le débogage ; elle vous donne de la visibilité sur les téléchargements de modèles, les étapes du processeur IA et les éventuels avertissements émis par la bibliothèque.

```csharp
using Microsoft.Extensions.Logging;
using System;

public class ConsoleLogger : ILogger
{
    // Minimal ILogger implementation that writes to the console.
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool IsEnabled(LogLevel logLevel) => true;

    public void Log<TState>(LogLevel logLevel, EventId eventId,
        TState state, Exception exception, Func<TState, Exception, string> formatter)
    {
        Console.WriteLine($"[{logLevel}] {formatter(state, exception)}");
    }
}
```

Vous pouvez maintenant brancher ce logger dans Aspose AI :

```csharp
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;

// ...

ILogger consoleLogger = new ConsoleLogger();   // Implements ILogger
AsposeAI ai = new AsposeAI(consoleLogger);
```

**Ce que vous verrez :** Lorsque le modèle de correction orthographique est téléchargé automatiquement, la console affichera une ligne comme :

```
[Information] Downloading model to YOUR_DIRECTORY/Models/spellcheck.onnx …
```

C’est l’avantage du **add console logger** – vous ne vous demandez jamais si une opération en arrière‑plan a réussi.

---

## Étape 3 – Configurer et enregistrer le post‑processeur de correction orthographique

Aspose AI est fourni avec un post‑processeur de correction orthographique pratique qui nettoie les erreurs OCR courantes (par ex., « rec0gn1ze » → « recognize »). Nous le configurerons, indiquerons éventuellement à la bibliothèque où stocker le modèle, puis l’enregistrerons.

```csharp
// Create the built‑in spell‑check processor
SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

// Optional: tell AsposeAI where to keep downloaded models
AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
{
    AllowAutoDownload = true,
    DirectoryModelPath = "YOUR_DIRECTORY/Models"
};

// Register the processor with the AI engine
ai.SetPostProcessor(spellProcessor, modelConfig);
```

**Pourquoi vous pourriez vouloir un chemin personnalisé :** Dans les pipelines CI/CD, vous souhaitez souvent mettre en cache les modèles dans un répertoire connu afin d'éviter des téléchargements répétés. Le drapeau `AllowAutoDownload` garantit que le modèle est récupéré la première fois que vous exécutez le code.

---

## Étape 4 – Exécuter le post‑processeur sur le résultat OCR

Avec le texte OCR en main et le processeur de correction orthographique prêt, nous transmettons la chaîne brute à `AsposeAI`. Le moteur exécute le modèle, et le processeur stocke le texte corrigé en interne.

```csharp
// Assume ocrResult contains the raw OCR output from Step 1
string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");

// Run the post‑processor – it expects an IEnumerable<string>
ai.RunPostprocessor(new[] { ocrResult });
```

Après cet appel, `spellProcessor` contient une collection d'objets `RecognitionResult`, chacun avec une propriété `RecognitionText` qui contient la version nettoyée.

---

## Étape 5 – Récupérer et afficher le texte corrigé

Enfin, nous extrayons la chaîne corrigée du processeur et l'affichons. C'est le moment où vous voyez réellement le bénéfice à la fois de l'OCR et du flux de travail **add console logger**.

```csharp
// Grab the first (and only) result
string correctedText = spellProcessor.GetResult()[0].RecognitionText;
Console.WriteLine("\nCorrected OCR output:\n" + correctedText);
```

**Sortie attendue** (en supposant que l'image contienne la phrase « Aspose OCR demo » avec quelques défauts OCR) :

```
Raw OCR output:
Asp0se OCR d3mo

[Information] Model downloaded successfully.
[Information] Spell‑check completed.

Corrected OCR output:
Aspose OCR demo
```

Remarquez comment le logger nous a indiqué que le modèle était prêt, et la ligne corrigée s'affiche proprement.

---

## Étape 6 – Nettoyer les ressources

`AsposeAI` et `OcrEngine` implémentent tous deux `IDisposable`. Les libérer libère la mémoire native et les poignées de fichiers, ce qui est particulièrement important dans les services de longue durée.

```csharp
// At the end of Main()
ai.Dispose();   // Releases AI resources
// OcrEngine is already disposed via the using‑statement in PerformOcr()
```

---

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet console (`dotnet new console`). Remplacez `"YOUR_DIRECTORY"` par un dossier réel sur votre machine.

```csharp
using Aspose.OCR;
using Aspose.OCR.AI;
using Aspose.OCR.AI.PostProcessors;
using Microsoft.Extensions.Logging; // optional logger
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // ---------- Step 1: OCR ----------
        string ocrResult = PerformOcr("YOUR_DIRECTORY/input.png");
        if (string.IsNullOrEmpty(ocrResult)) return;

        // ---------- Step 2: Initialise AI with console logger ----------
        ILogger consoleLogger = new ConsoleLogger(); // implements ILogger
        AsposeAI ai = new AsposeAI(consoleLogger);

        // ---------- Step 3: Spell‑check processor ----------
        SpellCheckAIProcessor spellProcessor = new SpellCheckAIProcessor();

        // ---------- Step 4: Model configuration (optional) ----------
        AsposeAIModelConfig modelConfig = new AsposeAIModelConfig
        {
            AllowAutoDownload = true,
            DirectoryModelPath = "YOUR_DIRECTORY/Models"
        };

        // ---------- Step 5: Register and run ----------
        ai.SetPostProcessor(spellProcessor, modelConfig);
        ai.RunPostprocessor(new[] { ocrResult });

        // ---------- Step 6: Show corrected text ----------
        string correctedText = spellProcessor.GetResult()[0].RecognitionText;
        Console.WriteLine("\nCorrected OCR output:\n" + correctedText);

        // ---------- Clean up ----------
        ai.Dispose();
    }

    static string PerformOcr(string imagePath)
    {
        using (OcrEngine ocr = new OcrEngine())
        {
            ocr.Image = ImageStream.FromFile(imagePath);
            if (!ocr.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return string.Empty;
            }
            string raw = ocr.Text;
            Console.WriteLine("Raw OCR output:\n" + raw);
            return raw;
        }
    }
}

// Minimal console logger implementation
public class ConsoleLogger : ILogger
{
    public IDisposable BeginScope<TState>(TState state) => null;
    public bool

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}