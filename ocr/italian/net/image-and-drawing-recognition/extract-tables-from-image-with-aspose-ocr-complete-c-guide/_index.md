---
category: general
date: 2026-05-31
description: Estrai tabelle da un'immagine usando Aspose OCR in C#. Scopri come convertire
  l'immagine in tabella, abilitare il rilevamento delle tabelle e ottenere i risultati
  in modo efficiente.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: it
og_description: Estrai tabelle da un'immagine con Aspose OCR. Questa guida mostra
  come convertire l'immagine in tabella, abilitare il rilevamento delle tabelle e
  gestire i risultati in C#.
og_title: Estrai tabelle da immagine – Tutorial C# passo passo
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
title: Estrai tabelle da immagine con Aspose OCR – Guida completa C#
url: /it/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Estrarre tabelle da immagine – Guida completa in C#

Ti è mai capitato di dover **estrarre tabelle da immagine** senza sapere da dove cominciare? Non sei l’unico; molti sviluppatori incontrano questo ostacolo quando cercano di trasformare fatture o ricevute scannerizzate in dati utilizzabili. La buona notizia? Con Aspose OCR puoi **convertire immagine in tabella** in poche righe di codice C#.

In questo tutorial percorreremo un esempio reale: caricare un PNG che contiene una tabella, trasformare quel layout visivo in una griglia strutturata e stampare il contenuto di ogni cella con i relativi punteggi di confidenza. Alla fine avrai uno snippet completamente funzionante da inserire in qualsiasi progetto .NET, oltre a consigli per gestire casi particolari e scalare la soluzione.

## Cosa ti servirà

Prima di immergerci, assicurati di avere:

- **.NET 6.0** o versioni successive (il codice funziona anche con .NET Framework 4.6+)
- Pacchetto NuGet **Aspose.OCR** (`Install-Package Aspose.OCR`)
- Un file immagine che contenga effettivamente una tabella (ad es. `invoice_with_table.png`)
- Un IDE C# di base (Visual Studio, Rider o VS Code con l’estensione C#)

Tutto qui—nessun motore OCR aggiuntivo, nessuna dipendenza pesante. Pronto? Iniziamo.

## Passo 1: Inizializzare il motore OCR per **estrarre tabelle da immagine**

Per prima cosa creiamo un’istanza di `OcrEngine` e la puntiamo all’immagine di origine. Pensa al motore come al cervello che leggerà ogni pixel e cercherà di interpretare il layout.

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

> **Perché è importante:** Senza inizializzare correttamente il motore, l’OCR non ha nulla da analizzare e non otterrai alcuna tabella dall’immagine. La chiamata `ImageStream.FromFile` gestisce anche i problemi di formato più comuni (PNG, JPEG, BMP) così non servono passaggi di conversione aggiuntivi.

## Passo 2: Abilitare il rilevamento delle tabelle – La chiave per **convertire immagine in tabella**

Aspose OCR può leggere testo semplice da un’immagine, ma non capirà automaticamente righe e colonne a meno che non gli chiedi di cercare le tabelle. Qui entra in gioco il flag `DetectTables`.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Consiglio esperto:** Se ti serve solo il testo grezzo, lascia `DetectTables` a `false`. Abilitandolo si aggiunge un piccolo overhead, ma il risultato è una struttura pulita e ordinata che puoi inviare direttamente a un foglio di calcolo o a un database.

## Passo 3: Eseguire il riconoscimento OCR – Il momento della verità

Ora chiediamo al motore di leggere effettivamente l’immagine. Il metodo `Recognize` restituisce un oggetto `OcrResult` che contiene sia il testo semplice sia le eventuali tabelle rilevate.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **Cosa succede dietro le quinte?** Aspose esegue una serie di passaggi di pre‑elaborazione dell’immagine (deskew, binarizzazione) prima di applicare il suo riconoscitore di testo basato su rete neurale. Quando `DetectTables` è true, esegue anche un’analisi del layout che raggruppa i caratteri in righe e colonne.

## Passo 4: Iterare sulle tabelle rilevate – **Estrarre tabelle da immagine** in azione

Se il motore ha trovato delle tabelle, appariranno in `result.Tables`. Scorreremo ogni tabella, poi ogni riga e colonna, stampando il testo della cella e la percentuale di confidenza.

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

> **Perché controllare la confidenza?** L’OCR non è perfetto, soprattutto con scansioni a bassa risoluzione. Il valore `Confidence` (0‑100) ti permette di decidere se accettare la cella così com’è o segnalarla per una revisione manuale. Una soglia tipica è l’80 % per dati critici.

### Output previsto

Supponendo che l’immagine di origine contenga una tabella 3 × 4 di voci di fattura, potresti vedere qualcosa di simile:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Se non vengono rilevate tabelle, `result.Tables` sarà vuoto—nulla da stampare, ma il programma terminerà comunque correttamente.

## Passo 5: Gestire casi particolari e problemi comuni

### Immagini a bassa risoluzione

Quando l’immagine di origine è inferiore a 150 dpi, l’algoritmo di rilevamento delle tabelle potrebbe non riconoscere i bordi delle celle. Una soluzione rapida è ingrandire l’immagine usando `System.Drawing` prima di passarla ad Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Tabelle inclinate

Se la tabella è ruotata anche solo di pochi gradi, abilita l’auto‑deskew:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Più tabelle in una pagina

Aspose OCR restituisce ogni tabella come un oggetto separato in `result.Tables`. Puoi gestirle singolarmente o unirle in un unico `DataTable` se ti serve una vista unificata.

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

### Esportare in Excel

Una volta ottenuto un `DataTable`, esportare in un file `.xlsx` è un gioco da ragazzi con `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Ora hai davvero **convertito immagine in tabella** e puoi consegnare il foglio di calcolo ai processi successivi.

## Esempio completo – Dal principio alla fine

Di seguito trovi il programma completo, pronto per essere eseguito. Copialo in un nuovo progetto console, sostituisci il percorso del file e premi **F5**.

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

**Spiegazione del flusso**

1. **Configurazione del motore** – Carica l’immagine e indica ad Aspose di cercare le tabelle.
2. **Messa a punto delle opzioni** – `DetectTables` fa il lavoro pesante; `Deskew` migliora la precisione su scansioni inclinate.
3. **Riconoscimento** – Restituisce sia il testo semplice sia una collezione di oggetti `Table`.
4. **Iterazione** – Stampa ogni cella con la relativa confidenza, costruendo al contempo un `DataTable` per l’esportazione.
5. **Esportazione** – Usa `ClosedXML` (una libreria leggera, senza interop) per scrivere un file `.xlsx`—perfetto per analisi o reportistica downstream.

## Domande frequenti

- **Funziona con i PDF?**  
  Sì. Converte prima ogni pagina PDF in immagine (`PdfRenderer` o `Ghostscript`), poi passa il bitmap ad Aspose OCR.

- **Posso estrarre tabelle da un JPG?**  
  Assolutamente. Il metodo `ImageStream.FromFile` accetta JPEG, PNG, BMP e TIFF nativamente.

- **Cosa succede se la mia tabella ha celle unite?**  
  Aspose OCR tratta le celle unite come celle logiche separate; potresti dover post‑processare l’output per combinarle in base a confidenza o pattern di contenuto.

- **Esiste un limite alla dimensione della tabella?**  
  Praticamente il motore gestisce tabelle fino a diverse centinaia di righe. Le prestazioni degradano linearmente, quindi valuta di suddividere scansioni molto grandi.

## Conclusioni

Ti abbiamo appena mostrato come


## Cosa dovresti imparare dopo?

- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}