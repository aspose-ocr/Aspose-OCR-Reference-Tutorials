---
category: general
date: 2026-05-25
description: αναγνωρίστε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR σε C#. Μάθετε
  πώς να φορτώνετε εικόνα για OCR, να ορίζετε τη γλώσσα OCR, να δημιουργείτε μηχανή
  OCR και να εξάγετε κείμενο από TIFF.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- set OCR language
- create OCR engine
language: el
og_description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#. Αυτό
  το σεμινάριο δείχνει πώς να δημιουργήσετε μηχανή OCR, να φορτώσετε εικόνα για OCR,
  να ορίσετε τη γλώσσα OCR και να εξάγετε κείμενο από TIFF.
og_title: Αναγνώριση κειμένου από εικόνα με Aspose OCR – Πλήρης Οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: recognize text from image using Aspose OCR in C#. Learn how to load
    image for OCR, set OCR language, create OCR engine and extract text from TIFF.
  headline: recognize text from image with Aspose OCR – Complete C# Guide
  type: TechArticle
- questions:
  - answer: Remove the `GpuDevice` line; the engine will automatically switch to CPU
      mode. Performance will be slower but the results remain accurate.
    question: What if my GPU isn’t detected?
  - answer: Absolutely—`Image.FromFile` works with any format supported by System.Drawing,
      so you can **load image for OCR** regardless of extension.
    question: Can I process PNG or JPEG files?
  - answer: Increase `ocrEngine.PreprocessOptions.Dpi` before calling `Recognize`.
      Higher DPI gives the engine more pixels to work with, improving accuracy.
    question: How do I handle low‑resolution scans?
  - answer: The `GpuMemoryLimit` property caps GPU usage. If you hit the limit, the
      engine will fallback to CPU for the remaining pages.
    question: Is there a limit to the size of the TIFF?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- GPU
- Text Extraction
title: Αναγνώριση κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/recognize-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα με Aspose OCR – Πλήρης Οδηγός C#

Ποτέ χρειάστηκε να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήσασταν σίγουροι ποια βιβλιοθήκη θα σας προσφέρει ταχύτητα και ακρίβεια; Δεν είστε μόνοι. Σε πολλά έργα επεξεργασίας τιμολογίων ή αρχειοθέτησης, το μεγαλύτερο πρόβλημα είναι η εξαγωγή καθαρού, αναζητήσιμου κειμένου από αρχεία TIFF χωρίς να γράψετε έναν προσαρμοσμένο parser.

Το ζήτημα είναι το εξής: το Aspose OCR για .NET κάνει όλη αυτή τη διαδικασία παιχνιδάκι. Σε αυτόν τον οδηγό θα περάσουμε από όλα όσα χρειάζεστε — εγκατάσταση του πακέτου, **δημιουργία μηχανής OCR**, φόρτωση ενός TIFF, ορισμός της γλώσσας OCR, και τέλος **εξαγωγή κειμένου από TIFF**. Στο τέλος θα έχετε μια έτοιμη εφαρμογή console που μπορεί να **αναγνωρίσει κείμενο από εικόνα** σε ελάχιστο χρόνο.

## Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί και με .NET Core και .NET Framework)
- Visual Studio 2022 (ή οποιοδήποτε IDE προτιμάτε)
- Πακέτο NuGet Aspose.OCR (η υποστήριξη GPU απαιτεί το πρόσθετο `Aspose.OCR.Gpu`)
- Μια GPU με υποστήριξη CUDA αν θέλετε την επιπλέον ταχύτητα (προαιρετικό αλλά συνιστάται)

> **Συμβουλή:** Αν δεν έχετε GPU, απλώς παραλείψτε τη γραμμή `GpuDevice` και η μηχανή θα επιστρέψει αυτόματα στη CPU.

## Βήμα 1: Εγκατάσταση Aspose OCR και Δημιουργία Μηχανής OCR

Πρώτα, προσθέστε τα απαραίτητα πακέτα μέσω NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu   # optional GPU support
```

Τώρα μπορούμε να **δημιουργήσουμε μηχανή OCR**. Αυτό το αντικείμενο είναι η καρδιά της διαδικασίας· κρατά τις ρυθμίσεις όπως η συσκευή εκτέλεσης και τα όρια μνήμης.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU support
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine (GPU‑enabled)
        var ocrEngine = new OcrEngine
        {
            // 0 = first GPU in the system; change if you have multiple cards
            GpuDevice = new GpuDevice(0),
            // Optional: cap GPU memory usage to 1024 MB
            GpuMemoryLimit = 1024
        };
```

**Γιατί είναι σημαντικό:** Συνδέοντας τη μηχανή με μια GPU μειώνετε δραστικά το χρόνο που χρειάζεται για **αναγνώριση κειμένου από εικόνα**, ειδικά για μεγάλες παρτίδες υψηλής ανάλυσης TIFF.

## Βήμα 2: Φόρτωση Εικόνας για OCR

Στη συνέχεια, πρέπει να **φορτώσετε εικόνα για OCR**. Το Aspose.OCR λειτουργεί με `System.Drawing.Image`, οπότε οποιαδήποτε μορφή υποστηρίζεται από το GDI+ (συμπεριλαμβανομένου του multi‑page TIFF) είναι αποδεκτή.

```csharp
        // Step 2: Load the image you want to process
        // Replace the path with the location of your TIFF file
        var imagePath = @"C:\Invoices\invoice_batch.tif";
        Image image = Image.FromFile(imagePath);
```

Αν εργάζεστε με multi‑page TIFF, μπορείτε να κάνετε βρόχο στις σελίδες χρησιμοποιώντας `image.SelectActiveFrame`, αλλά για τις περισσότερες περιπτώσεις μια ενιαία κλήση αρκεί.

## Βήμα 3: Ορισμός Γλώσσας OCR

Η μηχανή δεν ξέρει μαγικά ποια γλώσσα σκανάρετε. **Ορίστε τη γλώσσα OCR** πριν τρέξετε τον αναγνώστη· διαφορετικά θα λάβετε ακατάστατο αποτέλεσμα.

```csharp
        // Step 3: Tell the engine which language to expect
        ocrEngine.Language = OcrLanguage.English; // change to .German, .French, etc. as needed
```

> **Το ήξερες;** Η αλλαγή γλώσσας κατά την εκτέλεση είναι φθηνή· μπορείτε ακόμη να επεξεργαστείτε ένα έγγραφο με μεικτές γλώσσες αλλάζοντας αυτήν την ιδιότητα μεταξύ των σελίδων.

## Βήμα 4: Εκτέλεση Αναγνώρισης – Αναγνώριση Κειμένου από Εικόνα

Τώρα το διασκεδαστικό μέρος: πραγματικά **αναγνωρίστε κείμενο από εικόνα**. Η μέθοδος `Recognize` επιστρέφει μια απλή συμβολοσειρά με όλους τους ανιχνευμένους χαρακτήρες.

```csharp
        // Step 4: Run OCR and capture the output
        string recognizedText = ocrEngine.Recognize(image);
```

Αν χρειάζεστε βαθμολογίες εμπιστοσύνης ή περιοριστικά πλαίσια, μπορείτε να χρησιμοποιήσετε την υπερφόρτωση που επιστρέφει ένα αντικείμενο `OcrResult`, αλλά για τις περισσότερες εργασίες εξαγωγής η απλή συμβολοσειρά είναι επαρκής.

## Βήμα 5: Εξαγωγή Κειμένου από TIFF (και διαχείριση multi‑page αρχείων)

Όταν η πηγή είναι ένα TIFF που περιέχει πολλές σελίδες, θα θέλετε να επαναλάβετε τα βήματα 2‑4 για κάθε καρέ. Ακολουθεί ένας γρήγορος βρόχος που **εξάγει κείμενο από TIFF** σελίδα προς σελίδα:

```csharp
        // Optional: process multi‑page TIFFs
        var totalFrames = image.GetFrameCount(FrameDimension.Page);
        for (int i = 0; i < totalFrames; i++)
        {
            image.SelectActiveFrame(FrameDimension.Page, i);
            string pageText = ocrEngine.Recognize(image);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
```

Ο παραπάνω κώδικας εκτυπώνει το εξαγόμενο κείμενο για κάθε σελίδα, καθιστώντας εύκολο το άμεσο πέρασμα των αποτελεσμάτων σε βάση δεδομένων ή ευρετήριο αναζήτησης.

## Βήμα 6: Εμφάνιση ή Αποθήκευση του Εξαγόμενου Κειμένου

Τέλος, ας **εμφανίσουμε το εξαγόμενο κείμενο** και προαιρετικά να το γράψουμε σε αρχείο για μεταγενέστερη επεξεργασία.

```csharp
        // Step 6: Output the result to console
        Console.WriteLine("=== Full OCR Result ===");
        Console.WriteLine(recognizedText);

        // Optional: Save to a .txt file
        System.IO.File.WriteAllText(@"C:\Invoices\extracted_text.txt", recognizedText);
    }
}
```

Η εκτέλεση του προγράμματος θα πρέπει να εμφανίσει τους αναγνωρισμένους χαρακτήρες και να δημιουργήσει το `extracted_text.txt` δίπλα στο πηγαίο TIFF.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

- **Τι γίνεται αν η GPU μου δεν εντοπιστεί;**  
  Αφαιρέστε τη γραμμή `GpuDevice`; η μηχανή θα μεταβεί αυτόματα σε λειτουργία CPU. Η απόδοση θα είναι πιο αργή, αλλά τα αποτελέσματα παραμένουν ακριβή.

- **Μπορώ να επεξεργαστώ αρχεία PNG ή JPEG;**  
  Απόλυτα—`Image.FromFile` λειτουργεί με οποιαδήποτε μορφή υποστηρίζεται από το System.Drawing, οπότε μπορείτε να **φορτώσετε εικόνα για OCR** ανεξαρτήτως επέκτασης.

- **Πώς να αντιμετωπίσω σαρώσεις χαμηλής ανάλυσης;**  
  Αυξήστε το `ocrEngine.PreprocessOptions.Dpi` πριν καλέσετε το `Recognize`. Υψηλότερο DPI δίνει στη μηχανή περισσότερα pixel για εργασία, βελτιώνοντας την ακρίβεια.

- **Υπάρχει όριο στο μέγεθος του TIFF;**  
  Η ιδιότητα `GpuMemoryLimit` περιορίζει τη χρήση GPU. Αν φτάσετε το όριο, η μηχανή θα μεταβεί σε CPU για τις υπόλοιπες σελίδες.

---

## Συμπέρασμα

Τώρα έχετε ένα πλήρες, έτοιμο για παραγωγή απόσπασμα κώδικα που **αναγνωρίζει κείμενο από εικόνα** χρησιμοποιώντας το Aspose OCR σε C#. Ο οδηγός κάλυψε πώς να **δημιουργήσετε μηχανή OCR**, **φορτώσετε εικόνα για OCR**, **ορίσετε γλώσσα OCR**, και **εξάγετε κείμενο από TIFF**—όλα ενώ αξιοποιείτε την επιτάχυνση GPU για ταχύτητα.

Από εδώ μπορείτε:

- Να πειραματιστείτε με διαφορετικές γλώσσες (`OcrLanguage.Spanish`, `OcrLanguage.ChineseSimplified`, κ.λπ.).
- Να ενσωματώσετε το αποτέλεσμα σε ένα αναζητήσιμο ευρετήριο ElasticSearch.
- Να προσθέσετε μεταεπεξεργασία (ορθογραφικό έλεγχο, καθαρισμό με regex) για βελτίωση της ποιότητας των δεδομένων.

Δοκιμάστε το σε δική σας παρτίδα τιμολογίων, ρυθμίστε τα όρια μνήμης, και παρακολουθήστε την απόδοση του OCR να απογειώνεται. Καλό προγραμματισμό!

## Σχετικά Tutorials

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}