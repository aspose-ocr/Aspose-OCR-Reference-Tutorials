---
category: general
date: 2026-04-08
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) sur
  une image et à créer un fichier JSON en C# avec Aspose OCR. Ce tutoriel Aspose OCR
  C# montre la conversion d’une image OCR en JSON avec les valeurs de confiance.
draft: false
keywords:
- perform OCR on image
- write JSON file C#
- OCR image to JSON
- Aspose OCR C# tutorial
language: fr
og_description: Effectuez la reconnaissance optique de caractères (OCR) sur une image
  et exportez les résultats vers un fichier JSON en C#. Ce tutoriel couvre le flux
  de travail complet d’Aspose OCR en C#, y compris les scores de confiance.
og_title: Effectuer la reconnaissance OCR d’une image en JSON en C# – Guide Aspose
  OCR
tags:
- Aspose
- OCR
- C#
- JSON
title: Effectuer l'OCR d'une image en JSON en C# avec Aspose
url: /fr/net/text-recognition/perform-ocr-on-image-to-json-in-c-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer une OCR sur une image et obtenir du JSON en C# avec Aspose

Vous avez déjà eu besoin d'**effectuer une OCR sur des fichiers image** mais vous ne saviez pas comment obtenir les résultats sous forme structurée ? Vous n'êtes pas seul — les développeurs demandent constamment : « Comment transformer une image scannée en données exploitables ? » Bonne nouvelle, Aspose.OCR rend cela très simple, et vous pouvez même **write JSON file C#**‑style avec les scores de confiance inclus.

Dans ce guide, nous parcourrons un **aspose OCR C# tutorial** complet qui couvre tout, du chargement de l'image à l'exportation du texte reconnu au format JSON. À la fin, vous disposerez d’une application console exécutable qui **effectue une OCR sur une image**, convertit la sortie en JSON (y compris les valeurs de confiance) et l’enregistre en une seule ligne de code. Aucun pas caché, aucun script externe — juste du pur C#.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- le SDK .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Core et .NET Framework)
- Visual Studio 2022 (ou tout autre éditeur de votre choix)
- une licence valide **Aspose.OCR for .NET** ou une licence temporaire gratuite (l’essai gratuit suffit pour les tests)
- un fichier image (`input.png`) que vous souhaitez traiter (tout format courant — PNG, JPG, BMP—fonctionne)

C’est tout. Si l’un de ces éléments vous manque, procurez‑le‑vous maintenant ; le reste du tutoriel part du principe qu’ils sont déjà en place.

## Étape 1 : Installer le package NuGet Aspose.OCR

Première chose à faire — ajouter la bibliothèque à votre projet. Ouvrez un terminal dans le dossier du projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Cela récupère la dernière version (en avril 2026, c’est la 23.12) et ajoute les DLL nécessaires au dossier `bin`. Aucune configuration supplémentaire n’est requise.

## Étape 2 : Initialiser le moteur OCR (Effectuer une OCR sur l’image)

Nous créons maintenant une instance `OcrEngine` et indiquons la langue à utiliser. L’anglais (`"en"`) est le plus courant, mais vous pouvez le remplacer par `"fr"`, `"de"` ou toute autre langue prise en charge.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Path to your input image – change as needed
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        // Path where the JSON will be saved
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // Step 2: Initialize the OCR engine – this is where we **perform OCR on image**
        var ocrEngine = new OcrEngine
        {
            Language = "en"               // Set language; you can use ISO‑639‑1 codes
        };

        // Optional: tweak recognition options (speed vs. accuracy)
        // ocrEngine.RecognitionMode = RecognitionMode.LargeText; // Uncomment for large blocks
```

**Pourquoi nous l’initialisons ici :** `OcrEngine` contient toute la configuration nécessaire au processus de reconnaissance. Définir la langue dès le départ garantit que le moteur utilise le bon jeu de caractères, ce qui améliore considérablement la précision.

## Étape 3 : Reconnaître l’image et capturer la confiance

Le moteur étant prêt, nous lui fournissons le fichier image. La méthode `RecognizeImage` renvoie un objet `OcrResult` qui contient à la fois le texte extrait et un score de confiance pour chaque mot.

```csharp
        // Step 3: Perform OCR on the image file
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        // Verify that the result is not null
        if (ocrResult == null)
        {
            Console.WriteLine("OCR failed – check the file path and format.");
            return;
        }

        // For debugging: print the plain text to the console
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
```

**Que se passe‑t‑il en coulisses ?** Aspose exécute un reconnaisseur basé sur un réseau de neurones qui analyse chaque bloc de pixels, le compare à son modèle linguistique et associe une valeur de confiance (0‑100) indiquant le degré de certitude pour chaque mot.

## Étape 4 : Convertir le résultat en JSON (OCR Image to JSON)

Aspose rend la conversion très simple. En passant `includeConfidence: true`, nous obtenons une charge JSON qui ressemble à ceci :

```json
{
  "Text": "Hello world",
  "Words": [
    { "Value": "Hello", "Confidence": 97.3 },
    { "Value": "world", "Confidence": 95.8 }
  ]
}
```

Voici le code qui produit la chaîne JSON :

```csharp
        // Step 4: Convert OCR result to JSON, including confidence values
        string jsonResult = ocrResult.ToJson(includeConfidence: true);
```

**Pourquoi inclure la confiance ?** Si vous prévoyez d’alimenter les données dans des processus en aval (par ex. validation, mise en évidence dans l’UI), connaître les mots incertains vous permet de décider si vous devez demander une confirmation à l’utilisateur.

## Étape 5 : Écrire le fichier JSON en style C#

Nous allons maintenant **write JSON file C#**. La méthode `File.WriteAllText` est atomique et fonctionne sur toutes les plateformes, ce qui la rend parfaite pour les applications console.

```csharp
        // Step 5: Save the JSON output to a file
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

Voilà l’ensemble du flux de travail — cinq étapes concises qui **effectuent une OCR sur une image**, transforment la sortie en JSON et la persistant.

## Exemple complet fonctionnel

Ci‑dessous se trouve le programme complet que vous pouvez copier‑coller dans `Program.cs`. Assurez‑vous que `input.png` se trouve dans le même dossier que le binaire compilé ou ajustez les chemins en conséquence.

```csharp
using Aspose.Ocr;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // -------------------------------------------------------
        // 1️⃣ Set up file locations (feel free to change paths)
        // -------------------------------------------------------
        string inputPath = Path.Combine(Environment.CurrentDirectory, "input.png");
        string outputPath = Path.Combine(Environment.CurrentDirectory, "output.json");

        // -------------------------------------------------------
        // 2️⃣ Initialize the OCR engine – this is where we **perform OCR on image**
        // -------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = "en" // English – replace with "fr", "es", etc. as needed
        };

        // -------------------------------------------------------
        // 3️⃣ Recognize the image and obtain confidence values
        // -------------------------------------------------------
        OcrResult ocrResult = ocrEngine.RecognizeImage(inputPath);

        if (ocrResult == null)
        {
            Console.WriteLine("❌ OCR failed – verify the image path and format.");
            return;
        }

        // Show plain text (optional)
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine();

        // -------------------------------------------------------
        // 4️⃣ Convert the result to JSON – **OCR image to JSON**
        // -------------------------------------------------------
        string jsonResult = ocrResult.ToJson(includeConfidence: true);

        // -------------------------------------------------------
        // 5️⃣ Write the JSON file – **write JSON file C#** style
        // -------------------------------------------------------
        File.WriteAllText(outputPath, jsonResult);
        Console.WriteLine($"✅ JSON with confidence saved to: {outputPath}");
    }
}
```

### Résultat attendu

Lorsque vous exécutez le programme (`dotnet run`), vous verrez quelque chose comme :

```
=== Extracted Text ===
Hello world

✅ JSON with confidence saved to: C:\YourProject\output.json
```

Et `output.json` contiendra le JSON structuré présenté plus haut, complet avec les pourcentages de confiance pour chaque mot.

## Astuces pro & cas particuliers

- **Gestion des fichiers manquants :** Enveloppez l’appel `RecognizeImage` dans un `try/catch` pour `FileNotFoundException` si vous avez des chemins dynamiques.
- **Langues différentes :** Définissez `ocrEngine.Language = "fr"` pour le français, ou chargez un pack de langue personnalisé via `ocrEngine.LoadLanguage("custom.lang")`.
- **Documents volumineux :** Pour les PDF multi‑pages, convertissez chaque page en image d’abord (par ex. avec `Aspose.PDF`) puis bouclez sur les étapes OCR.
- **Optimisation des performances :** Si vous avez besoin de résultats rapides, passez à `RecognitionMode.Fast` — vous perdez un peu de précision mais gagnez en vitesse.
- **Mise en forme du JSON :** Vous voulez un JSON joliment indenté ? Utilisez `JsonConvert.SerializeObject` de Newtonsoft avec `Formatting.Indented` après avoir désérialisé la chaîne JSON d’Aspose.

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec .NET Framework ?**  
R : Absolument. Le même package NuGet cible .NET Standard 2.0, vous pouvez donc le référencer depuis .NET Framework 4.6.1 et versions ultérieures.

**Q : Et si j’ai besoin de la confiance pour le document entier, pas mot à mot ?**  
R : `OcrResult` expose également `OverallConfidence`. Vous pouvez l’ajouter manuellement au JSON :

```csharp
var customObj = new
{
    Text = ocrResult.Text,
    OverallConfidence = ocrResult.OverallConfidence,
    Words = ocrResult.Words
};
string json = JsonConvert.SerializeObject(customObj, Formatting.Indented);
```

**Q : Puis‑je diffuser le JSON directement vers une API web ?**  
R : Oui. Remplacez `File.WriteAllText` par un POST `HttpClient` qui envoie `jsonResult

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}