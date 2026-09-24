---
category: general
date: 2026-02-14
description: 'Hromadné OCR obrázků snadno: naučte se, jak extrahovat text z PNG souborů
  pomocí Aspose OCR s paralelním zpracováním v Javě.'
draft: false
keywords:
- batch image OCR
- extract text from png
- parallel OCR Java
- Aspose OCR async
- OCR batch processing
language: cs
og_description: Tutorial pro dávkové OCR obrázků, který ukazuje, jak extrahovat text
  z PNG souborů pomocí asynchronního API Aspose OCR v Javě.
og_title: Dávkové OCR obrázků v Javě – Rychlé získávání textu z PNG
tags:
- Java
- OCR
- Aspose
- Image Processing
title: Dávkový OCR obrázků v Javě – Rychle extrahujte text z PNG souborů
url: /cs/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hromadné OCR obrázků v Javě – Rychlé získání textu z PNG souborů

Už jste někdy potřebovali spustit **hromadné OCR obrázků** na složku PNG skenů, ale obávali jste se rychlosti? Nejste v tom sami. V mnoha reálných projektech—digitalizace faktur, archivace naskenovaných knih nebo zpracování účtenek—vývojáři musí **extrahovat text z PNG** obrázků rychle a spolehlivě.  

Dobrá zpráva? S asynchronním API Aspose OCR můžete vytvořit paralelní OCR pipeline během několika řádků Javy. V tomto průvodci projdeme kompletní, spustitelný řešení, vysvětlíme, proč je každá část důležitá, a ukážeme, jak ověřit výsledky. Na konci budete mít samostatný program, který zpracuje celou dávku PNG souborů paralelně a poskytne čistý, pravopisně opravený textový výstup.

## Co se naučíte

- Jak vypsat PNG soubory pro hromadné zpracování  
- Konfigurace Aspose `OcrEngine` pro anglický jazyk a opravu pravopisu  
- Spouštění OCR asynchronně pomocí `processAsync` a zpracování výsledku `Future`  
- Čtení a zobrazování rozpoznaného textu pro každý obrázek  
- Tipy pro škálování, zpracování chyb a ladění výkonu  

### Požadavky

- Java 8 nebo novější nainstalovaná (kód používá standardní balíček `java.util.concurrent`)  
- Licence Aspose OCR pro Java nebo bezplatná zkušební verze (ke stažení na webu Aspose)  
- Složka obsahující několik PNG snímků obrazovky nebo naskenovaných stránek, které chcete otestovat  

Teď se ponořme.

## Krok 1 – Shromážděte PNG soubory pro hromadné zpracování

Než OCR engine může něco udělat, musí vědět, které obrázky má zpracovat. Nejjednodušší způsob je vytvořit `List<String>` s absolutními nebo relativními cestami k souborům.

```java
// Step 1: Prepare a list of PNG files you want to run OCR on
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png",
        "YOUR_DIRECTORY/page4.png");
```

**Proč je to důležité:**  
Vytvoření seznamu předem umožní enginu naplánovat každý soubor nezávisle, což je základ pravého hromadného zpracování. Pokud později potřebujete dynamicky prohledávat adresář, stačí nahradit statické `Arrays.asList` streamem `Files.walk`.

## Krok 2 – Inicializujte a vyladěte Aspose OCR Engine

Aspose `OcrEngine` je vysoce konfigurovatelný. Zde nastavíme jazyk na angličtinu a zapneme opravu pravopisu — dvě možnosti, které dramaticky zlepšují kvalitu extrahovaného textu, zejména z hlučných PNG skenů.

```java
// Step 2: Create and configure the OCR engine
OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getEngineOptions()
         .setLanguage(OcrLanguage.ENGLISH)          // English language model
         .setSpellCorrectionEnabled(true);          // Enable spell‑checking
```

**Proč tato nastavení:**  
- **Výběr jazyka** říká enginu, jakou znakovou sadu a slovník použít, čímž snižuje falešná rozpoznání.  
- **Oprava pravopisu** zachytí běžné chyby OCR (např. „1“ vs „l“) aniž byste museli výstup následně zpracovávat.

> **Tip:** Pokud vaše obrázky obsahují více jazyků, můžete předat seznam jako `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.FRENCH)`.

## Krok 3 – Spusťte asynchronní hromadné zpracování

Těžkou práci provádí `processAsync`. Vrací `Future<List<OcrResult>>`, což umožňuje hlavnímu vláknu pokračovat v dalších úkolech, zatímco OCR běží na pozadí.

```java
// Step 3: Start asynchronous processing of the image batch
Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

// (Optional) Do something useful while OCR runs, e.g., log progress, load UI, etc.
System.out.println("OCR started – you can perform other tasks now...");
```

**Proč asynchronně:**  
Spouštění OCR sekvenčně může být bolestivě pomalé — každý PNG může trvat sekundu nebo déle. Delegováním práce do thread poolu využijete více CPU jader a výrazně zkrátíte celkový čas běhu.

## Krok 4 – Získejte výsledky, až budou připravené

Až budete připraveni výstup použít, jednoduše zavolejte `get()` na `Future`. Tento volání blokuje jen do doby, než OCR skončí, a pak vám předá seznam objektů `OcrResult` ve stejném pořadí jako vstupní seznam.

```java
// Step 4: Wait for all results and retrieve them
List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion
```

**Zpracování časových limitů:**  
Pokud chcete předejít neomezenému blokování, použijte `ocrFuture.get(60, TimeUnit.SECONDS)` a zachyťte `TimeoutException`, abyste implementovali náhradní řešení.

## Krok 5 – Zobrazte rozpoznaný text pro každý PNG

Nyní, když máte výsledky, projděte je a vytiskněte extrahovaný text spolu s původním názvem souboru. Tady konečně **extrahujete text z PNG** souborů.

```java
// Step 5: Show the OCR output for each image
for (int i = 0; i < ocrResults.size(); i++) {
    System.out.println("File: " + imageFiles.get(i));
    System.out.println(ocrResults.get(i).getText());
    System.out.println("---");
}
```

**Příklad očekávaného výstupu**

```
File: YOUR_DIRECTORY/page1.png
Invoice #12345
Date: 2024‑03‑01
Total: $1,250.00
---
File: YOUR_DIRECTORY/page2.png
...
```

Pokud OCR engine nedokáže stránku rozpoznat, odpovídající `getText()` vrátí prázdný řetězec — v produkčním kódu je vždy dobré to zkontrolovat.

## Kompletní funkční příklad

Níže je kompletní, připravený k spuštění program, který spojuje všechny části dohromady. Zkopírujte jej do souboru pojmenovaného `ParallelOcrDemo.java`, nahraďte `YOUR_DIRECTORY` cestou k vaší PNG složce a spusťte `javac ParallelOcrDemo.java && java ParallelOcrDemo`.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Prepare a list of image files to be processed
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png",
                "YOUR_DIRECTORY/page4.png");

        // Step 2: Create and configure the OCR engine (set language and enable spell‑checking)
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getEngineOptions()
                 .setLanguage(OcrLanguage.ENGLISH)
                 .setSpellCorrectionEnabled(true);

        // Step 3: Start asynchronous processing of the image batch
        Future<List<OcrResult>> ocrFuture = ocrEngine.processAsync(imageFiles);

        // (Optional) Perform other work here while OCR runs in the background...
        System.out.println("OCR processing started in background...");

        // Step 4: Wait for all results and retrieve them
        List<OcrResult> ocrResults = ocrFuture.get(); // blocks until completion

        // Step 5: Display the recognized text for each file
        for (int i = 0; i < ocrResults.size(); i++) {
            System.out.println("File: " + imageFiles.get(i));
            System.out.println(ocrResults.get(i).getText());
            System.out.println("---");
        }
    }
}
```

### Spuštění ukázky

1. **Kompilace** – `javac -cp "aspose-ocr.jar" ParallelOcrDemo.java`  
2. **Spuštění** – `java -cp ".:aspose-ocr.jar" ParallelOcrDemo`  

Měli byste vidět název každého PNG souboru následovaný extrahovaným textem, odděleným pomlčkami.  

> **Poznámka:** Pokud narazíte na `LicenseException`, ujistěte se, že načtete svou Aspose licenci před vytvořením engine:

```java
License lic = new License();
lic.setLicense("Aspose.OCR.Java.lic");
```

## Škálování – Tipy pro reálné hromadné OCR

| Situace | Doporučení |
|-----------|----------------|
| **Stovky PNG** | Zvyšte velikost thread poolu pomocí `ocrEngine.setThreadPoolSize(8)` (nebo vyšší, odpovídající počtu CPU jader). |
| **Omezená paměť** | Zpracovávejte soubory v menších částech (např. dávky po 50) a po každé části uvolněte seznam `OcrResult`. |
| **Proměnlivá kvalita obrázků** | Povolte `setPreprocessingOptions` pro automatické otočení, vyrovnání nebo zvýšení kontrastu před rozpoznáním. |
| **Více jazyků** | Zavolejte `setLanguage(OcrLanguage.ENGLISH, OcrLanguage.SPANISH)` a případně nastavte vlastní slovník. |
| **Zpracování chyb** | Zabalte `ocrFuture.get()` do try‑catch bloku pro `ExecutionException`, abyste zaznamenali neúspěšné soubory, aniž byste přerušili celou dávku. |

## Často kladené otázky

**Q: Funguje to i s JPEG nebo TIFF soubory?**  
A: Rozhodně. Metoda `processAsync` přijímá jakýkoli formát podporovaný Aspose OCR (PNG, JPEG, TIFF, BMP, atd.). Stačí změnit přípony souborů ve vašem seznamu.

**Q: Co když potřebuji zachovat rozložení (tabulky, sloupce)?**  
A: Aspose OCR poskytuje metodu `getLayoutResult()`, která vrací poziční data. Tabulky můžete rekonstruovat analýzou ohraničujících rámečků každého slova.

**Q: Můžu to spustit na serverless platformě?**  
A: Ano — stačí zabalit JAR s knihovnou Aspose a nasadit na AWS Lambda, Azure Functions nebo Google Cloud Functions. Nezapomeňte nastavit dostatečnou paměť funkce, aby zvládla OCR thread pool.

## Závěr

Nyní máte kompletní, samostatné **hromadné OCR obrázků** řešení, které efektivně **extrahuje text z PNG** souborů pomocí asynchronního API Aspose OCR v Javě. Tutoriál pokryl vše od přípravy seznamu souborů po konfiguraci jazyka a opravy pravopisu, spuštění paralelního zpracování, zpracování výsledků a škálování pipeline pro produkční zatížení.

Jste připraveni na další krok? Zkuste přepnout jazyk na francouzštinu, experimentujte s vlastními slovníky nebo integrujte výstup do vyhledávatelného indexu ElasticSearch. Možnosti jsou neomezené, když spojíte rychlé hromadné OCR s moderní Java konkurencí.

Šťastné programování a ať je vaše extrakce textu rychlá a přesná! 

![Diagram ukazující paralelní OCR pracovníky zpracovávající více PNG souborů](/images/batch-ocr-diagram.png){: .center alt="Diagram zpracování hromadného OCR obrázků"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}