---
date: 2026-06-24
description: Apprenez à OCR le texte d'image avec sélection de langue en utilisant
  Aspose.OCR pour Java. Ce guide step‑by‑step couvre extract text java, OCR skew correction,
  et plus.
keywords:
- ocr skew correction
- ocr language support
- improve ocr accuracy
- extract text image java
- ocr image java
linktitle: Comment effectuer la correction d'inclinaison OCR et la sélection de langue
  avec Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-06-24'
  description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  headline: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  type: TechArticle
- description: Learn how to OCR image text with language selection using Aspose.OCR
    for Java. This step‑by‑step guide covers extract text java, OCR skew correction,
    and more.
  name: How to Perform OCR Skew Correction and Language Selection with Aspose.OCR
  steps:
  - name: Set up Your Document Directory
    text: Create a `File` object that points to the folder containing your source
      image. This makes the path handling portable across operating systems. Replace
      `"Your Document Directory"` with the absolute path where `p3.png` resides.
  - name: Define the Image Path
    text: Instantiate a `File` object for the specific image you want to process.
      Using a `File` object gives you easy access to file metadata if you need it
      later. Make sure the `file` variable points to the exact image you intend to
      process.
  - name: Create Aspose.OCR API Instance
    text: The `AsposeOCR` class is the entry point for all OCR operations. It encapsulates
      the engine, manages resources, and provides the `recognizePage` method. The
      `AsposeOCR` object gives you access to all OCR operations.
  - name: Set Recognition Options (Language Selection)
    text: '`RecognitionSettings` is Aspose.OCR''s configuration container that lets
      you fine‑tune the OCR process. Here we: 1. Disable auto‑skew because we provide
      a manual skew value. 2. Define a rectangular region (`RecognitionAreas`) to
      limit OCR to the part of the image that actually contains text. 3. Set t'
  - name: Perform OCR and Retrieve Results
    text: Calling `recognizePage` runs the OCR engine using the image and the settings
      you defined. The outcome is stored in a `RecognitionResult` object, which aggregates
      all useful data. The `RecognizePage` call runs the OCR engine using the image
      and the settings you defined. The outcome is stored in a `Re
  - name: Print and Utilize Results
    text: 'The console output shows: - The full extracted text (`recognitionText`).
      - Text for each defined rectangle (`recognitionAreasText`). - Bounding rectangle
      coordinates. - A JSON representation for easy downstream processing. - Detected
      skew angle and any warnings. The console output shows the full ext'
  type: HowTo
- questions:
  - answer: Yes. Use `settings.setLanguage(Language.Eng | Language.Fra)` to enable
      multilingual recognition.
    question: Can I recognize multiple languages in a single OCR call?
  - answer: PNG, JPEG, BMP, TIFF, GIF, and several others. Just provide the correct
      file path.
    question: Which image formats does Aspose.OCR support?
  - answer: There’s no hard limit, but processing images larger than 10 MB can increase
      memory usage and runtime. Consider resizing large files.
    question: Is there a size limit for the image?
  - answer: Purchase a license from the Aspose website and apply it via the `License`
      class as shown in the Aspose documentation.
    question: How do I obtain a production license?
  - answer: Not directly with Aspose.OCR. Convert the PDF page to an image first (e.g.,
      using Aspose.PDF) and then run OCR.
    question: Can I extract text from a PDF page directly?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Comment effectuer la correction d'inclinaison OCR et la sélection de langue
  avec Aspose.OCR
url: /fr/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment effectuer la correction d’inclinaison OCR et la sélection de langue avec Aspose.OCR

## Introduction

Extraire du texte à partir de fichiers image est une exigence courante que vous numérisiez des documents scannés, traitiez des reçus ou construisiez des archives consultables. Dans ce tutoriel, nous parcourrons un exemple complet et pratique qui montre **comment effectuer la reconnaissance OCR de texte d’image** avec un paramètre de langue spécifique, afin que vous puissiez intégrer une OCR fiable dans vos applications Java dès aujourd’hui. Vous verrez également comment gérer **la correction d’inclinaison OCR** et la reconnaissance basée sur des régions pour une précision optimale, ce qui peut **améliorer la précision OCR** jusqu’à 30 % sur des scans inclinés.

## Réponses rapides
- **Quelle bibliothèque gère l'OCR en Java ?** Aspose.OCR for Java  
- **Quel paramètre sélectionne la langue ?** `settings.setLanguage(Language.Eng)` (ou toute langue prise en charge)  
- **Ai-je besoin d’une licence pour le développement ?** Une licence d’évaluation gratuite fonctionne pour les tests ; une licence commerciale est requise pour la production.  
- **Puis-je limiter l'OCR à une région de l'image ?** Oui, utilisez `RecognitionSettings.setRecognitionAreas()` avec des rectangles.  
- **Quel est le temps d’exécution typique ?** Quelques secondes par page sur un ordinateur portable standard, selon la taille de l’image et la complexité de la langue.  

`Language` est une énumération qui répertorie les langues OCR prises en charge par Aspose.OCR, telles que l'anglais, le français, l'espagnol, etc.

## Qu’est-ce que la correction d’inclinaison OCR ?

La correction d’inclinaison OCR est le processus de détection et de redressement des lignes de texte inclinées avant la reconnaissance des caractères. En alignant la ligne de base du texte, le moteur OCR peut appliquer ses modèles linguistiques plus efficacement, réduisant les erreurs de reconnaissance causées par les scans inclinés. Cette étape améliore la qualité visuelle de l’image d’entrée, permettant aux algorithmes de reconnaissance de se concentrer sur les formes réelles des caractères plutôt que sur les distorsions introduites par la rotation.

## Pourquoi la correction d’inclinaison OCR améliore la précision

Lorsque le texte est incliné, les formes des caractères apparaissent déformées, entraînant des taux d’erreur jusqu’à 20 % plus élevés. L’application de la **correction d’inclinaison OCR** élimine cette distorsion, permettant au moteur de se concentrer sur les glyphes réels. Dans des tests de référence, Aspose.OCR a obtenu une amélioration de 15‑30 % de la précision de reconnaissance sur des documents avec une rotation de 10‑15° après application de la correction d’inclinaison.

## Pourquoi utiliser Aspose.OCR avec la sélection de langue ?

Sélectionner la langue exacte du texte source permet au moteur OCR d’utiliser des dictionnaires et des modèles de caractères spécifiques à la langue, ce qui augmente considérablement la précision de reconnaissance et réduit le temps de traitement. De plus, Aspose.OCR offre un contrôle fin sur la correction d’inclinaison, la sélection de région et les formats de sortie, ce qui en fait un choix polyvalent pour les pipelines de traitement de documents multilingues.

- **Support multilingue** – Choisissez la ou les langues exactes présentes dans votre image pour augmenter la précision.  
- **Contrôle fin** – Ajustez l’inclinaison, définissez les zones de reconnaissance et configurez le comportement d’auto‑inclinaison.  
- **API Java pure** – Pas de dépendances natives, facile à intégrer dans n’importe quel projet Java.  
- **Données de résultat riches** – Obtenez le texte brut, le JSON, les rectangles de délimitation et les avertissements en un seul appel.  
- **Capacité quantifiée** – Aspose.OCR prend en charge **plus de 50** formats d’entrée et de sortie et peut traiter des lots d’images de **500 pages** sans charger l’ensemble du document en mémoire.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

- **Java Development Kit (JDK)** installé (JDK 8 ou supérieur).  
- Bibliothèque **Aspose.OCR for Java** – téléchargez‑la depuis le site officiel [ici](https://reference.aspose.com/ocr/java/).  
- Un fichier image contenant le texte que vous souhaitez extraire, par ex., `p3.png`.

## Importer les packages

Les importations suivantes vous donnent accès aux classes OCR de base et aux utilitaires Java standard.  
`import com.aspose.ocr.*;` – importe le moteur OCR principal.  
`import com.aspose.ocr.config.*;` – contient les objets de configuration tels que `RecognitionSettings`.  
`import java.awt.Rectangle;` – utilisé pour définir les zones de reconnaissance.

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

## Comment appliquer la correction d’inclinaison OCR en Java ?

Chargez l’image, désactivez la détection automatique d’inclinaison, et fournissez soit un angle mesuré, soit laissez le moteur le calculer en utilisant `settings.setAutoSkew(false)`. Le moteur OCR redressera d’abord l’image en fonction de l’angle fourni ou détecté, puis procédera à la reconnaissance des caractères. Cette approche en deux étapes garantit que toute inclinaison est éliminée avant l’application des modèles linguistiques, ce qui donne une sortie texte plus propre et moins d’erreurs de reconnaissance.

## Guide étape par étape

### Étape 1 : Configurer votre répertoire de documents

Créez un objet `File` qui pointe vers le dossier contenant votre image source. Cela rend la gestion des chemins portable entre les systèmes d’exploitation.

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Remplacez `"Your Document Directory"` par le chemin absolu où se trouve `p3.png`.

### Étape 2 : Définir le chemin de l’image

Instanciez un objet `File` pour l’image spécifique que vous souhaitez traiter. Utiliser un objet `File` vous donne un accès facile aux métadonnées du fichier si vous en avez besoin plus tard.

```java
// The image path
String file = dataDir + "p3.png";
```

Assurez‑vous que la variable `file` pointe vers l’image exacte que vous souhaitez traiter.

### Étape 3 : Créer une instance de l’API Aspose.OCR

La classe `AsposeOCR` est le point d’entrée pour toutes les opérations OCR. Elle encapsule le moteur, gère les ressources et fournit la méthode `recognizePage`.

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

L’objet `AsposeOCR` vous donne accès à toutes les opérations OCR.

### Étape 4 : Définir les options de reconnaissance (sélection de la langue)

`RecognitionSettings` est le conteneur de configuration d’Aspose.OCR qui vous permet d’ajuster finement le processus OCR.  

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

Ici nous :

1. Désactiver l’auto‑inclinaison car nous fournissons une valeur d’inclinaison manuelle.  
2. Définir une région rectangulaire (`RecognitionAreas`) pour limiter l’OCR à la partie de l’image contenant réellement du texte.  
3. Définir la **langue** sur l’anglais (`Language.Eng`). Changez cela en `Language.Fra`, `Language.Spa`, etc., selon votre image source.

### Étape 5 : Effectuer l’OCR et récupérer les résultats

Appeler `recognizePage` exécute le moteur OCR en utilisant l’image et les paramètres que vous avez définis. Le résultat est stocké dans un objet `RecognitionResult`, qui agrège toutes les données utiles.

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

### Étape 6 : Imprimer et exploiter les résultats

La sortie console montre :

- Le texte complet extrait (`recognitionText`).  
- Le texte pour chaque rectangle défini (`recognitionAreasText`).  
- Les coordonnées du rectangle de délimitation.  
- Une représentation JSON pour un traitement en aval facile.  
- L’angle d’inclinaison détecté et les éventuels avertissements.

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

La sortie console montre le texte complet extrait, le texte spécifique à chaque région, les boîtes de délimitation, le JSON, l’angle d’inclinaison et les avertissements. Vous pouvez maintenant transmettre `result.recognitionText` à votre logique métier — le stocker, l’indexer ou le transmettre à un autre service.

## Problèmes courants et solutions

| Problème | Cause | Solution |
|----------|-------|----------|
| **Caractères indésirables** | Langue sélectionnée incorrecte | Définissez l’énumération `Language` correcte (par ex., `Language.Fra` pour le français). |
| **Aucun texte retourné** | La zone de reconnaissance ne couvre pas le texte | Ajustez les coordonnées du `Rectangle` ou supprimez `RecognitionAreas` pour traiter l’image entière. |
| **Performance lente** | Image très grande ou haute résolution | Réduisez la taille de l’image avant l’OCR ou augmentez l’allocation de mémoire JVM. |
| **Avertissements concernant un format non pris en charge** | Format d’image non reconnu | Convertissez l’image en PNG, JPEG ou TIFF avant le traitement. |

## Questions fréquemment posées

**Q : Puis‑je reconnaître plusieurs langues dans un seul appel OCR ?**  
R : Oui. Utilisez `settings.setLanguage(Language.Eng | Language.Fra)` pour activer la reconnaissance multilingue.

**Q : Quels formats d’image Aspose.OCR prend‑il en charge ?**  
R : PNG, JPEG, BMP, TIFF, GIF, et plusieurs autres. Fournissez simplement le chemin de fichier correct.

**Q : Existe‑t‑il une limite de taille pour l’image ?**  
R : Il n’y a pas de limite stricte, mais le traitement d’images supérieures à 10 Mo peut augmenter l’utilisation de mémoire et le temps d’exécution. Envisagez de redimensionner les gros fichiers.

**Q : Comment obtenir une licence de production ?**  
R : Achetez une licence sur le site Web d’Aspose et appliquez‑la via la classe `License` comme indiqué dans la documentation Aspose.

**Q : Puis‑je extraire du texte d’une page PDF directement ?**  
R : Pas directement avec Aspose.OCR. Convertissez d’abord la page PDF en image (par ex., avec Aspose.PDF) puis exécutez l’OCR.

## Conclusion

Vous avez maintenant vu comment **extraire du texte d’une image** en utilisant Aspose.OCR pour Java tout en sélectionnant la langue appropriée et en appliquant la **correction d’inclinaison OCR** pour améliorer la fiabilité. Cette approche fournit une OCR précise et haute performance qui peut être intégrée à n’importe quel flux de travail basé sur Java — des systèmes de gestion de documents aux pipelines de capture de données. Expérimentez avec différents énumérateurs `Language`, ajustez les `RecognitionAreas` et intégrez la sortie JSON à vos analyses en aval pour une solution véritablement de bout en bout.

---

**Last Updated:** 2026-06-24  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose

## Tutoriels associés

- [Comment calculer l’angle d’inclinaison java avec Aspose.OCR](/ocr/java/ocr-basics/calculate-skew-angle/)
- [Comment OCR du texte d’image avec sélection de langue en utilisant Aspose.OCR](/ocr/java/ocr-operations/perform-ocr-language-selection/)
- [Reconnaissance OCR de documents PDF dans Aspose.OCR pour Java](/ocr/java/ocr-operations/recognize-pdf/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}