---
category: general
date: 2026-02-19
description: Extrahujte text z obrázku pomocí Java OCR. Naučte se příklad Java OCR,
  který načte obrázek pro OCR a extrahuje text z fakturačních souborů během několika
  kroků.
draft: false
keywords:
- extract text from image
- java ocr example
- load image for ocr
- extract text from invoice
language: cs
og_description: Extrahujte text z obrázku pomocí Java OCR. Tento průvodce ukazuje,
  jak načíst obrázek pro OCR a získat text z faktur pomocí jednoduchého příkladu Java
  OCR.
og_title: Extrahovat text z obrázku v Javě – kompletní příklad OCR
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Extrahovat text z obrázku v Javě – Kompletní příklad OCR
url: /cs/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z obrázku v Javě – kompletní OCR příklad

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nebyli jste si jisti, kterou knihovnu zvolit? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku při automatizaci zpracování faktur nebo tvorbě prohledávatelných archivů. Dobrá zpráva? Několika řádky Javy můžete načíst obrázek pro OCR, definovat oblast zájmu a získat přesně ten text, který potřebujete.  

V tomto tutoriálu projdeme **java ocr example**, který přesně ukazuje, jak **load image for OCR**, nastavit ROI a **extract text from invoice** soubory pomocí Aspose.OCR. Na konci budete mít spustitelný program, který můžete vložit do libovolného Java projektu.

## Co se naučíte

- Jak vytvořit instanci `OcrEngine` a proč je důležitá.
- Správný způsob **load image for OCR** pomocí Aspose `ImageStream`.
- Nastavení **region of interest (ROI)**, aby se zpracovávala pouze část obrázku obsahující částku faktury.
- Extrahování rozpoznaného textu a jeho výpis do konzole.
- Běžné úskalí (např. špatné souřadnice obdélníku) a rychlé opravy.

**Požadavky**

- Java 8 nebo novější nainstalována.
- Maven nebo Gradle pro stažení knihovny Aspose.OCR (`com.aspose:aspose-ocr`).
- Ukázkový obrázek faktury (`invoice.png`) umístěný v známém adresáři.

Máte vše připravené? Skvělé — ponořme se do toho.

![Extract text from image using Java OCR](/images/extract-text-from-image-java.png "extract text from image example")

## Extrahovat text z obrázku – krok za krokem Java OCR příklad

Níže je celý zdrojový kód. Klidně jej zkopírujte a vložte do `RoiOcrExample.java` a spusťte přímo.

```java
import com.aspose.ocr.*;

public class RoiOcrExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance.
        // The engine holds all configuration and performs the heavy lifting.
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image.
        // You can point to any PNG, JPG, or TIFF file. Here we use a sample invoice.
        String imagePath = "YOUR_DIRECTORY/invoice.png";
        ocrEngine.setImage(ImageStream.fromFile(imagePath));

        // Step 3: Define the region of interest (ROI) you want to recognize.
        // x = 120, y = 340, width = 500, height = 120 – tweak these values for your own layout.
        Rectangle regionOfInterest = new Rectangle(120, 340, 500, 120);
        ocrEngine.setRegionOfInterest(regionOfInterest);

        // Step 4: Perform OCR on the specified ROI and retrieve the text.
        // recognize() returns an OcrResult object; getText() extracts the plain string.
        String extractedText = ocrEngine.recognize().getText();

        // Step 5: Output the recognized text.
        System.out.println("ROI text: " + extractedText);
    }
}
```

### Proč je každý krok důležitý

1. **Creating the OCR engine** – bez enginu neexistuje kontext pro zpracování obrázku. Objekt vám také umožní později doladit jazykové balíčky, pokud potřebujete podporu více jazyků.  
2. **Loading the image** – `ImageStream.fromFile` abstrahuje formát souboru a zajišťuje, že engine správně načte bajty. Pokud to vynecháte, dostanete `NullPointerException`.  
3. **Setting the ROI** – zpracování celé stránky může být neefektivní. Zúžením obdélníku na oblast celkové částky faktury urychlíte rozpoznávání a snížíte šum.  
4. **Calling `recognize()`** – zde se děje magie. Metoda spustí OCR algoritmus nad ROI a vytvoří objekt výsledku.  
5. **Printing the output** – ve skutečných projektech byste pravděpodobně text uložili do databáze, ale `System.out.println` je ideální pro rychlou ukázku.

## Načíst obrázek pro OCR

Pokud se ptáte, zda cesta musí být absolutní nebo relativní, odpověď je, že obojí funguje — jen se ujistěte, že Java proces může soubor přečíst. Ve Windows je třeba zpětná lomítka escapovat (`C:\\images\\invoice.png`) nebo můžete použít lomítka (`C:/images/invoice.png`).  

**Tip:** Pokud zpracováváte mnoho faktur ve smyčce, znovu použijte stejnou instanci `OcrEngine`; ukládá interní zdroje do cache a zvyšuje propustnost.

## Definovat oblast zájmu (ROI)

Výběr správného obdélníku může být trochu pokus‑a‑omyl. Praktický způsob, jak najít souřadnice, je otevřít obrázek v libovolném grafickém editoru (např. GIMP nebo Paint.NET) a najíždět myší na oblast — v stavovém řádku uvidíte hodnoty X/Y.  

Edge case: některé faktury mají proměnlivé rozvržení. V takovém případě můžete provést rychlý předběžný sken celého obrázku, najít klíčová slova jako „Total:“ pomocí regexu a poté dynamicky upravit ROI.

## Proveďte OCR a získejte text

Volání `recognize()` je synchronní — váš vlákno blokuje, dokud engine nedokončí. Pro velké dávky můžete spustit thread pool a zpracovávat obrázky paralelně. Jen si pamatujte, že každé vlákno potřebuje vlastní instanci `OcrEngine`; nejsou thread‑safe.

## Spusťte a ověřte výstup

Kompilujte a spusťte:

```bash
javac -cp "path/to/aspose-ocr.jar" RoiOcrExample.java
java -cp ".:path/to/aspose-ocr.jar" RoiOcrExample
```

Měli byste vidět něco jako:

```
ROI text: $1,254.00
```

Pokud výstup vypadá poškozeně, zkontrolujte souřadnice ROI a ujistěte se, že kvalita obrázku je vysoká (300 dpi nebo více funguje nejlépe).  

### Běžné úskalí a jak je opravit

| Příznak | Pravděpodobná příčina | Oprava |
|---------|-----------------------|--------|
| Prázdný řetězec | ROI mimo hranice obrázku | Ověřte hodnoty obdélníku vůči rozměrům obrázku |
| Chybně rozpoznaná slova | Nízké rozlišení | Použijte zdroj s vyšším rozlišením nebo aplikujte předzpracování obrázku (např. binarizaci) |
| `java.lang.NoClassDefFoundError` | Chybějící Aspose JAR v classpath | Přidejte `aspose-ocr.jar` do `-cp` nebo použijte správu závislostí Maven/Gradle |

## Závěr

Nyní víte, jak **extract text from image** v Javě pomocí stručného **java ocr example**. Správným načtením obrázku, definováním zaměřené ROI a voláním `recognize()` můžete spolehlivě **extract text from invoice** soubory a předat tato data do následných systémů.

Co dál? Zkuste vyměnit ROI za různé pole (datum, jméno dodavatele), experimentujte s jazykovými balíčky pro vícejazyčné faktury nebo integrujte OCR krok do microservisu Spring Boot. Stejný vzor funguje pro účtenky, pasy nebo jakýkoli dokument, kde potřebujete přesné extrahování textu.

Máte-li otázky ohledně škálování tohoto řešení nebo zpracování špatných skenů, zanechte komentář níže — šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}