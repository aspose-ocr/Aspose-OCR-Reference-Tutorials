---
date: 2025-12-17
description: Apprenez comment obtenir les rectangles de lignes OCR en utilisant Aspose.OCR
  pour .NET afin de reconnaître les lignes de texte dans les images et d'extraire
  facilement les coordonnées des lignes.
linktitle: Get OCR Line Rectangles for Image Text Lines
second_title: Aspose.OCR .NET API
title: Obtenir les rectangles de lignes OCR pour les lignes de texte d'image
url: /fr/net/image-and-drawing-recognition/get-rectangles-for-lines/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir les rectangles de lignes OCR pour les lignes de texte d'image

## Introduction

Dans ce tutoriel, vous découvrirez **comment obtenir les rectangles de lignes OCR** avec Aspose.OCR pour .NET. À la fin du guide, vous serez capable de **reconnaître les lignes de texte dans une image** et **d'extraire les coordonnées des lignes** pour chaque ligne détectée — parfait pour le traitement en aval tel que l'analyse de mise en page, l'extraction de données ou le rendu personnalisé.

## Réponses rapides
- **What does “get OCR line rectangles” mean?** It returns the bounding boxes of each text line detected in an image.  
- **Which API method is used?** `AsposeOcr.GetRectangles(..., AreasType.LINES, ...)`.  
- **Do I need a license?** A free trial works for development; a commercial license is required for production.  
- **Supported image formats?** PNG, JPEG, BMP, TIFF, and more.  
- **Can I run this on .NET Core?** Yes, Aspose.OCR fully supports .NET Core and .NET 5/6.

## Prérequis

Avant de plonger dans le tutoriel, assurez‑vous d’avoir les prérequis suivants :

- Connaissances de base en C# et développement .NET.  
- Un environnement de développement intégré (IDE) tel que Visual Studio.  
- Bibliothèque Aspose.OCR pour .NET installée. Vous pouvez la télécharger [ici](https://releases.aspose.com/ocr/net/).  
- Une image d'exemple contenant du texte pour la reconnaissance OCR.

## Importer les espaces de noms

Assurez‑vous d’avoir les espaces de noms nécessaires importés dans votre projet. Ajoutez les lignes suivantes en haut de votre fichier C# :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

Maintenant, décomposons le processus d’obtention des rectangles pour les lignes dans la reconnaissance d’image OCR en étapes faciles à suivre.

## Étape 1 : Configurer votre répertoire de documents

```csharp
// ExStart:3
string dataDir = "Your Document Directory";
// ExEnd:3
```

Remplacez `"Your Document Directory"` par le chemin réel du dossier qui contient votre image d’exemple.

## Étape 2 : Initialiser Aspose.OCR

```csharp
// ExStart:4
AsposeOcr api = new AsposeOcr();
// ExEnd:4
```

Créez une instance de la classe `AsposeOcr` pour accéder aux fonctionnalités OCR.

## Étape 3 : Spécifier le chemin de l'image

```csharp
// ExStart:5
string fullPath = dataDir + "sample.png";
// ExEnd:5
```

Définissez le chemin complet de l'image sur laquelle vous souhaitez effectuer l'OCR.

## Étape 4 : Reconnaître l'image et obtenir les rectangles

```csharp
// ExStart:6
List<Rectangle> lines = api.GetRectangles(fullPath, AreasType.LINES, false);
// ExEnd:6
```

La méthode `GetRectangles` renvoie une liste d’objets `Rectangle`, chacun représentant les coordonnées d’une ligne de texte détectée. C’est le cœur de **l’obtention des rectangles de lignes OCR**.

## Étape 5 : Afficher le résultat

```csharp
// ExStart:7
Console.WriteLine("Areas coordinates:");
lines.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
// ExEnd:7
```

Affichez les coordonnées des zones détectées dans la console. Vous verrez des valeurs que vous pourrez ensuite utiliser pour **extraire les coordonnées des lignes** pour un traitement personnalisé.

## Pourquoi utiliser Aspose.OCR pour les rectangles de lignes ?

- **Haute précision** – Des algorithmes avancés détectent les lignes même dans des images bruyantes ou inclinées.  
- **Multi‑plateforme** – Fonctionne sur .NET Framework, .NET Core et .NET 5/6.  
- **Aucune dépendance externe** – Bibliothèque pure .NET, aucune DLL native à distribuer.  
- **Sortie riche** – En plus des rectangles de lignes, vous pouvez également récupérer les mots, les caractères et les scores de confiance.

## Problèmes courants et solutions

| Problème | Solution |
|----------|----------|
| **Aucun rectangle retourné** | Assurez‑vous que l'image contient du texte clair et horizontal et que `AreasType.LINES` est spécifié. |
| **Coordonnées incorrectes** | Vérifiez le DPI de l'image ; les images à basse résolution peuvent entraîner des limites inexactes. |
| **Goulot d'étranglement de performance sur les grandes images** | Redimensionnez l'image à une résolution raisonnable avant d'appeler `GetRectangles`. |
| **Exception de licence** | Utilisez une licence d'essai pour les tests ; appliquez une licence complète pour la production afin d'éviter les limites d'évaluation. |

## FAQ

### Q1 : Puis‑je utiliser Aspose.OCR pour .NET avec n'importe quel type d'image ?

A1 : Aspose.OCR prend en charge un large éventail de formats d'image, garantissant une flexibilité dans vos applications OCR.

### Q2 : Quelle est la précision de la reconnaissance OCR ?

A2 : Aspose.OCR utilise des algorithmes avancés pour une haute précision, ce qui le rend adapté à divers scénarios de reconnaissance de texte.

### Q3 : Une version d'essai est‑elle disponible ?

A3 : Oui, vous pouvez explorer les capacités d'Aspose.OCR pour .NET avec l'[essai gratuit](https://releases.aspose.com/).

### Q4 : Où puis‑je trouver une documentation complète ?

A4 : Consultez la [documentation](https://reference.aspose.com/ocr/net/) pour des informations détaillées et des directives d'utilisation.

### Q5 : Besoin d'aide ou avez‑vous des questions spécifiques ?

A5 : Visitez le [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour le support communautaire et les discussions.

## Questions fréquemment posées

**Q : Puis‑je extraire des mots individuels au lieu de lignes complètes ?**  
A : Oui, utilisez `AreasType.WORDS` avec la même méthode `GetRectangles` pour obtenir des boîtes englobantes au niveau des mots.

**Q : L'API prend‑elle en charge les PDF multi‑pages ?**  
A : Convertissez chaque page PDF en image d'abord, puis appelez `GetRectangles` sur chaque image.

**Q : Comment gérer le texte tourné ?**  
A : Activez l'option de rotation automatique dans les paramètres OCR ou pré‑tournez l'image avant le traitement.

**Q : Existe‑t‑il un moyen d'obtenir les scores de confiance pour chaque ligne ?**  
A : Après avoir obtenu les rectangles, appelez `api.RecognizeImage(...).Lines` pour accéder aux objets ligne qui incluent les valeurs de confiance.

**Q : Quelles versions de .NET sont compatibles ?**  
A : La bibliothèque fonctionne avec .NET Framework 4.5+, .NET Core 3.1+ et .NET 5/6.

## Conclusion

Félicitations ! Vous avez réussi à **obtenir les rectangles de lignes OCR** pour une image en utilisant Aspose.OCR pour .NET. Avec les boîtes englobantes en main, vous pouvez désormais alimenter les coordonnées des lignes dans des flux de travail en aval tels que le rendu personnalisé, l'extraction de données ou l'analyse de mise en page.

---

**Last Updated:** 2025-12-17  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}