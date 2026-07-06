---
category: general
date: 2026-03-28
description: Μάθετε πώς να εξάγετε πίνακες από εικόνες με το Aspose OCR σε C#. Αυτός
  ο οδηγός καλύπτει πώς να εντοπίζετε πίνακες σε εικόνα, να φορτώνετε την εικόνα για
  OCR και να εξάγετε πίνακες από αρχεία PNG.
draft: false
keywords:
- how to extract tables
- extract table from image
- detect tables in image
- load image for ocr
- extract tables from png
language: el
og_description: Βήμα-βήμα οδηγός για το πώς να εξάγετε πίνακες από εικόνες με το Aspose
  OCR σε C#. Περιλαμβάνει κώδικα, εξηγήσεις και συμβουλές για την ανίχνευση πινάκων
  σε αρχεία εικόνας.
og_title: Πώς να εξάγετε πίνακες από εικόνες χρησιμοποιώντας το Aspose OCR (C#)
tags:
- Aspose OCR
- C#
- Table Extraction
title: Πώς να εξάγετε πίνακες από εικόνες χρησιμοποιώντας το Aspose OCR (C#)
url: /el/net/image-and-drawing-recognition/how-to-extract-tables-from-images-using-aspose-ocr-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εξάγετε Πίνακες από Εικόνες χρησιμοποιώντας το Aspose OCR (C#)

Έχετε αναρωτηθεί ποτέ **πώς να εξάγετε πίνακες** από ένα σαρωμένο τιμολόγιο ή ένα στιγμιότυπο οθόνης ενός υπολογιστικού φύλλου; Δεν είστε ο μόνος. Σε πολλά πραγματικά έργα πρέπει να μετατρέψουμε μια εικόνα πίνακα σε κάτι που μπορούμε να ερωτήσουμε—συνήθως ένα CSV ή ένα DataTable. Τα καλά νέα; Το Aspose OCR το κάνει παιχνιδάκι, και μπορείτε να το κάνετε με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία: από **load image for OCR**, μέχρι **detect tables in image**, και τελικά **extract table from image** και αποθήκευση ως αρχείο CSV. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που μπορεί να **extract tables from PNG** αρχεία (ή οποιοδήποτε υποστηριζόμενο bitmap) χωρίς καμία δυσκολία.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί και με .NET Framework)
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε)
- Ένα αρχείο άδειας Aspose.OCR για .NET (μπορείτε να ξεκινήσετε με δωρεάν δοκιμή)
- Μια δείγμα εικόνας που περιέχει πίνακα (π.χ., `invoice_table.png`)

Αν κάτι από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—απλώς εγκαταστήστε το .NET SDK και κατεβάστε το πακέτο NuGet, και θα είστε έτοιμοι.

## Επισκόπηση της Λύσης

Σε υψηλό επίπεδο η ροή εργασίας φαίνεται ως εξής:

1. **Load the image** που θέλετε να επεξεργαστείτε.
2. **Run OCR recognition** ώστε η μηχανή να γνωρίζει πού βρίσκεται το κείμενο.
3. **Create a TableExtractor** που σαρώει τα αποτελέσματα OCR για δομές τύπου πλέγματος.
4. **Extract all detected tables** και επιλέξτε αυτόν που χρειάζεστε.
5. **Save the table** ως CSV (ή οποιαδήποτε άλλη μορφή προτιμάτε).

Κάθε βήμα εξηγείται λεπτομερώς παρακάτω, με πλήρη αποσπάσματα κώδικα που μπορείτε να αντιγράψετε‑επικολλήσετε.

<img src="table_extraction_example.png" alt="πώς να εξάγετε πίνακες από εικόνα παράδειγμα" width="600">

*(Η παραπάνω εικόνα δείχνει ένα δείγμα πίνακα τιμολογίου που θα εξάγουμε.)*

## Βήμα 1 – Φόρτωση της Εικόνας για OCR

Το πρώτο πράγμα που πρέπει να κάνετε είναι να πείτε στο Aspose OCR ποιο αρχείο να διαβάσει. Η βιβλιοθήκη υποστηρίζει PNG, JPEG, BMP, TIFF, και μερικές άλλες μορφές. Ακολουθεί ο ελάχιστος κώδικας:

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

**Γιατί αυτό είναι σημαντικό:**  
`Image.FromFile` κάνει το βαριά έργο της αποκωδικοποίησης του PNG (ή οποιουδήποτε άλλου bitmap) σε μορφή που μπορεί να καταλάβει η μηχανή OCR. Αν παραλείψετε αυτό το βήμα ή περάσετε ένα κατεστραμμένο αρχείο, η επόμενη κλήση `Recognize()` θα ρίξει εξαίρεση.

> **Pro tip:** Αν εργάζεστε με μεγάλα PDF, εξάγετε κάθε σελίδα ως εικόνα πρώτα—διαφορετικά η μηχανή OCR θα εξαντλήσει τη μνήμη.

## Βήμα 2 – Αναγνώριση της Σελίδας (Απαιτείται Πριν από την Ανίχνευση Πίνακα)

Η αναγνώριση μετατρέπει τα ακατέργαστα δεδομένα pixel σε μια αναζητήσιμη διάταξη κειμένου. Χωρίς αυτό το βήμα το `TableExtractor` δεν έχει τίποτα με το οποίο να δουλέψει.

```csharp
// Perform OCR recognition – this populates internal structures
ocrEngine.Recognize();
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose OCR εκτελεί έναν εντοπιστή κειμένου βασισμένο σε νευρωνικό δίκτυο, στη συνέχεια δημιουργεί μια ιεραρχία αντικειμένων `Page`, `Paragraph`, και `Word`. Ο εντοπιστής πίνακα εξετάζει αργότερα τις χωρικές σχέσεις μεταξύ αυτών των λέξεων.

Αν επεξεργάζεστε πολλές εικόνες σε βρόχο, σκεφτείτε να επαναχρησιμοποιήσετε το ίδιο αντικείμενο `OcrEngine` και απλώς να αλλάζετε την ιδιότητα `Image`—αυτό μειώνει το κόστος κατανομής.

## Βήμα 3 – Δημιουργία TableExtractor και Ανίχνευση Πινάκων στην Εικόνα

Τώρα που τα δεδομένα OCR υπάρχουν, μπορούμε να ζητήσουμε από το Aspose να βρει πίνακες. Η κλάση `TableExtractor` κάνει ακριβώς αυτό.

```csharp
using Aspose.OCR.Table;

// ...

// Initialize the TableExtractor with the recognized engine
var tableExtractor = new TableExtractor(ocrEngine);

// Extract all tables detected on the page
List<Table> extractedTables = tableExtractor.ExtractAll();
```

**Γιατί να χρησιμοποιήσετε το `ExtractAll()`;**  
Μια μόνο εικόνα μπορεί να περιέχει πολλαπλούς πίνακες (σκεφτείτε μια αναφορά με πολλαπλές ενότητες). Το `ExtractAll()` επιστρέφει μια `List<Table>` ώστε να μπορείτε να επαναλάβετε, να επιλέξετε το σωστό ή ακόμη και να τα συγχωνεύσετε αργότερα.

Αν χρειάζεστε μόνο τον πρώτο πίνακα, μπορείτε με ασφάλεια να χρησιμοποιήσετε `extractedTables[0]`, αλλά πάντα να ελέγχετε αν η λίστα είναι κενή για να αποφύγετε `IndexOutOfRangeException`.

```csharp
if (extractedTables.Count == 0)
{
    Console.WriteLine("No tables were detected. Check the image quality or try adjusting OCR settings.");
    return;
}
```

## Βήμα 4 – Αποθήκευση του Εξαγόμενου Πίνακα ως CSV (ή οποιαδήποτε άλλη μορφή)

Το Aspose κάνει την εξαγωγή απλή. Η κλάση `Table` διαθέτει ενσωματωμένες μεθόδους `SaveCsv`, `SaveXls`, και `SaveJson`. Ακολουθεί πώς να γράψετε ένα αρχείο CSV:

```csharp
// Save the first detected table to CSV
string outputPath = @"C:\Output\invoice_table.csv";
extractedTables[0].SaveCsv(outputPath);

Console.WriteLine($"Table extraction completed. CSV saved to {outputPath}");
```

**Πώς φαίνεται το CSV;**  
Υποθέτοντας ότι η εικόνα προέλευσης περιείχε ένα πλέγμα 4 × 3, το CSV μπορεί να εμφανιστεί ως:

```
Item,Quantity,Price
Widget A,2,19.99
Widget B,5,9.50
Service C,1,150.00
```

Μπορείτε να ανοίξετε αυτό το αρχείο στο Excel, Power BI, ή να το τροφοδοτήσετε απευθείας στη γραμμή δεδομένων σας.

## Πλήρες Παράδειγμα Από Αρχή έως Τέλος

Παρακάτω είναι το πλήρες, αυτόνομο πρόγραμμα. Αντιγράψτε το σε ένα νέο έργο console (`dotnet new console`) και εκτελέστε το. Βεβαιωθείτε ότι το πακέτο NuGet `Aspose.OCR` είναι εγκατεστημένο (`dotnet add package Aspose.OCR`).

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

### Αναμενόμενο Αποτέλεσμα

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
Table extraction completed. CSV saved at: C:\Output\invoice_table.csv
```

Ανοίξτε το `invoice_table.csv` και θα βρείτε τις γραμμές και στήλες που αντικατοπτρίζουν την αρχική εικόνα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν η εικόνα είναι JPEG αντί για PNG;

Ο ίδιος κώδικας λειτουργεί—απλώς αλλάξτε την επέκταση αρχείου στο `Image.FromFile`. Το Aspose OCR ανιχνεύει αυτόματα τη μορφή, έτσι το **extract tables from png** δεν είναι αυστηρή απαίτηση· λειτουργεί με οποιοδήποτε υποστηριζόμενο bitmap.

### Ο πίνακάς μου έχει συγχωνευμένα κελιά. Θα διατηρηθούν;

Τα συγχωνευμένα κελιά αντιμετωπίζονται ως ξεχωριστές στήλες στην έξοδο CSV επειδή το CSV δεν υποστηρίζει ενοποίηση. Αν χρειάζεστε πιο πλούσια μορφοποίηση (π.χ., Excel με συγχωνευμένα κελιά), χρησιμοποιήστε το `SaveXls` αντί αυτού:

```csharp
extractedTables[0].SaveXls(@"C:\Output\invoice_table.xls");
```

### Η ανίχνευση παρέλειψε μια στήλη. Πώς μπορώ να βελτιώσω την ακρίβεια;

- Αυξήστε την ανάλυση της εικόνας (≥300 dpi είναι ιδανικό).
- Προεπεξεργαστείτε την εικόνα: μετατρέψτε σε κλίμακα του γκρι, αυξήστε την αντίθεση, ή εφαρμόστε φίλτρο ευθυγράμμισης.
- Ρυθμίστε τις ρυθμίσεις Aspose OCR όπως `PageSegMode` ή `Language` αν ο πίνακας περιέχει μη λατινικούς χαρακτήρες.

### Μπορώ να εξάγω πίνακες απευθείας από PDF;

Ναι. Μετατρέψτε κάθε σελίδα PDF σε εικόνα πρώτα (χρησιμοποιώντας `Aspose.PDF` ή οποιαδήποτε βιβλιοθήκη PDF‑σε‑εικόνα), έπειτα τροφοδοτήστε αυτές τις εικόνες στην ίδια ροή εργασίας.

## Συμβουλές για Παραγωγικές Υλοποιήσεις

1. **Wrap OCR in a try/catch** – τα περιβάλλοντα με δικαίωμα δικτύου μπορούν να ρίξουν εξαιρέσεις αδειών.
2. **Dispose of `Image` objects** – τυλίξτε τα σε μπλοκ `using` για να ελευθερώσετε τους εγγενείς πόρους.
3. **Log the confidence scores** – το `TableExtractor` εκθέτει `Table.Confidence` που μπορείτε να αποθηκεύσετε για παρακολούθηση ποιότητας.
4. **Batch processing** – Όταν επεξεργάζεστε εκατοντάδες τιμολόγια, παραλληλοποιήστε τις κλήσεις OCR αλλά σεβαστείτε τις οδηγίες ασφαλείας νήματος της άδειας.

## Επόμενα Βήματα

Τώρα που γνωρίζετε **πώς να εξάγετε πίνακες** από εικόνες, ίσως θέλετε να εξερευνήσετε:

- **Detect tables in image** βίντεο (χρησιμοποιώντας το `TableExtractor` του Aspose σε κάθε καρέ).
- **Load image for OCR** από ένα web API, επιτρέποντας υπηρεσίες εξαγωγής πινάκων βασισμένες στο cloud.
- **Extract tables from PNG** αρχεία αποθηκευμένα στο Azure Blob Storage, ενσωματώνοντας με Azure Functions για serverless επεξεργασία.

Νιώστε ελεύθεροι να πειραματιστείτε με διαφορετικές μορφές αρχείων, να ρυθμίσετε τις ρυθμίσεις OCR, ή να διοχετεύσετε την έξοδο CSV απευθείας σε μια βάση δεδομένων. Ο ουρανός είναι το όριο.

---

*Καλό κώδικα! Αν συναντήσετε προβλήματα ή έχετε ιδέες για βελτίωση, αφήστε ένα σχόλιο παρακάτω. Θα το λύσουμε μαζί.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}