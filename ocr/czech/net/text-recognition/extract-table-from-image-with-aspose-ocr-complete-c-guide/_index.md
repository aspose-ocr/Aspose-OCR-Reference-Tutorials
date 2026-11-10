---
category: general
date: 2026-03-18
description: Extrahujte tabulku z obrázku pomocí Aspose OCR v C#. Naučte se, jak převést
  tabulku do JSON, získat JSON tabulky a extrahovat text z obrázku během několika
  minut.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: cs
og_description: Extrahujte tabulku z obrázku pomocí Aspose OCR v C#. Naučte se převést
  tabulku do JSON, získat JSON tabulky a rychle extrahovat text z obrázku.
og_title: Extrahovat tabulku z obrázku pomocí Aspose OCR – Kompletní průvodce C#
tags:
- Aspose OCR
- C#
- Table Extraction
title: Extrahovat tabulku z obrázku pomocí Aspose OCR – kompletní průvodce C#
url: /cs/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahovat tabulku z obrázku – Kompletní průvodce C#

Už jste někdy potřebovali **extrahovat tabulku z obrázku**, ale nebyli jste si jisti, která knihovna to zvládne bez hromady ručního parsování? Nejste v tom sami. V mnoha projektech zpracování faktur nebo skenování účtenek je hlavní problém převést šumivý bitmapový soubor na strukturovanou tabulku, kterou může váš downstream systém využít.  

Dobrá zpráva? S Aspose OCR můžete **převést tabulku na JSON** během několika řádků a zároveň získáte čistý text celého obrázku, takže **extrahovat text z obrázku** je bonus. V tomto tutoriálu projdeme celý tok – od načtení obrázku po získání úhledné JSON reprezentace detekované tabulky.

> **Rychlý výsledek:** Na konci budete mít spustitelnou C# konzolovou aplikaci, která vypíše jak surový OCR text, tak JSON řetězec, který můžete přímo vložit do databáze nebo API.

## Požadavky

Než se pustíme dál, ujistěte se, že máte:

- .NET 6.0 SDK (nebo jakoukoli novější verzi .NET) nainstalovanou.  
- Platnou licenci Aspose OCR nebo bezplatnou zkušební verzi (knihovna funguje i bez licence, ale přidá vodoznak).  
- Obrázek, který skutečně obsahuje tabulku – například `invoice_table.png`.  
- Visual Studio 2022, VS Code nebo jakýkoli editor, který preferujete.

Žádné další NuGet balíčky kromě `Aspose.OCR` nejsou potřeba.

## Krok 1: Nastavení projektu a instalace Aspose OCR

Nejprve vytvořte nový konzolový projekt a přidejte OCR knihovnu.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Tip:** Pokud používáte firemní proxy, přidejte přepínač `--no-restore` a později spusťte `dotnet restore` s nastavenými proměnnými prostředí.

## Krok 2: Inicializace OCR enginu a povolení rozpoznávání tabulek

Jádrem řešení je `OcrEngine`. Zapnutím `EnableTableRecognition` řekneme Aspose OCR, aby hledal mřížkové struktury místo toho, aby vše považoval za prostý text.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;

class TableJsonDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable table detection – this is what lets us get a JSON table later
        ocrEngine.Settings.EnableTableRecognition = true;
```

Proč je tento krok klíčový? Bez rozpoznávání tabulek by engine převáděl obrázek na jeden řetězec, což by znemožnilo pozdější rekonstrukci řádků a sloupců. Povolení přidá lehkou fázi analýzy rozvržení, která téměř nic neovlivní výkon, ale přinese obrovské výhody v downstream zpracování.

## Krok 3: Načtení obrázku a spuštění rozpoznání

Nyní nasměrujeme engine na soubor, který obsahuje tabulku. `ImageStream.FromFile` podporuje většinu běžných formátů (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Pokud je obrázek velký, zvažte jeho předchozí zmenšení pro zrychlení zpracování. Aspose OCR automaticky detekuje DPI, ale sken s 300 DPI je optimální pro většinu tabulek.

## Krok 4: Extrahování čistého textu – “extract text from image”

I když je naším hlavním cílem tabulka, často stále potřebujete surový text pro logování nebo záložní zpracování.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

Vlastnost `Text` spojí vše, co engine vidí, a zachová zalomení řádků. To je užitečné, když potřebujete ověřit, že OCR správně přečetl záhlaví nebo patičky mimo oblast tabulky.

## Krok 5: Získání detekované tabulky jako JSON – “convert table to json” & “get table json”

Zde se děje magie. `GetTableAsJson()` serializuje detekované řádky, sloupce a obsah buněk do čistého JSON řetězce.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

Výsledný JSON vypadá zhruba takto (formátováno pro čitelnost):

```json
{
  "Rows": [
    {
      "Cells": [
        { "Text": "Item", "ColumnIndex": 0 },
        { "Text": "Quantity", "ColumnIndex": 1 },
        { "Text": "Price", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget A", "ColumnIndex": 0 },
        { "Text": "10", "ColumnIndex": 1 },
        { "Text": "$5.00", "ColumnIndex": 2 }
      ]
    },
    {
      "Cells": [
        { "Text": "Widget B", "ColumnIndex": 0 },
        { "Text": "7", "ColumnIndex": 1 },
        { "Text": "$8.50", "ColumnIndex": 2 }
      ]
    }
  ]
}
```

Proč je JSON preferovaný formát? Je jazykově neutrální, snadno se deserializuje do objektů a skvěle spolupracuje s moderními webovými API. Pokud potřebujete CSV, stačí iterovat přes řádky a spojit texty buněk čárkami.

## Krok 6: (Volitelné) Převod JSONu na .NET objekt – “convert image to json”

Pokud raději pracujete se silně typovanými objekty, deserializujte JSON pomocí `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Definujete `TableModel`, `RowModel` a `CellModel` tak, aby odpovídaly schématu JSONu. Tento krok ukazuje, jak můžete přejít od **convert image to json** až po typovaný objekt, což usnadní downstream validaci.

## Kompletní funkční příklad

Sestavením všeho dohromady získáte kompletní, připravený program. Uložte jej jako `Program.cs` ve složce projektu, kterou jste vytvořili dříve.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Structure;
using System.Text.Json;

class TableJsonDemo
{
    static void Main()
    {
        // Step 1: Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Enable table recognition
        ocrEngine.Settings.EnableTableRecognition = true;

        // Step 3: Load image containing a table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Step 4: Run OCR
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 5: Print full text (extract text from image)
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);

        // Step 6: Get table as JSON (convert table to json, get table json)
        string tableJson = ocrResult.GetTableAsJson();
        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);

        // Optional: Deserialize JSON to C# objects (convert image to json)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
    }
}

// Helper classes matching Aspose's JSON structure
public class TableModel
{
    public RowModel[] Rows { get; set; }
}
public class RowModel
{
    public CellModel[] Cells { get; set; }
}
public class CellModel
{
    public string Text { get; set; }
    public int ColumnIndex { get; set; }
}
```

### Očekávaný výstup

Po spuštění `dotnet run` byste měli vidět něco podobného:

```
Full text:
Item Quantity Price
Widget A 10 $5.00
Widget B 7 $8.50

Detected table (JSON):
{
  "Rows":[
    {"Cells":[{"Text":"Item","ColumnIndex":0},{"Text":"Quantity","ColumnIndex":1},{"Text":"Price","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget A","ColumnIndex":0},{"Text":"10","ColumnIndex":1},{"Text":"$5.00","ColumnIndex":2}]},
    {"Cells":[{"Text":"Widget B","ColumnIndex":0},{"Text":"7","ColumnIndex":1},{"Text":"$8.50","ColumnIndex":2}]}
  ]
}

First cell value: Item
```

Pokud výstup vypadá prázdně, zkontrolujte, že `EnableTableRecognition` je nastaveno na `true` a že obrázek skutečně obsahuje jasně viditelné mřížkové čáry.

## Časté problémy a jak se jim vyhnout

| Problém | Proč se vyskytuje | Řešení |
|-------|----------------|-----|
| **Žádný JSON** | Rozpoznávání tabulky vypnuto nebo obrázek má nízký kontrast. | Ujistěte se, že `ocrEngine.Settings.EnableTableRecognition = true` a zlepšete kvalitu obrázku (zvyšte kontrast, binarizujte). |
| **Částečné řádky** | OCR zmatený spojenými buňkami nebo otočeným textem. | Předzpracujte obrázek: korekce sklonu (`ImageProcessor.Rotate`) nebo ručně rozdělte spojené buňky. |
| **Unicode špatně** | Písmo nerozpoznáno (např. ručně psané). | Přepněte jazykové balíčky pomocí `ocrEngine.Language = Language.English;` nebo použijte jiný OCR engine pro ručně psaný text. |
| **Zpomalení výkonu** | Velmi velký obrázek (>5 MP). | Zmenšete na šířku ~1500 px při zachování DPI. |

## Další kroky: Přesah základů

Nyní, když umíte **extrahovat tabulku z obrázku** a **převést tabulku na JSON**, zvažte následující rozšíření:

- **Ukládat JSON** do databáze pomocí Entity Framework.  
- **Post‑process** JSON pro normalizaci měnových formátů (např. odstranit `$`).  
- **Dávkové zpracování** složky faktur pomocí `Directory.GetFiles` a paralelizace s `Parallel.ForEach`.  
- **Integrace** s Azure Functions nebo AWS Lambda pro serverless OCR pipeline.

Každé z těchto témat přirozeně přináší další sekundární klíčová slova jako **convert image to json** (když posíláte celý OCR výsledek do cloudového endpointu) a **get table json** pro downstream analytiku.

---

### Závěr

Ukázali jsme vám, jak **extrahovat tabulku z obrázku** pomocí Aspose OCR, převést tuto tabulku na čistý JSON a dokonce jej deserializovat do C# objektů. Stejný vzor

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}