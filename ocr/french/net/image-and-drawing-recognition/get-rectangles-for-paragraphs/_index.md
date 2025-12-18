---
date: 2025-12-17
description: Apprenez à extraire des rectangles pour les paragraphes dans les images
  OCR à l'aide d'Aspose.OCR pour .NET – le guide incontournable pour extraire des
  rectangles et obtenir les coordonnées des paragraphes.
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Comment extraire des rectangles pour les paragraphes dans la reconnaissance
  d'images OCR
url: /fr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire des rectangles pour les paragraphes dans la reconnaissance d'images OCR

## Introduction

Bienvenue dans notre guide complet sur **comment extraire des rectangles** pour les paragraphes dans la reconnaissance d'images OCR avec Aspose.OCR pour .NET. Si vous souhaitez améliorer votre pipeline de traitement de documents, extraire les limites des paragraphes et automatiser l'extraction de données, vous êtes au bon endroit. Nous parcourrons chaque étape — de la configuration de l'environnement à l'affichage des coordonnées des rectangles — afin que vous puissiez commencer à utiliser les résultats OCR immédiatement.

## Réponses rapides
- **Que signifie « extraire des rectangles » ?** Il renvoie les boîtes englobantes (x, y, largeur, hauteur) des zones de texte détectées.  
- **Quelle méthode d'API fournit les rectangles ?** `AsposeOcr.GetRectangles` avec `AreasType.PARAGRAPHS`.  
- **Ai‑je besoin d’une licence pour le développement ?** Un essai gratuit suffit pour les tests ; une licence commerciale est requise pour la production.  
- **Puis‑je traiter plusieurs images à la fois ?** Oui — parcourez votre liste d'images et appelez `GetRectangles` pour chaque fichier.  
- **Quels formats sont pris en charge ?** PNG, JPEG, TIFF, BMP et bien d’autres.

## Qu’est‑ce que « comment extraire des rectangles » en OCR ?

En terminologie OCR, extraire des rectangles signifie identifier les limites géométriques qui entourent chaque paragraphe ou ligne de texte au sein d’une image. Ces coordonnées vous permettent de mettre en évidence, recadrer ou analyser davantage des sections spécifiques d’un document numérisé.

## Pourquoi extraire les coordonnées des paragraphes ?

- **Traitement post‑extraction précis** – vous pouvez injecter chaque rectangle dans des flux de travail en aval (par ex., traduction, rédaction).  
- **UI/UX améliorée** – superposez les boîtes englobantes sur l’image originale pour montrer aux utilisateurs où le texte a été trouvé.  
- **Automatisation par lots** – localisez et isolez rapidement les paragraphes dans de grands ensembles de documents.

## Prérequis

- Connaissances de base en C# et développement .NET.  
- Un environnement de développement avec Aspose.OCR pour .NET installé – vous pouvez le télécharger [ici](https://releases.aspose.com/ocr/net/).  
- Familiarité avec les concepts de traitement d’image et pourquoi l’OCR est essentiel pour extraire du texte à partir de fichiers numérisés.

## Importer les espaces de noms

Dans votre fichier C#, importez les espaces de noms requis afin que les classes OCR soient disponibles :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Étape 1 : Configurer le répertoire de vos documents

Définissez le dossier qui contient les images que vous souhaitez analyser :

```csharp
string dataDir = "Your Document Directory";
```

## Étape 2 : Initialiser l’instance AsposeOcr

Créez un objet `AsposeOcr` – cela vous donne accès à toutes les fonctions OCR :

```csharp
AsposeOcr api = new AsposeOcr();
```

## Étape 3 : Spécifier le chemin de l’image

Indiquez le fichier image exact que vous voulez traiter :

```csharp
string fullPath = dataDir + "sample.png";
```

## Étape 4 : Reconnaître l’image et obtenir les rectangles de paragraphes

Appelez la méthode `GetRectangles`. Le fait de définir `detect_areas` à `true` indique au moteur de renvoyer les rectangles **de paragraphe** :

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## Étape 5 : Afficher les résultats

Affichez les coordonnées afin de voir les **coordonnées de paragraphes extraites** qui ont été détectées :

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## Problèmes courants et solutions

| Problème | Raison | Solution |
|----------|--------|----------|
| Aucun rectangle renvoyé | Qualité de l’image trop faible ou `AreasType` incorrect | Assurez‑vous que l’image est nette et utilisez `AreasType.PARAGRAPHS`. |
| Les coordonnées sont décalées d’un pixel | Mauvaise correspondance de l’échelle DPI | Définissez le DPI correct lors du chargement de l’image ou utilisez `api.Config.Dpi`. |
| Exception de licence | Exécution sans licence valide en production | Appliquez une licence temporaire ou permanente via `api.SetLicense`. |

## Questions fréquemment posées

**Q : Aspose.OCR est‑il compatible avec différents formats d’image ?**  
R : Oui, Aspose.OCR prend en charge PNG, JPEG, TIFF, BMP et de nombreux autres formats courants.

**Q : Puis‑je utiliser Aspose.OCR pour le traitement par lots de plusieurs images ?**  
R : Absolument ! Parcourez une collection de chemins de fichiers et appelez `GetRectangles` pour chaque image.

**Q : Existe‑t‑il un essai gratuit disponible pour Aspose.OCR pour .NET ?**  
R : Oui, vous pouvez explorer un essai gratuit [ici](https://releases.aspose.com/).

**Q : Comment obtenir une licence temporaire pour Aspose.OCR ?**  
R : Vous pouvez acquérir une licence temporaire [ici](https://purchase.aspose.com/temporary-license/).

**Q : Où puis‑je trouver un support supplémentaire et des discussions liées à Aspose.OCR ?**  
R : Rendez‑vous sur le [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour le support communautaire et les discussions.

## Conclusion

Dans ce tutoriel, nous avons montré **comment extraire des rectangles** pour les paragraphes en utilisant Aspose.OCR pour .NET, parcouru chaque extrait de code et expliqué comment interpréter les coordonnées renvoyées. En intégrant ces étapes dans votre application, vous pouvez extraire de manière fiable les limites des paragraphes, améliorer les flux de travail documentaires et créer des solutions OCR plus intelligentes.

---

**Dernière mise à jour :** 2025-12-17  
**Testé avec :** Aspose.OCR 24.11 pour .NET  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}