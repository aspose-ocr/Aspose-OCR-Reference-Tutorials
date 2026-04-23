---
date: 2026-04-23
description: Apprenez à convertir des images en PDF C# à l'aide d'Aspose.OCR, à enregistrer
  les résultats OCR multipages en tant que documents et à extraire le texte des images.
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: Convertir des images en PDF C# – Enregistrer le résultat OCR multipage
second_title: Aspose.OCR .NET API
title: Extraire le texte des images – Convertir les images en PDF C#
url: /fr/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte à partir d'images – Convertir des images en PDF C#

## Introduction

Dans ce tutoriel, vous découvrirez comment **extraire du texte à partir d'images** tout en **convertissant des images en PDF C#** à l'aide d'Aspose.OCR pour .NET, puis enregistrer le résultat OCR multipage sous forme de document. Que vous ayez besoin de **batch image to pdf** pour l'archivage, de **convert scanned images pdf** pour la conformité, ou simplement d'extraire du texte consultable à partir d'images, nous parcourrons chaque étape avec des explications claires, des conseils pratiques et des recommandations de bonnes pratiques.

## Réponses rapides
- **Quel est le sujet de ce tutoriel ?** Conversion de plusieurs images en PDF/Docx/Txt/Xlsx et extraction de texte à partir d'images avec Aspose.OCR en C#.
- **Quels formats de sortie sont pris en charge ?** Docx, Text, Pdf, et Xlsx (vous pouvez également générer directement du PDF).
- **Ai-je besoin d'une licence ?** Un essai gratuit suffit pour l'évaluation ; une licence permanente est requise pour la production.
- **Quelles versions de .NET sont compatibles ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Puis-je extraire du texte lors de la conversion ?** Oui — utilisez les résultats OCR pour extraire le texte avant l'enregistrement.

## Qu'est-ce que « extraire du texte à partir d'images » et pourquoi le combiner avec la conversion PDF ?
Extraire du texte à partir d'images consiste à utiliser l'OCR (Reconnaissance Optique de Caractères) pour transformer les caractères visuels en chaînes consultables et modifiables. Lorsque vous **convertissez des images en PDF C#**, vous intégrez ces chaînes dans le PDF afin que le document devienne consultable et indexable — idéal pour l'archivage numérique et l'exploration de données.

## Pourquoi utiliser Aspose.OCR pour cette tâche ?
- **Haute précision** sur des dizaines de langues.  
- **Support multipage** – gérez des lots d'images en un seul appel (idéal pour les scénarios **batch image to pdf**).  
- **Enregistrement direct** vers les formats bureautiques populaires sans étapes de conversion supplémentaires.  
- **Intégration .NET complète** – aucune dépendance native, fonctionne sous Windows, Linux et les environnements cloud.

## Prérequis
1. Installez Aspose.OCR pour .NET. Vous pouvez le télécharger [ici](https://releases.aspose.com/ocr/net/).  
2. Obtenez un essai gratuit ou une licence achetée – obtenez un essai [ici](https://releases.aspose.com/) ou achetez-en un [ici](https://purchase.aspose.com/buy).  
3. Consultez la [documentation](https://reference.aspose.com/ocr/net/) officielle pour vous familiariser avec l'API.  
4. Rejoignez la communauté sur les [forums de support](https://forum.aspose.com/c/ocr/16) pour obtenir de l'aide en cas d'obstacle.  

Maintenant que tout est prêt, commençons à coder.

## Importer les espaces de noms

Commencez par ajouter les espaces de noms requis à votre fichier C# :

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Ces importations vous donnent accès aux collections, à la gestion des fichiers, à LINQ et aux classes Aspose OCR.

## Étape 1 : définir le répertoire de votre document

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Remplacez `"Your Document Directory"` par le chemin absolu ou relatif où se trouvent vos images sources et où vous souhaitez enregistrer les fichiers de sortie.

## Étape 2 : initialiser Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Créer un objet `AsposeOcr` vous donne accès à toutes les opérations OCR, y compris le flux de travail **convert images to PDF C#**.

## Étape 3 : reconnaître les images

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

La méthode `RecognizeMultipleImages` traite chaque fichier de la liste et renvoie une collection de `RecognitionResult`. Vous pouvez fournir n'importe quel nombre d'images, ce qui est parfait pour les scénarios **convert scanned images pdf**.

## Étape 4 : enregistrer les résultats dans les formats préférés

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Choisissez le format qui convient le mieux à votre flux de travail en aval :

- **Docx** – document Word modifiable avec texte consultable.  
- **Text** – extraction de texte brut pour une extraction rapide de données (**extract text from images**).  
- **Pdf** – la sortie PDF classique, idéale pour l'archivage.  
- **Xlsx** – représentation sous forme de feuille de calcul pour les données tabulaires.

## Cas d'utilisation courants
- **Archivage numérique :** Convertir des contrats papier numérisés en PDF consultables.  
- **Automatisation de la saisie de données :** Extraire le texte des reçus ou factures et l'alimenter dans une base de données.  
- **Traitement par lots :** Gérer des milliers d'images en une seule tâche avec un code minimal — parfait pour les besoins **batch image to pdf**.

## Dépannage et astuces
- **Ensembles d'images volumineux :** Traitez les images par lots plus petits pour éviter les pics de mémoire.  
- **Qualité d'image :** Assurez-vous que les images sont d'au moins 300 dpi pour une précision OCR optimale.  
- **Erreurs de licence :** Vérifiez que votre fichier de licence est correctement chargé avant d'appeler les méthodes OCR.  
- **Résultats vides :** Le moteur OCR renvoie un `RecognitionResult` vide pour les pages illisibles ; vérifiez `result[i].Text` pour des chaînes nulles ou vides et gérez en conséquence.

## Questions fréquemment posées
**Q : Puis-je convertir des images en PDF C# sans utiliser l'OCR ?**  
R : Oui, vous pouvez utiliser Aspose.PDF ou d'autres bibliothèques pour une conversion pure image‑vers‑PDF, mais l'OCR ajoute du texte consultable.

**Q : Comment extraire du texte à partir d'images C# après la conversion ?**  
R : La liste `result` renvoyée par `RecognizeMultipleImages` contient des propriétés `Text` que vous pouvez écrire dans un fichier `.txt` ou traiter directement.

**Q : Est-il possible de définir des marges de page ou une orientation personnalisées ?**  
R : Lors de l'enregistrement en PDF ou Docx, vous pouvez modifier la mise en page du document via les API Aspose.Words ou Aspose.PDF avant d'appeler `SaveMultipageDocument`.

**Q : Que se passe-t-il si une image ne peut pas être lue ?**  
R : Le moteur OCR renvoie un `RecognitionResult` vide pour cette page ; vous pouvez vérifier `result[i].Text` pour des chaînes nulles ou vides et gérer en conséquence.

**Q : L'API prend‑elle en charge le déploiement cloud ?**  
R : Oui, la bibliothèque fonctionne sur n'importe quel runtime .NET, y compris Azure Functions et AWS Lambda, tant que le runtime répond aux exigences de version.

---

**Dernière mise à jour :** 2026-04-23  
**Testé avec :** Aspose.OCR 24.11 pour .NET  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}