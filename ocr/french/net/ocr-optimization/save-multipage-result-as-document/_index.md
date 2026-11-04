---
date: 2026-04-29
description: Apprenez à convertir des images en PDF C# à l'aide d'Aspose.OCR, à enregistrer
  les résultats OCR multipages sous forme de documents, et à extraire du texte à partir
  d'images C#.
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: Convertir des images en PDF C# – Enregistrer le résultat OCR multipage
second_title: Aspose.OCR .NET API
title: Convertir les images en PDF C# – Enregistrer le résultat OCR multipage
url: /fr/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir des images en PDF C# – Enregistrer le résultat OCR multipage

## Introduction

Dans ce tutoriel, vous découvrirez comment **convertir des images en PDF C#** en utilisant la puissante bibliothèque **Aspose.OCR** pour .NET. Que vous ayez besoin de **convertir des fichiers TIFF numérisés en PDF recherchables**, d'extraire du texte d'images pour l'exploration de données, ou de générer un classeur Excel à partir d'un lot d'images, ce guide vous accompagne à chaque étape avec des explications claires, des conseils pratiques et des recommandations de bonnes pratiques.

## Réponses rapides
- **Quel est le sujet de ce tutoriel ?** Conversion de plusieurs images en PDF, Docx, Text et Xlsx en utilisant Aspose.OCR en C# et enregistrement du résultat OCR sous forme de document multipage.  
- **Quels formats de sortie sont pris en charge ?** Docx, Text, Pdf et Xlsx (vous pouvez également générer directement du PDF).  
- **Ai-je besoin d'une licence ?** Un essai gratuit suffit pour l'évaluation ; une licence permanente est requise pour la production.  
- **Quelles versions de .NET sont compatibles ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.  
- **Puis-je extraire du texte lors de la conversion ?** Oui — utilisez les résultats OCR pour extraire du texte recherchable avant l'enregistrement.  

## Qu’est‑ce que « convertir des images en PDF C# » ?

Convertir des images en PDF en C# signifie prendre programmétiquement un ou plusieurs fichiers bitmap (PNG, JPEG, TIFF, etc.) et générer un document PDF qui conserve la mise en page visuelle tout en intégrant éventuellement du texte recherchable via OCR. Aspose.OCR fournit une **bibliothèque OCR C#** qui gère l’ensemble du processus, y compris la prise en charge multipage et l’enregistrement direct dans les formats bureautiques populaires.

## Pourquoi utiliser Aspose.OCR pour cette tâche ?

- **OCR haute précision** qui prend en charge des dizaines de langues.  
- **Traitement multipage** – fournissez un dossier complet d'images et obtenez un seul PDF recherchable.  
- **Exportation directe** vers Docx, Text, Pdf et Xlsx sans étape de conversion supplémentaire.  
- **Pure .NET** – aucune dépendance native, fonctionne sous Windows, Linux et les environnements cloud.  

## Prérequis

1. Installez Aspose.OCR pour .NET. Vous pouvez le télécharger [ici](https://releases.aspose.com/ocr/net/).  
2. Obtenez un essai gratuit ou une licence achetée – obtenez un essai [ici](https://releases.aspose.com/) ou achetez‑en un [ici](https://purchase.aspose.com/buy).  
3. Consultez la [documentation officielle](https://reference.aspose.com/ocr/net/) pour vous familiariser avec l’API.  
4. Rejoignez la communauté sur les [forums de support](https://forum.aspose.com/c/ocr/16) pour obtenir de l’aide en cas d’obstacle.  

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

## Étape 1 : Définir votre répertoire de documents

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

Remplacez `"Your Document Directory"` par le chemin absolu ou relatif où se trouvent vos images sources et où vous souhaitez enregistrer les fichiers de sortie.

## Étape 2 : Initialiser Aspose.OCR

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Créer un objet `AsposeOcr` vous donne accès à toutes les opérations OCR, y compris le flux de travail **convertir des images en PDF C#**.

## Étape 3 : Reconnaître les images

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

La méthode `RecognizeMultipleImages` traite chaque fichier de la liste et renvoie une collection de `RecognitionResult`. Vous pouvez fournir n'importe quel nombre d'images, ce qui est parfait pour les scénarios de **conversion d'images numérisées en PDF**.

## Étape 4 : Enregistrer les résultats dans les formats souhaités

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Choisissez le format qui convient le mieux à votre flux de travail en aval :

- **Docx** – document Word éditable avec texte recherchable.  
- **Text** – extraction de texte brut pour une exploration de données rapide (**extraire du texte d'images**).  
- **Pdf** – le format PDF classique, idéal pour l'archivage.  
- **Xlsx** – représentation sous forme de feuille de calcul pour les données tabulaires (**convertir des images en xlsx**).

## Comment convertir des images en PDF C# – Récapitulatif étape par étape

1. **Préparez le dossier** contenant les images que vous souhaitez convertir.  
2. **Créez une instance `AsposeOcr`** pour accéder aux fonctions OCR.  
3. **Appelez `RecognizeMultipleImages`** pour obtenir les résultats OCR de chaque fichier.  
4. **Enregistrez le résultat multipage** en utilisant `SaveMultipageDocument` dans le format souhaité.

## Cas d’utilisation courants

- **Archivage numérique :** Convertir des contrats papier numérisés en PDF recherchables.  
- **Automatisation de la saisie de données :** Extraire le texte des reçus ou factures et l’alimenter dans une base de données.  
- **Traitement par lots :** Gérer des milliers d'images en une seule tâche avec un code minimal.  
- **Générer un PDF à partir de TIFF :** Idéal pour les documents numérisés haute résolution qui doivent rester fidèles à l'original.

## Dépannage et conseils

- **Ensembles d'images volumineux :** Traitez les images par lots plus petits pour éviter les pics de mémoire.  
- **Qualité de l'image :** Assurez‑vous que les images ont au moins 300 dpi pour une précision OCR optimale.  
- **Erreurs de licence :** Vérifiez que votre fichier de licence est correctement chargé avant d’appeler les méthodes OCR.  
- **Résultats vides :** Si une image ne peut pas être lue, le `RecognitionResult` correspondant aura une propriété `Text` vide — vérifiez les chaînes nulles ou vides avant l’enregistrement.  

## Questions fréquemment posées

**Q : Puis‑je convertir des images en PDF C# sans utiliser l’OCR ?**  
R : Oui, vous pouvez utiliser Aspose.PDF ou d’autres bibliothèques pour une conversion pure image‑vers‑PDF, mais l’OCR ajoute du texte recherchable qui rend le PDF beaucoup plus utile.

**Q : Comment extraire du texte d'images C# après la conversion ?**  
R : La liste `result` renvoyée par `RecognizeMultipleImages` contient une propriété `Text` pour chaque page. Vous pouvez écrire ces chaînes dans un fichier `.txt` ou les traiter directement dans votre application.

**Q : Est‑il possible de définir des marges ou une orientation de page personnalisées ?**  
R : Lors de l’enregistrement en PDF ou Docx, vous pouvez modifier la mise en page du document via les API Aspose.Words ou Aspose.PDF avant d’appeler `SaveMultipageDocument`.

**Q : Que se passe‑t‑il si une image ne peut pas être lue ?**  
R : Le moteur OCR renvoie un `RecognitionResult` vide pour cette page ; vous pouvez le détecter et ignorer ou consigner le fichier problématique.

**Q : L’API prend‑elle en charge le déploiement cloud ?**  
R : Oui, la bibliothèque fonctionne sur n’importe quel runtime .NET, y compris Azure Functions et AWS Lambda, tant que le runtime répond aux exigences de version.

## Conclusion

Vous disposez maintenant d’un flux de travail complet et prêt pour la production afin de **convertir des images en PDF C#**, d’extraire du texte recherchable, et même de générer des fichiers Word, texte brut ou Excel à partir d’un lot d’images. N’hésitez pas à expérimenter différents formats de sortie, à ajuster les paramètres OCR pour des langues spécifiques, ou à intégrer le code dans des pipelines de traitement de documents plus vastes.

---

**Dernière mise à jour :** 2026-04-29  
**Testé avec :** Aspose.OCR 24.11 for .NET  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}