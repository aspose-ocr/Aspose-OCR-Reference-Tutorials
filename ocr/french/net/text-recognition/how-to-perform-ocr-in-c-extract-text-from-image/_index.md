---
category: general
date: 2026-04-03
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) en
  C# et à extraire du texte d’une image à l’aide d’Aspose OCR, avec vérification orthographique
  pour la langue russe.
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: fr
og_description: Apprenez à effectuer la reconnaissance optique de caractères (OCR)
  en C# et à extraire du texte d’une image à l’aide d’Aspose OCR, avec vérification
  orthographique pour la langue russe.
og_title: Comment réaliser l'OCR en C# – Extraire le texte d'une image
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: Comment réaliser l'OCR en C# – Extraire le texte d’une image
url: /fr/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer de l'OCR en C# – Extraire du texte d'une image

Vous vous êtes déjà demandé **comment effectuer de l'OCR** sur une photo d'une note manuscrite ? Peut-être avez‑vous un reçu numérisé, un panneau dans une langue étrangère, ou une page PDF qui refuse le copier‑coller. Bonne nouvelle ? En quelques lignes de C# et avec la bibliothèque Aspose OCR, vous pouvez transformer cette image en texte modifiable en un clin d’œil.  

Dans ce guide, nous ne vous montrerons pas seulement **comment effectuer de l'OCR**, nous passerons également en revue **extraire du texte d'une image**, **convertir une image en texte**, et même **comment vérifier l'orthographe** du résultat lorsque vous traitez des documents en langue russe. Ça semble beaucoup ? Restez avec nous – nous décomposerons tout étape par étape.

## Ce que vous apprendrez

* Configurer Aspose OCR pour la prise en charge du russe.  
* Charger un fichier image et exécuter la reconnaissance optique de caractères pour **extraire du texte d'une image**.  
* Utiliser le correcteur orthographique intégré pour corriger automatiquement les mots mal orthographiés – la réponse parfaite à “**comment vérifier l'orthographe**” du résultat OCR.  
* Afficher la chaîne nettoyée dans la console, prête pour un traitement ou un stockage ultérieur.

**Prérequis** – vous aurez besoin de :

* .NET 6.0 ou ultérieur (le code fonctionne également avec .NET Framework 4.8).  
* Une licence Aspose OCR valide ou une clé d'évaluation temporaire.  
* Un fichier image contenant du texte russe (pour la démo, nous l’appellerons `russian_note.jpg`).  

Si l’un de ces éléments vous est inconnu, pas de souci. Les étapes ci‑dessous incluent la commande NuGet exacte pour récupérer Aspose OCR, et le code est entièrement autonome.

![exemple de OCR](/images/ocr-demo.png "exemple d'OCR en C#")

## Étape 1 – Installer Aspose OCR et ajouter les espaces de noms

Tout d’abord, vous avez besoin de la bibliothèque. Ouvrez un terminal dans le dossier de votre projet et exécutez :

```bash
dotnet add package Aspose.OCR
```

Cette commande récupère la dernière version stable (en date d’avril 2026, il s’agit de la 22.9). Après la restauration du paquet, ajoutez les directives `using` requises en haut de votre fichier C# :

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*Astuce :* Si vous utilisez Visual Studio, l’IDE proposera d’ajouter ces directives automatiquement dès que vous taperez le premier nom de classe.

## Étape 2 – Initialiser le moteur OCR pour la langue russe

La partie **comment effectuer de l'OCR** commence par créer une instance `OcrEngine`. En spécifiant `OcrLanguage.Russian`, nous indiquons au moteur de charger le jeu de caractères cyrillique et les heuristiques propres à la langue.

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

Pourquoi est‑ce important ? Sans définir la langue, le moteur utilise l’anglais par défaut et interprétera mal de nombreux caractères cyrilliques, produisant une sortie brouillée. Configurer explicitement la langue améliore considérablement la précision.

## Étape 3 – Charger l'image et **convertir l'image en texte**

Nous chargeons maintenant l’image en mémoire. La méthode `Image.FromFile` fonctionne avec la plupart des formats courants (JPG, PNG, BMP). Après le chargement, nous appelons `Recognize` pour **convertir l'image en texte**.

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

La variable `rawText` contient maintenant la sortie brute de l’OCR, qui peut encore contenir des fautes de frappe ou des caractères mal reconnus. Vous pouvez l’afficher pour voir ce que le moteur a capturé :

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## Étape 4 – **Comment vérifier l'orthographe** du résultat OCR

L’OCR russe peut être bruyant, surtout avec des scans à basse résolution. Aspose fournit une classe `SpellChecker` qui comprend les dictionnaires russes dès l’installation. Voici comment l’appeler :

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

La méthode `CheckAndCorrect` renvoie une nouvelle chaîne où les mots mal orthographiés sont remplacés par les alternatives les plus probables. Elle respecte également la ponctuation, évitant ainsi un bloc de texte incompréhensible.

*Cas particulier :* Si la sortie OCR est vide (par ex., l’image est entièrement blanche), `CheckAndCorrect` renverra simplement une chaîne vide. Il est judicieux de prévoir ce cas si vous prévoyez d’écrire le résultat dans un fichier.

## Étape 5 – Afficher le résultat nettoyé

Enfin, nous affichons la chaîne corrigée. Dans une application réelle, vous pourriez l’écrire dans une base de données, une API JSON ou un document Word. Pour cette démo, un affichage console suffit :

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

Lorsque vous exécutez le programme, vous devriez voir quelque chose comme :

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

Remarquez comment le correcteur orthographique a transformé “Привeт” (e latin mélangé) en le cyrillique correct “Привет”. C’est la magie de **comment vérifier l'orthographe** du résultat OCR.

## Exemple complet fonctionnel

Voici le programme complet et exécutable qui rassemble toutes les étapes. Copiez‑collez‑le dans un nouveau projet console et appuyez sur **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### Sortie attendue

Exécuter le programme avec une photo claire et haute résolution d’une écriture manuscrite russe produit généralement une phrase propre et lisible. Si l’image est floue, vous pouvez encore obtenir des mots partiellement corrects, mais le correcteur orthographique atténuera la plupart des erreurs évidentes.

## Pièges courants et astuces

| Problème | Pourquoi cela se produit | Comment corriger / éviter |
|----------|--------------------------|---------------------------|
| **Caractères indésirables** | Basse résolution DPI ou arrière‑plan bruité | Pré‑traiter l’image (augmenter le contraste, redimensionner à ≥300 dpi) avant de la passer à `Recognize`. |
| **Sortie vide** | Chemin de fichier incorrect ou format non pris en charge | Vérifier le chemin, et utiliser `Image.FromFile` dans un bloc `try/catch` pour afficher les erreurs. |
| **Le correcteur orthographique manque des erreurs** | Mots rares absents du dictionnaire | Étendre le dictionnaire en chargeant une liste de mots personnalisée via `spellChecker.AddUserDictionary("mywords.txt")`. |
| **Lenteur de performance sur de gros lots** | L’OCR est gourmand en CPU | Exécuter l’OCR sur un thread en arrière‑plan ou utiliser `Parallel.ForEach` pour plusieurs images. |
| **Exception de licence** | Utilisation de la version d’évaluation au‑delà de la période d’essai | Acheter une licence et appeler `License license = new License(); license.SetLicense("Aspose.Total.lic");` avant de créer `OcrEngine`. |

## Prochaines étapes – Aller au‑delà de l’OCR simple

Maintenant que vous avez maîtrisé **comment effectuer de l'OCR**, envisagez ces extensions :

* **Traitement par lots** – Parcourir un dossier d’images et écrire chaque texte corrigé dans un fichier `.txt`.  
* **Conversion PDF** – Utiliser Aspose PDF pour intégrer le texte extrait dans un PDF consultable.  
* **Détection de langue** – Si vous devez gérer plusieurs langues, inspectez d’abord le résultat OCR et changez `OcrLanguage` en conséquence.  
* **Intégration avec Azure Cognitive Services** – Comparer les résultats d’Aspose avec l’API OCR de Microsoft pour une approche hybride.

Tous ces sujets impliquent naturellement les mots‑clés secondaires **extraire du texte d'une image**, **convertir l'image en texte**, et **comment vérifier l'orthographe**, donc

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}