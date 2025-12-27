---
date: 2025-12-27
description: Apprenez à utiliser Aspose.OCR pour .NET afin d'extraire du texte d'une
  image, de reconnaître le texte dans les images et de convertir une image en PDF
  .NET dans divers formats de documents.
linktitle: Save Result as Document in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Convertir une image en PDF .NET – Enregistrer le résultat en tant que document
  dans la reconnaissance d’images OCR
url: /fr/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir une image en PDF .NET – Enregistrer le résultat en tant que document dans la reconnaissance d'image OCR

## Introduction

Bienvenue dans le monde passionnant de la reconnaissance optique de caractères (OCR) avec Aspose.OCR pour .NET ! Dans ce tutoriel, vous apprendrez comment **convertir une image en PDF .NET**, extraire du texte d’une image, et enregistrer la sortie OCR dans des formats de documents recherchables tels que PDF, DOCX, TXT et Excel. Que vous ayez besoin de créer un PDF recherchable ou d’exporter les résultats OCR vers Excel, les étapes ci‑dessous vous guideront rapidement et efficacement.

## Quick Answers
- **Que signifie « image to pdf .net » ?** Il s’agit de convertir des fichiers image en documents PDF à l’aide de bibliothèques .NET, ici Aspose.OCR.  
- **Quels formats puis‑je exporter les résultats OCR ?** DOCX, TXT, PDF et XLSX sont pris en charge nativement.  
- **Ai‑je besoin d’une licence pour une utilisation en production ?** Oui, une licence commerciale est requise pour la production ; un essai gratuit est disponible pour l’évaluation.  
- **Puis‑je extraire du texte recherchable du PDF ?** Absolument – le PDF généré est un **ocr to searchable pdf** que vous pouvez indexer.  
- **Quelles versions de .NET sont prises en charge ?** Aspose.OCR fonctionne avec .NET Framework 4.5+, .NET Core 3.1+, et .NET 5/6+.  

## Qu’est‑ce que « image to pdf .net » ?
« Image to PDF .NET » désigne le processus consistant à prendre des images raster (PNG, JPEG, TIFF, etc.) et à les transformer programmatiquement en fichiers PDF à l’aide d’une bibliothèque .NET. Aspose.OCR ne se contente pas de convertir l’image ; il effectue également l’OCR, vous permettant de **reconnaître le texte dans les images** et d’intégrer ce texte dans le PDF résultant, le rendant ainsi recherchable.

## Pourquoi utiliser Aspose.OCR pour cette tâche ?
- **Haute précision** – moteur OCR avancé qui gère de multiples langues et polices.  
- **Conversion en une étape** – vous pouvez à la fois reconnaître le texte et l’enregistrer directement en PDF, DOCX, TXT ou Excel sans post‑traitement supplémentaire.  
- **Aucune dépendance externe** – bibliothèque pure .NET, aucune binaire native requise.  
- **Flexibilité** – changez facilement le format de sortie pour créer un document à partir de l’OCR ou exporter l’OCR vers Excel pour l’analyse de données.

## Prérequis

Avant de commencer ce voyage OCR, assurez‑vous d’avoir les prérequis suivants :

- Aspose.OCR pour .NET. Assurez‑vous que la bibliothèque Aspose.OCR est installée. Vous pouvez la télécharger [ici](https://releases.aspose.com/ocr/net/).

- Répertoire de documents : disposez d’un répertoire dédié à vos documents et mettez à jour la variable `dataDir` dans le code fourni en conséquence.

## Import Namespaces

Commencez par importer les espaces de noms nécessaires. Ce sont les blocs de construction qui donneront à votre code les capacités OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

Maintenant, décomposons l’exemple en plusieurs étapes :

## How to Convert Image to PDF .NET Using Aspose.OCR

### Step 1: Initialize Aspose.OCR

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

Cette étape prépare le terrain en initialisant l’API Aspose.OCR.

### Step 2: Recognize Image

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

Ici, nous utilisons Aspose.OCR pour **reconnaître le texte dans l’image spécifiée** (remplacez `"sample.png"` par votre fichier image). C’est à ce moment que l’opération **extract text from image** s’exécute.

### Step 3: Save Result in Different Formats

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

Personnalisez cette étape selon vos besoins. Aspose.OCR vous permet de **enregistrer le texte reconnu dans divers formats de documents tels que DOCX, TXT, PDF et XLSX**, créant ainsi **un document from OCR** ou **exporting OCR to Excel**.

### Step 4: Display Success Message

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

Un simple message de confirmation pour vous indiquer que le processus s’est terminé sans accroc.

En suivant ces étapes, vous avez exploité avec succès la puissance d’Aspose.OCR pour .NET afin de reconnaître le texte dans les images et d’enregistrer les résultats dans différents formats de documents, y compris un **ocr to searchable pdf**.

## Common Issues and Solutions
- **Image non reconnue** – Assurez‑vous que l’image possède une résolution suffisante (au moins 300 dpi) et qu’elle est dans un format pris en charge (PNG, JPEG, TIFF).  
- **Détection de langue incorrecte** – Passez un objet `RecognitionSettings` avec la propriété `Language` appropriée (par ex., `Language = Language.English`).  
- **Fichier de sortie non créé** – Vérifiez que `dataDir` pointe vers un dossier valide et accessible en écriture et que les noms de fichiers sont uniques.

## Frequently Asked Questions

**Q : Aspose.OCR est‑il compatible avec différents formats d’image ?**  
R : Oui, Aspose.OCR prend en charge un large éventail de formats d’image, assurant une flexibilité dans vos tâches OCR.

**Q : Puis‑je personnaliser les paramètres de reconnaissance pour une meilleure précision ?**  
R : Absolument ! Aspose.OCR fournit des paramètres de reconnaissance pour affiner le processus OCR selon vos exigences spécifiques.

**Q : Existe‑t‑il un essai gratuit disponible ?**  
R : Oui, vous pouvez commencer avec un essai gratuit [ici](https://releases.aspose.com/).

**Q : Comment obtenir des licences temporaires pour Aspose.OCR ?**  
R : Les licences temporaires peuvent être obtenues [ici](https://purchase.aspose.com/temporary-license/).

**Q : Où puis‑je obtenir de l’aide ou rejoindre la communauté ?**  
R : Rejoignez la communauté Aspose.OCR sur le [Aspose Forum](https://forum.aspose.com/c/ocr/16) pour le support et les discussions.

## Conclusion

En conclusion, Aspose.OCR pour .NET ouvre un monde de possibilités pour les conversions **image to pdf .net**, l’extraction de texte et la génération de documents. Que vous extrayiez des données, créiez des PDF recherchables ou exportiez les résultats OCR vers Excel, Aspose.OCR simplifie le processus grâce à son API intuitive et son ensemble de fonctionnalités robuste.

---

**Last Updated:** 2025-12-27  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}