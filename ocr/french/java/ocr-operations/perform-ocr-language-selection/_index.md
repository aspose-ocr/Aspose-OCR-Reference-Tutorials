---
title: Exécution de l'OCR avec la sélection de la langue dans Aspose.OCR
linktitle: Exécution de l'OCR avec la sélection de la langue dans Aspose.OCR
second_title: API Java Aspose.OCR
description: Débloquez une extraction précise du texte à partir d’images avec Aspose.OCR pour Java. Suivez notre guide étape par étape pour une OCR précise avec sélection de la langue.
weight: 11
url: /fr/java/ocr-operations/perform-ocr-language-selection/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exécution de l'OCR avec la sélection de la langue dans Aspose.OCR

## Introduction

Dans un paysage technologique en constante évolution, la reconnaissance optique de caractères (OCR) joue un rôle central dans l’extraction d’informations significatives à partir des images. Aspose.OCR for Java se distingue comme un outil puissant qui permet aux développeurs d'intégrer de manière transparente les fonctionnalités OCR dans leurs applications Java. Dans ce guide étape par étape, nous explorerons comment effectuer une OCR avec sélection de langue à l'aide d'Aspose.OCR, libérant ainsi le potentiel de traiter divers contenus avec précision.

## Conditions préalables

Avant de plonger dans le didacticiel, assurez-vous que les conditions préalables suivantes sont remplies :

- Environnement de développement Java : assurez-vous que Java est installé sur votre système et que votre environnement de développement est configuré.

-  Bibliothèque Aspose.OCR : téléchargez et installez la bibliothèque Aspose.OCR pour Java. Vous pouvez trouver la bibliothèque et la documentation associée[ici](https://reference.aspose.com/ocr/java/).

- Fichier image : préparez un fichier image contenant le texte que vous souhaitez extraire. Par exemple, utilisons un fichier nommé "p3.png".

## Importer des packages

Dans votre projet Java, importez les packages nécessaires pour exploiter la fonctionnalité Aspose.OCR. Ajoutez les lignes suivantes au début de votre fichier Java :

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

## Étape 1 : Configurez votre répertoire de documents

```java
// Le chemin d'accès au répertoire des documents.
String dataDir = "Your Document Directory";
```

Remplacez « Votre répertoire de documents » par le chemin réel du répertoire où se trouve votre fichier image.

## Étape 2 : définir le chemin de l'image

```java
// Le chemin des images
String file = dataDir + "p3.png";
```

Ajustez la variable de fichier pour qu'elle pointe vers votre fichier image spécifique.

## Étape 3 : Créer une instance d'API Aspose.OCR

```java
// Créer une instance d'API
AsposeOCR api = new AsposeOCR();
```

Initialisez l'objet AsposeOCR pour accéder à ses fonctionnalités.

## Étape 4 : Définir les options de reconnaissance

```java
// Définir les options de reconnaissance
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Personnalisez les paramètres de reconnaissance en fonction de vos besoins. Ajustez les paramètres tels que l’inclinaison, la langue et les zones de reconnaissance.

## Étape 5 : Effectuer l'OCR et récupérer les résultats

```java
// Obtenir l'objet de résultat
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

Exécutez l’opération OCR à l’aide du fichier image et des paramètres spécifiés. Capturez le résultat dans l'objet RecognitionResult.

## Étape 6 : Imprimer et utiliser les résultats

```java
// Résultat d'impression
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

Imprimez le texte extrait, les zones de reconnaissance, la représentation JSON, l'angle d'inclinaison et les avertissements éventuels. Utilisez les résultats selon vos besoins dans votre candidature.

## Conclusion

Dans ce didacticiel, nous avons approfondi l'intégration transparente d'Aspose.OCR pour Java pour effectuer une OCR avec sélection de langue. Cette puissante bibliothèque ouvre un monde de possibilités aux développeurs souhaitant extraire avec précision le texte des images.

## FAQ

### Q1 : Puis-je utiliser Aspose.OCR pour plusieurs langues en un seul processus de reconnaissance ?

A1 : Oui, vous pouvez définir plusieurs langues dans RecognitionSettings pour améliorer la précision de la reconnaissance du contenu multilingue.

### Q2 : Comment puis-je gérer différents formats d'image avec Aspose.OCR ?

A2 : Aspose.OCR prend en charge divers formats d'image, notamment PNG, JPEG et TIFF. Fournissez simplement le chemin de fichier correct dans la variable de chemin d'image.

### Q3 : Y a-t-il une limite à la taille de l’image qu’Aspose.OCR peut traiter ?

A3 : Aspose.OCR peut gérer des images de différentes tailles, mais des images plus grandes peuvent nécessiter plus de temps de traitement et de ressources.

### Q4 : Puis-je affiner les paramètres de reconnaissance pour des régions spécifiques d’une image ?

A4 : Absolument. Utilisez la fonctionnalité RecognitionAreas pour définir des rectangles spécifiques dans l'image pour une reconnaissance ciblée.

### Q5 : Aspose.OCR est-il adapté aux projets personnels et commerciaux ?

A5 : Oui, Aspose.OCR offre des options de licence flexibles, ce qui le rend adapté à un usage personnel et commercial.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
