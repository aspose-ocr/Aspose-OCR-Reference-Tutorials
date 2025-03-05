---
title: Préparer des rectangles dans la reconnaissance d'images OCR
linktitle: Préparer des rectangles dans la reconnaissance d'images OCR
second_title: API Aspose.OCR .NET
description: Libérez le potentiel d’Aspose.OCR pour .NET avec notre guide complet. Apprenez étape par étape comment préparer des rectangles pour la reconnaissance d'images. Améliorez vos applications .NET grâce à une intégration OCR transparente.
type: docs
weight: 11
url: /fr/net/ocr-optimization/prepare-rectangles/
---
## Introduction

Dans le paysage technologique en constante évolution, la reconnaissance optique de caractères (OCR) joue un rôle central dans la transformation des images en texte lisible par machine. Aspose.OCR for .NET se distingue comme une solution robuste pour les développeurs recherchant une intégration transparente des fonctionnalités OCR dans leurs applications .NET. Dans ce guide complet, nous explorerons le processus de préparation de rectangles dans la reconnaissance d'images OCR à l'aide d'Aspose.OCR pour .NET.

## Conditions préalables

Avant de plonger dans le didacticiel, assurez-vous que les conditions préalables suivantes sont remplies :

- Une connaissance pratique du développement .NET.
-  Aspose.OCR pour la bibliothèque .NET installée. Vous pouvez le télécharger[ici](https://releases.aspose.com/ocr/net/).
- Une compréhension de base des concepts de reconnaissance d'images.

## Importer des espaces de noms

Commençons par importer les espaces de noms nécessaires pour lancer notre parcours OCR :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Étape 1 : Configurez votre répertoire de documents

 Commencez par spécifier le répertoire dans lequel vos documents sont stockés. Remplacer`"Your Document Directory"` avec le chemin réel vers vos documents.

```csharp
// Le chemin d'accès au répertoire des documents.
string dataDir = "Your Document Directory";

// Initialiser une instance d'AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Étape 2 : Reconnaître l'image avec plusieurs rectangles

Dans cette étape, nous montrerons comment reconnaître le texte d'une image à l'aide de plusieurs rectangles. Suivez ces sous-étapes :

### 2.1 Définir des rectangles

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### 2.2 Effectuer la reconnaissance OCR

```csharp
// premier cas
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Afficher le texte reconnu
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Étape 3 : Reconnaître l'image avec les paramètres de reconnaissance

Dans cette étape, nous présenterons une méthode alternative utilisant RecognitionSettings pour la reconnaissance d'images :

### 3.1 Définir les paramètres de reconnaissance

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### 3.2 Afficher le texte reconnu

```csharp
// Afficher le texte reconnu
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Conclusion

Toutes nos félicitations! Vous avez réussi le processus de préparation des rectangles dans la reconnaissance d'images OCR à l'aide d'Aspose.OCR pour .NET. Ce guide vous permet d'intégrer l'OCR de manière transparente dans vos applications .NET, améliorant ainsi leurs capacités de reconnaissance de texte.

### FAQ

### Q1 : Puis-je utiliser Aspose.OCR pour .NET avec d’autres frameworks .NET ?

A1 : Oui, Aspose.OCR pour .NET est compatible avec divers frameworks .NET.

### Q2 : Existe-t-il un essai gratuit disponible pour Aspose.OCR pour .NET ?

 A2 : Absolument ! Vous pouvez accéder à l'essai gratuit[ici](https://releases.aspose.com/).

### Q3 : Comment puis-je obtenir du support pour Aspose.OCR pour .NET ?

 A3 : Visitez le[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour un soutien dédié.

### Q4 : Puis-je obtenir une licence temporaire à des fins de test ?

 A4 : Oui, vous pouvez acquérir une licence temporaire[ici](https://purchase.aspose.com/temporary-license/).

### Q5 : Où puis-je trouver la documentation d'Aspose.OCR pour .NET ?

 A5 : La documentation est disponible[ici](https://reference.aspose.com/ocr/net/).