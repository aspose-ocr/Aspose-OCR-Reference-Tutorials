---
date: 2026-06-29
description: Apprenez à enregistrer les résultats OCR avec Aspose.OCR pour .NET –
  un guide pas à pas sur la façon d’enregistrer la sortie OCR, de convertir une image
  en searchable pdf, d’extraire le texte d’un PNG et d’exporter vers DOCX, TXT, PDF
  ou XLSX.
keywords:
- how to save ocr
- image to searchable pdf
- extract text from png
- create searchable pdf
- ocr result to txt
linktitle: Comment enregistrer le résultat OCR en document
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  headline: How to Save OCR Result as Document
  type: TechArticle
- description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  name: How to Save OCR Result as Document
  steps:
  - name: Initialize Aspose.OCR
    text: AsposeOcr is the primary class that performs OCR operations. Set the path
      to your working directory and create an instance of the OCR engine.
  - name: Recognize Image
    text: RecognitionResult holds the text and layout information extracted from the
      image. Pass the image file (e.g., a PNG) to the recognizer. This is where we
      **recognize text images** and turn them into a `RecognitionResult`.
  - name: Save Result in Different Formats
    text: Now we export the recognized text. Choose the format that fits your workflow—whether
      you need to **convert image to searchable pdf**, **extract text from png**,
      or generate a spreadsheet.
  - name: Display Success Message
    text: A simple console message confirms that the process completed without errors.
  type: HowTo
- questions:
  - answer: It refers to persisting the text recognized from an image into a file
      format like DOCX, PDF, etc.
    question: What does “how to save ocr” mean?
  - answer: DOCX, TXT, PDF, and XLSX are supported out‑of‑the‑box.
    question: Which formats can I export to?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—save the OCR result as PDF to get a searchable PDF document.
    question: Can I convert image to PDF directly?
  - answer: Absolutely; you can **extract text from PNG** images with the same API.
    question: Is PNG supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: Comment enregistrer le résultat OCR en document
url: /fr/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment enregistrer le résultat OCR en tant que document

## Introduction

Dans ce tutoriel, vous découvrirez **comment enregistrer l'ocr** à l'aide d'Aspose.OCR pour .NET. Nous parcourrons la reconnaissance de texte dans une image, puis la conversion de ce texte en formats de documents populaires tels que DOCX, TXT, PDF et XLSX. À la fin, vous pourrez automatiser l'extraction de données à partir d'images et les stocker sous forme de fichiers consultables et modifiables—parfait pour l'archivage, le reporting ou le traitement en aval.

## Réponses rapides
- **Que signifie « how to save ocr » ?** Il s'agit de persister le texte reconnu à partir d'une image dans un format de fichier tel que DOCX, PDF, etc.  
- **Quels formats puis‑je exporter ?** DOCX, TXT, PDF et XLSX sont pris en charge immédiatement.  
- **Ai‑je besoin d'une licence ?** Un essai gratuit suffit pour l'évaluation ; une licence commerciale est requise pour une utilisation en production.  
- **Puis‑je convertir une image en PDF directement ?** Oui—enregistrez le résultat OCR au format PDF pour obtenir un document PDF consultable.  
- **Le format PNG est‑il pris en charge ?** Absolument ; vous pouvez **extraire du texte d'images PNG** avec la même API.

## Qu'est-ce que l'OCR et pourquoi enregistrer les résultats sous forme de documents ?

L'OCR (Optical Character Recognition) convertit le texte imprimé ou manuscrit présent dans les images en chaînes lisibles par machine. Enregistrer ces chaînes sous forme de documents vous permet de créer des **PDF consultables**, de remplir des feuilles de calcul, de générer des rapports modifiables ou d'archiver des journaux en texte brut. Aspose.OCR peut transformer une image numérisée en **PDF consultable** en une seule étape, éliminant le besoin d'outils de création de PDF séparés.

## Prérequis

Avant de commencer, assurez‑vous d'avoir :

- Aspose.OCR pour .NET installé. Vous pouvez le télécharger **[ici](https://releases.aspose.com/ocr/net/)**.  
- Un dossier sur votre machine qui contiendra les images sources et les documents de sortie. Mettez à jour la variable `dataDir` dans le code pour qu'elle pointe vers ce dossier.

## Importer les espaces de noms

Nous avons besoin de quelques espaces de noms .NET pour accéder aux I/O de fichiers et aux classes Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Étape 1 : Initialiser Aspose.OCR

AsposeOcr est la classe principale qui effectue les opérations OCR. Définissez le chemin vers votre répertoire de travail et créez une instance du moteur OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Étape 2 : Reconnaître l'image

RecognitionResult contient le texte et les informations de mise en page extraits de l'image. Passez le fichier image (par ex., un PNG) au reconnaisseur. C'est ici que nous **reconnaissons les images texte** et les transformons en un `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Étape 3 : Enregistrer le résultat dans différents formats

Nous exportons maintenant le texte reconnu. Choisissez le format qui correspond à votre flux de travail—que vous ayez besoin de **convertir une image en PDF consultable**, **extraire du texte d'un PNG**, ou de générer une feuille de calcul.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Étape 4 : Afficher le message de succès

Un simple message console confirme que le processus s'est terminé sans erreurs.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Pièges courants et conseils

- **Chemins de fichiers :** Utilisez toujours des chemins absolus ou assurez‑vous que `dataDir` se termine par un séparateur de chemin (`\` ou `/`).  
- **Qualité de l'image :** Des images à plus haute résolution améliorent la précision ; envisagez un prétraitement (redressement, débruitage) pour de meilleurs résultats.  
- **Mode licence :** En mode évaluation, la sortie peut contenir un filigrane ; appliquez une licence valide pour le supprimer.

## Questions fréquemment posées

**Q1. Aspose.OCR est‑il compatible avec différents formats d'image ?**  
R1 : Oui, Aspose.OCR prend en charge plus de 30 formats d'image—y compris PNG, JPEG, TIFF, BMP et GIF—offrant ainsi une grande flexibilité pour vos tâches OCR.

**Q2 : Puis‑je personnaliser les paramètres de reconnaissance pour une meilleure précision ?**  
R2 : Absolument ! Aspose.OCR fournit `RecognitionSettings` pour affiner le processus OCR selon vos exigences spécifiques.

**Q3 : Existe‑t‑il un essai gratuit disponible ?**  
R3 : Oui, vous pouvez commencer avec un essai gratuit **[ici](https://releases.aspose.com/)**.

**Q4 : Comment obtenir une licence temporaire pour Aspose.OCR ?**  
R4 : Les licences temporaires sont disponibles **[ici](https://purchase.aspose.com/temporary-license/)**.

**Q5 : Où puis‑je obtenir de l'aide ou rejoindre la communauté ?**  
R5 : Rejoignez la communauté Aspose.OCR sur **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** pour le support et les discussions.

---

**Dernière mise à jour :** 2026-06-29  
**Testé avec :** Aspose.OCR 24.11 pour .NET  
**Auteur :** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés

- [Extraire du texte d'une image avec Aspose.OCR .NET](/ocr/net/image-and-drawing-recognition/)
- [Convertir des images en PDF C# – Enregistrer le résultat OCR multipage](/ocr/net/ocr-optimization/save-multipage-result-as-document/)
- [Extraire du texte d'images – Paramètres OCR](/ocr/net/ocr-settings/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}