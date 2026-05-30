---
category: general
date: 2026-04-26
description: Jak rychle provést dávkové OCR PNG obrázků. Naučte se extrahovat text
  z PNG, převádět obrázky na text, zapisovat rozpoznaný text a číst adresář PNG pomocí
  Aspose OCR.
draft: false
keywords:
- how to batch OCR
- extract text from png
- convert images to text
- write recognized text
- read png directory
language: cs
og_description: Jak dávkově provádět OCR PNG obrázků v C# s Aspose OCR. Tento průvodce
  ukazuje, jak extrahovat text z PNG, převést obrázky na text a efektivně zapisovat
  rozpoznaný text.
og_title: Jak dávkově provádět OCR PNG obrázků v C# – krok za krokem
tags:
- OCR
- C#
- Aspose
title: Jak hromadně provádět OCR PNG obrázků v C# – Kompletní průvodce
url: /cs/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak dávkově OCR PNG obrázky v C# – Kompletní průvodce

Už jste se někdy zamýšleli **jak dávkově OCR** celou složku PNG souborů, aniž byste museli psát samostatný program pro každý obrázek? Nejste jediní, kdo se potýká s desítkami snímků obrazovky, naskenovaných účtenek nebo grafiky, které je potřeba převést na prohledávatelný text. V tomto tutoriálu si projdeme praktické řešení, které **extrahuje text z PNG**, **převádí obrázky na text** a **zapíše rozpoznaný text** do jednotlivých souborů – a to vše při automatickém čtení adresáře s PNG soubory.

Na konci tohoto průvodce budete mít připravenou spustitelnou C# konzolovou aplikaci, která zpracuje libovolný počet obrázků najednou. Žádné další skripty, žádné ruční kopírování a vkládání – jen čistý kód, který za vás udělá těžkou práci.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód funguje také na .NET Framework).  
- **Aspose.OCR for .NET** NuGet balíček (zdarma zkušební verze stačí pro testování).  
- Složku s několika *.png* soubory, které chcete OCRovat.  
- Visual Studio 2022 nebo jakékoli jiné C# IDE dle vašeho výběru.

Pokud máte vše připravené, můžeme rovnou přistoupit k implementaci.

## Krok 1 – Připravte vstupní a výstupní složky *(Read PNG Directory)*

Prvním krokem je nasměrovat program na složku, která obsahuje obrázky, a rozhodnout, kam se uloží výsledné *.txt* soubory. Použití `Directory.GetFiles` nám poskytne čistý výčet všech PNG souborů v adresáři.

```csharp
using System;
using System.Collections.Generic;
using System.IO;

// Define where the source PNGs are and where the OCR results will be saved
string inputFolder = @"C:\MyProject\BatchImages";   // <-- change to your path
string outputFolder = @"C:\MyProject\BatchOutput";

// Ensure the output folder exists; create it if it doesn’t
if (!Directory.Exists(outputFolder))
{
    Directory.CreateDirectory(outputFolder);
}

// Grab every *.png* file – this is the “read png directory” part
IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
```

**Proč je to důležité:**  
- Použití masky (`*.png`) zaručuje, že zpracujeme jen soubory s obrázky a ignorujeme ostatní dokumenty.  
- Vytvoření výstupní složky za běhu zabraňuje pozdější výjimce `DirectoryNotFoundException`.

> **Tip:** Pokud potřebujete podporovat i jiné formáty (JPEG, BMP), stačí rozšířit vyhledávací vzor nebo zavolat `Directory.EnumerateFiles` s více příponami.

## Krok 2 – Inicializujte OCR engine *(Convert Images to Text)*

Aspose.OCR nabízí dva typy engine: CPU‑based `OcrEngine` a GPU‑akcelerovaný `GpuOcrEngine`. Pro většinu dávkových úloh je CPU engine naprosto dostačující, ale můžete změnit třídu, pokud máte výkonnou GPU.

```csharp
using Aspose.OCR;

// Initialise the OCR engine – CPU version
OcrEngine ocrEngine = new OcrEngine();   // Use new GpuOcrEngine() for GPU acceleration

// Set the language to Latin (covers English, French, Spanish, etc.)
ocrEngine.Language = Language.Latin;
```

**Proč je to důležité:**  
- Nastavení jazyka výrazně zvyšuje přesnost, protože engine ví, jakou znakovou sadu má očekávat.  
- Přepnutí na `GpuOcrEngine` je změna jedné řádky, pokud narazíte na výkonové limity u velkých dávek.

## Krok 3 – Vytvořte Batch Recogniser

Aspose poskytuje pohodlný `BatchRecognizer`, který přijímá výčet cest k souborům a postupně vrací výsledky. Tím se vyhneme načítání všech obrázků najednou – klíčová výhoda u velkých složek.

```csharp
// Build a batch recogniser that will use the previously configured engine
BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);
```

**Proč je to důležité:**  
- Batch recogniser zapouzdřuje logiku smyčky, takže se můžeme soustředit na to, co uděláme s každým výsledkem, místo toho, jak bezpečně iterovat.

## Krok 4 – Proveďte OCR na všech obrázcích a zapište výstup *(Write Recognized Text)*

Nyní skutečně spustíme OCR. Metoda `Recognize` vrací `IEnumerable<RecognitionResult>`, kde každý výsledek obsahuje extrahovaný text a další metadata.

```csharp
// Perform OCR on the entire collection of PNG files
IEnumerable<RecognitionResult> recognitionResults = batchRecognizer.Recognize(inputImageFiles);

// Write each recognised text to a separate *.txt* file
int fileIndex = 0;
foreach (RecognitionResult result in recognitionResults)
{
    // Build a unique output filename – out_0.txt, out_1.txt, …
    string outputPath = Path.Combine(outputFolder, $"out_{fileIndex++}.txt");

    // Save the plain text to disk
    File.WriteAllText(outputPath, result.Text);
}
```

**Proč je to důležité:**  
- Použití `File.WriteAllText` zajistí, že text bude uložen s kódováním UTF‑8, což zachová speciální znaky.  
- Postupné pojmenování (`out_0.txt`, `out_1.txt`) odpovídá pořadí zpracování, což je užitečné při ladění.

> **Okrajový případ:** Pokud se některý obrázek nepodaří OCRovat (např. poškozený soubor), `RecognitionResult.Text` bude prázdný. Do smyčky můžete přidat jednoduchou kontrolu a zaznamenat selhání:

```csharp
if (string.IsNullOrWhiteSpace(result.Text))
{
    Console.WriteLine($"Warning: No text extracted from {inputImageFiles.ElementAt(fileIndex - 1)}");
}
```

## Krok 5 – Sestavte vše dohromady – Kompletní funkční příklad

Níže najdete kompletní program, který můžete zkopírovat do nového konzolového projektu. Obsahuje `using` direktivy, validaci složek a malé uživatelské rozhraní v konzoli, abyste věděli, kdy dávka skončila.

```csharp
// ---------------------------------------------------------------
// Batch OCR for PNG files using Aspose.OCR
// ---------------------------------------------------------------
using System;
using System.Collections.Generic;
using System.IO;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // 1️⃣ Define input & output directories
        string inputFolder = @"C:\MyProject\BatchImages";   // <-- adjust
        string outputFolder = @"C:\MyProject\BatchOutput";

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"Error: Input folder does not exist -> {inputFolder}");
            return;
        }

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ Gather all PNG files
        IEnumerable<string> inputImageFiles = Directory.GetFiles(inputFolder, "*.png");
        Console.WriteLine($"Found {inputImageFiles?.Count() ?? 0} PNG files to process.");

        // 3️⃣ Initialise OCR engine (CPU) and set language
        OcrEngine ocrEngine = new OcrEngine();   // Swap with GpuOcrEngine() if needed
        ocrEngine.Language = Language.Latin;

        // 4️⃣ Create batch recogniser
        BatchRecognizer batchRecognizer = new BatchRecognizer(ocrEngine);

        // 5️⃣ Run OCR and write results
        IEnumerable<RecognitionResult> results = batchRecognizer.Recognize(inputImageFiles);
        int index = 0;
        foreach (RecognitionResult result in results)
        {
            string outPath = Path.Combine(outputFolder, $"out_{index++}.txt");
            File.WriteAllText(outPath, result.Text);
        }

        Console.WriteLine($"✅ OCR complete! Text files saved to {outputFolder}");
    }
}
```

**Očekávaný výstup:**  
Po spuštění program vypíše něco podobného:

```
Found 12 PNG files to process.
✅ OCR complete! Text files saved to C:\MyProject\BatchOutput
```

A ve výstupní složce uvidíte `out_0.txt` … `out_11.txt`, přičemž každý soubor obsahuje čistý text odpovídajícího obrázku.

## Často kladené otázky a tipy

| Otázka | Odpověď |
|----------|--------|
| *Mohu OCRovat i podadresáře?* | Ano – nahraďte `Directory.GetFiles` voláním `Directory.EnumerateFiles(inputFolder, "*.png", SearchOption.AllDirectories)`. |
| *Co když potřebuji jiný jazyk?* | Nastavte `ocrEngine.Language = Language.Spanish;` (nebo libovolný podporovaný enum). |
| *Jak zvládnout obrovské dávky (tisíce souborů)?* | Zvažte zpracování po částech nebo použití `Parallel.ForEach` s omezeným počtem paralelních úloh, aby nedošlo k vyčerpání paměti. |
| *Je výstup vždy UTF‑8?* | `File.WriteAllText` ve výchozím nastavení používá UTF‑8 bez BOM, což funguje pro většinu latinských jazyků. Pro asijské skripty můžete explicitně nastavit `Encoding.UTF8`. |
| *Mohu získat skóre spolehlivosti?* | `RecognitionResult` obsahuje `Confidence` – můžete jej zaznamenat spolu s textem pro kontrolu kvality. |

## Vizuální přehled *(How to Batch OCR – Diagram)*

![Jak dávkově OCR workflow diagram ukazující vstupní složku → OCR engine → batch recogniser → výstupní txt soubory](https://example.com/diagram-how-to-batch-ocr.png "Jak dávkově OCR")

*Alt text obsahuje hlavní klíčové slovo, splňující SEO požadavky na obrázek.*

## Závěr

Právě jsme prošli **jak dávkově OCR** adresář PNG souborů pomocí Aspose.OCR, od načtení složky až po zápis každého rozpoznaného textového souboru. Řešení je zcela samostatné, funguje na jakémkoli moderním .NET runtime a lze jej rozšířit o GPU akceleraci, podporu více jazyků nebo paralelní zpracování.

Jste připraveni na další krok? Vyzkoušejte výměnu `Language.Latin` za jiný jazyk, nebo integrujte výstup do vyhledávacího indexu, aby se vaše dokumenty okamžitě staly prohledávatelnými. Možnosti jsou neomezené, jakmile zvládnete dávkové OCR.

Šťastné programování a dejte vědět v komentářích, pokud narazíte na nějaké problémy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}