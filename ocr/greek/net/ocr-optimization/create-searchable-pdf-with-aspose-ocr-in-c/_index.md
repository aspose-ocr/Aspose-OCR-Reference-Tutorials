---
category: general
date: 2026-04-01
description: Δημιουργήστε αναζητήσιμο PDF σε C# χρησιμοποιώντας το Aspose OCR – μάθετε
  πώς να μετατρέπετε σαρωμένα PDF, να προσθέτετε OCR σε PDF και να ενεργοποιείτε την
  επιτάχυνση GPU για γρήγορα αποτελέσματα.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF σε C# γρήγορα—μετατρέψτε σκαναρισμένο
  PDF, προσθέστε OCR στο PDF και ενεργοποιήστε την επιτάχυνση GPU για υψηλής απόδοσης
  επεξεργασία.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης με Aspose OCR σε C#
tags:
- Aspose OCR
- C#
- PDF processing
title: Δημιουργία Αναζητήσιμου PDF με Aspose OCR σε C#
url: /el/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF με Aspose OCR σε C#

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμα PDF** αρχεία από ένα σωρό σαρωμένων εγγράφων; Δεν είστε οι μόνοι—πολλές ομάδες παλεύουν με τη μετατροπή PDF που περιέχουν μόνο εικόνες σε περιεχόμενα που μπορούν να αναζητηθούν με κείμενο. Τα καλά νέα; Με το Aspose OCR μπορείτε να **μετατρέψετε σαρωμένο PDF** σε πλήρως αναζητήσιμη έκδοση με λίγες μόνο γραμμές κώδικα C#. Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία, από την προσθήκη OCR σε PDF μέχρι την προαιρετική **ενεργοποίηση επιτάχυνσης GPU** για αύξηση ταχύτητας.

Θα σας δείξουμε επίσης πώς να **μετατρέψετε pdf σε αναζητήσιμο** μορφή, θα συζητήσουμε γιατί μπορεί να θέλετε να **προσθέσετε OCR σε PDF**, και θα σας δώσουμε πρακτικές συμβουλές για τη διαχείριση μεγάλων παρτίδων. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που παράγει ένα αναζητήσιμο PDF το οποίο μπορείτε να ενσωματώσετε σε οποιοδήποτε σύστημα διαχείρισης εγγράφων.

---

## What You’ll Need

- **.NET 6.0** ή νεότερο (το API λειτουργεί επίσης με .NET Framework, αλλά το .NET 6+ είναι η ιδανική επιλογή).
- **Aspose.OCR for .NET** πακέτο NuGet (`Install-Package Aspose.OCR`).
- Ένα σαρωμένο αρχείο PDF (μόνο εικόνα) για είσοδο.
- Προαιρετικά: ένα μηχάνημα συμβατό με GPU με εγκατεστημένο CUDA® εάν θέλετε να **ενεργοποιήσετε την επιτάχυνση GPU**.

Αυτό είναι όλο—χωρίς βαριές μηχανές OCR, χωρίς εξωτερικές υπηρεσίες. Όλα εκτελούνται τοπικά.

---

## Create Searchable PDF – Step‑by‑Step Overview

Παρακάτω είναι η υψηλού επιπέδου ροή που θα ακολουθήσουμε:

1. **Αρχικοποίηση της μηχανής OCR** – ενημερώστε το Aspose για τη γλώσσα που πρέπει να αναγνωρίσει και αν θα χρησιμοποιηθεί το GPU.
2. **Καθορίστε τη μηχανή στο σαρωμένο PDF** – ορίστε τις διαδρομές εισόδου και εξόδου.
3. **Εκτελέστε τη μετατροπή** – το Aspose κάνει τη βαριά δουλειά και γράφει ένα αναζητήσιμο PDF.
4. **Επαληθεύστε το αποτέλεσμα** – ανοίξτε το αρχείο εξόδου και δοκιμάστε μια αναζήτηση κειμένου.

Κάθε βήμα είναι χωρισμένο σε δική του ενότητα, ώστε να μπορείτε να επιλέξετε τα μέρη που σας ενδιαφέρουν περισσότερο.

---

## Convert Scanned PDF to Searchable PDF

Το πρώτο πράγμα που πρέπει να κάνετε είναι να δημιουργήσετε μια παρουσία του `OcrEngine`. Αυτό το αντικείμενο είναι η κύρια μηχανή που διαβάζει τις raster εικόνες μέσα στο PDF σας και εξάγει το κείμενο.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Γιατί λειτουργεί:** `ConvertToSearchablePdf` διαβάζει κάθε σελίδα, εκτελεί OCR στο raster περιεχόμενο και στη συνέχεια ενσωματώνει ένα αόρατο στρώμα κειμένου πίσω από την αρχική εικόνα. Το αποτέλεσμα φαίνεται ακριβώς όπως το αρχικό σαρωμένο έγγραφο, αλλά τώρα μπορείτε να αντιγράψετε, να επιλέξετε και να αναζητήσετε το κείμενο.

---

## Add OCR to PDF Using Aspose

Αν έχετε ήδη ένα PDF και απλώς θέλετε να **προσθέσετε OCR σε PDF** χωρίς να μετατρέψετε ολόκληρο το αρχείο, μπορείτε να καλέσετε την ίδια μέθοδο—το Aspose θεωρεί τη λειτουργία ως “προσθήκη OCR”. Ο παραπάνω κώδικας το κάνει ήδη, αλλά εδώ είναι μια γρήγορη παραλλαγή που δείχνει πώς μπορείτε να επεξεργαστείτε πολλαπλά αρχεία σε βρόχο:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**Συμβουλή:** Διατηρήστε την ίδια παρουσία `OcrEngine` για ολόκληρη τη παρτίδα. Η επανδημιουργία της κάθε φορά προσθέτει περιττό φόρτο, ειδικά όταν **ενεργοποιείτε την επιτάχυνση GPU**.

---

## Enable GPU Acceleration for Faster OCR

Η επιτάχυνση GPU μπορεί να μειώσει λεπτά από μια μεγάλη παρτίδα. Το Aspose OCR αξιοποιεί το NVIDIA CUDA στο παρασκήνιο, οπότε χρειάζεται μόνο να αλλάξετε μια boolean σημαία:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Πότε να το χρησιμοποιήσετε:** Εάν επεξεργάζεστε PDF μεγαλύτερα από 10 MB ή διαχειρίζεστε περισσότερα από μερικές δεκάδες αρχεία, το GPU συνήθως θα σας δώσει αύξηση ταχύτητας 2‑3×. Σε ένα μέτριο laptop χωρίς GPU που υποστηρίζει CUDA, αφήστε το `false`—η βιβλιοθήκη θα επιστρέψει αυτόματα στην CPU.

**Συνηθισμένο λάθος:** Η παράλειψη εγκατάστασης της σωστής έκδοσης του οδηγού CUDA μπορεί να προκαλέσει εξαίρεση χρόνου εκτέλεσης (`CudaException`). Βεβαιωθείτε ότι ο οδηγός σας ταιριάζει με την έκδοση που περιμένει το Aspose (ελέγξτε τις σημειώσεις έκδοσης στη σελίδα NuGet).

---

## Full Working Example (All Steps Combined)

Παρακάτω είναι μια αυτόνομη εφαρμογή κονσόλας που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο .NET. Περιλαμβάνει χρήσιμα σχόλια, διαχείριση σφαλμάτων και ένα τελικό βήμα επαλήθευσης που εκτυπώνει τον αριθμό των επεξεργασμένων σελίδων.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Αναμενόμενη έξοδος**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

Ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα PDF και δοκιμάστε να πληκτρολογήσετε μια λέξη που εμφανίζεται στις σαρωμένες εικόνες. Εάν το κείμενο επισημαίνεται, έχετε δημιουργήσει επιτυχώς **αναζητήσιμο pdf**.

---

## Common Pitfalls and Pro Tips

| Πρόβλημα | Γιατί συμβαίνει | Πώς να το διορθώσετε / Αποφύγετε |
|----------|----------------|---------------------------------|
| **GPU δεν εντοπίστηκε** | Λείπει ή δεν ταιριάζει ο οδηγός CUDA. | Εγκαταστήστε την έκδοση του οδηγού που αναγράφεται στις σημειώσεις έκδοσης του Aspose· ορίστε `UseGpuAcceleration = false` ως εναλλακτική. |
| **Λάθος γλώσσα** | Το OCR προεπιλογή είναι τα Αγγλικά· άλλες γλώσσες απαιτούν ρητή ρύθμιση. | Ορίστε `Language = Language.Spanish` (ή οποιοδήποτε υποστηριζόμενο enum) πριν από τη μετατροπή. |
| **Μεγάλα PDF προκαλούν OutOfMemory** | Η μηχανή φορτώνει ολόκληρες σελίδες στη μνήμη. | Επεξεργαστείτε το PDF σε τμήματα χρησιμοποιώντας `ocrEngine.PageRange = new PageRange(1, 5)` για κάθε παρτίδα. |
| **Το αρχείο εξόδου είναι κατεστραμμένο** | Ο φάκελος προορισμού δεν έχει δικαιώματα εγγραφής. | Εκτελέστε την εφαρμογή με αυξημένα δικαιώματα ή επιλέξτε διαδρομή με δικαιώματα εγγραφής. |
| **Το στρώμα κειμένου δεν είναι αναζητήσιμο** | Ο προβολέας αποθηκεύει στην κρυφή μνήμη την παλιά έκδοση. | Ανανεώστε τον προβολέα PDF ή ανοίξτε ξανά το αρχείο. |

**Συμβουλή επαγγελματία:** Όταν αντιμετωπίζετε ένα μείγμα σαρωμένων και εγγενών PDF, ελέγξτε τη σημαία `HasText` κάθε σελίδας (`PdfPageInfo.HasText`) πριν τρέξετε OCR. Αυτό εξοικονομεί κύκλους CPU και αποτρέπει διπλό OCR σε σελίδες που είναι ήδη αναζητήσιμες.

---

## Verify the Result Programmatically (Optional)

Εάν θέλετε να αυτοματοποιήσετε την επαλήθευση, το Aspose.PDF μπορεί να εξάγει το κρυφό κείμενο:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Αυτό το απόσπασμα αποδεικνύει ότι πραγματικά **μετατρέπετε pdf σε αναζητήσιμο** μορφή, όχι απλώς επικάλυψη εικόνας.

---

## Image Example

![Παράδειγμα εξόδου δημιουργίας αναζητήσιμου PDF](https://example.com/images/searchable-pdf.png "Δημιουργία αναζητήσιμου PDF με χρήση Aspose OCR")

*Κείμενο alt:* **create searchable pdf** παράδειγμα που δείχνει πριν (σκαναρισμένο) και μετά (αναζητήσιμο) προβολή.

---

## Next Steps & Related Topics

- **Επεξεργασία παρτίδας:** Τυλίξτε τον βρόχο από την ενότητα “Add OCR to PDF” σε Windows Service ή Azure Function για εργασίες νύχτας.
- **Προηγμένη υποστήριξη γλώσσας:** Εξερευνήστε `ocrEngine.Language = Language.Multilingual` για έγγραφα που περιέχουν μεικτά σενάρια.
- **Καθαρισμός μετά το OCR:** Χρησιμοποιήστε το `TextFragmentAbsorber` του Aspose.PDF για διόρθωση κοινών σφαλμάτων OCR (π.χ., “0” vs “O”).
- **Security

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}