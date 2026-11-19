---
category: general
date: 2026-06-03
description: Effectuez une OCR sur une image et extrayez le texte à l'aide d'Aspose.OCR.
  Apprenez à détecter les mots mal orthographiés et à obtenir des suggestions d'orthographe
  dans une démonstration C# unique.
draft: false
keywords:
- perform OCR on image
- extract text from image
- detect misspelled words
- get spelling suggestions
- how to extract text
language: fr
og_description: Effectuer une OCR sur l’image pour extraire le texte, puis détecter
  les mots mal orthographiés et obtenir des suggestions d’orthographe avec Aspose.OCR
  en C#.
og_title: Effectuer la reconnaissance optique de caractères sur une image et détecter
  les mots mal orthographiés en C#
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on image and extract text from image using Aspose.OCR.
    Learn how to detect misspelled words and get spelling suggestions in a single
    C# demo.
  headline: Perform OCR on Image and Detect Misspelled Words in C#
  type: TechArticle
tags:
- Aspose OCR
- C#
- Spell Checking
title: Effectuer une reconnaissance optique de caractères sur une image et détecter
  les mots mal orthographiés en C#
url: /fr/net/text-recognition/perform-ocr-on-image-and-detect-misspelled-words-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer la reconnaissance optique de caractères (OCR) sur une image et détecter les mots mal orthographiés en C#

Vous êtes-vous déjà demandé comment **perform OCR on image** des fichiers sans perdre patience ? Vous n'êtes pas seul. Que vous numérisiez de vieilles lettres, scanniez des reçus ou construisiez un flux de travail intelligent pour les documents, extraire du texte propre à partir d’images est le premier obstacle. Bonne nouvelle : avec Aspose.OCR, vous pouvez mettre en place une solution en quelques minutes, et en prime vous pouvez également **detect misspelled words** et **get spelling suggestions** lors de la même exécution.

Dans ce tutoriel, nous allons parcourir une application console C# complète, prête à l’emploi, qui **extracts text from image**, exécute un correcteur orthographique anglais, et affiche chaque erreur avec des suggestions de correction pratiques. À la fin, vous saurez exactement **how to extract text**, comment appeler l’API de vérification orthographique, et à quoi ressemble la sortie console attendue.

## Ce que vous allez créer

- Charger un bitmap (ou PNG) contenant des fautes typographiques.  
- Exécuter Aspose.OCR pour **perform OCR on image** et obtenir les données brutes sous forme de chaîne.  
- Initialiser le correcteur orthographique anglais intégré.  
- **Detect misspelled words** et **get spelling suggestions** pour chaque mot.  
- Imprimer un rapport clair dans la console.

Pas de services externes, pas d’appels HTTP compliqués — juste un seul package NuGet et quelques lignes de code.

## Prérequis

- .NET 6.0 SDK ou version ultérieure (le code fonctionne également avec .NET Framework 4.7+).  
- Visual Studio 2022 (ou tout autre éditeur de votre choix).  
- Package NuGet Aspose.OCR for .NET (`Aspose.OCR`).  
- Un fichier image (`letter_with_typos.png`) placé quelque part où le projet peut y accéder.

Si vous n’avez jamais utilisé Aspose auparavant, pas d’inquiétude — l’installation du package est aussi simple que d’exécuter :

```bash
dotnet add package Aspose.OCR
```

Passons maintenant à l’implémentation.

## Étape 1 : Créer le projet et installer Aspose.OCR

Créez un nouveau projet console et ajoutez la bibliothèque OCR :

```bash
dotnet new console -n OcrSpellDemo
cd OcrSpellDemo
dotnet add package Aspose.OCR
```

Une fois la restauration terminée, ouvrez `Program.cs`. Nous remplacerons le contenu par défaut par le code complet plus tard, mais commençons d’abord par expliquer l’utilité de chaque espace de noms.

- `Aspose.OCR` – Moteur OCR principal et gestion des images.  
- `Aspose.OCR.SpellCheck` – Utilitaires de vérification orthographique fournis avec la bibliothèque.  
- `System` – Classes de base .NET standard (par ex., `Console`).

## Étape 2 : Charger l’image et **perform OCR on image**

Le premier vrai travail consiste à fournir l’image au moteur OCR. Aspose.OCR lit de nombreux formats (PNG, JPEG, TIFF). Voici l’extrait qui fait le gros du travail :

```csharp
// Step 2: Load the image that contains the text to be recognized
var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

// Step 3: Perform OCR to extract the raw text from the image
var ocrEngine = new OcrEngine();
var ocrResult = ocrEngine.Recognize(image);
```

> **Pourquoi c’est important :** `OcrImage.FromFile` masque les détails au niveau des pixels, tandis que `OcrEngine.Recognize` exécute le modèle neuronal entraîné qui traduit les glyphes visuels en caractères Unicode. La propriété `ocrResult.Text` contient maintenant la chaîne brute — exactement ce dont vous avez besoin pour **extract text from image**.

> **Astuce :** Si votre image contient plusieurs langues, vous pouvez définir `ocrEngine.Language = OcrLanguage.Multilingual;` avant d’appeler `Recognize`.

## Étape 3 : Initialiser le correcteur orthographique anglais

Aspose.OCR fournit un moteur de vérification orthographique intégré qui comprend l’anglais dès le départ. L’initialiser ne prend qu’une ligne :

```csharp
// Step 4: Initialise the English spell‑checker
var spellChecker = new SpellChecker(OcrLanguage.English);
```

> **Pourquoi cette étape est cruciale :** La sortie OCR peut inclure des caractères mal reconnus (par ex., “l” vs “1”) ou de véritables fautes de frappe du document source. Le correcteur orthographique analysera la chaîne, repérera les jetons suspects et proposera des alternatives.

## Étape 4 : **Detect misspelled words** et obtenir les suggestions

Nous injectons maintenant le texte OCR dans le vérificateur :

```csharp
// Step 5: Check the recognized text for misspelled words and obtain suggestions
var misspellings = spellChecker.Check(ocrResult.Text);
```

`misspellings` est une collection où chaque entrée contient le mot erroné et un tableau de corrections possibles.

## Étape 5 : Afficher les résultats

Enfin, nous parcourons la collection et imprimons un rapport lisible :

```csharp
// Step 6: Output each misspelled word together with its suggested corrections
foreach (var entry in misspellings)
{
    Console.WriteLine($"Misspelled: {entry.Word}");
    Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
}
```

### Sortie console attendue

En supposant que `letter_with_typos.png` contienne la phrase :

```
Ths is an exampel of a lettter with som misspelled wrds.
```

L’exécution du démonstration produira quelque chose comme :

```
Misspelled: Ths
  Suggestions: This, Thus, The
Misspelled: exampel
  Suggestions: example, exemplar, exampell
Misspelled: lettter
  Suggestions: letter, litter, lett
Misspelled: som
  Suggestions: some, sum, son
Misspelled: wrds
  Suggestions: words, wards, wryds
```

Remarquez comment chaque faute est associée à plusieurs corrections plausibles — exactement ce qu’il faut pour créer une interface utilisateur de correction conviviale.

## Exemple complet fonctionnel

Voici le programme **complet, prêt à copier‑coller**. Remplacez `YOUR_DIRECTORY` par le chemin réel vers votre fichier image.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Load the image that contains the text to be recognized
        var image = OcrImage.FromFile(@"YOUR_DIRECTORY/letter_with_typos.png");

        // Step 2: Perform OCR to extract the raw text from the image
        var ocrEngine = new OcrEngine();
        var ocrResult = ocrEngine.Recognize(image);

        // Step 3: Initialise the English spell‑checker
        var spellChecker = new SpellChecker(OcrLanguage.English);

        // Step 4: Check the recognized text for misspelled words and obtain suggestions
        var misspellings = spellChecker.Check(ocrResult.Text);

        // Step 5: Output each misspelled word together with its suggested corrections
        foreach (var entry in misspellings)
        {
            Console.WriteLine($"Misspelled: {entry.Word}");
            Console.WriteLine("  Suggestions: " + string.Join(", ", entry.Suggestions));
        }

        // Optional: Keep console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

> **Cas limites à considérer**  
> - **Image vide :** Si le moteur OCR renvoie une chaîne vide, `spellChecker.Check` renverra simplement une collection vide — pas de plantage.  
> - **Texte non anglais :** Remplacez `OcrLanguage.English` par `OcrLanguage.French` (ou toute langue prise en charge) pour **detect misspelled words** dans d’autres paramètres régionaux.  
> - **Documents volumineux :** Pour les PDF multi‑pages, vous parcourriez chaque page, exécuteriez l’OCR, puis agrègeriez les résultats avant la vérification orthographique.

## Vue d’ensemble visuelle (texte alternatif)

![Diagram showing the flow to perform OCR on image, extract text from image, and then detect misspelled words with spelling suggestions](perform-ocr-on-image-flow.png)

*Le diagramme ci‑dessus illustre le pipeline de bout en bout : image → moteur OCR → texte brut → correcteur orthographique → suggestions.*

## Questions fréquentes & Astuces avancées

| Question | Réponse |
|----------|--------|
| **Ai‑je besoin d’une connexion Internet ?** | Non. Aspose.OCR fonctionne entièrement en local ; idéal pour les environnements hors ligne ou sécurisés. |
| **Quelle est la précision du correcteur orthographique ?** | Il utilise un dictionnaire d’environ 150 k mots anglais et un algorithme de correspondance floue, donc la plupart des fautes courantes sont détectées. |
| **Puis‑je personnaliser le dictionnaire ?** | Oui. `SpellChecker.AddUserDictionary("custom.txt")` vous permet de charger des termes spécifiques à votre domaine (par ex., noms de produits). |
| **Que faire si l’image est inclinée ?** | Le moteur OCR détecte automatiquement l’orientation, mais vous pouvez appeler manuellement `ocrEngine.ImagePreprocessing.Rotate(angle)` pour les cas récalcitrants. |
| **Existe‑t‑il un moyen de mettre en évidence les suggestions dans l’UI ?** | Après avoir récupéré la collection `misspellings`, vous pouvez mapper chaque `entry.Word` à sa position dans `ocrResult.Text` et le souligner dans un RichTextBox ou une vue web. |

## Conclusion

Nous venons de vous montrer **how to perform OCR on image**, **extract text from image**, puis **detect misspelled words** tout en **getting spelling suggestions** — le tout avec une petite application console C#. L’idée centrale est simple : laissez Aspose.OCR faire le travail lourd de reconnaissance de caractères, puis laissez son correcteur orthographique intégré nettoyer le résultat. À partir d’ici, vous pouvez transformer la démo en un service complet de traitement de documents, l’intégrer à une API web, ou la brancher à un éditeur de bureau.

Prêt pour l’étape suivante ? Essayez de changer la langue en espagnol, traitez un PDF multi‑pages, ou créez une petite interface WPF qui permet à l’utilisateur de cliquer sur un mot pour accepter une suggestion. Les blocs de construction sont déjà en place — continuez à expérimenter.

Si vous avez rencontré des problèmes ou avez des idées d’extensions, laissez un commentaire ci‑dessous. Bon codage !


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}