---
date: 2025-12-21
description: Apprenez à effectuer la reconnaissance optique de caractères (OCR) et
  à extraire du texte à partir d’une image avec Aspose.OCR pour .NET. Ce guide étape
  par étape montre la reconnaissance de texte multilingue et la sélection de la langue.
linktitle: How to Perform OCR with Language Selection in Aspose.OCR
second_title: Aspose.OCR .NET API
title: Comment effectuer la reconnaissance optique de caractères avec sélection de
  langue dans Aspose.OCR
url: /fr/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer l'OCR avec sélection de langue dans Aspose.OCR

## Introduction

Si vous devez **commenter effectuer l'OCR** ​​sur des images et extraire du texte à partir de fichiers image dans une application .NET, Aspose.OCR pour .NET fournit une solution rapide, précise et sensible au langage. Dans ce didacticiel, nous présenterons un exemple réel illustrant la reconnaissance d'images OCR avec sélection de langue, afin que vous puissiez extraire du texte multilingue à partir d'images avec seulement quelques lignes de code.

## Réponses rapides
- **Que fait Aspose.OCR ?** Il reconnaît le texte imprimé et manuscrit dans les images et renvoie le texte extrait.
- **Puis-je choisir la langue ?** Oui – vous pouvez préciser n'importe quelle langue prise en charge telle que l'anglais, l'allemand, l'espagnol, le chinois, etc.
- **Ai-je besoin d'une licence pour le développement ?** Un essai gratuit suffit pour l'évaluation ; une licence est requise pour la mise en production.
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.
- **La correction d'inclinaison est‑elle automatique ?** Vous pouvez activer `AutoSkew` et ajuster finement le paramètre `SkewAngle`.

## Pourquoi choisir Aspose.OCR pour les tâches OCR ?

- **Haute précision** sur de nombreuses politiques et qualités d'image.
- **Sélection de langue intégrée** élimine le besoin de packs de langues externes.
- **API simple** qui s'intègre proprement aux projets C# existants.
- **Aucune dépendance externe** – tout fonctionne localement, garantissant la sécurité de vos données.

## Prérequis

Avant de Sous-marin dans le code, assurez-vous d'avoir les prérequis suivants en place :

- Aspose.OCR for .NET : assurez-vous d'avoir la bibliothèque Aspose.OCR installée. Vous pouvez la télécharger depuis la [page de téléchargement Aspose.OCR pour .NET](https://releases.aspose.com/ocr/net/).

- Environnement de développement : configurez un environnement de travail avec une application .NET. Si vous ne l'avez pas encore fait, consultez la [documentation](https://reference.aspose.com/ocr/net/) pour des instructions détaillées.

## Importer des espaces de noms

Dans votre application .NET, commencez par importer les espaces de noms nécessaires :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

### Étape 1 : Initialiser Aspose.OCR

Commencez par initialiser une instance de la classe Aspose.OCR. Cela prépare le terrain pour exploiter les capacités d'OCR dans votre application.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Étape 2 : Spécifier le chemin de l'image

Ensuite, définissez le chemin de l'image sur laquelle vous souhaitez effectuer l'OCR. Assurez‑vous que l'image est accessible depuis votre application.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

### Étape 3 : Reconnaître l'image avec sélection de langue

Voici maintenant l'opération principale d'OCR. Utilisez la bibliothèque Aspose.OCR pour reconnaître le texte de l'image spécifiée. Ajustez les paramètres de reconnaissance, y compris la sélection de la langue.

```csharp
// Recognize image           
RecognitionResult result = api.RecognizeImage(fullPath, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    SkewAngle = 0.2F,
    Language = Language.Eng, // Choose the language: none, eng, deu, por, spa, fra, ita, cze, dan, dum, est, fin, lav, lit, nor, pol, rum, srp_hrv, slk, slv, swe, chi
});
```

### Étape 4 : Imprimer et afficher les résultats

Après l'opération d'OCR, imprimez et affichez les résultats, incluant le texte reconnu, les zones, les avertissements et la représentation JSON.

```csharp
// Print result
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
// ExEnd:1
```

### Problèmes courants et astuces

- **Sélection de langue incorrecte** – Si la sortie apparaît illisible, vérifiez que la propriété `Langue` correspond à la langue de l'image source.
- **Images inclinées** – Activez `AutoSkew` ou ajustez manuellement `SkewAngle` pour une meilleure précision sur les scans inclinés.
- **Fichiers volumineux** – Traitez les grandes images par morceaux ou réduisez la résolution avant de les passer à `RecognizeImage` afin de conserver la mémoire.

## Conclusion

Félicitations ! Vous avez appris **comment effectuer l'OCR** ​​avec sélection de langue en utilisant Aspose.OCR pour .NET. Ce tutoriel vous a montré comment extraire du texte à partir de fichiers image, personnaliser les paramètres de reconnaissance et gérer le contenu multilingue sans effort.

## FAQ

### Q1 : Aspose.OCR est-il adapté à la reconnaissance de texte multilingue ?

**R1:** Oui, Aspose.OCR prend en charge plusieurs langues, offrant une flexibilité pour les tâches d'OCR multilingues.

### Q2 : Puis‑je affiner les paramètres d'OCR pour des caractéristiques d'image spécifiques ?

**R2 :** Absolument ! Ajustez les paramètres tels que l'angle d'inclinaison, la reconnaissance de lignes et la détection de zones pour optimiser l'OCR selon différents scénarios.

### Q3 : Où puis‑je trouver un support supplémentaire ou des discussions communautaires ?

**R3 :** Consultez le [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour obtenir du support et participer aux discussions avec la communauté.

### Q4 : Un essai gratuit est-il disponible ?

**R4:** Oui, explorez l'[essai gratuit](https://releases.aspose.com/) pour découvrir les capacités d'Aspose.OCR.

### Q5 : Comment puis-je acheter Aspose.OCR pour .NET ?

**R5:** Pour acheter, consultez la [page d'achat](https://purchase.aspose.com/buy).

---

**Dernière mise à jour :** 2025-12-21
**Testé avec :** Aspose.OCR 24.11 pour .NET
**Auteur :** Aspose 

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}