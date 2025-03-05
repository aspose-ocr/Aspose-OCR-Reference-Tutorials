---
title: Effectuer une OCR sur une image à partir d'une URL dans la reconnaissance d'image OCR
linktitle: Effectuer une OCR sur une image à partir d'une URL dans la reconnaissance d'image OCR
second_title: API Aspose.OCR .NET
description: Explorez l'intégration transparente de l'OCR avec Aspose.OCR pour .NET. Reconnaissez le texte des images avec précision.
type: docs
weight: 10
url: /fr/net/ocr-optimization/perform-ocr-on-image-from-url/
---
## Introduction

Dans le domaine de la reconnaissance optique de caractères (OCR), Aspose.OCR pour .NET se distingue comme un outil puissant qui permet aux développeurs d'extraire le contenu textuel des images avec précision. Si vous souhaitez intégrer les fonctionnalités OCR dans votre application .NET et effectuer une reconnaissance de texte sans effort, ce guide étape par étape vous guidera tout au long du processus d'exécution de l'OCR sur une image à partir d'une URL.

## Conditions préalables

Avant de vous plonger dans le didacticiel, assurez-vous que les conditions préalables suivantes sont remplies :

-  Aspose.OCR pour .NET : assurez-vous que la bibliothèque Aspose.OCR est intégrée à votre projet .NET. Vous pouvez le télécharger depuis le[page de sortie](https://releases.aspose.com/ocr/net/).

- Environnement de développement : disposez d'un environnement de développement .NET fonctionnel configuré sur votre machine.

## Importer des espaces de noms

Dans votre projet .NET, incluez les espaces de noms nécessaires pour accéder aux fonctionnalités Aspose.OCR. Ajoutez l'extrait de code suivant à votre projet :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Étape 1 : Configurez votre répertoire de documents

 Commencez par spécifier le répertoire dans lequel vos documents sont stockés. Remplacer`"Your Document Directory"` avec le chemin réel vers vos documents.

```csharp
string dataDir = "Your Document Directory";
```

## Étape 2 : Obtenez l’image pour la reconnaissance

Fournissez l'URL de l'image sur laquelle vous souhaitez effectuer une OCR. Assurez-vous que l’image est accessible au public.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4" ;
```

## Étape 3 : initialiser AsposeOcr

Créez une instance de la classe AsposeOcr pour accéder aux fonctionnalités OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

## Étape 4 : Reconnaître l'image

Utilisez la bibliothèque Aspose.OCR pour reconnaître le texte de l'URL de l'image spécifiée. Ajustez les paramètres de reconnaissance en fonction de vos besoins.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

## Étape 5 : Imprimer le résultat

Affichez le résultat de la reconnaissance, y compris le texte reconnu, les zones et les éventuels avertissements.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

## Étape 6 : Exécuter et vérifier

Exécutez votre application et si tout est correctement configuré, vous devriez voir le processus OCR exécuté avec succès.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Conclusion

Avec Aspose.OCR pour .NET, l'intégration des fonctionnalités OCR dans vos applications .NET devient une expérience transparente. Ce didacticiel vous a guidé tout au long du processus d'exécution de l'OCR sur une image à partir d'une URL, vous fournissant ainsi une base pour exploiter la puissance de la reconnaissance de texte dans vos projets.

## FAQ

### Q1 : Aspose.OCR est-il adapté à la gestion de plusieurs langues ?

A1 : Oui, Aspose.OCR prend en charge la reconnaissance de texte dans différentes langues, ce qui le rend polyvalent pour les applications internationales.

### Q2 : Puis-je utiliser Aspose.OCR pour la reconnaissance de texte sur une seule ligne et sur plusieurs lignes ?

A2 : Absolument ! Aspose.OCR offre une flexibilité pour reconnaître du texte sur une seule ligne et sur plusieurs lignes, en s'adaptant à votre cas d'utilisation spécifique.

### Q3 : Existe-t-il des options de licence disponibles pour Aspose.OCR ?

 A3 : Oui, vous pouvez explorer les options de licence et effectuer des achats sur le[Magasin Aspose](https://purchase.aspose.com/buy).

### Q4 : Existe-t-il un essai gratuit disponible pour Aspose.OCR ?

 A4 : Oui, vous pouvez essayer Aspose.OCR gratuitement en visitant le[page des versions](https://releases.aspose.com/).

### Q5 : Où puis-je trouver de l'aide ou des discussions communautaires liées à Aspose.OCR ?

 A5 : Visitez le[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour le soutien et l’engagement avec la communauté.