---
description: Apprenez à enregistrer les résultats OCR avec Aspose.OCR pour .NET –
  convertissez une image en PDF, extrayez le texte d’un PNG et sauvegardez le texte
  reconnu au format DOCX, TXT, PDF ou XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: Comment enregistrer le résultat OCR en tant que document
url: /fr/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment enregistrer le résultat OCR en document

## Introduction

Dans ce tutoriel, vous découvrirez **comment enregistrer la sortie OCR** à l’aide d’Aspose.OCR pour .NET. Nous parcourrons la reconnaissance de texte dans une image, puis la conversion de ce texte en formats de documents populaires tels que DOCX, TXT, PDF et XLSX. À la fin, vous pourrez automatiser l’extraction de données à partir d’images et les stocker sous forme de fichiers recherchables et modifiables—parfait pour l’archivage, les rapports ou le traitement en aval.

## Réponses rapides
- **Que signifie « how to save ocr » ?** Cela fait référence à la persistance du texte reconnu à partir d’une image dans un format de fichier comme DOCX, PDF, etc.  
- **Vers quels formats puis‑je exporter ?** DOCX, TXT, PDF et XLSX sont pris en charge nativement.  
- **Ai‑je besoin d’une licence ?** Une version d’essai gratuite suffit pour l’évaluation ; une licence commerciale est requise pour une utilisation en production.  
- **Puis‑je convertir directement une image en PDF ?** Oui—enregistrez le résultat OCR au format PDF pour obtenir un document PDF recherchable.  
- **Le PNG est‑il supporté ?** Absolument ; vous pouvez **extraire du texte à partir d’images PNG** avec la même API.

## Qu’est‑ce que l’OCR et pourquoi enregistrer les résultats en documents ?

La Reconnaissance Optique de Caractères (OCR) transforme le texte imprimé ou manuscrit présent dans les images en chaînes lisibles par machine. Enregistrer ces chaînes sous forme de documents vous permet de :

* Créer des PDF recherchables pour la conformité.  
* Alimenter des feuilles de calcul (XLSX) pour l’analyse de données.  
* Générer des rapports modifiables (DOCX).  
* Archiver des journaux en texte brut (TXT) pour une recherche rapide.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- Aspose.OCR pour .NET installé. Vous pouvez le télécharger **[ici](https://releases.aspose.com/ocr/net/)**.  
- Un dossier sur votre machine qui contiendra les images sources et les documents de sortie. Mettez à jour la variable `dataDir` dans le code pour qu’elle pointe vers ce dossier.

## Importer les espaces de noms

Nous avons besoin de quelques espaces de noms .NET pour accéder aux I/O de fichiers et aux classes Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Étape 1 : Initialiser Aspose.OCR

Définissez le chemin vers votre répertoire de travail et créez une instance du moteur OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Étape 2 : Reconnaître l’image

Passez le fichier image (par ex., un PNG) au reconnaisseur. C’est ici que nous **reconnaissons les images de texte** et les transformons en un `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Étape 3 : Enregistrer le résultat dans différents formats

Nous exportons maintenant le texte reconnu. Choisissez le format qui correspond à votre flux de travail—que vous ayez besoin de **convertir une image en PDF**, **d’extraire du texte à partir d’un PNG**, ou de générer une feuille de calcul.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Étape 4 : Afficher le message de succès

Un simple message console confirme que le processus s’est terminé sans erreur.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Pièges courants & astuces

- **Chemins de fichiers :** Utilisez toujours des chemins absolus ou assurez‑vous que `dataDir` se termine par un séparateur de chemin (`\` ou `/`).  
- **Qualité de l’image :** Des images à plus haute résolution améliorent la précision ; envisagez un pré‑traitement (redressement, débruitage) pour de meilleurs résultats.  
- **Mode licence :** En mode évaluation, la sortie peut contenir un filigrane ; appliquez une licence valide pour le supprimer.

## Questions fréquentes

**Q1. Aspose.OCR est‑il compatible avec différents formats d’image ?**  
R1 : Oui, Aspose.OCR prend en charge un large éventail de formats d’image, assurant une flexibilité dans vos tâches OCR.

**Q2 : Puis‑je personnaliser les paramètres de reconnaissance pour une meilleure précision ?**  
R2 : Absolument ! Aspose.OCR fournit `RecognitionSettings` pour affiner le processus OCR selon vos exigences spécifiques.

**Q3 : Existe‑t‑il un essai gratuit ?**  
R3 : Oui, vous pouvez commencer avec un essai gratuit **[ici](https://releases.aspose.com/)**.

**Q4 : Comment obtenir une licence temporaire pour Aspose.OCR ?**  
R4 : Les licences temporaires sont disponibles **[ici](https://purchase.aspose.com/temporary-license/)**.

**Q5 : Où puis‑je obtenir de l’aide ou rejoindre la communauté ?**  
R5 : Rejoignez la communauté Aspose.OCR sur **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** pour le support et les discussions.

---

**Dernière mise à jour :** 2026-02-12  
**Testé avec :** Aspose.OCR 24.11 pour .NET  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}