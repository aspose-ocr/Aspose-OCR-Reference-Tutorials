---
category: general
date: 2026-06-06
description: Jak provést OCR v Javě – rychle extrahovat text z obrázku, převést obrázek
  na text a číst text z jpg pomocí jednoduchého příkladu kódu.
draft: false
keywords:
- how to perform OCR
- ocr in java
- extract text from image
- convert image to text
- read text from jpg
language: cs
og_description: jak provést OCR v Javě – naučte se, jak extrahovat text z obrázku,
  převést obrázek na text a číst text z jpg s připraveným příkladem k okamžitému spuštění.
og_title: Jak provést OCR v Javě – krok za krokem průvodce
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  headline: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  type: TechArticle
- description: how to perform OCR in Java – quickly extract text from image, convert
    image to text, and read text from jpg using a simple code example.
  name: How to Perform OCR in Java – Complete Guide to Extract Text from Images
  steps:
  - name: What You’ll Learn
    text: '- Install an OCR library (yes, **ocr in java** is easier than you think).
      - Create and configure an OCR engine instance. - Load a JPG (or any image) and
      set the language. - Process the image and **extract text from image** files.
      - Print the recognized string to the console.'
  - name: Expected Output
    text: 'If `input.jpg` contains the Mongolian phrase “Сайн байна уу?” the console
      will show:'
  - name: 'Pro Tip: Batch Processing'
    text: 'If you need to **extract text from image** files in bulk, wrap the core
      logic in a loop:'
  type: HowTo
tags:
- OCR
- Java
- Image Processing
title: Jak provést OCR v Javě – Kompletní průvodce extrakcí textu z obrázků
url: /cs/java/ocr-basics/how-to-perform-ocr-in-java-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět OCR v Javě – Kompletní průvodce extrahováním textu z obrázků

Už jste se někdy zamysleli nad tím, **jak provádět OCR** na obrázku, který jste pořízili telefonem? Nejste v tom sami. Ať už vytváříte aplikaci pro skenování účtenek, nebo jen potřebujete získat text ze skenovaného PDF, **jak provádět OCR** v Javě je dovednost, která se rychle vyplatí. V tomto tutoriálu projdeme praktickým příkladem, který **extrahuje text z obrázku** souborů, **převádí obrázek na text**, a dokonce vám ukáže, jak **číst text z jpg** pomocí několika řádků kódu.

> *Tip:* Stejný přístup funguje pro PNG, BMP nebo jakýkoli formát, který OCR engine podporuje—stačí vyměnit název souboru.

## Jak provádět OCR v Javě – Přehled

Optické rozpoznávání znaků (OCR) je technologie, která převádí obrázky písmen na skutečný, prohledávatelný text. V ekosystému Java existuje několik knihoven – Tesseract, Asprise a komerční SDK – všechny poskytují podobný workflow: načíst obrázek, říct enginu, jaký jazyk očekává, spustit rozpoznávání a získat výsledek. Níže použijeme generickou třídu `OcrEngine`, aby byl příklad přehledný, ale můžete ji nahradit libovolnou konkrétní implementací, která následuje stejný vzor.

### Co se naučíte

- Nainstalujte OCR knihovnu (ano, **ocr in java** je jednodušší, než si myslíte).
- Vytvořte a nakonfigurujte instanci OCR engine.
- Načtěte JPG (nebo jakýkoli obrázek) a nastavte jazyk.
- Zpracujte obrázek a **extrahujte text z obrázku** souborů.
- Vytiskněte rozpoznaný řetězec do konzole.

Na konci budete mít samostatný Java program, který můžete vložit do libovolného projektu a spustit okamžitě.

![příklad provádění OCR](ocr-example.png "ilustrace jak provádět OCR v Javě")

## Krok 1 – Instalace a import OCR knihovny (ocr in java)

Než napíšete jediný řádek Java, potřebujete knihovnu, která skutečně provede těžkou práci. Pokud používáte Maven, přidejte závislost takto (nahraďte `com.example.ocr` skutečným group ID vašeho zvoleného SDK):

```xml
<dependency>
    <groupId>com.example</groupId>
    <artifactId>ocr-sdk</artifactId>
    <version>1.4.2</version>
</dependency>
```

Pokud dáváte přednost Gradlu:

```gradle
implementation 'com.example:ocr-sdk:1.4.2'
```

Jakmile je JAR na vašem classpath, importujte třídy, které budete potřebovat:

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;
```

> **Proč je to důležité:** Importování správných tříd zabraňuje chybám „cannot find symbol“ a dělá vaše IDE spokojeným – nic není frustrujícíji než chybějící import, když se snažíte **převést obrázek na text**.

## Krok 2 – Vytvoření instance OCR engine (jak provádět OCR)

Nyní, když je knihovna připravena, spusťte engine. Představte si engine jako mozek, který se podívá na pixely a odhadne písmena.

```java
// Step 2: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Vytvoření engine je obvykle levné; většina SDK alokuje interní buffery líně, takže můžete bezpečně znovu použít stejnou instanci napříč mnoha obrázky, pokud zpracováváte dávku.

## Krok 3 – Načtení obrázku a nastavení jazyka (extrahovat text z obrázku)

Dalším krokem je poskytnout engine něco ke čtení. Zde načteme JPEG z disku a řekneme OCR engine, že text je v mongolštině (kód ISO 639‑2 „mon“). Můžete změnit cestu nebo kód jazyka podle vašeho použití.

```java
// Step 3: Load the image you want to recognize
ocrEngine.setImage(new OcrInputImage("YOUR_DIRECTORY/input.jpg"));

// Step 3b: Specify the language (e.g., English = "eng", Mongolian = "mon")
ocrEngine.getSettings().setLanguage("mon");
```

> **Poznámka:** Pokud nenastavíte jazyk, engine výchozí na angličtinu, což může výrazně snížit přesnost, když je text ve skutečnosti cyrilice nebo jiném skriptu. Vždy, když můžete, specifikujte správný jazyk.

## Krok 4 – Zpracování obrázku a získání výsledku (převést obrázek na text)

S obrázkem a jazykem na místě požádejte engine, aby udělal své kouzlo. Volání `process()` spustí OCR algoritmus a vrátí objekt `OcrResult` obsahující rozpoznaný řetězec a skóre důvěry.

```java
// Step 4: Process the image and obtain the recognition result
OcrResult ocrResult = ocrEngine.process();
```

Za scénou může engine provádět předzpracování – vyrovnání, binarizaci, redukci šumu – takže tyto kroky nemusíte psát sami. Proto jsou většina moderních OCR knihoven radostí pro úkoly **převést obrázek na text**.

## Krok 5 – Výstup extrahovaného textu (číst text z jpg)

Nakonec vytáhněte čistý text z výsledku a udělejte s ním něco užitečného. Pro tuto ukázku jej jednoduše vytiskneme do konzole, ale můžete jej zapsat do souboru, vložit do vyhledávacího indexu nebo předat jiné službě.

```java
// Step 5: Output the extracted text
System.out.println(ocrResult.getText());
```

Tento řádek sám dokazuje, že jste úspěšně **četli text z jpg** (nebo jakéhokoli podporovaného formátu). Pokud výstup vypadá poškozeně, zkontrolujte kód jazyka a kvalitu obrázku.

## Kompletní funkční příklad (všechny kroky dohromady)

Níže je kompletní, připravená ke spuštění Java třída, která spojuje všechny části. Zkopírujte ji do souboru pojmenovaného `OcrDemo.java`, upravte cestu k obrázku a jazyk, poté spusťte `javac OcrDemo.java && java OcrDemo`.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrInputImage;
import com.example.ocr.OcrResult;

/**
 * Demonstrates how to perform OCR in Java using a generic OCR SDK.
 * This example loads a JPG, sets the language to Mongolian, and prints
 * the recognized text to the console.
 *
 * Replace the import package with the actual library you are using.
 */
public class OcrDemo {

    public static void main(String[] args) {
        // Validate command‑line arguments
        if (args.length < 2) {
            System.err.println("Usage: java OcrDemo <image-path> <language-code>");
            System.exit(1);
        }

        String imagePath = args[0];   // e.g., "input.jpg"
        String language = args[1];    // e.g., "mon" for Mongolian

        // Step 1: Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image
        ocrEngine.setImage(new OcrInputImage(imagePath));

        // Step 3: Set the language (ISO‑639‑2)
        ocrEngine.getSettings().setLanguage(language);

        // Step 4: Run the recognition
        OcrResult result = ocrEngine.process();

        // Step 5: Print the extracted text
        System.out.println("=== Recognized Text ===");
        System.out.println(result.getText());
    }
}
```

### Očekávaný výstup

Pokud `input.jpg` obsahuje mongolskou frázi „Сайн байна уу?“, konzole zobrazí:

```
=== Recognized Text ===
Сайн байна уу?
```

Pokud je obrázek rozmazaný nebo je špatně nastaven kód jazyka, uvidíte poškozené znaky nebo prázdný řetězec – běžné úskalí, která probereme dále.

## Běžné úskalí a jak je opravit

| Příznak | Pravděpodobná příčina | Řešení |
|---------|-----------------------|--------|
| Poškozené cyrilické znaky | Špatný kód jazyka (výchozí na angličtinu) | Nastavte `ocrEngine.getSettings().setLanguage("mon")` nebo příslušný kód. |
| Žádný výstup | Cesta k obrázku nesprávná nebo soubor nečitelný | Ověřte cestu, ujistěte se, že soubor existuje a proces má oprávnění ke čtení. |
| Nízká přesnost (<70 %) | Obrázek má nízký kontrast nebo je otočený | Předzpracujte obrázek: zvýšte kontrast, vyrovnejte, nebo převést na odstíny šedi před předáním engine. |
| `OutOfMemoryError` při velkých PDF | Načítání mnoha vysokorozlišovacích stránek najednou | Zpracovávejte stránky po jedné, nebo před OCR zmenšete rozlišení obrázků. |

### Tip: Dávkové zpracování

Pokud potřebujete **extrahovat text z obrázku** souborů hromadně, zabalte hlavní logiku do smyčky:

```java
for (File img : new File("batchFolder").listFiles()) {
    ocrEngine.setImage(new OcrInputImage(img.getAbsolutePath()));
    OcrResult r = ocrEngine.process();
    System.out.println(r.getText());
}
```

Tento úryvek ukazuje, jak snadné je škálovat od jednoho JPG k celé složce skenů.

## Dál – Co prozkoumat dál?

- **Language Packs:** Většina OCR SDK umožňuje stáhnout další soubory jazykových dat. Přidání nového balíčku vám umožní **převést obrázek na text** pro jazyky mimo angličtinu a mongolštinu.
- **PDF OCR:** Kombinujte tento kód s Apache PDFBox pro

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, aby vám pomohly zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Extrahovat text z obrázků – Základy OCR s Aspose.OCR pro Java](/ocr/english/java/ocr-basics/)
- [Převést obrázek na text v Javě pomocí Aspose.OCR BufferedImage](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Jak provádět OCR textu obrázku s jazykem pomocí Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}