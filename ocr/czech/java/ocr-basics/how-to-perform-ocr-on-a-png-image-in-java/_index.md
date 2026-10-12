---
category: general
date: 2026-10-11
description: Naučte se, jak provádět OCR na PNG obrázku v Javě, extrahovat text z
  obrázku a převést obrázek na text pomocí jednoduchého příkladu OcrEngine.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text from image
- recognize text from PNG
- load image java
- convert image to text
language: cs
lastmod: 2026-10-11
og_description: Jak provést OCR na PNG obrázku v Javě, extrahovat text z obrázku a
  převést obrázek na text pomocí stručného, připraveného k okamžitému spuštění příkladu.
og_image_alt: Diagram showing how to perform OCR on a PNG image using Java
og_title: Jak provést OCR na PNG obrázku v Javě – kompletní průvodce
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
title: Jak provést OCR na PNG obrázku v Javě
url: /cs/java/ocr-basics/how-to-perform-ocr-on-a-png-image-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR na PNG obrázku v Javě

Pokud potřebujete **provádět OCR** na souboru s obrázkem, je nezbytné se naučit **jak provádět OCR** v Javě pro mnoho automatizačních úkolů. Ať už digitalizujete účtenky, indexujete naskenované dokumenty nebo budujete prohledávatelný archiv fotografií, schopnost **extrahovat text z obrázku** šetří nespočet manuálních hodin.

Tento tutoriál vám ukáže kompletní, spustitelný příklad, který načte PNG, spustí OCR engine a **rozpozná text z PNG** souborů. Také uvidíte, jak **převést obrázek na text** a jak řešit běžné problémy, jako je nízké rozlišení vstupu nebo ne‑ASCII znaky.

## Co dosáhnete

Na konci tohoto průvodce budete schopni:

* **load image java** kód, který načte PNG z disku,
* inicializovat lehký OCR engine,
* **extract text from image** a vytisknout výsledek do konzole,
* přizpůsobit řešení pro jiné formáty obrázků nebo hromadné zpracování.

Nejsou vyžadovány žádné externí služby — pouze jedna open‑source OCR knihovna (Tess4J) a runtime Java SE.

---

## Předpoklady

* Java 17 nebo novější (kód se kompiluje s JDK 17).
* Maven nebo Gradle pro správu závislostí.
* Základní znalost příkazové řádky a IDE dle vašeho výběru.
* Knihovna `tess4j` (Java wrapper pro Tesseract). Přidejte následující Maven závislost:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Pokud používáte Gradle, ekvivalent je:

```gradle
implementation 'net.sourceforge.tess4j:tess4j:5.4.0'
```

Také potřebujete soubory dat Tesseract (`.traineddata`). Stáhněte si anglický datový balíček z oficiálního repozitáře a umístěte jej do složky pojmenované `tessdata` v kořenovém adresáři projektu.

---

## Krok 1: Načtení obrázku v Javě

Načtení PNG je jednoduché pomocí standardní třídy `ImageIO`. Níže uvedený kód demonstruje **load image java** bezpečným způsobem, který zachytává výjimky:

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

**Proč je to důležité:** `ImageIO.read` automaticky detekuje formát obrázku, ale explicitně kontrolujeme, zda není výsledek `null`, abychom předešli tichým selháním při poškozeném PNG. Tento vzor je osvědčenou praxí, když **load image java** pro OCR.

---

## Krok 2: Inicializace OCR engine

Tess4J obaluje nativní binárku Tesseract a poskytuje jednoduché Java API. Následující metoda vytvoří instanci `Tesseract`, nasměruje ji do složky `tessdata` a nastaví jazyk na angličtinu:

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

**Proč to děláme:** Inicializace engine jednou a jeho opětovné použití pro více obrázků snižuje režii při startu. Volání `setOcrEngineMode` vybírá výchozí režim, který funguje dobře pro většinu PNG. Pokud narazíte na šumivé skeny, můžete experimentovat s jinými režimy (např. `OEM_LSTM_ONLY`).

---

## Krok 3: Provedení OCR a **recognize text from PNG**

Nyní spojíme načítač obrázku a OCR engine. Níže uvedená metoda spustí OCR na `BufferedImage` a vrátí extrahovaný řetězec:

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

**Plný spustitelný příklad**

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

**Očekávaný výstup**

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑09‑30
Total: $1,234.56
Thank you for your business!
```

Konzole zobrazí přesné znaky, které engine extrahoval ze souboru `sample.png`. Pokud PNG obsahuje jen jedno slovo, výstup bude toto slovo následované novým řádkem.

---

## Krok 4: Běžné varianty a okrajové případy

### 4.1 Zpracování nízkého rozlišení PNG

Tesseract funguje nejlépe na obrázcích s alespoň 300 DPI. Pokud je váš zdrojový PNG menší, před OCR jej upscaleujte:

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

Použijte `upscale(image, 2)` před voláním `extractText`, aby se zvýšila přesnost.

### 4.2 Extrahování textu v jiných jazycích

Pro **extract text from image**, který obsahuje jiné jazyky, stáhněte příslušné soubory `.traineddata` a nastavte kód jazyka:

```java
tesseract.setLanguage("eng+deu"); // English + German
```

### 4.3 Hromadné zpracování více PNG

Pokud potřebujete **recognize text from PNG** soubory ve složce, projděte adresář:

```java
File folder = new File("pngs/");
for (File file : folder.listFiles((d, name) -> name.toLowerCase().endsWith(".png"))) {
    BufferedImage img = loadPng(file.getPath());
    String text = extractText(img, ocrEngine);
    System.out.println("File: " + file.getName());
    System.out.println(text);
}
```

### 4.4 Řešení OCR chyb

Typické OCR chyby zahrnují zaměnění `0` (nula) za `O` nebo `1` za `l`. Post‑processing pomocí regulárních výrazů může výsledek vyčistit:

```java
String cleaned = recognizedText.replaceAll("[\\r\\n]+", " ").trim();
```

---

## Profesionální tipy pro spolehlivé OCR v Javě

| Tip | Důvod |
|-----|--------|
| **Používejte bezztrátový PNG** | Artefakty komprese v JPEG mohou engine zmást. |
| **Ořízněte bílé okraje** | Nadbytečná bílá plocha zvyšuje dobu zpracování a může způsobit falešné pozitivy. |
| **Nastavte `tesseract.setPageSegMode(ITesseract.PSM_AUTO)`** jen když je rozložení neznámé; jinak zvolte konkrétní režim (např. `PSM_SINGLE_BLOCK`). |
| **Cacheujte instanci `ITesseract`** |

## Co se naučíte dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobným vysvětlením, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní přístupy ve vašich projektech.

- [How to Read Text from an Image in Java Using Aspose OCR – Complete Guide](/ocr/english/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [How to Use OCR in Java – Recognize Text from Image Quickly](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/)
- [Batch Image OCR in Java – Extract Text from PNG Files Fast](/ocr/english/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}