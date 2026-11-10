---
category: general
date: 2026-06-16
description: Návod na OCR ohraničovací rámeček v Javě ukazuje, jak extrahovat text
  z obrázku, číst text z obrázku a získat skóre důvěryhodnosti OCR pro soubory JPG.
draft: false
keywords:
- ocr bounding box
- extract text from image
- ocr confidence score
- recognize text from jpg
- read text from image
language: cs
og_description: OCR ohraničující rámeček v Javě vám umožňuje rozpoznávat text z JPG
  souborů, extrahovat text z obrázku a zobrazovat skóre důvěryhodnosti OCR – vše v
  jednoduchém příkladu kódu.
og_title: OCR ohraničovací rámeček v Javě – Extrahovat text z obrázku
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: OCR bounding box tutorial in Java shows how to extract text from image,
    read text from image, and get OCR confidence score for JPG files.
  headline: OCR Bounding Box in Java – Extract Text from Image
  type: TechArticle
tags:
- OCR
- Java
- image-processing
- text-recognition
title: OCR ohraničující rámeček v Javě – Extrahování textu z obrázku
url: /cs/java/advanced-ocr-techniques/ocr-bounding-box-in-java-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Bounding Box v Javě – Extrahování textu z obrázku

Už jste se někdy ptali, jak získat **ocr bounding box** pro každý kus textu v Java obrázku? V tomto tutoriálu vám ukážeme, jak **extrahovat text z obrázku** souborů, **číst text z obrázku**, a dokonce zobrazit **ocr confidence score**, zatímco **rozpoznáváte text z jpg** souborů. Krátká odpověď? Několik řádků kódu s moderní OCR knihovnou a trochu vysvětlení, proč je každé volání důležité.

Níže najdete kompletní, připravený k spuštění příklad, krok‑za‑krokem rozbor a několik praktických tipů, které můžete zkopírovat přímo do svého projektu. Na konci budete schopni vygenerovat něco jako:

```
Text: "Hello World"  Confidence: 0.97  Box: (x=12, y=45, width=210, height=30)
```

## Co budete potřebovat

- **Java 11** nebo novější (syntaxe níže používá klíčové slovo `var` pro stručnost, ale můžete jej vynechat pro starší JDK).  
- OCR knihovna, která nabízí Java API – pro tento návod použijeme **[Tesseract4J](https://github.com/nguyenq/tess4j)**, tenkou obálku kolem populárního Tesseract enginu.  
- JPEG obrázek (`.jpg`), který obsahuje jasný, tištěný text.  
- Vaše oblíbené IDE (IntelliJ IDEA, Eclipse, VS Code…) – jakékoliv bude stačit.

Pokud vám knihovna chybí, stačí přidat tuto Maven závislost:

```xml
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.4.0</version>
</dependency>
```

Teď se ponořme.

![OCR bounding box example](ocr-bounding-box.png "OCR bounding box example")

## OCR Bounding Box: Nastavení enginu

První věc, kterou musíte udělat, je vytvořit instanci OCR enginu. Představte si to jako zapnutí skeneru, který později bude číst pixely.

```java
import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;

ITesseract ocrEngine = new Tesseract();          // Step 1 – create the OCR engine
ocrEngine.setDatapath("tessdata");               // point to the language data files
ocrEngine.setLanguage("eng");                    // we’ll work with English for now
```

**Proč je to důležité:**  
Bez nastavení `datapath` Tesseract nebude vědět, kde jsou umístěny jazykové balíčky, a dostanete kryptickou chybu „Failed loading language“. Volání `setLanguage` je volitelné, pokud potřebujete jen výchozí anglický balíček, ale explicitní nastavení činí kód srozumitelnějším pro budoucí čtenáře.

## Načtení obrázku, který chcete zpracovat

Dále poskytněte enginu JPEG, který chcete analyzovat. Knihovna přijímá `File` nebo `BufferedImage`; pro jednoduchost použijeme `File`.

```java
import java.io.File;

File imageFile = new File("YOUR_DIRECTORY/text_page.jpg");   // Step 2 – load the image
```

**Pro tip:**  
Pokud je váš obrázek v resources (např. uvnitř JAR), použijte `getResourceAsStream` a zabalte jej pomocí `ImageIO.read`. Tímto způsobem tutoriál funguje jak lokálně, tak v zabalené aplikaci.

## Provedení OCR rozpoznání

Nyní skutečně požádáme engine, aby přečetl obrázek. Výsledkem je řetězec prostého textu, ale také chceme **ocr confidence score** a **ocr bounding box** pro každý řádek.

```java
try {
    // Step 3 – run OCR and get a result object with layout data
    var result = ocrEngine.doOCR(imageFile, null);
    // The simple doOCR call returns only text; to get boxes we need the
    // getWords method with a specific page iterator level.
    var words = ocrEngine.getWords(imageFile, ITesseract.PageIteratorLevel.RIL_WORD);
    
    // Step 4 – iterate over each detected word
    for (var word : words) {
        System.out.printf(
            "Text: \"%s\"  Confidence: %.2f  Box: %s%n",
            word.getText(),
            word.getConfidence(),
            word.getBoundingBox().toString()
        );
    }
} catch (TesseractException e) {
    System.err.println("OCR failed: " + e.getMessage());
}
```

**Proč používáme `getWords` místo prostého `doOCR`:**  
`doOCR` vám poskytne surový řetězec, ale zahodí prostorové informace. Voláním `getWords` s `RIL_WORD` (nebo `RIL_TEXTLINE`, pokud preferujete rámečky na úrovni řádku) získáme seznam objektů `Word`, z nichž každý obsahuje text, důvěru a ohraničující obdélník. To je jádro funkce **ocr bounding box**.

## Porozumění výstupu

Spuštěním výše uvedeného úryvku na čistém JPEG získáte výstup podobný tomuto:

```
Text: "Hello"  Confidence: 0.99  Box: java.awt.Rectangle[x=34,y=12,width=112,height=28]
Text: "World"  Confidence: 0.97  Box: java.awt.Rectangle[x=156,y=12,width=98,height=28]
```

- **Text** – rozpoznané znaky.  
- **Confidence** – desetinná hodnota mezi 0 a 1; vyšší hodnota znamená, že engine je si jistější.  
- **Box** – obdélník, který obklopuje slovo v pixelových souřadnicích (x, y, šířka, výška).  

Nyní můžete **číst text z obrázku** a také přesně vědět, kde se každý úryvek nachází na plátně – ideální pro zvýrazňování, ořezávání nebo předávání do následných NLP pipeline.

## Okrajové případy a běžné úskalí

| Situace | Na co si dát pozor | Oprava / Řešení |
|-----------|-------------------|-------------------|
| Obrázek je rozmazaný nebo má nízký kontrast | Skóre důvěry dramaticky klesá (často pod 0,6). | Předzpracování pomocí OpenCV: zvýšit kontrast, aplikovat prahování. |
| JPEG obsahuje otočený text | Ohraničující rámečky jsou zkosené nebo chybí. | Použijte `ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO_OSD)`, aby Tesseract automaticky detekoval orientaci. |
| Velké obrázky způsobují OutOfMemoryError | Halda Java se zaplní při načítání velkých obrázků. | Zmenšete obrázek před OCR (`ImageIO.read` → `BufferedImage.getScaledInstance`). |
| Potřebujete rámečky na úrovni řádku místo úrovně slova | `RIL_WORD` vrací rámečky pro každé slovo. | Přepněte na `ITesseract.PageIteratorLevel.RIL_TEXTLINE`. |
| Neanglické znaky se zobrazují jako � | Jazyková data nejsou načtena. | Stáhněte si příslušný soubor `.traineddata` a nastavte `setDatapath` na jeho složku. |

Řešení těchto problémů včas vám ušetří hodiny ladění později.

## Kompletní funkční příklad (všechny kroky v jednom souboru)

Níže je samostatná Java třída, kterou můžete zkopírovat a vložit do složky `src/main/java` a spustit pomocí `mvn exec:java`. Spojuje vše, o čem jsme mluvili.

```java
package com.example.ocrdemo;

import net.sourceforge.tess4j.ITesseract;
import net.sourceforge.tess4j.ITesseract.RenderedFormat;
import net.sourceforge.tess4j.Tesseract;
import net.sourceforge.tess4j.TesseractException;
import net.sourceforge.tess4j.Word;

import java.io.File;
import java.util.List;

public class OcrBoundingBoxDemo {

    public static void main(String[] args) {
        // ==== Step 1: Initialize the OCR engine ====
        ITesseract ocrEngine = new Tesseract();
        ocrEngine.setDatapath("tessdata"); // folder containing .traineddata files
        ocrEngine.setLanguage("eng");      // English language pack

        // Optional: improve accuracy for printed text
        ocrEngine.setPageSegMode(ITesseract.PageSegMode.PSM_AUTO);
        ocrEngine.setOcrEngineMode(ITesseract.OEM_TESSERACT_ONLY);

        // ==== Step 2: Load the JPEG you want to read ====
        File imageFile = new File("YOUR_DIRECTORY


## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s krok‑za‑krokem vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní implementační přístupy ve vašich projektech.

- [Extrahovat text z obrázku v Javě s Aspose.OCR – režim Detekce oblastí](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extrahovat textové obrázky – Základy OCR s Aspose.OCR pro Javu](/ocr/english/java/ocr-basics/)
- [Jak provést OCR textu na obrázku s jazykem pomocí Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}