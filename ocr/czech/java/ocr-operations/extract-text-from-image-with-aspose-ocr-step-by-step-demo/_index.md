---
category: general
date: 2026-02-14
description: Extrahujte text z obrázku pomocí Aspose OCR. Naučte se, jak načíst obrázek
  pro OCR, přečíst text z obdélníku a během několika minut si projděte tento tutoriál
  Aspose OCR.
draft: false
keywords:
- extract text from image
- load image for ocr
- read text from rectangle
- aspose ocr tutorial
language: cs
og_description: Extrahujte text z obrázku okamžitě. Tento průvodce ukazuje, jak načíst
  obrázek pro OCR, přečíst text z obdélníku a dokončit tutoriál Aspose OCR.
og_title: Extrahování textu z obrázku pomocí Aspose OCR – rychlý průvodce
tags:
- Aspose
- OCR
- Java
title: Extrahování textu z obrázku pomocí Aspose OCR – krok za krokem ukázka
url: /cs/java/ocr-operations/extract-text-from-image-with-aspose-ocr-step-by-step-demo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku pomocí Aspose OCR – krok za krokem ukázka

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nevedeli jste, kde začít? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku, když poprvé řeší skenování účtenek nebo ověřování ID. Dobrá zpráva? S Aspose OCR můžete načíst obrázek, definovat přesnou oblast, kde se text nachází, a získat znaky během několika řádků.

V tomto **aspose ocr tutorial** vás provedeme vším, co potřebujete: načtením obrázku pro OCR, nastavením obdélníku, který řekne enginu, kde má hledat, a nakonec přečtením extrahovaného textu. Na konci budete mít spustitelný Java program, který vytiskne text ROI do konzole — žádná hádanka, jen jasné, fungující řešení.

## Co budete potřebovat

| Požadavek | Proč je důležitý |
|--------------|----------------|
| **Java JDK 8+** | Aspose OCR je distribuováno jako Java knihovna; jakýkoli moderní JDK postačí. |
| **Aspose.OCR for Java** (download from the Aspose website or add via Maven) | Poskytuje třídy `OcrEngine`, `ImageStream` a související. |
| **An image file** (e.g., `receipt.jpg`) that contains printable text | Ukážeme enginu obdélník uvnitř tohoto souboru. |
| **IDE or editor** (IntelliJ, Eclipse, VS Code…) | Pomůže vám rychle zkompilovat a spustit ukázku. |

Pokud používáte Maven, přidejte tuto závislost do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check Aspose for the latest version -->
</dependency>
```

> **Tip:** Číslo verze výše je aktuální k únoru 2026. Aktualizací na nejnovější vydání zajistíte opravy chyb a vylepšení výkonu.

## Krok 1 – Inicializace OCR enginu

Nejprve potřebujete instanci `OcrEngine`. Považujte ji za mozek, který bude analyzovat pixely.

```java
// Step 1: Create the OCR engine object
OcrEngine ocrEngine = new OcrEngine();
```

Proč to takto vytvořit? Aspose odděluje engine (který obsahuje konfiguraci) od dat obrázku, což vám dává flexibilitu znovu použít stejný engine pro více obrázků, pokud chcete.

## Krok 2 – Načtení obrázku pro OCR

Nyní skutečně **načteme obrázek pro OCR**. Pomocná metoda `ImageStream.fromFile` načte soubor do proudu, který Aspose rozumí.

```java
// Step 2: Load the target image (replace with your own path)
String imagePath = "YOUR_DIRECTORY/receipt.jpg";
ocrEngine.setImage(ImageStream.fromFile(imagePath));
```

Pokud soubor nelze najít, engine vyhodí výjimku, takže byste to v produkčním kódu mohli zabalit do bloku try‑catch. Pro tuto ukázku necháme výjimku propuknout — ukázka zůstane přehledná.

## Krok 3 – Definování obdélníku (Čtení textu z obdélníku)

Zde se část **čtení textu z obdélníku** ukáže v plné síle. Řeknete enginu přesně, kde má hledat, což urychlí zpracování a sníží falešně pozitivní výsledky.

```java
// Step 3: Create a rectangle that covers the area with the receipt total
// Parameters: x, y, width, height (all in pixels)
Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);
```

> **Proč obdélník?**  
> Většina dokumentů má předvídatelné rozvržení — např. účtenka, kde částka vždy stojí blízko spodní části. Zaměřením se na tento výřez OCR engine ignoruje nepodstatnou grafiku a zvyšuje přesnost.

**Hraniční případ:** Pokud obdélník přesahuje hranice obrázku, Aspose jej tiše ořízne, ale přijdete o data. Rychlá kontrola může tomu zabránit:

```java
if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
    regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
    throw new IllegalArgumentException("ROI exceeds image dimensions.");
}
```

## Krok 4 – Zpracování obrázku

Po nastavení všeho požádáme engine, aby udělal své kouzlo.

```java
// Step 4: Run OCR on the defined ROI
OcrResult ocrResult = ocrEngine.process();
```

Volání `process()` vrací objekt `OcrResult`, který obsahuje extrahovaný text, skóre důvěry a dokonce ohraničující rámečky pro každé slovo, pokud je budete potřebovat později.

## Krok 5 – Výstup extrahovaného textu

Nakonec výsledek vytiskněte. Ve skutečné aplikaci jej můžete uložit do databáze nebo předat jinému servisu, ale pro tuto ukázku stačí výstup do konzole.

```java
// Step 5: Display the recognized text
System.out.println("ROI text:");
System.out.println(ocrResult.getText());
```

**Očekávaný výstup** (předpokládáme, že obdélník zachytil celkovou částku na účtence):

```
ROI text:
$12.34
```

Pokud je ROI prázdná nebo je obrázek rozmazaný, uvidíte prázdný řetězec nebo zkreslené znaky. Upravit obdélník, zlepšit kvalitu obrázku nebo povolit předzpracování Aspose (např. `setAutoSkewCorrection(true)`).

## Kompletní funkční příklad

Níže je kompletní, připravený program. Zkopírujte jej do souboru pojmenovaného `RoiDemo.java`, upravte cestu k obrázku a spusťte `javac RoiDemo.java && java RoiDemo`.

```java
import com.aspose.ocr.*;
import java.awt.Rectangle;

/**
 * Demo: Extract text from a specific rectangle (ROI) in an image using Aspose OCR.
 * Adjust the rectangle coordinates to match the area you want to read.
 */
public class RoiDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image for OCR
        // Replace YOUR_DIRECTORY with the actual folder containing receipt.jpg
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.jpg"));

        // Step 3: Define the region of interest where text is expected
        // (x, y, width, height) in pixels
        Rectangle regionOfInterest = new Rectangle(120, 350, 600, 200);
        ocrEngine.getEngineOptions().setRegionOfInterest(regionOfInterest);

        // Optional sanity check – ensures ROI fits inside the image
        if (regionOfInterest.x + regionOfInterest.width > ocrEngine.getImage().getWidth() ||
            regionOfInterest.y + regionOfInterest.height > ocrEngine.getImage().getHeight()) {
            throw new IllegalArgumentException("ROI exceeds image dimensions.");
        }

        // Step 4: Perform OCR on the defined ROI
        OcrResult ocrResult = ocrEngine.process();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(ocrResult.getText());
    }
}
```

> **Ověření výsledku:** Po spuštění porovnejte výstup v konzoli se skutečným textem uvnitř obdélníku. Pokud se shodují, úspěšně jste **extrahovali text z obrázku** pomocí Aspose OCR.

## Časté otázky a tipy

### Co když potřebuji zpracovat více ROI ve stejném obrázku?
Vytvořte nový `Rectangle` pro každou oblast, znovu zavolejte `setRegionOfInterest` a spusťte `process()` znovu. Engine znovu použije stejná data obrázku, takže výkon zůstane rychlý.

### Jak Aspose zachází s různými jazyky nebo fonty?
Můžete přepnout jazykový model pomocí `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.English)`. Pro ne‑latinské skripty načtěte odpovídající jazykový balíček (k dispozici na stránce ke stažení Aspose).

### Podporuje knihovna vstupní PDF?
Ano — Aspose OCR může přijímat PDF proudy přímo. Stačí nahradit `ImageStream.fromFile` za `ImageStream.fromPdfFile("doc.pdf")` a případně zadat číslo stránky.

### Můžu zlepšit přesnost u nízkokvalitních skenů?
Povolte předzpracování:

```java
ocrEngine.getEngineOptions().setAutoSkewCorrection(true);
ocrEngine.getEngineOptions().setBinarizationMethod(BinarizationMethod.Otsu);
```

## Závěr

Právě jsme prošli kompletní **aspose ocr tutorial**, který ukazuje, jak **extrahovat text z obrázku**, **načíst obrázek pro OCR** a **číst text z obdélníku** pomocí Javy. Klíčové kroky jsou inicializace enginu, předání obrázku, definování oblasti zájmu, zpracování a nakonec vytištění výsledku.

Odtud můžete zkoumat:

* **Dávkové zpracování** – procházet složku s účtenkami a ukládat každou částku do databáze.  
* **Dynamické detekování ROI** – použít knihovny pro zpracování obrazu (OpenCV) k automatickému nalezení textových bloků.  
* **Post‑processing** – aplikovat regex nebo fuzzy matching k vyčištění OCR nedostatků.

Vyzkoušejte tyto nápady, upravte obdélník podle svých dokumentů a během chvilky budete mít robustní pipeline pro extrakci textu. Šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}