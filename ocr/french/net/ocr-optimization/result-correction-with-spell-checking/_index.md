---
title: Correction des résultats avec vérification orthographique dans la reconnaissance d'images OCR
linktitle: Correction des résultats avec vérification orthographique dans la reconnaissance d'images OCR
second_title: API Aspose.OCR .NET
description: Améliorez la précision de l'OCR avec Aspose.OCR pour .NET. Corrigez l’orthographe, personnalisez les dictionnaires et obtenez une reconnaissance de texte sans erreur sans effort.
type: docs
weight: 13
url: /fr/net/ocr-optimization/result-correction-with-spell-checking/
---
## Introduction

Dans le domaine de la reconnaissance optique de caractères (OCR), l'obtention de résultats précis est cruciale pour extraire des informations significatives à partir des images. Un défi courant consiste à gérer les mots mal orthographiés dans le processus de reconnaissance. Heureusement, Aspose.OCR pour .NET fournit une solution puissante pour améliorer les résultats de l'OCR grâce à la vérification orthographique.

Ce didacticiel vous guidera tout au long du processus de correction des résultats avec vérification orthographique à l'aide d'Aspose.OCR pour .NET. À la fin, vous serez équipé pour améliorer la précision du texte dérivé de l'OCR, garantissant ainsi une sortie plus raffinée et sans erreur.

## Conditions préalables

Avant de nous plonger dans la magie du correcteur orthographique, assurez-vous d'avoir les conditions préalables suivantes en place :

-  Aspose.OCR pour la bibliothèque .NET : téléchargez et installez la bibliothèque Aspose.OCR à partir du[page de sortie](https://releases.aspose.com/ocr/net/).

- Répertoire de documents : assurez-vous d'avoir un répertoire désigné pour vos documents. Remplacez « Votre répertoire de documents » dans les extraits de code par le chemin réel.

## Importer des espaces de noms

Commençons par importer les espaces de noms nécessaires dans votre projet .NET :

```csharp
using System;
using Aspose.OCR.SpellChecker;
using System.Collections.Generic;
```

## Étape 1 : initialiser Aspose.OCR

Initialisez une instance d'Aspose.OCR pour lancer le processus OCR.

```csharp
// Le chemin d'accès au répertoire des documents.
string dataDir = "Your Document Directory";

// Initialiser une instance d'AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Étape 2 : Reconnaître l'image

Ensuite, reconnaissez le texte d'une image à l'aide d'Aspose.OCR. Voici un extrait illustrant ce processus :

```csharp
// Reconnaître l'image
RecognitionResult result = api.RecognizeImage(dataDir + "sample_bad.png", new RecognitionSettings(Language.Eng));
```

## Étape 3 : avant la correction

Récupérez le résultat OCR avant correction pour comparer avec la version corrigée.

```csharp
// Obtenir le résultat
Console.WriteLine("BEFORE CORRECTION:\n" + result.RecognitionText);
```

## Étape 4 : Après correction

Appliquez la vérification orthographique pour obtenir le résultat corrigé. L'extrait de code suivant illustre cette étape :

```csharp
// Obtenez un résultat corrigé
string correctedResult = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng);
Console.WriteLine("AFTER CORRECTION:\n" + correctedResult);
```

## Étape 5 : Mots mal orthographiés et suggestions

Obtenez une liste de mots mal orthographiés ainsi que des suggestions de corrections en utilisant le code suivant :

```csharp
// Obtenez une liste de mots mal orthographiés avec des suggestions
List<SpellCheckError> errorsList = result.GetSpellCheckErrorList(SpellCheckLanguage.Eng);
foreach (var word in errorsList)
{
	Console.Write("Word:" + word.Word);
	Console.Write(" StartPosition:" + word.StartPosition);
	Console.WriteLine(" Length:" + word.Length);
	Console.WriteLine("SuggestedWords:");
	foreach (var suggest in word.SuggestedWords)
	{
		Console.Write(suggest.Word + " ");
	}
	Console.WriteLine();
}
```

## Étape 6 : Corriger le texte de l'utilisateur

Corrigez le texte spécifique fourni par l'utilisateur à l'aide de la bibliothèque Aspose.OCR :

```csharp
// Corriger le texte utilisateur
Console.WriteLine("recogniition -> " + api.CorrectSpelling("recogniition"));
```

## Étape 7 : Correction avec le dictionnaire utilisateur

Améliorez encore la correction en incorporant un dictionnaire utilisateur personnalisé :

```csharp
// Obtenez le résultat corrigé avec le dictionnaire utilisateur
string correctedResultUserDict = result.GetSpellCheckCorrectedText(SpellCheckLanguage.Eng, dataDir+"dictionary.txt");
Console.WriteLine("AFTER CORRECTION WITH USER DICTIONARY:\n" + correctedResultUserDict);
```

## Conclusion

Toutes nos félicitations! Vous avez parcouru avec succès les fonctionnalités de vérification orthographique d’Aspose.OCR pour .NET. Cette fonctionnalité vous permet d'affiner les résultats OCR, garantissant l'exactitude et éliminant les erreurs.

## FAQ

### Q1 : Puis-je utiliser Aspose.OCR pour des langues autres que l’anglais ?

A1 : Oui, Aspose.OCR prend en charge plusieurs langues. Ajustez les paramètres de langue en conséquence.

### Q2 : Comment intégrer Aspose.OCR dans mon projet .NET ?

 A2 : Reportez-vous au[Documentation](https://reference.aspose.com/ocr/net/) pour les étapes d’intégration détaillées.

### Q3 : Existe-t-il une version d’essai disponible pour Aspose.OCR ?

 A3 : Oui, vous pouvez explorer les fonctionnalités avec le[version d'essai gratuite](https://releases.aspose.com/).

### Q4 : Puis-je télécharger un dictionnaire personnalisé pour la vérification orthographique ?

A4 : Absolument ! Le didacticiel montre comment améliorer la correction à l'aide d'un dictionnaire fourni par l'utilisateur.

### Q5 : Où puis-je demander de l'aide pour Aspose.OCR ?

 A5 : Visitez le[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour le soutien et les conseils de la communauté.