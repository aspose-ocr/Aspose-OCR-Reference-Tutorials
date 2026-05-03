---
category: general
date: 2026-05-03
description: Vytvořte pevný pool vláken v Javě pro rychlé získávání textu z obrázků.
  Naučte se spouštět OCR, převádět obrázek na text a zvyšovat výkon pomocí paralelního
  zpracování OCR.
draft: false
keywords:
- create fixed thread pool
- extract text from images
- how to run OCR
- convert image to text
- parallel OCR processing
language: cs
og_description: Vytvořte pevný pool vláken v Javě pro rychlé získávání textu z obrázků.
  Naučte se, jak spustit OCR, převést obrázek na text a zvýšit výkon pomocí paralelního
  zpracování OCR.
og_title: Vytvořte pevný pool vláken pro paralelní OCR v Javě
tags:
- Java
- OCR
- Multithreading
title: Vytvořte pevný pool vláken pro paralelní OCR v Javě
url: /cs/java/advanced-ocr-techniques/create-fixed-thread-pool-for-parallel-ocr-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření pevného thread poolu pro paralelní OCR v Javě

Už jste někdy potřebovali **create fixed thread pool** pro zrychlení OCR úloh, ale nebyli jste si jisti, kde začít? Nejste v tom sami. V mnoha projektech s velkým množstvím obrázků je úzkým místem jednovláknové volání OCR a řešení je překvapivě jednoduché: spustit pool pracovních vláken a nechat je zpracovávat soubory paralelně.  

V tomto tutoriálu se naučíte, jak **extract text from images** pomocí Aspose OCR, jak **run OCR** efektivně a jak **convert image to text** bez přetížení CPU. Na konci budete mít připravený Java program, který demonstruje **parallel OCR processing** na několika ukázkových obrázcích.

## Co vytvoříte

Sestavíme malou konzolovou aplikaci, která:

* Načte seznam cest k obrázkům (PNG, JPG, TIFF, BMP).
* **Creates a fixed thread pool** vytvořený podle počtu jader CPU.
* Spustí OCR úlohu pro každý obrázek.
* Shromáždí rozpoznaný text a vypíše jej do konzole.
* Čistě ukončí executor.

Žádné externí nástroje pro sestavení, žádné složité frameworky — jen čistá Java a knihovna Aspose OCR. Pokud máte Java 8+ a slušné IDE, jste připraveni.

## Požadavky

* **Java Development Kit (JDK) 8 or newer** – kód používá lambda výrazy, takže starší verze se nebudou kompilovat.
* **Aspose OCR for Java** – stáhněte JAR z webu Aspose nebo jej přidejte pomocí Maven (`com.aspose:aspose-ocr`).
* Složka s několika testovacími obrázky (kód odkazuje na `YOUR_DIRECTORY`).  
* Základní znalost Java concurrency (zbytek vysvětlíme).

> *Pro tip:* Pokud používáte Maven, přidejte závislost do svého `pom.xml` a nechte IDE spravovat classpath.  

## Krok 1: Přidejte potřebné importy

Nejprve přiveďte potřebné třídy do rozsahu. Není to jen boilerplate; každý import říká JVM, kde najít OCR engine, utility pro práci s obrázky a nástroje pro souběžnost, které nám umožňují **create fixed thread pool** instance.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;
```

* `com.aspose.ocr.*` – hlavní OCR API.  
* `java.util.*` – kolekce pro ukládání cest k obrázkům a výsledků.  
* `java.util.concurrent.*` – balíček pro souběžnost, který obsahuje `ExecutorService` a `Future`.

## Krok 2: Definujte obrázky ke zpracování

Dále uvedeme soubory, ze kterých chceme **extract text from images**. Použití `Arrays.asList` udržuje kód stručný a umožňuje nám vyměnit vlastní adresář, aniž bychom zasahovali do zbytku logiky.

```java
List<String> imagePaths = Arrays.asList(
        "YOUR_DIRECTORY/image1.png",
        "YOUR_DIRECTORY/image2.jpg",
        "YOUR_DIRECTORY/image3.tif",
        "YOUR_DIRECTORY/image4.bmp"
);
```

Klidně přidejte další položky; thread pool se automaticky přizpůsobí počtu jader CPU, které máte.

## Krok 3: **Create Fixed Thread Pool** odpovídající počtu jader CPU

Toto je jádro tutoriálu. Zeptáme se runtime, kolik jader je k dispozici, a požádáme továrnu `Executors`, aby nám poskytla pool přesně této velikosti. Proč pevný? Protože předvídatelný počet vláken zabraňuje obávanému „výbuchu vláken“, který může OS vyhladit o zdroje.

```java
int coreCount = Runtime.getRuntime().availableProcessors();
ExecutorService executor = Executors.newFixedThreadPool(coreCount);
```

* `availableProcessors()` vrací počet logických jader (včetně hyper‑threadů).  
* `newFixedThreadPool(coreCount)` zajišťuje, že nepřekročíme kapacitu CPU, což je nejbezpečnější způsob, jak **run OCR** paralelně.

## Krok 4: Odeslat OCR úlohu pro každý obrázek

Nyní převádíme každou cestu k souboru na callable, který **runs OCR**, rozpozná text a vrátí výsledek. Všimněte si, že v lambda výrazu vytváříme novou instanci `OcrEngine` — tím se vyhneme sdílení stavu enginu, které není thread‑safe.

```java
List<Future<String>> ocrResults = new ArrayList<>();
for (String path : imagePaths) {
    ocrResults.add(executor.submit(() -> {
        OcrEngine engine = new OcrEngine();          // fresh engine per task
        engine.setImage(ImageStream.fromFile(path));
        engine.getLanguage().setEnglish(true);
        return engine.recognize() ? engine.getText()
                                   : "Failed: " + path;
    }));
}
```

* Každé volání `submit` předá lambda výrazu poolu, který jej naplánuje na volné vlákno.  
* `Future<String>` objekty nám umožní později získat rozpoznaný text, přičemž zachovají pořadí, pokud jej potřebujete.

## Krok 5: Získat a zobrazit rozpoznaný text

Jakmile jsou všechny úlohy zařazeny do fronty, jednoduše iterujeme přes seznam `Future`, voláme `get()`, abychom blokovali, dokud každá OCR úloha nedokončí. Zde se ukazuje krok **convert image to text**: volání `engine.getText()` vrací surový řetězec.

```java
for (Future<String> result : ocrResults) {
    System.out.println("OCR result:\n" + result.get());
}
```

Typický výstup v konzoli vypadá takto:

```
OCR result:
Hello world!
OCR result:
Invoice #12345
Date: 2026‑04‑30
...
```

Pokud soubor selže (například je poškozený), uvidíte řádek začínající `Failed:` následovaný cestou — užitečné pro rychlé ladění.

## Krok 6: Vyčistit službu Executor

Nikdy nezapomeňte ukončit pool; jinak může JVM zůstat běžet, protože si myslí, že stále něco běží. Elegantní ukončení umožní dokončit všechny běžící úlohy před ukončením procesu.

```java
executor.shutdown();
```

Můžete také zavolat `awaitTermination`, pokud potřebujete vynutit časový limit, ale pro většinu nástrojů v příkazové řádce stačí jednoduché `shutdown()`.

## Kompletní funkční příklad

Níže je kompletní, připravený program. Zkopírujte jej do souboru pojmenovaného `ParallelOcrTutorial.java`, upravte cesty k obrázkům a spusťte `javac` + `java` jako obvykle.

```java
import com.aspose.ocr.*;
import java.util.*;
import java.util.concurrent.*;

public class ParallelOcrTutorial {
    public static void main(String[] args) throws Exception {
        // Step 2: Define the images to be processed
        List<String> imagePaths = Arrays.asList(
                "YOUR_DIRECTORY/image1.png",
                "YOUR_DIRECTORY/image2.jpg",
                "YOUR_DIRECTORY/image3.tif",
                "YOUR_DIRECTORY/image4.bmp"
        );

        // Step 3: Create a fixed‑size thread pool matching the CPU cores
        int coreCount = Runtime.getRuntime().availableProcessors();
        ExecutorService executor = Executors.newFixedThreadPool(coreCount);

        // Step 4: Submit an OCR task for each image
        List<Future<String>> ocrResults = new ArrayList<>();
        for (String path : imagePaths) {
            ocrResults.add(executor.submit(() -> {
                OcrEngine engine = new OcrEngine();          // fresh engine per task
                engine.setImage(ImageStream.fromFile(path));
                engine.getLanguage().setEnglish(true);
                return engine.recognize() ? engine.getText()
                                           : "Failed: " + path;
            }));
        }

        // Step 5: Retrieve and display the recognized text
        for (Future<String> result : ocrResults) {
            System.out.println("OCR result:\n" + result.get());
        }

        // Step 6: Clean up the executor service
        executor.shutdown();
    }
}
```

**Očekávaný výsledek:** textový obsah každého obrázku vytištěný do konzole ve stejném pořadí jako v seznamu `imagePaths`. Pokud se některý obrázek nepodaří zpracovat, uvidíte oznámení o selhání místo prázdného řádku.

## Časté otázky a okrajové případy

### Co když mám více obrázků než vláken?

Pevný thread pool automaticky zařadí přebytečné úlohy do fronty. Jakmile vlákno dokončí aktuální OCR úlohu, převezme další. Toto chování fronty je podstatou **parallel OCR processing** — získáte maximální propustnost bez přetížení CPU.

### Můžu změnit jazyk?

Určitě. Nahraďte `engine.getLanguage().setEnglish(true);` příslušným jazykovým příznakem, např. `setFrench(true)` nebo povolte více jazyků voláním několika setterů před `recognize()`.

### Jak zacházet s velmi velkými obrázky?

Velké soubory mohou spotřebovat hodně paměti na vlákno. Pokud zaznamenáte `OutOfMemoryError`, zvažte zmenšení obrázku před předáním enginu, nebo zvýšte velikost haldy pomocí `-Xmx`. Další přístup je použít **cached thread pool** (`

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}