---
date: 2025-12-10
description: Apprenez à reconnaître le texte à partir d’une image et à extraire les
  paragraphes d’une image en utilisant Aspose.OCR pour Java. Guide étape par étape
  avec des exemples de code.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Reconnaître le texte à partir d'une image et récupérer les rectangles des zones
  de texte
url: /fr/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Reconnaître le texte à partir d'une image et récupérer les rectangles des zones de texte

## Introduction

Si vous devez **recognize text from image** des fichiers image dans une application Java, Aspose.OCR for Java offre une méthode rapide et précise pour le faire. Dans ce tutoriel, nous parcourrons les étapes exactes nécessaires pour extraire des paragraphes d’une image, obtenir les rectangles englobants de chaque zone de texte et afficher ces coordonnées dans la console. À la fin, vous comprendrez pourquoi cette approche fonctionne, comment intégrer la bibliothèque et où vous pouvez l’étendre pour vos propres cas d’utilisation.

## Réponses rapides
- **What does “recognize text from image” mean?** Cela signifie convertir les caractères visuels d’une image en données de chaîne éditables.  
- **Which library handles this in Java?** Aspose.OCR for Java.  
- **Do I need a license for development?** Une licence temporaire est disponible pour les tests ; une licence complète est requise pour la production.  
- **Can I extract paragraphs instead of single words?** Oui – utilisez `AreasType.PARAGRAPHS` pour obtenir des rectangles au niveau des paragraphes.  
- **Is the code compatible with Java 11+?** Absolument, l’API fonctionne avec Java 11 et les versions ultérieures.

## Qu’est‑ce que “recognize text from image” dans Aspose.OCR ?

La méthode `RecognizePage` d’Aspose.OCR analyse le bitmap, applique les algorithmes OCR et renvoie la chaîne reconnue. Lorsque vous demandez les zones de texte, la bibliothèque calcule également les coordonnées exactes du `Rectangle` pour chaque bloc de texte, ce qui facilite la mise en évidence ou le traitement de sections spécifiques ultérieurement.

## Pourquoi utiliser Aspose.OCR pour Java ?

- **High accuracy** – prend en charge plusieurs langues et des polices complexes.  
- **Easy integration** – Intégration facile – un seul JAR ajoute toutes les capacités OCR.  
- **Flexible output** – Sortie flexible – vous pouvez récupérer du texte brut, du HTML formaté ou des rectangles précis des zones de texte.  
- **Thread‑safe** – Thread‑safe – adapté aux environnements serveur à haut débit.

## Prerequisites

- **Java Development Kit** (JDK 11 ou plus récent) installé sur votre machine.  
- **Aspose.OCR for Java** library – téléchargez-le depuis le site officiel [here](https://releases.aspose.com/ocr/java/).  
- Un IDE ou un outil de construction (Maven/Gradle) pour gérer la dépendance JAR.

## Importer les packages

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

## Guide étape par étape

### Étape 1 : Configurer votre projet
Créez un nouveau projet Java (ou ajoutez‑en un existant) et placez le JAR Aspose.OCR sur le classpath. Si vous utilisez Maven, ajoutez la dépendance comme décrit dans le package de téléchargement.

### Étape 2 : Définir le répertoire du document et le chemin de l’image
Spécifiez où se trouve votre image d’exemple :

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Étape 3 : Créer une instance Aspose.OCR
Instanciez le moteur OCR :

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Étape 4 : Reconnaître le texte dans l’image
Appelez `RecognizePage` pour convertir l’image en texte brut. Cette étape montre la fonctionnalité principale **recognize text from image** :

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Étape 5 : Obtenir les rectangles avec les zones de texte
Récupérez maintenant les rectangles englobants pour chaque paragraphe (ou d’autres types de zones). C’est ici que vous **extract paragraphs from image** et obtenez leurs coordonnées :

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Problèmes courants et dépannage

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `IOException` on `RecognizePage` | Chemin de fichier incorrect ou permission de lecture manquante | Vérifiez que `imagePath` pointe vers un PNG/JPG existant et que l’application a accès au système de fichiers. |
| Empty result string | Image de mauvaise qualité ou langue non prise en charge | Pré‑traitez l’image (augmentez le contraste, binarisez) ou spécifiez la langue correcte avec `api.setLanguage("eng")`. |
| No rectangles returned | Utilisation du mauvais `AreasType` (par ex., `WORDS` alors que vous attendez des paragraphes) | Passez à `AreasType.PARAGRAPHS` ou `AreasType.LINES` selon le besoin. |

## Questions fréquentes

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

Dans ce tutoriel, vous avez appris comment **recognize text from image** des fichiers en utilisant Aspose.OCR pour Java, extraire des paragraphes et récupérer les rectangles exacts qui entourent chaque bloc de texte. Ces capacités vous permettent de créer des PDF recherchables, de mettre en évidence du texte dans des superpositions UI, ou d’alimenter des processus en aval avec des données structurées. Explorez davantage l’API pour personnaliser les paramètres de langue, gérer différents formats d’image ou intégrer le stockage cloud.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}