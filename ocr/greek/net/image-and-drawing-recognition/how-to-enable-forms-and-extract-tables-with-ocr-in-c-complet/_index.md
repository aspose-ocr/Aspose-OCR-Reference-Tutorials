---
category: general
date: 2026-01-04
description: Μάθετε πώς να ενεργοποιήσετε τις φόρμες και να εξάγετε πίνακες από εικόνες
  χρησιμοποιώντας OCR σε C#. Αυτό το βήμα‑βήμα tutorial δείχνει επίσης πώς να εκτελέσετε
  OCR σε εικόνα και να εντοπίσετε πίνακες με OCR.
draft: false
keywords:
- how to enable forms
- how to extract tables
- run OCR image
- use OCR C#
- detect tables OCR
language: el
og_description: Οδηγός βήμα‑προς‑βήμα για το πώς να ενεργοποιήσετε φόρμες, να εξάγετε
  πίνακες, να εκτελέσετε OCR σε εικόνα και να εντοπίσετε OCR πινάκων χρησιμοποιώντας
  C#.
og_title: Πώς να ενεργοποιήσετε τις φόρμες και να εξάγετε πίνακες με OCR σε C#
tags:
- OCR
- C#
- Computer Vision
title: Πώς να ενεργοποιήσετε φόρμες και να εξάγετε πίνακες με OCR σε C# – Πλήρης οδηγός
url: /el/net/image-and-drawing-recognition/how-to-enable-forms-and-extract-tables-with-ocr-in-c-complet/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Ενεργοποιήσετε Φόρμες και να Εξάγετε Πίνακες με OCR σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να ενεργοποιήσετε φόρμες** όταν σαρώνετε τιμολόγια, αποδείξεις ή οποιοδήποτε δομημένο έγγραφο; Δεν είστε μόνοι. Σε πολλά πραγματικά έργα το μεγαλύτερο εμπόδιο είναι να κάνετε το OCR να κατανοήσει τόσο τα πεδία της φόρμας **όσο** και τους πίνακες χωρίς εκατομμύρια γραμμές προσαρμοσμένης ανάλυσης.  

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από μια πρακτική, ολοκληρωμένη λύση που δείχνει **πώς να ενεργοποιήσετε φόρμες**, **πώς να εξάγετε πίνακες**, και ακόμη **πώς να εκτελέσετε επεξεργασία εικόνας OCR** σε ένα μόνο πρόγραμμα C#. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα που εντοπίζει πίνακες με τρόπο OCR, εξάγει ζεύγη κλειδί‑τιμή και τα εκτυπώνει στην κονσόλα.

> **Προαπαιτούμενα** – .NET 6+ (ή .NET Framework 4.7+), μια αναφορά στο OCR SDK που χρησιμοποιείτε (το παράδειγμα υποθέτει μια γενική κλάση `OcrEngine`), και ένα αρχείο εικόνας (`invoice_table.png`) που περιέχει πίνακα ή φόρμα. Δεν απαιτούνται άλλες εξωτερικές βιβλιοθήκες.

![how to enable forms with OCR C#](image.png)

## Τι Καλύπτει Αυτό το Tutorial

- **Ενεργοποίηση αναγνώρισης φόρμας** ώστε πεδία όπως “Invoice Number” ή “Date” να εντοπίζονται αυτόματα.  
- **Εξαγωγή πινάκων** από σαρωμένα έγγραφα, παρέχοντας αριθμό γραμμών/στηλών και το περιεχόμενο των κελιών.  
- **Εκτέλεση επεξεργασίας εικόνας OCR** με μία κλήση και διαχείριση του αποτελέσματος προγραμματιστικά.  
- Συμβουλές για **detect tables OCR** σε ειδικές περιπτώσεις, όπως συγχωνευμένα κελιά ή ελλιπείς γραμμές.  

Ας βουτήξουμε.

## Βήμα 1: Ρύθμιση του OCR Engine – πώς να ενεργοποιήσετε φόρμες

Πριν μπορέσει να γίνει οποιαδήποτε αναγνώριση, χρειάζεστε μια παρουσία του OCR engine. Τα περισσότερα SDK παρέχουν έναν απλό κατασκευαστή· θα δείξουμε επίσης πού μπορείτε να ρυθμίσετε επιλογές αργότερα.

```csharp
using System;
using System.Linq;

// Assume the OCR SDK namespace is OcrSdk
using OcrSdk;

public class OcrDemo
{
    public static void Main()
    {
        // Create the OCR engine – this is where “how to enable forms” starts.
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image that contains a table or form.
        // Replace the path with the actual location of your PNG/JPEG/TIFF file.
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");
```

**Γιατί είναι σημαντικό:** Η δημιουργία του engine κατανέμει εσωτερικούς πόρους (όπως μοντέλα γλώσσας). Αν παραλείψετε αυτό το βήμα, η επόμενη κλήση `Recognize` θα ρίξει `NullReferenceException`.

## Βήμα 2: Ενεργοποίηση Δομημένης Εξαγωγής – πώς να εξάγετε πίνακες & detect tables OCR

Τώρα ενεργοποιούμε τις δύο βασικές λειτουργίες: αναγνώριση πινάκων και εξαγωγή πεδίων φόρμας. Τα σύγχρονα OCR engines προσφέρουν boolean flags ή ένα πιο λεπτομερές αντικείμενο `Config`.

```csharp
        // Enable structured extraction features.
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms
```

**Pro tip:** Αν χρειάζεστε μόνο μία από τις λειτουργίες, η απενεργοποίηση της άλλης μπορεί να βελτιώσει την απόδοση έως και 20 %.

## Βήμα 3: Εκτέλεση OCR Image και Λήψη Αποτελέσματος – run OCR image

Με το engine ρυθμισμένο, μια μόνο κλήση μεθόδου κάνει το σκληρό έργο. Το επιστρεφόμενο `OcrResult` περιέχει συλλογές για πίνακες και πεδία φόρμας.

```csharp
        // Run OCR – this is the “run OCR image” step.
        OcrResult ocrResult = ocrEngine.Recognize();

        // -----------------------------------------------------------------
        // Step 4: Process Detected Tables – how to extract tables
        // -----------------------------------------------------------------
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");

            // Show the first row for a quick sanity check.
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // -----------------------------------------------------------------
        // Step 5: Process Detected Form Fields – how to enable forms
        // -----------------------------------------------------------------
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

### Αναμενόμενη Εξαγωγή στην Κονσόλα

```
Table 1: 5 rows, 4 columns
Item | Qty | Price | Total
InvoiceNumber: INV-2025-001
Date: 2025-12-31
Customer: Acme Corp.
```

Οι ακριβείς αριθμοί θα διαφέρουν ανάλογα με την πηγή εικόνας, αλλά θα πρέπει να δείτε μια γραμμή σύνοψης για κάθε πίνακα ακολουθούμενη από τις τιμές των κελιών της πρώτης γραμμής, και στη συνέχεια μια λίστα ζευγών κλειδί‑τιμή για τα πεδία της φόρμας.

## Βήμα 4: Διαχείριση Ειδικών Περιπτώσεων Κατά το Detect Tables OCR

Ακόμη και με `EnableTableRecognition = true`, το OCR μπορεί να αντιμετωπίσει προβλήματα:

| Ζήτημα | Γιατί Συμβαίνει | Γρήγορη Λύση |
|-------|----------------|-----------|
| **Συγχωνευμένα κελιά** | Η μηχανή αντιμετωπίζει την συγχωνευμένη περιοχή ως ένα μόνο κελί. | Μετά‑επεξεργασία γραμμών: εντοπίστε ασυνήθιστα πλατιά κελιά και χωρίστε τα βάσει κενών. |
| **Ελλιπείς γραμμές** | Οι γραμμές του πίνακα είναι αχνές ή σπασμένες. | Αυξήστε την αντίθεση της εικόνας πριν τη δώσετε στο engine (`ocrEngine.PreprocessImage`). |
| **Πίνακες με περιστροφή** | Το έγγραφο σαρώθηκε υπό γωνία. | Χρησιμοποιήστε `ocrEngine.Config.AutoRotate = true` (αν είναι διαθέσιμο). |

**Συμβουλή:** Πάντα ελέγχετε `table.Rows.Count` και `table.Columns.Count` πριν προσπελάσετε δείκτες ώστε να αποφύγετε `IndexOutOfRangeException`.

## Βήμα 5: Συνδυάζοντας Όλα – Ένα Πλήρες, Εκτελέσιμο Παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο project κονσόλας. Περιλαμβάνει τις οδηγίες `using`, τη ρύθμιση του engine και τη λογική επεξεργασίας που παρουσιάστηκε νωρίτερα.

```csharp
using System;
using System.Linq;
using OcrSdk;   // Replace with your actual OCR SDK namespace

public class OcrDemo
{
    public static void Main()
    {
        // 1️⃣ Create OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Load the target image
        ocrEngine.LoadImage(@"YOUR_DIRECTORY/invoice_table.png");

        // 3️⃣ Enable structured extraction (forms + tables)
        ocrEngine.Config.EnableTableRecognition = true;   // detect tables OCR
        ocrEngine.Config.EnableFormRecognition = true;    // how to enable forms

        // 4️⃣ Run OCR – “run OCR image”
        OcrResult ocrResult = ocrEngine.Recognize();

        // 5️⃣ Process tables – “how to extract tables”
        foreach (var table in ocrResult.Tables)
        {
            Console.WriteLine($"Table {table.Id}: {table.Rows.Count} rows, {table.Columns.Count} columns");
            if (table.Rows.Count > 0)
            {
                var firstRow = table.Rows[0];
                Console.WriteLine(string.Join(" | ", firstRow.Cells.Select(c => c.Text)));
            }
        }

        // 6️⃣ Process form fields – “how to enable forms”
        foreach (var field in ocrResult.FormFields)
        {
            Console.WriteLine($"{field.Key}: {field.Value}");
        }
    }
}
```

Τρέξτε το πρόγραμμα (`dotnet run` ή `Ctrl+F5` στο Visual Studio) και θα δείτε την έξοδο στην κονσόλα όπως περιγράφηκε παραπάνω.

## Συχνές Ερωτήσεις (FAQ)

**Ε: Λειτουργεί αυτό με είσοδο PDF;**  
Α: Τα περισσότερα OCR SDK δέχονται PDF εσωτερικά μετατρέποντας κάθε σελίδα σε raster. Απλώς καλέστε `ocrEngine.LoadPdf("file.pdf")` αντί για `LoadImage`.

**Ε: Τι γίνεται αν η εικόνα μου περιέχει τόσο πίνακα *όσο* και υπογραφή;**  
Α: Η υπογραφή θα εμφανιστεί ως ξεχωριστή περιοχή εικόνας. Μπορείτε να την αγνοήσετε ελέγχοντας `ocrResult.Images` για κείμενο χαμηλής εμπιστοσύνης.

**Ε: Μπορώ να εξάγω τους πίνακες σε CSV;**  
Α: Φυσικά. Μετά την επανάληψη πάνω σε `table.Rows`, γράψτε κάθε `cell.Text` σε ένα `StringBuilder` διαχωρισμένο με κόμματα, έπειτα αποθηκεύστε το string σε αρχείο `.csv`.

## Συμπέρασμα

Τώρα ξέρετε **πώς να ενεργοποιήσετε φόρμες**, **πώς να εξάγετε πίνακες**, και τα ακριβή βήματα για **run OCR image** επεξεργασία χρησιμοποιώντας C#. Το παράδειγμα δείχνει ολόκληρη τη ροή εργασίας—από τη δημιουργία του engine, τη διαμόρφωση, μέχρι τη διαχείριση των αποτελεσμάτων—ώστε να το αντιγράψετε απευθείας στα δικά σας έργα.  

Στη συνέχεια, δοκιμάστε να αντικαταστήσετε την εικόνα δείγματος με ένα πολύ‑σελίδων PDF τιμολογίου, πειραματιστείτε με `ocrEngine.Config.AutoRotate`, ή διοχετεύστε τα εξαγόμενα δεδομένα σε μια βάση. Αυτές οι επεκτάσεις θα ενισχύσουν την εξοικείωσή σας με **detect tables OCR** και **use OCR C#** σε παραγωγικά σενάρια.

Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}