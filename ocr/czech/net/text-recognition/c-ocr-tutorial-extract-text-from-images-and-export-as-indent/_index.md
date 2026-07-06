---
category: general
date: 2026-05-02
description: c# OCR tutoriál, který ukazuje, jak extrahovat text z obrázku v c#, rozpoznat
  text v PNG a poté zapsat odsazený JSON pomocí JsonSerializer v c#. Krok za krokem
  průvodce pro vývojáře.
draft: false
keywords:
- c# ocr tutorial
- extract text image c#
- recognize png text
- write indented json
- use jsonserializer c#
language: cs
og_description: C# OCR tutoriál, který ukazuje, jak v C# extrahovat text z obrázku
  a rozpoznat text v PNG, a poté zapsat odsazený JSON pomocí JsonSerializer v C#.
  Kompletní, spustitelný příklad.
og_title: c# OCR tutoriál – Extrahovat text a exportovat jako odsazený JSON
tags:
- OCR
- C#
- Aspose
- JSON
title: c# OCR tutoriál – Extrahovat text z obrázků a exportovat jako odsazený JSON
url: /cs/net/text-recognition/c-ocr-tutorial-extract-text-from-images-and-export-as-indent/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# ocr tutorial – Extrahování textu z obrázků a export jako odsazený JSON

Už jste někdy potřebovali **c# ocr tutorial**, který jde od obrázku s textem přímo k hezky naformátovanému souboru JSON? Nejste v tom sami. V mnoha projektech – například skenování faktur, parsování účtenek nebo i jednoduché získávání textu z memů – skončíte s PNG souborem a přemýšlíte, jak z něj vytáhnout slova, aniž byste museli psát vlastní rozpoznávač.  

Tento návod vám poskytne praktické řešení: **extrahujeme text z obrázku c#** pomocí Aspose.OCR, **rozpoznáme png text** a poté **zapíšeme odsazený json** pomocí `JsonSerializer` v C#. Na konci budete mít samostatnou konzolovou aplikaci, kterou můžete vložit do libovolného .NET řešení. Žádné vágní odkazy typu „viz dokumentace“, jen kompletní, připravený příklad ke zkopírování.

## Co budete potřebovat

- **.NET 6** (nebo jakákoli novější verze .NET). Starší frameworky fungují, ale ukázaná syntaxe cílí na .NET 6+.
- **Aspose.OCR for .NET** – nainstalujte přes NuGet: `dotnet add package Aspose.OCR`.
- Ukázkový PNG obrázek (`text.png`) obsahující jasný, strojově čitelný text.
- IDE nebo editor dle vašeho výběru – Visual Studio, VS Code, Rider atd.

> **Pro tip:** Pokud plánujete zpracovávat mnoho obrázků, zvažte opětovné použití jedné instance `OcrEngine` místo vytváření nové pro každý soubor. Snížíte tak režii a zvýšíte propustnost.

## Krok 1: Vytvořte projekt c# ocr tutorial

Nejprve vytvořte konzolový projekt. Následující příkazy vytvoří strukturu a přidají OCR knihovnu:

```bash
dotnet new console -n OcrJsonDemo
cd OcrJsonDemo
dotnet add package Aspose.OCR
```

Nyní otevřete vygenerovaný soubor `Program.cs`. Později nahradíme jeho obsah kompletním příkladem, ale prozatím se ujistěte, že se projekt úspěšně sestaví:

```bash
dotnet build
```

Pokud nevidíte žádné chyby, můžete pokračovat.

## Krok 2: Rozpoznání PNG textu z obrázku

Srdcem každého **c# ocr tutorial** je samotný OCR engine. Aspose.OCR abstrahuje nízkoúrovňové detaily a poskytuje čistou třídu `OcrEngine`. Níže vytvoříme engine, nasměrujeme ho na PNG soubor a požádáme ho o rozpoznání textu.

```csharp
using Aspose.OCR;
using System;
using System.Text.Json;

class JsonExportExample
{
    public static void Run()
    {
        // 1️⃣ Create an OCR engine instance – this is the entry point for all OCR work.
        var ocrEngine = new OcrEngine();

        // 2️⃣ Recognize text from the input image. 
        //    The method automatically detects the language (default is English) and returns an OcrResult.
        var ocrResult = ocrEngine.RecognizeImage("YOUR_DIRECTORY/text.png");

        // If the image couldn't be read, handle it gracefully.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No text detected – double‑check the file path and image quality.");
            return;
        }

        // Continue to serialization...
```

### Proč to funguje

- **`RecognizeImage`** podporuje mnoho formátů (PNG, JPEG, BMP). Speciálně **recognize png text**, protože PNG zachovává bezztrátové detaily, což je pro OCR ideální.
- Vrácený `OcrResult` obsahuje nejen prostý text, ale i skóre důvěry pro každý glyf, což se hodí, pokud později potřebujete filtrovat znaky s nízkou důvěrou.

## Krok 3: Zápis odsazeného JSON pomocí JsonSerializer c#

Nyní, když máme `ocrResult`, dalším logickým krokem v našem **c# ocr tutorial** je převést tento objekt na čitelný JSON. Vestavěný serializer `System.Text.Json` to zvládne a nastavíme ho tak, aby **write indented json** pro přehlednost.

```csharp
        // 3️⃣ Serialize the OCR result (including confidence per glyph) to indented JSON.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // This makes the output pretty‑printed.
        };

        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 4️⃣ Display the JSON result – you could also write it to a file if you prefer.
        Console.WriteLine(jsonOutput);
    }
}
```

### Správné použití `JsonSerializer`

- Přepínač `WriteIndented` je nejjednodušší způsob, jak **write indented json** bez nutnosti třetích knihoven.
- Pokud někdy potřebujete názvy vlastností v camelCase, přidejte do možností `PropertyNamingPolicy = JsonNamingPolicy.CamelCase`.
- Řetězec `jsonOutput` můžete uložit pomocí `File.WriteAllText("result.json", jsonOutput);` – praktické pro reálné pipeline.

## Krok 4: Spusťte a ověřte výstup

Zkompilujte a spusťte program:

```bash
dotnet run
```

Předpokládáme, že `text.png` obsahuje frázi *„Hello, OCR World!“*, měli byste vidět něco jako:

```json
{
  "Text": "Hello, OCR World!",
  "Confidence": 0.9875,
  "Lines": [
    {
      "Text": "Hello, OCR World!",
      "Confidence": 0.9875,
      "Words": [
        {
          "Text": "Hello,",
          "Confidence": 0.9921,
          "BoundingBox": { "X": 12, "Y": 34, "Width": 58, "Height": 20 }
        },
        {
          "Text": "OCR",
          "Confidence": 0.9812,
          "BoundingBox": { "X": 78, "Y": 34, "Width": 34, "Height": 20 }
        },
        {
          "Text": "World!",
          "Confidence": 0.9890,
          "BoundingBox": { "X": 118, "Y": 34, "Width": 62, "Height": 20 }
        }
      ]
    }
  ]
}
```

Tento JSON je **odsazený**, takže se snadno čte v logách nebo jej můžete předat dalším službám.

### Okrajové případy a tipy

| Situace | Co dělat |
|-----------|------------|
| **Obrázek je rozmazaný** | Zvyšte `ocrEngine.Config.Dpi` (např. `ocrEngine.Config.Dpi = 300`) před voláním `RecognizeImage`. |
| **Jazyk není angličtina** | Nastavte `ocrEngine.Config.Language = OcrLanguage.German` (nebo jakýkoli podporovaný jazyk). |
| **Velká dávka souborů** | Procházejte adresář v cyklu, přičemž znovu použijete stejnou instanci `OcrEngine`; uložte každý JSON výsledek pod unikátním názvem souboru. |
| **Potřebujete jen text s vysokou důvěrou** | Před serializací filtrujte `ocrResult.Lines`, kde `Confidence` ≥ 0.95. |

## Kompletní funkční příklad (připravený ke kopírování)

Níže je *celý* program, připravený vložit do `Program.cs`. Obsahuje všechny kroky, ošetření chyb a komentáře, které kód činí samovysvětlujícím.

```csharp
using Aspose.OCR;
using System;
using System.IO;
using System.Text.Json;

class JsonExportExample
{
    public static void Main()
    {
        // 👉 Step 1: Initialize the OCR engine.
        var ocrEngine = new OcrEngine();

        // 👉 Step 2: Path to the PNG image you want to process.
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "text.png");

        if (!File.Exists(imagePath))
        {
            Console.WriteLine($"Image not found at {imagePath}");
            return;
        }

        // 👉 Step 3: Perform OCR – this is where we **recognize png text**.
        var ocrResult = ocrEngine.RecognizeImage(imagePath);

        // 👉 Step 4: Validate the result.
        if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
        {
            Console.WriteLine("No recognizable text found. Try a clearer image or adjust DPI settings.");
            return;
        }

        // 👉 Step 5: Configure JsonSerializer to **write indented json**.
        var jsonOptions = new JsonSerializerOptions
        {
            WriteIndented = true // Pretty‑print the JSON.
        };

        // 👉 Step 6: Serialize the OCR result – this demonstrates **use jsonserializer c#**.
        string jsonOutput = JsonSerializer.Serialize(ocrResult, jsonOptions);

        // 👉 Step 7: Output to console (or write to a file).
        Console.WriteLine(jsonOutput);

        // Optional: Save to disk.
        string outputPath = Path.ChangeExtension(imagePath, ".json");
        File.WriteAllText(outputPath, jsonOutput);
        Console.WriteLine($"JSON saved to {outputPath}");
    }
}
```

Spusťte kód, podívejte se do konzole nebo do vygenerovaného souboru `.json` a uvidíte extrahovaný text spolu se skóre důvěry, vše pěkně **odsazené**.

## Závěr

Nyní máte solidní **c# ocr tutorial**, který ukazuje, jak **extract text image c#**, **recognize png text**, a **write indented json** pomocí `JsonSerializer`. Příklad je kompletní, spustitelný a obsahuje praktické tipy pro reálné scénáře.  

Další kroky? Vyzkoušejte výměnu Aspose.OCR za jiný engine (např. Tesseract) a podívejte se, jak se změní struktura `OcrResult`, nebo pošlete JSON do downstream API, které ukládá OCR data do databáze. Můžete také experimentovat s **use jsonserializer c#** možnostmi, jako jsou vlastní konvertory pro formátování dat nebo zpracování enumů.

Šťastné kódování a ať jsou vaše OCR pipeline vždy přesné!  

---  

![c# ocr tutorial diagram](image.png "Diagram illustrating OCR flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}