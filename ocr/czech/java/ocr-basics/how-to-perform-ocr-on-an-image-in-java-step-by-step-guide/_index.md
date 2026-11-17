---
category: general
date: 2026-11-17
description: Naučte se, jak provádět OCR na obrázku v Javě a extrahovat text z fotografií
  pomocí jednoduchého příkladu kódu. Obsahuje tipy na čtení obrázku v Javě.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to perform OCR
- extract text image
- read image java
- convert image to text
- image to text java
language: cs
lastmod: 2026-11-17
og_description: Jak provést OCR na obrázku v Javě a rychle extrahovat text. Postupujte
  podle tohoto průvodce, abyste načetli obrázek v Javě a převedli jej na text s připraveným
  příkladem k okamžitému spuštění.
og_image_alt: Screenshot showing Java code that performs OCR on an image
og_title: Jak provést OCR na obrázku v Javě – krok za krokem
schemas:
- author: Aspose
  dateModified: '2026-11-17'
  description: Learn how to perform OCR on an image in Java and extract text from
    pictures using a simple code example. Includes read image Java tips.
  headline: How to perform OCR on an image in Java – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Java
- Image processing
- Text extraction
title: Jak provést OCR na obrázku v Javě – krok za krokem průvodce
url: /cs/java/ocr-basics/how-to-perform-ocr-on-an-image-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR na obrázku v Javě – krok za krokem

Pokud potřebujete **jak provést OCR** na obrázku, tento tutoriál vám ukáže kompletní, spustitelné řešení v Javě. Uvidíte, jak načíst soubor s obrázkem, nakonfigurovat OCR engine a získat text, který engine rozpozná.

Práce se skenovanými dokumenty, účtenkami nebo screenshoty často vyžaduje převod vizuálního obsahu na prohledávatelný text. Tento průvodce vás provede každým krokem, od načtení obrázku až po vytištění získaného textu, a také se zabývá běžnými úskalími, jako jsou nepodporované formáty souborů a nulové výsledky.

## Předpoklady

Než začnete, ujistěte se, že máte:

* Java Development Kit (JDK) 8 nebo novější nainstalovaný.
* Nástroj pro sestavování (Maven nebo Gradle) pro stažení OCR knihovny.
* Soubor s obrázkem (JPEG, PNG, BMP), který chcete zpracovat.

Kód používá **OCR knihovnu z balíčku `com.asprise.ocr`**, protože vyžaduje jen jeden JAR a funguje na všech hlavních platformách. Nahraďte ji jiným poskytovatelem (Tesseract, Google Vision, atd.) výměnou importních příkazů a kódu pro inicializaci engine.

## Krok 1: Přidejte OCR závislost

Pokud používáte Maven, přidejte následující závislost do svého `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.2.0</version>
</dependency>
```

Pro Gradle umístěte tento řádek do `build.gradle`:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.2.0'
```

Tyto řádky zajistí, že **read image Java** kód se může zkompilovat a že OCR engine bude k dispozici za běhu.

## Krok 2: Načtěte obrázek v Javě

Načtení souboru s obrázkem je první konkrétní krok v jakémkoli **extract text image** workflow. Vestavěná třída Javy `ImageIO` zvládá většinu běžných formátů.

```java
import java.awt.image.BufferedImage;
import java.io.File;
import javax.imageio.ImageIO;

/**
 * Loads an image from the supplied path.
 *
 * @param path absolute or relative path to the image file
 * @return a BufferedImage instance, or null if the file cannot be read
 */
private static BufferedImage loadImage(String path) {
    try {
        return ImageIO.read(new File(path));
    } catch (Exception e) {
        System.err.println("Failed to read image: " + e.getMessage());
        return null;
    }
}
```

**Proč je to důležité:** `ImageIO.read` vrací `null` pro nepodporované formáty nebo poškozené soubory. Výše uvedená metoda zaznamená problém a vrátí `null`, aby mohl další krok reagovat elegantně.

## Krok 3: Vytvořte a nakonfigurujte OCR engine

OCR engine musí vědět, jaký jazyk má rozpoznávat. Nastavení jazyka výrazně zvyšuje přesnost, zejména u dokumentů v jiných jazycích než angličtina.

```java
import com.asprise.ocr.Ocr;

/**
 * Instantiates an OCR engine configured for English.
 *
 * @return a ready‑to‑use Ocr object
 */
private static Ocr createEngine() {
    Ocr ocrEngine = new Ocr();
    // The first argument is the language; "eng" is the ISO code for English.
    ocrEngine.startEngine("eng", Ocr.SPEED_FAST);
    return ocrEngine;
}
```

**Proč je to důležité:** Spuštění engine je relativně náročná operace, takže jej vytvoříte jednou a znovu použijete pro více obrázků, pokud vaše aplikace zpracovává dávky.

## Krok 4: Proveďte OCR a převedete obrázek na text

Jakmile je obrázek načten a engine připraven, můžete spustit krok rozpoznání. Toto je jádro **how to perform OCR**.

```java
/**
 * Runs OCR on a BufferedImage and returns the recognized text.
 *
 * @param ocrEngine an initialized Ocr instance
 * @param image     the image to process
 * @return the extracted text, or an empty string if nothing is recognized
 */
private static String extractText(Ocr ocrEngine, BufferedImage image) {
    if (image == null) {
        return "";
    }
    // The third parameter (0) tells the engine to return plain text.
    String result = ocrEngine.recognize(image, 0);
    return result != null ? result.trim() : "";
}
```

**Zvládání okrajových případů:** Pokud je obrázek `null`, metoda vrátí prázdný řetězec místo vyhození `NullPointerException`. To činí okolní kód odolnějším při práci se soubory dodanými uživatelem.

## Krok 5: Zobrazte získaný text

Nakonec vytiskněte výsledek do konzole nebo jej předávejte dalšímu komponentu (např. databázi nebo UI widgetu).

```java
/**
 * Demonstrates the full OCR workflow.
 *
 * @param args command‑line arguments (first argument = path to image)
 */
public static void main(String[] args) {
    if (args.length == 0) {
        System.err.println("Usage: java OcrDemo <path-to-image>");
        return;
    }

    String imagePath = args[0];
    BufferedImage image = loadImage(imagePath);
    Ocr ocrEngine = createEngine();

    String text = extractText(ocrEngine, image);
    System.out.println("=== Recognized Text ===");
    System.out.println(text.isEmpty() ? "(no text detected)" : text);

    // Clean up the OCR engine to free native resources.
    ocrEngine.stopEngine();
}
```

Když spustíte program pomocí `java OcrDemo sample.jpg`, konzole zobrazí rozpoznané znaky. Tím je dokončen cyklus **convert image to text**.

### Očekávaný výstup

```
=== Recognized Text ===
The quick brown fox jumps over the lazy dog.
```

Pokud obrázek neobsahuje žádné čitelné znaky, program vypíše `(no text detected)`.

## Běžné varianty a jak je přizpůsobit

| Variation | What changes | When to use |
|-----------|--------------|-------------|
| **Different language** | Replace `"eng"` with `"spa"` for Spanish, `"fra"` for French, etc. | Documents written in a language other than English |
| **Batch processing** | Loop over a list of file paths, reuse the same `Ocr` instance. | Large sets of scanned pages |
| **Higher accuracy** | Use `Ocr.SPEED_SLOW` or enable `ocrEngine.setConfig("tessedit_char_whitelist", "0123456789")` for numeric-only scans. | When OCR quality is critical (e.g., invoice numbers) |
| **Tesseract alternative** | Swap the import to `net.sourceforge.tess4j.Tesseract` and adjust the initialization code. | Projects that already depend on Tesseract |

## Profesionální tipy

* **Zmenšete velké obrázky** před předáním engine; rychlost OCR se škáluje s počtem pixelů.
* **Předzpracujte** obrázek (odstín šedi, zvýšení kontrastu) pomocí knihoven jako OpenCV, pokud je zdroj šumivý.
* **Ukládejte OCR engine do cache**, pokud jej voláte mnohokrát během krátké doby – spouštění a zastavování engine představuje režii.
* **Ověřujte výsledek** pomocí regulárních výrazů, když očekáváte konkrétní formát (např. datum, telefonní číslo).

## Závěr

Nyní víte **jak provést OCR** na obrázku v Javě, od načtení souboru po zobrazení získaného textu. Tutoriál pokryl **read image Java**, **extract text image**, **convert image to text** a **image to text java** techniky a poskytl praktické tipy pro reálné scénáře.  

Odtud můžete:

* Integrovat krok OCR do webové služby, která přijímá nahrané soubory.
* Kombinovat výstup s indexem pro full‑textové vyhledávání ve skenovaných dokumentech.
* Prozkoumat pokročilé možnosti OCR, jako je podpora více jazyků nebo vlastní sady znaků.

Šťastné programování a užívejte si převod obrázků na prohledávatelný text!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohl zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [How to Use OCR in Java – Extract Text from Image with Spell Correction](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-extract-text-from-image-with-spell-co/)
- [Convert Image to Text in Java Using Aspose OCR – Full Guide](/ocr/english/java/ocr-operations/convert-image-to-text-in-java-using-aspose-ocr-full-guide/)
- [How to Enable GPU for OCR in Java – Extract Text from Image](/ocr/english/java/advanced-ocr-techniques/how-to-enable-gpu-for-ocr-in-java-extract-text-from-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}