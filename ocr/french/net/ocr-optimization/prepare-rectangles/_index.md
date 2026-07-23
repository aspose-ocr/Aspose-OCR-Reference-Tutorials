---
date: 2026-07-23
description: Apprenez à extraire du texte d'une image en utilisant Aspose.OCR for
  .NET, en préparant des rectangles pour améliorer la précision de l'OCR et convertir
  l'image en texte efficacement.
keywords:
- extract text from image
- convert image to text
- improve ocr accuracy
lastmod: 2026-07-23
linktitle: Préparer des rectangles dans la reconnaissance d'images OCR
og_description: Extraire du texte d'une image en utilisant Aspose.OCR for .NET. Apprenez
  à préparer des rectangles, à augmenter la précision de l'OCR et à convertir l'image
  en texte efficacement.
og_image_alt: Guide to extract text from image using rectangles with Aspose.OCR for
  .NET
og_title: Extraire du texte d'une image avec des rectangles – Guide OCR
schemas:
- author: Aspose
  dateModified: '2026-07-23'
  description: Learn how to extract text from image using Aspose.OCR for .NET, preparing
    rectangles to improve OCR accuracy and convert image to text efficiently.
  headline: Extract Text from Image with Rectangles – OCR Guide
  type: TechArticle
- questions:
  - answer: It converts visual characters in a picture into machine‑readable strings.
    question: What does “extract text from image” mean?
  - answer: Aspose.OCR for .NET provides a full‑featured OCR engine.
    question: Which library handles this in .NET?
  - answer: A free trial works for development; a commercial license is required for
      deployment.
    question: Do I need a license for production?
  - answer: Yes—define rectangles to target only the areas that contain useful text.
    question: Can I limit OCR to specific zones?
  - answer: .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.
    question: What .NET versions are supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
tags:
- ocr
- Aspire.OCR
- .NET image processing
- extract text from image
title: Extraire du texte d'une image avec des rectangles – Guide OCR
url: /fr/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d'une image avec des rectangles – Guide OCR

## Introduction

La reconnaissance optique de caractères (OCR) vous permet **d'extraire du texte d'une image** afin qu'ils deviennent recherchables et modifiables. Dans ce tutoriel, nous vous montrerons comment améliorer la précision de l'OCR en préparant des rectangles personnalisés qui concentrent le moteur sur les zones exactes dont vous avez besoin. En utilisant Aspose.OCR pour .NET, vous verrez le flux de travail complet — de la configuration du projet à la récupération des chaînes reconnues — afin que vous puissiez intégrer une conversion fiable d'image en texte dans n'importe quelle application .NET.

## Réponses rapides
- **Que signifie “extract text from image” ?** Il convertit les caractères visuels d'une image en chaînes lisibles par machine.  
- **Quelle bibliothèque gère cela dans .NET ?** Aspose.OCR pour .NET fournit un moteur OCR complet.  
- **Ai-je besoin d'une licence pour la production ?** Un essai gratuit fonctionne pour le développement ; une licence commerciale est requise pour le déploiement.  
- **Puis-je limiter l'OCR à des zones spécifiques ?** Oui — définissez des rectangles pour cibler uniquement les zones contenant du texte utile.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Qu'est-ce que “extract text from image” avec des rectangles ?
Le processus `extract text from image` lit les caractères à l'intérieur des zones rectangulaires définies, en ignorant tout le reste. En limitant l'OCR à ces zones, vous obtenez une meilleure précision, un traitement plus rapide et moins d'effort de post‑traitement. Cette approche isole le texte qui vous intéresse tout en éliminant les graphiques d'arrière‑plan, les éléments décoratifs et autres bruits visuels pouvant perturber le moteur OCR.

## Pourquoi préparer des rectangles avant l'OCR ?
Préparer des rectangles vous permet de concentrer le moteur OCR sur les parties les plus pertinentes d'une image, ce qui améliore à la fois la vitesse et la précision. En réduisant la zone d'analyse, vous diminuez la quantité de données que le moteur doit examiner, ce qui conduit à des résultats plus rapides et à moins d'erreurs de reconnaissance causées par le bruit visuel superflu.

- **Se concentrer sur le contenu pertinent :** Ignorer les en-têtes, pieds de page ou graphiques décoratifs qui pourraient perturber le moteur.  
- **Améliorer les performances :** Des régions plus petites nécessitent moins de calculs, réduisant le temps d'exécution jusqu'à 40 % sur de grands scans.  
- **Améliorer la précision :** Réduire le bruit visuel augmente les taux de reconnaissance de caractères de ~85 % à >95 % sur des documents bruyants.

## Pourquoi cela importe pour les projets réels
De nombreux documents professionnels — reçus, factures, cartes d'identité — combinent texte avec logos ou codes-barres. En dessinant des rectangles autour des champs dont vous avez réellement besoin, vous extrayez uniquement les données précieuses, réduisant considérablement le travail de nettoyage en aval et augmentant la fiabilité des flux de travail automatisés. Cette extraction ciblée diminue l'effort de post‑traitement et aide à maintenir la conformité aux normes de gestion des données.

## Cas d'utilisation courants
- **Automatisation de la saisie de données :** Extraire des champs spécifiques à partir de formulaires numérisés ou de reçus de dépenses.  
- **Vérifications de conformité :** Isoler les clauses légales ou les déclarations réglementaires pour vérification.  
- **Indexation de contenu :** Indexer uniquement le titre ou la légende d'une image pour la visibilité dans les moteurs de recherche.

## Prérequis

- Connaissances de base en C# et développement .NET.  
- Bibliothèque Aspose.OCR pour .NET installée – téléchargez‑la **[ici](https://releases.aspose.com/ocr/net/)** ou parcourez toutes les versions **[ici](https://releases.aspose.com/)**.  
- Une image d'exemple (par ex., `sample.png`) contenant le texte que vous souhaitez extraire.

## Importer les espaces de noms

Les instructions `using` importent le moteur OCR et les classes de géométrie dans le scope.

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Étape 1 : Configurer votre répertoire de documents

Spécifiez le dossier contenant vos images et créez une instance du moteur OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Comment extraire du texte d'une image en utilisant plusieurs rectangles
Chargez l'image une fois, puis fournissez une liste de rectangles au moteur OCR. Chaque rectangle définit une région d'intérêt, et le moteur renvoie une chaîne distincte pour chaque région, vous permettant de gérer les champs individuellement et de combiner les résultats selon les besoins.

### Définir les rectangles

`Rectangle` décrit les coordonnées X‑Y et la taille de chaque zone que vous souhaitez analyser.  

```csharp
List<Rectangle> rects = new List<Rectangle>()
{
    new Rectangle(138, 352, 2033, 537),
    new Rectangle(147, 890, 2033, 1157),
    new Rectangle(923, 2045, 465, 102),
    new Rectangle(104, 2147, 2076, 819)
};
```

### Effectuer la reconnaissance OCR

La méthode `RecognizeImage` traite l'image en utilisant la liste de rectangles fournie et renvoie le texte reconnu pour chaque région.  

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

## Comment extraire du texte d'une image en utilisant RecognitionSettings (Approche alternative)
Si vous préférez un appel basé sur des paramètres, vous pouvez obtenir le même résultat avec `RecognitionSettings`. Cet objet vous permet de regrouper les définitions de rectangles avec la langue, le DPI et d'autres options OCR, offrant un appel d'API propre à paramètre unique.

### Définir les paramètres de reconnaissance

`RecognitionSettings` vous permet de regrouper la liste de rectangles et des options supplémentaires (par ex., langue, DPI) dans un seul objet.  

```csharp
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings
{
    RecognitionAreas = rects
});
```

### Afficher le texte reconnu

Itérez sur les chaînes retournées et affichez le texte de chaque région.  

```csharp
// Display the recognized text
foreach (string s in result.RecognitionAreasText)
{
    Console.WriteLine(s);
}
```

## Problèmes courants et astuces

- **Coordonnées de rectangle incorrectes :** Vérifiez que `X`, `Y`, `Width` et `Height` correspondent à la zone prévue.  
- **Qualité de l'image :** Les images basse résolution ou fortement compressées dégradent les résultats OCR ; envisagez un pré‑traitement comme la binarisation.  
- **Résultats vides :** Assurez‑vous que les rectangles contiennent réellement du texte lisible ; sinon le moteur renvoie des chaînes vides.

## Dépannage et bonnes pratiques

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| Pas de sortie ou chaînes vides | Rectangles hors des limites de l'image | Vérifiez à nouveau les dimensions de l'image et les coordonnées des rectangles |
| Caractères illisibles | Contraste faible ou bruit | Appliquer une conversion en niveaux de gris et un seuillage avant l'OCR |
| Performance lente sur les gros fichiers | Trop de rectangles ou image très grande | Divisez l'image ou réduisez le nombre de rectangles si possible |

## Conclusion

Vous savez maintenant comment **extraire du texte d'une image** en préparant des rectangles personnalisés avec Aspose.OCR pour .NET. Cette approche vous offre un contrôle précis du traitement OCR, offrant des fonctionnalités d'extraction de texte plus rapides et plus précises pour toute solution .NET.

## Foire aux questions

**Q:** Puis-je utiliser Aspose.OCR pour .NET avec d'autres frameworks .NET ?  
**A:** Oui, Aspose.OCR pour .NET fonctionne avec .NET Framework 4.5+, .NET Core 3.1+, et .NET 5/6/7.

**Q:** Existe-t-il un essai gratuit disponible ?  
**A:** Absolument ! Téléchargez l'essai **[ici](https://releases.aspose.com/)**.

**Q:** Où puis‑je obtenir du support pour Aspose.OCR pour .NET ?  
**A:** Consultez le **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** pour une assistance dédiée.

**Q:** Puis‑je obtenir une licence temporaire pour les tests ?  
**A:** Oui, une licence temporaire est disponible **[ici](https://purchase.aspose.com/temporary-license/)**.

**Q:** Où se trouve la documentation officielle ?  
**A:** La référence complète de l'API est disponible **[ici](https://reference.aspose.com/ocr/net/)**.

---

**Dernière mise à jour :** 2026-07-23  
**Testé avec :** Aspose.OCR 24.11 pour .NET  
**Auteur :** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés

- [Comment extraire des rectangles pour les paragraphes dans la reconnaissance d'images OCR](/ocr/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/)
- [Comment faire de l'OCR sur une image – Effectuer l'OCR sur une image dans la reconnaissance d'images OCR](/ocr/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Comment extraire du texte d'une image en utilisant Aspose.OCR pour .NET](/ocr/net/text-recognition/get-recognition-result/)


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}