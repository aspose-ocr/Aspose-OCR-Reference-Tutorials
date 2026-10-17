---
category: general
date: 2026-03-18
description: Comment redresser rapidement une image avec Aspose OCR Java. Apprenez
  à prétraiter l'image pour l'OCR, nettoyer l'image numérisée et améliorer la précision
  de l'OCR en quelques étapes seulement.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- clean scanned image
- improve ocr accuracy
language: fr
og_description: Comment redresser une image avec Aspose OCR Java, prétraiter l'image
  pour l'OCR, nettoyer l'image numérisée et améliorer la précision de l'OCR.
og_title: Comment redresser une image pour l'OCR – Guide Java
tags:
- OCR
- Java
- Image Processing
title: Comment redresser une image pour l’OCR – Guide de prétraitement Java
url: /fr/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-java-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment redresser une image pour l'OCR – Guide de pré‑traitement Java

Vous vous êtes déjà demandé **comment redresser une image** qui provient d’un scanner avec un angle étrange ? Vous n’êtes pas seul — de nombreux développeurs rencontrent ce problème lorsqu’ils essaient d’extraire du texte de documents très illustrés. Bonne nouvelle : avec quelques lignes de Java et Aspose OCR, vous pouvez aligner, débruiter et extraire du texte propre sans effort.

Dans ce tutoriel, nous parcourrons l’ensemble du flux de travail : charger un scan bruité et tourné, appliquer un filtre de redressement, éliminer le bruit visuel, puis **extraire le texte de l’image**. À la fin, vous saurez **prétraiter une image pour l’OCR**, **nettoyer les images scannées**, et **améliorer la précision de l’OCR** pour tout projet nécessitant une extraction fiable du texte.

## Ce dont vous avez besoin

- Java 17 (ou tout JDK récent) – le code utilise les fonctionnalités standard du langage.  
- Bibliothèque Aspose OCR pour Java (l’essai gratuit suffit pour les expérimentations).  
- Une image d’exemple à la fois bruitée et tournée (par ex. `noisy-rotated.png`).  
- Votre IDE préféré (IntelliJ IDEA, Eclipse, VS Code…) – tout ce qui peut compiler du Java.

Aucun framework supplémentaire, aucune magie Maven/Gradle ; les seules instructions d’importation sont celles montrées ci‑dessous.

---

## Comment redresser une image avec Aspose OCR

La première chose à traiter est l’inclinaison de l’image. Si les lignes de texte ne sont pas horizontales, le moteur OCR lira mal les caractères. Le `DeskewFilter` fait le gros du travail.

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.Image;
import com.aspose.ocr.preprocess.DeskewFilter;
import com.aspose.ocr.preprocess.DenoiseFilter;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the raw scanned image
        Image scannedImage = Image.load("YOUR_DIRECTORY/noisy-rotated.png");

        // Step 3: Correct the image orientation (deskew)
        DeskewFilter deskewFilter = new DeskewFilter();
        scannedImage = deskewFilter.apply(scannedImage);

        // Step 4: Reduce visual noise (denoise)
        DenoiseFilter denoiseFilter = new DenoiseFilter();
        scannedImage = denoiseFilter.apply(scannedImage);

        // Step 5: Perform OCR on the cleaned image
        String recognizedText = ocrEngine.recognize(scannedImage);

        // Step 6: Output the extracted text
        System.out.println(recognizedText);
    }
}
```

> **Pourquoi c’est important :** Le `DeskewFilter` analyse la géométrie de l’image, estime l’angle de rotation et pivote le bitmap pour le remettre à l’horizontale. Sans cette étape, la plupart des moteurs OCR considèrent les lettres inclinées comme des glyphes totalement différents, ce qui fait chuter vos efforts pour **améliorer la précision de l’OCR**.

> **Astuce :** Si vous traitez des documents qui peuvent être à l’envers, activez le drapeau `setAutoRotate` sur le `DeskewFilter` (disponible dans les versions récentes d’Aspose). Il retourne automatiquement de 180° quand c’est nécessaire.

![Diagram showing before and after rotation – how to deskew image](https://example.com/deskew-diagram.png "how to deskew image example")

*Image alt text: how to deskew image example*

---

## Prétraiter l’image pour l’OCR – Dénoyautage et nettoyage

Une fois l’image redressée, le prochain obstacle est le bruit visuel — ces taches, artefacts de compression ou motifs de fond qui perturbent le moteur OCR. Le `DenoiseFilter` applique un algorithme de lissage subtil qui préserve les contours (les lettres) tout en éliminant le grain.

```java
// Step 4 (continued): Reduce visual noise (denoise)
DenoiseFilter denoiseFilter = new DenoiseFilter();
scannedImage = denoiseFilter.apply(scannedImage);
```

### Quand ajuster les paramètres de débruitage

- **Scans très sombres :** augmentez la puissance du filtre (`denoiseFilter.setStrength(2)`) pour éliminer les ombres de fond.  
- **Polices à petite taille :** réduisez la puissance afin d’éviter le flou des minuscules sérifs.  
- **Documents couleur :** convertissez d’abord en niveaux de gris (`scannedImage = scannedImage.toGrayscale();`) — le moteur OCR fonctionne mieux sur des images à canal unique.

Ces ajustements font partie des meilleures pratiques pour **nettoyer les images scannées** ; un bitmap plus propre se traduit directement par des scores de confiance plus élevés du moteur OCR.

---

## Extraire le texte de l’image – Exécuter le moteur OCR

Maintenant que l’image est droite et silencieuse, il est temps de **extraire le texte de l’image**. La classe `OcrEngine` gère tout en coulisses : segmentation, classification des caractères et modélisation linguistique.

```java
// Step 5: Perform OCR on the cleaned image
String recognizedText = ocrEngine.recognize(scannedImage);
System.out.println(recognizedText);
```

#### Résultat attendu

Si votre fichier source contient la ligne « **Invoice # 12345** », la console devrait afficher quelque chose comme :

```
Invoice # 12345
Date: 2026-03-18
Total: $1,250.00
```

Si la sortie apparaît brouillonnée, revérifiez les étapes précédentes—en particulier le redressement. Même une inclinaison d’un degré peut corrompre les chiffres et les symboles.

---

## Pièges courants & astuces pour **améliorer la précision de l’OCR**

| Problème | Pourquoi cela nuit à la précision | Solution rapide |
|----------|-----------------------------------|-----------------|
| **Rotation résiduelle** | L’OCR attend des lignes de base horizontales. | Vérifiez avec `deskewFilter.getAngle()` et consignez la valeur. |
| **Sur‑débruitage** | Floute les traits fins, transformant « i » en « l ». | Utilisez `setStrength(0.5)` pour les polices délicates. |
| **Mauvais format d’image** | La compression JPEG ajoute des artefacts. | Privilégiez PNG ou TIFF pour un stockage sans perte. |
| **Langue incorrecte** | Le moteur utilise l’anglais par défaut ; d’autres alphabets nécessitent une configuration explicite. | `ocrEngine.setLanguage(OcrEngine.Language.Spanish);` |
| **DPI faible (≤150)** | Pas assez de données pixels pour une segmentation fiable. | Rééchantillonnez à 300 DPI avant le traitement (`scannedImage = scannedImage.resample(300);`). |

### Bonus : Traitement par lots

Si vous avez un dossier de scans, encapsulez la démonstration dans une boucle :

```java
File folder = new File("YOUR_DIRECTORY");
for (File file : folder.listFiles((dir, name) -> name.endsWith(".png"))) {
    Image img = Image.load(file.getAbsolutePath());
    img = new DeskewFilter().apply(img);
    img = new DenoiseFilter().apply(img);
    String text = ocrEngine.recognize(img);
    System.out.println("=== " + file.getName() + " ===");
    System.out.println(text);
}
```

Ce modèle vous permet de **prétraiter une image pour l’OCR** à grande échelle, tout en gardant le code propre et les performances prévisibles.

---

## Récapitulatif & étapes suivantes

Nous avons couvert **comment redresser une image**, **prétraiter une image pour l’OCR**, puis **extraire le texte de l’image** avec Aspose OCR Java. En redressant le scan, en éliminant le bruit et en fournissant un bitmap impeccable au moteur, vous constaterez une **amélioration notable de la précision de l’OCR**.

Et après ? Envisagez ces extensions :

- **Détection de langue** – changez `ocrEngine.setLanguage` en fonction du script détecté.  
- **Export PDF** – injectez le texte reconnu dans un générateur PDF pour des documents consultables.  
- **Post‑traitement machine‑learning** – appliquez une correction orthographique ou des dictionnaires personnalisés sur le résultat OCR.

Testez ces idées, expérimentez avec différentes forces de filtre, et vous disposerez rapidement d’un pipeline robuste pour tout projet de numérisation de documents.

---

*Bon codage ! Si vous rencontrez un problème, laissez un commentaire ci‑dessous—je vous aiderai à affiner les paramètres de redressement et de débruitage.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}