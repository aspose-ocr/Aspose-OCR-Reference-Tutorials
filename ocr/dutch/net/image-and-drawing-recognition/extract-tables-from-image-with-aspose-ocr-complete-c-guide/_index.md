---
category: general
date: 2026-05-31
description: Tabellen extraheren uit een afbeelding met Aspose OCR in C#. Leer hoe
  je een afbeelding naar een tabel converteert, tabeldetectie inschakelt en resultaten
  efficiënt weergeeft.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: nl
og_description: Tabellen extraheren uit afbeelding met Aspose OCR. Deze gids laat
  zien hoe je een afbeelding naar een tabel converteert, tabeldetectie inschakelt
  en resultaten verwerkt in C#.
og_title: Tabellen uit afbeelding extraheren – Stapsgewijze C#‑handleiding
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
title: Tabellen extraheren uit afbeelding met Aspose OCR – Complete C#‑gids
url: /nl/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tabellen uit afbeelding extraheren – Complete C# gids

Heb je ooit **tabellen uit een afbeelding moeten extraheren** maar wist je niet waar te beginnen? Je bent niet de enige; veel ontwikkelaars lopen tegen dit probleem aan wanneer ze gescande facturen of bonnetjes willen omzetten naar bruikbare gegevens. Het goede nieuws? Met Aspose OCR kun je **een afbeelding naar een tabel converteren** in slechts een paar regels C#‑code.

In deze tutorial lopen we een real‑world voorbeeld door: een PNG laden die een tabel bevat, die visuele lay‑out omzetten naar een gestructureerd raster, en de inhoud van elke cel afdrukken met vertrouwensscores. Aan het einde heb je een volledig werkend fragment dat je in elk .NET‑project kunt plaatsen, plus tips voor het afhandelen van randgevallen en het schalen van de oplossing.

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

- **.NET 6.0** of later (de code werkt ook met .NET Framework 4.6+)
- **Aspose.OCR** NuGet‑pakket (`Install-Package Aspose.OCR`)
- Een afbeeldingsbestand dat daadwerkelijk een tabel bevat (bijv. `invoice_with_table.png`)
- Een basis C#‑IDE (Visual Studio, Rider, of VS Code met de C#‑extensie)

Dat is alles—geen extra OCR‑engines, geen zware afhankelijkheden. Klaar? Laten we aan de slag gaan.

## Stap 1: Initialiseert de OCR‑engine om **tabellen uit afbeelding te extraheren**

Eerst maken we een `OcrEngine`‑instantie en wijzen we deze op onze bronafbeelding. Beschouw de engine als het brein dat elke pixel leest en probeert de lay‑out te begrijpen.

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

> **Waarom dit belangrijk is:** Zonder de engine correct te initialiseren heeft de OCR‑engine niets om te analyseren, en krijg je nooit tabellen uit de afbeelding. De `ImageStream.FromFile`‑aanroep regelt ook veelvoorkomende formaatproblemen (PNG, JPEG, BMP) zodat je geen extra conversiestappen nodig hebt.

## Stap 2: Schakel tabeldetectie in – De sleutel tot **afbeelding naar tabel converteren**

Aspose OCR kan platte tekst uit een afbeelding lezen, maar begrijpt niet automatisch rijen en kolommen tenzij je het vraagt naar tabellen te zoeken. Hier komt de `DetectTables`‑vlag om de hoek kijken.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Pro tip:** Als je alleen ruwe tekst nodig hebt, laat `DetectTables` op `false`. Het inschakelen voegt een kleine overhead toe, maar het resultaat is een nette, gestructureerde output die je direct kunt invoeren in een spreadsheet of database.

## Stap 3: Voer OCR‑herkenning uit – Het moment van de waarheid

Nu vragen we de engine de afbeelding daadwerkelijk te lezen. De `Recognize`‑methode retourneert een `OcrResult`‑object dat zowel platte tekst als eventuele gedetecteerde tabellen bevat.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **Wat gebeurt er onder de motorkap?** Aspose voert een reeks beeld‑preprocessing stappen uit (deskewing, binarisatie) voordat het zijn neurale‑netwerk‑gebaseerde teksterkenner toepast. Wanneer `DetectTables` true is, wordt er ook een lay‑out‑analyse uitgevoerd die tekens groepeert in rijen en kolommen.

## Stap 4: Doorloop gedetecteerde tabellen – **Tabellen uit afbeelding extraheren** in actie

Als de engine tabellen heeft gevonden, verschijnen deze in `result.Tables`. We lopen elke tabel, vervolgens elke rij en kolom door, en printen de celtekst en het vertrouwenspercentage.

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

> **Waarom vertrouwensscore controleren?** OCR is niet perfect, vooral niet bij scans met lage resolutie. De `Confidence`‑waarde (0‑100) laat je beslissen of je de cel accepteert zoals hij is of markeert voor handmatige controle. Een typische drempel is 80 % voor kritieke data.

### Verwachte output

Als de bronafbeelding een 3 × 4‑tabel met factuurregels bevat, zie je mogelijk iets als:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Als er geen tabellen worden gedetecteerd, is `result.Tables` leeg—er is niets om af te drukken, maar het programma sluit wel netjes af.

## Stap 5: Randgevallen en veelvoorkomende valkuilen afhandelen

### Afbeeldingen met lage resolutie

Wanneer je bronafbeelding onder de 150 dpi ligt, kan het tabeldetectie‑algoritme celgrenzen missen. Een snelle oplossing is de afbeelding opschalen met `System.Drawing` voordat je deze aan Aspose doorgeeft:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Scheve tabellen

Als de tabel een paar graden gedraaid is, schakel auto‑deskew in:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Meerdere tabellen op één pagina

Aspose OCR retourneert elke tabel als een apart object in `result.Tables`. Je kunt ze afzonderlijk behandelen, of ze samenvoegen tot één `DataTable` als je een eenduidig overzicht nodig hebt.

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

### Exporteren naar Excel

Zodra je een `DataTable` hebt, is exporteren naar een `.xlsx`‑bestand een fluitje van een cent met `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Nu heb je echt **afbeelding naar tabel geconverteerd** en kun je de spreadsheet doorgeven aan downstream processen.

## Volledig werkend voorbeeld – Van begin tot eind

Hieronder staat het complete, kant‑klaar programma dat alles samenbrengt. Plak het in een nieuw console‑project, vervang het bestandspad, en druk op **F5**.

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

**Uitleg van de flow**

1. **Engine‑configuratie** – Laadt de afbeelding en vertelt Aspose om naar tabellen te zoeken.  
2. **Opties afstemmen** – `DetectTables` doet het zware werk; `Deskew` verbetert de nauwkeurigheid bij scheve scans.  
3. **Herkenning** – Retourneert zowel platte tekst als een collectie van `Table`‑objecten.  
4. **Iteratie** – Print elke cel met vertrouwensscore, terwijl ook een `DataTable` wordt opgebouwd voor later export.  
5. **Export** – Gebruikt `ClosedXML` (een lichte, geen‑interop bibliotheek) om een `.xlsx`‑bestand te schrijven—perfect voor downstream‑analyse of rapportage.

## Veelgestelde vragen

- **Werkt dit met PDF’s?**  
  Ja. Converteer eerst elke PDF‑pagina naar een afbeelding (`PdfRenderer` of `Ghostscript`), en geef de bitmap vervolgens aan Aspose OCR.

- **Kan ik tabellen uit een JPG extraheren?**  
  Absoluut. De `ImageStream.FromFile`‑methode accepteert JPEG, PNG, BMP en TIFF direct.

- **Wat als mijn tabel samengevoegde cellen heeft?**  
  Aspose OCR behandelt samengevoegde cellen als afzonderlijke logische cellen; je moet mogelijk de output post‑processen om ze te combineren op basis van vertrouwensscore of inhoudspatronen.

- **Is er een limiet aan de tabelgrootte?**  
  Praktisch gezien verwerkt de engine tabellen tot enkele honderden rijen. De prestaties nemen lineair af, dus overweeg het opsplitsen van zeer grote scans.

## Afronding

We hebben je net laten zien hoe je

## Wat moet je hierna leren?

- [Hoe een tabel uit een afbeelding te extraheren met Aspose.OCR voor .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Tekst uit afbeelding extraheren – OCR‑optimalisatie met Aspose.OCR voor .NET](/ocr/english/net/ocr-optimization/)
- [Hoe tekst uit een afbeelding te extraheren door rechthoeken voor OCR voor te bereiden](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}