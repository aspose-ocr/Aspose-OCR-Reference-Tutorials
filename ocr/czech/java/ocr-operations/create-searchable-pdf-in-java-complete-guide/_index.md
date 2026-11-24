---
category: general
date: 2026-07-05
description: Vytvořte prohledávatelný PDF v Javě pomocí Aspose OCR. Naučte se, jak
  komprimovat obrázky v PDF, převést naskenovaný obrázek na PDF a zakázat vkládání
  fontů do PDF pro menší soubory.
draft: false
keywords:
- create searchable pdf
- compress images in pdf
- convert scanned image to pdf
- disable font embedding pdf
language: cs
og_description: Vytvořte prohledávatelný PDF v Javě s Aspose OCR. Tento tutoriál ukazuje,
  jak komprimovat obrázky v PDF, převést naskenovaný obrázek na PDF a zakázat vkládání
  fontů do PDF.
og_title: Vytvořte prohledávatelný PDF v Javě – průvodce krok po kroku
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to compress
    images in PDF, convert scanned image to PDF, and disable font embedding PDF for
    smaller files.
  headline: Create Searchable PDF in Java – Complete Guide
  type: TechArticle
tags:
- Java
- OCR
- PDF
title: Vytvořte prohledávatelný PDF v Javě – Kompletní průvodce
url: /cs/java/ocr-operations/create-searchable-pdf-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF v Javě – Kompletní průvodce

Už jste někdy potřebovali **create searchable PDF** z naskenovaného dokumentu, ale uvízli jste u části „jak to udělat“? Nejste v tom sami. V mnoha projektech je převod TIFF nebo JPEG na PDF, který lze skutečně prohledávat, *must‑have* funkcí, zejména když chcete také **compress images in PDF**, aby velikost souboru zůstala zvládnutelná.  

V tomto tutoriálu projdeme praktickým příkladem pomocí Aspose OCR pro Java. Na konci přesně budete vědět, jak **convert scanned image to PDF**, upravit nastavení **compress images in PDF** a dokonce **disable font embedding PDF**, abyste ušetřili několik kilobajtů. Žádné zbytečnosti – jen kompletní, spustitelné řešení, které můžete dnes vložit do svého kódu.

## Co se naučíte

- Nastavit Aspose OCR engine v Java projektu.  
- Provést OCR na TIFF (nebo jakémkoli rastrovém obrázku).  
- Konfigurovat `PdfSaveOptions` pro **compress images in PDF** a **disable font embedding PDF**.  
- Uložit výsledek jako **searchable PDF**, který můžete okamžitě indexovat nebo prohledávat.  

**Požadavky**  
- Nainstalovaný Java 8 nebo novější.  
- Maven nebo Gradle pro správu závislostí (ukážeme Maven ukázku).  
- Naskenovaný soubor obrázku (TIFF, PNG nebo JPEG) připravený ke zpracování.  

Pokud je máte, pojďme na to.

![Create searchable PDF workflow – Java OCR to PDF conversion](/images/create-searchable-pdf-workflow.png "Diagram showing the steps to create searchable PDF with Aspose OCR")

## Krok 1: Přidání Aspose OCR závislosti

Nejprve přidejte knihovnu Aspose OCR do svého projektu. S Mavenem přidejte toto do vašeho `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- Use the latest stable version -->
</dependency>
```

Pokud dáváte přednost Gradlu, ekvivalent je:

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

> **Tip:** Sledujte poznámky k vydání Aspose; novější verze často přinášejí zvýšení výkonu a přesnosti OCR.

## Krok 2: Inicializace OCR engine

Vytvoření OCR engine je tak jednoduché jako vytvoření instance `OcrEngine`. Tento objekt bude zpracovávat vše od načítání obrázku po extrakci textu.

```java
import com.aspose.ocr.OcrEngine;

// ...

// Step 2: Create an OCR engine instance
OcrEngine engine = new OcrEngine();
```

Proč potřebujeme dedikovaný engine? Aspose odděluje těžkou práci (předzpracování obrázků, jazykové modely) od zbytku aplikace, takže můžete znovu použít stejný `engine` pro více souborů, aniž byste znovu inicializovali náročné zdroje.

## Krok 3: Provedení OCR na naskenovaném obrázku

Nyní předáme engine naskenovaný soubor. Metoda `recognizeImage` vrací `RecognitionResult`, který obsahuje extrahovaný text a informace o rozložení.

```java
import com.aspose.ocr.RecognitionResult;

// ...

// Step 3: Perform OCR on the source image
String sourcePath = "YOUR_DIRECTORY/document_scan.tif"; // could be .png or .jpg too
RecognitionResult result = engine.recognizeImage(sourcePath);
```

> **Co když obrázek není TIFF?**  
> Aspose OCR automaticky detekuje běžné rastrové formáty, takže jej můžete nasměrovat na JPEG, PNG nebo BMP bez úpravy kódu.

## Krok 4: Konfigurace PDF Save Options (Komprese obrázků a zakázání vkládání fontů)

Zde zazáří sekundární klíčová slova. Řekneme Aspose, aby **compress images in PDF** a **disable font embedding PDF**. Obě nastavení snižují konečnou velikost souboru – užitečné, když distribuujete desítky dokumentů.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

// ...

// Step 4: Set up PDF save options
PdfSaveOptions pdfOpts = new PdfSaveOptions();

// Reduce PDF size by compressing images
pdfOpts.setCompressImages(true);
pdfOpts.setImageQuality(80); // 0‑100, 80 is a good balance

// Prevent fonts from being embedded – saves a few KB per page
pdfOpts.setEmbedFonts(false);
```

**Proč komprimovat obrázky?**  
Naskenované stránky jsou často vysokého rozlišení; komprese na 80 % kvality může zmenšit 10‑stránkový PDF z 12 MB na méně než 3 MB bez znatelné ztráty kvality.

**Proč zakázat vkládání fontů?**  
Pokud OCR engine používá standardní systémové fonty (např. Arial nebo Times New Roman), jejich vkládání je nadbytečné. Vypnutí této funkce dále zmenšuje velikost souboru, zejména u velkých šarží.

## Krok 5: Uložení OCR výsledku jako prohledávatelného PDF

Poslední krok spojí vše dohromady: původní obrázek, extrahovanou textovou vrstvu a PDF možnosti, které jsme právě nastavili.

```java
// Step 5: Save the OCR result as a searchable PDF
String outputPath = "YOUR_DIRECTORY/document.pdf";
engine.saveAsSearchablePdf(outputPath, pdfOpts);

System.out.println("Searchable PDF created at: " + outputPath);
```

Když otevřete `document.pdf` v Adobe Readeru nebo jakémkoli moderním prohlížeči, uvidíte původní naskenovaný obrázek **plus** neviditelnou textovou vrstvu. Zadání slova do vyhledávacího pole zvýrazní shody – přesně to, co slibuje „create searchable pdf“.

### Očekávaný výstup

Spuštěním programu s platným TIFF získáte něco jako:

```
Searchable PDF created at: YOUR_DIRECTORY/document.pdf
```

Otevřete PDF, stiskněte `Ctrl+F`, zadejte slovo, které se na naskenované stránce vyskytuje, a sledujte, jak vás přenese na správné místo. To je znak úspěšného workflow **create searchable pdf**.

## Časté problémy a jak se jim vyhnout

| Problém | Proč se stane | Řešení |
|-------|----------------|-----|
| **Blank PDF** | `PdfSaveOptions` nebyly předány do `saveAsSearchablePdf`. | Ujistěte se, že voláte přetížení, které přijímá `PdfSaveOptions`. |
| **Garbage characters** | Jazyk OCR není nastaven (výchozí je angličtina). | Použijte `engine.getLanguage().setLanguage(OcrLanguage.FRENCH);` před `recognizeImage`. |
| **Huge file size** | `setCompressImages(false)` nebo `setEmbedFonts(true)`. | Nechte oba příznaky nastavené tak, jak je uvedeno výše. |
| **Image distortion** | `setImageQuality` nastaven příliš nízko (<50). | Držte se hodnot 70‑90 pro dobrý kompromis. |

## Rozšíření příkladu

Nyní, když můžete **convert scanned image to PDF** a kontrolovat velikost, můžete chtít:

- **Dávkové zpracování** složky skenů pomocí jednoduché smyčky `for(File f : folder.listFiles())`.  
- Přidat **vodoznaky** pomocí Aspose PDF (`PdfDocument.addWatermarkText`).  
- Exportovat OCR text do **plain .txt** souboru pro indexovací systémy (`result.getText().writeToFile("doc.txt")`).  

Všechny tyto rozšíření znovu používají stejnou instanci `OcrEngine`, čímž udržují nízkou spotřebu paměti.

## Kompletní, připravený k spuštění kód

```java
import com.aspose.ocr.OcrEngine;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOcrDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Perform OCR on the source image
        String source = "YOUR_DIRECTORY/document_scan.tif";
        RecognitionResult result = engine.recognizeImage(source);

        // Step 3: Configure PDF save options (compress images & disable fonts)
        PdfSaveOptions pdfOpts = new PdfSaveOptions();
        pdfOpts.setCompressImages(true);      // Reduce PDF size by compressing images
        pdfOpts.setImageQuality(80);          // Image quality (0‑100)
        pdfOpts.setEmbedFonts(false);         // Do not embed fonts to keep file size small

        // Step 4: Save the OCR result as a searchable PDF
        String output = "YOUR_DIRECTORY/document.pdf";
        engine.saveAsSearchablePdf(output, pdfOpts);

        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF created at: " + output);
    }
}
```

Zkopírujte a vložte toto do svého IDE, nahraďte `YOUR_DIRECTORY` skutečnou cestou a spusťte. Pokud je vše správně nastaveno, získáte **searchable PDF**, který je také lehký díky kompresi obrázků a zakázanému vkládání fontů.

## Závěr

Právě jsme probrali vše, co potřebujete k vytvoření **create searchable pdf** souborů v Javě pomocí Aspose OCR. Od inicializace engine, provedení OCR, úpravy **compress images in pdf** a **disable font embedding pdf**, až po finální uložení prohledávatelného dokumentu – každý krok byl vysvětlen s *proč*.

Jste připraveni na další výzvu? Zkuste přidat jazykové balíčky OCR, dávkové zpracování celých složek nebo vrstvení PDF s anotacemi. Základy, které jste právě zvládli, vám usnadní tato rozšíření.

Máte otázky nebo chcete sdílet své tipy? Zanechte komentář níže a šťastné programování!

## Co byste se měli naučit dál?

Následující tutoriály pokrývají úzce související témata, která staví na technikách předvedených v tomto průvodci. Každý zdroj obsahuje kompletní funkční ukázky kódu s podrobnými vysvětleními, které vám pomohou zvládnout další funkce API a prozkoumat alternativní přístupy k implementaci ve vašich projektech.

- [Rozpoznat text v PDF – OCR operace s Aspose.OCR pro Java](/ocr/english/java/ocr-operations/)
- [OCR rozpoznávání PDF dokumentů v Aspose.OCR pro Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Jak provést OCR PDF v .NET s Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}