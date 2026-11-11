---
category: general
date: 2026-04-29
description: Naučte se, jak provádět OCR souborů TIFF pomocí režimu streamování Aspose
  OCR. Tento průvodce vám ukáže, jak efektivně extrahovat textové dlaždice z dlaždicových
  TIFF obrázků.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: cs
og_description: jak provést OCR TIFF pomocí Aspose OCR streaming. Krok‑za‑krokem kód
  pro extrakci textových dlaždic z velkých TIFF obrázků.
og_title: Jak provést OCR TIFF – kompletní průvodce streamováním
tags:
- OCR
- Java
- Aspose
- TIFF
title: Jak provést OCR TIFF – streamovat velké TIFFy a extrahovat textové dlaždice
  v Javě
url: /cs/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# jak OCR tiff – Streamování velkých TIFF souborů a extrakce textových dlaždic v Javě

Už jste se někdy zamýšleli **jak OCR tiff** soubory, které jsou tak velké, že se nevejdou najednou do paměti? Nejste v tom sami. Mnoho vývojářů narazí na problém, když jsou jejich TIFF obrázky rozděleny na desítky dlaždic a běžné volání `ocrEngine.recognize()` selže.  

Dobrá zpráva? Režim streamování v Aspose OCR vám umožní předávat každou dlaždici jako samostatný stream, takže můžete **extrahovat textové dlaždice** bez přetížení haldy. V tomto tutoriálu projdeme kompletním, připraveným příkladem v Javě, vysvětlíme, proč je každý řádek důležitý, a upozorníme na úskalí, kterým se chcete vyhnout.

> **Co získáte:** spustitelný program, který za běhu spojí dlaždicové TIFFy, vypíše sloučený text a ukáže vám, jak přizpůsobit kód pro jiné jazyky nebo formáty obrázků.

---

## Požadavky

- **Java 17** nebo novější (kód používá try‑with‑resources, takže funguje i na JDK 8+, ale JDK 17 je aktuální LTS).
- **Aspose.OCR for Java** knihovna (v. 23.10 nebo novější). Přidejte ji pomocí Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Složka obsahující jednotlivé TIFF dlaždice (např. `tile_0.tif`, `tile_1.tif`, …).  
- Volitelně: IDE jako IntelliJ IDEA nebo VS Code – ale prostý textový editor také stačí.

---

## Krok 1 – Připravte cesty k dlaždicím (Proč je to důležité)

Než OCR engine může něco udělat, musí vědět, kde se každá část obrázku nachází. Hard‑codování cest je v pořádku pro ukázku, ale v produkci pravděpodobně budete procházet adresář nebo číst manifest soubor.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Pro tip:** uchovávejte dlaždice v lexikografickém pořadí (0, 1, 2…) protože engine spojí rozpoznaný text ve stejném pořadí, v jakém mu předáte streamy.

---

## Krok 2 – Zapněte režim streamování v OCR engine (Primární klíčové slovo)

Nyní vytvoříme instanci `OcrEngine` a zapneme streamování. To je jádro **jak OCR tiff** bez načítání celého obrázku do RAM.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Why streaming?**  
Když je zavoláno `setEnableStreaming(true)`, engine zachází s každým příchozím `ImageStream` jako s pokračováním předchozího. Vytvoří interní virtuální plátno, virtuálně spojí dlaždice a spustí OCR až na konci. Tím se vyhnete „OutOfMemoryError“, ke kterému by došlo, kdybyste se pokusili načíst multi‑gigabajtový TIFF najednou.

---

## Krok 3 – Přidejte každou dlaždici jako vstupní stream (Sekundární klíčové slovo)

Zde je smyčka, která předává každou dlaždici engine. Blok `try‑with‑resources` zajišťuje, že souborový handle je rychle uzavřen, což je klíčové při práci s desítkami souborů.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Všimněte si, že fráze **extrahovat textové dlaždice** je přirozeně zakomponována: každá iterace *extrahuje* text z jedné dlaždice a přidává jej do rostoucího výsledného souboru.

---

## Krok 4 – Spusťte rozpoznání a vypište sloučený text (Primární klíčové slovo)

Po zařazení všech dlaždic se jedním voláním provede OCR na virtuálním obrázku. Výsledek obsahuje celý text, jako byste měli jeden obrovský TIFF.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Očekávaný výstup** (předpokládáme, že dlaždice obsahují frázi „Hello World“ rozdělenou mezi sebou):

```
=== OCR Output ===
Hello World
```

Pokud vaše dlaždice obsahují více řádků, objeví se ve stejném pořadí, v jakém jste je poskytli. Výsledek můžete také zapsat do souboru pomocí `ocrResult.getText()` pro další zpracování.

---

## Krok 5 – Kompletní, spustitelný příklad (Všechny kroky na jednom místě)

Níže je celý program, který můžete zkopírovat do souboru `StreamingExample.java`. Obsahuje všechny importy, komentáře i ošetření chyb.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Uložte, přeložte a spusťte:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Měli byste vidět spojený OCR text vytištěný v konzoli.

---

## Pokročilé tipy & běžné úskalí (Proč to funguje)

| Problém | Proč k tomu dochází | Jak opravit / optimalizovat |
|---------|---------------------|-----------------------------|
| **Chyby nedostatku paměti** | Načtení plnohodnotného TIFF do `BufferedImage` spotřebuje celou haldu. | Použijte režim streamování (`setEnableStreaming(true)`) – engine nikdy nevyprodukuje celý obrázek. |
| **Nesoulad pořadí dlaždic** | Soubory se řadí abecedně místo číselně (např. `tile_10.tif` před `tile_2.tif`). | Číslujte s nulovým doplněním (`tile_00.tif`, `tile_01.tif`) nebo řaďte programově pomocí `Comparator`. |
| **Špatný jazyk** | OCR ve výchozím nastavení používá angličtinu; text v jiném jazyce bude poškozený. | Zavolejte `ocrEngine.getLanguageSettings().setLanguage("fr")` (nebo jakýkoli podporovaný ISO kód). |
| **Částečné selhání** | Jeden poškozený soubor zastaví celý proces. | Zachyťte `IOException` pro každou dlaždici, logujte a rozhodněte, zda pokračovat nebo ukončit. |
| **Úzké hrdlo výkonu** | Disková I/O dominuje při čtení mnoha malých souborů. | Zabalte dlaždice do ZIPu a streamujte z paměti, nebo použijte rychlý SSD. |

---

## Kdy použít streamování vs. OCR jedné obrázkové souboru

- **Streamování** je ideální pro:
  - Vícestránkové TIFFy nebo gigapixelové skeny.
  - Situace s omezenou pamětí (např. Docker kontejnery, mobilní zařízení).
  - Pipeline, které již přijímají úseky obrázku (např. videozáznamy z kamery).

- **OCR jedné obrázkové souboru** funguje dobře pro:
  - Malé PNG/JPEG soubory (< 5 MB).
  - Jednorázové skeny, kde jednoduchost převyšuje výkon.

---

## Závěr

Nyní máte pevné pochopení **jak OCR tiff** soubory pomocí streamovacích možností Aspose OCR a víte, jak **extrahovat textové dlaždice** efektivně. Kompletní řešení – inicializace engine, zapnutí streamování, přidání každé dlaždice a nakonec rozpoznání virtuálního plátna – pokrývá „co“, „proč“ i „jak“, co potřebujete pro produkčně připravený kód.

Další kroky? Vyzkoušejte výměnu `"en"` za jiný jazyk, nebo experimentujte s různými formáty obrázků (`.png`, `.jpg`). Výsledek OCR můžete také přímo poslat do vyhledávacího indexu nebo generátoru PDF. Vzor zůstává stejný: stream, spoj, rozpoznávej.

Máte otázky ohledně škálování na stovky dlaždic, nebo potřebujete pomoc s ošetřením chyb? Zanechte komentář níže a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}