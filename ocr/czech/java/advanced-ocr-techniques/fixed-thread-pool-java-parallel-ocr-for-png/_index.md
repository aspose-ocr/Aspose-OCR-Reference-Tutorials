---
category: general
date: 2026-02-17
description: Naučte se, jak v Javě použít pevný pool vláken k extrahování textu z
  PNG obrázků s paralelním zpracováním OCR a správně ukončit službu Executor.
draft: false
keywords:
- fixed thread pool java
- extract text from png
- parallel ocr processing
- convert scanned pages text
- shut down executor service
language: cs
og_description: Objevte, jak může pevný thread pool v Javě paralelně extrahovat text
  z PNG obrázků, převádět text naskenovaných stránek a bezpečně ukončit ExecutorService.
og_title: Java pevný pool vláken – paralelní OCR pro PNG
tags:
- java
- ocr
- multithreading
- aspose
title: Pevný pool vláken Java – paralelní OCR pro PNG
url: /cs/java/advanced-ocr-techniques/fixed-thread-pool-java-parallel-ocr-for-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# pevný thread pool java – paralelní OCR pro PNG

Už jste se někdy zamýšleli, jak urychlit OCR na hromadě souborů PNG pomocí **fixed thread pool java**? V tomto tutoriálu si projdeme **extrahování textu z PNG** obrázků paralelně, **převod textu naskenovaných stránek** na editovatelné řetězce a bezpečné **shut down executor service**, jakmile je práce hotová.

Pokud jste někdy zírali na jednovláknovou smyčku, která se táhne minuty, znáte frustraci z čekání, až se každá stránka dokončí, než začne další. Dobrá zpráva? S několika řádky Javy a Aspose OCR můžete uvolnit sílu všech jader CPU, převést naskenované stránky na prohledávatelný text a udržet aplikaci responzivní.  

Níže najdete kompletní, připravený příklad, plus vysvětlení, proč je každá část důležitá, běžné úskalí a tipy, které můžete použít s libovolnou OCR knihovnou.

---

## Co budete potřebovat

- **Java 17** (nebo jakýkoli recentní JDK) – kód používá moderní syntaxi `var` střídmě, ale funguje i na starších verzích.  
- **Aspose.OCR for Java** knihovna – můžete ji získat z Maven Central nebo stáhnout trial z Aspose.  
- Sadu **PNG** souborů, které chcete zpracovat – např. naskenované účtenky, stránky knih nebo screenshoty.  
- Základní znalost Java concurrency – není povinná, ale užitečná.

To je vše. Žádné externí služby, žádný Docker, jen čistá Java a trochu multithreadingové magie.

## Krok 1: Přidání Aspose OCR závislosti a licence (volitelné)

Nejprve se ujistěte, že Aspose OCR JAR je ve vašem classpath. Pokud používáte Maven, přidejte:

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Pokud nemáte licenci, knihovna poběží v evaluačním režimu; kód funguje stejným způsobem. Pro načtení licence (doporučeno pro produkci) umístěte `Aspose.OCR.lic` do složky resources a použijte:

```java
// Load the Aspose OCR license (optional)
License license = new License();
license.setLicense("Aspose.OCR.lic");
```

> **Pro tip:** Uložte licenční soubor mimo verzovací systém, aby nedošlo k neúmyslnému zveřejnění.

## Krok 2: Vytvoření thread‑safe instance `OcrEngine`

Aspose OCR `OcrEngine` je thread‑safe, pokud znovu použijete stejnou instanci napříč úkoly. Vytvoření jednou šetří paměť a zabraňuje režii znovu‑inicializace engine pro každý obrázek.

```java
// One shared OcrEngine for all threads
OcrEngine ocrEngine = new OcrEngine();
```

Proč znovu použít? Představte si engine jako těžkopádného pracovníka, který načítá jazykové modely do paměti. Vytvoření nového engine pro každý obrázek by bylo jako najímat nového specialistu pro každou drobnou úlohu – nákladné a zbytečné.

## Krok 3: Nastavení Fixed Thread Pool v Javě

Nyní přichází hvězda celého představení: **fixed thread pool java**. Nastavíme jeho velikost podle počtu logických procesorů, aby každé jádro dostalo práci bez přetížení.

```java
// Determine available processors and create a fixed pool
int threadCount = Runtime.getRuntime().availableProcessors();
ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);
```

Použití *fixed* pool (namísto cached) vám poskytuje předvídatelné využití zdrojů a zabraňuje obávaným výkyvům „out‑of‑memory“, když najednou dorazí stovky obrázků.

## Krok 4: Seznam PNG souborů, které chcete zpracovat (extrahování textu z PNG)

Shromážděte cesty k obrázkům, které chcete OCR. Ve skutečném projektu můžete prohledávat adresář nebo číst z databáze; zde použijeme několik pevně zakódovaných příkladů.

```java
List<String> imageFiles = Arrays.asList(
        "YOUR_DIRECTORY/page1.png",
        "YOUR_DIRECTORY/page2.png",
        "YOUR_DIRECTORY/page3.png"
);
```

> **Poznámka:** Přípona souboru **png** je důležitá, protože Aspose OCR automaticky detekuje formát, ale můžete také použít JPEG nebo TIFF.

## Krok 5: Odeslání OCR úkolů – paralelní OCR zpracování

Každý obrázek se stane callable, který vrací rozpoznaný text. Protože `OcrEngine` je sdílený, stačí do úkolu předat cestu k souboru.

```java
List<Future<String>> ocrFutures = new ArrayList<>();

for (String imagePath : imageFiles) {
    ocrFutures.add(threadPool.submit(() -> {
        // Prepare input for this image
        OcrInput input = new OcrInput();
        input.add(imagePath);

        // Perform OCR using the shared engine
        OcrResult result = ocrEngine.recognize(input);

        // Return the plain text
        return result.getText();
    }));
}
```

Proč to zabalit do `Future`? Umožní nám okamžitě spustit všechny úlohy a později sbírat výsledky v pořadí, v jakém byly odeslány – ideální pro zachování pořadí stránek při **convert scanned pages text** zpět do dokumentu.

## Krok 6: Získání výsledků a zobrazení (převod naskenovaných stránek na text)

Nyní čekáme, až každé `Future` dokončí, a vypíšeme výstup. Volání `get()` blokuje jen do dokončení konkrétní úlohy, ne celého poolu.

```java
for (Future<String> future : ocrFutures) {
    System.out.println("----");
    System.out.println(future.get()); // prints OCR result for one PNG
}
```

Typický výstup v konzoli vypadá takto:

```
----
The quick brown fox jumps over the lazy dog.
----
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----
Page 3 content goes here…
```

Pokud raději zapisujete výsledky do souborů, nahraďte `System.out.println` voláním `Files.writeString`.

## Krok 7: Čisté vypnutí Executor Service

Když jsou všechny úkoly dokončeny, je zásadní **shut down executor service**; jinak může JVM udržovat ne‑daemon vlákna aktivní, což brání elegantnímu ukončení.

```java
threadPool.shutdown();               // No new tasks accepted
if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
    threadPool.shutdownNow();        // Force shutdown after timeout
}
```

Vzor `awaitTermination` dává poolu šanci dokončit probíhající práci, než ho vynutíme. Ignorování tohoto kroku je častým zdrojem úniků paměti v dlouho běžících aplikacích.

## Kompletní funkční příklad

Spojením všeho dohromady zde máte kompletní program, který můžete zkopírovat do `ParallelBatchDemo.java` a spustit:

```java
import com.aspose.ocr.*;

import java.util.*;
import java.util.concurrent.*;

public class ParallelBatchDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license (optional)
        License license = new License();
        license.setLicense("Aspose.OCR.lic");

        // 2️⃣ Shared, thread‑safe OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Fixed thread pool java – one thread per core
        int threadCount = Runtime.getRuntime().availableProcessors();
        ExecutorService threadPool = Executors.newFixedThreadPool(threadCount);

        // 4️⃣ Files to process – extract text from png
        List<String> imageFiles = Arrays.asList(
                "YOUR_DIRECTORY/page1.png",
                "YOUR_DIRECTORY/page2.png",
                "YOUR_DIRECTORY/page3.png"
        );

        // 5️⃣ Submit tasks – parallel OCR processing
        List<Future<String>> ocrFutures = new ArrayList<>();
        for (String imagePath : imageFiles) {
            ocrFutures.add(threadPool.submit(() -> {
                OcrInput input = new OcrInput();
                input.add(imagePath);
                OcrResult result = ocrEngine.recognize(input);
                return result.getText();
            }));
        }

        // 6️⃣ Retrieve and print – convert scanned pages text
        for (Future<String> future : ocrFutures) {
            System.out.println("----");
            System.out.println(future.get());
        }

        // 7️⃣ Shut down executor service cleanly
        threadPool.shutdown();
        if (!threadPool.awaitTermination(60, TimeUnit.SECONDS)) {
            threadPool.shutdownNow();

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}