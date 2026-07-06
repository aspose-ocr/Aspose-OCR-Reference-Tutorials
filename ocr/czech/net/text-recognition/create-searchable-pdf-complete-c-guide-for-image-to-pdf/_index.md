---
category: general
date: 2026-04-08
description: Rychle vytvořte prohledávatelný PDF a naučte se, jak komprimovat obrázky
  v PDF, vkládat písma do PDF a rozpoznávat text z obrázku v C# pomocí Aspose.OCR.
draft: false
keywords:
- create searchable pdf
- compress pdf images
- embed fonts pdf
- image to searchable pdf
- recognize text image
language: cs
og_description: Rychle vytvořte prohledávatelný PDF pomocí Aspose.OCR. Naučte se komprimovat
  obrázky v PDF, vkládat písma do PDF a rozpoznávat text na obrázcích v jednom tutoriálu.
og_title: Vytvořte prohledávatelný PDF – kompletní průvodce C#
tags:
- Aspose.OCR
- C#
- PDF Generation
title: Vytvořte prohledávatelný PDF – Kompletní C# průvodce pro převod obrázku na
  PDF
url: /cs/net/text-recognition/create-searchable-pdf-complete-c-guide-for-image-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF – Kompletní průvodce v C#

Potřebujete **vytvořit prohledávatelné pdf** ze skenovaného obrázku? Nejsi jediný, kdo se díval na obrovský PNG a přemýšlel, jak ho převést na lehký, textově prohledávatelný dokument. Dobrou zprávou je, že s Aspose.OCR to můžete udělat během několika řádků a zároveň se naučíte, jak **compress PDF images**, **embed fonts PDF**, a **recognize text image** bez potíží.

V tomto tutoriálu projdeme celý proces: od načtení obrázku, spuštění OCR, úpravy možností uložení PDF až po finální zápis prohledávatelného PDF na disk. Na konci budete mít připravenou metodu, kterou můžete vložit do libovolného .NET projektu, a také několik profesionálních tipů pro okrajové případy, na které můžete později narazit.

## Co budete potřebovat

- **.NET 6+** (kód funguje také na .NET Framework 4.7, ale zaměříme se na .NET 6 pro moderní syntaxi).  
- **Aspose.OCR for .NET** – nainstalujte přes NuGet: `Install-Package Aspose.OCR`.  
- Soubor s obrázkem (PNG, JPEG, TIFF), který obsahuje text, který chcete učinit prohledávatelným.  
- Trocha zvědavosti – zbytek je popsán níže.

> **Pro tip:** Pokud plánujete zpracovávat desítky stránek, zvažte opětovné použití jediné instance `OcrEngine`, abyste se vyhnuli režii opakovaného načítání jazykových dat.

## Krok 1: Nastavení OCR enginu – Rozpoznání textu na obrázku

Prvním, co potřebujeme, je OCR engine, který dokáže přečíst znaky ze zdrojového bitmapu. Aspose.OCR vám umožní zadat jazyk (English, French, atd.) a vrátí objekt `OcrResult`, který obsahuje jak surový text, tak data obrázku.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

public static OcrResult LoadAndRecognize(string imagePath)
{
    // Initialize the OCR engine – “en” is the ISO code for English.
    var ocrEngine = new OcrEngine { Language = "en" };

    // Recognize the image and get the result.
    OcrResult result = ocrEngine.RecognizeImage(imagePath);

    // Quick sanity check – throw if nothing was detected.
    if (string.IsNullOrWhiteSpace(result.Text))
        throw new InvalidOperationException("No text was recognized in the image.");

    return result;
}
```

**Proč je to důležité:**

- Nastavení jazyka dramaticky zvyšuje přesnost; engine načítá jazykově specifické slovníky na pozadí.  
- `OcrResult` neobsahuje jen extrahovaný řetězec, ale také podkladový bitmap, který později vložíme do PDF, aby dokument zůstal vizuálně identický s původním skenem.

## Krok 2: Konfigurace možností uložení PDF – Komprese PDF obrázků a vložení fontů

Prohledávatelné PDF je v podstatě běžné PDF s neviditelnou textovou vrstvou nad naskenovaným obrázkem. Pokud ignorujete kompresi, může být výsledný soubor obrovský. Třída `PdfSaveOptions` vám poskytuje detailní kontrolu nad kvalitou obrázku, vložením fontů a tím, zda mají být fonty podmnoženy.

```csharp
public static PdfSaveOptions GetPdfSaveOptions()
{
    return new PdfSaveOptions
    {
        // Reduce file size by compressing the raster image.
        CompressImages = true,

        // ImageQuality ranges from 0 (worst) to 100 (best). 75 is a good balance.
        ImageQuality = 75,

        // Embedding fonts ensures the text layer looks the same on any machine.
        EmbedFonts = true,

        // Subsetting keeps only the glyphs we actually use – another size saver.
        FontSubset = true
    };
}
```

**Proč byste měli vložit fonty do PDF:**

Když je PDF otevřeno na systému, který nemá přesně ten font použité v OCR vrstvě, text se může zobrazit poškozeně. Vložení fontů zaručuje vizuální věrnost napříč platformami, což je klíčové pro právní nebo archivní dokumenty.

## Krok 3: Uložení výsledku jako prohledávatelné PDF – Obrázek na prohledávatelné PDF

Nyní spojíme vše dohromady: vezmeme `OcrResult`, použijeme naše `PdfSaveOptions` a zapíšeme soubor. Metoda `SaveAsSearchablePdf` provede těžkou práci – vytvoří skrytou textovou vrstvu, která odráží výstup OCR, a zároveň zachová původní obrázek.

```csharp
public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
{
    // Step 1: Recognize the image.
    OcrResult ocrResult = LoadAndRecognize(inputImage);

    // Step 2: Prepare PDF options.
    PdfSaveOptions pdfOptions = GetPdfSaveOptions();

    // Step 3: Write the searchable PDF.
    ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);

    Console.WriteLine($"Searchable PDF created at: {outputPdf}");
}
```

### Kompletní funkční příklad

Níže je samostatný konzolový program, který můžete zkopírovat a vložit do nového .NET konzolového projektu. Předpokládá, že obrázek se nachází ve složce `YOUR_DIRECTORY` relativně k spustitelnému souboru.

```csharp
using Aspose.Ocr;
using Aspose.Ocr.Pdf;
using System;

class Program
{
    static void Main()
    {
        string inputPath = "YOUR_DIRECTORY/input.png";
        string outputPath = "YOUR_DIRECTORY/output.pdf";

        try
        {
            CreateCompressedSearchablePdf(inputPath, outputPath);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }

    // --- Methods from the previous steps -------------------------------------------------
    public static OcrResult LoadAndRecognize(string imagePath)
    {
        var ocrEngine = new OcrEngine { Language = "en" };
        OcrResult result = ocrEngine.RecognizeImage(imagePath);
        if (string.IsNullOrWhiteSpace(result.Text))
            throw new InvalidOperationException("OCR did not detect any text.");
        return result;
    }

    public static PdfSaveOptions GetPdfSaveOptions()
    {
        return new PdfSaveOptions
        {
            CompressImages = true,
            ImageQuality = 75,
            EmbedFonts = true,
            FontSubset = true
        };
    }

    public static void CreateCompressedSearchablePdf(string inputImage, string outputPdf)
    {
        OcrResult ocrResult = LoadAndRecognize(inputImage);
        PdfSaveOptions pdfOptions = GetPdfSaveOptions();
        ocrResult.SaveAsSearchablePdf(outputPdf, pdfOptions);
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Spuštěním programu vznikne `output.pdf`, který můžete otevřít v Adobe Reader, Foxit nebo jakémkoli PDF prohlížeči a okamžitě vyhledávat slova, která byla původně jen na obrázku.

## Krok 4: Ověření výstupu – Funguje vyhledávání?

Po vygenerování souboru jej otevřete a vyzkoušejte vestavěné vyhledávání (Ctrl + F). Pokud najdete slova jako „invoice“, „date“ nebo „total“, úspěšně jste vytvořili **searchable PDF**.  

Pokud vyhledávání nic nevrátí:

1. **Check OCR accuracy** – možná je zdrojový obrázek nízkého rozlišení. Zvažte zvýšení DPI před OCR (Aspose umožňuje nastavit `Resolution` na engine).  
2. **Confirm font embedding** – otevřete vlastnosti PDF a pod *Fonts* byste měli vidět vložený font.  
3. **Inspect image compression** – velmi nízká hodnota `ImageQuality` může učinit vizuální vrstvu nečitelné, což někdy zmátne následné nástroje.

## Běžné varianty a okrajové případy

| Scénář | Co upravit | Proč |
|----------|----------------|-----|
| **Multi‑page TIFF** | Procházet každý rámec, volat `RecognizeImage` pro každou stránku a poté použít `PdfSaveOptions` s `AppendMode = true`. | Uchovává každou naskenovanou stránku jako samostatnou prohledávatelnou stránku. |
| **Non‑English language** | Změňte `Language = "fr"` (nebo odpovídající ISO kód) a volitelně poskytněte vlastní slovník. | Zlepšuje rozpoznávání pro znaky s diakritikou a jazykově specifické glyfy. |
| **Very large images** | Zmenšete bitmapu před OCR (`ocrEngine.Image = Image.FromFile(...).GetThumbnailImage(...)`). | Snižuje využití paměti a urychluje OCR bez výrazné ztráty přesnosti. |
| **Need OCR confidence** | Přistupte k `ocrResult.RecognizedWords` a zkontrolujte vlastnost `Confidence`. | Umožňuje označit slova s nízkou důvěrou pro ruční kontrolu. |

## Tipy pro výkon

- **Reuse the `OcrEngine`** při zpracování dávky souborů – kešuje jazyková data.  
- **Parallelize** krok rozpoznání pomocí `Parallel.ForEach`, pokud máte vícejádrový počítač, ale zápisy PDF provádějte sekvenčně, aby nedocházelo ke konfliktům při přístupu k souborům.  
- **Tune `ImageQuality`**: 85‑90 poskytuje téměř bezztrátové obrázky, zatímco 60‑70 je často dostačující pro dokumenty s velkým množstvím textu.

## Závěr

Probrali jsme vše, co potřebujete k **create searchable pdf** souborům z obrázků pomocí Aspose.OCR, a zároveň se naučili, jak **compress pdf images**, **embed fonts pdf**, a efektivně **recognize text image**. Kompletní ukázkový kód je připraven k vložení do libovolného C# projektu a další tipy vám pomohou přizpůsobit řešení většímu zatížení nebo různým jazykům.

Jste připraveni na další krok? Zkuste přidat vodoznak, sloučit více prohledávatelných PDF nebo integrovat tuto rutinu do webového API, aby uživatelé mohli nahrávat skeny a okamžitě získat prohledávatelná PDF. Možnosti jsou neomezené a s pevnými základy vám rozšíření workflow přijde snadné.

Šťastné kódování a ať vaše PDF zůstávají malé, prohledávatelné a dokonale vykreslené!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}