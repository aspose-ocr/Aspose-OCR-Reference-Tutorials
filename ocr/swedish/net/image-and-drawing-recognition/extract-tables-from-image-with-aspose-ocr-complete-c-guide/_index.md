---
category: general
date: 2026-05-31
description: Extrahera tabeller från en bild med Aspose OCR i C#. Lär dig hur du konverterar
  en bild till en tabell, aktiverar tabelligenkänning och effektivt visar resultat.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: sv
og_description: Extrahera tabeller från bild med Aspose OCR. Denna guide visar hur
  du konverterar en bild till en tabell, aktiverar tabellidentifiering och hanterar
  resultaten i C#.
og_title: Extrahera tabeller från bild – Steg‑för‑steg C#‑handledning
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: Extrahera tabeller från bild med Aspose OCR – Komplett C#‑guide
url: /sv/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrahera tabeller från bild – Komplett C#‑guide

Har du någonsin behövt **extrahera tabeller från bild** men varit osäker på var du ska börja? Du är inte ensam; många utvecklare stöter på detta hinder när de försöker omvandla skannade fakturor eller kvitton till användbara data. Den goda nyheten? Med Aspose OCR kan du **konvertera bild till tabell** med bara några rader C#‑kod.

I den här handledningen går vi igenom ett verkligt exempel: vi laddar en PNG som innehåller en tabell, omvandlar den visuella layouten till ett strukturerat rutnät och skriver ut varje cells innehåll med förtroendesiffror. När du är klar har du ett fullt fungerande kodexempel som du kan klistra in i vilket .NET‑projekt som helst, samt tips för att hantera kantfall och skala lösningen.

## Vad du behöver

Innan vi dyker ner, se till att du har:

- **.NET 6.0** eller senare (koden fungerar även med .NET Framework 4.6+)
- **Aspose.OCR** NuGet‑paket (`Install-Package Aspose.OCR`)
- En bildfil som faktiskt innehåller en tabell (t.ex. `invoice_with_table.png`)
- En grundläggande C#‑IDE (Visual Studio, Rider eller VS Code med C#‑tillägget)

Det är allt—inga extra OCR‑motorer, inga tunga beroenden. Är du redo? Låt oss köra.

## Steg 1: Initiera OCR‑motorn för att **extrahera tabeller från bild**

Först skapar vi en `OcrEngine`‑instans och pekar den på vår källbild. Tänk på motorn som hjärnan som läser varje pixel och försöker förstå layouten.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **Varför detta är viktigt:** Utan korrekt initiering har OCR‑motorn inget att analysera, och du får aldrig några tabeller ur bilden. Anropet `ImageStream.FromFile` tar också hand om vanliga formatproblem (PNG, JPEG, BMP) så du behöver inga extra konverteringssteg.

## Steg 2: Aktivera tabellidentifiering – Nyckeln till **konvertera bild till tabell**

Aspose OCR kan läsa vanlig text från en bild, men den förstår inte automatiskt rader och kolumner om du inte instruerar den att leta efter tabeller. Här kommer flaggan `DetectTables` in.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Pro tip:** Om du bara behöver råtext, låt `DetectTables` vara `false`. Att aktivera den ger en liten extra belastning, men resultatet blir en ren, strukturerad data som du kan föra direkt in i ett kalkylblad eller en databas.

## Steg 3: Utför OCR‑igenkänning – Sanningsögonblicket

Nu ber vi motorn att faktiskt läsa bilden. Metoden `Recognize` returnerar ett `OcrResult`‑objekt som innehåller både vanlig text och eventuella identifierade tabeller.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **Vad händer under huven?** Aspose kör en rad bildförbehandlingssteg (räta upp, binarisering) innan den applicerar sin neurala‑nätverks‑baserade textigenkänning. När `DetectTables` är true körs även ett layout‑analyssteg som grupperar tecken i rader och kolumner.

## Steg 4: Iterera genom identifierade tabeller – **extrahera tabeller från bild** i praktiken

Om motorn hittar några tabeller kommer de att finnas i `result.Tables`. Vi loopar igenom varje tabell, sedan varje rad och kolumn, och skriver ut celltexten samt förtroendeprocenten.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **Varför kontrollera förtroende?** OCR är inte perfekt, särskilt med lågupplösta skanningar. Värdet `Confidence` (0‑100) låter dig avgöra om du ska acceptera cellen som den är eller flagga den för manuell granskning. En vanlig tröskel är 80 % för kritiska data.

### Förväntad utdata

Om källbilden innehåller en 3 × 4‑tabell med fakturarader kan du se något liknande:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Om inga tabeller identifieras blir `result.Tables` tomt—inget att skriva ut, men programmet avslutas ändå på ett kontrollerat sätt.

## Steg 5: Hantera kantfall och vanliga fallgropar

### Lågupplösta bilder

När din källbild är under 150 dpi kan tabellidentifieringsalgoritmen missa cellgränser. En snabb lösning är att förstora bilden med `System.Drawing` innan du skickar den till Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Snedvridna tabeller

Om tabellen är roterad några grader, aktivera automatisk räta upp:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Flera tabeller på en sida

Aspose OCR returnerar varje tabell som ett separat objekt i `result.Tables`. Du kan behandla dem individuellt, eller slå ihop dem till ett enda `DataTable` om du behöver en enhetlig vy.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### Export till Excel

När du har ett `DataTable` är export till en `.xlsx`‑fil en barnlek med `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Nu har du verkligen **konverterat bild till tabell** och kan leverera kalkylbladet till efterföljande processer.

## Fullt fungerande exempel – Från början till slut

Nedan är det kompletta, körklara programmet som samlar allt. Klistra in det i ett nytt konsolprojekt, ersätt filsökvägen och tryck **F5**.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**Förklaring av flödet**

1. **Motorinställning** – Laddar bilden och talar om för Aspose att leta efter tabeller.
2. **Alternativjustering** – `DetectTables` gör det tunga arbetet; `Deskew` förbättrar noggrannheten på snedvridna skanningar.
3. **Igenkänning** – Returnerar både vanlig text och en samling `Table`‑objekt.
4. **Iteration** – Skriver ut varje cell med förtroende, samtidigt som en `DataTable` byggs för senare export.
5. **Export** – Använder `ClosedXML` (ett lättviktigt, utan interop‑bibliotek) för att skriva en `.xlsx`‑fil—perfekt för efterföljande analys eller rapportering.

## Vanliga frågor

- **Fungerar detta med PDF‑filer?**  
  Ja. Konvertera varje PDF‑sida till en bild först (`PdfRenderer` eller `Ghostscript`), och skicka sedan bitmapen till Aspose OCR.

- **Kan jag extrahera tabeller från en JPG?**  
  Absolut. Metoden `ImageStream.FromFile` accepterar JPEG, PNG, BMP och TIFF direkt.

- **Vad händer om min tabell har sammanslagna celler?**  
  Aspose OCR behandlar sammanslagna celler som separata logiska celler; du kan behöva efterbearbeta resultatet för att slå ihop dem baserat på förtroende eller innehållsmönster.

- **Finns det någon gräns för tabellstorlek?**  
  Praktiskt hanterar motorn tabeller med flera hundra rader. Prestandan minskar linjärt, så överväg att dela upp mycket stora skanningar.

## Avslutning

Vi har precis visat dig hur du

## Vad bör du lära dig härnäst?

- [Hur man extraherar tabell från bild med Aspose.OCR för .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Extrahera text från bild – OCR‑optimering med Aspose.OCR för .NET](/ocr/english/net/ocr-optimization/)
- [Hur man extraherar text från bild genom att förbereda rektanglar i OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}