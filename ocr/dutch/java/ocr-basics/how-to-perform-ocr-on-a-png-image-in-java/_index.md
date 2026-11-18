---
category: general
date: 2026-10-11
description: Leer hoe je OCR op een PNG‑afbeelding in Java uitvoert, tekst uit de
  afbeelding extraheert en de afbeelding naar tekst converteert met een eenvoudig
  OcrEngine‑voorbeeld.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: nl
lastmod: 2026-10-11
og_description: Hoe OCR uit te voeren op een PNG‑afbeelding in Java, tekst uit de
  afbeelding te extraheren en de afbeelding naar tekst te converteren met een beknopt,
  kant‑klaar voorbeeld.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Hoe OCR op een PNG-afbeelding in Java uit te voeren – volledige gids
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
title: Hoe OCR op een PNG-afbeelding in Java uit te voeren
url: /nl/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR uit te voeren op een PNG‑afbeelding in Java

Als je **OCR moet uitvoeren** op een afbeeldingsbestand, is het leren **hoe OCR uit te voeren** in Java essentieel voor veel automatiseringstaken. Of je nu bonnen digitaliseert, gescande documenten indexeert, of een doorzoekbaar foto‑archief bouwt, de mogelijkheid om **tekst uit afbeelding te extraheren** bespaart talloze handmatige uren.

Deze tutorial laat je een volledige, uitvoerbare oplossing zien die een PNG laadt, een OCR‑engine uitvoert, en **tekst uit PNG**‑bestanden herkent. Je ziet ook hoe je **afbeelding naar tekst converteert** en veelvoorkomende valkuilen aanpakt, zoals invoer met lage resolutie of niet‑ASCII‑tekens.

## Wat je zult bereiken

Aan het einde van deze gids kun je:

* **load image java** code die een PNG van schijf leest,
* een lichtgewicht OCR‑engine initialiseren,
* **tekst uit afbeelding** extraheren en het resultaat naar de console printen,
* de oplossing aanpassen voor andere afbeeldingsformaten of batch‑verwerking.

Er zijn geen externe services vereist—alleen één open‑source OCR‑bibliotheek (Tess4J) en de Java SE‑runtime.

---

## Vereisten

* Java 17 of nieuwer (de code compileert met JDK 17).
* Maven of Gradle voor dependency‑beheer.
* Basiskennis van de commandoregel en de IDE van jouw keuze.
* De `tess4j`‑bibliotheek (een Java‑wrapper voor Tesseract). Voeg de volgende Maven‑dependency toe:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Als je Gradle gebruikt, is het equivalent:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Je hebt ook de Tesseract‑databestanden (`.traineddata`) nodig. Download het Engelse datapakket van de officiële repository en plaats het in een map genaamd `tessdata` in de project‑root.

---

## Stap 1: Laad de afbeelding in Java

Het laden van een PNG is eenvoudig met de standaard `ImageIO`‑klasse. De code hieronder demonstreert **load image java** op een veilige, exception‑bewuste manier:

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

**Waarom dit belangrijk is:** `ImageIO.read` detecteert automatisch het afbeeldingsformaat, maar we controleren expliciet op `null` om stille fouten te voorkomen wanneer de PNG beschadigd is. Dit patroon is een best practice wanneer je **load image java** voor OCR gebruikt.

---

## Stap 2: Initialiseert de OCR‑engine

Tess4J omsluit de native Tesseract‑binary en biedt een eenvoudige Java‑API. De volgende methode maakt een `Tesseract`‑instance, wijst deze naar de `tessdata`‑map en stelt de taal in op Engels:

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

**Waarom we dit doen:** De engine één keer initialiseren en hergebruiken voor meerdere afbeeldingen vermindert de opstart‑overhead. De `setOcrEngineMode`‑aanroep selecteert de standaardmodus, die goed werkt voor de meeste PNG‑bestanden. Als je last hebt van ruis in scans, kun je experimenteren met andere modi (bijv. `OEM_LSTM_ONLY`).

---

## Stap 3: Voer OCR uit en **herken tekst uit PNG**

Nu combineren we de afbeeldingslader en de OCR‑engine. De methode hieronder voert OCR uit op een `BufferedImage` en retourneert de geëxtraheerde string:

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

**Volledig uitvoerbaar voorbeeld**

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

**Verwachte output**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

De console toont de exacte tekens die de engine heeft geëxtraheerd uit `sample.png`. Als de PNG slechts één woord bevat, is de output dat woord gevolgd door een nieuwe regel.

---

## Stap 4: Veelvoorkomende variaties en randgevallen

### 4.1 Omgaan met PNG's met lage resolutie

Tesseract werkt het beste op afbeeldingen met minimaal 300 DPI. Als je bron‑PNG kleiner is, schaal deze dan op vóór OCR:

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

Pas `upscale(image, 2)` toe vóór het aanroepen van `extractText` om de nauwkeurigheid te verbeteren.

### 4.2 Tekst in andere talen extraheren

Om **tekst uit afbeelding** te extraheren die andere talen bevat, download je de juiste `.traineddata`‑bestanden en stel je de taalcode in:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Batch‑verwerking van meerdere PNG's

Als je **tekst uit PNG**‑bestanden in een map moet herkennen, doorloop je de directory:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Omgaan met OCR‑fouten

Typische OCR‑fouten omvatten het verwarren van `0` (nul) met `O` of `1` met `l`. Naverwerking met reguliere expressies kan het resultaat opschonen:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Pro‑tips voor betrouwbare OCR in Java

| Tip | Reden |
|-----|--------|
| **Use a lossless PNG** | Compressie‑artefacten in JPEG kunnen de engine verwarren. |
| **Trim white borders** | Overtollige witruimte verhoogt de verwerkingstijd en kan valse positieven veroorzaken. |
| **Set `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** only when layout is unknown; otherwise choose a specific mode (e.g., `PSM_SINGLE_BLOCK`). | **Stel `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** alleen in wanneer de lay‑out onbekend is; kies anders een specifieke modus (bijv. `PSM_SINGLE_BLOCK`). |
| **Cache the `ITesseract` instance** | |

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}