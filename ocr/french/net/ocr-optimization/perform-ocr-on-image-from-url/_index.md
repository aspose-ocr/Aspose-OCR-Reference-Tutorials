---
date: 2025-12-22
description: Apprenez à reconnaître le texte à partir d’une image en utilisant Aspose.OCR
  pour .NET, en convertissant l’image en texte avec des paramètres de reconnaissance
  OCR précis.
linktitle: recognize text from image – Perform OCR on Image from URL
second_title: Aspose.OCR .NET API
title: Reconnaître le texte d’une image – Effectuer une OCR sur une image à partir
  d’une URL
url: /fr/net/ocr-optimization/perform-ocr-on-image-from-url/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Effectuer l'OCR sur une image depuis une URL dans la reconnaissance d'image OCR

## Introduction

Dans le domaine de la reconnaissance optique de caractères (OCR), Aspose.OCR pour .NET vous permet de **reconnaître du texte à partir d'une image** avec précision, offrant aux développeurs la capacité d'extraire du contenu d'images sans effort. Si vous souhaitez intégrer des fonctionnalités OCR dans votre application .NET et effectuer la reconnaissance de texte depuis une source distante, ce guide pas à pas vous accompagnera tout au long du processus d'exécution d'OCR sur une image à partir d'une URL.

## Réponses rapides
- **Que couvre ce tutoriel ?** Reconnaître du texte à partir d'une image située à une URL publique en utilisant Aspose.OCR pour .NET.
- **Quel mot clé principal est ciblé ?** *reconnaître le texte de l'image*
- **Dois-je avoir une licence ?** Un essai est disponible, mais une licence commerciale est requise pour une utilisation en production.
- **Quelles versions de .NET sont prises en charge ?** .NET Framework4.5+, .NETCore3.1+, .NET5/6+.
- **Combien de temps prend la mise en œuvre ?** Typiquement moins de 10minutes pour une configuration de base.

## Qu'est-ce que « reconnaître le texte à partir d'une image » ?
Reconnaître du texte à partir d'une image signifie convertir la représentation visuelle des caractères en texte éditable et interrogeable. Ce processus est souvent appelé **convertir une image en texte** ou **extraire du texte d'une image**, et il alimente des scénarios tels que la numérisation de documents, l'automatisation de la saisie de données et l'amélioration de l'accessibilité.

## Pourquoi utiliser Aspose.OCR pour .NET ?
- **Haute précision** avec prise en charge linguistique intégrée.
- **Paramètres de reconnaissance OCR à granularité fine** (par exemple, inclinaison automatique, détection de zone).
- **API simple** qui fonctionne à la fois avec .NET Framework et .NET Core.
- **Aucune dépendance externe** – tout s'exécute localement.

## Prérequis

Avant de Sous-marin dans le tutoriel, assurez-vous d'avoir les prérequis suivants :

- Aspose.OCR pour .NET : assurez-vous d'avoir la bibliothèque Aspose.OCR intégrée à votre projet .NET. Vous pouvez le télécharger depuis la [page de version](https://releases.aspose.com/ocr/net/).

- Environnement de développement : disposez d'un environnement de développement .NET fonctionnel installé sur votre machine.

## Importer des espaces de noms

Dans votre projet .NET, incluez les espaces de noms nécessaires pour accéder aux fonctionnalités Aspose.OCR. Ajoutez le fragment de code suivant à votre projet :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## Comment reconnaître le texte d'une image à l'aide d'une URL ?

### Étape 1 : Configurez votre répertoire de documents

Commencez par préciser le répertoire où vos documents sont stockés. Remplacez `"Your Document Directory"` par le chemin réel vers vos documents.

```csharp
string dataDir = "Your Document Directory";
```

### Étape 2 : Obtenez l'image pour la reconnaissance

Fournissez l'URL de l'image sur laquelle vous souhaitez exécuter l'OCR. Assurez-vous que l'image est accessible publiquement.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### Étape 3 : Initialiser AsposeOcr

Créez une instance de la classe AsposeOcr pour aux fonctionnalités OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

### Étape 4 : Reconnaître l'image

Utilisez la bibliothèque Aspose.OCR pour reconnaître le texte à partir de l'URL d'image spécifiée. Ajustez les paramètres de reconnaissance selon vos besoins.

```csharp
RecognitionResult result = api.RecognizeImageFromUri(uri, new RecognitionSettings
{
    DetectAreas = true,
    RecognizeSingleLine = false,
    AutoSkew = true,
    RecognitionAreas = new List<Rectangle>()
    {
        new Rectangle(1,3,390,70),
        new Rectangle(1,72,390,70)
    }
});
```

### Étape 5 : Imprimer le résultat

Affichez le résultat de la reconnaissance, incluant le texte reconnu, les zones détectées et les éventuels avertissements.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### Étape 6 : Exécuter et vérifier

Exécutez votre application, et si tout est correctement configuré, vous devriez voir le processus OCR s'exécuter avec succès.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Problèmes courants et solutions

- **Image non accessible au public** – Vérifiez que l'URL fonctionne dans un navigateur. Si l'image nécessite une authentification, téléchargez‑la d'abord et utilisez `RecognizeImageFromStream`.
- **Zones de reconnaissance incorrectes** – Ajustez les valeurs du `Rectangle` ou définissez `DetectAreas = false` pour laisser le moteur détecter automatiquement.
- **Langue non reconnue** – Assurez-vous que le pack de langue approprié est installé ou défini `Language = "eng"` (ou autre code ISO) dans `RecognitionSettings`.

## Questions fréquemment posées

### Q1 : Aspose.OCR est-il adapté à la gestion de plusieurs langues ?

A1 : Oui, Aspose.OCR prend en charge la reconnaissance de texte dans différentes langues, ce qui le rend polyvalent pour les applications internationales.

### Q2 : Puis-je utiliser Aspose.OCR pour la reconnaissance de texte sur une seule ligne et sur plusieurs lignes ?

R2 : Absolument ! Aspose.OCR offre une grande flexibilité pour la reconnaissance de texte sur une seule ligne ou sur plusieurs lignes, s’adaptant ainsi à votre cas d’utilisation spécifique.

### Q3 : Existe-t-il des options de licence pour Aspose.OCR ?

R3 : Oui, vous pouvez consulter les options de licence et effectuer des achats sur la [boutique Aspose](https://purchase.aspose.com/buy).

### Q4 : Existe-t-il une version d’essai gratuite d’Aspose.OCR ?

R4 : Oui, vous pouvez essayer Aspose.OCR gratuitement en consultant la [page des versions](https://releases.aspose.com/).

### Q5 : Où puis-je trouver de l’aide ou des discussions communautaires concernant Aspose.OCR ?

R5 : Rendez-vous sur le [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour obtenir de l’aide et interagir avec la communauté.

## Conclusion

Avec Aspose.OCR pour .NET, l'intégration de capacités OCR dans vos applications .NET devient une expérience fluide. Ce tutoriel vous a guidé à travers le processus de **reconnaître du texte à partir d'une image** en utilisant une URL, vous offrant une base solide pour exploiter l'extraction de texte dans vos projets.

---

**Dernière mise à jour :** 2025-12-22
**Testé avec :** Aspose.OCR 24.11 pour .NET
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}