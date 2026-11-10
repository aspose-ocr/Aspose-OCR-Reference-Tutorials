---
category: general
date: 2026-07-21
description: Extrahujte text z obrázku pomocí Java OCR. Naučte se, jak převést PNG
  na text, číst text z PNG, načíst obrázek pro OCR a provést OCR na obrázku během
  několika kroků.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- extract text from image
- convert png to text
- read text from png
- load image for ocr
- perform ocr on image
language: cs
lastmod: 2026-07-21
og_description: Extrahujte text z obrázku pomocí Javy. Tento průvodce vám ukáže, jak
  převést PNG na text, číst text z PNG, načíst obrázek pro OCR a efektivně provádět
  OCR na obrázku.
og_image_alt: Screenshot of Java code extracting text from an image using OCR
og_title: Extrahování textu z obrázku v Javě – krok za krokem OCR tutoriál
schemas:
- author: Aspose
  dateModified: '2026-07-21'
  description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  headline: Extract Text from Image in Java – Complete OCR Guide
  type: TechArticle
- description: Extract text from image using Java OCR. Learn how to convert PNG to
    text, read text from PNG, load image for OCR, and perform OCR on image in just
    a few steps.
  name: Extract Text from Image in Java – Complete OCR Guide
  steps:
  - name: Low‑Quality Images
    text: 'If the PNG is blurry or has low contrast, OCR accuracy drops. A quick fix
      is to pre‑process the image:'
  - name: Multi‑Language Support
    text: Tess4J can handle many languages. Just download the appropriate `.traineddata`
      file and point `tesseract.setLanguage("spa")` for Spanish, for example.
  - name: Large PDFs or Multi‑Page Images
    text: If you need to **extract text from image** files inside a PDF, split each
      page into PNGs first (using PDFBox) and then feed each PNG to the same OCR routine.
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Extrahovat text z obrázku v Javě – Kompletní průvodce OCR
url: /cs/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku v Javě – Kompletní průvodce OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nebyli jste si jisti, kterou Java knihovnu zvolit? Nejste v tom sami. Ať už digitalizujete účtenky, skenujete PDF nebo budujete prohledávatelný archiv, získávání textu z PNG je každodenní problém mnoha vývojářů.

V tomto tutoriálu vás provedeme praktickým řešením, které vám umožní **převést PNG na text**, **číst text z PNG**, **načíst obrázek pro OCR** a **provést OCR na obrázku**—vše pomocí několika řádků čistého Java kódu. Na konci budete mít spustitelný program, který můžete vložit do libovolného projektu.

## Co vytvoříte

Vytvoříme malou Java konzolovou aplikaci, která:

1. Načte soubor PNG z disku.  
2. Pošle obrázek do OCR motoru (Tess4J, Java wrapper pro Tesseract).  
3. Vytiskne rozpoznaný text do konzole.

Žádné externí služby, žádná magie—pouze čistá Java a open‑source OCR engine.

## Požadavky

- **Java 17** nebo novější (kód se kompiluje i se staršími verzemi, ale Java 17 poskytuje nejnovější jazykové vymoženosti).  
- **Maven** nebo **Gradle** pro správu závislostí.  
- Ukázkový PNG pojmenovaný `sample.png` umístěný ve složce, na kterou můžete odkazovat (např. `src/main/resources`).  
- Základní znalost Java metody `main` a zpracování výjimek.

Pokud některý z těchto pojmů není vám znám, nebojte se—každý krok obsahuje rychlý přehled.

## Krok 1: Nastavení projektu a přidání OCR knihovny

Nejprve vytvořte nový Maven projekt (nebo Gradle, pokud dáváte přednost). Přidejte závislost Tess4J, která vám přinese binární soubory Tesseract.

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
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

> **Tip:** Pokud používáte Gradle, ekvivalentní řádek je `implementation 'net.sourceforge.tess4j:tess4j:5.5.1'`.

Přidání této knihovny vám poskytne třídu `Tesseract`, která zajišťuje těžkou práci s **prováděním OCR na obrázku**.

## Krok 2: Načtení obrázku pro OCR

Nyní potřebujeme **načíst obrázek pro OCR**. Tess4J pracuje s `java.awt.image.BufferedImage`, takže PNG načteme pomocí `ImageIO`.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

public class OcrDemo {

    /**
     * Loads a PNG file from the given path and returns a BufferedImage.
     *
     * @param path absolute or relative path to the PNG file
     * @return BufferedImage containing the image data
     * @throws IOException if the file cannot be read
     */
    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image to be recognized
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }
```

Výše uvedená metoda čistě odděluje logiku **načtení obrázku pro OCR**, což usnadňuje testování zbytku kódu. Všimněte si komentáře – odráží původní úryvek a rozšiřuje jej pro větší srozumitelnost.

## Krok 3: Provést OCR na obrázku

S obrázkem v paměti můžeme nyní **provést OCR na obrázku**. Instance `Tesseract` je náš engine; nakonfigurujeme ji tak, aby používala výchozí anglická jazyková data, která jsou součástí Tess4J.

```java
    /**
     * Runs OCR on the supplied BufferedImage and returns the extracted text.
     *
     * @param image the image to analyze
     * @return plain text recognized from the image
     * @throws TesseractException if the OCR process fails
     */
    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();

        // Optional: set the datapath if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");

        // Step 4: Run OCR and capture the recognized text
        return tesseract.doOCR(image);
    }
```

Zde jsme sloučili původní „Krok 1“ a „Krok 4“ do jedné metody, protože objekt `Tesseract` je levný na vytvoření a chceme, aby kód zůstal kompaktní. Komentář stále odkazuje na původní kroky pro sledovatelnost.

## Krok 4: Sestavení všeho dohromady – Metoda main

Nakonec vše spojíme v metodě `main`. Zde **čtete text z PNG** a uvidíte výsledek vytištěný do konzole.

```java
    public static void main(String[] args) {
        // Adjust the path to point at your PNG file
        String imagePath = "src/main/resources/sample.png";

        try {
            // Load the PNG image
            BufferedImage image = loadImage(imagePath);

            // Extract text from the image
            String recognizedText = extractText(image);

            // Step 5: Display the extracted text
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("OCR error: " + e.getMessage());
        }
    }
}
```

Když spustíte `mvn compile exec:java -Dexec.mainClass="com.example.ocrdemo.OcrDemo"` (nebo ekvivalent v Gradle), měli byste vidět něco jako:

```
=== OCR Result ===
Hello, world!
This is a sample PNG file.
```

Tento výstup dokazuje, že jste úspěšně **extrahovali text z obrázku**, **převáděli PNG na text** a **četli text z PNG** v jednom přehledném programu.

## Řešení běžných okrajových případů

### Nízkokvalitní obrázky

Pokud je PNG rozmazaný nebo má nízký kontrast, přesnost OCR klesá. Rychlé řešení je předzpracovat obrázek:

```java
// Example: Convert to grayscale and apply a binary threshold
BufferedImage gray = new BufferedImage(
        image.getWidth(), image.getHeight(),
        BufferedImage.TYPE_BYTE_GRAY);
Graphics2D g = gray.createGraphics();
g.drawImage(image, 0, 0, null);
g.dispose();

// Simple binary threshold
for (int y = 0; y < gray.getHeight(); y++) {
    for (int x = 0; x < gray.getWidth(); x++) {
        int rgb = gray.getRGB(x, y) & 0xFF;
        int binary = rgb < 128 ? 0x000000 : 0xFFFFFF;
        gray.setRGB(x, y, binary);
    }
}
String text = extractText(gray);
```

### Podpora více jazyků

Tess4J dokáže zpracovat mnoho jazyků. Stačí stáhnout odpovídající soubor `.traineddata` a nastavit `tesseract.setLanguage("spa")` pro španělštinu, například.

### Velké PDF nebo vícestránkové obrázky

Pokud potřebujete **extrahovat text z obrázku** souborů uvnitř PDF, nejprve rozdělte každou stránku na PNG (pomocí PDFBox) a poté pošlete každý PNG do stejné OCR rutiny.

## Kompletní funkční příklad (Všechen kód na jednom místě)

Níže je kompletní, připravená ke spuštění Java třída. Zkopírujte a vložte ji do `src/main/java/com/example/ocrdemo/OcrDemo.java` a můžete začít.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

import javax.imageio.ImageIO;
import java.awt.image.BufferedImage;
import java.io.File;
import java.io.IOException;

/**
 * Demonstrates how to extract text from image (PNG) using Java and Tess4J.
 */
public class OcrDemo {

    private static BufferedImage loadImage(String path) throws IOException {
        // Step 2: Load the image for OCR
        File imgFile = new File(path);
        return ImageIO.read(imgFile);
    }

    private static String extractText(BufferedImage image) throws TesseractException {
        // Step 1: Initialize the OCR engine
        Tesseract tesseract = new Tesseract();
        // Uncomment and set if you have a custom tessdata folder
        // tesseract.setDatapath("tessdata");
        // Step 4: Perform OCR on image
        return tesseract.doOCR(image);
    }

    public static void main(String[] args) {
        // Path to the PNG you want to convert to text
        String imagePath = "src/main/resources/sample.png";

        try {
            BufferedImage image = loadImage(imagePath);
            String recognizedText = extractText(image);
            System.out.println("=== OCR Result ===");
            System.out.println(recognizedText);
        } catch (IOException e) {
            System.err.println("Failed to load image: " + e.getMessage());
        } catch (TesseractException e) {
            System.err.println("Error during OCR: " + e.getMessage());
        }
    }
}
```

Spuštěním třídy se vytiskne výsledek OCR, což potvrzuje, že jste úspěšně **provedli OCR na obrázku** a převedli svůj PNG na editovatelný text.

## Shrnutí a další kroky

Začali jsme **extrahováním textu z obrázku** pomocí lehkého Java nastavení. Nyní víte, jak **načíst obrázek pro OCR**, **provést OCR na obrázku** a **číst text z PNG**—základní stavební kameny pro jakýkoli pipeline digitalizace dokumentů.

Chcete jít dál? Vyzkoušejte tyto nápady:

- **Dávkové zpracování:** Procházet adresář PNG souborů a zapisovat každý výsledek do souboru `.txt`.  
- **Integrace s databází:** Ukládat extrahované řetězce spolu s metadaty pro prohledávatelné archivy.  
- **Kombinace s NLP:** Poslat výstup OCR do modelu sentiment‑analýzy pro rychlé poznatky.  

Každé z těchto rozšíření staví na stejných základních konceptech, které jsme pokryli, takže jste připraveni experimentovat.

---

*Šťastné programování! Pokud narazíte na problémy

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahování textu z obrázku Java s Aspose.OCR Detekce oblastí](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [obrázek na text java: Převod obrázku na text s Aspose.OCR](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Jak OCR text z obrázku s jazykem pomocí Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}