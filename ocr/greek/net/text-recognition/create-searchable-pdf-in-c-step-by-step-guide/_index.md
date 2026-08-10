---
category: general
date: 2026-03-02
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από σκαναρισμένο PDF εικόνας
  χρησιμοποιώντας το Aspose OCR. Μάθετε πώς να μετατρέψετε σκαναρισμένο PDF εικόνας
  σε PDF/A‑2b και να εξάγετε κείμενο PDF σε λίγα λεπτά.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to create pdf/a
- extract text pdf
- image to searchable pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένες εικόνες. Αυτός ο οδηγός
  δείχνει πώς να μετατρέψετε το PDF σαρωμένης εικόνας σε PDF/A‑2b και να εξάγετε κείμενο
  PDF χρησιμοποιώντας το Aspose OCR.
og_title: Δημιουργία Αναζητήσιμου PDF σε C# – Πλήρης Οδηγός
tags:
- C#
- Aspose
- OCR
- PDF/A
title: Δημιουργία Αναζητήσιμου PDF σε C# – Οδηγός Βήμα‑βήμα
url: /el/net/text-recognition/create-searchable-pdf-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF σε C# – Πλήρης Οδηγός

Έχετε ποτέ χρειαστεί να **δημιουργήσετε αναζητήσιμο PDF** από ένα σαρωμένο έγγραφο αλλά δεν ήξερτε από πού να ξεκινήσετε; Δεν είστε μόνοι· πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν η ροή εργασίας τους απαιτεί ένα αναζητήσιμο αρχείο αντί για μια επίπεδη εικόνα. Τα καλά νέα; Με λίγες γραμμές C# και Aspose OCR μπορείτε να μετατρέψετε οποιοδήποτε σαρωμένο TIFF (ή άλλη εικόνα) σε αρχείο PDF/A‑2b που είναι αμέσως αναζητήσιμο και έτοιμο για εξαγωγή κειμένου.

Σε αυτόν τον οδηγό θα περάσουμε από όλη τη διαδικασία—φόρτωση μιας σαρωμένης εικόνας, εκτέλεση OCR, μετατροπή του αποτελέσματος σε έγγραφο PDF/A‑2b και τελικά αποθήκευση ενός **αναζητήσιμου PDF** που μπορείτε να ευρετηριάσετε. Στο τέλος θα γνωρίζετε επίσης πώς να **μετατρέψετε σαρωμένο PDF εικόνας** σε PDF/A σύμφωνο με τα πρότυπα, πώς να **εξάγετε κείμενο PDF** αργότερα, και τι να ρυθμίσετε αν χρειαστεί να διαχειριστείτε πολυ‑σελίδες TIFF ή διαφορετικές γλώσσες OCR.

> **Συμβουλή:** Αν έχετε ήδη ένα PDF που αποτελείται μόνο από εικόνες, μπορείτε να εξάγετε κάθε σελίδα ως εικόνα και να τη δώσετε στην ίδια αλυσίδα επεξεργασίας—χωρίς επιπλέον εργαλεία.

## Τι Θα Χρειαστεί

- **.NET 6+** (ή .NET Framework 4.6+). Ο κώδικας μεταγλωττίζεται με οποιονδήποτε πρόσφατο μεταγλωττιστή C#.
- **Aspose.OCR** και **Aspose.Pdf** πακέτα NuGet. Εγκαταστήστε τα μέσω `dotnet add package Aspose.OCR` και `dotnet add package Aspose.Pdf`.
- Ένα **σαρωμένο TIFF** (ή JPEG/PNG) που θέλετε να μετατρέψετε σε αναζητήσιμο αρχείο PDF/A‑2b.
- Ένα κειμενογράφο ή IDE (Visual Studio, VS Code, Rider—επιλέξτε το αγαπημένο σας).

Δεν απαιτείται ειδικό υλικό, εξωτερικές υπηρεσίες ή μυστικά αρχεία ρυθμίσεων. Απλώς μερικές αναφορές NuGet και είστε έτοιμοι.

![Παράδειγμα δημιουργίας αναζητήσιμου PDF](/images/create-searchable-pdf.png "Δημιουργία αναζητήσιμου PDF από σαρωμένο TIFF χρησιμοποιώντας Aspose OCR")

## Βήμα 1 – Φόρτωση της Σαρωμένης Εικόνας (Κύρια Λέξη-Κλειδί σε Δράση)

Για να ξεκινήσουμε, πρέπει να διαβάσουμε τη σαρωμένη εικόνα σε ένα `Bitmap`. Το Aspose OCR λειτουργεί απευθείας με `System.Drawing.Bitmap`, οπότε οποιαδήποτε μορφή υποστηρίζεται από το GDI+ είναι αποδεκτή.

```csharp
using System.Drawing;

// Replace with the path to your scanned TIFF or other image
string inputPath = @"C:\Docs\input.tif";
Bitmap scannedImage = new Bitmap(inputPath);
```

*Γιατί είναι σημαντικό αυτό το βήμα:* Η μηχανή OCR δεν μπορεί να λειτουργήσει μόνο με διαδρομή αρχείου· χρειάζεται μια αναπαράσταση εικόνας στη μνήμη. Η πρώιμη φόρτωση της εικόνας σας επιτρέπει επίσης να ελέγξετε τις διαστάσεις, το DPI ή να εφαρμόσετε προεπεξεργασία (π.χ., ενίσχυση αντίθεσης) αν η ποιότητα της πηγής είναι χαμηλή.

## Βήμα 2 – Αρχικοποίηση της Μηχανής OCR (Convert Scanned Image PDF)

Το Aspose OCR παρέχεται με μια μηχανή μόνο CPU, η οποία είναι απολύτως επαρκής για τις περισσότερες επιτραπέζιες περιπτώσεις. Αν έχετε GPU μπορείτε να αλλάξετε μηχανή, αλλά η προεπιλογή είναι ο πιο απλός τρόπος για **convert scanned image PDF** σε αναζητήσιμο κείμενο.

```csharp
using Aspose.OCR;

// Create the OCR engine – the default CPU engine works for this demo
OcrEngine ocrEngine = new OcrEngine();
```

*Γιατί επιλέγουμε την προεπιλογή:* Αποφεύγει επιπλέον εξαρτήσεις και λειτουργεί αμέσως σε Windows, Linux και macOS. Για τεράστιες παρτίδες μπορείτε να εξετάσετε την έκδοση GPU, αλλά αυτό είναι μια βελτιστοποίηση που μπορείτε να διερευνήσετε αργότερα.

## Βήμα 3 – Αναγνώριση Κειμένου και Δημιουργία Εγγράφου PDF/A‑2b (How to Create PDF/A)

Η πραγματική μαγεία συμβαίνει όταν καλούμε τη `RecognizeToPdfA`. Αυτή η μέθοδος εκτελεί OCR στο bitmap και ενσωματώνει το παραγόμενο στρώμα κειμένου μέσα σε έναν κοντέινερ PDF/A‑2b—ιδανικό για μακροπρόθεσμη αρχειοθέτηση.

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Facades; // optional, not needed for this simple call

// Recognise the image and obtain a PDF/A‑2b document
using (PdfDocument pdfADocument = ocrEngine.RecognizeToPdfA(scannedImage, PdfAStandard.PdfA2b))
{
    // Step 4 – Save the searchable PDF/A file
    string outputPath = @"C:\Docs\output.pdf";
    pdfADocument.Save(outputPath);
}
```

*Γιατί PDF/A‑2b;* Το PDF/A είναι μια έκδοση PDF τυποποιημένη από το ISO για διατήρηση. Το επίπεδο **2b** εγγυάται ότι η οπτική εμφάνιση διατηρείται και ότι το στρώμα κειμένου είναι αναζητήσιμο—ακριβώς ό,τι χρειάζεστε όταν θέλετε να **extract text PDF** αργότερα.

## Βήμα 4 – Επαλήθευση του Αποτελέσματος (Image to Searchable PDF)

Μετά την ολοκλήρωση της αποθήκευσης, ανοίξτε το `output.pdf` σε οποιονδήποτε προβολέα PDF (Adobe Reader, Foxit, πρόγραμμα περιήγησης). Δοκιμάστε να επιλέξετε κείμενο, να αναζητήσετε μια λέξη ή να χρησιμοποιήσετε την εντολή “Copy” του προβολέα. Αν το κείμενο επισημαίνεται, έχετε μετατρέψει επιτυχώς μια εικόνα σε **searchable PDF**.

```csharp
Console.WriteLine("PDF/A‑2b file created at: " + outputPath);
```

Αν χρειάζεστε προγραμματιστική επαλήθευση του κειμένου, το Aspose PDF σας επιτρέπει να το εξάγετε:

```csharp
using Aspose.Pdf.Text;

TextAbsorber absorber = new TextAbsorber();
pdfADocument.Pages.Accept(absorber);
string extracted = absorber.Text;
Console.WriteLine("Extracted text preview (first 200 chars):");
Console.WriteLine(extracted.Substring(0, Math.Min(200, extracted.Length)));
```

*Γιατί να εξάγετε κείμενο;* Αυτό το απόσπασμα δείχνει πόσο εύκολο είναι να **extract text PDF** για ευρετηρίαση, αναζήτηση ή τροφοδοσία σε επόμενες αναλυτικές αλυσίδες.

## Βήμα 5 – Διαχείριση Σαρώσεων Πολλαπλών Σελίδων και Ρυθμίσεων Γλώσσας (Edge Cases)

### Πολυ‑σελίδες TIFF

Αν το αρχείο πηγής περιέχει πολλές σελίδες, κάντε βρόχο σε κάθε καρέ:

```csharp
for (int i = 0; i < scannedImage.GetFrameCount(FrameDimension.Page); i++)
{
    scannedImage.SelectActiveFrame(FrameDimension.Page, i);
    using (PdfDocument pageDoc = ocrEngine.RecognizeToPdfA(scannedImage, PdfAStandard.PdfA2b))
    {
        // Append each pageDoc to a master PDF (omitted for brevity)
    }
}
```

### Μη‑Αγγλικό Κείμενο

Ορίστε τη γλώσσα πριν από την αναγνώριση:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Αυτές οι ρυθμίσεις σας επιτρέπουν να **convert scanned image PDF** που περιέχει μη‑λατινικά σενάρια ή πολλαπλές σελίδες χωρίς να διακόψετε τη ροή εργασίας.

## Συνηθισμένα Παράπλευρα Προβλήματα και Πώς να Τα Αποφύγετε

- **Χαμηλής ανάλυσης εικόνες** – Η ακρίβεια του OCR μειώνεται δραματικά κάτω από 150 dpi. Αυξήστε την ανάλυση της εικόνας ή ζητήστε σάρωση υψηλότερης ανάλυσης.
- **Αντιστροφή χρώματος** – Αν η σάρωση είναι αρνητική (άσπρο κείμενο σε μαύρο), αντιστρέψτε τα χρώματα με `Graphics` πριν τη δώσετε στη μηχανή.
- **Προβλήματα διαδρομής αρχείου** – Χρησιμοποιήστε `Path.Combine` για να δημιουργήσετε διαδρομές ανεξάρτητες από το OS· αποφύγετε σκληρά καθορισμένα backslashes σε Linux.
- **Διαρροές μνήμης** – Το `Bitmap` υλοποιεί `IDisposable`. Τυλίξτε το σε μπλοκ `using` αν επεξεργάζεστε πολλά αρχεία σε βρόχο.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Drawing;

class PdfAExample
{
    static void Main()
    {
        // Step 1: Load the scanned image that will be processed
        using Bitmap scannedImage = new Bitmap(@"C:\Docs\input.tif");

        // Step 2: Create the OCR engine (default CPU engine is sufficient for this demo)
        OcrEngine ocrEngine = new OcrEngine();

        // OPTIONAL: Set language if needed
        // ocrEngine.Language = OcrLanguage.English;

        // Step 3: Recognize the image and obtain the result as a PDF/A‑2b document
        using (PdfDocument pdfADocument = ocrEngine.RecognizeToPdfA(scannedImage, PdfAStandard.PdfA2b))
        {
            // Step 4: Save the searchable PDF/A file
            string outputPath = @"C:\Docs\output.pdf";
            pdfADocument.Save(outputPath);
        }

        // Step 5: Inform the user that the file has been created
        Console.WriteLine("PDF/A‑2b file created at C:\\Docs\\output.pdf");
    }
}
```

Εκτελέστε αυτό το πρόγραμμα, υποδείξτε το `input.tif` σε οποιαδήποτε σαρωμένη σελίδα, και θα λάβετε ένα **searchable PDF** έτοιμο για αρχειοθέτηση ή ευρετηρίαση.

## Συμπέρασμα

Μόλις καλύψαμε πώς να **create searchable PDF** αρχεία σε C# χρησιμοποιώντας Aspose OCR και Aspose PDF. Η διαδικασία περιορίζεται στη φόρτωση μιας εικόνας, την εκτέλεση OCR και την εξαγωγή σε PDF/A‑2b—αρκετά απλή για ένα γρήγορο script, αρκετά ισχυρή για παραγωγικές αλυσίδες. Τώρα ξέρετε πώς να **convert scanned image PDF**, να δημιουργήσετε ένα αρχείο **PDF/A** σύμφωνο με τα πρότυπα, και αργότερα να **extract text PDF** για μηχανές αναζήτησης ή αναλύσεις.

Τι θα ακολουθήσει; Δοκιμάστε να επεξεργαστείτε δεκάδες TIFF, πειραματιστείτε με διαφορετικές γλώσσες OCR, ή ενσωματώστε το αποτέλεσμα σε σύστημα διαχείρισης εγγράφων. Μπορείτε επίσης να εξερευνήσετε την προσθήκη υδατογραφιών, ψηφιακών υπογραφών ή τη συμπίεση του τελικού PDF για αποδοτικότητα αποθήκευσης.

Μη διστάσετε να αφήσετε ένα σχόλιο αν αντιμετωπίσετε πρόβλημα, ή να μοιραστείτε πώς επεκτείνετε αυτό το παράδειγμα στα δικά σας έργα. Καλό κώδικα, και απολαύστε τη μετατροπή αυτών των στατικών σαρώσεων σε αναζητήσιμα, μελλοντικά ασφαλή PDFs!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}