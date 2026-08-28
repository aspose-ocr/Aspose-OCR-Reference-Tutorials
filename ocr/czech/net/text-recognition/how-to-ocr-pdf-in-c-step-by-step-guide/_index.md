---
category: general
date: 2025-12-29
description: Naučte se, jak provádět OCR PDF souborů v C# a extrahovat text z PDF
  stránek. Tento tutoriál také pokrývá převod PDF na text a techniky čtení PDF stránek
  v C#.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- extract pdf text c#
- read pdf page c#
language: cs
og_description: Jak provést OCR PDF v C# vysvětleno v stručném průvodci. Získejte
  kompletní kód pro extrakci textu z PDF, převod PDF na text a čtení stránky PDF v
  C#.
og_title: Jak provést OCR PDF v C# – Kompletní programovací průvodce
tags:
- OCR
- C#
- PDF processing
title: Jak provést OCR PDF v C# – krok za krokem
url: /cs/net/text-recognition/how-to-ocr-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provést OCR PDF v C# – krok za krokem průvodce

Už jste se někdy zamysleli, **jak provést OCR PDF** soubory přímo ze své C# aplikace? Možná máte hromadu naskenovaných faktur a potřebujete z nich vytáhnout text bez ručního kopírování. To je častý problém, zejména když jsou PDF založeny na obrázcích a tradiční extrakce textu selže.  

V tomto tutoriálu projdeme kompletní, připravené řešení, které nejen ukazuje, **jak provést OCR PDF**, ale také demonstruje, jak *extrahovat text z PDF*, *převést PDF na text* a *číst PDF stránku v C#* pomocí knihovny Aspose.OCR. Žádné vágní odkazy – jen kód, který můžete vložit do Visual Studia a začít experimentovat.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód funguje také na .NET Framework 4.7+)  
- **Aspose.OCR** NuGet balíček – nainstalujte pomocí `dotnet add package Aspose.OCR`  
- Naskenované PDF (např. `invoice.pdf`) umístěné ve složce, na kterou můžete odkazovat  
- Základní znalost C# konzolových aplikací  

To je vše. Pokud už máte projekt, stačí přidat balíček a můžete začít.

## Krok 1: Nastavte projekt a přidejte Aspose.OCR

Nejprve vytvořte nový konzolový projekt (nebo použijte existující) a přidejte OCR knihovnu.

```csharp
// Create a new console app (run this in a terminal)
// > dotnet new console -n OcrPdfDemo
// > cd OcrPdfDemo
// > dotnet add package Aspose.OCR
```

Proč je tento krok důležitý: Aspose.OCR řeší těžkou práci analýzy obrazu, detekce rozvržení a rozpoznávání znaků. Bez ní byste museli skládati rasterizér, Tesseract engine a spoustu lepidlového kódu.

## Krok 2: Importujte jmenné prostory a připravte OCR engine

Otevřete `Program.cs` (nebo libovolný .cs soubor, který preferujete) a přidejte potřebné `using` direktivy.

```csharp
using System;
using Aspose.OCR;   // Core OCR classes
```

Vytvoření engine je přímočaré, ale také nakonfigurujeme několik možností, které zvyšují přesnost u typických skenů faktur.

```csharp
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // Enable automatic language detection (optional but handy)
    Language = Language.English,
    // Turn on deskew to correct rotated pages
    ImagePreprocessingOptions = new ImagePreprocessingOptions
    {
        Deskew = true,
        Binarization = true
    }
};
```

**Tip:** Pokud znáte jazyk dopředu, nastavte `Language` explicitně; proces se tak urychlí.

## Krok 3: Odkaz na váš PDF soubor

Zadejte absolutní nebo relativní cestu k PDF, které chcete zpracovat. Pro tento příklad předpokládáme, že soubor leží ve složce `Samples`.

```csharp
// Path to the PDF you want to OCR
string pdfFilePath = @"Samples/invoice.pdf";

// Verify the file exists early to avoid runtime surprises
if (!System.IO.File.Exists(pdfFilePath))
{
    Console.WriteLine($"File not found: {pdfFilePath}");
    return;
}
```

Kontrola existence souboru je malý krok, ale ušetří vás od kryptických výjimek později.

## Krok 4: Vyberte stránku (stránky) k přečtení

PDF může mít desítky stránek, ale často potřebujete jen konkrétní – například druhou stránku faktury, kde je uvedena celková částka. Metoda `RecognizePdf` vám umožní cílit na jednu stránku nebo na celý dokument.

```csharp
// Extract text from page 2 (page numbers are 1‑based)
int pageNumber = 2;

// The method returns an OcrResult containing the recognized text
OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);
```

Pokud chcete *převést PDF na text* pro celý dokument, jednoduše vynechte argument `pageNumber`:

```csharp
// OcrResult fullResult = ocrEngine.RecognizePdf(pdfFilePath);
```

## Krok 5: Zobrazte nebo uložte extrahovaný text

Po dokončení práce OCR engine můžete buď vytisknout text do konzole, zapsat ho do souboru `.txt`, nebo předat jinému systému (např. databázi).

```csharp
// Show the recognized text in the console
Console.WriteLine("=== OCR Result (Page {0}) ===", pageNumber);
Console.WriteLine(ocrResult.Text);

// Optionally, save to a .txt file
string outputPath = $"output_page{pageNumber}.txt";
System.IO.File.WriteAllText(outputPath, ocrResult.Text);
Console.WriteLine($"Text saved to {outputPath}");
```

**Proč je to důležité:** Uložením výstupu vytvoříte znovupoužitelný artefakt – ideální pro následnou analytiku nebo indexování vyhledávání.

## Kompletní funkční příklad

Sestavením všech částí získáte samostatný program, který můžete zkopírovat do `Program.cs` a spustit okamžitě.

```csharp
using System;
using Aspose.OCR;

namespace OcrPdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine with helpful options
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                ImagePreprocessingOptions = new ImagePreprocessingOptions
                {
                    Deskew = true,
                    Binarization = true
                }
            };

            // 2️⃣ Define the PDF path
            string pdfFilePath = @"Samples/invoice.pdf";
            if (!System.IO.File.Exists(pdfFilePath))
            {
                Console.WriteLine($"Error: File not found -> {pdfFilePath}");
                return;
            }

            // 3️⃣ Choose which page to OCR (change as needed)
            int pageNumber = 2; // read PDF page C# example

            // 4️⃣ Perform OCR on the selected page
            OcrResult ocrResult = ocrEngine.RecognizePdf(pdfFilePath, pageNumber);

            // 5️⃣ Output the result
            Console.WriteLine($"--- OCR Result for page {pageNumber} ---");
            Console.WriteLine(ocrResult.Text);

            // 6️⃣ Save to a text file for later use
            string outputPath = $"output_page{pageNumber}.txt";
            System.IO.File.WriteAllText(outputPath, ocrResult.Text);
            Console.WriteLine($"Extracted text saved to: {outputPath}");
        }
    }
}
```

### Očekávaný výstup

```
--- OCR Result for page 2 ---
Invoice #12345
Date: 2024‑11‑30
Total: $1,250.00
...
Extracted text saved to: output_page2.txt
```

Pokud PDF obsahuje čisté, vysoce rozlišené skeny, výstup bude téměř dokonalý. U méně kvalitních obrázků může být potřeba další předzpracování (např. zvýšení DPI nebo aplikace filtrů); `ImagePreprocessingOptions` z Aspose.OCR lze upravit podle těchto scénářů.

## Často kladené otázky a okrajové případy

### 1️⃣ Co když je PDF chráněno heslem?
Přetížení `RecognizePdf` v Aspose.OCR přijímá objekt `PdfLoadOptions`, kde můžete nastavit heslo:

```csharp
var loadOptions = new PdfLoadOptions { Password = "mySecret" };
OcrResult result = ocrEngine.RecognizePdf(pdfFilePath, pageNumber, loadOptions);
```

### 2️⃣ Můžu OCR provést na celý dokument najednou?
Ano – stačí zavolat `RecognizePdf(pdfFilePath)` bez specifikace čísla stránky. Metoda vrátí jediný `OcrResult` obsahující spojovaný text ze všech stránek.

### 3️⃣ Jak se to liší od „extrahování textu z PDF“ pomocí knihovny založené na textu?
Čisté extrahování textu (např. pomocí iTextSharp) funguje jen u PDF, které již obsahují vybratelný text. **Jak provést OCR PDF** je nutné, když je PDF ve skutečnosti sbírkou obrázků, jako jsou naskenované faktury. V takových případech OCR engine provádí optické rozpoznávání znaků a převádí obrázky na prohledávatelný text.

### 4️⃣ Jaký je výkon u velkých PDF?
Doba zpracování roste přibližně lineárně s počtem stránek a rozlišením obrazu. Pro hromadné úlohy zvažte:
- Spuštění OCR paralelně (`Parallel.ForEach`)  
- Snížení DPI před OCR (`Resolution = 150`)  
- Caching instance `OcrEngine` místo jejího opakovaného vytváření pro každý soubor

### 5️⃣ Existuje způsob, jak získat ohraničující rámečky každého slova?
`OcrResult` poskytuje kolekci objektů `OcrRegion`, z nichž každý obsahuje souřadnice. Můžete je iterovat a vytvářet prohledávatelné PDF nebo zvýraznit výsledky v UI.

```csharp
foreach (var region in ocrResult.Regions)
{
    Console.WriteLine($"{region.Text} – ({region.Bounds.X}, {region.Bounds.Y}, {region.Bounds.Width}, {region.Bounds.Height})");
}
```

## Tipy pro produkční nasazení

- **Zpracování chyb:** Obalte OCR volání do try/catch bloků, abyste zachytili výjimky specifické pro knihovnu.  
- **Logování:** Zaznamenávejte čísla stránek a časy zpracování; pomáhá to identifikovat problematické skeny.  
- **Správa paměti:** Uvolněte velké objekty `Bitmap`, pokud před OCR ručně převádíte PDF stránky na obrázky.  
- **Bezpečnost:** Nikdy neukládejte surová PDF na nezabezpečené disky; zvažte jejich streamování přímo do OCR engine.  

## Závěr

Nyní máte kompletní, end‑to‑end odpověď na **jak provést OCR PDF** pomocí C#. Tutoriál pokryl vše od instalace Aspose.OCR, výběru konkrétní stránky, extrakce textu až po řešení běžných okrajových případů. S tímto základem můžete *extrahovat text z PDF*, *převést PDF na text* a *číst PDF stránku v C#* pro jakýkoli dokumentační pipeline, který budujete.

Jste připraveni na další krok? Zkuste předat výstup OCR do full‑textového vyhledávače jako Lucene.NET, nebo generovat prohledávatelná PDF překrytím rozpoznaného textu na původní obrázky. Možnosti jsou neomezené a právě jste získali nástroje, jak je využít.

---

![how to ocr pdf example](image-placeholder.png "Illustration of OCR processing on a PDF page")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}