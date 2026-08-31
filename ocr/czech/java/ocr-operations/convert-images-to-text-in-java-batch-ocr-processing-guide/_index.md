---
category: general
date: 2026-01-02
description: Převádějte obrázky na text v Javě pomocí Aspose OCR. Ovládněte dávkové
  zpracování OCR, načítejte obrázky ze složky a filtrujte soubory podle přípony.
draft: false
keywords:
- convert images to text
- batch ocr processing
- read images from folder
- extract text from png
- filter files by extension
language: cs
og_description: Převádějte obrázky na text rychle pomocí Javy. Tento návod zahrnuje
  dávkové zpracování OCR, čtení obrázků ze složky a filtrování souborů podle přípony.
og_title: Převod obrázků na text v Javě – Kompletní průvodce dávkovým OCR
tags:
- OCR
- Java
- Aspose
title: Převod obrázků na text v Javě – Průvodce dávkovým zpracováním OCR
url: /cs/java/ocr-operations/convert-images-to-text-in-java-batch-ocr-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Převod obrázků na text v Javě – Průvodce dávkovým zpracováním OCR

Už jste někdy potřebovali **převést obrázky na text**, ale nebyli jste si jisti, jak najednou zpracovat desítky souborů? Nejste v tom sami — vývojáři neustále bojují s extrahováním dat z PNG, JPG a dalších skenů. Dobrá zpráva? S Aspose OCR můžete během několika minut vytvořit pipeline pro dávkové zpracování OCR, číst obrázky ze složkových struktur a dokonce filtrovat soubory podle přípony, takže pracujete jen s tím, co je důležité.

V tomto tutoriálu vytvoříme samostatný Java program, který projde adresář, vybere každý `.png` nebo `.jpg`, pošle každý obrázek do Aspose OCR asynchronně a vytiskne extrahovaný text v původním pořadí. Na konci budete mít znovupoužitelný úryvek, který můžete vložit do libovolného projektu, který potřebuje **převést obrázky na text** ve velkém měřítku.

---

![Convert images to text example](https://example.com/convert-images-to-text.png "Screenshot of Java console output showing converted text from PNG files")

## Co vytvoříte

- Jednotný engine `AsposeOCR` sdílený mezi vlákny (efektivní a thread‑safe).  
- `ParallelRecognizer`, který spouští OCR úlohy paralelně, ideální pro **dávkové zpracování OCR**.  
- Logika, která **čte obrázky ze složky** pomocí `java.nio.file.Files`.  
- Jednoduché filtry pro **extrahování textu z PNG** souborů, přičemž stále podporují JPG.  
- Čisté ukončení interního thread poolu, aby nedocházelo k únikům zdrojů.

### Požadavky

- Java 17 (nebo jakákoli recentní LTS verze).  
- Maven nebo Gradle pro stažení knihovny Aspose OCR.  
- Složka plná PNG/JPG obrázků, které chcete zpracovat.  
- Základní znalost Java streamů — nic složitého není potřeba.

> **Pro tip:** Pokud ještě nemáte licenci, Aspose nabízí zdarma dočasný klíč, který můžete použít pro testování.

## Krok 1 – Nastavení projektu a přidání Aspose OCR

Nejprve vytvořte nový Maven projekt (nebo Gradle, jak chcete). Přidejte závislost Aspose OCR do `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

> **Proč je to důležité:** Deklarace závislosti dopředu zajišťuje, že kompilátor vidí `AsposeOCR`, `ParallelRecognizer` a související třídy. Také garantuje, že stejná verze je použita na všech strojích, což je klíčové pro reprodukovatelné **dávkové zpracování OCR**.

Až se sestavení dokončí, obnovte IDE a měli byste vidět balíčky Aspose pod `External Libraries`.

## Krok 2 – Převod obrázků na text – Inicializace OCR enginu

Potřebujeme jen **jednu** instanci OCR enginu pro celé spuštění. Sdílení mezi vlákny šetří paměť a zrychluje, protože engine načte jazykové balíčky jen jednou.

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

> **Vysvětlení:** `ParallelRecognizer` obaluje engine do thread‑poolu. Když odešlete mnoho souborů, každý dostane svůj pracovní thread, což umožňuje skutečný paralelismus na vícejádrových CPU.

## Krok 3 – Čtení obrázků ze složky – Procházení stromu adresářů

Nyní potřebujeme **číst obrázky ze složky** a shromáždit každý PNG nebo JPG. API `Files.walk` to udělá jedním řádkem, ale přidáme filtr pro **extrahování textu z PNG** jen když je to potřeba.

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

> **Proč zde filtrujeme:** Použití `filter` nám umožní **filtrovat soubory podle přípony** brzy, což později snižuje zbytečný I/O. Také to udržuje kód čitelný — není potřeba složité regexy.

## Krok 4 – Dávkové zpracování OCR – Odeslání úloh asynchronně

S připraveným seznamem souborů posíláme každou cestu do `ParallelRecognizer`. Metoda `recognizeAsync` vrací `Future<OcrResult>`, který uložíme pro pozdější získání.

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

> **Co se děje pod kapotou?** Každé volání zařadí úlohu do interního executor service rozpoznávače. Úlohy běží paralelně, takže složka se 100 obrázky může být zpracována během zlomku času, který by zabral jednovláknový cyklus.

## Krok 5 – Získání výsledků v původním pořadí – Zachování sekvence souborů

Protože jsme futures uložili ve stejném pořadí jako `imagePaths`, můžeme jednoduše projít seznam a zavolat `get()`. Volání blokuje jen do dokončení konkrétního obrázku, čímž zachová pořadí bez dalšího sledování.

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

**Ukázkový výstup v konzoli** (zkrácený pro stručnost):

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

> **Řešení okrajových případů:** Pokud konkrétní obrázek vyhodí výjimku (poškozený soubor, nepodporovaný formát), zachytíme ji a pokračujeme ve zpracování zbytku — nezbytný zvyk pro spolehlivé **dávkové OCR pipeline**.

## Krok 6 – Úklid – Ukončení rozpoznávače

Nikdy nezapomeňte ukončit interní thread pool; jinak se může JVM po ukončení zaseknout.

```java
// Step 6: Shut down the recognizer to clean up its internal thread pool
parallelRecognizer.shutdown();
```

To je vše! Program nyní projde libovolný adresář, filtruje PNG/JPG soubory, spustí OCR paralelně a vytiskne výsledky.

## Kompletní funkční příklad

Níže je kompletní, připravená Java třída ke zkopírování a vložení. Nahraďte `"YOUR_DIRECTORY"` cestou k vaší složce s obrázky a spusťte ji z IDE nebo z příkazové řádky.

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

Spusťte třídu, sledujte, jak se konzole zaplní extrahovanými řetězci, a oslavte fakt, že jste právě **převáděli obrázky na text** bez psaní jediného smyčky, která blokuje I/O.

## Často kladené otázky (FAQ)

**Q: Mohu zpracovávat i PDF nebo TIFF?**  
A: Rozhodně. Aspose OCR podporuje mnoho formátů — stačí přidat příslušné přípony souborů do filtru v kroku 2.

**Q: Co když potřebuji jiný jazyk, například španělštinu?**  
A: Změňte `RecognitionLanguage.ENGLISH` na `RecognitionLanguage.SPANISH`. Ujistěte se, že je jazykový balíček nainstalován (Aspose zahrnuje většinu hlavních jazyků již v balíčku).

**Q: Moje složka obsahuje podsložky — budou skenovány?**  
A: Ano. `Files.walk` prochází celý strom rekurzivně, takže každý vnořený PNG/J

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}