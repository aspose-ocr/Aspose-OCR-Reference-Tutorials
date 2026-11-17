---
category: general
date: 2026-03-18
description: Εξαγωγή πίνακα από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να μετατρέψετε τον πίνακα σε JSON, να λάβετε το JSON του πίνακα και να εξάγετε
  κείμενο από την εικόνα σε λίγα λεπτά.
draft: false
keywords:
- extract table from image
- convert table to json
- convert image to json
- extract text from image
- get table json
language: el
og_description: Εξάγετε πίνακα από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να μετατρέψετε τον πίνακα σε JSON, να λάβετε το JSON του πίνακα και να εξάγετε
  κείμενο από την εικόνα γρήγορα.
og_title: Εξαγωγή πίνακα από εικόνα με το Aspose OCR – Πλήρης οδηγός C#
tags:
- Aspose OCR
- C#
- Table Extraction
title: Εξαγωγή Πίνακα από Εικόνα με Aspose OCR – Πλήρης Οδηγός C#
url: /el/net/text-recognition/extract-table-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Πίνακα από Εικόνα – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **extract table from image** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη μπορεί να το κάνει χωρίς ένα βουνό χειροκίνητης ανάλυσης; Δεν είστε μόνοι. Σε πολλά έργα επεξεργασίας τιμολογίων ή σάρωσης αποδείξεων, το πραγματικό πρόβλημα είναι η μετατροπή ενός θορυβώδους bitmap σε έναν δομημένο πίνακα που το σύστημα σας μπορεί να καταναλώσει.  

Τα καλά νέα; Με το Aspose OCR μπορείτε να **convert table to JSON** σε λίγες γραμμές, και επίσης λαμβάνετε το απλό κείμενο ολόκληρης της εικόνας, έτσι το **extract text from image** είναι ένα επιπλέον πλεονέκτημα. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία – από τη φόρτωση μιας εικόνας μέχρι την απόκτηση μιας καθαρής αναπαράστασης JSON του εντοπισμένου πίνακα.

> **Quick win:** Στο τέλος θα έχετε μια εκτελέσιμη εφαρμογή C# console που εκτυπώνει τόσο το ακατέργαστο κείμενο OCR όσο και μια συμβολοσειρά JSON που μπορείτε να τροφοδοτήσετε απευθείας σε μια βάση δεδομένων ή ένα API.

## Προαπαιτούμενα

- .NET 6.0 SDK (ή οποιαδήποτε πρόσφατη έκδοση .NET) εγκατεστημένο.  
- Ένα έγκυρο άδεια Aspose OCR ή μια δωρεάν δοκιμή (η βιβλιοθήκη λειτουργεί χωρίς άδεια αλλά προσθέτει υδατογράφημα).  
- Μια εικόνα που περιέχει πραγματικά έναν πίνακα – για παράδειγμα `invoice_table.png`.  
- Visual Studio 2022, VS Code, ή οποιονδήποτε επεξεργαστή προτιμάτε.

Δεν απαιτούνται επιπλέον πακέτα NuGet πέρα από το `Aspose.OCR`.

## Βήμα 1: Ρύθμιση του Έργου και Εγκατάσταση του Aspose OCR

Πρώτα, δημιουργήστε ένα νέο έργο console και ενσωματώστε τη βιβλιοθήκη OCR.

```bash
dotnet new console -n TableJsonDemo
cd TableJsonDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Εάν χρησιμοποιείτε εταιρικό proxy, προσθέστε τη σημαία `--no-restore` και εκτελέστε `dotnet restore` αργότερα με τις κατάλληλες μεταβλητές περιβάλλοντος.

## Βήμα 2: Αρχικοποίηση του OCR Engine και Ενεργοποίηση της Αναγνώρισης Πίνακα

Η καρδιά της λύσης είναι το `OcrEngine`. Με την εναλλαγή του `EnableTableRecognition` λέμε στο Aspose OCR να ψάχνει για δομές τύπου πλέγματος αντί να αντιμετωπίζει τα πάντα ως απλό κείμενο.

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

Γιατί είναι κρίσιμο αυτό το βήμα; Χωρίς την αναγνώριση πίνακα, η μηχανή θα επίπεδε το εικόνα σε μια ενιαία συμβολοσειρά, καθιστώντας αδύνατη την επαναδημιουργία των γραμμών και των στηλών αργότερα. Η ενεργοποίηση προσθέτει μια ελαφριά φάση ανάλυσης διάταξης που δεν κοστίζει σχεδόν τίποτα σε απόδοση, αλλά προσφέρει τεράστια οφέλη στο downstream.

## Βήμα 3: Φόρτωση της Εικόνας σας και Εκτέλεση της Αναγνώρισης

Τώρα κατευθύνουμε τη μηχανή στο αρχείο που περιέχει τον πίνακα. Η `ImageStream.FromFile` υποστηρίζει τις περισσότερες κοινές μορφές (PNG, JPEG, TIFF).

```csharp
        // Load the image that contains the table
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/invoice_table.png");

        // Perform OCR – this returns an OcrResult object with multiple helpers
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

Εάν η εικόνα είναι μεγάλη, σκεφτείτε να την αλλάξετε μέγεθος πρώτα για να επιταχύνετε την επεξεργασία. Το Aspose OCR ανιχνεύει αυτόματα το DPI, αλλά μια σάρωση 300 DPI είναι το ιδανικό σημείο για τους περισσότερους πίνακες.

## Βήμα 4: Εξαγωγή του Απλού Κειμένου – “extract text from image”

Ακόμα και αν ο κύριος στόχος μας είναι ο πίνακας, συχνά χρειάζεστε ακόμα το ακατέργαστο κείμενο για καταγραφή ή εναλλακτική επεξεργασία.

```csharp
        // Output the full recognized text
        Console.WriteLine("Full text:");
        Console.WriteLine(ocrResult.Text);
```

Η ιδιότητα `Text` συνενώνει όλα όσα βλέπει η μηχανή, διατηρώντας τις αλλαγές γραμμής. Αυτό είναι χρήσιμο όταν χρειάζεται να επαληθεύσετε ότι το OCR διάβασε σωστά τις κεφαλίδες ή τα υποσέλιδα εκτός της περιοχής του πίνακα.

## Βήμα 5: Λήψη του Εντοπισμένου Πίνακα ως JSON – “convert table to json” & “get table json”

Εδώ συμβαίνει η μαγεία. Η `GetTableAsJson()` σειριοποιεί τις εντοπισμένες γραμμές, στήλες και περιεχόμενα κελιών σε μια καθαρή συμβολοσειρά JSON.

```csharp
        // Retrieve the table structure as a JSON string
        string tableJson = ocrResult.GetTableAsJson();

        Console.WriteLine("\nDetected table (JSON):");
        Console.WriteLine(tableJson);
    }
}
```

Το παραγόμενο JSON φαίνεται κάπως έτσι (μορφοποιημένο για ευανάγνωστη εμφάνιση):

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

Γιατί το JSON είναι η προτιμώμενη μορφή; Είναι ανεξάρτητο από γλώσσα, εύκολο στην αποσειριοποίηση σε αντικείμενα και λειτουργεί άψογα με σύγχρονα web APIs. Εάν χρειάζεστε CSV αντί αυτού, απλώς επαναλάβετε τις γραμμές και ενώστε τα κείμενα των κελιών με κόμματα.

## Βήμα 6: (Προαιρετικό) Μετατροπή του JSON σε αντικείμενο .NET – “convert image to json”

Αν προτιμάτε να εργάζεστε με ισχυρούς τύπους, αποσειριοποιήστε το JSON χρησιμοποιώντας το `System.Text.Json`.

```csharp
using System.Text.Json;

...

        // Deserialize into a C# class (optional)
        var table = JsonSerializer.Deserialize<TableModel>(tableJson);
        Console.WriteLine("\nFirst cell value: " + table.Rows[0].Cells[0].Text);
```

Θα ορίσετε τα `TableModel`, `RowModel` και `CellModel` ώστε να ταιριάζουν με το σχήμα του JSON. Αυτό το βήμα δείχνει πώς μπορείτε να περάσετε από **convert image to json** μέχρι ένα τυποποιημένο αντικείμενο, καθιστώντας την επαλήθευση downstream εύκολη.

## Πλήρες Παράδειγμα Λειτουργίας

Συνδυάζοντας όλα, εδώ είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα. Αποθηκεύστε το ως `Program.cs` μέσα στο φάκελο του έργου που δημιουργήθηκε νωρίτερα.

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

### Αναμενόμενη Έξοδος

Όταν εκτελέσετε `dotnet run`, θα πρέπει να δείτε κάτι παρόμοιο με:

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

Εάν η έξοδος φαίνεται κενή, ελέγξτε ξανά ότι το `EnableTableRecognition` είναι ορισμένο σε `true` και ότι η εικόνα περιέχει σαφείς γραμμές πλέγματος.

## Συνηθισμένα Προβλήματα & Πώς να τα Αποφύγετε

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Δεν επιστράφηκε JSON** | Η ανίχνευση πίνακα είναι απενεργοποιημένη ή η εικόνα έχει πολύ χαμηλή αντίθεση. | Βεβαιωθείτε ότι `ocrEngine.Settings.EnableTableRecognition = true` και βελτιώστε την ποιότητα της εικόνας (αυξήστε την αντίθεση, δυαδικοποιήστε). |
| **Μερικές γραμμές** | Το OCR μπερδεύεται από συγχωνευμένα κελιά ή περιστραμμένο κείμενο. | Προεπεξεργασία της εικόνας: διόρθωση κλίσης (`ImageProcessor.Rotate`) ή χειροκίνητη διάσπαση των συγχωνευμένων κελιών. |
| **Ακατανόητο Unicode** | Η γραμματοσειρά δεν αναγνωρίζεται (π.χ., χειρόγραφη). | Αλλάξτε τα πακέτα γλώσσας μέσω `ocrEngine.Language = Language.English;` ή χρησιμοποιήστε διαφορετική μηχανή OCR για χειρόγραφο κείμενο. |
| **Μείωση απόδοσης** | Πολύ μεγάλη εικόνα (>5 MP). | Μειώστε το μέγεθος σε ~1500 px πλάτος διατηρώντας το DPI. |

## Επόμενα Βήματα: Πέρα από τα Βασικά

Τώρα που μπορείτε να **extract table from image** και **convert table to JSON**, σκεφτείτε αυτές τις επεκτάσεις:

- **Persist the JSON** σε μια βάση δεδομένων με Entity Framework.  
- **Post‑process** το JSON για να κανονικοποιήσετε μορφές νομισμάτων (π.χ., αφαιρέστε το `$`).  
- **Batch process** ένα φάκελο τιμολογίων χρησιμοποιώντας `Directory.GetFiles` και παράλληλη εκτέλεση με `Parallel.ForEach`.  
- **Integrate** με Azure Functions ή AWS Lambda για serverless OCR pipelines.

Κάθε ένα από αυτά τα θέματα φέρνει φυσικά τις άλλες δευτερεύουσες λέξεις-κλειδιά όπως **convert image to json** (όταν στέλνετε ολόκληρο το αποτέλεσμα OCR σε ένα cloud endpoint) και **get table json** για downstream analytics.

### Συμπέρασμα

Μόλις σας δείξαμε πώς να **extract table from image** χρησιμοποιώντας το Aspose OCR, να μετατρέψετε αυτόν τον πίνακα σε καθαρό JSON, και ακόμη να το αποσειριοποιήσετε σε αντικείμενα C#. Το ίδιο μοτίβο

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}