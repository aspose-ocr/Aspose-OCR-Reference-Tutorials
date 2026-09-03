---
category: general
date: 2026-01-10
description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Naučte se, jak převést
  text naskenovaného dokumentu pomocí dávkového zpracování a uložit výsledky.
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Tento tutoriál ukazuje,
  jak převést text naskenovaného dokumentu pomocí dávkového zpracování.
og_title: Extrahovat text z obrázku v C# – kompletní průvodce Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extrahování textu z obrázku v C# – Kompletní průvodce Aspose OCR
url: /cs/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku – Kompletní průvodce Aspose OCR

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nebyli jste si jisti, kde začít? Nejste v tom sami; mnoho vývojářů narazí na tento problém při práci se skenovanými PDF, více‑stránkovými TIFFy nebo fotografiemi účtenek. Dobrou zprávou je, že s Aspose OCR můžete **převést text ze skenovaného dokumentu** během několika řádků C#.

V tomto tutoriálu si projdeme reálný scénář: vezmeme více‑stránkový TIFF, spustíme dávkové OCR na každé stránce a zapíšeme jeden textový soubor, který bude obsahovat obsah všech stránek. Na konci budete mít připravenou konzolovou aplikaci, pochopíte, proč je každý krok důležitý, a budete vědět, jak upravit tok pro okrajové případy, jako jsou obrázky chráněné heslem nebo vlastní jazykové balíčky.

## Prerequisites

- .NET 6.0 SDK nebo novější (kód funguje také s .NET Core a .NET Framework)  
- Visual Studio 2022 (nebo jakýkoli editor, který preferujete)  
- Licenční soubor Aspose OCR (nebo můžete použít režim bezplatného hodnocení)  
- Více‑stránkový soubor obrázku (např. `multipage.tif`) umístěný ve složce, na kterou můžete odkazovat  

Kromě `Aspose.OCR` nejsou vyžadovány žádné další balíčky NuGet; nainstalujeme jej v prvním kroku.

## Step 1 – Install Aspose  OCR and Set Up the Project

Abychom mohli začít, vytvořte nový konzolový projekt a přidejte knihovnu Aspose OCR.

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **Tip:** Pokud máte licenční soubor (`Aspose.OCR.lic`), zkopírujte jej do kořenového adresáře projektu. Knihovna jej automaticky načte za běhu.

Proč tento krok? Instalace balíčku vám poskytne přístup k `BatchProcessor`, `OcrEngine` a dalším užitečným třídám, které abstrahují nízkoúrovňové zpracování obrázků. Zároveň zajistí, že používáte nejnovější OCR algoritmy, které Aspose nabízí.

## Step 2 – Load the Multi‑Page Image with BatchProcessor

`BatchProcessor` je navržen právě pro tento scénář: iteraci přes každou stránku více‑stránkového obrázku, aniž byste museli soubory ručně rozdělovat.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

`BatchProcessor` načte všechny stránky do paměti a zpřístupní je přes `batchProcessor.Pages`. Každý objekt stránky zná své číslo (`ocrPage.Number`), které později použijeme pro přehledné nadpisy.

## Step 3 – Prepare a StringBuilder to Accumulate Results

Chceme jeden textový soubor, který bude obsahovat výstup OCR ze všech stránek, oddělený nadpisy. `StringBuilder` je nejefektivnější způsob, jak v cyklu spojovat řetězce.

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

Proč `StringBuilder`? Spojování řetězců pomocí `+` uvnitř smyčky by při každé iteraci alokovalo nový řetězec, což snižuje výkon – zejména u velkých dokumentů.

## Step 4 – Iterate Over Each Page, Run OCR, and Append Results

Nyní jádro tutoriálu: procházet každou stránku, rozpoznat text a uložit jej s označením stránky.

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**Proč nový `OcrEngine` pro každou stránku?** Někteří vývojáři znovu používají jediný engine a mění jeho vlastnost `Image`, ale to může zachovat nastavení jazyka nebo předchozí výsledky, což vede k subtilním chybám. Vytvoření čerstvého engine zaručuje čistý stav.

### Handling Common Edge Cases

- **Prázdné stránky:** Pokud stránka neobsahuje žádný rozpoznatelný text, `ocrEngine.Text` bude prázdný řetězec. Můžete vložit zástupný text, např. “(Žádný text nebyl detekován)”.
- **Výběr jazyka:** Ve výchozím nastavení Aspose OCR používá angličtinu. Pro zpracování němčiny nebo francouzštiny nastavte `ocrEngine.Language = Language.German;` před voláním `Recognize()`.
- **Tip pro výkon:** U obrovských TIFFů můžete povolit `ocrEngine.UseParallelProcessing = true;` a využít více jader.

## Step 5 – Write the Combined Output to a Text File

Nakonec uložíme nashromážděný řetězec na disk.

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

Výsledný soubor `multipage_result.txt` bude vypadat zhruba takto:

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

Nyní máte **extrahovaný text z obrázku** a efektivně **převést text ze skenovaného dokumentu** do vyhledávatelného, editovatelného formátu.

## Bonus – Visual Overview (Image Alt Text)

Níže je jednoduchý diagram toku procesu.  
*Alt text:* “Diagram ukazující, jak extrahovat text z obrázku pomocí dávkového zpracování Aspose OCR v C#”.

![OCR Flow Diagram](placeholder-image-url.png)

*(Pokud tento tutoriál publikujete na statické stránce, nahraďte zástupný obrázek skutečným SVG nebo PNG.)*

## Frequently Asked Questions

**Funguje to i s PDF soubory?**  
Ano, Aspose OCR může číst PDF stránky jako obrázky. Stačí nejprve převést PDF na obrázky, nebo použít `PdfDocument` z `Aspose.PDF` a předat rasterizovaný obrázek každé stránky do `OcrEngine`.

**Co když je můj TIFF chráněn heslem?**  
`BatchProcessor` přímo neřeší šifrování. Dešifrujte soubor pomocí knihovny jako `Aspose.Imaging` před předáním do OCR pipeline.

**Mohu místo prostého textu získat JSON?**  
Určitě. Nahraďte logiku `StringBuilder` serializátorem JSON (např. `System.Text.Json`) a uložte text každé stránky pod klíč `pageNumber`.

## Full Working Example

Zde je kompletní program, který můžete zkopírovat do `Program.cs`. Obsahuje všechny `using` direktivy, ošetření chyb a komentáře.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

Program spusťte pomocí:

```bash
dotnet run
```

Měli byste vidět zprávu v konzoli potvrzující úspěch a výstupní soubor bude obsahovat sloučené OCR výsledky.

## Conclusion

Právě jsme ukázali praktický způsob, jak **extrahovat text z obrázku** pomocí Aspose OCR, a převést libovolný více‑stránkový skenovaný soubor na prostý, vyhledávatelný text. Využitím `BatchProcessor` a čistého nastavení `OcrEngine` pro každou stránku můžete spolehlivě **převést text ze skenovaného dokumentu**, přičemž kód zůstane jednoduchý a udržovatelný.

Nebojte se experimentovat: vyzkoušejte různé jazyky, přepněte na výstup JSON nebo integrujte tuto logiku do webového API, které zpracovává nahrané soubory za běhu. Základní vzor zůstává stejný – načíst, rozpoznat, akumulovat a uložit.

Máte další otázky ohledně OCR, licencování Aspose nebo zpracování masivních dávkách dokumentů? Zanechte komentář níže nebo si prostudujte oficiální dokumentaci Aspose pro podrobnější informace. Šťastné kódování!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}