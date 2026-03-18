---
category: general
date: 2026-03-18
description: Extrahera tabell från bild med Aspose OCR i C#. Lär dig hur du konverterar
  tabellen till JSON, får tabell‑JSON och extraherar text från bilden på några minuter.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: sv
og_description: Extrahera tabell från bild med Aspose OCR i C#. Lär dig att konvertera
  tabellen till JSON, hämta tabellens JSON och extrahera text från bilden snabbt.
og_title: Extrahera tabell från bild med Aspose OCR – Komplett C#‑guide
tags:
- Aspose OCR
- C#
- Table Extraction
title: Extrahera tabell från bild med Aspose OCR – Komplett C#-guide
url: /sv/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera tabell från bild – Komplett C#‑guide

Har du någonsin behövt **extract table from image** men varit osäker på vilket bibliotek som kan göra det utan en berg av manuell parsning? Du är inte ensam. I många fakturabehandlings‑ eller kvittoscan‑projekt är den verkliga smärtan att omvandla en brusig bitmap till en strukturerad tabell som ditt downstream‑system kan konsumera.  

Den goda nyheten? Med Aspose OCR kan du **convert table to JSON** på några få rader, och du får även ren text från hela bilden, så **extract text from image** är en bonus. I den här handledningen går vi igenom hela flödet – från att ladda en bild till att få en prydlig JSON‑representation av den upptäckta tabellen.

> **Quick win:** Vid slutet kommer du att ha en körbar C#‑konsolapp som skriver ut både den råa OCR‑texten och en JSON‑sträng som du kan mata direkt in i en databas eller ett API.

## Förutsättningar

- .NET 6.0 SDK (eller någon nyare .NET‑version) installerad.  
- En giltig Aspose OCR‑licens eller en gratis provperiod (biblioteket fungerar utan licens men lägger till ett vattenmärke).  
- En bild som faktiskt innehåller en tabell – till exempel `invoice_table.png`.  
- Visual Studio 2022, VS Code, eller någon editor du föredrar.

Inga extra NuGet‑paket utöver `Aspose.OCR` krävs.

## Steg 1: Skapa projektet och installera Aspose  OCR

Först, skapa ett nytt konsolprojekt och hämta OCR‑biblioteket.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Om du använder en företagsproxy, lägg till flaggan `--no-restore` och kör `dotnet restore` senare med rätt miljövariabler.

## Steg 2: Initiera OCR‑motorn och aktivera tabelligenkänning

Kärnan i lösningen är `OcrEngine`. Genom att slå på `EnableTableRecognition` säger vi till Aspose  OCR att leta efter rutnäts‑liknande strukturer istället för att behandla allt som ren text.

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

Varför är detta steg avgörande? Utan tabelligenkänning skulle motorn platta till bilden till en enda sträng, vilket gör det omöjligt att återkonstruera rader och kolumner senare. Att aktivera den lägger till en lättviktig layout‑analysfas som nästan inte påverkar prestandan men ger stora downstream‑fördelar.

## Steg 3: Ladda din bild och kör igenkänningen

Nu pekar vi motorn på filen som innehåller tabellen. `ImageStream.FromFile` stöder de flesta vanliga format (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Om bilden är stor, överväg att ändra storlek på den först för att snabba upp bearbetningen. Aspose  OCR upptäcker automatiskt DPI, men en 300 DPI‑skanning är en bra kompromiss för de flesta tabeller.

## Steg 4: Extrahera ren text – “extract text from image”

Även om vårt huvudmål är tabellen, behöver du ofta fortfarande den råa texten för loggning eller reservbearbetning.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

`Text`‑egenskapen konkatenerar allt som motorn ser, och bevarar radbrytningar. Detta är praktiskt när du behöver verifiera att OCR korrekt läst rubriker eller sidfötter utanför tabellområdet.

## Steg 5: Hämta den upptäckta tabellen som JSON – “convert table to json” & “get table json”

Här sker magin. `GetTableAsJson()` serialiserar de upptäckta raderna, kolumnerna och cellinnehållet till en ren JSON‑sträng.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

Den resulterande JSON‑strängen ser ungefär ut så här (formaterad för läsbarhet):

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

Varför är JSON det föredragna formatet? Det är språk‑oberoende, enkelt att deserialisera till objekt, och fungerar bra med moderna webb‑API:er. Om du istället behöver en CSV, iterera bara över raderna och slå ihop celltexterna med kommatecken.

## Steg 6: (Valfritt) Konvertera JSON till ett .NET‑objekt – “convert image to json”

Om du föredrar att arbeta med starka typer, deserialisera JSON‑strängen med `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Du skulle definiera `TableModel`, `RowModel` och `CellModel` för att matcha JSON‑schemat. Detta steg visar hur du kan gå från **convert image to json** hela vägen till ett typat objekt, vilket gör downstream‑validering enkelt.

## Fullt fungerande exempel

När vi sätter ihop allt, här är det kompletta, färdiga programmet. Spara det som `Program.cs` i projektmappen som skapades tidigare.

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

### Förväntad utdata

När du kör `dotnet run` bör du se något liknande:

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

Om utdata ser tom ut, dubbelkolla att `EnableTableRecognition` är satt till `true` och att bilden faktiskt innehåller tydliga rutlinjer.

## Vanliga fallgropar & hur man undviker dem

| Problem | Varför det händer | Lösning |
|---------|-------------------|--------|
| **Ingen JSON returnerad** | Tabelligenkänning inaktiverad eller bilden har för låg kontrast. | Säkerställ att `ocrEngine.Settings.EnableTableRecognition = true` och förbättra bildkvaliteten (öka kontrast, binarisera). |
| **Ofullständiga rader** | OCR förvirrad av sammanslagna celler eller roterad text. | Förbehandla bilden: räta upp (`ImageProcessor.Rotate`) eller dela upp sammanslagna celler manuellt. |
| **Unicode‑skräp** | Typsnittet känns inte igen (t.ex. handskrivet). | Byt språkpaket via `ocrEngine.Language = Language.English;` eller använd en annan OCR‑motor för handskrift. |
| **Prestandaförsämring** | Mycket stor bild (>5 MP). | Skala ner till ~1500 px i bredd samtidigt som DPI bevaras. |

## Nästa steg: Gå bortom grunderna

Nu när du kan **extract table from image** och **convert table to JSON**, överväg dessa tillägg:

- **Persist the JSON** till en databas med Entity Framework.  
- **Post‑process** JSON‑en för att normalisera valutformat (t.ex. ta bort `$`).  
- **Batch process** en mapp med fakturor med `Directory.GetFiles` och parallellisera med `Parallel.ForEach`.  
- **Integrate** med Azure Functions eller AWS Lambda för serverlösa OCR‑pipelines.

Varje av dessa ämnen introducerar naturligt de andra sekundära nyckelorden som **convert image to json** (när du skickar hela OCR‑resultatet till en moln‑endpoint) och **get table json** för downstream‑analys.

---

### Slutsats

Vi har just visat dig hur du **extract table from image** med Aspose  OCR, omvandlar den tabellen till ren JSON, och till och med deserialiserar den till C#‑objekt. Samma mönster

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}