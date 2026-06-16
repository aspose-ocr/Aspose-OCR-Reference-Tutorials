---
category: general
date: 2026-03-07
description: Extrahujte text z PNG souborů pomocí C#. Naučte se, jak převést obrázek
  na text v C# a rychle číst text ze skenovaných obrázků.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: cs
og_description: Extrahujte text z PNG souborů pomocí C#. Tento průvodce ukazuje, jak
  převést obrázek na text v C# a číst text ze skenovaných obrázků pomocí Aspose OCR.
og_title: Extrahování textu z PNG v C# – Kompletní průvodce OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Extrahování textu z PNG v C# – Kompletní průvodce OCR
url: /cs/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat text z PNG v C# – Kompletní průvodce OCR

Už jste někdy potřebovali **extract text from PNG** soubory, ale nebyli jste si jisti, kde začít? Nejste v tom sami – většina vývojářů narazí na tuto překážku, když poprvé čelí naskenovaným grafikám nebo screenshotům, které mají být převáděny na prohledávatelný text. Dobrá zpráva? S několika řádky C# a Aspose OCR můžete během chvilky převést jakýkoli PNG na editovatelné řetězce.

V tomto tutoriálu projdeme celý proces: od vyhledání PNG souborů na disku, spuštění OCR úloh paralelně, až po zobrazení přehledného náhledu každého výsledku. Na konci budete vědět, jak **convert image to text C#** styl, budete schopni **read text from scanned images** efektivně a také uvidíte nejlepší způsob, jak **run OCR on images** bez zatížení UI vlákna.

## Co budete potřebovat

- .NET 6.0 nebo novější (kód funguje i na .NET Core a .NET Framework)  
- Aspose.OCR NuGet balíček (`Install-Package Aspose.OCR`)  
- Složka plná *.png* souborů, které chcete zpracovat  
- Jakékoli IDE, které máte rádi (Visual Studio, VS Code, Rider…)

Žádná další konfigurace není potřeba; knihovna obsahuje vše potřebné pro dekódování PNG, JPEG, TIFF a dalších formátů.

## Krok 1: Najděte všechny PNG soubory – začíná „Extract Text from PNG“

Nejprve musíme najít každý PNG, na který chceme spustit OCR. Použití `Directory.GetFiles` je rychlé a spolehlivé.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Proč je to důležité:* Jednorázové prohledání adresáře udržuje zbytek pipeline jednoduchý a brzká kontrola zabraňuje tichému „žádnému výstupu“, který může být později těžko laditelný.

## Krok 2: Spusťte paralelní OCR úlohy – efektivně **run OCR on images**

Spouštění OCR sekvenčně je v pořádku pro pár souborů, ale reálné projekty často pracují s desítkami či stovkami souborů. Vytvořením `Task` pro každý obrázek udržíme CPU vytížené, zatímco knihovna provádí těžkou práci.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Tip:* `Task.Run` přenese práci do thread poolu, což znamená, že vaše UI (pokud nějaké máte) zůstane responzivní. Na serveru se stejný vzor dobře škáluje napříč jádry.

## Krok 3: Počkejte na všechny úlohy – shromážděte výsledky

Nyní čekáme, až se dokončí každá OCR operace. `Task.WhenAll` vrací pole, které odpovídá původnímu pořadí souborů, takže je snadné spárovat výsledky s názvy souborů.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Poznámka o okrajových případech:* Pokud některý obrázek vyhodí výjimku (poškozený soubor, nepodporovaný formát), celý `WhenAll` propaguje výjimku. Můžete obalit vnitřní `Task.Run` do try/catch a vrátit prázdný řetězec nebo diagnostickou zprávu, pokud potřebujete odolnost vůči chybám.

## Krok 4: Zobrazte náhled – ověřte výstup **convert image to text C#**

Rychlý náhled vám pomůže potvrdit, že OCR fungovalo, než začnete data ukládat někam jinam.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Typický výstup v konzoli vypadá takto:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Pokud náhled ukazuje nesmysly, zkontrolujte kvalitu obrázku nebo zvažte předzpracování (např. binarizaci) – ale pro většinu čistých PNG Aspose OCR dosáhne správného výsledku hned na první pokus.

## Volitelné: Uložte výsledky do CSV – reálný případ použití

Většina projektů potřebuje extrahovaný text ve strukturovaném formátu. Níže je malý pomocník, který zapisuje název souboru a celý OCR text do CSV souboru.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Nyní můžete CSV importovat do Excelu, Power BI nebo jakéhokoli downstream systému, který očekává **read text from scanned images**.

## Často kladené otázky

**Co když jsou mé PNG soubory obrovské (více než 5 MB)?**  
Aspose OCR automaticky down‑sampleuje velké obrázky, aby udržel rozumnou spotřebu paměti, ale můžete ručně změnit velikost pomocí `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` a omezit šířku na 2000 px při zachování poměru stran.

**Mohu to spustit na Linuxu?**  
Ano. Aspose OCR je multiplatformní; jen se ujistěte, že jsou nainstalovány nativní závislosti (`libgdiplus` na některých distribucích).

**Je výchozí jazyk OCR nastaven na angličtinu?**  
Ano. Pokud potřebujete jiný jazyk, nastavte `engine.Language = OcrLanguage.French;` (nebo jakýkoli podporovaný enum) před voláním `Recognize()`.

**Jak zacházet s PDF soubory chráněnými heslem, které obsahují PNG?**  
Nejprve převést stránky PDF na obrázky (pomocí Aspose PDF nebo jiné knihovny) a pak tyto PNG předat do stejné pipeline. Princip **how to run OCR on images** zůstává stejný.

## Kompletní funkční příklad (Async Main)

Níže je samostatný program, který můžete zkopírovat a vložit do konzolového projektu. Obsahuje všechny výše uvedené části plus malý pomocník pro validaci vstupní složky.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Očekávaný výstup** (ukázka pro dva PNG):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Závěr

Právě jsme prošli vším, co potřebujete k **extract text from PNG** souborů pomocí C#. Od vyhledání souborů, spuštění paralelních OCR úloh, náhledu řetězců až po jejich uložení do CSV – tento průvodce vám poskytuje produkčně připravený vzor pro scénáře **convert image to text C#**.  

Jste připraveni na další krok? Zkuste stejnou pipeline použít na JPEG nebo TIFF soubory, experimentujte s různými OCR jazyky nebo propojte výsledky s vyhledávacím indexem, abyste mohli **read text from scanned images** okamžitě.  

Máte otázky ohledně okrajových případů, ladění výkonu nebo licencování? Zanechte komentář nebo napište do komunity Aspose – šťastné kódování!  

![Příklad extrakce textu z PNG](extract-text-png.png "Extrahovat text z PNG pomocí Aspose OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}