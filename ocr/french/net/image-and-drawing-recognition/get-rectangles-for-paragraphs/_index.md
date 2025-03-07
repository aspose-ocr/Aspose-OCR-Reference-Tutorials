---
title: Obtenez des rectangles pour les paragraphes dans la reconnaissance d'images OCR
linktitle: Obtenez des rectangles pour les paragraphes dans la reconnaissance d'images OCR
second_title: API Aspose.OCR .NET
description: Débloquez des fonctionnalités OCR avancées avec Aspose.OCR pour .NET. Extrayez les rectangles de paragraphe sans effort.
weight: 11
url: /fr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenez des rectangles pour les paragraphes dans la reconnaissance d'images OCR

## Introduction

Bienvenue dans notre guide complet sur l'utilisation d'Aspose.OCR pour .NET pour extraire des rectangles de paragraphe dans la reconnaissance d'images OCR. Si vous souhaitez améliorer vos capacités de traitement de documents et exploiter la puissance de la reconnaissance optique de caractères (OCR) dans vos applications .NET, vous êtes au bon endroit.

## Conditions préalables

Avant de plonger dans le didacticiel, assurez-vous que les conditions préalables suivantes sont remplies :

- Connaissance de base du développement C# et .NET.
-  Un environnement de développement mis en place avec Aspose.OCR pour .NET. Si ce n'est pas déjà fait, vous pouvez le télécharger[ici](https://releases.aspose.com/ocr/net/).
- Une compréhension des concepts de traitement d'image et de l'importance de l'OCR dans l'extraction de texte à partir d'images.

## Importer des espaces de noms

Dans votre code C#, assurez-vous d'avoir importé les espaces de noms nécessaires pour utiliser Aspose.OCR efficacement. Incluez les éléments suivants en haut de votre fichier :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Étape 1 : Configurez votre répertoire de documents

Commencez par initialiser le chemin d'accès à votre répertoire de documents où sont stockées les images à traiter OCR :

```csharp
string dataDir = "Your Document Directory";
```

## Étape 2 : initialiser l'instance AsposeOcr

Créez une instance de la classe AsposeOcr pour accéder aux fonctionnalités OCR :

```csharp
AsposeOcr api = new AsposeOcr();
```

## Étape 3 : Spécifiez le chemin de l'image

Définissez le chemin complet vers l'image que vous souhaitez traiter :

```csharp
string fullPath = dataDir + "sample.png";
```

## Étape 4 : Reconnaître l'image et obtenir des rectangles de paragraphe

 Invoquer le`GetRectangles` méthode pour obtenir des rectangles pour les paragraphes dans l’image OCR. Ensemble`detect_areas` à`true` si vous souhaitez extraire des paragraphes :

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Étape 5 : Imprimer les résultats

Imprimez les coordonnées des zones identifiées :

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Étape 6 : Conclusion

Toutes nos félicitations! Vous avez exécuté avec succès le processus de reconnaissance d'image OCR pour obtenir des rectangles pour les paragraphes à l'aide d'Aspose.OCR pour .NET.

## Conclusion

Dans ce didacticiel, nous avons exploré les étapes fondamentales pour intégrer Aspose.OCR for .NET dans vos applications, vous permettant d'extraire des rectangles de paragraphe à partir d'images traitées par OCR. Aspose.OCR simplifie la mise en œuvre de l'OCR, ce qui en fait un outil précieux pour le traitement de documents et l'extraction de texte.

## FAQ

### Q1 : Aspose.OCR est-il compatible avec différents formats d’image ?

R1 : Oui, Aspose.OCR prend en charge divers formats d'image, notamment PNG, JPEG et TIFF.

### Q2 : Puis-je utiliser Aspose.OCR pour le traitement par lots de plusieurs images ?

A2 : Absolument ! Aspose.OCR facilite le traitement par lots pour gérer plusieurs images de manière transparente.

### Q3 : Existe-t-il un essai gratuit disponible pour Aspose.OCR pour .NET ?

 A3 : Oui, vous pouvez explorer un essai gratuit[ici](https://releases.aspose.com/).

### Q4 : Comment puis-je obtenir une licence temporaire pour Aspose.OCR ?

 A4 : Vous pouvez acquérir une licence temporaire[ici](https://purchase.aspose.com/temporary-license/).

### Q5 : Où puis-je trouver une assistance supplémentaire et des discussions liées à Aspose.OCR ?

 A5 : Rendez-vous au[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour le soutien et les discussions de la communauté.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
