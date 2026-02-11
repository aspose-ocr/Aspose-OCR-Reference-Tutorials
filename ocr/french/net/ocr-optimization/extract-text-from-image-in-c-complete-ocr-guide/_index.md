---
category: general
date: 2026-02-11
description: Extraire du texte d’une image en C# avec Aspose OCR. Apprenez comment
  charger une image pour l’OCR, améliorer la précision de l’OCR et corriger les erreurs
  d’OCR avec la vérification orthographique.
draft: false
keywords:
- extract text from image
- image to text c#
- improve ocr accuracy
- load image for ocr
- fix ocr errors
language: fr
og_description: Extraire du texte d’une image en C# avec Aspose OCR. Ce guide montre
  comment charger une image pour l’OCR, améliorer la précision de l’OCR et corriger
  les erreurs d’OCR.
og_title: Extraire du texte d’une image en C# – Guide complet d’OCR
tags:
- C#
- OCR
- Aspose
- Text Extraction
title: Extraire du texte d’une image en C# – Guide complet d’OCR
url: /fr/net/ocr-optimization/extract-text-from-image-in-c-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d’une image en C# – Guide complet d’OCR

Vous avez déjà eu besoin d’**extraire du texte d’une image** mais les résultats ressemblaient à du charabia ? Vous n’êtes pas seul. Dans de nombreuses applications réelles—par exemple la numérisation de reçus, la digitalisation de notes ou la migration de documents anciens—obtenir du texte propre à partir d’une photo est le premier, et souvent le plus difficile, obstacle.

Heureusement, avec Aspose OCR vous pouvez **charger l’image pour l’OCR**, exécuter une vérification orthographique, et repartir avec du texte propre et interrogeable. Dans ce tutoriel, nous parcourrons toute la chaîne, de la lecture d’un JPEG au polissage du résultat, et vous verrez exactement comment **améliorer la précision de l’OCR** en même temps.

> **Ce que vous obtiendrez :** un programme console C# prêt à l’emploi qui extrait le texte d’une image, corrige les erreurs courantes d’OCR, et affiche à la fois les résultats bruts et nettoyés.

---

## Ce dont vous avez besoin

- .NET 6 ou supérieur (le code fonctionne également avec .NET Framework 4.7+)
- Visual Studio 2022 (ou tout autre IDE de votre choix)
- Une clé d’essai gratuite Aspose OCR ou une version sous licence
- Un fichier image contenant du texte tapé ou imprimé (par ex., `typed_note.jpg`)

Aucune autre bibliothèque tierce n’est requise—Aspose gère les modèles linguistiques et la vérification orthographique automatiquement.

---

## Étape 1 – Installer le package NuGet Aspose OCR

Avant de pouvoir **extraire du texte d’une image**, le moteur OCR doit être disponible sur la machine.

```powershell
# From the Package Manager Console
Install-Package Aspose.OCR
```

Ou, si vous préférez la CLI :

```bash
dotnet add package Aspose.OCR
```

Le package inclut les données linguistiques, mais définir `AutomaticResourceDownload = true` (comme nous le ferons plus tard) garantit que tout dictionnaire manquant sera téléchargé au moment de l’exécution.

---

## Étape 2 – Charger l’image pour l’OCR

La première chose dont le moteur a besoin est un bitmap. Vous pouvez lui fournir n’importe quel format supporté par `System.Drawing.Image`, tel que PNG, JPEG, BMP ou TIFF.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Path to your source picture – change this to your own folder
string imagePath = @"C:\MyImages\typed_note.jpg";

// Load the image inside a using block so the file handle is released promptly
using (Image image = Image.FromFile(imagePath))
{
    // The rest of the OCR pipeline lives inside this block
}
```

> **Pourquoi le bloc `using` ?** Il libère automatiquement l’objet `Image`, évitant les problèmes de verrouillage de fichier qui surviennent souvent lorsqu’on oublie de libérer les ressources.

---

## Étape 3 – Effectuer l’OCR – « Image to Text C# » en action

Nous allons maintenant **extraire du texte d’une image**. La classe `OcrEngine` fait le gros du travail.

```csharp
// Step 3: Initialise the OCR engine
var ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true, // pulls language packs if missing
    Language = OcrLanguage.English    // set to your document's language
};

// Inside the using block from Step 2
var ocrResult = ocrEngine.Recognize(image);
string rawText = ocrResult.Text;
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

À ce stade vous avez une chaîne qui reflète ce que le moteur voit sur l’image. En pratique, le résultat peut contenir des caractères parasites, des mots mal reconnus ou des sauts de ligne étranges—d’où l’étape suivante.

---

## Étape 4 – Améliorer la précision de l’OCR avec la vérification orthographique

Aspose fournit un `SpellChecker` dédié qui connaît la langue que vous traitez. L’appliquer sur la chaîne brute corrige souvent les erreurs les plus flagrantes.

```csharp
// Step 4: Initialise spell‑check (resources are auto‑downloaded)
var spellChecker = new SpellChecker(OcrLanguage.English);

// Correct the OCR output
string correctedText = spellChecker.Correct(rawText);
Console.WriteLine("\nCorrected OCR output:");
Console.WriteLine(correctedText);
```

> **Astuce :** Si vous travaillez avec un vocabulaire spécifique à un domaine (par ex., des termes médicaux), vous pouvez fournir un dictionnaire personnalisé à `SpellChecker` via ses surcharges.

---

## Étape 5 – Corriger manuellement les erreurs d’OCR (facultatif)

Même le meilleur correcteur orthographique peut manquer des erreurs dépendant du contexte. Un passage de post‑traitement rapide peut attraper des confusions comme « l » vs « 1 » ou « O » vs « 0 ».

```csharp
// Simple regex to replace common OCR confusions
string finalText = System.Text.RegularExpressions.Regex.Replace(
    correctedText,
    @"\b([lI])\b", // isolated l or I
    "1");

// Additional custom rules can be added here
Console.WriteLine("\nFinal cleaned text:");
Console.WriteLine(finalText);
```

N’hésitez pas à enrichir cette section avec vos propres heuristiques—peut‑être une table de correspondance pour les codes produits ou une liste d’acronymes connus.

---

## Exemple complet fonctionnel

Voici le programme complet que vous pouvez copier‑coller dans un nouveau projet d’application console. Il inclut chaque étape décrite, ainsi que des commentaires utiles.

```csharp
// ------------------------------------------------------------
// Extract Text from Image in C# – Full Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Text.RegularExpressions;

class Program
{
    static void Main()
    {
        // 1️⃣ Configure OCR engine – automatic download ensures language data is present
        var ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to analyse
        string imagePath = @"C:\MyImages\typed_note.jpg";
        using (Image image = Image.FromFile(imagePath))
        {
            // 3️⃣ Run OCR – this is where we *extract text from image*
            var ocrResult = ocrEngine.Recognize(image);
            string rawText = ocrResult.Text;
            Console.WriteLine("Before (raw OCR):");
            Console.WriteLine(rawText);
            Console.WriteLine(new string('-', 40));

            // 4️⃣ Spell‑check to *improve OCR accuracy*
            var spellChecker = new SpellChecker(OcrLanguage.English);
            string correctedText = spellChecker.Correct(rawText);
            Console.WriteLine("After (spell‑checked):");
            Console.WriteLine(correctedText);
            Console.WriteLine(new string('-', 40));

            // 5️⃣ Optional custom clean‑up – *fix OCR errors* that the spell‑checker missed
            string finalText = Regex.Replace(correctedText,
                @"\b([lI])\b", // replace isolated 'l' or 'I' with '1'
                "1");

            Console.WriteLine("Final (post‑processed):");
            Console.WriteLine(finalText);
        }
    }
}
```

### Résultat attendu

En supposant que `typed_note.jpg` contienne la phrase « Hello world, this is a test 123 », la console affichera quelque chose comme :

```
Before (raw OCR):
H3llo w0rld, th1s is a test 123

After (spell‑checked):
Hello world, this is a test 123

Final (post‑processed):
Hello world, this is a test 123
```

Remarquez comment le correcteur orthographique a transformé « H3llo » en « Hello », et comment l’expression régulière a supprimé le « 1 » errant dans « th1s ».

---

## Questions fréquentes et cas particuliers

| Question | Réponse |
|----------|---------|
| **Puis‑je utiliser une autre langue ?** | Oui. Définissez `ocrEngine.Language = OcrLanguage.Spanish` (ou tout autre enum supporté) et transmettez la même langue à `SpellChecker`. |
| **Que faire si mon image est très grande ?** | Redimensionnez‑la avant de la passer à l’OCR ; `Image` possède la méthode `GetThumbnailImage` pour un redimensionnement rapide. |
| **Ai‑je besoin d’une connexion Internet ?** | Seulement la première fois qu’un pack de langue manque ; ensuite les ressources sont mises en cache localement. |
| **Comment gérer les PDF multi‑pages ?** | Convertissez chaque page en image (par ex., avec `PdfRenderer`) et exécutez le même pipeline page par page. |
| **Le correcteur orthographique est‑il sensible à la langue ?** | Absolument. Il utilise le même modèle linguistique que vous avez fourni au moteur OCR, assurant la cohérence. |

---

## Prochaines étapes et sujets associés

- **Traitement par lots :** Enveloppez le code dans une boucle `foreach` pour traiter un dossier d’images.
- **Texte manuscrit :** Remplacez par `OcrLanguage.EnglishHandwritten` pour de meilleurs résultats sur des notes cursives.
- **Parallélisme :** Utilisez `Parallel.ForEach` pour accélérer les gros volumes sur des machines multi‑cœurs.
- **Export vers JSON/CSV :** Sérialisez `finalText` avec les métadonnées (nom de fichier, scores de confiance) pour des analyses en aval.

Si vous êtes curieux de transformer les chaînes extraites en PDF interrogeables, consultez notre guide sur **« Create searchable PDF from image in C# »**. Il s’appuie directement sur le même pipeline OCR que nous venons de couvrir.

---

## Conclusion

Nous venons de démontrer une méthode pragmatique pour **extraire du texte d’une image** en C# avec Aspose OCR, tout en montrant comment **charger l’image pour l’OCR**, **améliorer la précision de l’OCR**, et **corriger les erreurs d’OCR** à l’aide d’un correcteur orthographique intégré et d’un petit nettoyage regex. L’exemple complet fonctionne immédiatement, ne nécessite qu’un seul package NuGet, et peut être étendu pour s’adapter à pratiquement n’importe quel scénario de digitalisation de documents.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}