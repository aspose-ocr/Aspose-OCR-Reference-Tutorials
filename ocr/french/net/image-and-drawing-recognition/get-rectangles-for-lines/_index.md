---
date: 2026-02-22
description: Apprenez comment réaliser une analyse de mise en page OCR en reconnaissant
  les lignes de texte dans une image et en extrayant les rectangles de lignes à l'aide
  d'Aspose.OCR pour .NET.
linktitle: Layout Analysis OCR – Get Line Rectangles from Images
second_title: Aspose.OCR .NET API
title: Analyse de mise en page OCR – Obtenir les rectangles de lignes à partir d'images
url: /fr/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Analyse de mise en page OCR – Obtenir les rectangles de lignes à partir d'images

## Introduction

Dans ce tutoriel, vous découvrirez **comment obtenir les rectangles de lignes OCR** avec Aspose.OCR pour .NET. À la fin du guide, vous serez capable de **reconnaître les lignes de texte dans une image** et **d'extraire les coordonnées des lignes** pour chaque ligne détectée—idéal pour le traitement en aval tel que **l'analyse de mise en page OCR**, l'extraction de données ou le rendu personnalisé.

## Quick Answers
- **Que signifie « obtenir les rectangles de lignes OCR » ?** Cela renvoie les boîtes englobantes de chaque ligne de texte détectée dans une image.  
- **Quelle méthode API est utilisée ?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Ai‑je besoin d’une licence ?** Une version d’essai gratuite suffit pour le développement ; une licence commerciale est requise pour la production.  
- **Formats d’image pris en charge ?** PNG, JPEG, BMP, TIFF, et plus.  
- **Puis‑je l’exécuter sur .NET Core ?** Oui, Aspose.OCR prend pleinement en charge .NET Core et .NET 5/6.

## Prérequis

Avant de plonger dans le tutoriel, assurez‑vous d’avoir les prérequis suivants :

- Connaissances de base en C# et développement .NET.  
- Un environnement de développement intégré (IDE) tel que Visual Studio.  
- Bibliothèque Aspose.OCR pour .NET installée. Vous pouvez la télécharger [ici](https://releases.aspose.com/ocr/net/).  
- Une image d’exemple contenant du texte pour la reconnaissance OCR.

## Import Namespaces

Assurez‑vous d’avoir les espaces de noms nécessaires importés dans votre projet. Ajoutez les lignes suivantes en haut de votre fichier C# :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Passons maintenant à la décomposition du processus d’obtention des rectangles de lignes dans la reconnaissance d’image OCR, étape par étape.

## layout analysis ocr – Guide étape par étape

### Step 1: Set Up Your Document Directory

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Remplacez `"Your Document Directory"` par le chemin réel du dossier qui contient votre image d’exemple.

### Step 2: Initialize Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Créez une instance de la classe `AsposeOcr` pour accéder aux fonctionnalités OCR.

### Step 3: Specify Image Path

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Définissez le chemin complet de l’image sur laquelle vous souhaitez effectuer l’OCR.

### Step 4: Recognize Image and Get Rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

La méthode `GetRectangles` renvoie une liste d’objets `Rectangle`, chacun représentant les coordonnées d’une ligne de texte détectée. C’est le cœur de **l’obtention des rectangles de lignes OCR** et cela permet **l’analyse de mise en page OCR**.

### Step 5: Print Result

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Affichez les coordonnées des zones détectées dans la console. Vous verrez des valeurs que vous pourrez ensuite utiliser pour **extraire les coordonnées des lignes** lors d’un traitement personnalisé.

## Why Use Aspose.OCR for Line Rectangles?

- **Haute précision** – Des algorithmes avancés détectent les lignes même dans des images bruyantes ou inclinées.  
- **Cross‑platform** – Fonctionne sur .NET Framework, .NET Core et .NET 5/6.  
- **Aucune dépendance externe** – Bibliothèque pure .NET, aucune DLL native à déployer.  
- **Sortie riche** – En plus des rectangles de lignes, vous pouvez également récupérer les mots, caractères et scores de confiance.

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| **No rectangles returned** | Assurez‑vous que l’image contient du texte clair et horizontal et que `AreasType.LINES` est spécifié. |
| **Incorrect coordinates** | Vérifiez le DPI de l’image ; les images basse résolution peuvent entraîner des limites inexactes. |
| **Performance bottleneck on large images** | Redimensionnez l’image à une résolution raisonnable avant d’appeler `GetRectangles`. |
| **License exception** | Utilisez une licence d’essai pour les tests ; appliquez une licence complète pour la production afin d’éviter les limites d’évaluation. |

## Frequently Asked Questions

**Q : Puis‑je extraire des mots individuels au lieu de lignes complètes ?**  
R : Oui, utilisez `AreasType.WORDS` avec la même méthode `GetRectangles` pour obtenir des boîtes englobantes au niveau des mots.

**Q : L’API prend‑elle en charge les PDF multi‑pages ?**  
R : Convertissez chaque page PDF en image d’abord, puis appelez `GetRectangles` sur chaque image.

**Q : Comment gérer le texte tourné ?**  
R : Activez l’option de rotation automatique dans les paramètres OCR ou pré‑tournez l’image avant le traitement.

**Q : Existe‑t‑il un moyen d’obtenir les scores de confiance pour chaque ligne ?**  
R : Après avoir obtenu les rectangles, appelez `api.RecognizeImage(...).Lines` pour accéder aux objets ligne incluant les valeurs de confiance.

**Q : Quelles versions de .NET sont compatibles ?**  
R : La bibliothèque fonctionne avec .NET Framework 4.5+, .NET Core 3.1+, et .NET 5/6.

## Real‑World Use Cases

- **Document layout analysis OCR** – Alimentez les rectangles de lignes dans un moteur de mise en page pour reconstruire les structures de colonnes.  
- **Automated data extraction** – Utilisez les coordonnées pour découper les lignes individuelles dans des pipelines NLP en aval.  
- **Custom rendering** – Superposez les boîtes englobantes sur l’image originale pour une vérification visuelle ou des superpositions UI.  

## Conclusion

Félicitations ! Vous avez réussi à **obtenir les rectangles de lignes OCR** pour une image en utilisant Aspose.OCR pour .NET. Avec les boîtes englobantes en main, vous pouvez désormais injecter les coordonnées des lignes dans des flux de travail en aval tels que le rendu personnalisé, l’extraction de données ou **l’analyse de mise en page OCR**.

---

**Last Updated:** 2026-02-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}