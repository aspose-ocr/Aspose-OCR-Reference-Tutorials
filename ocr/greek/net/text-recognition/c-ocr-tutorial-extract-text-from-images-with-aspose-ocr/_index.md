---
category: general
date: 2026-03-21
description: 'c# OCR tutorial: Μάθετε πώς να εξάγετε κείμενο από εικόνα, να σαρώσετε
  τιμολόγια και να φορτώσετε εικόνα σε c# χρησιμοποιώντας το Aspose OCR με επιτάχυνση
  GPU.'
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- ocr invoice scanning
- how to ocr image
- load image in c#
language: el
og_description: 'c# OCR tutorial: Βήμα‑βήμα οδηγός για εξαγωγή κειμένου από εικόνα,
  εκτέλεση σάρωσης τιμολογίων με OCR και μάθετε πώς να κάνετε OCR εικόνας σε C# χρησιμοποιώντας
  επιτάχυνση GPU.'
og_title: c# OCR tutorial – Εξαγωγή κειμένου από εικόνες με Aspose OCR
tags:
- OCR
- C#
- Image Processing
title: c# OCR οδηγός – Εξαγωγή κειμένου από εικόνες με το Aspose OCR
url: /el/net/text-recognition/c-ocr-tutorial-extract-text-from-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR tutorial – Εξαγωγή Κειμένου από Εικόνες με Aspose OCR

Έχετε αναρωτηθεί ποτέ πώς να **c# OCR tutorial** αντιμετωπίσετε ένα πραγματικό πρόβλημα, όπως η μετατροπή μιας σαρωμένης τιμής σε επεξεργάσιμο κείμενο; Δεν είστε μόνοι. Πολλοί προγραμματιστές συναντούν εμπόδια όταν χρειάζεται να *extract text from image* αρχεία και καταλήγουν να γράφουν εύθραυστους αναλυτές που σπάνε στην πρώτη θορυβώδη σάρωση.

Το θέμα είναι—η Aspose.OCR κάνει όλη τη διαδικασία παιχνιδάκι, ειδικά όταν ενεργοποιήσετε την επιτάχυνση GPU. Σε αυτόν τον οδηγό θα δείτε ακριβώς **how to ocr image** αρχεία σε C#, πώς να φορτώσετε εικόνα σε c# σωστά, και ακόμη να αντιμετωπίσετε κοινά προβλήματα σάρωσης τιμολογίων χωρίς να τρελαίνεστε.

Στο τέλος αυτού του tutorial θα έχετε μια εκτελέσιμη εφαρμογή console που διαβάζει μια τιμολόγηση TIFF, εκτελεί OCR στο GPU και εκτυπώνει καθαρό κείμενο plain‑text. Χωρίς μαγεία, μόνο σταθερός κώδικας που μπορείτε να αντιγράψετε‑επικολλήσετε και να προσαρμόσετε.

---

## Τι Θα Χρειαστείτε

- **.NET 6.0** (ή νεότερο) – η τρέχουσα έκδοση LTS, ώστε να είστε έτοιμοι για το μέλλον.
- **Aspose.OCR for .NET** πακέτο NuGet – έκδοση 23.10 (η πιο πρόσφατη τη στιγμή της συγγραφής).
- Ένα **GPU‑enabled machine** (προαιρετικό αλλά συνιστάται) – ο κώδικας επιστρέφει σε CPU αν δεν βρεθεί συμβατό GPU.
- Ένα παράδειγμα εικόνας, π.χ., `large_invoice.tif`. Οποιαδήποτε υποστηριζόμενη μορφή (PNG, JPEG, TIFF, PDF) λειτουργεί.

Αν δεν έχετε εγκαταστήσει ακόμη το πακέτο NuGet, εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Τώρα που καλύψαμε τις προαπαιτήσεις, ας βουτήξουμε στα πραγματικά βήματα.

---

## Βήμα 1: Δημιουργήστε ένα Νέο Project Console και Προσθέστε το Aspose.OCR

Πρώτα, δημιουργήστε μια νέα εφαρμογή console ώστε να διατηρήσουμε το tutorial αυτόνομο.

```bash
dotnet new console -n OcrInvoiceDemo
cd OcrInvoiceDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Χρησιμοποιήστε τη σημαία `-n` για να δώσετε στο project σας ένα σημασιολογικό όνομα· κρατάει τη λύση οργανωμένη όταν αρχίσετε να προσθέτετε περισσότερα modules αργότερα.

Το αρχείο `Program.cs` που δημιουργεί το Visual Studio θα είναι το πεδίο παιχνιδιού μας. Ανοίξτε το και διαγράψτε τη προεπιλεγμένη γραμμή `Console.WriteLine` – θα την αντικαταστήσουμε με τη λογική OCR.

## Βήμα 2: Φορτώστε Εικόνα σε C# – Ο Σωστός Τρόπος

Η φόρτωση μιας εικόνας μπορεί να φαίνεται απλή, αλλά αν γίνει λανθασμένα μπορεί να προκαλέσει διαρροές μνήμης ή κλείδωμα του αρχείου. Η κλάση `System.Drawing.Image` λειτουργεί καλά για τις περισσότερες περιπτώσεις, όμως πρέπει να τη τυλίξετε σε ένα μπλοκ `using` για να εξασφαλίσετε την απελευθέρωση.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 👉 Step 2: Load the image you want to OCR.
            // Replace the path with the actual location of your invoice file.
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // The using statement ensures the image gets disposed automatically.
            using var inputImage = Image.FromFile(imagePath);
            
            // Continue to the OCR engine setup…
        }
    }
}
```

Παρατηρήστε το σχόλιο `// 👉 Step 2:` – αντικατοπτρίζει την αρίθμηση βημάτων στο tutorial μας και βοηθά όποιον διαβάζει τον κώδικα αργότερα.

## Βήμα 3: Αρχικοποιήστε τη Μηχανή OCR με Επιτάχυνση GPU

Η Aspose.OCR σας επιτρέπει να επιλέξετε τη λειτουργία επεξεργασίας κατά τη δημιουργία. Το `OcrEngineMode.Gpu` λέει στη βιβλιοθήκη να χρησιμοποιεί την κάρτα γραφικών αν την εντοπίσει· διαφορετικά επιστρέφει σιωπηλά σε CPU, ώστε να μην χρειάζεται να γράψετε επιπλέον λογική εναλλακτικού.

```csharp
// 👉 Step 3: Create the OCR engine.
// The constructor argument selects GPU mode; it's the fastest option for large invoices.
var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);
```

> **Why GPU?**  
> Το OCR σε τιμολόγια υψηλής ανάλυσης μπορεί να είναι απαιτητικό για το CPU. Η εκχώρηση στο GPU μειώνει το χρόνο εκτέλεσης από αρκετά δευτερόλεπτα σε κλάσμα, ειδικά όταν επεξεργάζεστε παρτίδες.

## Βήμα 4: Εκτελέστε OCR και Εξάγετε Κείμενο από την Εικόνα

Τώρα συμβαίνει η μαγεία. Καλέστε το `Recognize` και πάρτε το plain text. Η Aspose επιστρέφει ένα αντικείμενο `OcrResult` που περιέχει το ακατέργαστο κείμενο, τις βαθμολογίες εμπιστοσύνης, και ακόμη τα πλαίσια περιγράμματος ανά χαρακτήρα αν τα χρειαστείτε αργότερα.

```csharp
// 👉 Step 4: Perform the OCR operation.
OcrResult ocrResult = ocrEngine.Recognize(inputImage);

// Display the extracted text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Όταν εκτελέσετε το πρόγραμμα, θα πρέπει να δείτε κάτι όπως:

```
=== OCR Output ===
Invoice #12345
Date: 03/15/2026
Total: $1,234.56
...
```

Αν η έξοδος φαίνεται ακατάληπτη, ελέγξτε ξανά ότι η εικόνα έχει υψηλή αντίθεση και ότι η γλώσσα OCR είναι ρυθμισμένη σωστά (η προεπιλογή είναι Αγγλικά). Μπορείτε επίσης να ρυθμίσετε το `ocrEngine.Settings` για καλύτερη ακρίβεια, αλλά οι προεπιλογές λειτουργούν καλά για τα περισσότερα τυπωμένα τιμολόγια.

## Βήμα 5: Διαχείριση Ακραίων Περιστατικών Σάρωσης OCR Τιμολογίων

Τα τιμολόγια έρχονται σε πολλές μορφές—κάποια είναι multi‑page, άλλα έχουν πίνακες ή χειρόγραφες σημειώσεις. Εδώ είναι μερικές γρήγορες προσαρμογές που μπορείτε να κάνετε χωρίς να ξαναγράψετε ολόκληρη τη ροή.

### 5.1 Multi‑Page PDFs ή TIFFs

Αν το αρχείο προέλευσης περιέχει πολλαπλές σελίδες, θα πρέπει να κάνετε βρόχο σε κάθε σελίδα και να ενωθεί τα αποτελέσματα.

```csharp
using var multiPageImage = Image.FromFile(@"C:\Invoices\multi_page_invoice.tif");

// Aspose can split multi‑page TIFFs into separate images.
for (int i = 0; i < multiPageImage.GetFrameCount(FrameDimension.Page); i++)
{
    multiPageImage.SelectActiveFrame(FrameDimension.Page, i);
    using var page = (Image)multiPageImage.Clone();
    var pageResult = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

### 5.2 Low‑Resolution Scans

Αν το DPI είναι κάτω από 150, αυξήστε την ανάλυση της εικόνας πριν τη στείλετε στη μηχανή. Αυτό βελτιώνει δραματικά την αναγνώριση χαρακτήρων.

```csharp
// Simple nearest‑neighbor scaling – replace with a better algorithm if needed.
var highRes = new Bitmap(inputImage, new Size(inputImage.Width * 2, inputImage.Height * 2));
var highResResult = ocrEngine.Recognize(highRes);
Console.WriteLine(highResResult.Text);
```

### 5.3 Custom Language Packs

Από προεπιλογή η Aspose χρησιμοποιεί Αγγλικά. Για άλλες γλώσσες, κατεβάστε το κατάλληλο language pack από τον ιστότοπο της Aspose και καταχωρίστε το:

```csharp
ocrEngine.Settings.Language = OcrLanguage.Spanish; // example for Spanish invoices
```

Αυτές οι ρυθμίσεις κάνουν τη λύση **ocr invoice scanning** σας αρκετά ανθεκτική για παραγωγικές εργασίες.

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω βρίσκεται το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενσωματώνει όλα τα παραπάνω βήματα. Αντιγράψτε το στο `Program.cs`, προσαρμόστε τη διαδρομή του αρχείου και πατήστε **F5**.

```csharp
// ---------------------------------------------------------------
// Complete c# OCR tutorial – Aspose OCR with GPU acceleration
// ---------------------------------------------------------------
using System;
using System.Drawing;
using System.Drawing.Imaging;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace OcrInvoiceDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // Step 1: Initialize the OCR engine (GPU mode)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine(OcrEngineMode.Gpu);

            // -----------------------------------------------------------------
            // Step 2: Load the image you want to process
            // -----------------------------------------------------------------
            const string imagePath = @"C:\Invoices\large_invoice.tif";

            // Using ensures the image is disposed properly.
            using var inputImage = Image.FromFile(imagePath);

            // -----------------------------------------------------------------
            // Step 3: Run OCR and extract plain text
            // -----------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(inputImage);

            // -----------------------------------------------------------------
            // Step 4: Output the result
            // -----------------------------------------------------------------
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);

            // -----------------------------------------------------------------
            // Optional: Demonstrate handling a multi‑page TIFF (comment out if not needed)
            // -----------------------------------------------------------------
            // HandleMultiPageTiff(@"C:\Invoices\multi_page_invoice.tif", ocrEngine);
        }

        // ---------------------------------------------------------------
        // Helper for multi‑page TIFFs – shows how to iterate pages
        // ---------------------------------------------------------------
        static void HandleMultiPageTiff(string path, OcrEngine engine)
        {
            using var multiPage = Image.FromFile(path);
            int pageCount = multiPage.GetFrameCount(FrameDimension.Page);

            for (int i = 0; i < pageCount; i++)
            {
                multiPage.SelectActiveFrame(FrameDimension.Page, i);
                using var page = (Image)multiPage.Clone();
                var result = engine.Recognize(page);
                Console.WriteLine($"\n--- Page {i + 1} ---");
                Console.WriteLine(result.Text);
            }
        }
    }
}
```

**Αναμενόμενη έξοδος** (truncated for brevity):

```
=== OCR Output ===
Invoice #98765
Date: 02/28/2026
Bill To: Acme Corp.
Subtotal: $2,500.00
Tax (8%): $200.00
Total: $2,700.00
...
```

Εκτελέστε το πρόγραμμα και βεβαιωθείτε ότι η κονσόλα εκτυπώνει το κείμενο που βλέπετε στο τιμολόγιο. Αν παίρνετε κενές συμβολοσειρές, ελέγξτε ξανά ότι η διαδρομή της εικόνας είναι σωστή και ότι το αρχείο δεν είναι κατεστραμμένο.

---

## Συχνές Ερωτήσεις (FAQ)

**Q: Λειτουργεί αυτό σε Linux;**  
A: Ναι. Η Aspose.OCR είναι cross‑platform. Απλώς εγκαταστήστε το .NET runtime για Linux και το ίδιο πακέτο NuGet λειτουργεί. Η επιτάχυνση GPU απαιτεί GPU συμβατό με CUDA και τον κατάλληλο οδηγό.

**Q: Τι γίνεται αν δεν έχω GPU;**  
A: Ο κατασκευαστής `OcrEngineMode.Gpu` επιστρέφει αυτόματα σε CPU όταν δεν εντοπιστεί συμβατό GPU. Θα λάβετε ακόμη ακριβή αποτελέσματα· θα πάρει μόνο λίγο περισσότερο χρόνο.

**Q: Μπορώ να κάνω OCR σε χειρόγραφες σημειώσεις;**  
A: Τα προεπιλεγμένα μοντέλα της Aspose εστιάζουν σε τυπωμένο κείμενο. Για χειρόγραφους θα χρειαστείτε εξειδικευμένο μοντέλο ή διαφορετική υπηρεσία (π.χ., Azure Form Recognizer). Ωστόσο, μπορείτε ακόμα να δοκιμάσετε τον ίδιο κώδικα—απλώς περιμένετε χαμηλότερες βαθμολογίες εμπιστοσύνης.

---

## Συμπέρασμα

Μόλις ολοκληρώσατε ένα **c# OCR tutorial** που δείχνει πώς να *extract text from image* αρχεία, να εκτελέσετε **ocr invoice scanning**, και να καταλάβετε **how to o

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}