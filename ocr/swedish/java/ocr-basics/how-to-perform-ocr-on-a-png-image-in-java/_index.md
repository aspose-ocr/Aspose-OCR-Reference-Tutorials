---
category: general
date: 2026-10-11
description: Lär dig hur du utför OCR på en PNG‑bild i Java, extraherar text från
  bilden och konverterar bilden till text med ett enkelt OcrEngine‑exempel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: sv
lastmod: 2026-10-11
og_description: Hur man utför OCR på en PNG‑bild i Java, extraherar text från bilden
  och konverterar bilden till text med ett kortfattat, färdigt‑att‑köra exempel.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Hur man utför OCR på en PNG-bild i Java – komplett guide
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
title: Hur man utför OCR på en PNG-bild i Java
url: /sv/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man utför OCR på en PNG-bild i Java

Om du behöver **perform OCR** på en bildfil, är det viktigt att lära sig **how to perform OCR** i Java för många automatiseringsuppgifter. Oavsett om du digitaliserar kvitton, indexerar skannade dokument eller bygger ett sökbart fotoarkiv, sparar förmågan att **extract text from image** filer otaliga manuella timmar.

Denna handledning visar en komplett, körbar lösning som laddar en PNG, kör en OCR-motor och **recognize text from PNG** filer. Du kommer också att se hur man **convert image to text** och hanterar vanliga fallgropar såsom lågupplöst indata eller icke‑ASCII‑tecken.

## Vad du kommer att uppnå

* **load image java** kod som läser en PNG från disk,
* initiera en lättviktig OCR-motor,
* **extract text from image** och skriv ut resultatet till konsolen,
* anpassa lösningen för andra bildformat eller batch‑bearbetning.

Inga externa tjänster krävs—endast ett enda open‑source OCR‑bibliotek (Tess4J) och Java SE‑runtime.

---

## Förutsättningar

* Java 17 eller nyare (koden kompileras med JDK 17).
* Maven eller Gradle för beroendehantering.
* Grundläggande kunskap om kommandoraden och den IDE du föredrar.
* Biblioteket `tess4j` (en Java‑wrapper för Tesseract). Lägg till följande Maven‑beroende:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Om du använder Gradle, är motsvarande:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Du behöver också Tesseract‑datafilerna (`.traineddata`). Ladda ner det engelska datapaketet från det officiella repot och placera det i en mapp som heter `tessdata` i projektets rot.

---

## Steg 1: Ladda bilden i Java

Att ladda en PNG är enkelt med standardklassen `ImageIO`. Koden nedan demonstrerar **load image java** på ett säkert, undantags‑medvetet sätt:

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

**Varför detta är viktigt:** `ImageIO.read` upptäcker automatiskt bildformatet, men vi kontrollerar explicit om resultatet är `null` för att undvika tysta fel när PNG‑filen är korrupt. Detta mönster är en bästa praxis när du **load image java** för OCR.

---

## Steg 2: Initiera OCR‑motorn

Tess4J omsluter den inhemska Tesseract‑binären och exponerar ett enkelt Java‑API. Följande metod skapar en `Tesseract`‑instans, pekar den mot `tessdata`‑mappen och konfigurerar språket till engelska:

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

**Varför vi gör detta:** Att initiera motorn en gång och återanvända den för flera bilder minskar startkostnaden. Anropet `setOcrEngineMode` väljer standardläget, vilket fungerar bra för de flesta PNG‑filer. Om du stöter på brusiga skanningar kan du experimentera med andra lägen (t.ex. `OEM_LSTM_ONLY`).

---

## Steg 3: Utför OCR och **recognize text from PNG**

Nu kombinerar vi bildladdaren och OCR‑motorn. Metoden nedan kör OCR på en `BufferedImage` och returnerar den extraherade strängen:

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

**Fullt körbart exempel**

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

**Förväntad utskrift**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Konsolen kommer att visa exakt de tecken som motorn extraherade från `sample.png`. Om PNG‑filen bara innehåller ett enda ord, blir utskriften det ordet följt av en radbrytning.

---

## Steg 4: Vanliga variationer och kantfall

### 4.1 Hantera lågupplösta PNG‑filer

Tesseract fungerar bäst på bilder med minst 300 DPI. Om din käll‑PNG är mindre, skala upp den innan OCR:

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

Använd `upscale(image, 2)` innan du anropar `extractText` för att förbättra noggrannheten.

### 4.2 Extrahera icke‑engelsk text

För att **extract text from image** som innehåller andra språk, ladda ner lämpliga `.traineddata`‑filer och ange språk‑koden:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Batch‑bearbeta flera PNG‑filer

Om du behöver **recognize text from PNG** filer i en mapp, iterera över katalogen:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Hantera OCR‑fel

Typiska OCR‑misstag inkluderar att läsa `0` (noll) som `O` eller `1` som `l`. Efterbehandling med reguljära uttryck kan rensa resultatet:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Pro‑tips för pålitlig OCR i Java

| Tip | Reason |
|-----|--------|
| **Använd en förlustfri PNG** | Komprimeringsartefakter i JPEG kan förvirra motorn. |
| **Trimma vita kanter** | Överflödig vit yta ökar bearbetningstiden och kan orsaka falska positiva. |
| **Ställ in `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** endast när layouten är okänd; annars välj ett specifikt läge (t.ex. `PSM_SINGLE_BLOCK`). | |
| **Cacha `ITesseract`‑instansen** | |

## Vad bör du lära dig härnäst?

Följande handledningar täcker närliggande ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}