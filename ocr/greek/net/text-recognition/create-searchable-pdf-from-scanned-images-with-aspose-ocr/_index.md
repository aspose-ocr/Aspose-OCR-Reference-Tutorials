---
category: general
date: 2026-02-27
description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένο PDF σε δευτερόλεπτα χρησιμοποιώντας
  το Aspose OCR. Μάθετε πώς να μετατρέψετε σαρωμένα PDF, να κάνετε OCR μετατροπή PDF
  και να εξάγετε κείμενο από PDF χωρίς κόπο.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr convert pdf
- extract text from pdf
- convert image pdf
language: el
og_description: Δημιουργήστε άμεσα PDF με δυνατότητα αναζήτησης. Αυτό το σεμινάριο
  δείχνει πώς να μετατρέψετε σαρωμένα PDF, να κάνετε OCR μετατροπή PDF και να εξάγετε
  κείμενο από PDF με το Aspose OCR.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης – Γρήγορος οδηγός Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Δημιουργία PDF με δυνατότητα αναζήτησης από σαρωμένες εικόνες με Aspose OCR
url: /el/net/text-recognition/create-searchable-pdf-from-scanned-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Σαρωμένες Εικόνες με Aspose OCR

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από ένα τιμολόγιο μόνο σε χαρτί αλλά δεν ξέρατε από πού να ξεκινήσετε; Με το Aspose OCR μπορείτε να **δημιουργήσετε αναζητήσιμο PDF** με λίγες μόνο γραμμές C#—χωρίς εξωτερικές υπηρεσίες, χωρίς χειροκίνητη αντιγραφή‑επικόλληση.  

Σε αυτόν τον οδηγό θα περάσουμε από όλα όσα χρειάζεστε για να **μετατρέψετε σαρωμένα pdf** αρχεία σε πλήρως αναζητήσιμα PDF, θα εξηγήσουμε γιατί κάθε βήμα είναι σημαντικό και ακόμη θα δείξουμε πώς να **εξάγετε κείμενο από pdf** εάν προτιμάτε ακατέργαστες συμβολοσειρές αντί για έξοδο PDF. Στο τέλος θα έχετε ένα επαναχρησιμοποιήσιμο snippet που αντιμετωπίζει το κοινό πρόβλημα του “PDF μόνο με εικόνες” και μια σειρά συμβουλών για ειδικές περιπτώσεις.

![δημιουργία αναζητήσιμου pdf με χρήση Aspose OCR](image-placeholder.png "δημιουργία αναζητήσιμου pdf με χρήση Aspose OCR")

## Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (το API λειτουργεί σε .NET Core, .NET Framework και .NET 5+)
- Visual Studio 2022 (ή οποιονδήποτε επεξεργαστή προτιμάτε)
- Ένα πακέτο NuGet Aspose OCR (`Aspose.OCR`) – θα το εγκαταστήσουμε στο πρώτο βήμα
- Ένα σαρωμένο αρχείο PDF (μόνο εικόνα) που θέλετε να μετατρέψετε σε **αναζητήσιμο PDF**

Αυτό είναι όλο—χωρίς επιπλέον μηχανές OCR, χωρίς προβλήματα άδειας για δοκιμαστική εκτέλεση.  

Τώρα, ας βουτήξουμε.

## Βήμα 1: Εγκατάσταση της Βιβλιοθήκης Aspose OCR (και μια Γρήγορη Συμβουλή)

Πριν τρέξει οποιοσδήποτε κώδικας, η βιβλιοθήκη πρέπει να αναφερθεί. Ανοίξτε ένα τερματικό στο φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

> **Συμβουλή:** Εάν χρησιμοποιείτε το Package Manager του Visual Studio, αναζητήστε το “Aspose.OCR” και κάντε κλικ στο **Install**. Η δωρεάν δοκιμή λειτουργεί για έως και 20 σελίδες, κάτι ιδανικό για δοκιμές.

Η εγκατάσταση του πακέτου σας δίνει πρόσβαση στα `OcrEngine`, `OcrLanguage` και `OcrOutputFormat`—τις τρεις κλάσεις που θα χρησιμοποιήσουμε για **ocr convert pdf**.

## Βήμα 2: Διαμόρφωση της Μηχανής OCR (Δημιουργία Αναζητήσιμου PDF – Βασικές Ρυθμίσεις)

Η μηχανή πρέπει να γνωρίζει ποια γλώσσα θα αναγνωρίσει και ποια μορφή εξόδου αναμένετε. Στην περίπτωσή μας θέλουμε ένα PDF αγγλικής γλώσσας που να είναι αναζητήσιμο.

```csharp
using Aspose.OCR;
using System;

// Step 2: Set up the OCR engine
var ocrEngine = new OcrEngine
{
    // Choose the language of the source document
    Language = OcrLanguage.English,

    // Tell Aspose we want a searchable PDF as the result
    OutputFormat = OcrOutputFormat.SearchablePdf
};
```

Γιατί να ορίσουμε ρητά το `Language`; Η ακρίβεια του OCR μειώνεται δραματικά όταν η μηχανή μαντεύει τη γλώσσα, ειδικά για έγγραφα που περιέχουν αριθμούς ή μικτές γραφές. Με το να το θέσουμε στα Αγγλικά παίρνουμε πιο καθαρά επίπεδα κειμένου, κάτι που βελτιώνει το βήμα **extract text from pdf** αργότερα.

## Βήμα 3: Μετατροπή Σαρωμένου PDF σε Αναζητήσιμο PDF

Τώρα που η μηχανή είναι έτοιμη, δείξτε την στο αρχείο προέλευσης και πείτε της πού να γράψει το αποτέλεσμα. Αυτή η ενιαία κλήση κάνει το σκληρό έργο: rasterizes κάθε σελίδα, εκτελεί OCR και γράφει ένα νέο PDF με ένα αόρατο επίπεδο κειμένου.

```csharp
// Step 3: Perform the conversion
ocrEngine.RecognizePdf(
    @"C:\Docs\invoice_scanned.pdf",   // input – image‑only PDF
    @"C:\Docs\invoice_searchable.pdf" // output – searchable PDF
);
```

Εάν το PDF προέλευσης περιέχει πολλαπλές σελίδες, το Aspose OCR τις επεξεργάζεται διαδοχικά, διατηρώντας την αρχική διάταξη. Το αρχείο εξόδου μπορεί να ανοιχθεί σε οποιονδήποτε προβολέα PDF· θα παρατηρήσετε ότι μπορείτε τώρα να επιλέγετε και να αναζητάτε λέξεις που προηγουμένως ήταν μόνο εικόνες.

### Επαλήθευση του Αποτελέσματος (Extract Text from PDF)

Για να είστε απολύτως σίγουροι ότι η μετατροπή πέτυχε, ίσως θέλετε να εξάγετε προγραμματιστικά το κείμενο:

```csharp
using Aspose.Pdf;           // Add Aspose.PDF if you also need text extraction
using System.Text;

// Load the newly created searchable PDF
var doc = new Document(@"C:\Docs\invoice_searchable.pdf");
var sb = new StringBuilder();

foreach (Page page in doc.Pages)
{
    // Extract the hidden text layer
    sb.Append(page.Text);
}

Console.WriteLine("Extracted text:\n" + sb.ToString());
```

Αυτό το snippet δείχνει πώς μπορείτε να **extract text from pdf** μετά το βήμα OCR, κάτι χρήσιμο για ευρετηρίαση ή τροφοδοσία του περιεχομένου σε μηχανή αναζήτησης. Σημειώστε ότι χρειάζεστε το ξεχωριστό πακέτο `Aspose.PDF` για αυτό το μέρος· είναι ένα ελαφρύ πρόσθετο.

## Βήμα 4: Διαχείριση Συνηθισμένων Ακραίων Περιπτώσεων Όταν **Convert Image PDF**

Ενώ η βασική ροή λειτουργεί για τα περισσότερα PDF, τα πραγματικά αρχεία μπορούν να παρουσιάσουν απρόοπτα:

| Κατάσταση | Γιατί Συμβαίνει | Πώς να το Διαχειριστείτε |
|-----------|----------------|--------------------------|
| **Σελίδες με περιστροφή** | Οι σαρωτές μερικές φορές περιστρέφουν τις σελίδες αυτόματα κατά 90°. | Ορίστε `ocrEngine.RotatePages = true` πριν καλέσετε το `RecognizePdf`. |
| **Μικτές γλώσσες** | Τα τιμολόγια μπορεί να περιέχουν γαλλικούς ή γερμανικούς όρους. | Χρησιμοποιήστε `OcrLanguage.Multilingual` ή συνδυάστε πολλαπλές γλώσσες με `|` (π.χ., `OcrLanguage.English | OcrLanguage.French`). |
| **Μεγάλα αρχεία (> 100 σελίδες)** | Οι περιορισμοί της δωρεάν δοκιμής μπορούν να σταματήσουν την επεξεργασία ενδιάμεσα στο αρχείο. | Αγοράστε άδεια ή χωρίστε το PDF σε τμήματα χρησιμοποιώντας το `Aspose.Pdf` πριν το OCR. |
| **Σαρώσεις χαμηλής ανάλυσης** | Το κείμενο γίνεται θολό, η ακρίβεια του OCR μειώνεται. | Αυξήστε το DPI χρησιμοποιώντας `ocrEngine.ImageResolution = 300` (η προεπιλογή είναι 200). |

Η αντιμετώπιση αυτών των σεναρίων εξασφαλίζει ότι η **ocr convert pdf** pipeline σας παραμένει ανθεκτική στην παραγωγή.

## Βήμα 5: Αυτοματοποίηση της Ολόκληρης Διαδικασίας (Συσκευασία σε Μέθοδο)

Εάν δημιουργείτε μια υπηρεσία επεξεργασίας τιμολογίων, πιθανότατα θα θέλετε μια επαναχρησιμοποιήσιμη μέθοδο. Εδώ είναι μια συμπαγής έκδοση που δέχεται διαδρομές εισόδου και εξόδου, διαχειρίζεται την περιστροφή και επιστρέφει το εξαγόμενο κείμενο.

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Text;

public static class PdfSearchableHelper
{
    /// <summary>
    /// Converts an image‑only PDF to a searchable PDF and returns the hidden text.
    /// </summary>
    /// <param name="inputPath">Path to the scanned PDF.</param>
    /// <param name="outputPath">Path where the searchable PDF will be saved.</param>
    /// <returns>All extracted text as a single string.</returns>
    public static string ConvertAndExtract(string inputPath, string outputPath)
    {
        // 1️⃣ Initialize OCR engine
        var ocr = new OcrEngine
        {
            Language = OcrLanguage.English,
            OutputFormat = OcrOutputFormat.SearchablePdf,
            RotatePages = true,            // fixes rotated scans automatically
            ImageResolution = 300          // improve accuracy on low‑res scans
        };

        // 2️⃣ Perform conversion
        ocr.RecognizePdf(inputPath, outputPath);

        // 3️⃣ Load result and pull out hidden text
        var doc = new Document(outputPath);
        var sb = new StringBuilder();

        foreach (Page page in doc.Pages)
            sb.Append(page.Text);

        return sb.ToString();
    }
}
```

Τώρα μπορείτε να καλέσετε:

```csharp
string extracted = PdfSearchableHelper.ConvertAndExtract(
    @"C:\Docs\contract_scanned.pdf",
    @"C:\Docs\contract_searchable.pdf");

Console.WriteLine("OCR completed. Extracted text length: " + extracted.Length);
```

Αυτή είναι μια πλήρης ροή εργασίας **convert image pdf** → **searchable PDF**, όλα ενσωματωμένα σε μια μόνο μέθοδο που μπορείτε να ενσωματώσετε σε οποιαδήποτε υπηρεσία ASP.NET Core ή εφαρμογή κονσόλας.

## Συχνές Ερωτήσεις (FAQ)

**Q: Λειτουργεί αυτό σε macOS/Linux;**  
A: Απόλυτα. Το runtime .NET 6 και το Aspose OCR είναι cross‑platform, έτσι ο ίδιος κώδικας εκτελείται σε Windows, macOS και Linux containers.

**Q: Τι γίνεται αν χρειάζομαι μόνο το κείμενο και δεν με ενδιαφέρει το αναζητήσιμο PDF;**  
A: Παραλείψτε το βήμα `OutputFormat` και ορίστε `OutputFormat = OcrOutputFormat.Text`. Η μηχανή θα επιστρέψει άμεσα απλό κείμενο.

**Q: Μπορώ να διατηρήσω τα μεταδεδομένα του αρχικού PDF;**  
A: Ναι. Μετά τη μετατροπή, μπορείτε να αντιγράψετε τα μεταδεδομένα από το αντικείμενο `Document` προέλευσης στο νέο χρησιμοποιώντας `doc.Info.Title`, `doc.Info.Author`, κ.λπ.

**Q: Υπάρχει όριο στον αριθμό των σελίδων;**  
A: Η δωρεάν δοκιμή περιορίζεται σε 20 σελίδες ανά έγγραφο. Μια πλήρης άδεια αφαιρεί αυτόν τον περιορισμό.

## Συμπέρασμα

Τώρα ξέρετε πώς να **create searchable PDF**

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}