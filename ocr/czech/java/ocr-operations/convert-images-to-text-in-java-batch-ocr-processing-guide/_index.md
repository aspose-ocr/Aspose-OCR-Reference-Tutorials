---
category: general
date: 2026-08-28
description: Naučte se, jak v Java pomocí Aspose OCR extrahovat text z png obrázků.
  Tento tutoriál pokrývá dávkové zpracování OCR, čtení obrázků ze složky a filtrování
  souborů podle přípony.
draft: false
keywords:
- extract text from png
- read images from folder
- filter files by extension
- how to batch ocr
- aspose ocr java tutorial
lastmod: 2026-08-28
og_description: Naučte se, jak v Java pomocí Aspose OCR extrahovat text z png obrázků.
  Tento tutoriál pokrývá dávkové zpracování OCR, čtení obrázků ze složky a filtrování
  souborů podle přípony.
og_image_alt: 'Developer guide: extract text from png images in Java using Aspose
  OCR'
og_title: Jak extrahovat text z png v Java – průvodce dávkovým OCR
schemas:
- author: Aspose
  dateModified: '2026-08-28'
  description: Learn how to extract text from png images in Java using Aspose OCR.
    This tutorial covers batch OCR processing, reading images from a folder, and filtering
    files by extension.
  headline: How to extract text from png in Java – batch OCR guide
  type: TechArticle
- questions:
  - answer: Absolutely. Aspose OCR supports 30+ formats—including PDF, TIFF, BMP,
      and GIF—so just add the desired extensions to the filter in the directory‑walk
      step.
    question: Can I process PDFs or TIFFs as well?
  - answer: Change `RecognitionLanguage.ENGLISH` to `RecognitionLanguage.SPANISH`
      (or any supported language). The language packs are bundled with the library,
      so no extra download is required.
    question: What if I need a language other than English, such as Spanish?
  - answer: Yes. `Files.walk` traverses the entire tree recursively, so every nested
      PNG/J
    question: My folder contains sub‑folders—will they be scanned?
  - answer: Enable streaming mode by calling `ocrEngine.setUseStreaming(true)`. This
      tells the engine to read the image in chunks, dramatically reducing peak memory
      usage.
    question: How do I handle extremely large images that exceed 200 MB?
  - answer: Yes. When constructing `ParallelRecognizer`, pass the desired maximum
      thread count as the second argument (e.g., `new ParallelRecognizer(ocrEngine,
      4)`).
    question: Is there a way to limit the number of concurrent OCR threads?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
title: Jak extrahovat text z png v Java – průvodce dávkovým OCR
url: /cs/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak extrahovat text z png v Javě – průvodce dávkovým OCR

Pokud jste někdy potřebovali **extrahovat text z png** souborů, ale nebyli jste si jisti, jak operaci rozšířit mimo několik obrázků, jste na správném místě. Mnoho vývojářů začíná s jedním voláním OCR na obrázek a rychle narazí na výkonnostní limity, když složka naroste na desítky nebo stovky souborů. S Aspose OCR pro Javu můžete vytvořit robustní dávkový OCR pipeline, který prochází adresář, filtruje jen typy obrázků, o které vám jde, spouští rozpoznávání paralelně a vrací výsledky ve stejném pořadí jako zdrojové soubory. Na konci tohoto průvodce budete mít připravený Java úryvek, který spolehlivě a efektivně zvládne **dávkové zpracování OCR**.

![Příklad převodu obrázků na text](https://example.com/convert-images-to-text.png "Snímek obrazovky výstupu Java konzole zobrazujícího převedený text z PNG souborů")

## Rychlé odpovědi
- **Jaká knihovna zpracovává OCR?** Aspose OCR pro Javu.
- **Mohu zpracovávat PNG a JPG společně?** Ano – ukázka filtruje oba typy souborů.
- **Je OCR engine thread‑safe?** Jedna sdílená instance `AsposeOCR` je bezpečná pro souběžné použití.
- **Potřebuji licenci pro testování?** Bezplatný dočasný klíč je k dispozici od Aspose.
- **Budou podadresáře skenovány automaticky?** `Files.walk` prochází celý strom rekurzivně.

## Co je extrahování textu z PNG?

`extract text from png` označuje proces aplikace optického rozpoznávání znaků (OCR) na soubory Portable Network Graphics, aby se viditelné znaky staly prohledávatelnými, editovatelnými řetězci. Engine Aspose OCR čte pixelová data, identifikuje tvary glyfů a vrací Unicode text jedním voláním metody.

## Proč použít Aspose OCR pro Javu?

Aspose OCR podporuje **30+ jazyků**, zpracovává až **500 obrázků za minutu** na standardním 8‑jádrovém serveru a může zvládnout soubory až **200 MB** bez načítání celého obrázku do paměti. Tyto kvantifikované schopnosti znamenají, že můžete spolehlivě spouštět velké dávkové úlohy na běžném hardwaru, aniž byste narazili na limity paměti.

## Předpoklady
- Java 17 (nebo jakákoli nedávná LTS verze).
- Maven nebo Gradle pro správu závislostí.
- Adresář obsahující PNG/JPG obrázky, které chcete zpracovat.
- Základní znalost Java streamů a balíčku `java.nio.file`.
- (Volitelné) Dočasný licenční klíč Aspose OCR pro hodnocení.

> **Pro tip:** Bezplatný dočasný klíč vyprší po 30 dnech, ale poskytuje plný přístup k API pro testování.

## Jak dávková OCR pipeline zachovává pořadí?

`Future<OcrResult>` představuje čekající výsledek OCR, který lze získat po dokončení zpracování. Pipeline zachovává původní pořadí souborů tím, že ukládá objekty `Future<OcrResult>` do seznamu, který odráží pořadí vstupní kolekce `Path`. Když později iterujete přes futures a voláte `get()`, každé volání blokuje jen pro svůj odpovídající obrázek, takže výstupní sekvence odpovídá vstupní sekvenci bez nutnosti dalšího řazení.

## Co je Aspose OCR pro Javu?

`AsposeOCR` je hlavní třída knihovny Aspose OCR, která zapouzdřuje všechny jazykové balíčky, nastavení rozpoznávání a interní nativní zdroje. Je navržena tak, aby byla vytvořena jednou během životnosti aplikace a bezpečně sdílena mezi více vlákny. Protože načítá jazyková data jen jednou, opětovné použití stejné instance snižuje režii inicializace a zvyšuje propustnost při dávkových operacích.

## Jak nastavit projekt a přidat Aspose OCR

Nejprve vytvořte Maven (nebo Gradle) projekt a přidejte závislost Aspose OCR do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>24.10</version>
</dependency>
```

> **Proč je to důležité:** Deklarace závislosti předem zajišťuje, že kompilátor vidí `AsposeOCR`, `ParallelRecognizer` a související třídy. Také garantuje, že stejná verze je použita na všech strojích, což je klíčové pro reprodukovatelné **dávkové zpracování OCR**.

Po dokončení sestavení obnovte IDE; nyní byste měli vidět balíčky Aspose pod **External Libraries**.

## Jak inicializovat OCR engine – sdílet jednu instanci

`AsposeOCR` je hlavní třída OCR engine poskytovaná knihovnou Aspose OCR. Potřebujeme jen **jednu** instanci OCR engine pro celý běh. Sdílení mezi vlákny šetří paměť a zrychluje věci, protože engine načítá jazykové balíčky jen jednou.

```java
AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");
```

`AsposeOCR` je thread‑safe, takže ji můžete bezpečně předat `ParallelRecognizer`, který bude spravovat pool pracovních vláken.

> **Vysvětlení:** `ParallelRecognizer` obaluje engine do thread‑poolu. Když odešlete mnoho souborů, každý dostane své vlastní pracovní vlákno, což umožňuje pravou paralelnost na vícejádrových CPU.

## Jak číst obrázky ze složky – projít strom adresářů

`Files.walk` je metoda Java NIO, která rekurzivně prochází strom souborů a vrací stream objektů `Path`. Nyní potřebujeme **číst obrázky ze složky** a shromáždit každý PNG nebo JPG. API `Files.walk` to umožňuje jedním řádkem, ale přidáme filtr, aby **extrahování textu z PNG** probíhalo jen podle potřeby.

```java
List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
    .filter(Files::isRegularFile)
    .filter(p -> {
        String lower = p.toString().toLowerCase();
        return lower.endsWith(".png") || lower.endsWith(".jpg");
    })
    .collect(Collectors.toList());
```

> **Proč filtrujeme zde:** Použití `filter` nám umožňuje **filtrovat soubory podle přípony** brzy, což snižuje zbytečný I/O později. Navíc kód zůstává čitelný – není potřeba složitých regulárních výrazů.

## Jak odeslat OCR úlohy asynchronně

`recognizeAsync` odešle obrázek do OCR engine pro asynchronní zpracování a vrátí `Future<OcrResult>` představující čekající výsledek. S připraveným seznamem souborů posuneme každou cestu do `ParallelRecognizer`. Metoda `recognizeAsync` vrací `Future<OcrResult>`, který uložíme pro pozdější získání.

```java
ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine, Runtime.getRuntime().availableProcessors());
List<Future<OcrResult>> futures = new ArrayList<>();

for (Path imagePath : imagePaths) {
    futures.add(recognizer.recognizeAsync(imagePath));
}
```

> **Co se děje pod kapotou?** Každé volání zařadí úlohu do interního executor service recognizeru. Úlohy běží paralelně, takže složka se 100 obrázky může být zpracována během zlomku času, který by zabral jednovláknový cyklus.

## Jak získat výsledky při zachování pořadí souborů

`Future<OcrResult>` drží výsledek asynchronní OCR úlohy a poskytuje metodu `get()` pro získání rozpoznaného textu. Protože jsme futures uložili ve stejném pořadí jako `imagePaths`, můžeme jednoduše iterovat přes seznam a volat `get()`. Volání blokuje jen do dokončení konkrétního obrázku, čímž se zachovává pořadí bez dalšího vedení.

```java
for (int i = 0; i < futures.size(); i++) {
    try {
        OcrResult result = futures.get(i).get();
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println("Text: " + result.getText());
    } catch (Exception e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

**Ukázka výstupu v konzoli** (zkráceno pro stručnost):

```
File: invoice1.png
Text: Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...
```

> **Zvládání okrajových případů:** Pokud konkrétní obrázek vyvolá výjimku (poškozený soubor, nepodporovaný formát), zachytíme ji a pokračujeme v zpracování ostatních – nezbytný zvyk pro spolehlivé **dávkové OCR pipeline**.

## Jak uvolnit prostředky – vypnout recognizer

`ParallelRecognizer.shutdown()` zastaví interní thread pool, čímž zajistí, že všechny OCR úlohy dokončí před ukončením aplikace. Nikdy nezapomeňte vypnout interní thread pool; jinak může JVM po ukončení viset.

```java
recognizer.shutdown();
```

A to je vše! Program nyní prochází libovolný adresář, filtruje PNG/JPG soubory, spouští OCR paralelně a vypisuje výsledky v původním pořadí.

---

## Kompletní funkční příklad (kopíruj‑a‑vložit)

Níže je kompletní, připravená ke spuštění Java třída. Nahraďte `"YOUR_DIRECTORY"` cestou k vaší složce s obrázky a spusťte ji z IDE nebo z příkazové řádky.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.*;

public class BatchOcrDemo {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine (single shared instance)
        AsposeOCR ocrEngine = new AsposeOCR("YOUR_LICENSE_KEY");

        // Create a parallel recognizer that uses a thread pool
        ParallelRecognizer recognizer = new ParallelRecognizer(ocrEngine,
                Runtime.getRuntime().availableProcessors());

        // Walk the directory and collect PNG/JPG files
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(Files::isRegularFile)
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        // Submit OCR jobs asynchronously
        List<Future<OcrResult>> futures = new ArrayList<>();
        for (Path imagePath : imagePaths) {
            futures.add(recognizer.recognizeAsync(imagePath));
        }

        // Retrieve results in the original order
        for (int i = 0; i < futures.size(); i++) {
            try {
                OcrResult result = futures.get(i).get();
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println("Text: " + result.getText());
            } catch (Exception e) {
                System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Clean up the recognizer's thread pool
        recognizer.shutdown();
    }
}
```

Spusťte třídu, sledujte, jak se konzole zaplní extrahovanými řetězci, a oslavte fakt, že jste právě **převáděli obrázky na text** bez psaní jediného smyčkového kódu, který by blokoval I/O.

---

## Často kladené otázky (FAQ)

**Q: Mohu zpracovávat také PDF nebo TIFF?**  
A: Rozhodně. Aspose OCR podporuje 30+ formátů – včetně PDF, TIFF, BMP a GIF – takže stačí přidat požadované přípony do filtru v kroku procházení adresáře.

**Q: Co když potřebuji jazyk jiný než angličtinu, například španělštinu?**  
A: Změňte `RecognitionLanguage.ENGLISH` na `RecognitionLanguage.SPANISH` (nebo jakýkoli podporovaný jazyk). Jazykové balíčky jsou součástí knihovny, takže není nutné nic dalšího stahovat.

**Q: Můj adresář obsahuje podadresáře—budou skenovány?**  
A: Ano. `Files.walk` prochází celý strom rekurzivně, takže každý vnořený PNG/J

**Q: Jak zacházet s extrémně velkými obrázky, které přesahují 200 MB?**  
A: Aktivujte režim streamování voláním `ocrEngine.setUseStreaming(true)`. Tím engine čte obrázek po částech, což dramaticky snižuje špičkovou spotřebu paměti.

**Q: Existuje způsob, jak omezit počet souběžných OCR vláken?**  
A: Ano. Při vytváření `ParallelRecognizer` předáte požadovaný maximální počet vláken jako druhý argument (např. `new ParallelRecognizer(ocrEngine, 4)`).

---

## Poslední aktualizace:
**2026-08-28**  
**Testováno s:** Aspose OCR pro Javu 24.10  
**Autor:** Aspose  

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

// ...

// Step 2: Create a single OCR engine instance and a parallel recognizer that uses it
AsposeOCR ocrEngine = new AsposeOCR();               // Loads language data internally
ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);
```

```java
import java.nio.file.*;
import java.util.*;
import java.util.stream.Collectors;

// ...

// Step 3: Find all PNG and JPG images in the target directory
Path imagesRoot = Paths.get("YOUR_DIRECTORY"); // <-- replace with your path
List<Path> imagePaths = Files.walk(imagesRoot)
        .filter(p -> {
            String name = p.toString().toLowerCase();
            return name.endsWith(".png") || name.endsWith(".jpg");
        })
        .collect(Collectors.toList());

if (imagePaths.isEmpty()) {
    System.out.println("No PNG or JPG files found in " + imagesRoot);
    return;
}
```

```java
import java.util.concurrent.*;

// ...

// Step 4: Submit each image for asynchronous recognition
List<Future<OcrResult>> recognitionFutures = new ArrayList<>();

for (Path image : imagePaths) {
    Future<OcrResult> future = parallelRecognizer.recognizeAsync(
            image.toString(),
            RecognitionLanguage.ENGLISH); // Change language if needed
    recognitionFutures.add(future);
}
```

```java
// Step 5: Retrieve and display the OCR results in the original order
for (int i = 0; i < recognitionFutures.size(); i++) {
    try {
        OcrResult result = recognitionFutures.get(i).get(); // blocks if not ready
        System.out.println("File: " + imagePaths.get(i).getFileName());
        System.out.println(result.getText()); // The extracted text
        System.out.println("-----");
    } catch (InterruptedException | ExecutionException e) {
        System.err.println("Failed to process " + imagePaths.get(i) + ": " + e.getMessage());
    }
}
```

```
File: invoice_001.png
Invoice #001
Date: 2024‑03‑15
Total: $1,250.00
-----
File: receipt_202403.jpg
Receipt
Item A - $45.00
Item B - $30.00
Grand Total: $75.00
-----
```

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.ParallelRecognizer;
import com.aspose.ocr.OcrResult;
import com.aspose.ocr.RecognitionLanguage;

import java.nio.file.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.stream.Collectors;

public class BatchParallelExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create a single OCR engine instance and a parallel recognizer that uses it
        AsposeOCR ocrEngine = new AsposeOCR();
        ParallelRecognizer parallelRecognizer = new ParallelRecognizer(ocrEngine);

        // Step 2: Find all PNG and JPG images in the target directory
        List<Path> imagePaths = Files.walk(Paths.get("YOUR_DIRECTORY"))
                .filter(p -> {
                    String lower = p.toString().toLowerCase();
                    return lower.endsWith(".png") || lower.endsWith(".jpg");
                })
                .collect(Collectors.toList());

        if (imagePaths.isEmpty()) {
            System.out.println("No images found – nothing to convert.");
            parallelRecognizer.shutdown();
            return;
        }

        // Step 3: Submit each image for asynchronous recognition
        List<Future<OcrResult>> recognitionFutures = new ArrayList<>();
        for (Path image : imagePaths) {
            recognitionFutures.add(
                    parallelRecognizer.recognizeAsync(
                            image.toString(),
                            RecognitionLanguage.ENGLISH));
        }

        // Step 4: Retrieve and display the OCR results in the original order
        for (int i = 0; i < recognitionFutures.size(); i++) {
            try {
                OcrResult result = recognitionFutures.get(i).get(); // blocks until processed
                System.out.println("File: " + imagePaths.get(i).getFileName());
                System.out.println(result.getText());
                System.out.println("-----");
            } catch (InterruptedException | ExecutionException e) {
                System.err.println("Error processing " + imagePaths.get(i) + ": " + e.getMessage());
            }
        }

        // Step 5: Shut down the recognizer to clean up its internal thread pool
        parallelRecognizer.shutdown();
    }
}
```

## Související tutoriály

- [Převod obrázků na text v Java dávkovém OCR průvodci](/ocr/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/)
- [Čtení textu z obrázku v Javě – kompletní Aspose OCR průvodce](/ocr/java/ocr-basics/read-text-from-image-in-java-complete-aspose-ocr-guide/)
- [Extrahování textu z obrázků pomocí Aspose.OCR – povolené znaky](/ocr/java/advanced-ocr-techniques/specify-allowed-characters/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}