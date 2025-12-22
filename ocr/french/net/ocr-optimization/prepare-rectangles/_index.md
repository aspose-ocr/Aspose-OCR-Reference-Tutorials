---
date: 2025-12-22
description: Apprenez à extraire du texte d’une image à l’aide d’Aspose.OCR pour .NET.
  Ce guide vous explique comment préparer des rectangles pour la reconnaissance d’image
  OCR et améliorer la précision.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Comment extraire du texte d’une image en préparant des rectangles dans l’OCR
url: /fr/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Préparer des rectangles pour la reconnaissance d'images OCR

## Introduction

La reconnaissance optique de caractères (OCR) est essentielle pour convertir le contenu visuel en texte consultable et modifiable. Dans ce tutoriel, vous **extraitrez du texte d'une image** en préparant des rectangles personnalisés qui concentrent le moteur OCR sur des zones spécifiques. En utilisant Aspose.OCR pour .NET, nous parcourrons chaque étape — de la configuration de votre projet à la récupération du texte reconnu — afin que vous puissiez intégrer une puissante fonctionnalité de conversion d'image en texte dans vos applications .NET.

## Réponses rapides
- **Que signifie « extraire du texte d'une image » ?** Cela signifie convertir les caractères visuels d'une image en chaînes lisibles par machine.  
- **Quelle bibliothèque aide à cela en .NET ?** Aspose.OCR for .NET.  
- **Ai-je besoin d'une licence pour le développement ?** Un essai gratuit suffit pour les tests ; une licence est requise pour la production.  
- **Puis-je cibler des zones spécifiques ?** Oui, en définissant des rectangles qui limitent la portée de l'OCR.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Qu'est-ce que « extraire du texte d'une image » avec des rectangles ?
Lorsque vous définissez des zones rectangulaires sur une image, le moteur OCR ne traite que ces zones. Cela améliore la précision, réduit le temps de traitement et vous permet d'ignorer les arrière-plans bruyants ou les sections non pertinentes.

## Pourquoi préparer des rectangles avant l'OCR ?
- **Se concentrer sur le contenu pertinent :** Ignorer les en-têtes, pieds de page ou graphiques décoratifs.  
- **Améliorer les performances :** Des régions plus petites signifient une reconnaissance plus rapide.  
- **Améliorer la précision :** Moins de bruit visuel conduit à des résultats plus propres.

## Prérequis

- Familiarité avec le développement C# et .NET.  
- Bibliothèque Aspose.OCR pour .NET installée – vous pouvez la télécharger **[ici](https://releases.aspose.com/ocr/net/)**.  
- Une image d'exemple (par ex., `sample.png`) contenant le texte que vous souhaitez extraire.

## Importer les espaces de noms

Tout d'abord, importez les espaces de noms requis :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Étape 1 : Configurer votre répertoire de documents

Spécifiez l'emplacement de vos fichiers image et créez une instance du moteur OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Comment extraire du texte d'une image en utilisant plusieurs rectangles

### Étape 2 : Reconnaître l'image avec plusieurs rectangles

#### 2.1 Définir les rectangles

Créez une liste d'objets `Rectangle` qui délimitent les zones que vous souhaitez que le moteur OCR analyse.

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

#### 2.2 Effectuer la reconnaissance OCR

Passez le chemin de l'image et la liste de rectangles à `RecognizeImage`. La méthode renvoie une collection de chaînes — chaque entrée correspond à un rectangle.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Étape 3 : Reconnaître l'image avec les paramètres de reconnaissance (approche alternative)

Si vous préférez utiliser `RecognitionSettings`, vous pouvez obtenir le même résultat avec un appel d'API légèrement différent.

#### 3.1 Définir les paramètres de reconnaissance

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

#### 3.2 Afficher le texte reconnu

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Problèmes courants et astuces

- **Coordonnées de rectangle incorrectes :** Assurez-vous que les valeurs `X`, `Y`, `Width` et `Height` correspondent correctement à la région souhaitée.  
- **Qualité de l'image :** Les images à basse résolution peuvent donner de mauvais résultats OCR ; envisagez un prétraitement (par ex., binarisation).  
- **Résultats vides :** Vérifiez que les rectangles contiennent réellement du texte ; sinon le moteur renvoie des chaînes vides.

## Conclusion

Vous avez maintenant appris comment **extraire du texte d'une image** en préparant des rectangles personnalisés avec Aspose.OCR pour .NET. Cette technique vous offre un contrôle granulaire du traitement OCR, vous aidant à créer des fonctionnalités d'extraction de texte plus rapides et plus précises dans vos applications.

## Questions fréquentes

**Q:** Puis-je utiliser Aspose.OCR pour .NET avec d'autres frameworks .NET ?  
**A:** Oui, Aspose.OCR pour .NET est compatible avec divers frameworks .NET.

**Q:** Existe-t-il un essai gratuit disponible pour Aspose.OCR pour .NET ?  
**A:** Absolument ! Vous pouvez accéder à l'essai gratuit **[ici](https://releases.aspose.com/)**.

**Q:** Comment obtenir du support pour Aspose.OCR pour .NET ?  
**A:** Consultez le **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** pour un support dédié.

**Q:** Puis-je obtenir une licence temporaire à des fins de test ?  
**A:** Oui, vous pouvez acquérir une licence temporaire **[ici](https://purchase.aspose.com/temporary-license/)**.

**Q:** Où puis-je trouver la documentation pour Aspose.OCR pour .NET ?  
**A:** La documentation est disponible **[ici](https://reference.aspose.com/ocr/net/)**.

---

**Dernière mise à jour :** 2025-12-22  
**Testé avec :** Aspose.OCR 24.11 for .NET  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}