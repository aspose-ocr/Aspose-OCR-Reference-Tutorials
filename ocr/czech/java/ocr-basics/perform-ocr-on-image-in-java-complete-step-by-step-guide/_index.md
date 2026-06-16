---
category: general
date: 2026-06-16
description: Naučte se, jak provádět OCR na souborech obrázků v Javě. Tento tutoriál
  pokrývá rozpoznávání textu z PNG, extrahování textu z obrázku, převod obrázku na
  text a načítání obrázku pro OCR.
draft: false
keywords:
- perform OCR on image
- recognize text from PNG
- extract text from image
- convert image to text
- load image for OCR
language: cs
og_description: Proveďte OCR na obrázku pomocí Javy. Tento průvodce ukazuje, jak rozpoznat
  text z PNG, extrahovat text z obrázku a převést obrázek na text s připraveným příkladem
  k okamžitému spuštění.
og_title: Proveďte OCR na obrázku v Javě – Kompletní programovací tutoriál
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  headline: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Learn how to perform OCR on image files in Java. This tutorial covers
    recognizing text from PNG, extracting text from image, converting image to text,
    and loading image for OCR.
  name: Perform OCR on Image in Java – Complete Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'If `hello.png` contains the phrase “Hello, OCR world!”, the console will
      display something like:'
  - name: 5.1 Dealing with Low‑Resolution Images
    text: 'If the source PNG is blurry, OCR accuracy drops. A quick fix is to upscale
      the image before feeding it to the engine:'
  - name: 5.2 Multi‑Language Documents
    text: 'If you anticipate French or German text, simply add the language codes
      to `setLanguage`:'
  - name: 5.3 Skipping Empty Pages
    text: 'Sometimes a scanned PDF page renders as a blank PNG. Detecting an empty
      image saves processing time:'
  type: HowTo
tags:
- Java
- OCR
- Image Processing
title: Provádějte OCR na obrázku v Javě – Kompletní krok‑za‑krokem průvodce
url: /cs/java/ocr-basics/perform-ocr-on-image-in-java-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Provádění OCR na obrázku v Javě – Kompletní průvodce krok za krokem

Už jste někdy potřebovali **perform OCR on image** soubory, ale nebyli jste si jisti, kterou knihovnu pro Javu zvolit? Nejste v tom sami. Ať už vytváříte skener účtenek, archiv dokumentů, nebo jste jen zvědaví, jak převést obrázky na prohledávatelný text, naučit se **perform OCR on image** s Javou je užitečná dovednost.

V tomto tutoriálu projdeme vše, co potřebujete k **perform OCR on image** souborům: načtení obrázku, konfiguraci engine, rozpoznání textu a nakonec vytištění výsledku. Na konci budete schopni **recognize text from PNG** soubory, **extract text from image** zdroje a **convert image to text** pomocí několika řádků kódu.

## Prerequisites

- Java 17 nebo novější (kód se kompiluje s jakýmkoli recentním JDK)
- Maven nainstalován (nebo váš oblíbený build nástroj)
- Základní znalost syntaxe Javy
- PNG soubor, který chcete otestovat (budeme ho nazývat `hello.png`)

> **Pro tip:** Pokud nemáte po ruce PNG, vytvořte jej pořízením snímku obrazovky libovolného textu a uložte jej jako `hello.png` do složky nazvané `resources`.

## Co budeme stavět

Malá konzolová aplikace pojmenovaná `OcrDemo`, která:

1. **Loads image for OCR** – načte PNG z disku.
2. **Performs OCR on image** – používá engine Tesseract přes Tess4J.
3. **Extracts text from image** – vrací `String` s rozpoznaným obsahem.
4. Vytiskne výsledek do konzole.

Pojďme na to.

## Krok 1: Nastavte projekt a přidejte Tess4J

Nejprve vytvořte nový Maven projekt (nebo Gradle, pokud dáváte přednost). Přidejte závislost Tess4J, která obaluje populární OCR engine Tesseract.

```xml
<!-- pom.xml -->
<project>
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.example</groupId>
  <artifactId>ocr-demo</artifactId>
  <version>1.0.0</version>
  <properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
  </properties>

  <dependencies>
    <!-- Tess4J – Java wrapper for Tesseract OCR -->
    <dependency>
      <groupId>net.sourceforge.tess4j</groupId>
      <artifactId>tess4j</artifactId>
      <version>5.5.1</version>
    </dependency>
  </dependencies>
</project>
```

> **Why Tess4J?** Je aktivně udržována, funguje napříč platformami a poskytuje čisté Java API pro úkoly **perform OCR on image**.

## Krok 2: Připravte logiku načítání obrázku

Nyní napíšeme pomocnou metodu, která **load image for OCR**. Metoda používá `ImageIO` z Javy k načtení PNG do `BufferedImage`.

```java
package com.example.ocr;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Utility class responsible for loading images from the file system.
 */
public final class ImageLoader {

    private ImageLoader() { /* utility class */ }

    /**
     * Loads a PNG (or any supported format) from the given path.
     *
     * @param path absolute or relative path to the image file
     * @return BufferedImage instance ready for OCR processing
     * @throws IOException if the file cannot be read
     */
    public static BufferedImage load(String path) throws IOException {
        File imgFile = new File(path);
        if (!imgFile.exists()) {
            throw new IOException("Image file not found: " + path);
        }
        return ImageIO.read(imgFile);
    }
}
```

Všimněte si, že název metody jasně odráží záměr **load image for OCR**, což činí kód samodokumentujícím.

## Krok 3: Nakonfigurujte OCR engine pro **Perform OCR on Image**

S obrázkem v ruce vytvoříme instanci `Tesseract`, povolíme automatické rozpoznání jazyka a zavoláme `doOCR`. To je jádro toho, jak **perform OCR on image** data.

```java
package com.example.ocr;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

/**
 * Wrapper around Tess4J that abstracts the OCR workflow.
 */
public final class OcrEngine {

    private final ITesseract tesseract;

    public OcrEngine() {
        tesseract = new Tesseract();

        // Use the bundled tessdata folder (you can also point to a custom one)
        tesseract.setDatapath("tessdata");

        // Enable automatic language detection – improves accuracy across multilingual images
        tesseract.setLanguage("eng"); // fallback language
        tesseract.setOcrEngineMode(ITesseract.OEM_DEFAULT);
        tesseract.setPageSegMode(ITesseract.PSM_AUTO);
    }

    /**
     * Performs OCR on the supplied BufferedImage and returns the recognized text.
     *
     * @param image image to be processed
     * @return the text extracted from the image
     * @throws TesseractException if OCR fails
     */
    public String recognize(BufferedImage image) throws TesseractException {
        return tesseract.doOCR(image);
    }
}
```

> **Why enable auto‑detect?** Umožňuje engine vybrat nejlepší jazykový model pro obrázek, což je zvláště užitečné, když **convert image to text** ze zdrojů, které kombinují angličtinu a jiné skripty.

## Krok 4: Sestavte vše dohromady – Hlavní aplikace

Zde je vstupní bod, který **recognize text from PNG**, **extract text from image**, a nakonec vytiskne výsledek. Toto je kompletní, spustitelný příklad.

```java
package com.example.ocr;

import net.sourceforge.tess4j.TesseractException;
import java.awt.image.BufferedImage;
import java.io.IOException;

/**
 * Demo application that shows how to perform OCR on image files.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Path to the PNG you want to process
        String imagePath = "resources/hello.png";

        try {
            // Step 1: Load image for OCR
            BufferedImage image = ImageLoader.load(imagePath);

            // Step 2: Create OCR engine instance
            OcrEngine engine = new OcrEngine();

            // Step 3: Perform OCR on image and retrieve the text
            String recognizedText = engine.recognize(image);

            // Step 4: Output the recognized text to the console
            System.out.println("=== Recognized Text ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR processing error: " + e.getMessage());
        }
    }
}
```

### Očekávaný výstup

Pokud `hello.png` obsahuje frázi “Hello, OCR world!”, konzole zobrazí něco jako:

```
=== Recognized Text ===
Hello, OCR world!
```

Přesný výstup se může mírně lišit v závislosti na kvalitě obrázku, ale měli byste vidět text, který jste umístili do PNG.

## Krok 5: Řešení běžných okrajových případů

### 5.1 Práce s nízkým rozlišením obrázků

Pokud je zdrojové PNG rozmazané, přesnost OCR klesá. Rychlé řešení je zvětšit obrázek před předáním engine:

```java
import java.awt.Graphics2D;
import java.awt.RenderingHints;

public static BufferedImage upscale(BufferedImage original, int factor) {
    int width = original.getWidth() * factor;
    int height = original.getHeight() * factor;
    BufferedImage scaled = new BufferedImage(width, height, original.getType());
    Graphics2D g = scaled.createGraphics();
    g.setRenderingHint(RenderingHints.KEY_INTERPOLATION,
                       RenderingHints.VALUE_INTERPOLATION_BICUBIC);
    g.drawImage(original, 0, 0, width, height, null);
    g.dispose();
    return scaled;
}
```

Zavolejte `upscale(image, 2)` před `engine.recognize(image)`, aby se zlepšily výsledky.

### 5.2 Dokumenty s více jazyky

Pokud očekáváte francouzský nebo německý text, jednoduše přidejte jazykové kódy do `setLanguage`:

```java
tesseract.setLanguage("eng+fra+deu");
```

Engine se pak pokusí **extract text from image** pomocí kombinovaných jazykových modelů.

### 5.3 Přeskakování prázdných stránek

Někdy se naskenovaná stránka PDF zobrazí jako prázdné PNG. Detekce prázdného obrázku šetří čas zpracování:

```java
if (image.getWidth() == 0 || image.getHeight() == 0) {
    System.out.println("Empty image – skipping OCR.");
    return;
}
```

## Krok 6: Balíčkování a spuštění aplikace

- **Compile:** `mvn clean compile`
- **Run:** `mvn exec:java -Dexec.mainClass="com.example.ocr.OcrDemo"`

Ujistěte se, že složka `tessdata` (obsahující jazykové soubory) leží vedle zkompilovaného JAR souboru nebo specifikujte její absolutní cestu v `OcrEngine`.

## Závěr

Nyní máte solidní, připravený pro produkci vzor pro **perform OCR on image** soubory pomocí Javy. Od **loading image for OCR** po **recognize text from PNG**, pokryli jsme, jak **extract text from image**, **convert image to text**, a jak řešit složité scénáře jako skeny s nízkým rozlišením nebo obsah ve více jazycích.

Dále můžete zkoumat:

- **Batch processing** – projít adresář PNG souborů a zapsat každý výsledek do souboru `.txt`.
- **PDF generation** – vložit extrahovaný text zpět do prohledávatelných PDF.
- **Cloud OCR services** – porovnat výkon lokálního Tesseractu s API jako Google Vision nebo Azure Cognitive Services.

Neváhejte experimentovat, ladit parametry a sdílet své poznatky. Šťastné kódování a ať se vaše obrázky vždy převádějí na čistý, prohledávatelný text! 

![Diagram ukazující OCR workflow pro perform OCR on image](https://example.com/ocr-workflow.png "příklad perform OCR on image")

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [rozpoznat textový obrázek s Aspose OCR – Kompletní Java OCR tutoriál](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Převést obrázek na text v Javě pomocí Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Extrahovat text z obrázku v Javě s Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}