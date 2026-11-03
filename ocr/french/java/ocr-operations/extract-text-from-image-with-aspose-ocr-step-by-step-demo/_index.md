---
category: general
date: 2026-02-14
description: Extraire du texte d’une image avec Aspose OCR. Apprenez comment charger
  une image pour l’OCR, lire le texte d’un rectangle, et suivre ce tutoriel Aspose
  OCR en quelques minutes.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: fr
og_description: Extrayez le texte d’une image instantanément. Ce guide montre comment
  charger une image pour l’OCR, lire le texte d’un rectangle et réaliser un tutoriel
  Aspose OCR.
og_title: Extraire du texte d’une image avec Aspose OCR – Guide rapide
tags:
- Aspose
- OCR
- Java
title: Extraire du texte à partir d’une image avec Aspose OCR – Démonstration pas
  à pas
url: /fr/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extraire du texte d’une image avec Aspose OCR – Démonstration étape par étape

Vous avez déjà eu besoin d’**extraire du texte d’une image** sans savoir par où commencer ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils abordent pour la première fois la numérisation de tickets ou la vérification d’identités. La bonne nouvelle ? Avec Aspose OCR, vous pouvez charger une image, définir la région exacte où se trouve le texte, et récupérer les caractères en quelques lignes seulement.

Dans ce **aspose ocr tutorial** nous allons passer en revue tout ce dont vous avez besoin : charger l’image pour l’OCR, définir un rectangle qui indique au moteur où chercher, puis lire le texte extrait. À la fin, vous disposerez d’un programme Java exécutable qui affiche le texte de la ROI dans la console — pas de mystère, juste une solution claire et fonctionnelle.

## Ce dont vous aurez besoin

Avant de commencer, assurez‑vous d’avoir les éléments de base :

| Prérequis | Pourquoi c’est important |
|--------------|---------------------------|
| **Java JDK 8+** | Aspose OCR est fourni sous forme de bibliothèque Java ; n’importe quel JDK moderne convient. |
| **Aspose.OCR for Java** (téléchargez depuis le site Aspose ou ajoutez via Maven) | Fournit les classes `OcrEngine`, `ImageStream` et les classes associées. |
| **Un fichier image** (par ex. `receipt.jpg`) contenant du texte imprimable | Nous pointerons le moteur vers un rectangle à l’intérieur de ce fichier. |
| **IDE ou éditeur** (IntelliJ, Eclipse, VS Code…) | Vous aide à compiler et exécuter rapidement l’exemple. |

Si vous utilisez Maven, ajoutez cette dépendance à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Astuce pro :** Le numéro de version ci‑dessus est actuel en février 2026. Mettre à jour vers la dernière version vous assure d’obtenir les corrections de bugs et les améliorations de performances.

## Étape 1 – Initialiser le moteur OCR

Première chose à faire : créer une instance de `OcrEngine`. Pensez‑y comme le cerveau qui analysera les pixels.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Pourquoi le créer ainsi ? Aspose sépare le moteur (qui contient la configuration) des données d’image, vous offrant la flexibilité de réutiliser le même moteur pour plusieurs images si vous le souhaitez.

## Étape 2 – Charger l’image pour l’OCR

Nous allons maintenant **charger l’image pour l’OCR**. L’assistant `ImageStream.fromFile` lit le fichier dans un flux que Aspose peut comprendre.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Si le fichier est introuvable, le moteur lève une exception, il est donc conseillé d’envelopper cet appel dans un bloc try‑catch en production. Pour cette démonstration, nous laissons l’exception remonter — cela garde l’exemple propre.

## Étape 3 – Définir le rectangle (Lire le texte depuis le rectangle)

C’est ici que la partie **read text from rectangle** brille. Vous indiquez au moteur exactement où regarder, ce qui accélère le traitement et réduit les faux positifs.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Pourquoi un rectangle ?**  
> La plupart des documents ont des mises en page prévisibles — pensez à un ticket où le montant apparaît toujours en bas. En se concentrant sur cette tranche, le moteur OCR ignore les graphiques inutiles et améliore la précision.

**Cas limite :** Si le rectangle dépasse les limites de l’image, Aspose le tronque silencieusement, mais vous perdrez des données. Un petit contrôle de validité peut éviter cela :

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Étape 4 – Traiter l’image

Une fois tout configuré, nous demandons au moteur d’effectuer sa magie.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

L’appel `process()` renvoie un objet `OcrResult` contenant le texte extrait, les scores de confiance, et même les boîtes englobantes de chaque mot si vous en avez besoin plus tard.

## Étape 5 – Afficher le texte extrait

Enfin, imprimez le résultat. Dans une vraie application vous pourriez le stocker dans une base de données ou le transmettre à un autre service, mais pour ce tutoriel une sortie console suffit.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Sortie attendue** (en supposant que le rectangle a capturé le montant total sur un ticket) :

```
ROI text:
$12.34
```

Si la ROI est vide ou que l’image est floue, vous verrez une chaîne vide ou des caractères illisibles. Ajustez le rectangle, améliorez la qualité de l’image, ou activez les options de pré‑traitement d’Aspose (par ex. `setAutoSkewCorrection(true)`).

## Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté. Copiez‑collez‑le dans un fichier nommé `RoiDemo.java`, ajustez le chemin de l’image, puis lancez `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Vérification du résultat :** Après exécution, comparez la sortie console avec le texte réel à l’intérieur du rectangle. S’ils correspondent, vous avez réussi à **extraire du texte d’une image** avec Aspose OCR.

## Questions fréquentes & astuces

### Et si je dois traiter plusieurs ROI dans la même image ?
Créez un nouveau `Rectangle` pour chaque zone, appelez à nouveau `setRegionOfInterest`, puis relancez `process()`. Le moteur réutilise les mêmes données d’image, ce qui garde les performances rapides.

### Comment Aspose gère‑t‑il les différentes langues ou polices ?
Vous pouvez changer le modèle linguistique via `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Pour les scripts non latins, chargez le pack de langue approprié (disponible sur la page de téléchargement d’Aspose).

### La bibliothèque supporte‑t‑elle les entrées PDF ?
Oui—Aspose OCR accepte directement les flux PDF. Remplacez simplement `ImageStream.fromFile` par `ImageStream.fromPdfFile("doc.pdf")` et, si besoin, spécifiez le numéro de page.

### Puis‑je améliorer la précision sur des scans de mauvaise qualité ?
Activez le pré‑traitement :

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

Ces options nettoient le bruit et alignent le texte avant la reconnaissance.

## Conclusion

Nous venons de parcourir un **aspose ocr tutorial** complet montrant comment **extraire du texte d’une image**, **charger l’image pour l’OCR**, et **lire le texte depuis un rectangle** avec Java. Les étapes clés sont : initialiser le moteur, lui fournir une image, définir une région d’intérêt, lancer le traitement, puis afficher le résultat.

À partir d’ici, vous pouvez explorer :

* **Traitement par lots** — boucler sur un dossier de tickets et enregistrer chaque total dans une base de données.  
* **Détection dynamique de ROI** — utiliser des bibliothèques de traitement d’image (OpenCV) pour localiser automatiquement les blocs de texte.  
* **Post‑traitement** — appliquer des expressions régulières ou du fuzzy matching pour corriger les particularités de l’OCR.

Testez ces idées, ajustez le rectangle selon vos propres documents, et vous disposerez rapidement d’un pipeline d’extraction de texte robuste. Bon codage !

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}