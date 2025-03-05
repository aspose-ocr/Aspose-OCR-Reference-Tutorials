---
title: Exécution d'OCR sur une image à partir d'une URL dans Aspose.OCR pour Java
linktitle: Exécution d'OCR sur une image à partir d'une URL dans Aspose.OCR pour Java
second_title: API Java Aspose.OCR
description: Débloquez une extraction transparente de texte d’image en Java avec Aspose.OCR. OCR de haute précision avec une intégration facile.
type: docs
weight: 11
url: /fr/java/advanced-ocr-techniques/perform-ocr-image-from-url/
---
## Introduction

Bienvenue dans notre guide étape par étape sur l'exécution de la reconnaissance optique de caractères (OCR) sur une image à partir d'une URL à l'aide d'Aspose.OCR pour Java. Ce didacticiel est conçu pour vous aider à intégrer de manière transparente Aspose.OCR dans vos applications Java, vous permettant d'extraire facilement du texte à partir d'images. Aspose.OCR est une puissante bibliothèque OCR qui prend en charge divers formats d'image, ce qui en fait un outil précieux pour les applications nécessitant une extraction de texte.

## Conditions préalables

Avant de plonger dans le didacticiel, assurez-vous de disposer des prérequis suivants :

1. Environnement de développement Java : assurez-vous de disposer d'un environnement de développement Java fonctionnel configuré sur votre ordinateur.

2.  Bibliothèque Aspose.OCR : téléchargez et installez la bibliothèque Aspose.OCR pour Java. Vous pouvez trouver la bibliothèque et la documentation associée sur le[Site Web Aspose.OCR](https://reference.aspose.com/ocr/java/).

## Importer des packages

Dans votre projet Java, importez les packages nécessaires pour Aspose.OCR :

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Étape 1 : Créer une instance d'API

Initialisez une instance de la classe AsposeOCR :

```java
AsposeOCR api = new AsposeOCR();
```

## Étape 2 : Définir l'URL de l'image

Spécifiez l'URL de l'image à partir de laquelle vous souhaitez effectuer une OCR :

```java
String uri = "https://www.exemple.com/votre-image.png" ;
```

## Étape 3 : Définir les options de reconnaissance

Configurez les paramètres de reconnaissance, tels que la désactivation de l'inclinaison automatique et la définition des zones de reconnaissance :

```java
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);

// Définir des zones de reconnaissance à l'aide de rectangles
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
```

## Étape 4 : Effectuer l'OCR

Invoquez le processus de reconnaissance OCR :

```java
RecognitionResult result = null;
try {
    result = api.RecognizePageFromUri(uri, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

## Étape 5 : Imprimer les résultats

Affichez les résultats de la reconnaissance, y compris le texte extrait, le texte des zones de reconnaissance, la sortie JSON et les éventuels avertissements :

```java
System.out.println("Result: \n" + result.recognitionText + "\n\n");
System.out.println("RecognitionAreasText: \n");
for (String text : result.recognitionAreasText) {
    System.out.println(text);
}
System.out.println("JSON: \n" + result.GetJson());
System.out.println("Warnings: \n");
for (String warning : result.warnings) {
    System.out.println(warning);
}
```

Répétez ces étapes pour intégrer Aspose.OCR dans votre application Java et extraire le texte des images avec précision.

## Conclusion

En conclusion, l'utilisation d'Aspose.OCR pour Java fournit une solution robuste pour les tâches OCR, permettant aux développeurs d'extraire de manière transparente le texte des images. Le guide étape par étape garantit un processus d'intégration fluide, le rendant accessible aux développeurs de tous niveaux.

## FAQ

### Q1 : Quelle est la précision d'Aspose.OCR dans la reconnaissance du texte à partir d'images ?

A1 : Aspose.OCR offre une grande précision dans la reconnaissance de texte, en particulier lorsqu'il est configuré avec des zones de reconnaissance précises.

### Q2 : Aspose.OCR peut-il gérer plusieurs langues lors de la reconnaissance OCR ?

A2 : Oui, Aspose.OCR prend en charge la reconnaissance de texte dans plusieurs langues, offrant ainsi une polyvalence pour diverses applications.

### Q3 : Existe-t-il des considérations en matière de licence pour l'utilisation d'Aspose.OCR dans des projets commerciaux ?

A3 : Oui, assurez-vous du respect des conditions de licence Aspose.OCR pour une utilisation commerciale. Faire référence à[achat.aspose.com](https://purchase.aspose.com/buy) pour les détails de la licence.

### Q4 : Comment puis-je obtenir de l'aide pour les problèmes liés à Aspose.OCR ?

 A4 : Visitez le[Forum Aspose.OCR](https://forum.aspose.com/c/ocr/16) pour le soutien et les discussions de la communauté. Pour une assistance premium, envisagez d'acquérir une licence temporaire auprès de[Permis temporaire](https://purchase.aspose.com/temporary-license/).

### Q5 : Existe-t-il un essai gratuit disponible pour Aspose.OCR pour Java ?

 A5 : Oui, explorez les fonctionnalités d'Aspose.OCR avec l'essai gratuit disponible sur[releases.aspose.com](https://releases.aspose.com/).
