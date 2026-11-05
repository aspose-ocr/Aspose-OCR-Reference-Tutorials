---
category: general
date: 2026-03-26
description: Vytvořte prohledávatelný PDF pomocí Aspose.OCR Java – naučte se načíst
  obrázek pro OCR, nastavit primární jazyk, extrahovat text z obrázku a uložit OCR
  PDF.
draft: false
keywords:
- create searchable pdf
- set primary language
- extract text from image
- load image ocr
- save ocr pdf
language: cs
og_description: Vytvořte prohledávatelný PDF pomocí Aspose.OCR Java. Krok za krokem
  průvodce načtením OCR obrázku, nastavením primárního jazyka, extrakcí textu z obrázku
  a uložením OCR PDF.
og_title: Vytvořte prohledávatelný PDF pomocí Aspose.OCR – průvodce pro Javu
tags:
- Aspose.OCR
- Java
- PDF
- OCR
title: Vytvořte prohledávatelný PDF pomocí Aspose.OCR – Java průvodce
url: /cs/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF pomocí Aspose.OCR – průvodce pro Java

Už jste někdy potřebovali **create searchable pdf** z naskenovaného dokumentu, ale nevedeli ste, kde začít? Nejste v tom sami – mnoho vývojářů narazí na tuto překážku, když poprvé řeší OCR v Javě. Dobrou zprávou je, že Aspose.OCR usnadňuje celý proces – od načtení obrázku po nastavení primárního jazyka a nakonec uložení PDF s OCR – a to poměrně bezbolestně. V tomto tutoriálu projdeme kompletním, spustitelným příkladem, který **extracts text from image**, umožní vám **set primary language** a skončí **save OCR pdf**, které můžete otevřít v libovolném čtečce.

Také se podíváme na několik praktických tipů, jako je povolení akcelerace GPU pro rychlejší zpracování a práce s dokumenty obsahujícími více jazyků (v našem případě Tamil + English). Na konci budete mít solidní, připravený k nasazení úryvek kódu, který můžete vložit do svého projektu.

## Co budete potřebovat

- **Java 17** (nebo jakýkoli recentní JDK; Aspose.OCR podporuje Java 8+)
- **Aspose.OCR for Java** knihovna (stáhněte z oficiální stránky nebo přidejte přes Maven)
- **license file** (nebo 30‑denní trial)
- Obrázkový soubor obsahující text (demo používá `sample-mixed-tamil-eng.jpg`)

Žádné další frameworky, žádné nativní závislosti – jen čistá Java a Aspose.JARs.

## Krok 1: Vytvoření prohledávatelného PDF – nastavení projektu

Než se ponoříme do kódu, ujistěme se, že projekt je připraven na **create searchable pdf** soubory.

```bash
# Maven dependency (add to pom.xml)
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check the latest version -->
</dependency>
```

> **Pro tip:** Udržujte číslo verze aktuální; novější verze často obsahují opravy výkonu pro využití GPU.

Nyní vytvořte jednoduchou třídu Java s názvem `RecentFeaturesDemo`. Třída bude obsahovat veškerou logiku, kterou potřebujeme pro **load image OCR**, nastavení jazykových parametrů a nakonec **save OCR pdf**.

## Krok 2: Načtení obrázku OCR a inicializace enginu

Prvním skutečným krokem v pipeline je **load image OCR**. Tím se Aspose.OCR sdělí, který soubor má analyzovat.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // 2️⃣ Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Enable GPU acceleration – speeds up recognition dramatically
        ocrEngine.getEngineSettings().setUseGpu(true);
        // Use all available CPU cores for parallel processing
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);
```

> **Proč je to důležité:** Povolení GPU (`setUseGpu(true)`) může zkrátit dobu zpracování až o 70 % na moderním hardwaru, zatímco paralelní zpracování zajišťuje, že CPU není nečinné, když je GPU zaneprázdněno.

## Krok 3: Nastavení primárního jazyka (a sekundárního)

Pokud tento krok přeskočíte, Aspose.OCR se bude snažit hádat jazyk, což je pomalejší a méně přesné. Zde je, jak **set primary language** na Tamil a přidat angličtinu jako záložní.

```java
        // 3️⃣ Define languages – primary is Tamil, secondary is English
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English);
```

> **Explanation:** Primární jazyk ovlivňuje sadu znaků a slovník používaný během rozpoznávání. Přidání sekundárního jazyka je klíčové pro dokumenty s více skripty (např. účtenka s textem v Tamil i angličtině).  
> **Edge case:** Pokud váš dokument obsahuje více než dva jazyky, můžete pro každý další zavolat `addAdditionalLanguage(...)`.

## Krok 4: Předzpracování obrázku – korekce sklonu a odšumění

Naskenované obrázky často trpí rotací nebo šumem na pozadí. Předzpracování pomáhá OCR enginu **extract text from image** spolehlivěji.

```java
        // 4️⃣ Pre‑processing options
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // auto‑rotate tilted pages
                 .setDenoise(true); // suppress speckles and background patterns
```

> **Tip:** Pokud víte, že obrázek je již čistý, můžete vynechat `setDenoise(true)`, abyste ušetřili několik milisekund.

## Krok 5: Načtení souboru obrázku

Nyní, když je engine připraven, nasměrujeme ho na soubor, který chceme analyzovat.

```java
        // 5️⃣ Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

> **Co když je cesta špatná?** Aspose.OCR vyhodí jasnou `FileNotFoundException`. Zabalte volání do try‑catch, pokud potřebujete elegantní zpracování chyb.

## Krok 6: Spuštění OCR a extrakce textu z obrázku

S veškerým nastavením je čas skutečně spustit rozpoznávání. Tento krok **extracts text from image** a připraví data potřebná pro vytvoření PDF.

```java
        // 6️⃣ Perform recognition
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Print the raw OCR output – handy for debugging
            System.out.println("Recognized text:");
            System.out.println(recognizedText);
```

Typický výstup do konzole pro demonstrační obrázek vypadá takto:

```
வணக்கம் World
This is a mixed language sample.
```

Všimnete si, že řádek v Tamil je správně vykreslen, následovaný angličtinou. To je výsledek správného **set primary language**.

## Krok 7: Uložení OCR PDF – poslední část

Poslední částí skládačky je **save OCR pdf**. Aspose.OCR může vložit neviditelnou textovou vrstvu nad původní obrázek, čímž učiní PDF prohledávatelným.

```java
            // 7️⃣ (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Otevřete `searchable.pdf` v Adobe Reader, stiskněte **Ctrl + F** a můžete vyhledávat jak tamilská, tak anglická slova – přesně to, co workflow **create searchable pdf** slibuje.

## Kompletní funkční příklad (kopíru‑vložit)

Níže je kompletní program, který můžete zkompilovat a spustit tak, jak je. Nahraďte zástupné cesty vlastními adresáři.

```java
import com.aspose.ocr.*;

public class RecentFeaturesDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Load your Aspose.OCR license (or use the 30‑day trial)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineSettings().setUseGpu(true);                     // enable CUDA GPU acceleration
        ocrEngine.getEngineSettings().setUseParallelProcessing(true);     // use multiple CPU cores
        ocrEngine.getLanguageSettings().setLanguage(Language.Tamil);      // primary language
        ocrEngine.getLanguageSettings().setSecondaryLanguage(Language.English); // secondary language
        ocrEngine.getPreprocessingSettings()
                 .setDeskew(true)   // correct image rotation
                 .setDenoise(true); // reduce background noise

        // Step 3: Load the image you want to recognize
        String imagePath = "YOUR_DIRECTORY/sample-mixed-tamil-eng.jpg";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 4: Run OCR and obtain the plain‑text result
        if (ocrEngine.recognize()) {
            String recognizedText = ocrEngine.getText();

            // Step 5: (Optional) Save a searchable PDF with an OCR layer
            String pdfPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.save(pdfPath, SaveFormat.PdfSearchable);

            System.out.println("Recognized text:");
            System.out.println(recognizedText);
            System.out.println("\nSearchable PDF saved to: " + pdfPath);
        } else {
            System.err.println("Recognition failed: " + ocrEngine.getErrorMessage());
        }
    }
}
```

Spusťte jej pomocí:

```bash
javac -cp "path/to/aspose-ocr.jar" RecentFeaturesDemo.java
java -cp ".:path/to/aspose-ocr.jar" RecentFeaturesDemo
```

Měli byste vidět extrahovaný text vytištěný do konzole, následovaný potvrzením, že **searchable pdf** byl zapsán na disk.

## Časté otázky a okrajové případy

### Co když potřebuji **load image OCR** z pole bajtů?

Můžete nahradit `ImageStream.fromFile(imagePath)` za `ImageStream.fromBytes(byteArray)`. To je užitečné, když obrázek pochází z databáze nebo webové služby.

### Jak zacházet s PDF, které již obsahují obrázky?

Aspose.OCR může pracovat přímo na stránkách PDF: `ocrEngine.setDocument(PdfDocument.fromFile("input.pdf"))`. Engine interně rasterizuje každou stránku před rozpoznáním.

### Moje GPU není detekována – mám ponechat `setUseGpu(true)`?

Pokud `setUseGpu(true)` selže, Aspose.OCR automaticky přejde na CPU. Můžete zkontrolovat `ocrEngine.getEngineSettings().isGpuAvailable()` před jeho povolením.

### Můžu **save OCR pdf** s vlastními metadaty?

Ano. Po rozpoznání použijte `ocrEngine.getPdfSaveOptions().setTitle("My Document")` nebo `setAuthor("John Doe")` před voláním `save`.

## Tipy pro výkon při zpracování velkých dávek

- **Batch processing:** Znovu použijte stejnou instanci `OcrEngine` napříč více obrázky. Mezi běhy volejte jen `ocrEngine.clear()`.
- **Thread pool:** Zabalte každý úkol obrázku do `Callable` a odešlete do `ExecutorService`. Protože jsme povolili paralelní zpracování, každý vlákno bude těžit z vícejádrového využití.
- **Memory management:** Pro gigapixelové obrázky zvažte down‑sampling pomocí `ocrEngine.getPreprocessingSettings().setResizeFactor(0.5)`, aby byl využití RAM rozumné.

## Závěr

Právě jsme prošli kompletním workflow **create searchable pdf** pomocí Aspose.OCR pro Java. Začínáme od **load image OCR**, 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}