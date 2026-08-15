---
category: general
date: 2026-04-29
description: Hromadně OCR obrázky rychle pomocí Aspose OCR v C#. Naučte se, jak extrahovat
  text z jpg souborů, číst text ze skenů a zpracovávat seznam obrázků paralelně.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: cs
og_description: Hromadně rychle provádějte OCR obrázků pomocí Aspose OCR. Tento průvodce
  ukazuje, jak extrahovat text z JPG, číst text ze skenů a paralelně zpracovávat seznam
  obrázků.
og_title: Dávkové OCR obrázků v C# – Paralelní OCR JPG skenů
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Dávkové OCR obrázků v C# – Paralelní OCR JPG skenů
url: /cs/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Dávkové OCR obrázků v C# – Paralelní OCR JPG skenů

Už jste někdy potřebovali **batch OCR images**, ale nebyli jste si jisti, jak rozšířit práci na více souborů? Nejste sami – vývojáři často narazí na problém, když se snaží číst text ze skenů po jednom. Dobrou zprávou je, že s Aspose OCR můžete **extract text from jpg** soubory, **read text from scans**, a **process image list** položky paralelně pomocí několika řádků C#.

V tomto tutoriálu projdeme kompletním, připraveným příkladem, který přesně ukazuje, jak to udělat. Na konci budete mít samostatnou konzolovou aplikaci, která rozpozná složku s JPEG skeny, vytiskne text každé stránky a řekne vám, jak dlouho každá operace trvala. Žádná externí dokumentace ke sledování, žádné poloviční úryvky kódu – jen kompletní řešení, které můžete vložit do Visual Studia a spustit.

## Co budete potřebovat

- **.NET 6.0** nebo novější (kód se také kompiluje na .NET Framework 4.6+)
- **Aspose.OCR** NuGet balíček (`Install-Package Aspose.OCR`)
- Několik JPG nebo skenovaných obrázkových souborů, které chcete zpracovat
- Jakékoli IDE, které máte rádi; používám Visual Studio 2022, ale VS Code také funguje

To je vše. Pokud už máte NuGet balíček, můžete začít.

## Krok 1 – Inicializace OCR enginu (Batch OCR Images Setup)

Prvním krokem je vytvořit instanci `OcrEngine` a nastavit jazyk, který má hledat. Ve většině případů stačí angličtina, ale můžete vyměnit `OcrLanguage.English` za jakýkoli podporovaný jazyk.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Proč je to důležité:* Inicializace enginu jednou a jeho opětovné používání napříč všemi obrázky je mnohem efektivnější než vytváření nové instance pro každý soubor. Také to umožňuje Aspose sdílet interní zdroje, což je nezbytné pro **parallel OCR processing**.

## Krok 2 – Vytvoření seznamu obrázků (Process Image List)

Dále definujeme kolekci cest k souborům, které chceme předat dávkovému rozpoznávači. Tento seznam můžete vytvořit dynamicky pomocí `Directory.GetFiles`, ale pro přehlednost několik položek napíšeme přímo.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Tip:* Pokud máte tisíce skenů, zvažte použití `Directory.EnumerateFiles` s filtrem jako `*.jpg`, abyste se vyhnuli načítání celého seznamu najednou do paměti.

## Krok 3 – Spuštění dávkového rozpoznání (Parallel OCR Processing)

Nyní přichází jádro celého procesu: volání `BatchRecognize`. Metoda přijímá argument `maxDegreeOfParallelism`, který určuje, kolik vláken Aspose spustí. Ve výchozím nastavení používá čtyři vlákna, ale můžete jej zvýšit, pokud má váš procesor více jader.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*Co se děje pod kapotou?* Aspose rozdělí kolekci `imagePaths` na úseky, předá každý úsek samostatnému vláknu a agreguje výsledky. To je nejefektivnější způsob, jak **extract text from jpg** soubory, když máte **process image list**, kterou lze zpracovat souběžně.

## Krok 4 – Zobrazení výsledků (Read Text from Scans)

Nakonec projdeme kolekci `recognitionResults` a vytiskneme text každého souboru a dobu zpracování. Objekt `OcrResult` také poskytuje název zdrojového souboru, což pomáhá při logování nebo ukládání výstupu.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Očekávaný výstup (příklad):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Všimněte si, že každý blok uvádí název souboru, jak dlouho OCR trvalo, a extrahovaný text. To je přesně ta informace, kterou potřebujete při **reading text from scans** v produkčním pipeline.

## Řešení běžných okrajových případů

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **Missing file** | `FileNotFoundException` vyvolá uvnitř `BatchRecognize` | Ověřte cesty pomocí `File.Exists` před přidáním do `imagePaths`. |
| **Unsupported format** | Aspose podporuje pouze rastrové obrázky (JPG, PNG, BMP, TIFF). | Převést PDF na obrázky nejprve (použijte Aspose.PDF) nebo tyto soubory přeskočit. |
| **Memory pressure** | Velmi velké obrázky mohou při běhu mnoha vláken vyčerpat RAM. | Snižte `maxDegreeOfParallelism` nebo před OCR změňte velikost obrázků. |
| **Non‑English text** | Nastavený jazyk na angličtinu bude postrádat jiné skripty. | Změňte `Language = OcrLanguage.French` (nebo kombinaci více jazyků). |

Tyto tipy udržují váš dávkový úkol robustní, zejména když **processing an image list** pochází od uživatelských nahrávek nebo skenovaného archivu.

## Pro tip – Ladění paralelismu

Pokud spustíte na 8‑jádrovém stroji, zvyšte paralelismus na 6 nebo 8 a sledujte zlepšení rychlosti. Pamatujte však, že každé vlákno také spotřebovává paměť pro bitmapu. Dobré pravidlo:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

Vložte `maxThreads` do `BatchRecognize` pro dynamickou, stroj‑závislou konfiguraci.

## Kompletní funkční příklad (připravený ke kopírování a vložení)

Níže je kompletní program připravený ke kompilaci. Stačí nahradit `YOUR_DIRECTORY` cestou, kde jsou vaše JPG skeny.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Poznámka:** Řádek `using System.IO;` je vyžadován pro pomocníka `Directory`. Kód vytiskne přátelskou zprávu, pokud nejsou nalezeny žádné JPG soubory, čímž zabrání tichému selhání.

## Závěr

Právě jsme předvedli čistý workflow **batch OCR images**, který **extracts text from jpg** soubory, **reads text from scans**, a efektivně **processes an image list** pomocí **parallel OCR processing**. Kompletní spustitelný příklad ukazuje přesně, jak nastavit engine, předat mu kolekci souborů a zpracovat výsledky – vše při zachování kontroly nad využitím paměti a počtem vláken.

Jste připraveni na další krok? Zkuste změnit jazyk na francouzštinu, přidejte konverzi PDF‑na‑obrázek nebo uložte OCR text do databáze. Vzor zůstává stejný: inicializovat jednou, předat seznam a nechat Aspose provést těžkou práci paralelně.

Máte otázky nebo chcete sdílet vlastní úpravy? Zanechte komentář níže a šťastné programování!

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}