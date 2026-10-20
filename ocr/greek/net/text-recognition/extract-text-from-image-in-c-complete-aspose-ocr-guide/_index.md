---
category: general
date: 2026-01-10
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να μετατρέπετε το κείμενο σαρωμένου εγγράφου με επεξεργασία παρτίδας και να
  αποθηκεύετε τα αποτελέσματα.
draft: false
keywords:
- extract text from image
- convert scanned document text
- batch OCR processing
- Aspose OCR
- C# OCR tutorial
language: el
og_description: Εξαγωγή κειμένου από εικόνα με το Aspose OCR σε C#. Αυτό το σεμινάριο
  δείχνει πώς να μετατρέψετε το κείμενο σαρωμένου εγγράφου χρησιμοποιώντας επεξεργασία
  παρτίδας.
og_title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός Aspose OCR
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από εικόνα σε C# – Πλήρης οδηγός Aspose OCR
url: /el/net/text-recognition/extract-text-from-image-in-c-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή κειμένου από εικόνα – Πλήρης οδηγός Aspose OCR

Κάποτε χρειάστηκε να **εξαγάγετε κείμενο από εικόνα** αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είσαι μόνος· πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν δουλεύουν με σαρωμένα PDF, πολυ‑σελίδες TIFF ή αποδείξεις σε μορφή φωτογραφίας. Τα καλά νέα είναι ότι με το Aspose OCR μπορείς να **μετατρέψεις κείμενο σαρωμένου εγγράφου** με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό σενάριο: λήψη ενός πολυ‑σελίδων TIFF, εκτέλεση batch OCR σε κάθε σελίδα και δημιουργία ενός μοναδικού αρχείου κειμένου που περιέχει το περιεχόμενο όλων των σελίδων. Στο τέλος θα έχεις μια έτοιμη για εκτέλεση εφαρμογή console, θα καταλάβεις γιατί κάθε βήμα είναι σημαντικό και θα ξέρεις πώς να προσαρμόσεις τη ροή για ειδικές περιπτώσεις όπως εικόνες με κωδικό πρόσβασης ή προσαρμοσμένα πακέτα γλώσσας.

## Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)  
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάς)  
- Αρχείο άδειας Aspose OCR (ή μπορείς να χρησιμοποιήσεις τη δωρεάν λειτουργία αξιολόγησης)  
- Αρχείο εικόνας πολλαπλών σελίδων (π.χ., `multipage.tif`) τοποθετημένο σε φάκελο που μπορείς να αναφέρεις  

Δεν απαιτούνται επιπλέον πακέτα NuGet εκτός από το `Aspose.OCR`; θα το εγκαταστήσουμε στο πρώτο βήμα.

## Βήμα 1 – Εγκατάσταση Aspose OCR και ρύθμιση του έργου

```bash
dotnet new console -n ImageTextExtractor
cd ImageTextExtractor
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν διαθέτεις αρχείο άδειας (`Aspose.OCR.lic`), αντέγραψέ το στη ρίζα του έργου. Η βιβλιοθήκη θα το εντοπίσει αυτόματα κατά το χρόνο εκτέλεσης.

Γιατί αυτό το βήμα; Η εγκατάσταση του πακέτου σου δίνει πρόσβαση σε `BatchProcessor`, `OcrEngine` και άλλες χρήσιμες κλάσεις που αφαιρούν την ανάγκη χειρισμού εικόνας χαμηλού επιπέδου. Επίσης εξασφαλίζει ότι χρησιμοποιείς τους πιο πρόσφατους αλγόριθμους OCR που παρέχει η Aspose.

## Βήμα 2 – Φόρτωση της πολυ‑σελίδας εικόνας με BatchProcessor

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System.Text;

// Step 2: Initialize the batch processor with the path to your TIFF
var batchProcessor = new BatchProcessor(@"YOUR_DIRECTORY\multipage.tif");

// Verify that pages were loaded
if (batchProcessor.Pages.Count == 0)
{
    Console.WriteLine("No pages found – double‑check the file path.");
    return;
}
```

Το `BatchProcessor` έχει σχεδιαστεί ακριβώς για αυτό το σενάριο: επανάληψη σε κάθε σελίδα μιας εικόνας πολλαπλών σελίδων χωρίς να χρειάζεται να χωρίσεις τα αρχεία χειροκίνητα.

Ο `BatchProcessor` διαβάζει όλες τις σελίδες στη μνήμη, τις εκθέτει μέσω του `batchProcessor.Pages`. Κάθε αντικείμενο σελίδας γνωρίζει τον αριθμό του (`ocrPage.Number`) που θα χρησιμοποιήσουμε αργότερα για σαφείς επικεφαλίδες.

## Βήμα 3 – Προετοιμασία StringBuilder για τη συσσώρευση των αποτελεσμάτων

```csharp
// Step 3: Create a StringBuilder to collect OCR results
var extractedText = new StringBuilder();
```

Γιατί StringBuilder; Η συνένωση συμβολοσειρών με `+` μέσα σε βρόχο δημιουργεί νέα αντικείμενα σε κάθε επανάληψη, μειώνοντας την απόδοση—ιδιαίτερα σε μεγάλα έγγραφα.

## Βήμα 4 – Επανάληψη σε κάθε σελίδα, εκτέλεση OCR και προσθήκη αποτελεσμάτων

```csharp
// Step 4: Process each page individually
foreach (var ocrPage in batchProcessor.Pages)
{
    // Create a fresh OcrEngine for every page – this isolates settings
    var ocrEngine = new OcrEngine
    {
        Image = ocrPage
    };

    // Perform recognition
    ocrEngine.Recognize();

    // Append a clear header and the recognized text
    extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
    extractedText.AppendLine(ocrEngine.Text);
}
```

**Γιατί νέο `OcrEngine` ανά σελίδα;** Κάποιοι προγραμματιστές επαναχρησιμοποιούν μία μηχανή και αλλάζουν την ιδιότητα `Image`, αλλά αυτό μπορεί να διατηρήσει ρυθμίσεις γλώσσας ή προηγούμενα αποτελέσματα, οδηγώντας σε λεπτές σφάλματα. Η δημιουργία νέας μηχανής εξασφαλίζει καθαρό περιβάλλον.

### Διαχείριση κοινών ειδικών περιπτώσεων

- **Κενές σελίδες:** Αν μια σελίδα δεν περιέχει αναγνωρίσιμο κείμενο, το `ocrEngine.Text` θα είναι κενό. Μπορείς να προσθέσεις έναν δείκτη όπως “(Δεν εντοπίστηκε κείμενο)”.
- **Επιλογή γλώσσας:** Από προεπιλογή το Aspose OCR χρησιμοποιεί Αγγλικά. Για επεξεργασία Γερμανικών ή Γαλλικών, όρισε `ocrEngine.Language = Language.German;` πριν καλέσεις το `Recognize()`.
- **Συμβουλή απόδοσης:** Για τεράστια TIFF, μπορείς να ενεργοποιήσεις `ocrEngine.UseParallelProcessing = true;` ώστε να εκμεταλλευτείς πολλαπλούς πυρήνες.

## Βήμα 5 – Εγγραφή του συνδυασμένου αποτελέσματος σε αρχείο κειμένου

```csharp
// Step 5: Save the result to a .txt file
string outputPath = @"YOUR_DIRECTORY\multipage_result.txt";
File.WriteAllText(outputPath, extractedText.ToString());

Console.WriteLine($"OCR complete! Results saved to {outputPath}");
```

Το παραγόμενο `multipage_result.txt` θα έχει περίπου την εξής μορφή:

```
--- Page 1 ---
This is the first page of the scanned document.
It contains a title and some introductory text.

--- Page 2 ---
Continuation of the report.
Data tables and figures follow.
```

Τώρα έχεις **εξαγάγει κείμενο από εικόνα** και έχεις **μετατρέψει κείμενο σαρωμένου εγγράφου** σε μορφή αναζητήσιμη και επεξεργάσιμη.

## Bonus – Οπτική επισκόπηση (Alt Text εικόνας)

Παρακάτω υπάρχει ένα απλό διάγραμμα ροής που απεικονίζει τη διαδικασία.  
*Alt text:* “Διάγραμμα που δείχνει πώς να εξαγάγετε κείμενο από εικόνα χρησιμοποιώντας batch processing του Aspose OCR σε C#”.

![OCR Flow Diagram](placeholder-image-url.png)

*(Αν δημοσιεύεις αυτό το tutorial σε στατικό site, αντικατέστησε το placeholder με ένα πραγματικό SVG ή PNG.)*

## Συχνές ερωτήσεις

**Λειτουργεί αυτό με αρχεία PDF;**  
Ναι, το Aspose OCR μπορεί να διαβάσει σελίδες PDF ως εικόνες. Απλώς χρειάζεται πρώτα να μετατρέψεις το PDF σε εικόνες, ή να χρησιμοποιήσεις το `PdfDocument` από το `Aspose.PDF` και να περάσεις την ραστερισμένη εικόνα κάθε σελίδας στο `OcrEngine`.

**Τι γίνεται αν το TIFF είναι προστατευμένο με κωδικό;**  
Το `BatchProcessor` δεν διαχειρίζεται κρυπτογράφηση απευθείας. Αποκρυπτογράφησε το αρχείο χρησιμοποιώντας μια βιβλιοθήκη όπως το `Aspose.Imaging` πριν το περάσεις στην αλυσίδα OCR.

**Μπορώ να εξάγω JSON αντί για απλό κείμενο;**  
Απολύτως. Αντικατάστησε τη λογική του `StringBuilder` με έναν JSON serializer (π.χ., `System.Text.Json`) και αποθήκευσε το κείμενο κάθε σελίδας κάτω από ένα κλειδί `pageNumber`.

## Πλήρες λειτουργικό παράδειγμα

Ακολουθεί το πλήρες πρόγραμμα που μπορείς να αντιγράψεις‑και‑επικολλήσεις στο `Program.cs`. Περιλαμβάνει όλες τις οδηγίες `using`, διαχείριση σφαλμάτων και σχόλια.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Text;

namespace ImageTextExtractor
{
    class Program
    {
        static void Main(string[] args)
        {
            // Adjust these paths to match your environment
            string inputImagePath = @"YOUR_DIRECTORY\multipage.tif";
            string outputTextPath = @"YOUR_DIRECTORY\multipage_result.txt";

            // 1️⃣ Load the multi‑page image
            var batchProcessor = new BatchProcessor(inputImagePath);
            if (batchProcessor.Pages.Count == 0)
            {
                Console.WriteLine("No pages detected – verify the file path.");
                return;
            }

            // 2️⃣ Prepare a StringBuilder for the final output
            var extractedText = new StringBuilder();

            // 3️⃣ Process each page
            foreach (var ocrPage in batchProcessor.Pages)
            {
                var ocrEngine = new OcrEngine
                {
                    Image = ocrPage,
                    // Uncomment to change language:
                    // Language = Language.German,
                    // UseParallelProcessing = true
                };

                // Run OCR
                ocrEngine.Recognize();

                // Append header and text
                extractedText.AppendLine($"--- Page {ocrPage.Number} ---");
                // Guard against empty results
                string pageText = string.IsNullOrWhiteSpace(ocrEngine.Text)
                    ? "(No text detected on this page)"
                    : ocrEngine.Text;
                extractedText.AppendLine(pageText);
            }

            // 4️⃣ Write to file
            File.WriteAllText(outputTextPath, extractedText.ToString());

            Console.WriteLine($"✅ Extraction complete. File saved at: {outputTextPath}");
        }
    }
}
```

Τρέξε το πρόγραμμα με:

```bash
dotnet run
```

Θα πρέπει να δεις το μήνυμα στην κονσόλα που επιβεβαιώνει την επιτυχία, και το αρχείο εξόδου θα περιέχει τα συνενωμένα αποτελέσματα OCR.

## Συμπέρασμα

Δείξαμε μια πρακτική μέθοδο για **εξαγωγή κειμένου από εικόνα** χρησιμοποιώντας το Aspose OCR, μετατρέποντας οποιοδήποτε πολυ‑σελίδων σαρωμένο αρχείο σε απλό, αναζητήσιμο κείμενο. Εκμεταλλευόμενοι το `BatchProcessor` και μια καθαρή ρύθμιση `OcrEngine` ανά σελίδα, μπορείς αξιόπιστα να **μετατρέψεις κείμενο σαρωμένου εγγράφου** διατηρώντας τον κώδικα απλό και συντηρήσιμο.

Νιώσε ελεύθερος/η να πειραματιστείς: δοκίμασε διαφορετικές γλώσσες, άλλαξε την έξοδο σε JSON, ή ενσωμάτωσε αυτή τη λογική σε ένα web API που επεξεργάζεται ανεβάσματα σε πραγματικό χρόνο. Το βασικό μοτίβο παραμένει το ίδιο—φόρτωση, αναγνώριση, συσσώρευση και αποθήκευση.

Έχεις περισσότερες ερωτήσεις σχετικά με OCR, άδειες Aspose ή διαχείριση τεράστιων δέσμης εγγράφων; Άφησε ένα σχόλιο παρακάτω ή δες την επίσημη τεκμηρίωση της Aspose για πιο βαθιές πληροφορίες. Καλό coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}