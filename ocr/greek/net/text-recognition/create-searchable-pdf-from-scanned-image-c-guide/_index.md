---
category: general
date: 2026-04-26
description: Δημιουργήστε PDF με δυνατότητα αναζήτησης από σαρωμένη εικόνα χρησιμοποιώντας
  το Aspose OCR σε C#. Μάθετε πώς να μετατρέψετε τη σαρωμένη εικόνα, να εξάγετε κείμενο
  και να δημιουργήσετε γρήγορα ένα PDF με δυνατότητα αναζήτησης.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: el
og_description: Δημιουργήστε αναζητήσιμο PDF από σαρωμένη εικόνα χρησιμοποιώντας το
  Aspose OCR. Βήμα‑βήμα κώδικας C# για μετατροπή, εξαγωγή κειμένου και δημιουργία
  αναζητήσιμου PDF.
og_title: Δημιουργία Αναζητήσιμου PDF από Σαρωμένη Εικόνα – Οδηγός C#
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Δημιουργία Αναζητήσιμου PDF από Σαρωμένη Εικόνα – Οδηγός C#
url: /el/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Δημιουργία Αναζητήσιμου PDF από Σαρωμένη Εικόνα – Οδηγός C#

Έχετε χρειαστεί ποτέ να **δημιουργήσετε αναζητήσιμα PDF** από συμβόλαια χαρτιού, αποδείξεις ή παλιά αρχεία; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το εμπόδιο όταν ένας πελάτης παραδίδει μια στοίβα σάρωσης TIFF και αναμένει ένα αναζητήσιμο PDF ως τελικό προϊόν.  

Σε αυτό το tutorial θα σας δείξουμε ακριβώς **πώς να κάνετε OCR σε ένα έγγραφο** και να μετατρέψετε μια σαρωμένη εικόνα σε **αναζητήσιμο PDF** με το Aspose OCR για .NET. Στο τέλος θα μπορείτε να **μετατρέψετε αρχεία σαρωμένων εικόνων**, **να εξάγετε κείμενο από εικόνα** και ακόμη να διαχειριστείτε πολυ-σελίδες TIFF χωρίς καμία δυσκολία.

## Τι Θα Χρειαστείτε

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο (το API λειτουργεί με .NET Core, .NET Framework και .NET 5+).  
* Ένα έγκυρο άδεια Aspose OCR ή να είστε εντάξει με το υδατογράφημα αξιολόγησης.  
* Το πακέτο NuGet `Aspose.OCR` εγκατεστημένο (`dotnet add package Aspose.OCR`).  
* Ένα δείγμα αρχείου TIFF (π.χ., `contract_scan.tif`) που θέλετε να μετατρέψετε σε αναζητήσιμο PDF.

Αυτό είναι όλο—χωρίς επιπλέον βιβλιοθήκες, χωρίς περίπλοκες ρυθμίσεις. Έτοιμοι; Ας ξεκινήσουμε.

![Δημιουργία παραδείγματος αναζητήσιμου PDF](create-searchable-pdf.png "παράδειγμα δημιουργίας αναζητήσιμου pdf")

## Βήμα 1 – Αρχικοποίηση του OCR Engine (Δημιουργία Αναζητήσιμου PDF)

Το πρώτο βήμα: χρειάζεστε μια παρουσία `OcrEngine`. Αυτό το αντικείμενο είναι ο «εργάτης» που διαβάζει το bitmap, αναγνωρίζει χαρακτήρες και σας επιστρέφει το κείμενο.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Γιατί να ορίσετε τη γλώσσα;**  
Αν το αφήσετε στην προεπιλογή, το Aspose θα δοκιμάσει όλα τα πακέτα γλωσσών, κάτι που επιβραδύνει τη διαδικασία. Ορίζοντας `Language.Latin` λέτε στην μηχανή να εστιάσει στο λατινικό αλφάβητο, προσφέροντας ταχύτερη εκτέλεση και πιο ακριβή αποτελέσματα για συμβόλαια στα αγγλικά.

## Βήμα 2 – Φόρτωση της Σαρωμένης Εικόνας (Μετατροπή Σαρωμένης Εικόνας)

Τώρα τροφοδοτούμε τη μηχανή με την εικόνα που θέλουμε να επεξεργαστούμε. Το Aspose μπορεί να διαβάσει διαδρομή αρχείου, ροή ή ακόμη και `byte[]`. Για απλότητα θα χρησιμοποιήσουμε `ImageStream.FromFile`.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Αν κάποια στιγμή χρειαστείτε **μετατροπή TIFF σε PDF**, θυμηθείτε ότι οι πολυ-σελίδες TIFF διαχειρίζονται αυτόματα—κάθε καρέ γίνεται ξεχωριστή σελίδα PDF.

## Βήμα 3 – Εκτέλεση OCR και Λήψη του Κειμένου (Εξαγωγή Κειμένου από Εικόνα)

Η εκτέλεση OCR είναι τόσο απλή όσο η κλήση του `Recognize`. Η μηχανή θα επιστρέψει ένα `RecognitionResult` που περιέχει το ακατέργαστο κείμενο, βαθμολογίες εμπιστοσύνης και πληροφορίες διάταξης.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Συμβουλή επαγγελματία:** Αν χρειάζεστε μόνο το κείμενο (χωρίς PDF), μπορείτε να σταματήσετε εδώ και να γράψετε το `extractedText` σε αρχείο `.txt`. Αλλά συνήθως ο στόχος μας είναι ένα αναζητήσιμο PDF, οπότε συνεχίζουμε.

## Βήμα 4 – Αποθήκευση ως Αναζητήσιμο PDF (Δημιουργία Αναζητήσιμου PDF)

Το Aspose κάνει το τελευταίο βήμα τεράστιο: απλώς καλέστε `Save` με `SaveFormat.PdfSearchable`. Στο παρασκήνιο η βιβλιοθήκη ενσωματώνει το εξαγόμενο κείμενο ως αόρατο στρώμα διατηρώντας την αρχική εμφάνιση της εικόνας.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

Όταν ανοίξετε το `contract_searchable.pdf` σε οποιονδήποτε προβολέα PDF, θα μπορείτε να επιλέξετε, να αντιγράψετε και να αναζητήσετε το κείμενο—ακριβώς αυτό που περιμένει ένας πελάτης από ένα “αναζητήσιμο PDF”.

## Διαχείριση Πολυ‑Σελίδων TIFF (Μετατροπή TIFF σε PDF)

Αν το πηγαίο αρχείο περιέχει πολλές σελίδες, το Aspose θα θεωρήσει κάθε καρέ ως ξεχωριστή σελίδα αυτόματα. Δεν απαιτούνται επιπλέον βρόχοι. Ωστόσο, μπορεί να θέλετε να ελέγξετε το DPI ή την ποιότητα εικόνας για κάθε σελίδα:

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Αφού ορίσετε αυτές τις επιλογές, επαναλάβετε το **Βήμα 2** για κάθε καρέ, ή απλώς δείξτε το `ImageStream.FromFile` στο πολυ‑σελίδες TIFF και αφήστε το Aspose να κάνει τη δουλειά.

## Συνηθισμένα Προβλήματα και Πώς να τα Διορθώσετε

| Συμπτωμα | Πιθανή Αιτία | Διόρθωση |
|----------|--------------|----------|
| Το κείμενο είναι ακατάλληλο ή λείπει | Λάθος γλώσσα ορίστηκε | Ορίστε `ocrEngine.Language` στο σωστό πακέτο γλώσσας (π.χ., `Language.German`). |
| Το PDF είναι τεράστιο (10 MB για μία σελίδα) | Η προεπιλεγμένη συμπίεση εικόνας είναι χαμηλή | Ρυθμίστε `ocrEngine.ImageProcessingOptions.Compression` σε `Jpeg` και ορίστε μια λογική τιμή `Quality` (0‑100). |
| Το OCR εκτελείται πολύ αργά | Χρήση της προεπιλογής `Auto` για εντοπισμό γλώσσας | Ορίστε ρητά τη γλώσσα που περιμένετε. |
| Δεν εμφανίζεται το αναζητήσιμο στρώμα | Αποθηκεύτηκε με `SaveFormat.Pdf` αντί για `PdfSearchable` | Χρησιμοποιήστε `PdfSearchable`. |

## Πλήρες Παράδειγμα Από‑Αρχή‑Προς‑Τέλος

Συνδυάζοντας τα παραπάνω, εδώ είναι μια έτοιμη για εκτέλεση εφαρμογή κονσόλας που μπορείτε να αντιγράψετε‑επικολλήσετε στο Visual Studio:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Τι θα δείτε:**  
* Ένα παράθυρο κονσόλας που εκτυπώνει ένα απόσπασμα του κειμένου που εξήχθη.  
* Ένα αρχείο `contract_searchable.pdf` δίπλα στο αρχικό TIFF. Ανοίξτε το, πατήστε **Ctrl + F**, και αναζητήστε οποιαδήποτε λέξη εμφανίστηκε στην αρχική σάρωση—voilà, λειτουργεί.

## Επόμενα Βήματα & Σχετικά Θέματα

* **Πώς να κάνετε OCR σε παρτίδες εγγράφων** – τυλίξτε τον κώδικα παραπάνω σε βρόχο `foreach` και επεξεργαστείτε ολόκληρο φάκελο.  
* **Μετατροπή σαρωμένων εικόνων** σε μορφές εκτός TIFF (PNG, JPEG) – η ίδια API λειτουργεί· απλώς αλλάξτε την επέκταση αρχείου.  
* **Εξαγωγή κειμένου από εικόνα** για περαιτέρω ανάλυση – περάστε το `result.Text` σε pipeline επεξεργασίας φυσικής γλώσσας.  
* **Βελτιστοποίηση μεγέθους PDF** – εξερευνήστε το `PdfSaveOptions` για περαιτέρω συμπίεση εικόνων ή ενσωμάτωση γραμματοσειρών μόνο όταν χρειάζεται.  

Πειραματιστείτε με αυτές τις ιδέες και σύντομα θα γίνετε ο άνθρωπος-αναφοράς για κάθε αίτημα “μετατρέψτε αυτή τη σάρωση σε αναζητήσιμο PDF”.

---

### TL;DR

Τώρα ξέρετε πώς να **δημιουργήσετε αναζητήσιμα PDF** από σαρωμένες εικόνες χρησιμοποιώντας το Aspose OCR σε C#. Η διαδικασία είναι: αρχικοποίηση της μηχανής, φόρτωση της εικόνας, εκτέλεση OCR και αποθήκευση με `PdfSearchable`. Ρυθμίστε τις γλώσσες, DPI και συμπίεση για ειδικές περιπτώσεις, και είστε έτοιμοι να **μετατρέψετε σαρωμένη εικόνα**, **εξάγετε κείμενο από εικόνα**, και ακόμη **μετατρέψετε TIFF σε PDF** σε κλίμακα. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}