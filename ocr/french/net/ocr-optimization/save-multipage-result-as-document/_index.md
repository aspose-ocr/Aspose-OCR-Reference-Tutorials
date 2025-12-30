---
date: 2025-12-30
description: Apprenez à convertir des images en PDF C# en utilisant Aspose.OCR, à
  enregistrer les résultats OCR multipages en tant que documents, et à extraire du
  texte à partir d’images C#.
linktitle: Convert Images to PDF C# – Save Multipage OCR Result
second_title: Aspose.OCR .NET API
title: Convertir des images en PDF C# – Enregistrer le résultat OCR multipage
url: /fr/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir des images en PDF C# – Enregistrer le résultat OCR multipage

## Introduction

Dans ce tutoriel, vous découvrirez comment **convertir des images en PDF C#** avec Aspose.OCR pour .NET et enregistrer la sortie OCR multipage résultante sous forme de document. Que vous ayez besoin de **convertir des images numérisées en PDF** pour l’archivage ou d’**extraire du texte à partir d’images C#** pour le traitement de données, ce guide vous accompagne à chaque étape — avec des exemples concrets et des conseils de bonnes pratiques.

## Réponses rapides
- **Que couvre ce tutoriel ?** Conversion de plusieurs images en PDF/Docx/Txt/Pdf/Xlsx à l’aide d’Aspose.OCR en C#.
- **Quels formats sont pris en charge ?** Docx, Text, Pdf et Xlsx (vous pouvez également générer directement du PDF).
- **Ai‑je besoin d’une licence ?** Une’essai gratuite suffit pour l’évaluation ; une licence permanente est requise en production.
- **Quelles versions de .NET sont compatibles ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
- **Puis‑je extraire du texte lors de la conversion ?** Oui — utilisez les résultats OCR pour récupérer le texte avant l’enregistrement.

## Qu’est‑ce que le “convert images to PDF C#” ?

Convertir des images en PDF en C# signifie prendre de façon programmatique un ou plusieurs fichiers bitmap (PNG, JPEG, TIFF, etc.) et générer un document PDF qui conserve la mise en page visuelle tout en intégrant éventuellement du texte recherchable via OCR. Aspose.OCR rend ce processus simple et hautement personnalisable.

## Pourquoi utiliser Aspose.OCR pour cette tâche ?

- **Moteur OCR haute précision** qui fonctionne avec de nombreuses langues.
- **Prise en charge multipage** — traitement de lots d’images en un seul appel.
- **Enregistrement direct** vers les formats bureautiques populaires sans étapes de conversion supplémentaires.
- **Intégration complète à .NET** — pas de dépendances natives ni d’outils externes.

## Prérequis

Avant de commencer, assurez‑vous d’avoir les éléments suivants :

1. Installez Aspose.OCR pour .NET. Vous pouvez le télécharger [ici](https://releases.aspose.com/ocr/net/).
2. Obtenez une licence d’essai gratuite ou une licence achetée — procurez‑vous un essai [ici](https://releases.aspose.com/) ou achetez‑en une [ici](https://purchase.aspose.com/buy).
3. Consultez la [documentation officielle](https://reference.aspose.com/ocr/net/) pour vous familiariser avec l’API.
4. Rejoignez la communauté sur les [forums de support](https://forum.aspose.com/c/ocr/16) pour obtenir de l’aide en cas d’obstacle.

Tout est prêt, passons au codage.

## Importer les espaces de noms

Ajoutez les espaces de noms requis à votre fichier C# :

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

Ces importations vous donnent accès aux collections, à la gestion de fichiers, à LINQ et aux classes Aspose OCR.

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

Créer un objet `AsposeOcr` vous donne accès à toutes les opérations OCR, y compris le flux de travail **convert images to PDF C#**.

## Étape 3 : Reconnaître les images

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

La méthode `RecognizeMultipleImages` traite chaque fichier de la liste et renvoie une collection de `RecognitionResult`. Vous pouvez fournir n’importe quel nombre d’images, ce qui est idéal pour les scénarios de **convert scanned images to PDF**.

## Étape 4 : Enregistrer les résultats dans les formats souhaités

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

Choisissez le format qui correspond le mieux à votre chaîne de traitement :

- **Docx** — document Word éditable avec texte recherchable.
- **Text** — extraction de texte brut pour une analyse rapide des données (**extract text from images C#**).
- **Pdf** — sortie PDF classique, idéale pour l’archivage.
- **Xlsx** — représentation sous feuille de calcul pour les données tabulaires.

## Cas d’utilisation courants

- **Archivage numérique :** Convertir des contrats papier numérisés en PDFs recherchables.
- **Automatisation de la saisie de données :** Extraire le texte des reçus ou factures et le transférer dans une base de données.
- **Traitement par lots :** Gérer des milliers d’images en un seul job avec un code minimal.

## Dépannage & conseils

- **Ensembles d’images volumineux :** Traitez les images par petits lots pour éviter les pics de mémoire.
- **Qualité d’image :** Assurez‑vous que les images sont d’au moins 300 dpi pour une précision OCR optimale.
- **Erreurs de licence :** Vérifiez que votre fichier de licence est correctement chargé avant d’appeler les méthodes OCR.

## Questions fréquentes (Original)

### Q1 : Une licence temporaire est‑elle disponible pour les tests ?

R1 : Oui, vous pouvez obtenir une licence temporaire [ici](https://purchase.aspose.com/temporary-license/) pour tester Aspose.OCR.

### Q2 : Puis‑je reconnaître du texte à partir d’images dans différents formats ?

R2 : Absolument ! Aspose.OCR prend en charge divers formats d’image, garantissant une grande flexibilité pour vos tâches OCR.

### Q3 : Existe‑t‑il des limites au nombre d’images à reconnaître ?

R3 : Le nombre d’images que vous pouvez traiter dépend de votre licence. Consultez la documentation pour plus de détails.

### Q4 : Comment gérer les erreurs lors de la reconnaissance OCR ?

R4 : Référez‑vous à la documentation pour les meilleures pratiques de gestion des erreurs ou demandez de l’aide sur les forums de support.

### Q5 : Aspose.OCR prend‑il en charge des langues autres que l’anglais ?

R5 : Oui, Aspose.OCR supporte plusieurs langues. Explorez la documentation pour les détails sur les langues prises en charge.

## Questions fréquentes supplémentaires

**Q : Puis‑je convertir des images en PDF C# sans utiliser l’OCR ?**  
R : Oui, vous pouvez utiliser Aspose.PDF ou d’autres bibliothèques pour une conversion pure image‑vers‑PDF, mais l’OCR ajoute du texte recherchable.

**Q : Comment extraire du texte à partir d’images C# après la conversion ?**  
R : La liste `result` renvoyée par `RecognizeMultipleImages` contient des propriétés `Text` que vous pouvez écrire dans un fichier `.txt` ou traiter directement.

**Q : Est‑il possible de définir des marges de page ou une orientation personnalisées ?**  
R : Lors de l’enregistrement en PDF ou Docx, vous pouvez modifier la mise en page du document via les API Aspose.Words ou Aspose.PDF avant d’appeler `SaveMultipageDocument`.

**Q : Que se passe‑t‑il si une image ne peut pas être lue ?**  
R : Le moteur OCR renvoie un `RecognitionResult` vide pour cette page ; vous pouvez vérifier `result[i].Text` pour détecter les chaînes nulles ou vides et gérer le cas en conséquence.

**Q : L’API supporte‑t‑elle le déploiement cloud ?**  
R : Oui, la bibliothèque fonctionne sur n’importe quel runtime .NET, y compris Azure Functions et AWS Lambda, tant que la version du runtime satisfait aux exigences.

---

**Dernière mise à jour :** 2025-12-30  
**Testé avec :** Aspose.OCR 24.11 pour .NET  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}