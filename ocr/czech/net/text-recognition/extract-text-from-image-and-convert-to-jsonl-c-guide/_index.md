---
category: general
date: 2026-01-02
description: Extrahujte text z obrázku pomocí Aspose OCR v C#. Naučte se, jak rychle
  a spolehlivě převést obrázek do formátu JSONL.
draft: false
keywords:
- extract text from image
- convert image to jsonl
language: cs
og_description: Extrahujte text z obrázku pomocí Aspose OCR a převeďte jej do formátu
  JSONL. Kompletní krok‑za‑krokem C# tutoriál pro vývojáře.
og_title: Extrahovat text z obrázku – převést do JSONL v C#
tags:
- C#
- OCR
- Aspose
- JSONL
title: Extrahujte text z obrázku a převěďte jej do JSONL – Průvodce C#
url: /cs/net/text-recognition/extract-text-from-image-and-convert-to-jsonl-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahování textu z obrázku a převod do JSONL – Kompletní C# tutoriál

Už jste někdy potřebovali **extrahovat text z obrázku**, ale nebyli jste si jisti, která knihovna vám poskytne čistý, strukturovaný výstup? Nejste v tom sami. V mnoha projektech zpracování účtenek nebo digitalizace dokumentů je úzkým místem převod bitmapy na prohledávatelný text *a* strojově čitelný formát.

Dobrá zpráva? S Aspose OCR můžete **extrahovat text z obrázku** a pomocí několika řádků kódu **převést obrázek do JSONL** pro následnou analytiku. Tento průvodce vás provede celým procesem, od načtení PNG až po zápis souboru JSON‑Lines, který lze streamovat do datové pipeline.

> **Tip:** Pokud již používáte .NET 6 nebo novější, stejný kód funguje bez jakékoli další konfigurace.

## Požadavky — Co budete potřebovat

- **.NET 6 SDK** (or any recent .NET version)
- **Aspose.OCR** NuGet package  
  ```bash
  dotnet add package Aspose.OCR
  ```
- **Newtonsoft.Json** for serialization  
  ```bash
  dotnet add package Newtonsoft.Json
  ```
- Ukázkový obrázek (např. `receipt.png`) umístěný ve složce, na kterou můžete odkazovat.
- IDE nebo editor dle vašeho výběru — Visual Studio, VS Code, Rider atd.

Žádné složité nastavení, žádné externí služby, jen pár NuGet balíčků.

![Extrahování textu z obrázku pomocí C# s Aspose OCR](https://example.com/assets/ocr-sample.png)

*Alt text: extrahování textu z obrázku pomocí C# s Aspose OCR*

## Krok 1: Načtěte obrázek, který chcete zpracovat  

První věc, kterou uděláte, když chcete **extrahovat text z obrázku**, je předat OCR enginu bitmapu. Použití `System.Drawing.Bitmap` je jednoduché a funguje pro většinu rastrových formátů.

```csharp
using System.Drawing;

// Adjust the path to where your receipt.png lives
string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
Bitmap receiptImage = new Bitmap(imagePath);
```

> **Proč je to důležité:** Načtení obrázku jako `Bitmap` poskytuje OCR enginu přímý přístup k pixelům, což zlepšuje rychlost rozpoznávání a přesnost ve srovnání se streamováním surových bajtů.

## Krok 2: Nakonfigurujte Aspose OCR pro výstup JSON‑Lines  

Aspose OCR vám umožňuje nastavit jazyk, výstupní formát a několik optimalizací výkonu. Zde požadujeme **JSON‑Lines** (jeden JSON objekt na řádek), protože je to ideální pro následné zpracování řádek po řádku.

```csharp
using Aspose.OCR;

// Create the engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine we’re dealing with English text
RecognitionOptions options = new RecognitionOptions
{
    Language = Language.English,
    OutputFormat = OutputFormat.JsonLines   // This is the key for converting image to JSONL
};
```

> **Tip:** Pokud potřebujete vícejazyčné účtenky, nastavte `Language = Language.Multilingual` nebo předávejte pole hodnot `Language`.

## Krok 3: Spusťte OCR a zachyťte výsledek  

Nyní skutečně **extrahujeme text z obrázku**. Metoda `Recognize` vrací objekt `OcrResult`, který obsahuje kolekci objektů `OcrLine`, z nichž každý představuje řádek rozpoznaného textu spolu s ohraničujícím rámečkem.

```csharp
// Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);
```

V tomto okamžiku `ocrResult.Lines` obsahuje vše, co potřebujete — surový text, skóre důvěry a souřadnice.

## Krok 4: Serializujte řádky do JSON‑Lines  

Převedeme kolekci na pěkně odsazený JSON řetězec. I když jsou JSON‑Lines obvykle kompaktní, přidání odsazení usnadňuje kontrolu souboru během vývoje.

```csharp
using Newtonsoft.Json;

// Serialize each line as a separate JSON object
string jsonLines = JsonConvert.SerializeObject(
    ocrResult.Lines,
    Formatting.Indented
);
```

Výsledná proměnná `jsonLines` vypadá zhruba takto (zkráceno pro stručnost):

```json
{
  "Text": "Store XYZ",
  "Confidence": 0.98,
  "BoundingBox": { "X": 10, "Y": 15, "Width": 120, "Height": 20 }
}
{
  "Text": "Date: 01/01/2026",
  "Confidence": 0.95,
  "BoundingBox": { "X": 10, "Y": 45, "Width": 180, "Height": 20 }
}
```

Každý řádek končí znakem nového řádku, což vám poskytuje skutečný **JSONL** (JSON‑Lines) soubor.

## Krok 5: Zapište JSON‑Lines na disk  

Nakonec výstup uložíme, aby jej ostatní služby — jako Spark, Logstash nebo jednoduchý Bash skript — mohly načítat řádek po řádku.

```csharp
using System.IO;

// Choose a destination file
string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
File.WriteAllText(outputPath, jsonLines);
```

Když otevřete `receipt.jsonl`, uvidíte jeden JSON objekt na řádek, připravený ke streamování.

## Krok 6: Ověřte export  

Rychlá kontrola vám ušetří hodiny ladění později. Přečtěme si první několik řádků zpět a vypišme je do konzole.

```csharp
Console.WriteLine("First three lines of the JSONL output:");
foreach (var line in File.ReadLines(outputPath).Take(3))
{
    Console.WriteLine(line);
}
```

Typický výstup v konzoli:

```
First three lines of the JSONL output:
{"Text":"Store XYZ","Confidence":0.98,"BoundingBox":{"X":10,"Y":15,"Width":120,"Height":20}}
{"Text":"Date: 01/01/2026","Confidence":0.95,"BoundingBox":{"X":10,"Y":45,"Width":180,"Height":20}}
{"Text":"Total   $23.45","Confidence":0.97,"BoundingBox":{"X":10,"Y":75,"Width":150,"Height":20}}
```

Pokud vidíte něco podobného, gratulujeme — úspěšně jste **extrahovali text z obrázku** a **převáděli obrázek do JSONL**.

## Časté problémy a jak se jim vyhnout  

| Problém | Proč k tomu dochází | Řešení |
|-------|----------------|-----|
| **Prázdný výstup** | Cesta k obrázku je nesprávná nebo soubor není čitelný. | Použijte `File.Exists(imagePath)` před vytvořením bitmapy. |
| **Nízké skóre důvěry** | Obrázek je rozmazaný nebo má nízký kontrast. | Předzpracujte obrázek (např. `Bitmap.RotateFlip`, `Graphics.Clear`) nebo zvyšte DPI. |
| **Nesprávný jazyk** | OCR výchozí jazyk je angličtina, ale účtenka je v jiném jazyce. | Nastavte `options.Language = Language.Spanish` (nebo odpovídající enum). |
| **JSONL se zobrazuje jako jediný JSON pole** | Použili jste `Formatting.None` bez zpracování nových řádků. | Ujistěte se, že každý serializovaný objekt končí `Environment.NewLine`. |

## Kompletní funkční příklad  

Níže je kompletní, připravený k spuštění program. Vložte jej do konzolového projektu a stiskněte **F5**.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;
using System.IO;
using System.Linq;
using Newtonsoft.Json;

namespace OcrToJsonlDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the image
            string imagePath = @"C:\MyProjects\OCRDemo\receipt.png";
            if (!File.Exists(imagePath))
            {
                Console.WriteLine($"Image not found at {imagePath}");
                return;
            }
            Bitmap receiptImage = new Bitmap(imagePath);

            // 2️⃣ Set up OCR options for JSON‑Lines output
            OcrEngine ocrEngine = new OcrEngine();
            RecognitionOptions options = new RecognitionOptions
            {
                Language = Language.English,
                OutputFormat = OutputFormat.JsonLines
            };

            // 3️⃣ Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage, options);

            // 4️⃣ Serialize to JSON‑Lines
            string jsonLines = JsonConvert.SerializeObject(
                ocrResult.Lines,
                Formatting.Indented
            );

            // 5️⃣ Write to file
            string outputPath = @"C:\MyProjects\OCRDemo\receipt.jsonl";
            File.WriteAllText(outputPath, jsonLines);
            Console.WriteLine($"✅ JSONL saved to {outputPath}");

            // 6️⃣ Quick verification
            Console.WriteLine("\nFirst three lines of output:");
            foreach (var line in File.ReadLines(outputPath).Take(3))
            {
                Console.WriteLine(line);
            }
        }
    }
}
```

**Očekávaný výsledek:** Soubor `receipt.jsonl` obsahující jeden JSON objekt na řádek, každý s poli `Text`, `Confidence` a `BoundingBox`. Nyní můžete tento soubor vložit do libovolné analytické pipeline, která konzumuje JSONL.

## Další kroky – Pokročilejší OCR  

- **Dávkové zpracování:** Zabalte výše uvedenou logiku do smyčky `foreach` pro zpracování celých složek s účtenkami.  
- **Paralelizace:** Použijte `Parallel.ForEach` pro vícejádrové zrychlení při práci s tisíci obrázky.  
- **Post‑zpracování:** Odstraňte řádky s nízkou důvěrou (`Confidence < 0.9`) před uložením.  
- **Integrace:** Odesílejte JSONL přímo do Azure Blob Storage nebo AWS S3 pomocí příslušných SDK.  
- **Alternativní formáty:** Přepněte `OutputFormat` na `PlainText` nebo `Xml`, pokud váš downstream systém preferuje tyto formáty.  

## Závěr  

Nyní máte robustní end‑to‑end řešení pro **extrahování textu z obrázku** a **převod obrázku do JSONL** pomocí Aspose OCR v C#. Tutoriál pokryl vše od načtení bitmapy po ověření výstupu, včetně několika praktických tipů, jak udržet vaši pipeline spolehlivou.

Vyzkoušejte to s vlastními účtenkami, fakturami nebo naskenovanými formuláři — sledujte, jak OCR engine během několika sekund převádí pixely na prohledávatelná, řádkově strukturovaná data. Pokud narazíte na okrajové případy (např. šikmé skeny nebo vícejazyčný text), vraťte se k sekci *RecognitionOptions* a upravte jazyk nebo předzpracování.

Šťastné programování a ať jsou vaše datové pipeline vždy čisté!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}