---
category: general
date: 2026-02-27
description: Vytvořte prohledávatelný PDF ze skenovaného PDF během několika sekund
  pomocí Aspose OCR. Naučte se, jak převést skenovaný PDF, OCR převod PDF a snadno
  extrahovat text z PDF.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr convert pdf
- extract text from pdf
- convert image pdf
language: cs
og_description: Vytvořte okamžitě prohledávatelný PDF. Tento tutoriál ukazuje, jak
  převést naskenovaný PDF, provést OCR konverzi PDF a extrahovat text z PDF pomocí
  Aspose OCR.
og_title: Vytvořte prohledávatelný PDF – Rychlý průvodce Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Vytvořte prohledávatelný PDF ze skenovaných obrázků pomocí Aspose OCR
url: /cs/net/text-recognition/create-searchable-pdf-from-scanned-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF ze skenovaných obrázků pomocí Aspose OCR

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** z faktury, která existuje jen na papíře, ale nevěděli jste, kde začít? S Aspose OCR můžete **vytvořit prohledávatelné PDF** během několika řádků C#—bez externích služeb, bez ručního kopírování a vkládání.  

V tomto průvodci projdeme vše, co potřebujete k **převodu naskenovaných pdf** souborů na plně prohledávatelná PDF, vysvětlíme, proč je každý krok důležitý, a dokonce ukážeme, jak **extrahovat text z pdf**, pokud dáváte přednost surovým řetězcům před výstupem PDF. Na konci budete mít znovupoužitelný úryvek, který řeší běžný problém „PDF jen s obrázky“ a několik tipů pro okrajové případy.

![vytvořit prohledávatelné pdf pomocí Aspose OCR](image-placeholder.png "vytvořit prohledávatelné pdf pomocí Aspose OCR")

## Co budete potřebovat

- .NET 6.0 nebo novější (API funguje na .NET Core, .NET Framework a .NET 5+)
- Visual Studio 2022 (nebo jakýkoli editor, který chcete)
- Balíček NuGet Aspose OCR (`Aspose.OCR`) – nainstalujeme jej v prvním kroku
- Naskenovaný PDF soubor (pouze obrázek), který chcete převést na **prohledávatelné PDF**

To je vše—žádné další OCR enginy, žádné problémy s licencí pro zkušební provoz.  

Teď se ponořme.

## Krok 1: Instalace knihovny Aspose OCR (a rychlý tip)

Než spustíte jakýkoli kód, je třeba knihovnu odkazovat. Otevřete terminál ve složce projektu a spusťte:

```bash
dotnet add package Aspose.OCR
```

> **Tip:** Pokud používáte Package Manager ve Visual Studio, vyhledejte “Aspose.OCR” a klikněte na **Install**. Bezplatná zkušební verze funguje až pro 20 stránek, což je ideální pro testování.

Instalace balíčku vám poskytne přístup k `OcrEngine`, `OcrLanguage` a `OcrOutputFormat`—třem třídám, které použijeme k **ocr převodu pdf**.

## Krok 2: Konfigurace OCR enginu (Vytvoření prohledávatelného PDF – základní nastavení)

Engine potřebuje vědět, jaký jazyk má rozpoznávat a jaký výstupní formát očekáváte. V našem případě chceme PDF v angličtině, které je prohledávatelné.

```csharp
using Aspose.OCR;
using System;

// Step 2: Set up the OCR engine
var ocrEngine = new OcrEngine
{
    // Choose the language of the source document
    Language = OcrLanguage.English,

    // Tell Aspose we want a searchable PDF as the result
    OutputFormat = OcrOutputFormat.SearchablePdf
};
```

Proč nastavit `Language` explicitně? Přesnost OCR dramaticky klesá, když engine hádá jazyk, zejména u dokumentů obsahujících čísla nebo smíšené skripty. Připoutáním na angličtinu získáme čistší textové vrstvy, což následně zlepšuje krok **extrahovat text z pdf** později.

## Krok 3: Převod naskenovaného PDF na prohledávatelné PDF

Jakmile je engine připraven, nasměrujte jej na zdrojový soubor a určete, kam má výsledek zapsat. Toto jediné volání provede těžkou práci: rasterizuje každou stránku, spustí OCR a zapíše nové PDF s neviditelnou textovou vrstvou.

```csharp
// Step 3: Perform the conversion
ocrEngine.RecognizePdf(
    @"C:\Docs\invoice_scanned.pdf",   // input – image‑only PDF
    @"C:\Docs\invoice_searchable.pdf" // output – searchable PDF
);
```

Pokud zdrojové PDF obsahuje více stránek, Aspose OCR je zpracuje sekvenčně a zachová původní rozvržení. Výstupní soubor lze otevřít v libovolném prohlížeči PDF; všimnete si, že nyní můžete vybírat a vyhledávat slova, která byla dříve jen obrázky.

### Ověření výsledku (Extrahovat text z PDF)

Abyste si byli naprosto jisti, že převod byl úspěšný, můžete programově získat text:

```csharp
using Aspose.Pdf;           // Add Aspose.PDF if you also need text extraction
using System.Text;

// Load the newly created searchable PDF
var doc = new Document(@"C:\Docs\invoice_searchable.pdf");
var sb = new StringBuilder();

foreach (Page page in doc.Pages)
{
    // Extract the hidden text layer
    sb.Append(page.Text);
}

Console.WriteLine("Extracted text:\n" + sb.ToString());
```

Tento úryvek ukazuje, jak můžete **extrahovat text z pdf** po kroku OCR, což je užitečné pro indexování nebo předání obsahu do vyhledávače. Všimněte si, že pro tuto část potřebujete samostatný balíček `Aspose.PDF`; jedná se o lehký doplněk.

## Krok 4: Řešení běžných okrajových případů při **převodu PDF s obrázky**

Zatímco základní tok funguje pro většinu PDF, soubory v reálném světě mohou přinést nečekané situace:

| Situace | Proč se to děje | Jak to řešit |
|-----------|----------------|------------------|
| **Otočené stránky** | Skenery někdy automaticky otočí stránky o 90°. | Nastavte `ocrEngine.RotatePages = true` před voláním `RecognizePdf`. |
| **Smíšené jazyky** | Faktury mohou obsahovat francouzské nebo německé výrazy. | Použijte `OcrLanguage.Multilingual` nebo kombinujte více jazyků pomocí `|` (např. `OcrLanguage.English | OcrLanguage.French`). |
| **Velké soubory (> 100 stránek)** | Limity bezplatné zkušební verze mohou zastavit zpracování uprostřed souboru. | Zakupte licenci nebo rozdělte PDF na části pomocí `Aspose.Pdf` před OCR. |
| **Nízké rozlišení skenů** | Text se rozmazává, přesnost OCR klesá. | Zvyšte DPI pomocí `ocrEngine.ImageResolution = 300` (výchozí je 200). |

Řešení těchto scénářů zajišťuje, že váš **ocr převod pdf** pipeline zůstane v produkci robustní.

## Krok 5: Automatizace celého procesu (zabalit do metody)

Pokud budujete službu pro zpracování faktur, pravděpodobně budete chtít znovupoužitelnou metodu. Zde je kompaktní verze, která přijímá vstupní a výstupní cesty, řeší otočení a vrací extrahovaný text.

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Text;

public static class PdfSearchableHelper
{
    /// <summary>
    /// Converts an image‑only PDF to a searchable PDF and returns the hidden text.
    /// </summary>
    /// <param name="inputPath">Path to the scanned PDF.</param>
    /// <param name="outputPath">Path where the searchable PDF will be saved.</param>
    /// <returns>All extracted text as a single string.</returns>
    public static string ConvertAndExtract(string inputPath, string outputPath)
    {
        // 1️⃣ Initialize OCR engine
        var ocr = new OcrEngine
        {
            Language = OcrLanguage.English,
            OutputFormat = OcrOutputFormat.SearchablePdf,
            RotatePages = true,            // fixes rotated scans automatically
            ImageResolution = 300          // improve accuracy on low‑res scans
        };

        // 2️⃣ Perform conversion
        ocr.RecognizePdf(inputPath, outputPath);

        // 3️⃣ Load result and pull out hidden text
        var doc = new Document(outputPath);
        var sb = new StringBuilder();

        foreach (Page page in doc.Pages)
            sb.Append(page.Text);

        return sb.ToString();
    }
}
```

Nyní můžete zavolat:

```csharp
string extracted = PdfSearchableHelper.ConvertAndExtract(
    @"C:\Docs\contract_scanned.pdf",
    @"C:\Docs\contract_searchable.pdf");

Console.WriteLine("OCR completed. Extracted text length: " + extracted.Length);
```

Jedná se o kompletní workflow **převod PDF s obrázky** → **prohledávatelné PDF**, vše zabaleno do jediné metody, kterou můžete vložit do libovolné služby ASP.NET Core nebo konzolové aplikace.

## Často kladené otázky (FAQ)

**Q: Funguje to na macOS/Linux?**  
A: Rozhodně. Runtime .NET 6 a Aspose OCR jsou multiplatformní, takže stejný kód běží na Windows, macOS i v Linuxových kontejnerech.

**Q: Co když potřebuji jen text a nezajímá mě prohledávatelné PDF?**  
A: Přeskočte krok `OutputFormat` a nastavte `OutputFormat = OcrOutputFormat.Text`. Engine přímo vrátí prostý text.

**Q: Můžu zachovat metadata původního PDF?**  
A: Ano. Po převodu můžete metadata ze zdrojového objektu `Document` zkopírovat do nového pomocí `doc.Info.Title`, `doc.Info.Author` atd.

**Q: Existuje limit na počet stránek?**  
A: Bezplatná zkušební verze omezuje na 20 stránek na dokument. Plná licence toto omezení odstraňuje.

## Závěr

Nyní víte, jak **vytvořit prohledávatelné PDF**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}