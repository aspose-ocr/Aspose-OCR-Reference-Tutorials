---
title: OCROOpération avec sélection de langue dans la reconnaissance d'images OCR
linktitle: OCROOpération avec sélection de langue dans la reconnaissance d'images OCR
second_title: API Aspose.OCR .NET
description: Débloquez de puissantes capacités OCR avec Aspose.OCR pour .NET. Extrayez le texte des images de manière transparente.
type: docs
weight: 12
url: /fr/net/ocr-configuration/ocr-operation-with-language-selection/
---
## Introduction

Dans le monde de la reconnaissance d'images et de la reconnaissance optique de caractères (OCR), Aspose.OCR for .NET s'impose comme un outil puissant pour les développeurs recherchant une extraction de texte précise et efficace à partir d'images. Ce guide étape par étape vous guidera à travers le processus de reconnaissance d'image OCR à l'aide d'Aspose.OCR pour .NET, en se concentrant sur l'opération de sélection de la langue.

## Conditions préalables

Avant de plonger dans le didacticiel, assurez-vous que les conditions préalables suivantes sont remplies :

-  Aspose.OCR pour .NET : assurez-vous que la bibliothèque Aspose.OCR est installée. Vous pouvez le télécharger depuis le[Page de téléchargement d'Aspose.OCR pour .NET](https://releases.aspose.com/ocr/net/).

- Environnement de développement : Mettre en place un environnement de travail avec une application .NET. Si vous ne l'avez pas encore fait, reportez-vous au[Documentation](https://reference.aspose.com/ocr/net/) pour des instructions détaillées.

## Importer des espaces de noms

Dans votre application .NET, commencez par importer les espaces de noms nécessaires :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Étape 1 : initialiser Aspose.OCR

Commencez par initialiser une instance de la classe Aspose.OCR. Cela ouvre la voie à l’utilisation des capacités OCR au sein de votre application.

```csharp
// ExDébut : 1
// Le chemin d'accès au répertoire des documents.
string dataDir = "Your Document Directory";

// Initialiser une instance d'AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Étape 2 : Spécifier le chemin de l'image

Ensuite, définissez le chemin d'accès à l'image sur laquelle vous souhaitez effectuer l'OCR. Assurez-vous que l’image est accessible depuis votre application.

```csharp
//Chemin de l'image
string fullPath = dataDir + "sample.png";
```

## Étape 3 : Reconnaître l'image avec la sélection de la langue

Vient maintenant l’opération de base de l’OCR. Utilisez la bibliothèque Aspose.OCR pour reconnaître le texte de l'image spécifiée. Ajustez les paramètres de reconnaissance, y compris la sélection de la langue.

```csharp
// Reconnaître l'image
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choisissez la langue : none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

## Étape 4 : Imprimer et afficher les résultats

Après l'opération OCR, imprimez et affichez les résultats, y compris le texte reconnu, les zones, les avertissements et la représentation JSON.

```csharp
// Résultat d'impression
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExFin : 1
```

## Conclusion

Toutes nos félicitations! Vous avez réussi à effectuer une reconnaissance d'image OCR avec sélection de langue à l'aide d'Aspose.OCR pour .NET. Ce didacticiel a démontré les étapes essentielles pour extraire du texte à partir d'images et a mis en évidence la flexibilité des options linguistiques.

## FAQ

### Q1 : Aspose.OCR est-il adapté à la reconnaissance de texte multilingue ?

A1 : Oui, Aspose.OCR prend en charge plusieurs langues, offrant ainsi une flexibilité pour les tâches OCR multilingues.

### Q2 : Puis-je affiner les paramètres OCR pour des caractéristiques d’image spécifiques ?

A2 : Absolument ! Ajustez les paramètres tels que l'angle d'inclinaison, la reconnaissance de ligne et la détection de zone pour optimiser l'OCR pour différents scénarios.

### Q3 : Où puis-je trouver une assistance supplémentaire ou des discussions communautaires ?

 A3 : Visitez le[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour du soutien et des discussions avec la communauté.

### Q4 : Existe-t-il un essai gratuit ?

 A4 : Oui, explorez le[essai gratuit](https://releases.aspose.com/) pour découvrir les capacités d’Aspose.OCR.

### Q5 : Comment puis-je acheter Aspose.OCR pour .NET ?

 A5 : Pour acheter, visitez le[page d'achat](https://purchase.aspose.com/buy).
