---
date: 2026-02-25
description: Apprenez à extraire le texte d’une image en C# avec Aspose.OCR pour .NET.
  Ce guide étape par étape présente la reconnaissance optique de caractères multilingue,
  la sélection de la langue et des conseils pratiques.
linktitle: Extract image text C# with language selection using Aspose.OCR
second_title: Aspose.OCR .NET API
title: Extraction du texte d'une image en C# avec sélection de langue à l'aide d'Aspose.OCR
url: /fr/net/ocr-configuration/ocr-operation-with-language-selection/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'image C# avec sélection de langue utilisant Aspose.OCR

## Introduction

Si vous devez **extraire du texte d'image C#** à partir de photos et de PDF dans une application .NET, Aspose.OCR pour .NET offre une solution rapide, précise et sensible à la langue. Dans ce tutoriel, nous parcourrons un exemple concret qui démontre la reconnaissance d'image OCR avec sélection de langue, afin que vous puissiez extraire du texte multilingue d'images en quelques lignes de code seulement. À la fin, vous verrez à quel point il est facile d'intégrer l'OCR dans vos projets C# et pourquoi cette approche est un choix solide pour les charges de travail en production.

## Réponses rapides
- **Que fait Aspose.OCR ?** Il reconnaît le texte imprimé et manuscrit dans les images et renvoie le texte extrait.  
- **Puis‑je choisir la langue ?** Oui – vous pouvez spécifier n'importe quelle langue prise en charge telle que l'anglais, l'allemand, l'espagnol, le chinois, etc.  
- **Ai‑je besoin d'une licence pour le développement ?** Un essai gratuit suffit pour l'évaluation ; une licence est requise pour une utilisation en production.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **La correction d’inclinaison est‑elle automatique ?** Vous pouvez activer `AutoSkew` et affiner le paramètre `SkewAngle`.  

## Qu’est‑ce que « extract image text C# » ?

Extraire du texte d'image en C# signifie utiliser une bibliothèque pour lire le contenu visuel d'une image (PNG, JPEG, TIFF, etc.) et le convertir en texte consultable et modifiable. Aspose.OCR fournit cette capacité localement, sans envoyer les données à des services externes, ce qui maintient votre flux de travail sécurisé et conforme.

## Pourquoi choisir Aspose.OCR pour les tâches OCR ?

- **Haute précision** sur de multiples polices et qualités d'image.  
- **Sélection de langue intégrée** élimine le besoin de packs de langues externes.  
- **API simple** qui s'intègre proprement aux projets C# existants, rendant la **extraction du texte d'image C#** directe.  
- **Aucune dépendance externe** – tout fonctionne localement, gardant vos données sécurisées.  

## Prérequis

Avant de plonger dans le code, assurez‑vous d'avoir les prérequis suivants :

- Aspose.OCR pour .NET : assurez‑vous que la bibliothèque Aspose.OCR est installée. Vous pouvez la télécharger depuis la [page de téléchargement Aspose.OCR pour .NET](https://releases.aspose.com/ocr/net/).

- Environnement de développement : configurez un environnement de travail avec une application .NET. Si vous ne l'avez pas encore fait, consultez la [documentation](https://reference.aspose.com/ocr/net/) pour des instructions détaillées.

## Importer les espaces de noms

Dans votre application .NET, commencez par importer les espaces de noms nécessaires :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Étape 1 : Initialiser Aspose.OCR

Commencez par initialiser une instance de la classe Aspose.OCR. Cela prépare l'utilisation des capacités OCR dans votre application.

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Étape 2 : Spécifier le chemin de l'image

Ensuite, définissez le chemin vers l'image sur laquelle vous souhaitez effectuer l'OCR. Assurez‑vous que l'image est accessible depuis votre application.

```csharp
// Image Path
string fullPath = dataDir + "sample.png";
```

## Étape 3 : Reconnaître l'image avec sélection de langue

Voici l'opération OCR principale. Utilisez la bibliothèque Aspose.OCR pour reconnaître le texte de l'image spécifiée. Ajustez les paramètres de reconnaissance, y compris la sélection de langue, pour affiner le processus **d'extraction du texte d'image C#**.

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

## Étape 4 : Imprimer et afficher les résultats

Après l'opération OCR, imprimez et affichez les résultats, incluant le texte reconnu, les zones, les avertissements et la représentation JSON.

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

## Problèmes courants et conseils

- **Sélection de langue incorrecte** – Si la sortie apparaît illisible, revérifiez que la propriété `Language` correspond à la langue de l'image source.  
- **Images inclinées** – Activez `AutoSkew` ou ajustez manuellement `SkewAngle` pour une meilleure précision sur les scans inclinés.  
- **Fichiers volumineux** – Traitez les grandes images par morceaux ou réduisez la résolution avant de les passer à `RecognizeImage` afin de conserver la mémoire.  

## Questions fréquemment posées

**Q : Aspose.OCR est‑il adapté à la reconnaissance de texte multilingue ?**  
R : Oui, Aspose.OCR prend en charge diverses langues, offrant une flexibilité pour les tâches OCR multilingues.

**Q : Puis‑je affiner les paramètres OCR pour des caractéristiques d'image spécifiques ?**  
R : Absolument ! Ajustez des paramètres comme l'angle d'inclinaison, la reconnaissance de lignes et la détection de zones pour optimiser l'OCR selon différents scénarios.

**Q : Où puis‑je trouver un support supplémentaire ou des discussions communautaires ?**  
R : Visitez le [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour le support et les discussions avec la communauté.

**Q : Existe‑t‑il un essai gratuit ?**  
R : Oui, explorez l’[essai gratuit](https://releases.aspose.com/) pour découvrir les capacités d’Aspose.OCR.

**Q : Comment puis‑je acheter Aspose.OCR pour .NET ?**  
R : Pour acheter, rendez‑vous sur la [page d'achat](https://purchase.aspose.com/buy).

## Conclusion

Félicitations ! Vous avez appris **comment extraire du texte d'image C#** avec sélection de langue en utilisant Aspose.OCR pour .NET. Ce tutoriel vous a montré comment configurer le moteur OCR, sélectionner la langue appropriée et gérer les résultats, vous offrant une base solide pour créer des fonctionnalités d'extraction de texte multilingue dans vos applications.

---

**Dernière mise à jour :** 2026-02-25  
**Testé avec :** Aspose.OCR 24.11 pour .NET  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}