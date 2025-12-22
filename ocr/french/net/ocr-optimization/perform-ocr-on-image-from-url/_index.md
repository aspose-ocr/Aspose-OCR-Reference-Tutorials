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

## Quick Answers
- **What does this tutorial cover?** Reconnaître du texte à partir d'une image située à une URL publique en utilisant Aspose.OCR pour .NET.  
- **Which primary keyword is targeted?** *recognize text from image*  
- **Do I need a license?** Un essai est disponible, mais une licence commerciale est requise pour une utilisation en production.  
- **What .NET versions are supported?** .NET Framework 4.5+, .NET Core 3.1+, .NET 5/6+.  
- **How long does implementation take?** Typiquement moins de 10 minutes pour une configuration de base.

## What is “recognize text from image”?
Reconnaître du texte à partir d'une image signifie convertir la représentation visuelle des caractères en texte éditable et interrogeable. Ce processus est souvent appelé **convertir une image en texte** ou **extraire du texte d'une image**, et il alimente des scénarios tels que la numérisation de documents, l'automatisation de la saisie de données et l'amélioration de l'accessibilité.

## Why use Aspose.OCR for .NET?
- **High accuracy** with built‑in language support.  
- **Fine‑grained OCR recognition settings** (e.g., auto‑skew, area detection).  
- **Simple API** that works with both .NET Framework and .NET Core.  
- **No external dependencies** – everything runs locally.

## Prerequisites

Avant de plonger dans le tutoriel, assurez‑vous d'avoir les prérequis suivants :

- Aspose.OCR pour .NET : assurez‑vous d'avoir la bibliothèque Aspose.OCR intégrée à votre projet .NET. Vous pouvez la télécharger depuis la [page de version](https://releases.aspose.com/ocr/net/).

- Environnement de développement : disposez d'un environnement de développement .NET fonctionnel installé sur votre machine.

## Import Namespaces

Dans votre projet .NET, incluez les espaces de noms nécessaires pour accéder aux fonctionnalités Aspose.OCR. Ajoutez le fragment de code suivant à votre projet :

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
```

## How to recognize text from image using a URL?

### Step 1: Set Up Your Document Directory

Commencez par spécifier le répertoire où vos documents sont stockés. Remplace `"Your Document Directory"` par le chemin réel vers vos documents.

```csharp
string dataDir = "Your Document Directory";
```

### Step 2: Get the Image for Recognition

Fournissez l'URL de l'image sur laquelle vous souhaitez exécuter l'OCR. Assurez‑vous que l'image est accessible publiquement.

```csharp
string uri = "https://qph.fs.quoracdn.net/main-qimg-0ff82d0dc3543dcd3b06028f5476c2e4";
```

### Step 3: Initialize AsposeOcr

Créez une instance de la classe AsposeOcr pour accéder aux fonctionnalités OCR.

```csharp
AsposeOcr api = new AsposeOcr();
```

### Step 4: Recognize Image

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

### Step 5: Print Result

Affichez le résultat de la reconnaissance, incluant le texte reconnu, les zones détectées et les éventuels avertissements.

```csharp
Console.WriteLine($"Text:\n {result.RecognitionText}");
Console.WriteLine("Areas:");
result.RecognitionAreasText.ForEach(a => Console.WriteLine($"{a}"));
Console.WriteLine("Warnings:");
result.Warnings.ForEach(w => Console.WriteLine($"{w}"));
Console.WriteLine($"JSON: {result.GetJson()}");
```

### Step 6: Execute and Verify

Exécutez votre application, et si tout est correctement configuré, vous devriez voir le processus OCR s'exécuter avec succès.

```csharp
Console.WriteLine("PerformOCROnImageFromUrl executed successfully");
```

## Common Issues and Solutions

- **Image not publicly accessible** – Vérifiez que l'URL fonctionne dans un navigateur. Si l'image nécessite une authentification, téléchargez‑la d'abord et utilisez `RecognizeImageFromStream`.
- **Incorrect recognition areas** – Ajustez les valeurs du `Rectangle` ou définissez `DetectAreas = false` pour laisser le moteur détecter automatiquement.
- **Language not recognized** – Assurez‑vous que le pack de langue approprié est installé ou définissez `Language = "eng"` (ou autre code ISO) dans `RecognitionSettings`.

## Frequently Asked Questions

### Q1: Is Aspose.OCR suitable for handling multiple languages?

A1: Yes, Aspose.OCR supports the recognition of text in various languages, making it versatile for international applications.

### Q2: Can I use Aspose.OCR for both single-line and multi-line text recognition?

A2: Absolutely! Aspose.OCR provides flexibility for recognizing both single-line and multi-line text, adapting to your specific use case.

### Q3: Are there any licensing options available for Aspose.OCR?

A3: Yes, you can explore licensing options and make purchases on the [boutique Aspose](https://purchase.aspose.com/buy).

### Q4: Is there a free trial available for Aspose.OCR?

A4: Yes, you can try out Aspose.OCR for free by visiting the [page des versions](https://releases.aspose.com/).

### Q5: Where can I find support or community discussions related to Aspose.OCR?

A5: Visit the [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) for support and engaging with the community.

## Conclusion

Avec Aspose.OCR pour .NET, l'intégration de capacités OCR dans vos applications .NET devient une expérience fluide. Ce tutoriel vous a guidé à travers le processus de **reconnaître du texte à partir d'une image** en utilisant une URL, vous offrant une base solide pour exploiter l'extraction de texte dans vos projets.

---

**Last Updated:** 2025-12-22  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}