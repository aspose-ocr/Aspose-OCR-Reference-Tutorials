---
title: Enregistrer le résultat multipage en tant que document dans la reconnaissance d'image OCR
linktitle: Enregistrer le résultat multipage en tant que document dans la reconnaissance d'image OCR
second_title: API Aspose.OCR .NET
description: Libérez le potentiel d’Aspose.OCR pour .NET. Enregistrez sans effort les résultats OCR de plusieurs pages sous forme de documents grâce à ce guide complet étape par étape.
type: docs
weight: 14
url: /fr/net/ocr-optimization/save-multipage-result-as-document/
---
## Introduction

Bienvenue dans le monde fascinant de la reconnaissance optique de caractères (OCR) utilisant Aspose.OCR pour .NET ! Dans ce didacticiel, nous explorerons comment exploiter les capacités d'Aspose.OCR pour enregistrer les résultats OCR multipages sous forme de documents. Que vous soyez un développeur chevronné ou que vous débutiez tout juste avec l'OCR, ce guide vous guidera à travers chaque étape, vous assurant de tirer le meilleur parti de cet outil puissant.

## Conditions préalables

Avant de plonger dans le didacticiel, assurons-nous que tout est configuré :

1.  Installez Aspose.OCR pour .NET : commencez par télécharger et installer Aspose.OCR pour .NET. Vous pouvez trouver les fichiers nécessaires[ici](https://releases.aspose.com/ocr/net/).

2.  Obtenez votre essai gratuit ou votre licence : si vous ne l'avez pas déjà fait, vous pouvez obtenir un essai gratuit[ici](https://releases.aspose.com/) ou acheter une licence[ici](https://purchase.aspose.com/buy).

3.  Explorez la Documentation : Familiarisez-vous avec le[documentation](https://reference.aspose.com/ocr/net/)pour Aspose.OCR pour .NET. C'est votre ressource incontournable pour obtenir des informations détaillées.

4.  Accédez aux forums d'assistance : si vous rencontrez des problèmes ou avez des questions, le[forums d'assistance](https://forum.aspose.com/c/ocr/16) constituent une ressource communautaire précieuse.

Maintenant que vous êtes prêt, passons au guide étape par étape.

## Importer des espaces de noms

Commencez votre projet en important les espaces de noms nécessaires :

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

## Étape 1 : définissez votre répertoire de documents

```csharp
// Le chemin d'accès au répertoire des documents.
string dataDir = "Your Document Directory";
```

 Assurez-vous de remplacer`"Your Document Directory"` avec le chemin réel vers votre répertoire de documents.

## Étape 2 : initialiser Aspose.OCR

```csharp
// Initialiser une instance d'AsposeOcr
AsposeOcr api = new AsposeOcr();
```

 Créer une instance de`AsposeOcr` pour accéder aux fonctionnalités OCR.

## Étape 3 : Reconnaître les images

```csharp
// Reconnaître l'image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

Utilisez Aspose.OCR pour reconnaître le texte de plusieurs images. Ajustez les chemins de fichiers en fonction de vos fichiers image.

## Étape 4 : Enregistrez les résultats dans les formats préférés

```csharp
// Enregistrez le résultat dans votre format préféré
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Choisissez le format souhaité (Docx, Texte, Pdf ou Xlsx) et enregistrez les résultats OCR sous forme de document de plusieurs pages.

## Conclusion

Toutes nos félicitations! Vous avez appris avec succès comment enregistrer les résultats OCR multipages sous forme de documents à l'aide d'Aspose.OCR pour .NET. Cet outil polyvalent ouvre un monde de possibilités pour la reconnaissance de texte dans vos projets.

## FAQ

### Q1 : Une licence temporaire est-elle disponible à des fins de test ?

 A1 : Oui, vous pouvez obtenir une licence temporaire[ici](https://purchase.aspose.com/temporary-license/) pour tester Aspose.OCR.

### Q2 : Puis-je reconnaître le texte d’images dans différents formats ?

A2 : Absolument ! Aspose.OCR prend en charge différents formats d'image, garantissant ainsi la flexibilité de vos tâches OCR.

### Q3 : Existe-t-il des limites quant au nombre d'images à reconnaître ?

A3 : Le nombre d'images que vous pouvez traiter dépend de votre licence. Consultez la documentation pour plus de détails.

### Q4 : Comment puis-je gérer les erreurs lors de la reconnaissance OCR ?

A4 : Reportez-vous à la documentation pour connaître les meilleures pratiques de gestion des erreurs ou demandez de l'aide sur les forums d'assistance.

### Q5 : Aspose.OCR prend-il en charge des langues autres que l’anglais ?

A5 : Oui, Aspose.OCR prend en charge plusieurs langues. Explorez la documentation pour plus de détails sur la prise en charge linguistique.