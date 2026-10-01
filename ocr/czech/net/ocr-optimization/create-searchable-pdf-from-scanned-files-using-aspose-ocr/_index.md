---
category: general
date: 2026-01-04
description: Rychle vytvořte prohledávatelný PDF ze skenovaného PDF. Naučte se, jak
  převést skenovaný PDF, přidat OCR do PDF a upravit kvalitu obrazu pomocí Aspose
  OCR v C#.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: cs
og_description: Vytvořte rychle prohledávatelný PDF ze skenovaného PDF. Postupujte
  podle tohoto podrobného návodu, jak převést skenovaný PDF, přidat OCR do PDF a upravit
  kvalitu obrazu.
og_title: Vytvořte prohledávatelný PDF ze skenovaných souborů pomocí Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Vytvořte prohledávatelný PDF ze skenovaných souborů pomocí Aspose OCR
url: /cs/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Vytvoření prohledávatelného PDF ze skenovaných souborů pomocí Aspose OCR

Už jste někdy potřebovali **vytvořit prohledávatelné PDF** ze zásoby skenovaných dokumentů, ale nevedeli jste, kde začít? Nejste v tom sami — mnoho vývojářů narazí na tuto překážku při budování pipeline pro správu dokumentů. Dobrá zpráva? S Aspose OCR můžete **převést skenované PDF**, přidat OCR a doladit kvalitu obrazu během několika řádků C#.

V tomto tutoriálu projdeme celý proces, od načtení skenovaného PDF až po uložení plně prohledávatelné verze. Na konci budete přesně vědět **jak použít OCR** s Aspose, proč je každé nastavení důležité a co upravit, když něco nefunguje podle plánu. Žádné vágní odkazy — jen kompletní, spustitelný příklad, který můžete dnes vložit do svého projektu.

## Požadavky

Než se pustíme do kódu, ujistěte se, že máte:

- .NET 6.0 nebo novější (kód funguje také s .NET Core a .NET Framework)
- Platnou licenci Aspose OCR (zdarma zkušební verze stačí pro testování)
- Vstupní PDF pojmenované `input.pdf` umístěné ve složce, kterou ovládáte
- Visual Studio 2022 nebo libovolný C# editor, který preferujete

To je vše. Pokud vám něco z toho není známé, zastavte se a nainstalujte chybějící součást — nic dalšího není potřeba.

## Krok 1: Inicializace OCR enginu a načtení skenovaného PDF  
**(Zde **přidáváme OCR do PDF** poprvé.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*Proč je tento krok potřeba?*  
`OcrEngine` je srdcem Aspose OCR. Načtení PDF říká enginu, kde hledat rastrové obrázky, které bude následně analyzovat. Pokud tento krok přeskočíte, není co převádět a následující kroky vyhodí výjimku.

> **Tip:** Pokud je vaše PDF chráněno heslem, použijte `ocrEngine.LoadPdf(path, password)`, abyste se vyhnuli chybě za běhu.

## Krok 2: Nastavení primárního a dalších jazyků  
**(Budeme **převádět skenované PDF** v angličtině, francouzštině a němčině.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*Proč záleží na jazyce?*  
Přesnost OCR závisí na očekávané znakové sadě. Deklarací angličtiny jako primárního jazyka a přidáním francouzštiny/němčiny může engine správně interpretovat diakritiku a speciální glyfy. Zapomenutí tohoto kroku často vede k nesmyslnému textu.

## Krok 3: Úprava kvality obrazu – doladění výstupu PDF  
**(Zde **upravujeme kvalitu obrazu** pro vyvážení velikosti souboru a čitelnosti.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*Proč ladit `ImageQuality`?*  
Vyšší hodnota (90‑100) zachovává ostrost, což je klíčové pro přesnost OCR, ale zároveň zvětšuje velikost souboru. Pokud archivujete miliony stránek, snižte ji na 70‑80 pro štíhlejší PDF bez výrazné ztráty čitelnosti.

## Krok 4: Uložení výsledku jako prohledávatelné PDF  
**(Nyní konečně **vytvoříme prohledávatelné PDF**, které můžete indexovat.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*Co se ve skutečnosti děje?*  
Aspose OCR extrahuje textovou vrstvu z každé stránky a vloží ji za původní obrázek. PDF zůstane vizuálně totožné, ale nyní můžete text vybírat, kopírovat a vyhledávat — obrovská výhoda pro následné workflow.

## Krok 5: Ověření výstupu (volitelné, ale doporučené)  
Je snadné předpokládat, že vše fungovalo, ale rychlá kontrola ušetří pozdější bolesti hlavy.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

Otevřete soubor, zkuste vybrat slovo nebo stiskněte `Ctrl+F` a zadejte frázi, o které víte, že je ve skenovaném originálu. Pokud je text vybíratelný, úspěšně jste **vytvořili prohledávatelné PDF**.

## Časté okrajové případy a jak je řešit  

| Situace | Proč k tomu dochází | Rychlé řešení |
|-----------|----------------|-----------|
| **Stránky s různým rozlišením** (některé 150 dpi, jiné 300 dpi) | Kvalita OCR se liší po stránkách, což vede k nerovnoměrné prohledávatelnosti. | Nastavte `ocrEngine.Config.Dpi = 300;` před načtením, aby se vynutilo up‑sampling, nebo předzpracujte pomocí `ImageProcessor` pro normalizaci DPI. |
| **Šifrované PDF** | Aspose OCR nemůže číst bez hesla. | Předávejte heslo metodě `LoadPdf` jak bylo ukázáno výše. |
| **Velká PDF (>500 MB)** | Spotřeba paměti prudce roste, což způsobí `OutOfMemoryException`. | Zpracovávejte dokument po částech: `ocrEngine.SplitPdfIntoPages();` pak OCR každé stránky zvlášť a výsledek sloučte. |
| **Ne‑latinské znaky** (např. cyrilice) | Jazyk nebyl přidán, takže se znaky zobrazí jako “?”. | Přidejte `Language.Russian` (nebo jiný potřebný jazyk) do `AdditionalLanguages`. |
| **Příliš nízká kvalita obrazu** | Text je rozmazaný, OCR selže. | Zvyšte `ImageQuality` nebo použijte `pdfOptions.Dpi = 300;` pro vložení obrázků vyššího rozlišení. |

## Kompletní, připravený příklad  

Níže je celý program, který můžete zkopírovat do nové konzolové aplikace. Obsahuje všechny kroky, ošetření chyb a komentáře pro přehlednost.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**Očekávaný výstup:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

Po otevření `output.pdf` byste měli být schopni vybrat a vyhledat jakýkoli text, který byl v původním skenu.

---

## Často kladené otázky (FAQ)

**Q: Funguje to i s PDF, které obsahují jak skenované obrázky, tak nativní text?**  
A: Rozhodně. Aspose OCR přidá skrytou textovou vrstvu jen tam, kde je potřeba, a existující text nechá nedotčený.

**Q: Můžu hromadně zpracovávat složku PDF?**  
A: Ano. Zabalte výše uvedený kód do smyčky `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` a podle toho upravte výstupní cestu.

**Q: Jak mohu dále snížit konečnou velikost PDF?**  
A: Snižte `ImageQuality` na 70‑80, povolte `Compress`, nebo použijte `pdfOptions.Dpi = 150` pro downsampling obrázků před vložením.

**Q: Existuje způsob, jak extrahovat OCR text bez vytváření PDF?**  
A: Zavolejte `ocrEngine.ExtractText();` po načtení PDF. Vrátí to řetězec prostého textu, který můžete uložit nebo indexovat.

---

## Závěr  

Právě jsme prošli **jak použít OCR** s Aspose k **vytvoření prohledávatelného PDF** ze skenovaného dokumentu, ukázali **jak převést skenované PDF**, demonstrovali **přidání OCR do PDF** a vysvětlili, jak **upravit kvalitu obrazu** pro optimální výsledek. Kompletní ukázkový kód je připravený ke spuštění a tabulka s řešením problémů vám pomůže pokračovat, i když se objeví neočekávané situace.

Co dál? Vyzkoušejte:

- Různé jazykové balíčky pro vícejazyčné archivy
- Vlastní předzpracování obrazu (odklon, odstranění šumu) pomocí `ImageProcessor`
- Integraci prohledávatelného PDF do SharePointu nebo ElasticSearch pipeline

Neváhejte zanechat komentář, pokud narazíte na problém nebo objevíte chytrý tip. Šťastné kódování a užívejte si okamžitě prohledávatelná PDF! 

![Vytvoření prohledávatelného PDF diagram ukazující OCR engine → jazyková konfigurace → možnosti uložení PDF → výstup prohledávatelného PDF](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}