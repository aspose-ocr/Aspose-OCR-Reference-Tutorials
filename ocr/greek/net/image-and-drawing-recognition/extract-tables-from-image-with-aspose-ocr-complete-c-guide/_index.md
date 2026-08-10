---
category: general
date: 2026-05-31
description: Εξαγωγή πινάκων από εικόνα χρησιμοποιώντας Aspose OCR σε C#. Μάθετε πώς
  να μετατρέπετε την εικόνα σε πίνακα, να ενεργοποιείτε την ανίχνευση πινάκων και
  να εξάγετε τα αποτελέσματα αποδοτικά.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: el
og_description: Εξαγωγή πινάκων από εικόνα με το Aspose OCR. Αυτός ο οδηγός δείχνει
  πώς να μετατρέψετε την εικόνα σε πίνακα, να ενεργοποιήσετε την ανίχνευση πινάκων
  και να διαχειριστείτε τα αποτελέσματα σε C#.
og_title: Εξαγωγή πινάκων από εικόνα – Βήμα‑βήμα εκπαίδευση C#
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
title: Εξαγωγή πινάκων από εικόνα με Aspose OCR – Πλήρης οδηγός C#
url: /el/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Πινάκων από Εικόνα – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **εξάγετε πίνακες από εικόνα** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν προσπαθούν να μετατρέψουν σαρωμένα τιμολόγια ή αποδείξεις σε χρησιμοποιήσιμα δεδομένα. Τα καλά νέα; Με το Aspose OCR μπορείτε να **μετατρέψετε εικόνα σε πίνακα** με λίγες μόνο γραμμές κώδικα C#.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα: φόρτωση ενός PNG που περιέχει πίνακα, μετατροπή της οπτικής διάταξης σε δομημένο πλέγμα και εκτύπωση του περιεχομένου κάθε κελιού με ποσοστά εμπιστοσύνης. Στο τέλος θα έχετε ένα πλήρως λειτουργικό snippet που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project, μαζί με συμβουλές για την αντιμετώπιση ακραίων περιπτώσεων και την κλιμάκωση της λύσης.

## Τι Θα Χρειαστείτε

- **.NET 6.0** ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)
- **Aspose.OCR** πακέτο NuGet (`Install-Package Aspose.OCR`)
- Ένα αρχείο εικόνας που περιέχει πραγματικά έναν πίνακα (π.χ., `invoice_with_table.png`)
- Ένα βασικό IDE για C# (Visual Studio, Rider ή VS Code με την επέκταση C#)

Αυτό είναι όλο—χωρίς επιπλέον μηχανές OCR, χωρίς βαριές εξαρτήσεις. Έτοιμοι; Ας ξεκινήσουμε.

## Βήμα 1: Αρχικοποίηση του OCR Engine για **Εξαγωγή Πινάκων από Εικόνα**

Πρώτα, δημιουργούμε μια παρουσία `OcrEngine` και την κατευθύνουμε στην πηγή εικόνας μας. Σκεφτείτε το engine ως τον εγκέφαλο που θα διαβάσει κάθε pixel και θα προσπαθήσει να καταλάβει τη διάταξη.

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

> **Why this matters:** Χωρίς σωστή αρχικοποίηση του engine, το OCR engine δεν έχει τίποτα να αναλύσει και δεν θα πάρετε ποτέ πίνακες από την εικόνα. Η κλήση `ImageStream.FromFile` φροντίζει επίσης για κοινά προβλήματα μορφής (PNG, JPEG, BMP) ώστε να μην χρειάζεστε επιπλέον βήματα μετατροπής.

## Βήμα 2: Ενεργοποίηση Ανίχνευσης Πινάκων – Το Κλειδί για **Μετατροπή Εικόνας σε Πίνακα**

Το Aspose OCR μπορεί να διαβάσει απλό κείμενο από μια εικόνα, αλλά δεν θα καταλάβει αυτόματα σειρές και στήλες εκτός αν του πείτε να ψάξει για πίνακες. Εδώ μπαίνει σε δράση η σημαία `DetectTables`.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **Pro tip:** Αν χρειάζεστε μόνο ακατέργαστο κείμενο, αφήστε το `DetectTables` σε `false`. Η ενεργοποίησή του προσθέτει μικρό κόστος, αλλά το αποτέλεσμα είναι ένα καθαρό, δομημένο αποτέλεσμα που μπορείτε να τροφοδοτήσετε απευθείας σε ένα spreadsheet ή βάση δεδομένων.

## Βήμα 3: Εκτέλεση OCR Αναγνώρισης – Η Στιγμή της Αλήθειας

Τώρα ζητάμε από το engine να διαβάσει πραγματικά την εικόνα. Η μέθοδος `Recognize` επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει τόσο το απλό κείμενο όσο και τυχόν ανιχνευμένους πίνακες.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **What happens under the hood?** Το Aspose εκτελεί μια σειρά βημάτων προεπεξεργασίας εικόνας (απλοποίηση κλίσης, δυαδικοποίηση) πριν εφαρμόσει τον αναγνώστη κειμένου βασισμένο σε νευρωνικά δίκτυα. Όταν το `DetectTables` είναι true, εκτελεί επίσης μια ανάλυση διάταξης που ομαδοποιεί χαρακτήρες σε σειρές και στήλες.

## Βήμα 4: Επανάληψη μέσω των Ανιχνευμένων Πινάκων – **Εξαγωγή Πινάκων από Εικόνα** σε Δράση

Αν το engine βρει πίνακες, θα εμφανιστούν στο `result.Tables`. Θα διασχίσουμε κάθε πίνακα, μετά κάθε σειρά και στήλη, εκτυπώνοντας το κείμενο του κελιού και το ποσοστό εμπιστοσύνης.

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

> **Why check confidence?** Το OCR δεν είναι τέλειο, ειδικά με σαρώσεις χαμηλής ανάλυσης. Η τιμή `Confidence` (0‑100) σας επιτρέπει να αποφασίσετε αν θα αποδεχτείτε το κελί όπως είναι ή θα το σημαδέψετε για χειροκίνητη επανεξέταση. Ένα τυπικό όριο είναι το 80 % για κρίσιμα δεδομένα.

### Αναμενόμενο Αποτέλεσμα

Υποθέτοντας ότι η πηγή εικόνας περιέχει έναν πίνακα 3 × 4 με στοιχεία τιμολογίου, μπορεί να δείτε κάτι τέτοιο:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

Αν δεν ανιχνευτούν πίνακες, το `result.Tables` θα είναι κενό—δεν υπάρχει τίποτα για εκτύπωση, αλλά το πρόγραμμα θα τερματιστεί ομαλά.

## Βήμα 5: Διαχείριση Ακραίων Περιπτώσεων και Συνηθισμένων Παγίδων

### Εικόνες Χαμηλής Ανάλυσης

Όταν η πηγή εικόνα είναι κάτω από 150 dpi, ο αλγόριθμος ανίχνευσης πινάκων μπορεί να χάσει τα όρια των κελιών. Μια γρήγορη λύση είναι η αύξηση της ανάλυσης της εικόνας χρησιμοποιώντας `System.Drawing` πριν τη δώσετε στο Aspose:

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### Πίνακες με Κλίση

Αν ο πίνακας είναι περιστραμμένος ακόμη και λίγους μοίρους, ενεργοποιήστε το auto‑deskew:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### Πολλαπλοί Πίνακες σε Μία Σελίδα

Το Aspose OCR επιστρέφει κάθε πίνακα ως ξεχωριστό αντικείμενο στο `result.Tables`. Μπορείτε να τους χειριστείτε ξεχωριστά ή να τους συγχωνεύσετε σε ένα ενιαίο `DataTable` αν χρειάζεστε ενοποιημένη προβολή.

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

### Εξαγωγή σε Excel

Μόλις έχετε ένα `DataTable`, η εξαγωγή σε αρχείο `.xlsx` είναι παιχνιδάκι με το `ClosedXML`:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

Τώρα έχετε πραγματικά **μετατρέψει εικόνα σε πίνακα** και μπορείτε να παραδώσετε το spreadsheet σε επόμενες διαδικασίες.

## Πλήρες Παράδειγμα Εργασίας – Από την Αρχή μέχρι το Τέλος

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενώνει όλα τα παραπάνω. Επικολλήστε το σε ένα νέο console project, αντικαταστήστε τη διαδρομή του αρχείου και πατήστε **F5**.

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

**Επεξήγηση της ροής**

1. **Engine setup** – Φορτώνει την εικόνα και λέει στο Aspose να ψάξει για πίνακες.  
2. **Options tuning** – Το `DetectTables` κάνει το σκληρό κομμάτι· το `Deskew` βελτιώνει την ακρίβεια σε κεκλιμένες σαρώσεις.  
3. **Recognition** – Επιστρέφει τόσο το απλό κείμενο όσο και μια συλλογή αντικειμένων `Table`.  
4. **Iteration** – Εκτυπώνει κάθε κελί με την εμπιστοσύνη, ενώ ταυτόχρονα δημιουργεί ένα `DataTable` για μελλοντική εξαγωγή.  
5. **Export** – Χρησιμοποιεί το `ClosedXML` (μια ελαφριά, χωρίς interop βιβλιοθήκη) για να γράψει ένα αρχείο `.xlsx`—ιδανικό για downstream analytics ή reporting.

## Συχνές Ερωτήσεις

- **Does this work with PDFs?**  
  Ναι. Μετατρέψτε πρώτα κάθε σελίδα PDF σε εικόνα (`PdfRenderer` ή `Ghostscript`), μετά δώστε το bitmap στο Aspose OCR.

- **Can I extract tables from a JPG?**  
  Απόλυτα. Η μέθοδος `ImageStream.FromFile` δέχεται JPEG, PNG, BMP και TIFF αμέσως.

- **What if my table has merged cells?**  
  Το Aspose OCR αντιμετωπίζει τα συγχωνευμένα κελιά ως ξεχωριστά λογικά κελιά· ίσως χρειαστεί να επεξεργαστείτε το αποτέλεσμα για να τα συνδυάσετε βάσει εμπιστοσύνης ή προτύπων περιεχομένου.

- **Is there a limit on table size?**  
  Πρακτικά, το engine διαχειρίζεται πίνακες μέχρι μερικές εκατοντάδες σειρές. Η απόδοση μειώνεται γραμμικά, οπότε σκεφτείτε να χωρίσετε πολύ μεγάλες σαρώσεις σε τμήματα.

## Συμπεράσματα

Μόλις σας δείξαμε πώς να

## Τι Θα Πρέπει να Μάθετε Στη Σειρά;

- [Πώς να εξάγετε πίνακα από εικόνα χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Προετοιμάζοντας Ορθογώνια στο OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}