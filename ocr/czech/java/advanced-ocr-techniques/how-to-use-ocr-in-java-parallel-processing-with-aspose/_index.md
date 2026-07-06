---
category: general
date: 2026-02-27
description: Naučte se, jak používat OCR v Javě k extrakci textu z obrázků ve formátech
  TIFF a PDF pomocí paralelního zpracování Aspose OCR. Rychlý, jednoduchý návod.
draft: false
keywords:
- how to use ocr
- perform ocr on pdf
- extract text from tiff
- extract image text java
language: cs
og_description: Naučte se, jak používat OCR v Javě k extrahování textu z obrázků ve
  formátech TIFF a PDF pomocí paralelního zpracování Aspose OCR.
og_title: Jak používat OCR v Javě – paralelní zpracování s Aspose
tags:
- OCR
- Java
- Aspose
title: Jak používat OCR v Javě – paralelní zpracování s Aspose
url: /cs/java/advanced-ocr-techniques/how-to-use-ocr-in-java-parallel-processing-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak používat OCR v Javě – Paralelní zpracování s Aspose

Už jste se někdy zamýšleli **jak používat OCR** k získání textu ze skenovaného dokumentu bez zbytečného úsilí? Nejste v tom sami. Vývojáři často narazí na problém, když potřebují číst text z obrázků—zejména TIFF a PDF—a zároveň udržet výkon pod kontrolou.  

V tomto tutoriálu vám ukážeme kompletní, připravené řešení, které **extrahuje text z obrázku v Javě** pomocí Aspose OCR, zapíná paralelní zpracování a dokonce umožňuje omezit počet vláken. Na konci budete mít jedinou třídu, která dokáže **provádět OCR na PDF** souborech a **extrahovat text z TIFF** obrázků během zlomku času, který by zabral jednovláknový přístup.

> **Co si odnesete**  
> * Jasné vysvětlení, proč je paralelní OCR důležité.  
> * Kompletní Java program (bez chybějících importů).  
> * Tipy, jak ladit využití vláken a jak řešit běžné úskalí.  

## Požadavky

- Java 8 nebo novější (kód se také kompiluje s JDK 11).  
- Knihovna Aspose.OCR pro Java – nejnovější JAR můžete stáhnout z Maven Central (`com.aspose:aspose-ocr`).  
- Soubor s obrázkem (`.tif`, `.tiff`) nebo PDF, které chcete zpracovat.  
- Přiměřené množství RAM — paralelní zpracování spustí několik vláken, ale Aspose je paměťově úsporný.

Pokud máte vše připravené, pojďme na to.

![Diagram ukazující OCR pipeline – jak používat OCR v Javě s paralelním zpracováním](how-to-use-ocr-pipeline.png)

*Image alt text: diagram příkladu použití OCR*

---

## Krok 1: Nastavte svůj projekt a přidejte Aspose OCR

### Proč je to důležité

Než budete moci **provádět OCR na PDF** nebo jakémkoli obrázku, musí být knihovna na classpath. Bez ní kompilátor vyhodí `ClassNotFoundException` a zaseknete se ve druhém kroku.

### Jak na to

Pokud používáte Maven, přidejte závislost:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the newest version -->
</dependency>
```

Pro Gradle:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Tip:** Udržujte číslo verze v souladu s poznámkami k vydání Aspose; novější verze často obsahují vylepšení výkonu pro paralelní zpracování.

---

## Krok 2: Vytvořte OCR engine a povolte paralelní zpracování

### Proč je to důležité

Ve výchozím nastavení Aspose OCR běží v jednom vlákně. Když mu předáte více‑stránkový PDF nebo dávku TIFF, engine zpracuje každou stránku po sobě — pomalu a neefektivně. Povolení paralelního zpracování umožní CPU zpracovat několik stránek najednou, což dramaticky zkrátí dobu běhu.

### Kód

```java
import com.aspose.ocr.*;

public class ParallelOcrDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Path to the input file (TIFF or PDF)
        String inputPath = "YOUR_DIRECTORY/input.tif";

        // 2️⃣ Instantiate the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Turn on parallel processing – this is the core of how to use OCR efficiently
        ocrEngine.getConfig().setUseParallelProcessing(true);

        // 4️⃣ (Optional) Limit threads – you can cap it to the number of cores you have
        // ocrEngine.getConfig().setMaxThreads(Runtime.getRuntime().availableProcessors());

        // 5️⃣ Run OCR
        OcrResult ocrResult = ocrEngine.processImage(inputPath);

        // 6️⃣ Output the recognised text
        System.out.println(ocrResult.getText());
    }
}
```

**Vysvětlení klíčových řádků**

- `setUseParallelProcessing(true)`: říká Aspose, aby rozložil zátěž na dostupná CPU jádra.  
- `setMaxThreads(...)`: můžete omezit velikost thread poolu, pokud běžíte na sdíleném serveru nebo chcete ponechat rezervu pro jiné služby.  
- `processImage(inputPath)`: funguje jak pro soubory s obrázky, tak pro PDF dokumenty, takže stejný volání **provádí OCR na PDF** i na TIFF.

---

## Krok 3: Zpracování různých typů vstupu – PDF vs. TIFF

### Proč je to důležité

I když `processImage` přijímá řetězec s cestou, podkladové zpracování se liší. PDF často obsahují více stránek, z nichž každá se stane samostatnou OCR úlohou. TIFF může být jednostránkový nebo více‑stránkový; Aspose zachází s každým rámcem jako se stránkou.

### Na co si dát pozor

| Vstup | Typický problém | Doporučené řešení |
|------|----------------|-------------------|
| PDF | Velké PDF mohou vyčerpat paměť, pokud jsou načteny všechny stránky najednou. | Použijte `ocrEngine.getConfig().setMemoryOptimization(true);` (k dispozici v novějších verzích). |
| Více‑stránkový TIFF | Některé starší TIFF používají nepodporovanou kompresi. | Převeďte do podporovaného formátu nejprve, nebo použijte Aspose‑ův pomocník `TiffImage`. |

Níže je rychlý úryvek, který ukazuje, jak detekovat typ souboru a zalogovat přátelskou zprávu:

```java
import java.nio.file.*;

String ext = Files.probeContentType(Paths.get(inputPath)).toLowerCase();
if (ext.contains("pdf")) {
    System.out.println("Processing a PDF – expect multiple pages.");
} else if (ext.contains("tiff") || ext.contains("tif")) {
    System.out.println("Processing a TIFF image.");
} else {
    System.out.println("Unsupported file type. This demo works with PDF and TIFF.");
}
```

---

## Krok 4: Ověření výstupu – Co byste měli vidět?

Když program skončí, uvidíte surový extrahovaný text vytištěný na konzoli. Pro jednoduchou naskenovanou fakturu může výstup vypadat takto:

```
Invoice #12345
Date: 02/15/2026
Total Amount: $1,250.00
Thank you for your business!
```

Pokud OCR narazí na problém s konkrétní stránkou, Aspose vloží zástupnou řádku jako `[Unrecognizable]`. Tyto řádky můžete později odfiltrovat, pokud potřebujete čistá data.

**Rychlá kontrola**

```java
if (ocrResult.getText().trim().isEmpty()) {
    System.err.println("No text detected – verify the image quality or try a different language.");
}
```

---

## Krok 5: Ladění výkonu – Kdy upravit počet vláken

### Proč je to důležité

Více vláken neznamená vždy rychlejší výsledky. Na 4‑jádrovém notebooku může spuštění 8 vláken způsobit režii spojenou s přepínáním kontextů. Naopak na 32‑jádrovém serveru můžete chtít využít plný výkon.

### Jak najít optimální nastavení

```java
int cores = Runtime.getRuntime().availableProcessors();
System.out.println("Available processors: " + cores);

// Experiment: set max threads to half the cores first
ocrEngine.getConfig().setMaxThreads(Math.max(1, cores / 2));
```

Spusťte program s různými nastaveními a změřte čas:

```java
long start = System.nanoTime();
ocrEngine.processImage(inputPath);
long elapsed = System.nanoTime() - start;
System.out.println("Elapsed time (ms): " + elapsed / 1_000_000);
```

Zaznamenejte časy, vyberte konfiguraci, která poskytuje nejlepší propustnost, a použijte ji v produkci.

---

## Krok 6: Rozšíření ukázky – Dávkové zpracování více souborů

Pokud potřebujete **extrahovat text z obrázku v Javě** z celého adresáře, zabalte jádro logiky do smyčky:

```java
Path folder = Paths.get("YOUR_DIRECTORY");
try (DirectoryStream<Path> stream = Files.newDirectoryStream(folder, "*.{tif,tiff,pdf}")) {
    for (Path file : stream) {
        System.out.println("\n--- Processing: " + file.getFileName() + " ---");
        OcrResult result = ocrEngine.processImage(file.toString());
        // Save or further process result.getText()
    }
}
```

Tento vzor dobře škáluje, protože engine již paralelně zpracovává stránky každého souboru. Vnější smyčka běží sekvenčně, ale můžete také odeslat každý soubor do `ExecutorService`, pokud chcete využít masivní CPU farmu.

---

## Časté úskalí a jak se jim vyhnout

| Příznak | Pravděpodobná příčina | Řešení |
|---------|----------------------|--------|
| `OutOfMemoryError` | Příliš mnoho stránek načtených najednou (zejména u obrovských PDF). | Povolit optimalizaci paměti (`setMemoryOptimization(true)`) nebo zpracovávat PDF stránku po stránce pomocí `processPage`. |
| Zkreslené znaky | Špatná konfigurace jazyka/znakové sady. | Zavolejte `ocrEngine.getConfig().setLanguage(OcrLanguage.English);` nebo odpovídající jazykový enum. |
| Pomalejší výkon i přes nastavený paralelní režim | OS omezuje tvorbu vláken nebo JVM běží s malým haldem. | Zvyšte parametr `-Xmx`, a ověřte limity OS pro vlákna (`ulimit -u`). |
| Prázdný výstup | Rozlišení vstupního obrázku < 300 dpi. | Zvyšte rozlišení obrázku před OCR nebo použijte skener, který výstupuje ve vyšším rozlišení. |

---

## Shrnutí – Co jsme probrali

- **Jak používat OCR** v Javě s `OcrEngine` od Aspose.  
- Povolení **paralelního zpracování** pro zrychlení **provádění OCR na PDF** a **extrahování textu z TIFF**.  
- Úprava počtu vláken pro optimální výkon.  
- Řešení okrajových případů, jako jsou velké PDF, více‑stránkové TIFF a nastavení jazyků.  
- Rozšíření jednosouborové ukázky na dávkový procesor pro reálné nasazení.

---

## Další kroky

Nyní, když ovládáte základy, můžete prozkoumat související témata:

- **Extrahovat text z obrázku v Javě** z rukopisných poznámek (povolte `setHandwritingRecognition(true)`).  
- Integrace OCR výstupu s Apache Tika pro extrakci metadat.  
- Ukládání výsledků do Elasticsearch pro prohledávatelné archivy dokumentů.  
- Použití Aspose OCR s dalšími jazyky, jako je Python nebo .NET — principy zůstávají stejné.

Nebojte se experimentovat s různými limity vláken, formáty obrázků a jazykovými balíčky. Čím více si s tím pohráváte, tím lépe pochopíte kompromisy mezi rychlostí a přesností.

---

### Šťastné programování!

Pokud narazíte na problémy nebo máte nápady na další optimalizace, zanechte komentář níže. Rád se zapojím do diskuze o OCR tricích — bez námahy, jen kód.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}