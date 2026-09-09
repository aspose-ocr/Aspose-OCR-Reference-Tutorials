---
date: 2026-02-09
description: Apprenez à convertir une image en texte et à extraire les rectangles
  des zones de texte à l’aide de la bibliothèque Aspose OCR Java. Guide étape par
  étape avec des exemples de code.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Convertir une image en texte – Reconnaître le texte à partir d’une image et
  récupérer les rectangles des zones de texte
url: /fr/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir une image en texte – Reconnaître le texte d’une image et récupérer les rectangles des zones de texte

## Introduction

Si vous devez **convertir une image en texte** et **reconnaître le texte d’une image** dans une application Java, Aspose.OCR for Java offre une méthode rapide et précise pour le faire. Dans ce tutoriel, nous parcourrons les étapes exactes nécessaires pour extraire les paragraphes d’une image, obtenir les rectangles englobants pour chaque zone de texte, et afficher ces coordonnées dans la console. À la fin, vous comprendrez pourquoi cette approche fonctionne, comment intégrer la bibliothèque, et où vous pouvez l’étendre pour vos propres cas d’utilisation.

## Quick Answers
- **Que signifie « reconnaître le texte d’une image » ?** Cela signifie convertir les caractères visuels d’une image en données de chaîne éditables.  
- **Quelle bibliothèque gère cela en Java ?** Aspose.OCR for Java.  
- **Ai-je besoin d’une licence pour le développement ?** Une licence temporaire est disponible pour les tests ; une licence complète est requise pour la production.  
- **Puis‑je extraire des paragraphes au lieu de mots uniques ?** Oui – utilisez `AreasType.PARAGRAPHS` pour obtenir des rectangles au niveau des paragraphes.  
- **Le code est‑il compatible avec Java 11+ ?** Absolument, l’API fonctionne avec Java 11 et versions ultérieures.

## What is “convert image to text” in Aspose.OCR?

Aspose.OCR’s `RecognizePage` method analyses the bitmap, applies OCR algorithms, and returns the recognized string. When you request text areas, the library also calculates the exact `Rectangle` coordinates for each block of text, making it easy to highlight or process specific sections later.

## Why use this **java ocr library**?
- **Haute précision** – prend en charge plusieurs langues et des polices complexes.  
- **Intégration facile** – un seul JAR ajoute toutes les capacités OCR.  
- **Sortie flexible** – vous pouvez récupérer du texte brut, du HTML formaté, ou des rectangles précis des zones de texte.  
- **Thread‑safe** – adapté aux environnements serveur à haut débit.

## Prerequisites

- **Kit de développement Java** (JDK 11 ou plus récent) installé sur votre machine.  
- **Bibliothèque Aspose.OCR for Java** – téléchargez‑la depuis le site officiel [here](https://releases.aspose.com/ocr/java/).  
- Un IDE ou un outil de construction (Maven/Gradle) pour gérer la dépendance JAR.

## Import Packages

Dans votre projet Java, importez les classes nécessaires :

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Step‑by‑Step Guide

### Step 1: Set Up Your Project
Créez un nouveau projet Java (ou ajoutez‑le à un projet existant) et placez le JAR Aspose.OCR sur le classpath. Si vous utilisez Maven, ajoutez la dépendance comme décrit dans le package de téléchargement.

### Step 2: Define Document Directory and Image Path
Spécifiez l’emplacement de votre image d’exemple :

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Step 3: Create Aspose.OCR Instance
Instanciez le moteur OCR :

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Step 4: Recognize Text in the Image
Appelez `RecognizePage` pour convertir l’image en texte brut. Cette étape montre la capacité principale de **reconnaître le texte d’une image en Java** :

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Step 5: Get Rectangles with Text Areas
Récupérez maintenant les rectangles englobants pour chaque paragraphe (ou autre type de zone). C’est ici que vous **extrayez des paragraphes d’une image** et obtenez leurs coordonnées :

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Common Issues & Troubleshooting

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `IOException` on `RecognizePage` | Chemin de fichier incorrect ou permission de lecture manquante | Vérifiez que `imagePath` pointe vers un PNG/JPG existant et que l’application a accès au système de fichiers. |
| Chaîne de résultat vide | Image de mauvaise qualité ou langue non prise en charge | Pré‑traitez l’image (augmentez le contraste, binarisez) ou spécifiez la langue correcte avec `api.setLanguage("eng")`. |
| Aucun rectangle retourné | Utilisation du mauvais `AreasType` (par ex., `WORDS` alors que vous attendez des paragraphes) | Passez à `AreasType.PARAGRAPHS` ou `AreasType.LINES` selon le besoin. |

## Frequently Asked Questions

**Q : Aspose.OCR est‑il compatible avec Java 11 ?**  
A : Oui, Aspose.OCR fonctionne avec Java 11 et les versions ultérieures.

**Q : Puis‑je utiliser Aspose.OCR pour des projets personnels et commerciaux ?**  
A : Oui, vous pouvez l’utiliser dans tout type de projet. Pour les détails de licence, visitez [here](https://purchase.aspose.com/buy).

**Q : Comment obtenir une licence temporaire pour l’évaluation ?**  
A : Vous pouvez obtenir une licence temporaire [here](https://purchase.aspose.com/temporary-license/).

**Q : Où puis‑je trouver le support communautaire ou l’assistance officielle ?**  
A : Pour le support et les discussions, visitez le [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).

**Q : Aspose.OCR prend‑il en charge le multithreading ?**  
A : Oui, la bibliothèque est thread‑safe et peut être utilisée dans des environnements concurrents pour de meilleures performances.

## Conclusion

Dans ce **tutoriel Aspose OCR Java** vous avez appris comment **convertir une image en texte** en utilisant Aspose.OCR for Java, extraire des paragraphes, et récupérer les rectangles exacts qui entourent chaque bloc de texte. Ces capacités vous permettent de créer des PDF recherchables, de mettre en évidence du texte dans des superpositions UI, ou d’alimenter des processus en aval avec des données structurées. Explorez davantage l’API pour personnaliser les paramètres de langue, gérer différents formats d’image, ou intégrer le stockage cloud.

---

**Last Updated:** 2026-02-09  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}