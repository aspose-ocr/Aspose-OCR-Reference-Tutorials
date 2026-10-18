---
date: 2026-02-25
description: Apprenez à extraire du texte d’une image à l’aide d’Aspose.OCR pour .NET.
  Ce guide vous accompagne dans la préparation de rectangles pour la reconnaissance
  d’images OCR et l’amélioration de la précision.
linktitle: Prepare Rectangles in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: Comment extraire du texte d’une image en préparant des rectangles dans l’OCR
url: /fr/net/ocr-optimization/prepare-rectangles/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Préparer des rectangles dans la reconnaissance d'images OCR

## Introduction

La reconnaissance optique de caractères (OCR) est essentielle pour convertir le contenu visuel en texte consultable et modifiable. Dans ce tutoriel, vous **extraitrez du texte d’une image** en préparant des rectangles personnalisés qui concentrent le moteur OCR sur des régions spécifiques. En utilisant Aspose.OCR pour .NET, nous parcourrons chaque étape — de la configuration de votre projet à la récupération du texte reconnu—afin que vous puissiez intégrer une puissante fonctionnalité image‑vers‑texte dans vos applications .NET.

## Réponses rapides
- **Que signifie « extrait du texte d’une image » ?** Cela consiste à convertir les caractères visuels d’une image en chaînes lisibles par machine.  
- **Quelle bibliothèque aide à cela sous .NET ?** Aspose.OCR pour .NET.  
- **Ai‑je besoin d’une licence pour le développement ?** Un essai gratuit suffit pour les tests ; une licence est requise pour la production.  
- **Puis‑je cibler des zones spécifiques ?** Oui, en définissant des rectangles qui limitent la portée de l’OCR.  
- **Quelles versions de .NET sont prises en charge ?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6/7.

## Qu’est‑ce que « extrait du texte d’une image » avec des rectangles ?
Lorsque vous définissez des zones rectangulaires sur une image, le moteur OCR ne traite que ces zones. Cela améliore la précision, réduit le temps de traitement et vous permet d’ignorer les arrière‑plans bruyants ou les sections non pertinentes.

## Pourquoi préparer des rectangles avant l’OCR ?
- **Se concentrer sur le contenu pertinent :** Ignorer les en‑têtes, pieds de page ou graphiques décoratifs.  
- **Améliorer les performances :** Des régions plus petites signifient une reconnaissance plus rapide.  
- **Accroître la précision :** Moins de bruit visuel conduit à des résultats plus propres.

## Pourquoi cela importe pour les projets réels
De nombreux documents professionnels — reçus, factures, cartes d’identité—présentent des mises en page mixtes où seules certaines parties contiennent du texte utile. En utilisant des rectangles, vous pouvez extraire uniquement les champs nécessaires, réduisant ainsi considérablement le travail de post‑traitement et augmentant la fiabilité globale de votre pipeline d’automatisation.

## Cas d’utilisation courants
- **Automatisation de la saisie de données :** Extraire des champs spécifiques à partir de formulaires numérisés.  
- **Vérifications de conformité :** Isoler et valider des blocs de texte juridique.  
- **Indexation de contenu :** Indexer uniquement le titre ou la légende d’une image pour les moteurs de recherche.  

## Prérequis

- Familiarité avec C# et le développement .NET.  
- Bibliothèque Aspose.OCR pour .NET installée – vous pouvez la télécharger **[ici](https://releases.aspose.com/ocr/net/)**.  
- Une image d’exemple (par ex., `sample.png`) contenant le texte que vous souhaitez extraire.

## Importer les espaces de noms

Tout d’abord, importez les espaces de noms requis :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Étape 1 : Configurer votre répertoire de documents

Spécifiez où résident vos fichiers image et créez une instance du moteur OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

## Comment extraire du texte d’une image en utilisant plusieurs rectangles

### Étape 2 : Reconnaître l’image avec plusieurs rectangles

#### 2.1 Définir les rectangles

Créez une liste d’objets `Rectangle` qui délimitent les zones que le moteur OCR doit analyser.

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

Passez le chemin de l’image et la liste de rectangles à `RecognizeImage`. La méthode renvoie une collection de chaînes — chaque entrée correspond à un rectangle.

```csharp
// first case
List<string> listResult = api.RecognizeImage(dataDir + "sample.png", rects);

// Display the recognized text
foreach (string s in listResult)
{
    Console.WriteLine(s);
}
```

### Étape 3 : Reconnaître l’image avec les paramètres de reconnaissance (approche alternative)

Si vous préférez utiliser `RecognitionSettings`, vous pouvez obtenir le même résultat avec un appel API légèrement différent.

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

## Problèmes courants & astuces

- **Coordonnées de rectangle incorrectes :** Vérifiez que les valeurs `X`, `Y`, `Width` et `Height` correspondent bien à la région souhaitée.  
- **Qualité de l’image :** Les images à basse résolution peuvent donner de mauvais résultats OCR ; envisagez un pré‑traitement (par ex., binarisation).  
- **Résultats vides :** Assurez‑vous que les rectangles contiennent réellement du texte ; sinon le moteur renvoie des chaînes vides.

## Dépannage et bonnes pratiques

| Symptom | Cause probable | Solution |
|---------|----------------|----------|
| Aucun résultat ou chaînes vides | Rectangles hors des limites de l’image | Revérifier les dimensions de l’image et les coordonnées des rectangles |
| Caractères illisibles | Contraste faible ou bruit | Appliquer un nettoyage d’image (niveaux de gris, seuillage) avant l’OCR |
| Performances lentes sur de gros fichiers | Trop de rectangles ou image très grande | Diviser l’image ou réduire le nombre de rectangles si possible |

## Conclusion

Vous avez maintenant appris comment **extraire du texte d’une image** en préparant des rectangles personnalisés avec Aspose.OCR pour .NET. Cette technique vous offre un contrôle granulaire du traitement OCR, vous aidant à créer des fonctionnalités d’extraction de texte plus rapides et plus précises dans vos applications.

## Questions fréquentes

**Q :** Puis‑je utiliser Aspose.OCR pour .NET avec d’autres frameworks .NET ?  
**R :** Oui, Aspose.OCR pour .NET est compatible avec divers frameworks .NET.

**Q :** Existe‑t‑il un essai gratuit pour Aspose.OCR pour .NET ?  
**R :** Absolument ! Vous pouvez accéder à l’essai gratuit **[ici](https://releases.aspose.com/)**.

**Q :** Comment obtenir du support pour Aspose.OCR pour .NET ?  
**R :** Consultez le **[forum Aspose.OCR](https://forum.aspose.com/c/ocr/16)** pour un support dédié.

**Q :** Puis‑je obtenir une licence temporaire pour les tests ?  
**R :** Oui, vous pouvez acquérir une licence temporaire **[ici](https://purchase.aspose.com/temporary-license/)**.

**Q :** Où trouver la documentation d’Aspose.OCR pour .NET ?  
**R :** La documentation est disponible **[ici](https://reference.aspose.com/ocr/net/)**.

---

**Dernière mise à jour :** 2026-02-25  
**Testé avec :** Aspose.OCR 24.11 pour .NET  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}