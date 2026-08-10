---
category: general
date: 2026-03-17
description: Δημιουργήστε γρήγορα PDF με δυνατότητα αναζήτησης μετατρέποντας σαρωμένα
  PDF με OCR. Μάθετε πώς να εκτελείτε OCR, να εξάγετε κείμενο από PDF και άλλα.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr to searchable pdf
- extract text from pdf
- how to run ocr
language: el
og_description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από σαρωμένα έγγραφα. Αυτός
  ο οδηγός δείχνει πώς να μετατρέψετε σαρωμένο PDF, να εκτελέσετε OCR και να εξάγετε
  κείμενο χρησιμοποιώντας C#.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης – Πλήρης οδηγός OCR σε C#
tags:
- OCR
- PDF
- C#
- .NET
title: Δημιουργία PDF με δυνατότητα αναζήτησης από σαρωμένα αρχεία – Οδηγός βήμα‑προς‑βήμα
  C#
url: /el/net/text-recognition/create-searchable-pdf-from-scanned-files-step-by-step-c-guid/
---

>}}

We must keep them unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία αναζητήσιμου PDF – Πλήρες C# Tutorial

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από μια στοίβα σαρωμένων σελίδων; Ίσως ψηφιοποιείτε παλιά συμβόλαια ή απλώς θέλετε τα PDF σας να είναι αναζητήσιμα στον Windows Explorer. Σε κάθε περίπτωση, πιθανότατα αναρωτιέστε πώς να **μετατρέψετε σαρωμένο pdf** σε κάτι που μπορείτε πραγματικά να αναζητήσετε.  

Τα καλά νέα; Με μερικές γραμμές C# και μια μηχανή OCR, μπορείτε να μετατρέψετε οποιοδήποτε PDF βασισμένο σε εικόνα σε πλήρως αναζητήσιμο PDF — χωρίς εξωτερικές υπηρεσίες. Σε αυτό το tutorial θα περάσουμε από όλη τη διαδικασία, από την εγκατάσταση της βιβλιοθήκης μέχρι την εξαγωγή κειμένου, και θα καλύψουμε το «γιατί» πίσω από κάθε βήμα ώστε να καταλάβετε πραγματικά τι συμβαίνει στο παρασκήνιο.

> **Γρήγορη απάντηση:** απλώς ορίστε `PdfConversionMode = PdfConversionMode.SearchablePdf`, τροφοδοτήστε το σαρωμένο αρχείο, καλέστε `Recognize()` και αποθηκεύστε το αποτέλεσμα.  

Παρακάτω θα βρείτε όλα όσα χρειάζεστε για να το κάνετε λειτουργικό σήμερα.

---

## Τι Θα Χρειαστεί

| Απαιτούμενο | Γιατί είναι σημαντικό |
|--------------|------------------------|
| .NET 6 or later (or .NET Framework 4.7+) | Το OCR SDK που θα χρησιμοποιήσουμε στοχεύει σε αυτές τις εκδόσεις χρόνου εκτέλεσης. |
| Visual Studio 2022 (or any C# IDE) | Κάνει την αποσφαλμάτωση και τη διαχείριση του NuGet απλή. |
| A NuGet‑compatible OCR library (e.g., **Aspose.OCR** or **Tesseract.NET**) | Παρέχει την κλάση `OcrEngine` που φαίνεται στον κώδικα. |
| A scanned PDF file to test with | Θα το μετατρέψουμε σε αναζητήσιμο PDF. |

Αν έχετε ήδη ένα project, απλώς προσθέστε το πακέτο OCR μέσω του Package Manager Console:

```powershell
Install-Package Aspose.OCR
```

*(Αντικαταστήστε το `Aspose.OCR` με τη βιβλιοθήκη της επιλογής σας· το API που δείχνουμε είναι αρκετά γενικό.)*

---

## Υλοποίηση Βήμα‑βήμα

Κάθε βήμα περιλαμβάνει τον ακριβή κώδικα C# που μπορείτε να αντιγράψετε‑επικολλήσετε, μαζί με μια σύντομη εξήγηση του **γιατί** υπάρχει η γραμμή.

### Βήμα 1: Αρχικοποίηση του OCR Engine  

Η δημιουργία του engine είναι το πρώτο πράγμα που κάνετε επειδή κρατά όλες τις ρυθμίσεις και την κατάσταση για την εκτέλεση της αναγνώρισης.

```csharp
using Aspose.OCR;          // <-- OCR library namespace
using System.IO;           // needed for file handling

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Pro tip:** Η επαναχρησιμοποίηση ενός μόνο αντικειμένου `OcrEngine` για πολλά αρχεία μειώνει την κατανάλωση μνήμης, ειδικά όταν επεξεργάζεστε μεγάλες δέσμες.

### Βήμα 2: Διαμόρφωση του Engine για Αναζητήσιμο PDF  

Το engine μπορεί να παράγει απλό κείμενο, εικόνες ή ένα αναζητήσιμο PDF. Ορίζοντας τη σωστή λειτουργία λέτε στη βιβλιοθήκη να ενσωματώσει ένα αόρατο στρώμα κειμένου πίσω από τις αρχικές εικόνες των σελίδων.

```csharp
// Step 2: Tell the engine to produce a searchable PDF
ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
```

*Γιατί;* Χωρίς αυτή τη σημαία η εκτέλεση OCR θα σας δώσει μόνο ένα `string` με το αναγνωρισμένο κείμενο, κάτι που δεν είναι χρήσιμο αν χρειάζεστε ακόμη τη διάταξη της αρχικής σελίδας.

### Βήμα 3: Φόρτωση του Σαρωμένου Εγγράφου  

Οι περισσότερες SDK OCR δέχονται ένα `Image` ή `ImageStream`. Εδώ χρησιμοποιούμε ένα βοηθητικό εργαλείο που διαβάζει ένα αρχείο PDF και αντιμετωπίζει κάθε σελίδα ως εικόνα.

```csharp
// Step 3: Load the scanned PDF you want to convert
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\scanned.pdf");
```

> **Edge case:** Αν το PDF σας περιέχει μιξάριστες raster και vector σελίδες, ορισμένα engines μπορεί να παραλείψουν τις vector σελίδες. Σε αυτή την περίπτωση, προ‑μετατρέψτε το PDF σε εικόνες (π.χ., με Ghostscript) πριν το δώσετε στο OCR engine.

### Βήμα 4: Εκτέλεση της Αναγνώρισης OCR  

Καλώντας το `Recognize()` γίνεται η βαριά δουλειά — ανίχνευση κειμένου, μοντελοποίηση γλώσσας και δημιουργία PDF—all behind the scenes.

```csharp
// Step 4: Run OCR; the result includes the searchable PDF object
var ocrResult = ocrEngine.Recognize();
```

Αν χρειάζεστε επίσης **extract text from pdf**, μπορείτε να το πάρετε από `ocrResult.Text`:

```csharp
string extractedText = ocrResult.Text;   // plain text version
```

### Βήμα 5: Αποθήκευση του Αναζητήσιμου PDF  

Τέλος, γράψτε το αποτέλεσμα στο δίσκο. Η ιδιότητα `PdfDocument` περιέχει ένα πλήρως σχηματισμένο PDF με αόρατο επικάλυμμα κειμένου.

```csharp
// Step 5: Persist the searchable PDF
ocrResult.PdfDocument.Save(@"C:\Docs\searchable.pdf");
```

Όταν ανοίξετε το `searchable.pdf` στο Adobe Reader ή στο Edge, θα μπορείτε να πληκτρολογήσετε μια λέξη στο πεδίο Find και να μεταβείτε αμέσως στη θέση όπου εμφανίζεται — όπως σε ένα φυσικό PDF.

---

## Επαλήθευση του Αποτελέσματος

1. Ανοίξτε το παραγόμενο αρχείο σε οποιονδήποτε PDF viewer.  
2. Πατήστε **Ctrl + F** και πληκτρολογήστε μια λέξη που γνωρίζετε ότι εμφανίζεται στις σαρωμένες σελίδες.  
3. Αν ο viewer επισημάνει τον όρο, έχετε δημιουργήσει επιτυχώς **create searchable pdf**.

Αν δεν βρεθεί τίποτα, ελέγξτε ξανά ότι το αρχικό PDF περιέχει αναγνώσιμο κείμενο (ορισμένες σάρωση είναι τόσο χαμηλής ανάλυσης που το OCR δεν μπορεί να αναγνωρίσει τίποτα). Η αύξηση του DPI πριν το OCR (π.χ., `ocrEngine.Config.Dpi = 300`) βοηθά συχνά.

---

## Συνηθισμένα Προβλήματα & Πώς να τα Διορθώσετε

| Σύμπτωμα | Πιθανή αιτία | Διόρθωση |
|----------|--------------|----------|
| Blank searchable PDF | `PdfConversionMode` left at default (image‑only) | Ορίστε `PdfConversionMode = PdfConversionMode.SearchablePdf`. |
| Garbled characters | Wrong language model | `ocrEngine.Config.Language = Language.English;` (ή η κατάλληλη γλώσσα). |
| Slow processing on large files | Engine re‑initializes per page | Επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine`, ή ενεργοποιήστε multi‑threading αν η βιβλιοθήκη το υποστηρίζει. |
| No text searchable after conversion | Input PDF is vector‑only (no raster images) | Μετατρέψτε πρώτα τις σελίδες PDF σε εικόνες (π.χ., `PdfRenderer` από Aspose.PDF). |

---

## Bonus: Εξαγωγή Κειμένου Απευθείας από το Αναζητήσιμο PDF  

Μερικές φορές χρειάζεστε το ακατέργαστο κείμενο για ευρετηρίαση ή ανάλυση. Εφόσον το `ocrResult` ήδη παρέχει το `Text`, μπορείτε να παραλείψετε το άνοιγμα του PDF ξανά. Ωστόσο, αν αργότερα έχετε μόνο το αρχείο PDF, χρησιμοποιήστε έναν εξαγωγέα κειμένου PDF:

```csharp
using Aspose.Pdf;   // PDF library for reading

var pdfDoc = new Document(@"C:\Docs\searchable.pdf");
var textAbsorber = new TextAbsorber();
pdfDoc.Pages.Accept(textAbsorber);
string fullText = textAbsorber.Text;
```

Τώρα έχετε **extract text from pdf** χωρίς να τρέξετε ξανά OCR — μια χρήσιμη συντόμευση όταν επεξεργάζεστε πολλά αρχεία.

---

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα σε Ένα Αρχείο)

```csharp
// ------------------------------------------------------------
// Full C# example: Convert a scanned PDF into a searchable PDF
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.Pdf;               // For optional text extraction
using Aspose.Pdf.Text;          // TextAbsorber class

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Configure for searchable PDF output
            ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
            // Optional: set language and DPI for better accuracy
            ocrEngine.Config.Language = Language.English;
            ocrEngine.Config.Dpi = 300;

            // 3️⃣ Load the scanned document (replace path as needed)
            string inputPath = @"C:\Docs\scanned.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 4️⃣ Run OCR – this creates both PDF and plain‑text results
            var ocrResult = ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\searchable.pdf";
            ocrResult.PdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");

            // 🎉 Bonus: Extract plain text without opening the PDF again
            string extractedText = ocrResult.Text;
            Console.WriteLine("\n--- Extracted Text Preview ---");
            Console.WriteLine(extractedText.Substring(0,
                Math.Min(300, extractedText.Length)) + "...");

            // Optional: Verify by re‑reading the PDF
            var pdfDoc = new Document(outputPath);
            var absorber = new TextAbsorber();
            pdfDoc.Pages.Accept(absorber);
            Console.WriteLine("\nText extracted from saved PDF:");
            Console.WriteLine(absorber.Text.Substring(0,
                Math.Min(300, absorber.Text.Length)) + "...");
        }
    }
}
```

**Expected output** (truncated for brevity):

```
Searchable PDF saved to: C:\Docs\searchable.pdf

--- Extracted Text Preview ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

Text extracted from saved PDF:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Αν δείτε το ίδιο απόσπασμα δύο φορές, το OCR πέτυχε και το PDF περιέχει πλέον ένα αναζητήσιμο στρώμα κειμένου.

---

## Επόμενα Βήματα & Σχετικά Θέματα

- **Batch processing:** Επανάληψη πάνω σε έναν φάκελο σαρωμένων PDF, επαναχρησιμοποιώντας το ίδιο αντικείμενο `OcrEngine` για βελτιωμένη απόδοση.  
- **Language detection:** Για πολυγλωσσικά αρχεία, αλλάξτε δυναμικά το `ocrEngine.Config.Language` βάσει των μεταδεδομένων του αρχείου.  
- **PDF/A compliance:** Ορισμένες βιομηχανίες απαιτούν αρχειοθετημένα PDF· ορίστε `PdfConversionMode = PdfConversionMode.SearchablePdfA` αν το SDK σας το υποστηρίζει.  
- **Performance tuning:** Πειραματιστείτε με `ocrEngine.Config.UseParallelProcessing = true` (αν είναι διαθέσιμο) για επιτάχυνση μεγάλων εργασιών.

Όλα αυτά βασίζονται στην κεντρική ιδέα του **how to run OCR** αποδοτικά ενώ **create searchable pdf** αρχεία που είναι αμέσως ευρετήσιμα.

---

## Συμπέρασμα

Τώρα έχετε μια πλήρη, έτοιμη για παραγωγή συνταγή για να μετατρέψετε οποιοδήποτε σαρωμένο έγγραφο σε ένα **create searchable pdf** αριστούργημα. Διαμορφώνοντας τη μηχανή OCR, φορτώνοντας την πηγή, εκτελώντας την αναγνώριση και αποθηκεύοντας το αποτέλεσμα, καλύψατε ολόκληρη τη ροή — από ακατέργαστη εικόνα μέχρι αναζητήσιμο, εξαγώγιμο PDF.  

Δοκιμάστε το με τα δικά σας αρχεία, προσαρμόστε το DPI ή τις ρυθμίσεις γλώσσας, και θα 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}