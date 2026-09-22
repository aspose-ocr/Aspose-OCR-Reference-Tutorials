---
date: 2026-02-12
description: Apprenez à extraire du texte d’image avec OCR et sélection de langue
  en utilisant Aspose.OCR pour Java. Ce guide étape par étape couvre l’extraction
  de texte Java, la correction d’inclinaison OCR et bien plus encore.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Comment OCR le texte d'image avec la langue en utilisant Aspose.OCR
url: /fr/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer la reconnaissance OCR de texte d'image avec la langue en utilisant Aspose.OCR

## Introduction

L'extraction de texte à partir de fichiers image est une exigence courante, que vous numérisiez des documents scannés, traitiez des reçus ou créiez des archives consultables. Dans ce tutoriel, nous parcourrons un exemple complet et pratique qui montre **comment faire de l'OCR sur du texte d'image** avec un paramètre de langue spécifique, afin que vous puissiez intégrer une OCR fiable dans vos applications Java dès aujourd'hui. Vous verrez également comment gérer la correction de l'inclinaison (skew) et la reconnaissance basée sur des régions pour une précision optimale.

## Réponses rapides
- **Quelle bibliothèque gère l'OCR en Java ?** Aspose.OCR for Java  
- **Quel paramètre sélectionne la langue ?** `settings.setLanguage(Language.Eng)` (ou toute langue prise en charge)  
- **Ai‑je besoin d'une licence pour le développement ?** Une licence d'évaluation gratuite fonctionne pour les tests ; une licence commerciale est requise pour la production.  
- **Puis‑je limiter l'OCR à une région de l'image ?** Oui, utilisez `RecognitionSettings.setRecognitionAreas()` avec des rectangles.  
- **Quel est le temps d'exécution typique ?** Quelques secondes par page sur un ordinateur portable standard, selon la taille de l'image et la complexité de la langue.

## Comment faire de l'OCR de texte d'image avec sélection de la langue
Dans cette section, nous répondons à la question principale **comment faire de l'OCR** d'une image lorsque vous connaissez la langue du texte. Sélectionner la bonne langue améliore considérablement la précision de la reconnaissance car le moteur OCR peut appliquer des dictionnaires et des modèles de caractères spécifiques à la langue.

### Pourquoi c'est important
- **Précision accrue** – les modèles spécifiques à la langue réduisent les erreurs de reconnaissance.  
- **Gain de performance** – le moteur ignore les vérifications de langues inutiles.  
- **Meilleure prise en charge des diacritiques** – le français, l'espagnol, l'allemand, etc., sont reconnus correctement lorsque l'énumération `Language` correspondante est utilisée.

## Qu’est‑ce que « extraire du texte d’une image » ?
Extraire du texte d’une image (OCR) convertit la représentation visuelle des caractères en chaînes lisibles par machine. Cela permet la recherche, l'analyse et les flux de travail d'extraction de données qui nécessiteraient autrement une transcription manuelle.

## Pourquoi utiliser Aspose.OCR avec sélection de la langue ?
- **Support multilingue** – choisissez la ou les langues exactes présentes dans votre image pour améliorer la précision.  
- **Contrôle fin** – ajustez l’inclinaison, définissez les zones de reconnaissance et configurez le comportement d’auto‑skew.  
- **API Java pure** – aucune dépendance native, facile à intégrer dans n’importe quel projet Java.  
- **Données de résultat riches** – obtenez du texte brut, du JSON, des rectangles de délimitation et des avertissements en un seul appel.

## Prerequisites

Avant de commencer, assurez-vous d'avoir :

- **Java Development Kit (JDK)** installé (JDK 8 ou supérieur).  
- **Bibliothèque Aspose.OCR for Java** – téléchargez‑la depuis le site officiel [ici](https://reference.aspose.com/ocr/java/).  
- Un fichier image contenant le texte que vous souhaitez extraire, par ex., `p3.png`.

## Import Packages

Dans votre fichier source Java, incluez les classes Aspose.OCR requises ainsi que les utilitaires Java standard :

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Step‑by‑Step Guide

### Step 1: Set up Your Document Directory

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Remplacez `"Your Document Directory"` par le chemin absolu où se trouve `p3.png`.

### Step 2: Define the Image Path

```java
// The image path
String file = dataDir + "p3.png";
```

Assurez‑vous que la variable `file` pointe vers l’image exacte que vous souhaitez traiter.

### Step 3: Create Aspose.OCR API Instance

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

L’objet `AsposeOCR` vous donne accès à toutes les opérations OCR.

### Step 4: Set Recognition Options (Language Selection)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Ici nous :

1. Désactiver l’auto‑skew car nous fournissons une valeur d’inclinaison manuelle.  
2. Définir une région rectangulaire (`RecognitionAreas`) pour limiter l’OCR à la partie de l’image contenant réellement du texte.  
3. Définir la **langue** sur l'anglais (`Language.Eng`). Changez cela en `Language.Fra`, `Language.Spa`, etc., selon votre image source.

### Step 5: Perform OCR and Retrieve Results

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

L’appel `RecognizePage` exécute le moteur OCR en utilisant l’image et les paramètres que vous avez définis. Le résultat est stocké dans un objet `RecognitionResult`.

### Step 6: Print and Utilize Results

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

La sortie console montre :

- Le texte complet extrait (`recognitionText`).  
- Le texte pour chaque rectangle défini (`recognitionAreasText`).  
- Les coordonnées du rectangle de délimitation.  
- Une représentation JSON pour un traitement en aval facile.  
- L’angle d’inclinaison détecté et les éventuels avertissements.

Vous pouvez maintenant injecter `result.recognitionText` dans votre logique métier — le stocker, l’indexer ou le transmettre à un autre service.

## Common Issues and Solutions

| Problème | Cause | Solution |
|----------|-------|----------|
| **Caractères indésirables** | Langue sélectionnée incorrecte | Définissez l’énumération `Language` correcte (par ex., `Language.Fra` pour le français). |
| **Aucun texte retourné** | La zone de reconnaissance ne couvre pas le texte | Ajustez les coordonnées du `Rectangle` ou supprimez `RecognitionAreas` pour traiter l’image entière. |
| **Performance lente** | Image très grande ou haute résolution | Réduisez la taille de l’image avant l’OCR ou augmentez l’allocation de mémoire pour la JVM. |
| **Avertissements concernant un format non pris en charge** | Format d’image non reconnu | Convertissez l’image en PNG, JPEG ou TIFF avant le traitement. |

## FAQ

**Q : Puis‑je reconnaître plusieurs langues en un seul appel OCR ?**  
R : Oui. Utilisez `settings.setLanguage(Language.Eng | Language.Fra)` pour activer la reconnaissance multilingue.

**Q : Quels formats d’image Aspose.OCR prend‑il en charge ?**  
R : PNG, JPEG, BMP, TIFF, GIF et plusieurs autres. Fournissez simplement le chemin de fichier correct.

**Q : Existe‑t‑il une limite de taille pour l’image ?**  
R : Il n’y a pas de limite stricte, mais les très grandes images augmentent l’utilisation de mémoire et le temps de traitement. Envisagez de redimensionner les gros fichiers.

**Q : Comment obtenir une licence de production ?**  
R : Achetez une licence sur le site Aspose et appliquez‑la via la classe `License` comme indiqué dans la documentation Aspose.

**Q : Puis‑je extraire du texte d’une page PDF directement ?**  
R : Pas directement avec Aspose.OCR. Convertissez d’abord la page PDF en image (par ex., avec Aspose.PDF) puis exécutez l’OCR.

## Conclusion

Vous avez maintenant vu comment **extraire du texte d’une image** en utilisant Aspose.OCR pour Java tout en sélectionnant la langue appropriée et en limitant la reconnaissance à des régions spécifiques. Cette approche fournit une OCR précise et haute performance qui peut être intégrée à n’importe quel flux de travail basé sur Java — des systèmes de gestion de documents aux pipelines de capture de données. Prêt à avancer ? Essayez de changer l’énumération de langue, expérimentez différentes zones de reconnaissance et intégrez les résultats dans votre propre logique d’application.

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}