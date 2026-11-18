---
category: general
date: 2026-03-28
description: Lär dig hur du extraherar tabeller från bilder med Aspose OCR i C#. Denna
  guide täcker hur du upptäcker tabeller i en bild, laddar bilden för OCR och extraherar
  tabeller från PNG‑filer.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: sv
og_description: Steg‑för‑steg‑handledning om hur man extraherar tabeller från bilder
  med Aspose OCR i C#. Inkluderar kod, förklaringar och tips för att upptäcka tabeller
  i bildfiler.
og_title: Hur man extraherar tabeller från bilder med Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: Hur man extraherar tabeller från bilder med Aspose OCR (C#)
url: /sv/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man extraherar tabeller från bilder med Aspose OCR (C#)

Har du någonsin undrat **hur man extraherar tabeller** från en skannad faktura eller en skärmdump av ett kalkylblad? Du är inte ensam. I många verkliga projekt måste vi omvandla en bild av en tabell till något vi kan fråga—vanligtvis en CSV eller en DataTable. Den goda nyheten? Aspose OCR gör det till en barnlek, och du kan göra det på bara några rader C#.

I den här handledningen går vi igenom hela processen: från **load image for OCR**, till **detect tables in image**, och slutligen **extract table from image** och spara den som en CSV‑fil. I slutet har du en färdigkörbar konsolapp som kan **extract tables from PNG**‑filer (eller någon annan stödd bitmap) utan krångel.

## Förutsättningar

- .NET 6.0 SDK eller senare (koden fungerar även med .NET Framework)
- Visual Studio 2022 (eller någon IDE du föredrar)
- En Aspose.OCR för .NET licensfil (du kan börja med en gratis provversion)
- En exempelbild som innehåller en tabell (t.ex. `invoice_table.png`)

Om något av detta låter obekant, oroa dig inte—installera bara .NET SDK och hämta NuGet‑paketet, så är du redo att köra.

## Översikt av lösningen

På en hög nivå ser arbetsflödet ut så här:

1. **Load the image** du vill bearbeta.
2. **Run OCR recognition** så att motorn vet var texten finns.
3. **Create a TableExtractor** som skannar OCR‑resultaten för rutnätsliknande strukturer.
4. **Extract all detected tables** och välj den du behöver.
5. **Save the table** som CSV (eller något annat format du föredrar).

Varje steg förklaras i detalj nedan, med kompletta kodsnuttar som du kan kopiera‑klistra.

<img src="table_extraction_example.png" alt="exempel på hur man extraherar tabeller från bild" width="600">

*(Bilden ovan visar ett exempel på en fakturatabell som vi kommer att extrahera.)*

## Steg 1 – Ladda bilden för OCR

Det första du måste göra är att tala om för Aspose OCR vilken fil som ska läsas. Biblioteket stödjer PNG, JPEG, BMP, TIFF och några andra format. Här är den minsta koden:

```csharp
using Aspose.OCR;
using System.Drawing;   // Required for Image.FromFile

// ...

// Load the image that contains the table
var ocrEngine = new OcrEngine
{
    Image = Image.FromFile(@"C:\Images\invoice_table.png") // <-- adjust the path
};
```

**Varför detta är viktigt:**  
`Image.FromFile` gör det tunga lyftet att avkoda PNG‑filen (eller någon annan bitmap) till ett format som OCR‑motorn kan förstå. Om du hoppar över detta steg eller skickar en korrupt fil, kommer det efterföljande `Recognize()`‑anropet att kasta ett undantag.

> **Proffstips:** Om du hanterar stora PDF‑filer, extrahera varje sida som en bild först—annars kommer OCR‑motorn att få slut på minne.

## Steg 2 – Känn igen sidan (Krävs innan tabellidentifiering)

Kännedom konverterar de råa pixeldata till en sökbar textlayout. Utan detta steg har `TableExtractor` inget att arbeta med.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**Vad händer under huven?**  
Aspose OCR kör en neuronnätsbaserad textdetektor, och skapar sedan en hierarki av `Page`, `Paragraph` och `Word`‑objekt. Tabelldetektorn granskar senare de rumsliga relationerna mellan dessa ord.

Om du bearbetar många bilder i en loop, överväg att återanvända samma `OcrEngine`‑instans och bara byta `Image`‑egenskapen—det minskar allokeringskostnaden.

## Steg 3 – Skapa en TableExtractor och upptäck tabeller i bilden

Nu när OCR‑data finns, kan vi be Aspose att hitta tabeller. Klassen `TableExtractor` gör precis det.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Varför använda `ExtractAll()`?**  
En enda bild kan innehålla flera tabeller (tänk på en rapport med flera sektioner). `ExtractAll()` returnerar en `List<Table>` så att du kan iterera, välja rätt eller till och med slå ihop dem senare.

Om du bara behöver den första tabellen kan du säkert använda `extractedTables[0]`, men skydda alltid mot en tom lista för att undvika `IndexOutOfRangeException`.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## Steg 4 – Spara den extraherade tabellen som CSV (eller något annat format)

Aspose gör exportering trivialt. Klassen `Table` har inbyggda metoderna `SaveCsv`, `SaveXls` och `SaveJson`. Så här skriver du en CSV‑fil:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**Hur ser CSV‑filen ut?**  
Om vi antar att källbilden innehöll ett 4 × 3‑rutnät, kan CSV‑filen se ut så här:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Du kan öppna den här filen i Excel, Power BI eller mata in den direkt i din datapipeline.

## Fullständigt end‑to‑end‑exempel

Nedan är det kompletta, fristående programmet. Kopiera det till ett nytt konsolprojekt (`dotnet new console`) och kör det. Se till att NuGet‑paketet `Aspose.OCR` är installerat (`dotnet add package Aspose.OCR`).

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;          // For Image
using Aspose.OCR;
using Aspose.OCR.Table;

namespace TableExtractTutorial
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Load the image that contains the table
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                Image = Image.FromFile(@"C:\Images\invoice_table.png")
            };

            // -------------------------------------------------
            // Step 2: Recognize the page (required before table detection)
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 3: Create a TableExtractor and detect tables
            // -------------------------------------------------
            var tableExtractor = new TableExtractor(ocrEngine);
            List<Table> extractedTables = tableExtractor.ExtractAll();

            // Guard against no tables found
            if (extractedTables.Count == 0)
            {
                Console.WriteLine("No tables detected. Verify image quality or OCR settings.");
                return;
            }

            // -------------------------------------------------
            // Step 4: Save the first extracted table as CSV
            // -------------------------------------------------
            string csvPath = @"C:\Output\invoice_table.csv";
            extractedTables[0].SaveCsv(csvPath);

            Console.WriteLine($"Table extraction completed. CSV saved at: {csvPath}");
        }
    }
}
```

### Förväntad utskrift

När du kör programmet bör du se något liknande:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

Öppna `invoice_table.csv` så hittar du raderna och kolumnerna som speglar den ursprungliga bilden.

## Vanliga frågor & edge‑cases

### Vad händer om bilden är en JPEG istället för PNG?

Samma kod fungerar—byt bara filändelsen i `Image.FromFile`. Aspose OCR upptäcker automatiskt formatet, så **extract tables from png** är inte ett hårt krav; det fungerar med vilken stödd bitmap som helst.

### Min tabell har sammanslagna celler. Kommer de att bevaras?

Sammanslagna celler behandlas som separata kolumner i CSV‑utdata eftersom CSV inte stödjer sammanslagning. Om du behöver rikare formatering (t.ex. Excel med sammanslagna celler), använd `SaveXls` istället:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### Detekteringen missade en kolumn. Hur kan jag förbättra noggrannheten?

- Öka bildens upplösning (≥300 dpi är idealiskt).
- Förbehandla bilden: konvertera till gråskala, öka kontrast, eller applicera ett deskew‑filter.
- Justera Aspose OCR‑inställningar som `PageSegMode` eller `Language` om tabellen innehåller icke‑latinska tecken.

### Kan jag extrahera tabeller direkt från en PDF?

Ja. Konvertera varje PDF‑sida till en bild först (med `Aspose.PDF` eller något PDF‑till‑bild‑bibliotek), och mata sedan in dessa bilder i samma arbetsflöde.

## Tips för produktionsklara implementationer

1. **Wrap OCR in a try/catch** – nätverkslicensierade miljöer kan kasta licensundantag.
2. **Dispose of `Image` objects** – omslut dem i `using`‑block för att frigöra inhemska resurser.
3. **Log the confidence scores** – `TableExtractor` exponerar `Table.Confidence` som du kan lagra för kvalitetsövervakning.
4. **Batch processing** – När du hanterar hundratals fakturor, parallellisera OCR‑anropen men respektera licensens trådsäkerhetsriktlinjer.

## Nästa steg

Nu när du vet **how to extract tables** från bilder, kanske du vill utforska:

- **Detect tables in image** videos (använda Aspose’s `TableExtractor` på varje bildruta).
- **Load image for OCR** från ett web‑API, vilket möjliggör molnbaserade tabellutdragningstjänster.
- **Extract tables from PNG**‑filer lagrade i Azure Blob Storage, integrerat med Azure Functions för serverlös bearbetning.

Känn dig fri att experimentera med olika filformat, justera OCR‑inställningarna, eller skicka CSV‑utdata direkt till en databas. Himlen är gränsen.

*Lycklig kodning! Om du stöter på problem eller har idéer för förbättringar, lämna en kommentar nedan. Vi löser det tillsammans.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}