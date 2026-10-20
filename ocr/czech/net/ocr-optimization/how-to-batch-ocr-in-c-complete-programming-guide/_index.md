---
category: general
date: 2026-03-13
description: Jak rychle a spolehlivě provádět hromadné OCR a zároveň se naučit, jak
  extrahovat text z TIFF souborů pomocí Aspose.OCR. Postupujte podle tohoto návodu
  krok za krokem.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: cs
og_description: Naučte se provádět dávkové OCR v C# a extrahovat text z TIFF souborů
  pomocí Aspose.OCR. Tento průvodce pokrývá nastavení, kód a tipy na osvědčené postupy.
og_title: Jak provádět dávkové OCR v C# – Kompletní programovací průvodce
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Jak provádět dávkové OCR v C# – Kompletní programovací průvodce
url: /cs/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět dávkové OCR v C# – Kompletní programovací průvodce

Už jste se někdy zamysleli **jak provádět dávkové OCR** hromady naskenovaných faktur, aniž byste museli psát samostatný skript pro každý soubor? Nejste v tom sami. V mnoha reálných projektech není problém samotná přesnost OCR, ale obrovské množství obrázků – často TIFFů – které je třeba převést na prohledávatelný text.  

Tento tutoriál vám ukáže **jak provádět dávkové OCR** pomocí `BatchProcessor` z Aspose.OCR a zároveň vás naučí **extrahovat text z tiff** souborů v jednom čistém běhu. Na konci budete mít připravenou konzolovou aplikaci, která zpracuje celý adresář, využije volitelnou akceleraci GPU a uloží výsledky jako prostý text kamkoli potřebujete.

## Co budete potřebovat

- **.NET 6+** (nebo .NET Framework 4.7.2, pokud dáváte přednost klasickému runtime)  
- **Aspose.OCR for .NET** – můžete získat NuGet balíček pomocí `dotnet add package Aspose.OCR`.  
- Složka s **TIFF** obrázky, které chcete číst (v tutoriálu je použita složka `Invoices` jako příklad).  
- Volitelně: GPU, která podporuje DirectX 11 nebo CUDA, pokud chcete urychlit zpracování.  

Žádné extra služby, žádné cloudové klíče – jen lokální C# projekt a knihovna Aspose.

## Krok 1: Nastavte projekt a nainstalujte Aspose.OCR

Nejprve vytvořte konzolovou aplikaci.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Tip:** Pokud používáte Windows a plánujete využít akceleraci GPU, ujistěte se, že máte nainstalován nejnovější grafický ovladač. Jinak se příznak `UseGpu = true` automaticky vrátí na CPU.

## Krok 2: Vytvořte konfiguraci BatchProcessoru

Nyní nakonfigurujeme `BatchProcessor`. Toto je jádro **jak provádět dávkové OCR** – řeknete Aspose, jaký jazyk očekávat, které předzpracovatelské filtry použít a zda využít GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Proč tato nastavení?**  
- `Language = Language.English` říká enginu, aby použil model pro anglický jazyk, který je mnohem přesnější než obecný model.  
- `UseGpu` může zkrátit dobu zpracování na polovinu na slušném GPU, ale je v pořádku nechat jej `false`, pokud používáte notebook bez GPU.  
- Pipeline filtrů napodobuje to, co by udělal člověk: narovná stránku a odstraní šmouhy před předáním OCR enginu.

## Krok 3: Nastavte procesor na vaši složku s TIFF soubory

Další část **jak provádět dávkové OCR** je říci knihovně, kde se nacházejí zdrojové soubory. Zástupné znaky jsou podporovány, takže můžete najednou načíst všechny soubory `.tif`.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Hraniční případ:** Pokud mají vaše obrázky smíšené přípony (`.tiff`, `.tif`, `.png`), zavolejte `AddFolder` vícekrát nebo použijte `*.*` a filtrujte později v kódu.

## Krok 4: Zvolte, kam se uloží výsledky OCR

Možná se ptáte, „Kam se uloží extrahovaný text?“ To je třetí pilíř **jak provádět dávkové OCR** – definování výstupního umístění a formátu. Uložíme soubory s prostým textem vedle originálů.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Pokud potřebujete místo prostého textu JSON nebo XML, stačí vyměnit `OutputFormat.PlainText` za `OutputFormat.Json` nebo `OutputFormat.Xml`. Knihovna provede konverzi za vás.

## Krok 5: Spusťte dávkovou úlohu a nahlaste výsledky

Nakonec spusťte úlohu. Metoda `Execute` blokuje, dokud není každý soubor zpracován, poté můžete zkontrolovat `ProcessedCount` pro potvrzení úspěchu.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Očekávaný výstup

Když spustíte program, konzole vypíše něco jako:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

Ve složce `Output` najdete jeden `.txt` soubor pro každý zdrojový TIFF, pojmenovaný podle původního obrázku (např. `Invoice_001.txt`). Otevřete libovolný soubor a uvidíte surový OCR text – ideální pro napájení vyhledávacího indexu nebo následného datového extrakčního pipeline.

## Řešení běžných problémů

### 1. GPU není k dispozici

Pokud je `UseGpu = true`, ale nenajde se kompatibilní zařízení, Aspose tiše přejde na CPU. Pro explicitní zachycení můžete odchytit `DeviceNotFoundException`:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Soubory, které nejsou TIFF, ve stejné složce

Když máte smíšenou složku, filtrujte programově:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Velké soubory přesahující paměť

Pro obrovské vícestránkové TIFFy povolte streamování:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Pro tipy pro vyšší přesnost při **extrahování textu z tiff**

- **Rozlišení je důležité** – Cílem by mělo být 300 dpi nebo více. Pod tím může OCR engine vynechat znaky.  
- **Barva vs. odstíny šedi** – Před OCR převádějte barevné skeny na odstíny šedi; `DeskewFilter` to již pod kapotou provádí, ale můžete přidat `ColorDepthReductionFilter` pro vyšší rychlost.  
- **Post‑processing** – Po získání prostého textu spusťte kontrolu pravopisu nebo čištění pomocí regexu, abyste opravili běžné OCR nedostatky (např. “0” vs “O”).

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je celý program, který můžete zkompilovat a spustit. Stačí nahradit placeholder cesty vlastními adresáři.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Zkompilujte a spusťte:

```bash
dotnet run
```

Nyní byste měli mít úhlednou sadu `.txt` souborů – každý je výsledkem **extrahování textu z tiff** pomocí plně automatizovaného dávkového procesu.

## Závěr

Prošli jsme **jak provádět dávkové OCR** v C# od začátku do konce, pokrývajíc vše, co potřebujete k efektivnímu **extrahování textu z tiff** souborů. Hlavní body jsou:

1. Použijte `BatchProcessor` z Aspose.OCR, abyste se vyhnuli psaní opakujících se smyček.  
2. Využijte předzpracovatelské filtry (deskew, despeckle) pro vyšší přesnost.  
3. Povolit akceleraci GPU, pokud je to možné, ale vždy mít záložní CPU.  
4. Ukládejte výsledky do předvídatelné struktury složek, aby je následné úlohy mohly automaticky načíst.

Odtud můžete zkoumat:

- Vložení prostého textu do **vyhledávacího indexu** (např. Elasticsearch) pro zpřístupnění faktur k vyhledávání.  
- Převod výstupu na **JSON** a předání modelu strojového učení, který extrahuje položky.  
- Přidání **zpracování chyb** pro poškozené TIFFy nebo problémy s oprávněními.

Vyzkoušejte to,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}