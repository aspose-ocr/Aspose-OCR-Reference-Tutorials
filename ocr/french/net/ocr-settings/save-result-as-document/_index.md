---
title: Enregistrer le résultat en tant que document dans la reconnaissance d'image OCR
linktitle: Enregistrer le résultat en tant que document dans la reconnaissance d'image OCR
second_title: API Aspose.OCR .NET
description: Libérez le potentiel d’Aspose.OCR pour .NET. Reconnaissez facilement le texte des images et enregistrez les résultats dans différents formats de documents.
weight: 10
url: /fr/net/ocr-settings/save-result-as-document/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enregistrer le résultat en tant que document dans la reconnaissance d'image OCR

## Introduction

Bienvenue dans le monde passionnant de la reconnaissance optique de caractères (OCR) avec Aspose.OCR pour .NET ! Dans ce didacticiel complet, nous approfondirons les subtilités de l'utilisation d'Aspose.OCR pour reconnaître le texte dans les images et montrerons comment enregistrer les résultats sous différents formats de document.

## Conditions préalables

Avant de nous lancer dans ce voyage OCR, assurez-vous d'avoir les conditions préalables suivantes en place :

-  Aspose.OCR pour .NET. Assurez-vous que la bibliothèque Aspose.OCR est installée. Vous pouvez le télécharger[ici](https://releases.aspose.com/ocr/net/).

-  Répertoire de documents : disposez d'un répertoire désigné pour vos documents et mettez à jour le`dataDir` variable dans le code fourni en conséquence.

## Importer des espaces de noms

Commencez par importer les espaces de noms nécessaires. Ce sont les éléments de base qui donneront à votre code des capacités OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Maintenant, décomposons l'exemple en plusieurs étapes :

## Étape 1 : initialiser Aspose.OCR

```csharp
// Le chemin d'accès au répertoire des documents.
string dataDir = "Your Document Directory";

// Initialiser une instance d'AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Cette étape prépare le terrain en initialisant l'API Aspose.OCR.

## Étape 2 : Reconnaître l'image

```csharp
// Reconnaître l'image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Ici, nous utilisons Aspose.OCR pour reconnaître le texte dans l'image spécifiée (remplacez "sample.png" par votre fichier image).

## Étape 3 : Enregistrer le résultat dans différents formats

```csharp
// Enregistrez le résultat dans votre format préféré
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Personnalisez cette étape en fonction de vos besoins. Aspose.OCR vous permet d'enregistrer le texte reconnu dans divers formats de documents tels que DOCX, TXT, PDF et XLSX.

## Étape 4 : Afficher le message de réussite

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Un simple message de confirmation pour vous informer que le processus s'est déroulé sans accroc.

En suivant ces étapes, vous avez réussi à exploiter la puissance d'Aspose.OCR pour .NET pour reconnaître le texte dans les images et enregistrer les résultats dans différents formats de document.

## Conclusion

En conclusion, Aspose.OCR pour .NET ouvre un monde de possibilités pour la reconnaissance de texte dans les images. Que vous extrayiez des données ou créiez des documents consultables, Aspose.OCR simplifie le processus grâce à son API intuitive.

## FAQ

### T1. Aspose.OCR est-il compatible avec différents formats d’image ?

A1 : Oui, Aspose.OCR prend en charge une large gamme de formats d'image, garantissant ainsi la flexibilité de vos tâches OCR.

### Q2 : Puis-je personnaliser les paramètres de reconnaissance pour une meilleure précision ?

A2 : Absolument ! Aspose.OCR fournit des paramètres de reconnaissance pour affiner le processus OCR en fonction de vos besoins spécifiques.

### Q3 : Existe-t-il un essai gratuit disponible ?

 A3 : Oui, vous pouvez commencer avec un essai gratuit[ici](https://releases.aspose.com/).

### Q4 : Comment puis-je obtenir des licences temporaires pour Aspose.OCR ?

 A4 : Des licences temporaires peuvent être obtenues[ici](https://purchase.aspose.com/temporary-license/).

### Q5 : Où puis-je demander de l'aide ou me connecter avec la communauté ?

 A5 : Rejoignez la communauté Aspose.OCR sur[Forum Aspose](https://forum.aspose.com/c/ocr/16) pour du soutien et des discussions.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
