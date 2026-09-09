---
category: general
date: 2026-01-04
description: Δημιουργήστε αναζητήσιμο PDF από ένα σαρωμένο PDF γρήγορα. Μάθετε πώς
  να μετατρέψετε σαρωμένο PDF, να προσθέσετε OCR σε PDF και να ρυθμίσετε την ποιότητα
  εικόνας με το Aspose OCR σε C#.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από ένα σαρωμένο PDF γρήγορα. Ακολουθήστε
  αυτόν τον οδηγό βήμα‑βήμα για να μετατρέψετε το σαρωμένο PDF, να προσθέσετε OCR
  στο PDF και να ρυθμίσετε την ποιότητα της εικόνας.
og_title: Δημιουργία PDF με δυνατότητα αναζήτησης από σαρωμένα αρχεία με τη χρήση
  του Aspose OCR
tags:
- Aspose OCR
- C#
- PDF processing
title: Δημιουργία Αναζητήσιμου PDF από Σαρωμένα Αρχεία με τη χρήση Aspose OCR
url: /el/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Σαρωμένα Αρχεία Χρησιμοποιώντας το Aspose OCR

Έχετε χρειαστεί ποτέ να **δημιουργήσετε αναζητήσιμο PDF** από ένα σωρό σαρωμένων εγγράφων αλλά δεν ήξερες από πού να ξεκινήσεις; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν χτίζουν pipelines διαχείρισης εγγράφων. Το καλό νέο; Με το Aspose OCR μπορείτε να **μετατρέψετε σαρωμένο PDF**, να προσθέσετε OCR και να ρυθμίσετε την ποιότητα της εικόνας με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε από τη διαδικασία από τη φόρτωση ενός σαρωμένου PDF μέχρι την αποθήκευση μιας πλήρως αναζητήσιμης έκδοσης. Στο τέλος θα γνωρίζετε ακριβώς **πώς να χρησιμοποιήσετε OCR** με το Aspose, γιατί κάθε ρύθμιση είναι σημαντική και τι να προσαρμόσετε όταν κάτι δεν πάει όπως προβλέπεται. Χωρίς ασαφείς αναφορές—μόνο ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο πρότζεκτ σας σήμερα.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)
- Ένα έγκυρο λ licenc Aspose OCR (η δωρεάν δοκιμή λειτουργεί για δοκιμές)
- Ένα αρχείο PDF με όνομα `input.pdf` τοποθετημένο σε φάκελο που ελέγχετε
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή C# προτιμάτε

Αυτό είναι όλο. Αν κάτι από αυτά δεν σας είναι γνωστό, κάντε παύση και εγκαταστήστε το απαιτούμενο κομμάτι—δεν χρειάζεται τίποτα άλλο.

## Βήμα 1: Αρχικοποίηση του OCR Engine και Φόρτωση του Σαρωμένου PDF  
**(Εδώ **προσθέτουμε OCR στο PDF** για πρώτη φορά.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*Γιατί αυτό το βήμα;*  
Το `OcrEngine` είναι η καρδιά του Aspose OCR. Η φόρτωση του PDF λέει στο engine πού να ψάξει για τις raster εικόνες που θα αναλύσει αργότερα. Αν το παραλείψετε, δεν υπάρχει τίποτα προς μετατροπή και τα επόμενα βήματα θα πετάξουν εξαίρεση.

> **Pro tip:** Αν το PDF σας είναι προστατευμένο με κωδικό, χρησιμοποιήστε `ocrEngine.LoadPdf(path, password)` για να αποφύγετε σφάλμα χρόνου εκτέλεσης.

## Βήμα 2: Ορισμός Πρωτεύουσας και Πρόσθετων Γλωσσών  
**(Θα **μετατρέψουμε σαρωμένο PDF** στα Αγγλικά, Γαλλικά και Γερμανικά.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*Γιατί η γλώσσα έχει σημασία;*  
Η ακρίβεια του OCR εξαρτάται από το σύνολο χαρακτήρων που αναμένει. Δηλώνοντας τα Αγγλικά ως κύρια γλώσσα και προσθέτοντας Γαλλικά/Γερμανικά, το engine μπορεί να ερμηνεύσει σωστά τους τονισμένους χαρακτήρες και τα ειδικά σύμβολα. Η παράλειψη αυτού συχνά οδηγεί σε ακατάληπτο κείμενο.

## Βήμα 3: Ρύθμιση Ποιότητας Εικόνας – Λεπτομερής Ρύθμιση της Εξόδου PDF  
**(Εδώ **ρυθμίζουμε την ποιότητα εικόνας** για να ισορροπήσουμε το μέγεθος αρχείου και την αναγνωσιμότητα.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*Γιατί να ρυθμίσουμε το `ImageQuality`;*  
Μια υψηλότερη τιμή (90‑100) διατηρεί την ευκρίνεια, κάτι κρίσιμο για την ακρίβεια του OCR, αλλά αυξάνει και το μέγεθος του αρχείου. Αν αρχειοθετείτε εκατομμύρια σελίδες, μειώστε το σε 70‑80 για ένα πιο ελαφρύ PDF χωρίς να θυσιάσετε υπερβολικά την αναγνωσιμότητα.

## Βήμα 4: Αποθήκευση του Αποτελέσματος ως Αναζητήσιμο PDF  
**(Τώρα τελικά **δημιουργούμε αναζητήσιμο PDF** που μπορείτε να ευρετηριάσετε.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*Τι συμβαίνει στην πραγματικότητα;*  
Το Aspose OCR εξάγει το στρώμα κειμένου από κάθε σελίδα και το ενσωματώνει πίσω από την αρχική εικόνα. Το PDF παραμένει οπτικά το ίδιο, αλλά τώρα μπορείτε να επιλέξετε, αντιγράψετε και αναζητήσετε το κείμενο—ένα τεράστιο πλεονέκτημα για τις επόμενες εργασίες.

## Βήμα 5: Επαλήθευση της Εξόδου (Προαιρετικό αλλά Συνιστάται)  
Είναι εύκολο να υποθέσετε ότι όλα λειτούργησαν, αλλά ένας γρήγορος έλεγχος αποτρέπει μελλοντικά προβλήματα.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

Ανοίξτε το αρχείο, δοκιμάστε να επιλέξετε μια λέξη ή πατήστε `Ctrl+F` και πληκτρολογήστε μια φράση που γνωρίζετε ότι υπάρχει στην αρχική σάρωση. Αν το κείμενο είναι επιλέξιμο, έχετε δημιουργήσει επιτυχώς **αναζητήσιμο PDF**.

## Συνηθισμένες Ακραίες Περιπτώσεις & Πώς να τις Διαχειριστείτε  

| Κατάσταση | Γιατί Συμβαίνει | Γρήγορη Λύση |
|-----------|----------------|--------------|
| **Σελίδες με ανάμεικτη ανάλυση** (μερικές 150 dpi, άλλες 300 dpi) | Η ποιότητα του OCR διαφέρει ανά σελίδα, οδηγώντας σε άνιση αναζητησιμότητα. | Ορίστε `ocrEngine.Config.Dpi = 300;` πριν τη φόρτωση για να εξαναγκάσετε up‑sampling, ή προεπεξεργαστείτε με `ImageProcessor` για ομαλοποίηση DPI. |
| **Κρυπτογραφημένο PDF** | Το Aspose OCR δεν μπορεί να διαβάσει χωρίς κωδικό. | Περνάτε τον κωδικό στο `LoadPdf` όπως φαίνεται παραπάνω. |
| **Μεγάλα PDFs (>500 MB)** | Η κατανάλωση μνήμης αυξάνεται, προκαλώντας `OutOfMemoryException`. | Επεξεργαστείτε το έγγραφο σε τμήματα: `ocrEngine.SplitPdfIntoPages();` στη συνέχεια OCR κάθε σελίδα ξεχωριστά και συγχωνεύστε τα αποτελέσματα. |
| **Μη‑λατινικοί χαρακτήρες** (π.χ. Κυριλλικοί) | Η γλώσσα δεν έχει προστεθεί, οπότε οι χαρακτήρες γίνονται “?”. | Προσθέστε `Language.Russian` (ή οποιαδήποτε απαιτούμενη γλώσσα) στα `AdditionalLanguages`. |
| **Πολύ χαμηλή ποιότητα εικόνας** | Το κείμενο γίνεται θολό, το OCR αποτυγχάνει. | Αυξήστε το `ImageQuality` ή χρησιμοποιήστε `pdfOptions.Dpi = 300;` για ενσωμάτωση εικόνων υψηλότερης ανάλυσης. |

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα  

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε μια νέα εφαρμογή console. Περιλαμβάνει όλα τα βήματα, διαχείριση σφαλμάτων και σχόλια για σαφήνεια.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**Αναμενόμενη έξοδος:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

Όταν ανοίξετε το `output.pdf`, θα πρέπει να μπορείτε να επιλέξετε και να αναζητήσετε οποιοδήποτε κείμενο υπήρχε στην αρχική σάρωση.

---

## Συχνές Ερωτήσεις (FAQs)

**Ε: Λειτουργεί αυτό με PDFs που περιέχουν τόσο σαρωμένες εικόνες όσο και εγγενές κείμενο;**  
Α: Απόλυτα. Το Aspose OCR προσθέτει ένα κρυφό στρώμα κειμένου μόνο όπου χρειάζεται, αφήνοντας το υπάρχον κείμενο αμετάβλητο.

**Ε: Μπορώ να επεξεργαστώ μαζικά έναν φάκελο PDFs;**  
Α: Ναι. Τυλίξτε τον παραπάνω κώδικα μέσα σε έναν βρόχο `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` και προσαρμόστε το μονοπάτι εξόδου ανάλογα.

**Ε: Πώς μπορώ να μειώσω περαιτέρω το τελικό μέγεθος του PDF;**  
Α: Μειώστε το `ImageQuality` σε 70‑80, ενεργοποιήστε `Compress`, ή χρησιμοποιήστε `pdfOptions.Dpi = 150` για downsample των εικόνων πριν την ενσωμάτωση.

**Ε: Υπάρχει τρόπος να εξάγω το κείμενο OCR χωρίς να δημιουργήσω PDF;**  
Α: Καλέστε `ocrEngine.ExtractText();` μετά τη φόρτωση του PDF. Αυτό επιστρέφει μια συμβολοσειρά plain‑text που μπορείτε να αποθηκεύσετε ή να ευρετηριάσετε.

---

## Συμπέρασμα  

Μόλις καλύψαμε **πώς να χρησιμοποιήσετε OCR** με το Aspose για να **δημιουργήσετε αναζητήσιμο PDF** από ένα σαρωμένο έγγραφο, σας δείξαμε πώς να **μετατρέψετε σαρωμένο PDF**, να **προσθέσετε OCR σε PDF**, και εξηγήσαμε πώς να **ρυθμίσετε την ποιότητα εικόνας** για βέλτιστα αποτελέσματα. Το πλήρες δείγμα κώδικα είναι έτοιμο για εκτέλεση, και ο πίνακας αντιμετώπισης προβλημάτων θα σας κρατήσει σε κίνηση όταν προκύψουν απρόοπτα.

Τι ακολουθεί; Δοκιμάστε:

- Διαφορετικά πακέτα γλωσσών για πολύγλωσσα αρχεία
- Προσαρμοσμένη προεπεξεργασία εικόνας (απλοποίηση, απομάκρυνση θορύβου) μέσω `ImageProcessor`
- Ενσωμάτωση του αναζητήσιμου PDF σε pipeline SharePoint ή ElasticSearch

Μη διστάσετε να αφήσετε σχόλιο αν αντιμετωπίσετε πρόβλημα ή ανακαλύψετε έξυπνη βελτίωση. Καλή προγραμματιστική δουλειά και απολαύστε τα άμεσα αναζητήσιμα PDFs! 

![Διάγραμμα ροής δημιουργίας αναζητήσιμου PDF που δείχνει OCR engine → ρυθμίσεις γλώσσας → επιλογές αποθήκευσης PDF → έξοδος αναζητήσιμου PDF](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}