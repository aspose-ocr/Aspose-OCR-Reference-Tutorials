---
category: general
date: 2026-03-21
description: Jak jednoduše provádět hromadné OCR v C# – naučte se extrahovat text
  z obrázků, převádět obrázky na text a ukládat OCR jako text s nastavením jazyka.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: cs
og_description: Jak provádět dávkové OCR v C# vám umožní extrahovat text z obrázků,
  převádět obrázky na text a ukládat OCR jako text při snadném nastavení jazyka OCR.
og_title: Jak provádět dávkové OCR v C# – rychlý průvodce
tags:
- OCR
- C#
- Aspose
title: Jak provádět dávkové OCR v C# – Rychle extrahovat text z obrázků
url: /cs/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Jak provádět hromadné OCR v C# – Rychlé získávání textu z obrázků

Už jste se někdy zamýšleli nad **tím, jak provádět hromadné OCR**, když máte stovky obrázků uložených ve složce? Nejste sami – vývojáři se neustále ptají, jak získat text z obrázků, aniž by museli psát smyčku pro každý soubor. Dobrou zprávou je, že Aspose.OCR vám poskytuje čistý, připravený na paralelní zpracování způsob, jak **převést obrázky na text** během několika řádků C#.

V tomto tutoriálu vás provedeme kompletním, připraveným příkladem, který ukazuje, jak **uložit OCR jako text**, vybrat správný jazyk a zvýšit paralelní zpracování pro rychlost. Na konci budete mít samostatné řešení, které můžete vložit do libovolného .NET projektu.

## Co budete potřebovat

- .NET 6 nebo novější (API funguje s .NET Core a .NET Framework)
- Aspose.OCR pro .NET (NuGet balíček `Aspose.OCR`)
- Složka s obrázky, které chcete zpracovat (PNG, JPEG, TIFF, atd.)
- Trochu zvědavosti na paralelní programování (volitelné, ale užitečné)

Žádné další služby, žádné cloudové klíče – jen čistý C# kód, který běží lokálně.

---

![pracovní postup hromadného OCR](placeholder.png){alt="diagram pracovního postupu hromadného OCR"}

## Krok 1: Nastavení projektu a instalace Aspose.OCR

Nejprve vytvořte konzolovou aplikaci (nebo použijte existující) a přidejte balíček Aspose.OCR:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

**Tip:** Pokud používáte Visual Studio, klikněte pravým tlačítkem na projekt → *Manage NuGet Packages* → vyhledejte *Aspose.OCR* a nainstalujte nejnovější stabilní verzi.

Tím získáte přístup k `OcrBatchProcessor`, `OcrEngineSettings` a výčtu `Language`.

## Krok 2: Definování vstupních a výstupních složek

Hromadný procesor potřebuje vědět, kde se nacházejí zdrojové obrázky a kam mají být zapsány extrahované textové soubory. Používejte absolutní nebo relativní cesty k kořeni projektu – jen se ujistěte, že složky existují před spuštěním kódu.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

**Proč je to důležité:** Pokud výstupní složka chybí, procesor vyhodí výjimku, což přeruší celé hromadné zpracování. Vytvoření složky předem zaručuje plynulý běh.

## Krok 3: Konfigurace nastavení OCR (včetně jazyka)

Zde **nastavujete jazyk OCR** pro celé hromadné zpracování. Aspose.OCR podporuje desítky jazyků; výchozí je angličtina, ale můžete přepnout na francouzštinu, španělštinu atd. změnou hodnoty výčtu `Language`.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Pokud budete potřebovat zpracovávat různé jazyky podle obrázku, můžete později přepsat toto nastavení pro jednotlivé soubory – více o tom později.

## Krok 4: Vytvoření objektu `OcrBatchProcessor`

Nyní vše spojíme. `OcrBatchProcessor` vám umožňuje zadat vstupní složku, výstupní složku, výstupní formát, paralelní možnosti a sdílená nastavení, která jsme právě vytvořili.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

**Proč paralelismus?** Když máte desítky nebo stovky obrázků, zpracování po jednom může být bolestivě pomalé. Nastavením `MaxDegreeOfParallelism` na 4 umožníte runtime použít čtyři CPU jádra současně, což dramaticky zkrátí celkový čas na typické pracovní stanici.

## Krok 5: Spuštění hromadné operace

Po nakonfigurování procesoru je spuštění jedním voláním metody. Knihovna automaticky zpracuje výčet souborů, OCR a zápis výsledků.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Když konzole vypíše *„Batch OCR completed.“*, najdete soubor `.txt` vedle každého původního obrázku ve složce `BatchResults`. Každý textový soubor obsahuje surové znaky extrahované ze svého zdrojového obrázku – přesně to, co potřebujete k **extrakci textu z obrázků** pro další zpracování.

### Očekávaný výstup

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Otevřete kterýkoli z těchto souborů a uvidíte čistý textový výstup obsahu obrázku.

## Krok 6: Ověření výsledků (volitelné)

Je dobrým zvykem dvakrát zkontrolovat několik souborů, aby bylo jisté, že OCR funguje podle očekávání. Rychlý způsob je přečíst první řádek každého vygenerovaného souboru a vypsat jej do konzole:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Pokud zaznamenáte poškozené znaky, zvažte změnu nastavení `Language` nebo úpravu kvality obrázku (např. zvýšení DPI, převod na odstíny šedi).

## Pokročilé varianty a okrajové případy

### 1. Přepis jazyka na úrovni souboru
Někdy hromadná sada obsahuje vícejazyčné dokumenty. Můžete prozkoumat název každého obrázku a při běhu přiřadit jazyk:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Různé výstupní formáty
Pokud potřebujete prohledávatelné PDF místo prostého textu, změňte `OutputFormat`:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Tím **převodíte obrázky na text** uvnitř PDF kontejneru a zachováte původní rozložení.

### 3. Zpracování velkých obrázků
Velmi vysoké rozlišení obrázků může spotřebovat hodně paměti. Pro udržení lehkosti procesu povolte down‑sampling obrázku:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Logování chyb
Procesor vyhodí výjimky pro nečitelné soubory. Zabalte `Execute` do try/catch a zaznamenejte problematické názvy souborů:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Kompletní funkční příklad

Spojením všeho dohromady zde máte kompletní, připravený program ke zkopírování a vložení:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Uložte tento soubor jako `Program.cs`, sestavte projekt a spusťte `dotnet run`. V konzoli uvidíte potvrzení o dokončení, následované krátkým náhledem extrahovaného textu.

---

## Závěr

Právě jsme probrali **jak provádět hromadné OCR** v C# pomocí Aspose.OCR, ukázali vám, jak **extrahovat text z obrázků**, **převést obrázky na text** a **uložit OCR jako text**, přičemž **nastavujete jazyk OCR** tak, aby odpovídal vašemu obsahu. Příklad je plně funkční, zahrnuje paralelní zpracování pro rychlost a nabízí rozšíření pro pokročilé scénáře, jako jsou přepisy jazyka na úrovni souboru nebo výstup do PDF.

Jste připraveni na další krok? Zkuste nahradit `OcrOutputFormat.PlainText` za `SearchablePdf` a uvidíte, jak snadno lze generovat prohledávatelné PDF. Nebo experimentujte s různými hodnotami `MaxDegreeOfParallelism`, abyste vytáhli poslední milisekundu z vícejádrového počítače.

Pokud narazíte na problémy, dvakrát zkontrolujte cesty ke složkám, ujistěte se, že jsou obrázky čitelné, a ověřte, že výčet jazyků odpovídá textu na vašich obrázcích. Šťastné programování a ať jsou vaše hromadné OCR rychlé a přesné!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}