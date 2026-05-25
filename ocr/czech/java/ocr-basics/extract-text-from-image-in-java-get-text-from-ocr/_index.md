---
category: general
date: 2026-05-25
description: Extrahujte text z obrázku v Javě pomocí OCR. Naučte se, jak načíst obrázek
  pro OCR, rozpoznat text z fotografie a získat text z OCR pomocí jednoduchého příkladu
  kódu.
draft: false
keywords:
- extract text from image
- get text from ocr
- recognize text from photo
- java image to text
- load image for ocr
language: cs
og_description: Extrahujte text z obrázku v Javě pomocí krok‑za‑krokem průvodce. Naučte
  se načíst obrázek pro OCR, rozpoznat text z fotografie a efektivně získat text z
  OCR.
og_title: Extrahovat text z obrázku v Javě – Získat text z OCR
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  headline: Extract Text from Image in Java – Get Text from OCR
  type: TechArticle
- description: Extract text from image in Java using OCR. Learn how to load image
    for OCR, recognize text from photo, and get text from OCR with a simple code example.
  name: Extract Text from Image in Java – Get Text from OCR
  steps:
  - name: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
    text: '**Wrong language setting** – If you forget step 2, the engine defaults
      to English, turning Cyrillic characters into gibberish. Always double‑check
      the language code.'
  - name: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
    text: '**Image quality matters** – Low‑resolution or blurry photos will degrade
      accuracy. Pre‑process with contrast enhancement or binarization if needed.'
  - name: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
    text: '**File path quirks** – On Windows, backslashes need escaping (`C:\images\file.jpg`).
      Using `Path.of(...)` from `java.nio.file` sidesteps this.'
  - name: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
    text: '**Memory leaks** – `OcrEngine` holds native resources. Call `ocrEngine.dispose()`
      when you’re done, especially in long‑running services.'
  - name: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
    text: '**Thread safety** – The engine isn’t thread‑safe out of the box. Create
      a separate instance per thread or synchronize access.'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Extrahovat text z obrázku v Javě – Získat text pomocí OCR
url: /cs/java/ocr-basics/extract-text-from-image-in-java-get-text-from-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku v Javě – Získat text z OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nebyli jste si jisti, kterou knihovnu pro Javu zvolit? Nejste v tom sami. Ať už digitalizujete účtenky, získáváte sériová čísla z fotografií produktů, nebo si jen hrajete na zábavný vedlejší projekt, převod obrázku na editovatelný text je běžná překážka.

V tomto tutoriálu projdeme kompletním, připraveným k okamžitému spuštění příkladem, který vám ukáže, jak **načíst obrázek pro OCR**, nakonfigurovat engine a nakonec **rozpoznat text z fotografie**, abyste mohli **získat text z OCR** pomocí jen několika řádků kódu. Žádné nejasné odkazy – vše, co potřebujete, je zde.

## Co se naučíte

* Jak nastavit lehký OCR engine v Javě.  
* Přesné kroky k **načtení obrázku pro OCR** a práci s různými cestami k souborům.  
* Proč nastavení jazyka má význam, když chcete **extrahovat text z obrázku**, který není v angličtině.  
* Jak bezpečně vypsat výsledek a co dělat, když engine nic nevrátí.  
* Několik profesionálních tipů, jak se vyhnout nejčastějším úskalím.

Na konci tohoto průvodce budete mít samostatný program, který načte JPEG (nebo PNG) obsahující ukrajinské znaky a vypíše rozpoznaný řetězec do konzole. Klidně si vyměňte jazyk nebo obrázek – vše je modulární.

---

![Diagram showing the flow of extracting text from image using Java OCR engine](/images/extract-text-from-image-java.png)

*Alt text: Diagram toku procesu extrahování textu z obrázku v Javě.*

## Požadavky

* **Java Development Kit (JDK) 11+** – kód používá moderní modulový systém, ale starší verze fungují s menšími úpravami.  
* **Maven nebo Gradle** – pro stažení OCR knihovny (použijeme **Asprise OCR** jako lehkou, zdarma pro vývojovou verzi).  
* Vzorek souboru obrázku (např. `ukrainian_sign.jpg`) umístěný na místě, kde ho program může číst.  
* Základní znalost `main` metody v Javě a zpracování výjimek.

Pokud máte vše připravené, můžete začít. Jinak si stáhněte JDK od Oracle nebo AdoptOpenJDK a nastavte jednoduchý Maven projekt – nic složitého.

---

## Krok 1: Přidání OCR závislosti

Nejprve řekněte svému nástroji pro sestavení, aby stáhl OCR engine. Pro Maven vložte následující do `pom.xml`:

```xml
<dependency>
    <groupId>com.asprise.ocr</groupId>
    <artifactId>asprise-ocr</artifactId>
    <version>1.0.2</version>
</dependency>
```

Pokud dáváte přednost Gradlu, ekvivalent je:

```gradle
implementation 'com.asprise.ocr:asprise-ocr:1.0.2'
```

Tyto koordináty stáhnou kompaktní JAR, který obsahuje `OcrEngine`, `OcrLanguage` a pomocné třídy, které použijeme. Pro základní latinské a cyrilické skripty nejsou potřeba žádné další nativní binární soubory.

## Krok 2: Vytvořte Java třídu pro **extrahování textu z obrázku**

Nyní napíšeme skutečný program. Uložte následující jako `ExtractTextDemo.java` do `src/main/java/com/example/ocr/`.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;

/**
 * Demonstrates how to extract text from image using Asprise OCR.
 * The example loads a JPEG, sets the language to Ukrainian,
 * runs recognition, and prints the result.
 */
public class ExtractTextDemo {

    public static void main(String[] args) {
        // ---- 1️⃣  Initialize the OCR engine ---------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ---- 2️⃣  Configure the engine to recognize Ukrainian text -----------
        // This is crucial if your image contains non‑Latin characters.
        ocrEngine.getEngineOptions().setLanguage(OcrLanguage.UKRAINIAN);

        // ---- 3️⃣  Load the image that contains Ukrainian characters ----------
        // Replace the path with the location of your own picture.
        String imagePath = "YOUR_DIRECTORY/ukrainian_sign.jpg";
        try {
            ocrEngine.getImage().loadFromFile(imagePath);
        } catch (Exception e) {
            System.err.println("Failed to load image: " + e.getMessage());
            return;
        }

        // ---- 4️⃣  Perform OCR recognition and obtain the extracted text -------
        String recognizedText;
        try {
            recognizedText = ocrEngine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Recognition error: " + e.getMessage());
            return;
        }

        // ---- 5️⃣  Output the recognized text to the console -------------------
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

### Proč tato struktura funguje

* **Samostatné číslované bloky** usnadňují sledování toku, zejména když hledáte místo, kde **načíst obrázek pro OCR** nebo **rozpoznat text z fotografie**.  
* `try/catch` kolem načítání obrázku a rozpoznání zajišťuje, že program selže elegantně – užitečné, když je špatná cesta k souboru nebo OCR engine nemůže najít jazyková data.  
* Nastavení jazyka na začátku (krok 2) výrazně zvyšuje přesnost pro ne‑anglické skripty. Pokud později potřebujete **java image to text** pro jiné jazyky, stačí vyměnit `OcrLanguage.UKRAINIAN` za `OcrLanguage.ENGLISH`, `FRENCH` atd.

## Krok 3: Sestavení a spuštění programu

Z kořenového adresáře projektu spusťte:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.ocr.ExtractTextDemo"
```

Nebo pokud používáte Gradle:

```bash
./gradlew run --args="com.example.ocr.ExtractTextDemo"
```

Za předpokladu, že `ukrainian_sign.jpg` obsahuje text *«Ласкаво просимо»* (ukrajinsky „Vítejte“), měli byste vidět něco jako:

```
=== OCR Result ===
Ласкаво просимо
```

Tento výstup potvrzuje, že jste úspěšně **extrahovali text z obrázku** a **získali text z OCR** v jednom spuštění.

## Krok 4: Úprava pracovního postupu – od **Java Image to Text** v reálných projektech

Zatímco demo je minimalistické, reálné aplikace často potřebují o něco víc:

| Scénář | Co upravit | Důvod |
|----------|----------------|--------|
| **Dávkové zpracování** | Procházet `List<Path>` a ukládat každý výsledek do databáze. | Snižuje manuální práci, když máte stovky fotografií. |
| **Různé formáty obrázků** | Použijte `ImageIO.read(new File(path))` pro předzpracování a poté předávejte `BufferedImage` do `ocrEngine.getImage().loadFromBufferedImage(bufImg)`. | Zpracovává PNG, BMP nebo dokonce PDF po konverzi. |
| **Ladění výkonu** | Zavolejte `ocrEngine.getEngineOptions().setSpeed(OcrEngine.Speed.FAST)`, pokud vám vyhovuje mírně nižší přesnost. | Zrychluje rozpoznávání na slabém hardware. |
| **Post‑zpracování** | Odstraňte mezery, nahraďte běžné chyby OCR (`0` → `O`, `1` → `I`). | Zlepšuje kvalitu dat v následných krocích. |

Tyto varianty zachovávají základní myšlenku — **rozpoznat text z fotografie** — a zároveň vám poskytují flexibilitu pro produkční zatížení.

## Časté úskalí a profesionální tipy

1. **Špatné nastavení jazyka** – Pokud zapomenete krok 2, engine výchozí nastavení je angličtina, což převádí cyrilické znaky na nesmysly. Vždy dvojitě zkontrolujte kód jazyka.  
2. **Kvalita obrázku má význam** – Nízké rozlišení nebo rozmazané fotografie sníží přesnost. Předzpracujte je zvýšením kontrastu nebo binarizací, pokud je potřeba.  
3. **Zvláštnosti cest k souborům** – Ve Windows je třeba escapovat zpětná lomítka (`C:\\images\\file.jpg`). Použití `Path.of(...)` z `java.nio.file` to obejde.  
4. **Úniky paměti** – `OcrEngine` drží nativní zdroje. Zavolejte `ocrEngine.dispose()`, když skončíte, zejména v dlouho běžících službách.  
5. **Bezpečnost vláken** – Engine není z výroby thread‑safe. Vytvořte samostatnou instanci pro každé vlákno nebo synchronizujte přístup.

## Kompletní funkční příklad (vše v jednom)

Níže je jeden soubor, který můžete zkopírovat a vložit do libovolného IDE. Obsahuje volání `dispose()` a malou pomocnou metodu, aby byl kód o něco přehlednější.

```java
package com.example.ocr;

import com.asprise.ocr.OcrEngine;
import com.asprise.ocr.OcrLanguage;
import java.nio.file.Path;

/**
 * Complete, runnable demo that extracts text from an image using Java OCR.
 */
public class FullDemo {

    public static void main(String[] args) {
        // Path to the image – change this to your own file.
        Path imgPath = Path.of("YOUR_DIRECTORY/ukrainian_sign.jpg");

        // Run the OCR workflow and capture the output.
        String result = extractTextFromImage(imgPath, OcrLanguage.UKRAINIAN);
        if (result != null) {
            System.out.println("=== OCR Result ===");
            System.out.println(result);
        }
    }

    /**
     * Core method that encapsulates the 5‑step OCR process.
     *
     * @param imagePath Path to the image file.
     * @param language  Desired OCR language.
     * @return Recognized text, or {@code null} if something went wrong.
     */
    private static String extractTextFromImage(Path imagePath, OcrLanguage language) {
        OcrEngine engine = new OcrEngine();
        try {
            // 1️⃣ Set language
            engine.getEngineOptions().setLanguage(language);

            // 2️⃣ Load image
            engine.getImage().loadFromFile(imagePath.toString());

            // 3️⃣ Recognize and return text
            return engine.recognize().getText();
        } catch (Exception e) {
            System.err.println("Error during OCR: " + e.getMessage());
            return null;
        } finally {
            // 4️⃣ Release native resources
            engine.dispose();
        }
    }
}
```

Spuštěním tohoto programu získáte stejný výstup v konzoli jako dříve. Klidně nahraďte `OcrLanguage.UKRAINIAN` za `OcrLanguage.ENGLISH` nebo jakýkoli jiný podporovaný jazyk, abyste viděli, jak se engine přizpůsobí.

## Závěr

Prošli jsme vším, co potřebujete k **extrahování textu z obrázku** pomocí Javy: od přidání OCR závislosti,

## Související tutoriály

- [rozpoznat textový obrázek pomocí Aspose OCR – Kompletní Java OCR tutoriál](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Jak OCR obrázkový text s jazykem pomocí Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Převést obrázek na text v Javě pomocí Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}