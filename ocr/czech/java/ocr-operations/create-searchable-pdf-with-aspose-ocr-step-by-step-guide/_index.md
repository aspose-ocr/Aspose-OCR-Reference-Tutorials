---
category: general
date: 2026-01-02
description: Vytvořte prohledávatelný PDF ze skenovaného PDF obrazu pomocí Aspose
  OCR. Naučte se nastavit jazyk OCR, vložit textovou vrstvu do PDF a použít možnosti
  vysoké komprese PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- high compression pdf
- embed text layer pdf
- set OCR language
language: cs
og_description: Rychle vytvořte prohledávatelný PDF. Tento návod ukazuje, jak převést
  naskenovaný PDF obrázek, vložit textovou vrstvu, nastavit jazyk OCR a povolit vysokou
  kompresi PDF.
og_title: Vytvořte prohledávatelný PDF pomocí Aspose OCR – kompletní průvodce
tags:
- Aspose OCR
- Java PDF
- Document Automation
title: Vytvořte prohledávatelný PDF pomocí Aspose OCR – průvodce krok za krokem
url: /cs/java/ocr-operations/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF – Kompletní programovací tutoriál

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** soubory ze skenovaných obrázků, ale nevedeli jste, kde začít? Nejste v tom jediní. V mnoha pracovních postupech s velkým množstvím dokumentů je obyčejné PDF jen s obrázkem slepou uličkou pro vyhledávání a indexaci.  

Dobrou zprávou je, že s Aspose OCR můžete **převést PDF se skenovaným obrázkem** na plně prohledávatelný dokument během několika řádků Java kódu. Tento tutoriál vás provede každým krokem – inicializací OCR enginu, nastavením vysoké komprese PDF, vložením skryté textové vrstvy a dokonce výběrem správného jazyka OCR.  

Na konci tohoto průvodce budete mít spustitelný program, který vytvoří prohledávatelné PDF, soubor, který můžete bez problémů vložit do jakéhokoli vyhledávače nebo systému správy dokumentů.

---

## Vytvoření prohledávatelného PDF – Přehled

Než se ponoříme do kódu, upřesněme, co vlastně znamená „vytvořit prohledávatelné PDF“. Prohledávatelné PDF obsahuje dvě paralelní vrstvy:

1. **Vizální vrstva** – originální skenovaný obrázek (nebo vykreslená stránka).  
2. **Textová vrstva** – neviditelné, ale strojově čitelné znaky získané pomocí OCR.

Když otevřete takové PDF v Adobe Readeru a vyberete text, ve skutečnosti pracujete se skrytou textovou vrstvou, nikoli s obrázkem. Tento dvojvrstvý přístup umožňuje funkci **embed text layer PDF**.

## Převod PDF se skenovaným obrázkem pomocí Aspose OCR

Prvním, co potřebujete, je skenovaný obrázek (PNG, JPEG, TIFF), který chcete převést na PDF. Aspose OCR dokáže tento obrázek načíst, spustit OCR a předat výsledek PDF zapisovači.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Initialize the OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Step 2: Configure PDF save options to embed a searchable text layer
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // enable searchable PDF
        pdfSaveOptions.setCompressionLevel(9);        // optional: high compression

        // Step 3: Perform OCR on the scanned image and save the result as a searchable PDF
        ocrEngine.recognizeImageAndSave(
                "YOUR_DIRECTORY/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,                // set OCR language
                "YOUR_DIRECTORY/output.pdf",                // output PDF file
                pdfSaveOptions);                            // options defined above

        // Step 4: Indicate that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

**Proč to funguje:**  
- `setCreateSearchablePdf(true)` říká Aspose, aby vygeneroval skrytou textovou vrstvu, čímž splňuje požadavek **embed text layer pdf**.  
- `setCompressionLevel(9)` posouvá soubor do rozsahu **high compression pdf**, zmenšuje konečnou velikost bez ztráty přesnosti OCR.  
- Argument `RecognitionLanguage.ENGLISH` ukazuje, jak **set OCR language**; můžete jej nahradit francouzštinou, němčinou atd., podle vašeho zdrojového materiálu.

## Nastavení vysoké komprese PDF

Velká skenovaná PDF mohou rychle narůst na stovky megabajtů. Aspose nabízí jednoduché kompresní API, které funguje na úrovni PDF. Metoda `setCompressionLevel` přijímá hodnoty od 0 (žádná komprese) do 9 (maximální komprese).  

```java
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
pdfSaveOptions.setCompressionLevel(9); // 9 = strongest compression
```

Pár tipů:

- **Používejte bezztrátové formáty obrázků** (PNG) pro skeny s velkým množstvím textu; JPEG je lepší pro fotografie.  
- **Povolte podmnožinu fontů** pokud vkládáte vlastní písma – Aspose to provádí automaticky při vytváření prohledávatelného PDF.  
- **Otestujte velikost výstupu** po každé změně; někdy komprese úrovně 8 poskytne 10 % úsporu velikosti s neznatelnou ztrátou kvality ve srovnání s úrovní 9.

## Vložení textové vrstvy PDF pro prohledatelnost

Pokud vynecháte volání `setCreateSearchablePdf(true)`, výsledný soubor bude vypadat v pořádku, ale nebudete moci prohledávat jeho obsah. Skrytá textová vrstva je vytvořena mapováním každého rozpoznaného znaku na jeho umístění na stránce.  

```java
pdfSaveOptions.setCreateSearchablePdf(true);
```

**Na co si dát pozor:**  

- **Dokumenty s více jazyky** – možná budete muset spustit OCR dvakrát, jednou pro každý jazyk, a poté sloučit textové vrstvy.  
- **Komplexní rozvržení** (tabulky, více sloupců) – Aspose odvádí slušnou práci, ale výstup si dvakrát ověřte v PDF prohlížeči, který zobrazuje skrytý text (např. režim „Edit PDF“ v Adobe Acrobat).

## Nastavení jazyka OCR pro přesné rozpoznání

Přesnost OCR enginu závisí na jazyce, který mu nastavíte. Aspose obsahuje sadu vestavěných jazyků a můžete také přidat vlastní jazykové balíčky.

```java
ocrEngine.recognizeImageAndSave(
        "input.png",
        RecognitionLanguage.ENGLISH, // change to RecognitionLanguage.FRENCH, etc.
        "output.pdf",
        pdfSaveOptions);
```

**Kdy změnit jazyk:**  

- Dokumenty obsahují **ne-latinské skripty** (cyrilice, arabština) – přepněte na odpovídající `RecognitionLanguage`.  
- Stránky s více jazyky – můžete volat `recognizeImageAndSave` dvakrát, pokaždé s jiným jazykem, a poté sloučit PDF soubory.

## Spuštění kompletního příkladu

Níže je celý, připravený k spuštění program. Nahraďte zástupné cesty skutečnými umístěními souborů, ujistěte se, že Aspose OCR JAR je ve vaší classpath, a spusťte.

```java
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.PdfSaveOptions;
import com.aspose.ocr.RecognitionLanguage;

public class PdfSearchableExample {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine
        AsposeOCR ocrEngine = new AsposeOCR();

        // Configure PDF save options
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions();
        pdfSaveOptions.setCreateSearchablePdf(true);   // embed text layer PDF
        pdfSaveOptions.setCompressionLevel(9);        // high compression PDF

        // Perform OCR and save searchable PDF
        ocrEngine.recognizeImageAndSave(
                "C:/scans/input.png",                 // path to scanned image
                RecognitionLanguage.ENGLISH,          // set OCR language
                "C:/output/searchable.pdf",           // output PDF
                pdfSaveOptions);                      // options defined above

        System.out.println("Searchable PDF created.");
    }
}
```

**Očekávaný výstup:** Po spuštění programu se v konzoli vypíše:

```
Searchable PDF created.
```

Otevřete `searchable.pdf` v libovolném PDF prohlížeči, zkuste vybrat text a uvidíte skrytou vrstvu v akci. Úspěšně jste **vytvořili prohledávatelné PDF** ze skenovaného obrázku.

![příklad vytvoření prohledávatelného pdf](image-placeholder.png "příklad vytvoření prohledávatelného pdf")

*Výše uvedený snímek (zástupný) by typicky ukazoval PDF prohlížeč s vybraným textem přes skenovanou stránku.*

## Závěr

Probrali jsme vše, co potřebujete k **vytvoření prohledávatelných PDF** souborů pomocí Aspose OCR:

- Inicializujte OCR engine.  
- **Převod PDF se skenovaným obrázkem** tím, že předáte PNG/JPEG do `recognizeImageAndSave`.  
- Použijte `setCreateSearchablePdf(true)` k **embed text layer PDF**.  
- Použijte `setCompressionLevel(9)` pro **high compression PDF**, který zůstane lehký.  
- Zvolte správný `RecognitionLanguage` pro **set OCR language** s maximální přesností.

Odtud můžete experimentovat s dávkovým zpracováním, různými jazyky nebo dokonce sloučit více skenovaných stránek do jednoho prohledávatelného PDF. Stejný vzor funguje i pro jiné jazyky, jako španělština nebo japonština – stačí vyměnit enum `RecognitionLanguage`.  

Neváhejte zanechat komentář, pokud narazíte na potíže, a šťastné programování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}