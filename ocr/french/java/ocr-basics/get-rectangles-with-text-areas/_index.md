---
date: 2026-06-19
description: Apprenez comment convertir une image en texte en Java, extraire les paragraphes
  d'une image et récupérer les rectangles des zones de texte à l'aide de la bibliothèque
  Aspose OCR Java.
keywords:
- image to text java
- convert scanned image text
- extract paragraphs from image
- aspose ocr java tutorial
linktitle: Image to Text Java – Reconnaître le texte à partir de l'image et récupérer
  les rectangles des zones de texte
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  headline: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  type: TechArticle
- description: Learn how to convert image to text in Java, extract paragraphs from
    image, and retrieve text area rectangles using Aspose OCR Java library.
  name: Image to Text Java – Convert Image to Text and Retrieve Text Area Rectangles
  steps:
  - name: Set Up Your Project
    text: Create a new Java project (or add to an existing one) and place the Aspose.OCR
      JAR on the classpath. If you use Maven, add the dependency as described in the
      download package.
  - name: Define Document Directory and Image Path
    text: 'Specify where your sample image resides:'
  - name: Create AsposeOCR Instance
    text: '`AsposeOCR` is the main class that provides OCR functionality. Instantiate
      the OCR engine:'
  - name: Recognize Text in the Image
    text: Load your image and call `RecognizePage` to convert the picture into plain
      text. This single method call performs image preprocessing, character segmentation,
      and language‑specific recognition in one step.
  - name: Get Rectangles with Text Areas
    text: Retrieve the bounding rectangles for each paragraph (or other area types).
      This step returns a collection of `Rectangle` objects that precisely enclose
      the detected text blocks, enabling you to highlight or further process individual
      sections. CODE_BLOCK_PLACEHOLDER_5_END
  type: HowTo
- questions:
  - answer: Yes, Aspose.OCR works with Java 11 and later versions.
    question: Is Aspose.OCR compatible with Java 11?
  - answer: Yes, you can use it in any type of project. For licensing details, visit
      [here](https://purchase.aspose.com/buy).
    question: Can I use Aspose.OCR for both personal and commercial projects?
  - answer: You can obtain a temporary license [here](https://purchase.aspose.com/temporary-license/).
    question: How do I obtain a temporary license for evaluation?
  - answer: For support and discussions, visit the [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).
    question: Where can I find community support or official assistance?
  - answer: Yes, the library is thread‑safe and can be used in concurrent environments
      for better performance.
    question: Does Aspose.OCR support multithreading?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Image to Text Java – Convertir l'image en texte et récupérer les rectangles
  des zones de texte
url: /fr/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Image en texte Java – Convertir une image en texte et récupérer les rectangles des zones de texte

## Introduction

Si vous devez **convertir une image en texte** dans une application Java, Aspose.OCR for Java fournit une solution rapide et précise. Dans ce tutoriel, nous parcourrons les étapes exactes nécessaires pour extraire des paragraphes d’une image, obtenir les rectangles englobants de chaque zone de texte et afficher ces coordonnées dans la console. À la fin, vous comprendrez pourquoi cette approche fonctionne, comment intégrer la bibliothèque et où vous pouvez l’étendre pour vos propres cas d’utilisation.

## Réponses rapides
`AreasType` est une énumération qui spécifie le niveau de segmentation du texte (mots, lignes, paragraphes).

- **Que signifie « reconnaître du texte à partir d’une image » ?** Cela signifie convertir les caractères visuels d’une image en données de chaîne modifiables.  
- **Quelle bibliothèque gère cela en Java ?** Aspose.OCR for Java.  
- **Ai-je besoin d’une licence pour le développement ?** Une licence temporaire est disponible pour les tests ; une licence complète est requise pour la production.  
- **Puis-je extraire des paragraphes au lieu de mots uniques ?** Oui – utilisez `AreasType.PARAGRAPHS` pour obtenir des rectangles au niveau des paragraphes.  
- **Le code est‑il compatible avec Java 11+ ?** Absolument, l’API fonctionne avec Java 11 et les versions ultérieures.

## Qu’est-ce que « convertir une image en texte » dans Aspose.OCR ?

`convert image to text` fait référence au processus d’analyse d’un bitmap, d’application d’algorithmes OCR et de renvoi des caractères reconnus sous forme de chaîne. La méthode `RecognizePage` d’Aspose.OCR effectue cette conversion tout en fournissant éventuellement les coordonnées exactes du `Rectangle` pour chaque bloc de texte détecté.

## Pourquoi utiliser cette **bibliothèque OCR Java** ?

Aspose.OCR prend en charge **plus de 30 langues** et peut traiter des images jusqu’à **50 Mo** sans charger le fichier complet en mémoire, offrant des temps de réponse inférieurs à une seconde sur du matériel serveur typique. La bibliothèque est thread‑safe, ne nécessite qu’un seul JAR et propose des formats de sortie flexibles — y compris du texte brut, du HTML et des rectangles précis des zones de texte — ce qui la rend idéale pour les scénarios d’entreprise à haut débit.

## Prérequis

- **Java Development Kit** (JDK 11 ou plus récent) installé sur votre machine.  
- Bibliothèque **Aspose.OCR for Java** – téléchargez‑la depuis le site officiel [ici](https://releases.aspose.com/ocr/java/).  
- Un IDE ou un outil de construction (Maven/Gradle) pour gérer la dépendance JAR.

## Importer les packages

In your Java project, import the necessary classes:

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

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Étape 2 : Définir le répertoire du document et le chemin de l’image
Specify where your sample image resides:

```java
// Create AsposeOCR instance
AsposeOCR api = new AsposeOCR();
```

### Étape 3 : Créer une instance AsposeOCR
`AsposeOCR` is the main class that provides OCR functionality.

Instantiate the OCR engine:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Étape 4 : Reconnaître le texte dans l’image
Load your image and call `RecognizePage` to convert the picture into plain text. This single method call performs image preprocessing, character segmentation, and language‑specific recognition in one step.

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

### Étape 5 : Obtenir les rectangles des zones de texte
Retrieve the bounding rectangles for each paragraph (or other area types). This step returns a collection of `Rectangle` objects that precisely enclose the detected text blocks, enabling you to highlight or further process individual sections.

CODE_BLOCK_PLACEHOLDER_5_END

## Problèmes courants et dépannage

| Symptôme | Cause probable | Solution |
|----------|----------------|----------|
| `IOException` sur `RecognizePage` | Chemin de fichier incorrect ou permission de lecture manquante | Vérifiez que `imagePath` pointe vers un PNG/JPG existant et que l’application a accès au système de fichiers. |
| Chaîne de résultat vide | Image de mauvaise qualité ou langue non prise en charge | Pré‑traitez l’image (augmentez le contraste, binarisez) ou spécifiez la bonne langue avec `api.setLanguage("eng")`. |
| Aucun rectangle retourné | Utilisation du mauvais `AreasType` (par ex., `WORDS` au lieu de paragraphes) | Passez à `AreasType.PARAGRAPHS` ou `AreasType.LINES` selon le besoin. |

## Questions fréquemment posées

**Q : Aspose.OCR est‑il compatible avec Java 11 ?**  
R : Oui, Aspose.OCR fonctionne avec Java 11 et les versions ultérieures.

**Q : Puis‑je utiliser Aspose.OCR pour des projets personnels et commerciaux ?**  
R : Oui, vous pouvez l’utiliser dans tout type de projet. Pour les détails de licence, visitez [ici](https://purchase.aspose.com/buy).

**Q : Comment obtenir une licence temporaire pour l’évaluation ?**  
R : Vous pouvez obtenir une licence temporaire [ici](https://purchase.aspose.com/temporary-license/).

**Q : Où puis‑je trouver le support communautaire ou l’assistance officielle ?**  
R : Pour le support et les discussions, visitez le [forum Aspose.OCR](https://forum.aspose.com/c/ocr/16).

**Q : Aspose.OCR prend‑il en charge le multithreading ?**  
R : Oui, la bibliothèque est thread‑safe et peut être utilisée dans des environnements concurrents pour de meilleures performances.

## Conclusion

Dans ce **tutoriel Aspose OCR Java** vous avez appris comment **convertir une image en texte** en utilisant Aspose.OCR pour Java, extraire des paragraphes et récupérer les rectangles exacts qui entourent chaque bloc de texte. Ces capacités vous permettent de créer des PDF recherchables, de mettre en surbrillance du texte dans des superpositions UI, ou d’alimenter des processus en aval avec des données structurées. Explorez davantage l’API pour personnaliser les paramètres de langue, gérer différents formats d’image ou intégrer le stockage cloud.

---

**Dernière mise à jour :** 2026-06-19  
**Testé avec :** Aspose.OCR 23.10 for Java  
**Auteur :** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés

- [Extraire du texte d’images – Bases de l’OCR avec Aspose.OCR pour Java](/ocr/java/ocr-basics/)
- [Extraire du texte d’une image Java avec le mode Détection des zones d’Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Convertir une image en texte en Java en utilisant Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}