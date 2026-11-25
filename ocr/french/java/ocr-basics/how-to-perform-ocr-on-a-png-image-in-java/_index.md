---
category: general
date: 2026-10-11
description: Apprenez à effectuer de l’OCR sur une image PNG en Java, à extraire le
  texte de l’image et à convertir l’image en texte avec un exemple simple d’OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: fr
lastmod: 2026-10-11
og_description: Comment effectuer une OCR sur une image PNG en Java, extraire le texte
  de l'image et convertir l'image en texte à l'aide d'un exemple concis, prêt à l'emploi.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Comment effectuer une OCR sur une image PNG en Java – guide complet
schemas:
- author: Aspose
  dateModified: '2026-10-11'
  description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  headline: How to perform OCR on a PNG image in Java
  type: TechArticle
- description: Learn how to perform OCR on a PNG image in Java, extract text from
    image and convert image to text with a simple OcrEngine example.
  name: How to perform OCR on a PNG image in Java
  steps:
  - name: 4.1 Handling low‑resolution PNGs
    text: 'Tesseract performs best on images with at least 300 DPI. If your source
      PNG is smaller, upscale it before OCR:'
  - name: 4.2 Extracting non‑English text
    text: 'To **extract text from image** that contains other languages, download
      the appropriate `.traineddata` files and set the language code:'
  - name: 4.3 Batch processing multiple PNGs
    text: 'If you need to **recognize text from PNG** files in a folder, iterate over
      the directory:'
  - name: 4.4 Dealing with OCR errors
    text: 'Typical OCR mistakes include misreading `0` (zero) as `O` or `1` as `l`.
      Post‑processing with regular expressions can clean the result:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
- Text Extraction
title: Comment effectuer la reconnaissance optique de caractères (OCR) sur une image
  PNG en Java
url: /fr/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment réaliser l'OCR sur une image PNG en Java

Si vous devez **effectuer une OCR** sur un fichier image, apprendre **comment effectuer une OCR** en Java est essentiel pour de nombreuses tâches d'automatisation. Que vous numérisiez des reçus, indexiez des documents scannés ou construisiez une archive photo consultable, la capacité à **extraire du texte d'une image** vous fait économiser d'innombrables heures manuelles.

Ce tutoriel vous montre une solution complète et exécutable qui charge un PNG, exécute un moteur OCR, et **reconnaît le texte des fichiers PNG**. Vous verrez également comment **convertir une image en texte** et gérer les pièges courants tels que les entrées basse résolution ou les caractères non ASCII.

## Ce que vous allez accomplir

* **load image java** code qui lit un PNG depuis le disque,
* initialiser un moteur OCR léger,
* **extract text from image** et afficher le résultat dans la console,
* adapter la solution à d'autres formats d'image ou au traitement par lots.

Aucun service externe n'est requis — seulement une bibliothèque OCR open‑source (Tess4J) et le runtime Java SE.

---

## Prérequis

* Java 17 ou plus récent (le code compile avec JDK 17).
* Maven ou Gradle pour la gestion des dépendances.
* Familiarité de base avec la ligne de commande et l'IDE de votre choix.
* La bibliothèque `tess4j` (un wrapper Java pour Tesseract). Ajoutez la dépendance Maven suivante :

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Si vous utilisez Gradle, l'équivalent est :

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Vous avez également besoin des fichiers de données Tesseract (`.traineddata`). Téléchargez le pack de données anglais depuis le dépôt officiel et placez-le dans un dossier nommé `tessdata` à la racine du projet.

---

## Étape 1 : Charger l'image en Java

Charger un PNG est simple avec la classe standard `ImageIO`. Le code ci‑dessous montre **load image java** de manière sûre et consciente des exceptions :

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Reads a PNG file from the given path and returns a BufferedImage.
 *
 * @param path absolute or relative path to the PNG file
 * @return BufferedImage representation of the file
 * @throws Exception if the file cannot be read or is not a PNG
 */
private static BufferedImage loadPng(String path) throws Exception {
    File imgFile = new File(path);
    if (!imgFile.exists()) {
        throw new IllegalArgumentException("File not found: " + path);
    }
    BufferedImage img = ImageIO.read(imgFile);
    if (img == null) {
        throw new IllegalArgumentException("Unsupported image format or corrupt file: " + path);
    }
    return img;
}
```

**Pourquoi c'est important :** `ImageIO.read` détecte automatiquement le format de l'image, mais nous vérifions explicitement la valeur `null` pour éviter les échecs silencieux lorsque le PNG est corrompu. Ce schéma est une bonne pratique lorsque vous **load image java** pour l'OCR.

---

## Étape 2 : Initialiser le moteur OCR

Tess4J encapsule le binaire natif Tesseract, exposant une API Java simple. La méthode suivante crée une instance `Tesseract`, la pointe vers le dossier `tessdata` et configure la langue en anglais :

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;

/**
 * Configures and returns a ready‑to‑use Tesseract instance.
 *
 * @return configured ITesseract object
 */
private static ITesseract createOcrEngine() {
    ITesseract tesseract = new Tesseract();
    // Path to the folder that contains .traineddata files
    tesseract.setDatapath("tessdata");
    // Language code – "eng" for English; you can add more languages later
    tesseract.setLanguage("eng");
    // Optional: increase OCR accuracy for PNGs with low DPI
    tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
    return tesseract;
}
```

**Pourquoi nous faisons cela :** Initialiser le moteur une fois et le réutiliser pour plusieurs images réduit le temps de démarrage. L'appel `setOcrEngineMode` sélectionne le mode par défaut, qui fonctionne bien pour la plupart des PNG. Si vous rencontrez des scans bruyants, vous pouvez expérimenter d'autres modes (par ex., `OEM_LSTM_ONLY`).

---

## Étape 3 : Effectuer l'OCR et **reconnaître le texte des PNG**

Nous combinons maintenant le chargeur d'image et le moteur OCR. La méthode ci‑dessous exécute l'OCR sur un `BufferedImage` et renvoie la chaîne extraite :

```java
/**
 * Runs OCR on the supplied image and returns the recognized text.
 *
 * @param image BufferedImage containing the PNG to process
 * @param tesseract configured OCR engine
 * @return plain‑text result of OCR
 * @throws Exception if OCR fails
 */
private static String extractText(BufferedImage image, ITesseract tesseract) throws Exception {
    // Tess4J can directly accept a BufferedImage
    return tesseract.doOCR(image);
}
```

**Exemple complet exécutable**

```java
import java.awt.image.BufferedImage;
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.TesseractException;

public class OcrDemo {

    public static void main(String[] args) {
        try {
            // 1️⃣ Load the PNG file
            BufferedImage image = loadPng("sample.png");

            // 2️⃣ Create and configure the OCR engine
            ITesseract ocrEngine = createOcrEngine();

            // 3️⃣ Recognize text from PNG
            String recognizedText = extractText(image, ocrEngine);

            // 4️⃣ Display the result – this is the **convert image to text** step
            System.out.println("=== OCR RESULT ===");
            System.out.println(recognizedText);
        } catch (Exception e) {
            System.err.println("Error during OCR processing:");
            e.printStackTrace();
        }
    }

    // ----- Helper methods from previous steps -----
    // loadPng, createOcrEngine, extractText (copy-pasted here for completeness)
    // ... (methods omitted for brevity; see the sections above) ...
}
```

**Sortie attendue**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

La console affichera les caractères exacts que le moteur a extraits de `sample.png`. Si le PNG ne contient qu'un seul mot, la sortie sera ce mot suivi d'un saut de ligne.

---

## Étape 4 : Variations courantes et cas limites

### 4.1 Gestion des PNG basse résolution

Tesseract fonctionne au mieux sur des images d'au moins 300 DPI. Si votre PNG source est plus petit, augmentez sa résolution avant l'OCR :

```java
import java.awt.Graphics2D;
import java.awt.Image;
import java.awt.RenderingHints;

private static BufferedImage upscale(BufferedImage src, int scaleFactor) {
    int width = src.getWidth() * scaleFactor;
    int height = src.getHeight() * scaleFactor;
    Image tmp = src.getScaledInstance(width, height, Image.SCALE_SMOOTH);
    BufferedImage resized = new BufferedImage(width, height, BufferedImage.TYPE_INT_ARGB);
    Graphics2D g2d = resized.createGraphics();
    g2d.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                         RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g2d.drawImage(tmp, 0, 0, null);
    g2d.dispose();
    return resized;
}
```

Appliquez `upscale(image, 2)` avant d'appeler `extractText` pour améliorer la précision.

### 4.2 Extraction de texte non anglais

Pour **extract text from image** contenant d'autres langues, téléchargez les fichiers `.traineddata` appropriés et définissez le code de langue :

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Traitement par lots de plusieurs PNG

Si vous devez **recognize text from PNG** dans un dossier, parcourez le répertoire :

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Gestion des erreurs d'OCR

Les erreurs OCR typiques incluent la confusion entre `0` (zéro) et `O` ou entre `1` et `l`. Un post‑traitement avec des expressions régulières peut nettoyer le résultat :

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Astuces pro pour un OCR fiable en Java

| Astuce | Raison |
|-----|--------|
| **Utiliser un PNG sans perte** | Les artefacts de compression du JPEG peuvent perturber le moteur. |
| **Supprimer les bordures blanches** | Les espaces blancs superflus augmentent le temps de traitement et peuvent provoquer des faux positifs. |
| **Définir `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** uniquement lorsque la mise en page est inconnue ; sinon choisissez un mode spécifique (par ex., `PSM_SINGLE_BLOCK`). |
| **Mettre en cache l'instance `ITesseract`** |  |

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment lire du texte à partir d'une image en Java avec Aspose OCR – Guide complet](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Comment utiliser l'OCR en Java – Reconnaître rapidement le texte d'une image](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [OCR d'images par lots en Java – Extraire rapidement le texte des fichiers PNG](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}