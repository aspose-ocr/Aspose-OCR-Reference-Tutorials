---
category: general
date: 2026-02-22
description: Vytvořte prohledávatelný PDF ze skenovaného PDF pomocí Aspose OCR v Javě.
  Naučte se převádět skenované PDF, komprimovat obrázky v PDF a efektivně rozpoznávat
  OCR v PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- compress pdf images
- recognize pdf ocr
- image pdf to text
language: cs
og_description: Vytvořte prohledávatelný PDF ze skenovaného PDF pomocí Aspose OCR
  v Javě. Tento krok‑za‑krokem návod ukazuje, jak převést skenovaný PDF, komprimovat
  obrázky v PDF a rozpoznat text pomocí OCR.
og_title: Vytvořte prohledávatelný PDF – Java průvodce převodem naskenovaných PDF.
tags:
- Java
- OCR
- PDF
- Aspose
title: Vytvořte prohledávatelný PDF – Java průvodce převodem naskenovaných PDF
url: /cs/java/advanced-ocr-techniques/create-searchable-pdf-java-guide-to-convert-scanned-pdfs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF – Java průvodce převodem naskenovaných PDF

Už jste někdy potřebovali **vytvořit prohledávatelný PDF** z hromady naskenovaných dokumentů? Je to častý problém—vaše PDF vypadají dobře, ale nemůžete použít *Ctrl + F* k vyhledání čehokoli. Dobrá zpráva? Několika řádky Java a Aspose OCR můžete převést tyto PDF obsahující jen obrázky na plně prohledávatelné soubory, **převést naskenované PDF** na text a dokonce zmenšit výsledek **kompresí obrázků PDF**.  

V tomto tutoriálu projdeme kompletním, spustitelným příkladem, vysvětlíme, proč je každé nastavení důležité, a ukážeme, jak upravit proces pro okrajové případy, jako jsou vícestránkové skeny nebo obrázky s nízkým rozlišením. Na konci budete mít solidní, připravený k nasazení úryvek kódu, který **recognize pdf ocr** spolehlivě rozpozná a vytvoří úhledný prohledávatelný dokument.

---

## Co budete potřebovat

- **Java 17** (nebo jakýkoli aktuální JDK; API je JDK‑agnostické)  
- **Aspose.OCR for Java** knihovna – můžete ji získat z Maven Central (`com.aspose:aspose-ocr`)  
- Naskenovaný PDF (pouze obrázek), který chcete učinit prohledávatelným  
- IDE nebo textový editor, ve kterém se cítíte pohodlně (IntelliJ, VS Code, Eclipse…)

Žádné těžké frameworky, žádné externí služby—pouze čistá Java a jediný JAR od třetí strany.  

---

![vytvořit prohledávatelný pdf příklad](placeholder-image.png "Ilustrace prohledávatelného PDF vytvořeného ze skenovaného dokumentu")

*Popisek obrázku:* **create searchable pdf** ilustrace ukazující před‑a‑po naskenovaného PDF převedeného na prohledávatelný text.

---

## Krok 1 – Inicializace OCR enginu  

První věc, kterou musíte udělat, je vytvořit instanci `OcrEngine`. Považujte ji za mozek, který analyzuje každý bitmap v PDF a vrací Unicode znaky.  

```java
import com.aspose.ocr.*;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Initialise the OCR engine – this object holds licensing info and global settings
        OcrEngine ocrEngine = new OcrEngine();
```

> **Tip:** Pokud plánujete zpracovávat mnoho PDF po sobě, znovu použijte stejný `OcrEngine` místo vytváření nového při každém spuštění. Ušetří to několik milisekund a sníží zatížení paměti.

---

## Krok 2 – Konfigurace PDF‑specifických OCR možností  

Aspose vám umožňuje jemně doladit, jak je výstupní PDF vytvořeno. Tři níže uvedená nastavení jsou nejvíce vlivná pro **compress pdf images**, zatímco zachovávají prohledávatelnost.

```java
        // Configure PDF‑specific options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // Higher DPI = better text recognition
        pdfOcrOptions.setCompressImages(true);           // Shrinks the final file size
        pdfOcrOptions.setEmbedOriginalImages(true);      // Keeps the visual look of the original scan
```

- **Output DPI** – 300 dpi je optimální hodnota; nižší hodnoty zrychlí proces, ale mohou vynechat malé písmo.  
- **CompressImages** – aktivuje bezztrátovou PNG kompresi pod kapotou; prohledávatelné PDF zůstane ostré, ale lehčí.  
- **EmbedOriginalImages** – bez tohoto příznaku by engine zahodil původní rastrový obrázek a zanechal jen neviditelný text. Zachování obrázku zajišťuje, že PDF vypadá přesně jako sken, což vyžaduje mnoho týmů pro soulad.

---

## Krok 3 – Načtení vašeho naskenovaného PDF do `OcrInput`  

Aspose čte zdrojový soubor pomocí obalu `OcrInput`. Můžete přidat více souborů, ale pro tuto ukázku se zaměříme na jediný **image PDF**.

```java
        // Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");   // <- replace with the path to your file
```

> **Proč nepředat jen `File`?** Použití `OcrInput` vám dává flexibilitu spojit několik PDF nebo dokonce kombinovat obrazové soubory (PNG, JPEG) před OCR. Je to doporučený vzor, když **convert scanned pdf**, který může být rozdělen do více zdrojů.

---

## Krok 4 – Provedení OCR a získání prohledávatelného PDF jako pole bajtů  

Nyní se děje magie. Engine analyzuje každou stránku, spustí svůj OCR engine a vytvoří nové PDF, které obsahuje jak původní obrázek, tak skrytou textovou vrstvu.

```java
        // Perform OCR – the result is a byte array representing the searchable PDF
        byte[] searchablePdfBytes = ocrEngine.recognizePdf(ocrInput, pdfOcrOptions);
```

Pokud potřebujete surový text pro jiné účely (např. indexování), můžete také zavolat `ocrEngine.recognize(ocrInput)`, který vrátí `String`. Ale pro cíl **create searchable pdf** je pole bajtů to, co zapíšete na disk.

---

## Krok 5 – Uložení prohledávatelného PDF na disk  

Nakonec zapíšete pole bajtů do souboru. Java NIO to umožňuje jedním řádkem.

```java
        // Write the searchable PDF to disk
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/searchable_output.pdf"),
                searchablePdfBytes
        );

        System.out.println("Searchable PDF created.");
    }
}
```

Když otevřete `searchable_output.pdf` v Adobe Acrobat nebo jakémkoli moderním prohlížeči, všimnete si, že můžete nyní vybrat, kopírovat a vyhledávat text—přesně to, co slibuje transformace **image pdf to text**.

---

## Převod naskenovaného PDF na text pomocí OCR (volitelné)

Někdy potřebujete jen extrahovaný čistý text, ne nové PDF. Můžete znovu použít stejný engine:

```java
        // Optional: extract plain text from the scanned PDF
        String extractedText = ocrEngine.recognize(ocrInput).getText();
        java.nio.file.Files.write(
                java.nio.file.Paths.get("YOUR_DIRECTORY/extracted_text.txt"),
                extractedText.getBytes()
        );
```

Tento úryvek ukazuje, jak snadné je **recognize pdf ocr** pro následné zpracování, jako je napájení vyhledávacího indexu nebo provádění analýzy přirozeného jazyka.

---

## Komprese obrázků PDF pro menší soubory  

Pokud jsou vaše zdrojové skeny obrovské (např. 600 dpi barevné skeny), výsledné prohledávatelné PDF může být stále objemné. Kromě příznaku `setCompressImages(true)` můžete před OCR ručně snížit rozlišení:

```java
        // Downscale each page image to 150 dpi before OCR (reduces size dramatically)
        pdfOcrOptions.setOutputDpi(150);
```

Snížení DPI zmenší velikost souboru přibližně na polovinu, ale otestujte čitelnost—některá písma se pod 150 dpi stanou nečitelné. Kompromis mezi **compress pdf images** a přesností OCR je něco, co rozhodnete na základě vašich úložných omezení.

---

## Vysvětlení nastavení Recognize PDF OCR  

| Nastavení                | Efekt na výstup                         | Typický případ použití                                   |
|--------------------------|------------------------------------------|----------------------------------------------------------|
| `setOutputDpi(int)`      | Řídí rozlišení rastru výstupu OCR        | Archivace vysoké kvality (300 dpi) vs. lehké webové PDF (150 dpi) |
| `setCompressImages`      | Povoluje PNG kompresi                    | Když potřebujete posílat PDF e-mailem nebo ukládat do cloudu |
| `setEmbedOriginalImages` | Udržuje původní sken viditelný            | Právní nebo compliance dokumenty, které musí zachovat původní vzhled |
| `setLanguage` (optional) | Vynutí jazykový model (např. "eng")      | Vícejazykové korpusy, kde výchozí automatické rozpoznání může selhat |

---

## Image PDF na Text – Běžné úskalí a jak se jim vyhnout  

1. **Low‑resolution scans** – Přesnost OCR výrazně klesá pod 150 dpi. Před předáním Aspose zdroj upscaleujte, nebo požádejte skener o vyšší DPI.  
2. **Rotated pages** – Pokud jsou stránky naskenovány šikmo, povolte auto‑rotaci: `pdfOcrOptions.setAutoRotate(true);`.  
3. **Encrypted PDFs** – Engine nemůže číst soubory chráněné heslem; nejprve je dešifrujte pomocí `PdfDocument` z Aspose.PDF.  
4. **Mixed raster and text** – Některé PDF již obsahují skrytou textovou vrstvu. Opětovné spuštění OCR může text duplikovat. Použijte `PdfOcrOptions.setSkipExistingText(true);` pro zachování původní vrstvy.  

Řešení těchto problémů zajišťuje, že váš pipeline **create searchable pdf** je robustní napříč reálnými kolekcemi dokumentů.

---

## Kompletní funkční příklad (všechny kroky v jednom souboru)

Níže je kompletní třída Java, kterou můžete zkopírovat a vložit do svého IDE. Nahraďte `YOUR_DIRECTORY` skutečnou cestou ke složce.

```java
import com.aspose.ocr.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class PdfToSearchableDemo {
    public static void main(String[] args) throws Exception {

        // 1️⃣ Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure PDF‑specific OCR options
        PdfOcrOptions pdfOcrOptions = new PdfOcrOptions();
        pdfOcrOptions.setOutputDpi(300);                 // higher DPI improves accuracy
        pdfOcrOptions.setCompressImages(true);           // reduce output size
        pdfOcrOptions.setEmbedOriginalImages(true);      // keep original visual fidelity

        // 3️⃣ Load the scanned PDF (image‑only) into an OcrInput object
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.pdf");        // <-- your source file

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}