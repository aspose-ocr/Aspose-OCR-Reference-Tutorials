---
category: general
date: 2025-12-30
description: Vytvořte prohledávatelný PDF z obrázku v C# – naučte se, jak převést
  TIFF na PDF, extrahovat text z obrázku a automatizovat tvorbu PDF.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- convert tiff to pdf
- extract text from image
- how to create pdf
language: cs
og_description: Vytvořte prohledávatelný PDF z obrázku pomocí Aspose OCR v C#. Tento
  návod ukazuje, jak převést TIFF na PDF, extrahovat text a zajistit soulad s PDF/A‑1b.
og_title: Vytvořte prohledávatelný PDF z TIFF – krok za krokem C# tutoriál
tags:
- Aspose OCR
- C#
- PDF generation
title: Vytvořte prohledávatelný PDF z TIFF – kompletní průvodce C#
url: /cs/net/text-recognition/create-searchable-pdf-from-tiff-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF z TIFF – Kompletní průvodce v C#

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze skenovaného TIFF, ale nevedeli jste, kde začít? Nejste v tom sami. Mnoho vývojářů narazí na tento problém, když potřebují prohledávatelná PDF pro archivaci nebo soulad s předpisy, a dobrá zpráva je, že řešení je překvapivě jednoduché s Aspose OCR.

V tomto tutoriálu projdeme převodem obrázku na PDF, extrakcí textu z obrázku a vylepšením výstupu tak, aby splňoval standardy PDF/A‑1b. Na konci budete schopni **převést tiff na pdf**, **extrahovat text z obrázku** a přesně vědět **jak vytvořit pdf** soubory, které jsou jak prohledávatelné, tak připravené k archivaci.

## Co budete potřebovat

- .NET 6 (nebo jakákoli recentní verze .NET) – kód funguje jak na .NET Core, tak na .NET Framework.  
- Aspose.OCR NuGet balíček – nainstalujte jej pomocí `dotnet add package Aspose.OCR`.  
- Vzorek TIFF souboru (`input.tif`), který chcete převést na prohledávatelné PDF.  
- Vývojové prostředí (Visual Studio, VS Code, Rider… libovolné).  

To je vše. Žádné extra SDK, žádné externí služby a žádné skryté konfigurační kroky.

![Příklad vytvoření prohledávatelného PDF](image-placeholder.png "Náhled prohledávatelného PDF")

## Krok 1 – Inicializace OCR enginu a načtení anglického modelu

Než můžeme obrázek převést na prohledávatelný text, OCR engine potřebuje vědět, jaký jazyk má rozpoznávat. Aspose OCR dodává jazykové balíčky, které můžete načíst podle potřeby.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Load the English language model (you can swap this for other languages)
ocrEngine.LoadLanguage(LanguageModel.English);
```

**Proč je to důležité:** Načtení správného jazykového modelu dramaticky zvyšuje přesnost rozpoznání. Pokud tento krok přeskočíte, engine se vrátí k obecnému modelu, který často vrací zkreslený text – zejména u nízkokvalitních TIFF souborů.

## Krok 2 – Rozpoznání textu ze zdrojového obrázku (volitelné, ale užitečné)

Spuštění OCR vám vrátí objekt `OcrResult`, který můžete prohlížet, logovat nebo dokonce uložit jako prostý text. Tento krok je volitelný, pokud vás zajímá jen finální PDF, ale je skvělý pro ladění.

```csharp
// Perform OCR on the input TIFF
var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/input.tif");

// Dump the raw text to the console (useful for validation)
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

**Pro tip:** Pokud se extrahovaný text zdá nesprávný, zvažte předzpracování obrázku (odklon, odstranění šumu) před předáním engine. Aspose OCR také nabízí utility pro vylepšení obrazu, které můžete zde řetězit.

## Krok 3 – Nastavení exportéru prohledávatelného PDF

Nyní řekneme Aspose, jak má finální PDF vypadat. `SearchablePdfExporter` vám umožní specifikovat výstupní cestu, soulad s PDF/A a několik dalších vymožeností.

```csharp
var pdfExporter = new SearchablePdfExporter
{
    // Where the searchable PDF will be saved
    OutputPath = "YOUR_DIRECTORY/output.pdf",

    // Enforce PDF/A‑1b compliance – ideal for long‑term archiving
    PdfACompliance = PdfACompliance.PdfA1b
};
```

**Proč PDF/A‑1b?** Mnoho odvětví (právo, medicína, finance) vyžaduje PDF, která splňují archivní standardy. Nastavením `PdfACompliance` zajistíte vložení fontů, nezávislost barev na zařízení a projde validací nástrojů.

## Krok 4 – Export OCR výsledku přímo do prohledávatelného PDF

S připraveným enginem a exportérem je těžká část jednou řádkou. Exportér interně vytvoří PDF stránku, překryje rozpoznaný text jako neviditelnou vrstvu a zapíše soubor.

```csharp
// Export the OCR result to a searchable PDF
pdfExporter.Export(ocrEngine, "YOUR_DIRECTORY/input.tif");

// Confirmation message
Console.WriteLine("Searchable PDF created at YOUR_DIRECTORY/output.pdf");
```

**Co se děje pod kapotou?**  
1. Původní TIFF je vložen jako rastrový obrázek.  
2. Text získaný OCR je umístěn navrchu, skrytý, ale vybratelný.  
3. Přidají se metadata (např. jazyk), aby PDF čtečky mohly text indexovat.

## Krok 5 – Ověření výstupu (manuální kontrola + programová validace)

Je vždy dobrá praxe potvrdit, že PDF je skutečně prohledávatelné.

```csharp
// Quick sanity check: open the PDF and try to extract its text
using var pdfReader = new Aspose.Pdf.Facades.PdfConverter();
pdfReader.BindPdf("YOUR_DIRECTORY/output.pdf");
var extracted = pdfReader.ExtractText();
Console.WriteLine("Text extracted from the PDF:");
Console.WriteLine(extracted);
```

Pokud můžete z PDF prohlížeče text kopírovat nebo jej vidíte v konzolovém výstupu výše, podařilo se vám to.

## Okrajové případy a běžné varianty

### Převod jiných formátů obrázků

Stejný kód funguje pro PNG, JPEG, BMP – stačí změnit příponu souboru v voláních `Recognize` a `Export`. Žádná extra konfigurace není potřeba.

### Vícestránkové TIFF soubory

Aspose OCR automaticky zpracuje každou stránku vícestránkového TIFF a exportér je sloučí do vícestránkového PDF. Pokud potřebujete stránku přeskočit, odfiltrujte `ocrResult.Pages` před exportem.

### Neanglické jazyky

Vyměňte `LanguageModel.English` za `LanguageModel.Spanish`, `LanguageModel.French` apod., nebo načtěte vlastní jazykový balíček. Nezapomeňte upravit PDF metadata, pokud cílíte na konkrétní locale.

### Snížení velikosti PDF

Pokud jsou TIFF soubory vysokého rozlišení, výsledné PDF může být objemné. Můžete před OCR zmenšit rozlišení obrázku:

```csharp
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Dpi = 150 // Lower DPI reduces size, but test for acceptable quality
};
```

### Práce s PDF chráněnými heslem

Pokud potřebujete výstup chránit, zabalte `SearchablePdfExporter` do šifrovacího API Aspose.Pdf po exportu:

```csharp
var pdfDoc = new Aspose.Pdf.Document("YOUR_DIRECTORY/output.pdf");
pdfDoc.Encrypt("userPassword", "ownerPassword", 
    Aspose.Pdf.Permissions.All, Aspose.Pdf.EncryptionAlgorithms.AES256);
pdfDoc.Save("YOUR_DIRECTORY/output_protected.pdf");
```

## Kompletní funkční příklad

Níže je kompletní, připravený k zkopírování program, který zahrnuje všechny kroky a volitelné úpravy zmíněné výše.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Export;
using Aspose.Pdf.Facades;

class Program
{
    static void Main()
    {
        // -----------------------------------------------------------------
        // 1️⃣ Initialize OCR engine and load language model
        // -----------------------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.LoadLanguage(LanguageModel.English);

        // Optional: lower DPI to shrink output size (adjust as needed)
        // ocrEngine.ImageProcessingOptions = new ImageProcessingOptions { Dpi = 150 };

        // -----------------------------------------------------------------
        // 2️⃣ Recognize text from the source TIFF
        // -----------------------------------------------------------------
        const string inputPath = @"YOUR_DIRECTORY/input.tif";
        var ocrResult = ocrEngine.Recognize(inputPath);
        Console.WriteLine("Extracted text from image:");
        Console.WriteLine(ocrResult.Text);

        // -----------------------------------------------------------------
        // 3️⃣ Configure the searchable PDF exporter
        // -----------------------------------------------------------------
        var pdfExporter = new SearchablePdfExporter
        {
            OutputPath = @"YOUR_DIRECTORY/output.pdf",
            PdfACompliance = PdfACompliance.PdfA1b // archival compliance
        };

        // -----------------------------------------------------------------
        // 4️⃣ Export OCR result to searchable PDF
        // -----------------------------------------------------------------
        pdfExporter.Export(ocrEngine, inputPath);
        Console.WriteLine("Searchable PDF created successfully.");

        // -----------------------------------------------------------------
        // 5️⃣ Verify by extracting text from the generated PDF
        // -----------------------------------------------------------------
        using var converter = new PdfConverter();
        converter.BindPdf(@"YOUR_DIRECTORY/output.pdf");
        var extractedFromPdf = converter.ExtractText();
        Console.WriteLine("Text extracted from the PDF:");
        Console.WriteLine(extractedFromPdf);
    }
}
```

**Očekávaný výstup:**  
- Konzole vypíše surový OCR text z TIFF.  
- Soubor `output.pdf` se objeví v `YOUR_DIRECTORY`.  
- Otevřením `output.pdf` v Adobe Reader můžete text vybrat a zkopírovat, což potvrzuje, že je prohledávatelné.

## Shrnutí

Probrali jsme vše, co potřebujete k **vytvoření prohledávatelného PDF** ze TIFF obrázků pomocí Aspose OCR v C#. Od inicializace OCR enginu, extrakce textu, nastavení souladu s PDF/A až po ověření finálního dokumentu – každý krok je jasně vysvětlen. Nyní také víte, jak **převést obrázek na pdf**, **převést tiff na pdf**, **extrahovat text z obrázku** a jak **vytvořit pdf** s prohledávatelnými vrstvami.

## Co zkusit dál

- **Batch processing:** Zabalte logiku do smyčky, která automaticky zpracuje desítky obrázků.  
- **Custom fonts:** Vložte firemní fonty pro konzistenci značky.  
- **Cloud integration:** Ukládejte PDF přímo do Azure Blob Storage nebo AWS S3 po vytvoření.  
- **UI front‑end:** Vytvořte jednoduchou WinForms/WPF aplikaci, která uživatelům umožní přetahovat obrázky pro okamžitou konverzi.  

Neváhejte experimentovat s různými jazykovými modely, nastavením DPI a úrovněmi PDF/A. API je dostatečně flexibilní, aby se přizpůsobilo téměř jakémukoli workflow, který si dokážete představit.

---

*Šťastné programování a ať jsou vaše PDF vždy prohledávatelná!*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}