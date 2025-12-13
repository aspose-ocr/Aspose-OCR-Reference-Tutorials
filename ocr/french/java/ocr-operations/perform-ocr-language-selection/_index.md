---
date: 2025-12-13
description: Apprenez à extraire du texte d’une image à l’aide d’Aspose.OCR pour Java
  avec sélection de la langue. Ce tutoriel pas à pas d’Aspose OCR Java montre une
  configuration OCR précise.
linktitle: How to Extract Text from Image with Language Selection Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Comment extraire du texte d’une image avec sélection de langue en utilisant
  Aspose.OCR
url: /fr/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment extraire du texte d'une image avec sélection de langue à l'aide d'Aspose.OCR

## Introduction

Extraire du texte à partir de fichiers image est une exigence courante, que vous numérisiez des documents scannés, traitiez des reçus ou construisiez des archives consultables. Aspose.OCR pour Java rend cette tâche simple et vous offre un contrôle fin sur la sélection de la langue, la correction de l’inclinaison et les zones de reconnaissance. Dans ce tutoriel, nous parcourrons un exemple complet et pratique qui montre **comment extraire du texte d'une image** avec un paramètre de langue spécifique, afin que vous puissiez intégrer un OCR fiable dans vos applications Java dès aujourd’hui.

## Quick Answers
- **Quelle bibliothèque gère l’OCR en Java ?** Aspose.OCR pour Java  
- **Quel paramètre sélectionne la langue ?** `settings.setLanguage(Language.Eng)` (ou toute langue prise en charge)  
- **Ai‑je besoin d’une licence pour le développement ?** Une licence d’évaluation gratuite fonctionne pour les tests ; une licence commerciale est requise pour la production.  
- **Puis‑je limiter l’OCR à une région de l’image ?** Oui, utilisez `RecognitionSettings.setRecognitionAreas()` avec des rectangles.  
- **Quel est le temps d’exécution typique ?** Quelques secondes par page sur un ordinateur portable standard, selon la taille de l’image et la complexité de la langue.

## Qu’est‑ce que « extraire du texte d’une image » ?
L’extraction de texte d’une image (OCR) convertit la représentation visuelle des caractères en chaînes lisibles par machine. Cela permet la recherche, l’analyse et les flux de travail d’extraction de données qui nécessiteraient autrement une transcription manuelle.

## Pourquoi utiliser Aspose.OCR avec sélection de langue ?
- **Prise en charge multilingue** – Choisissez la ou les langues exactes présentes dans votre image pour augmenter la précision.  
- **Contrôle fin** – Ajustez l’inclinaison, définissez des zones de reconnaissance et configurez le comportement d’auto‑inclinaison.  
- **API pure Java** – Sans dépendances natives, facile à intégrer dans n’importe quel projet Java.  
- **Données de résultat riches** – Obtenez du texte brut, du JSON, des rectangles de délimitation et des avertissements en un seul appel.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- **Java Development Kit (JDK)** installé (JDK 8 ou supérieur).  
- **Aspose.OCR pour Java** – téléchargez‑le depuis le site officiel [ici](https://reference.aspose.com/ocr/java/).  
- Un fichier image contenant le texte que vous souhaitez extraire, par ex. `p3.png`.

## Import Packages

Dans votre fichier source Java, incluez les classes Aspose.OCR requises ainsi que les utilitaires Java standards :

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

## Guide étape par étape

### Étape 1 : Configurer votre répertoire de documents

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Remplacez `"Your Document Directory"` par le chemin absolu où se trouve `p3.png`.

### Étape 2 : Définir le chemin de l’image

```java
// The image path
String file = dataDir + "p3.png";
```

Assurez‑vous que la variable `file` pointe vers l’image exacte que vous souhaitez traiter.

### Étape 3 : Créer une instance de l’API Aspose.OCR

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

L’objet `AsposeOCR` vous donne accès à toutes les opérations OCR.

### Étape 4 : Définir les options de reconnaissance (sélection de langue)

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

1. Désactivons l’auto‑inclinaison car nous fournissons une valeur d’inclinaison manuelle.  
2. Définissons une région rectangulaire (`RecognitionAreas`) pour limiter l’OCR à la partie de l’image contenant réellement du texte.  
3. Fixons la **langue** sur l’anglais (`Language.Eng`). Changez‑la en `Language.Fra`, `Language.Spa`, etc., selon votre image source.

### Étape 5 : Exécuter l’OCR et récupérer les résultats

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

L’appel `RecognizePage` lance le moteur OCR en utilisant l’image et les paramètres que vous avez définis. Le résultat est stocké dans un objet `RecognitionResult`.

### Étape 6 : Afficher et exploiter les résultats

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
- Les coordonnées des rectangles de délimitation.  
- Une représentation JSON pour un traitement en aval simplifié.  
- L’angle d’inclinaison détecté et les éventuels avertissements.

Vous pouvez maintenant injecter `result.recognitionText` dans votre logique métier — le stocker, l’indexer ou le transmettre à un autre service.

## Problèmes courants et solutions

| Problème | Cause | Solution |
|----------|-------|----------|
| **Caractères illisibles** | Mauvaise langue sélectionnée | Définissez le bon enum `Language` (par ex., `Language.Fra` pour le français). |
| **Aucun texte retourné** | La zone de reconnaissance ne couvre pas le texte | Ajustez les coordonnées du `Rectangle` ou supprimez `RecognitionAreas` pour traiter l’image entière. |
| **Performance lente** | Image très grande ou haute résolution | Réduisez la taille de l’image avant l’OCR ou augmentez l’allocation mémoire du JVM. |
| **Avertissements de format non pris en charge** | Format d’image non reconnu | Convertissez l’image en PNG, JPEG ou TIFF avant le traitement. |

## FAQ

**Q : Puis‑je reconnaître plusieurs langues en un seul appel OCR ?**  
R : Oui. Utilisez `settings.setLanguage(Language.Eng | Language.Fra)` pour activer la reconnaissance multilingue.

**Q : Quels formats d’image Aspose.OCR prend‑il en charge ?**  
R : PNG, JPEG, BMP, TIFF, GIF et plusieurs autres. Fournissez simplement le chemin de fichier correct.

**Q : Existe‑t‑il une limite de taille pour l’image ?**  
R : Il n’y a pas de limite stricte, mais les images très volumineuses augmentent l’utilisation mémoire et le temps de traitement. Envisagez de redimensionner les gros fichiers.

**Q : Comment obtenir une licence de production ?**  
R : Achetez une licence sur le site Aspose et appliquez‑la via la classe `License` comme indiqué dans la documentation Aspose.

**Q : Puis‑je extraire du texte directement d’une page PDF ?**  
R : Pas directement avec Aspose.OCR. Convertissez d’abord la page PDF en image (par ex., avec Aspose.PDF) puis lancez l’OCR.

## Conclusion

Vous avez maintenant vu comment **extraire du texte d’une image** à l’aide d’Aspose.OCR pour Java tout en sélectionnant la langue appropriée et en limitant la reconnaissance à des régions spécifiques. Cette approche offre un OCR précis et performant qui peut être intégré à n’importe quel flux de travail basé sur Java — des systèmes de gestion documentaire aux pipelines de capture de données.

---

**Dernière mise à jour :** 2025-12-13  
**Testé avec :** Aspose.OCR 24.11 pour Java  
**Auteur :** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}