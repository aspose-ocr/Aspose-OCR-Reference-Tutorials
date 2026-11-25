---
category: general
date: 2026-07-05
description: Εκτελέστε OCR σε εικόνα χρησιμοποιώντας το Aspose.OCR σε C#. Μάθετε πώς
  να φορτώνετε την εικόνα για OCR, να προεπεξεργάζεστε την εικόνα πριν το OCR και
  να εξάγετε κείμενο από απόδειξη ενώ βελτιώνετε την ακρίβεια του OCR.
draft: false
keywords:
- perform OCR on image
- extract text from receipt
- improve OCR accuracy
- load image for OCR
- preprocess image before OCR
language: el
og_description: Εκτελέστε OCR σε εικόνα σε C# χρησιμοποιώντας το Aspose.OCR. Αυτό
  το σεμινάριο δείχνει πώς να φορτώσετε εικόνα για OCR, να προεπεξεργαστείτε την εικόνα
  πριν το OCR και να εξάγετε κείμενο από απόδειξη με βελτιωμένη ακρίβεια OCR.
og_title: Εκτελέστε OCR σε εικόνα με το Aspose – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Perform OCR on image using Aspose.OCR in C#. Learn how to load image
    for OCR, preprocess image before OCR, and extract text from receipt while improving
    OCR accuracy.
  headline: Perform OCR on Image with Aspose – Complete C# Guide
  type: TechArticle
- description: Perform OCR on image using Aspose.OCR in C#. Learn how to load image
    for OCR, preprocess image before OCR, and extract text from receipt while improving
    OCR accuracy.
  name: Perform OCR on Image with Aspose – Complete C# Guide
  steps:
  - name: '**Load** the picture file into memory.'
    text: '**Load** the picture file into memory.'
  - name: '**Preprocess** it: deskew, denoise, and boost contrast.'
    text: '**Preprocess** it: deskew, denoise, and boost contrast.'
  - name: '**Run** the OCR engine.'
    text: '**Run** the OCR engine.'
  - name: '**Read** the resulting text.'
    text: '**Read** the resulting text.'
  type: HowTo
- questions:
  - answer: Aspose.OCR works best with printed text. For cursive or mixed fonts you
      may need a specialized handwriting model or a different library.
    question: What if the receipt is handwritten?
  - answer: Yes—convert each PDF page to an image (`Aspose.PDF` can help) and feed
      those images into the same pipeline.
    question: Can I process PDFs directly?
  - answer: Wrap the core logic inside a `foreach` loop that iterates over a folder
      of images. Remember to dispose of the `OcrEngine` after each file to free memory.
    question: Is there a way to batch‑process many receipts?
  - answer: Aspose offers a free evaluation with a watermark. For production use,
      purchase a license to remove the watermark and unlock full performance.
    question: Do I need a license?
  type: FAQPage
tags:
- Aspose.OCR
- C#
- Image Processing
title: Εκτέλεση OCR σε εικόνα με το Aspose – Πλήρης οδηγός C#
url: /el/net/ocr-optimization/perform-ocr-on-image-with-aspose-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε Εικόνα με το Aspose – Πλήρης Οδηγός C#

Έχετε ποτέ χρειαστεί να **εκτελέσετε OCR σε εικόνα** αρχεία, αλλά τα αποτελέσματα ήταν θολά, έλειπαν χαρακτήρες ή ήταν εντελώς λανθασμένα; Δεν είστε μόνοι—η σάρωση αποδείξεων, τιμολογίων ή χειρόγραφων σημειώσεων συχνά μετατρέπεται σε παιχνίδι εικασίας. Σε αυτόν τον οδηγό θα σας δείξουμε έναν πρακτικό τρόπο να **φορτώσετε εικόνα για OCR**, να την καθαρίσετε και τελικά να **εξάγετε κείμενο από απόδειξη** με εμφανή **βελτίωση της ακρίβειας του OCR**.

Το θέμα είναι: η βιβλιοθήκη Aspose.OCR σας παρέχει ένα καθαρό API που σας επιτρέπει να στοίβαζετε φίλτρα προεπεξεργασίας ακριβώς όπως τα χρειάζεστε. Στο τέλος αυτού του οδηγού θα έχετε μια έτοιμη‑για‑εκτέλεση εφαρμογή C# console που διαβάζει μια λοξή απόδειξη, την ευθυγραμμίζει, αφαιρεί το θόρυβο του φόντου, ενισχύει την αντίθεση και εκτυπώνει το καθαρό κείμενο στην κονσόλα. Καμία μυστήριο, μόνο βήμα‑βήμα κώδικας που μπορείτε να αντιγράψετε‑και‑επικολλήσετε.

## Τι Θα Μάθετε

- Πώς να **φορτώσετε εικόνα για OCR** χρησιμοποιώντας το `ImageStream` του Aspose.
- Ποια φίλτρα **προεπεξεργασίας εικόνας πριν το OCR** είναι πιο αποτελεσματικά για αποδείξεις.
- Τεχνικές για **βελτίωση της ακρίβειας του OCR** χωρίς να αγοράσετε ακριβά τρίτα προϊόντα.
- Οι ακριβείς εντολές για **εξαγωγή κειμένου από απόδειξη** και επαλήθευση του αποτελέσματος.
- Ένα πλήρες, εκτελέσιμο παράδειγμα που μπορείτε να ενσωματώσετε στο Visual Studio αμέσως.

### Προαπαιτούμενα

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core).
- Ένα έγκυρο πακέτο NuGet Aspose.OCR (`Aspose.OCR` 23.9 ή νεότερο).
- Μια δείγμα εικόνας απόδειξης (π.χ. `skewed_receipt.jpg`) τοποθετημένη σε φάκελο που μπορείτε να αναφέρετε.
- Βασική εξοικείωση με εφαρμογές κονσόλας C#.

Αν έχετε όλα αυτά, ας βουτήξουμε—χωρίς περιττές πληροφορίες, μόνο το ουσιώδες.

## Εκτέλεση OCR σε Εικόνα – Επισκόπηση Βήμα‑προς‑Βήμα

Πριν αρχίσουμε να γράφουμε κώδικα, φανταστείτε τη ροή εργασίας:

1. **Load** το αρχείο εικόνας στη μνήμη.  
2. **Preprocess** το: ευθυγράμμιση, αφαίρεση θορύβου και ενίσχυση αντίθεσης.  
3. **Run** τη μηχανή OCR.  
4. **Read** το παραγόμενο κείμενο.

Κάθε ένα από αυτά τα στάδια είναι ένα μικρό κομμάτι του παζλ, και μαζί **εκτελούν OCR σε εικόνα** αρχεία που διαφορετικά θα ήταν ακατανόητα. Οι παρακάτω ενότητες εξηγούν κάθε κομμάτι.

## Φόρτωση Εικόνας για OCR

Το πρώτο πράγμα που χρειάζεται οποιοδήποτε workflow OCR είναι ένα bitmap για επεξεργασία. Το Aspose αφαιρεί τη διαχείριση αρχείων πίσω από το `ImageStream`, πράγμα που σημαίνει ότι δεν χρειάζεται να ασχοληθείτε με το `System.Drawing` εκτός αν το θέλετε.

```csharp
using Aspose.OCR;
using System;

// Step 1: Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Step 2: Load the image you want to recognize
// Replace the path with the actual location of your receipt image
ocrEngine.Image = ImageStream.FromFile(@"C:\OCRDemo\skewed_receipt.jpg");

// Quick sanity check – make sure the image was loaded
if (ocrEngine.Image == null)
{
    Console.WriteLine("Failed to load image. Verify the file path.");
    return;
}
```

> **Why this matters:** Η σωστή φόρτωση της εικόνας είναι η βάση. Αν η διαδρομή είναι λανθασμένη, κάθε επόμενο φίλτρο θα λειτουργεί σιωπηλά πάνω σε μια κενή αναφορά, και θα λάβετε ένα κενό αποτέλεσμα. Ο έλεγχος παραπάνω σας προστατεύει από αυτό το πρόβλημα.

## Προεπεξεργασία Εικόνας Πριν το OCR

Οι φωτογραφίες αποδείξεων είναι γνωστές για τρία προβλήματα: περιστροφή, τυχαίους σπόρους και χαμηλή αντίθεση. Το Aspose διαθέτει τρία ενσωματωμένα φίλτρα που αντιμετωπίζουν άμεσα αυτά τα ζητήματα. Η σειρά είναι σημαντική—πρώτα ευθυγράμμιση, μετά αφαίρεση θορύβου και τέλος ενίσχυση αντίθεσης.

```csharp
// Step 3: Add preprocessing filters in the desired order
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Deskew);          // Corrects image rotation
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Denoise);        // Reduces noise
ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.ContrastBoost); // Enhances contrast
```

> **Pro tip:** Αν επεξεργάζεστε μια δέσμη αποδείξεων που όλες έχουν σαρωθεί στα 300 dpi, μπορείτε να παραλείψετε το `ContrastBoost` επειδή ο σαρωτής παρέχει ήδη αρκετή αντίθεση. Η πειραματική δοκιμή είναι το κλειδί για **βελτίωση της ακρίβειας του OCR** για το συγκεκριμένο σύνολο δεδομένων σας.

## Βελτίωση της Ακρίβειας του OCR με Φίλτρα

Τώρα που η εικόνα έχει προεπεξεργαστεί, η μηχανή OCR μπορεί να κάνει τη μαγεία της. Η κλήση `Recognize()` εκτελεί τον αναγνωριστή βασισμένο σε νευρωνικό δίκτυο πάνω στο καθαρισμένο bitmap.

```csharp
// Step 4: Perform OCR recognition
ocrEngine.Recognize();
```

Πίσω από τη σκηνή, το Aspose εφαρμόζει μοντέλα ειδικά για γλώσσες, διαχωρισμό χαρακτήρων και μετα-επεξεργασία. Παρέχοντας του μια ευθυγραμμισμένη, χωρίς θόρυβο, υψηλής αντίθεσης εικόνα, του δίνετε ουσιαστικά μια σελίδα βιβλίου σχολής—γι' αυτό και η **βελτίωση της ακρίβειας του OCR** που επιδιώκετε.

## Εξαγωγή Κειμένου από Απόδειξη

Τέλος, εξάγετε το αναγνωρισμένο κείμενο από τη μηχανή. Η ιδιότητα `Text` περιέχει το ακατέργαστο αποτέλεσμα Unicode, το οποίο μπορείτε να γράψετε στην κονσόλα, σε αρχείο ή σε βάση δεδομένων.

```csharp
// Step 5: Output the recognized text
Console.WriteLine("=== Recognized Receipt Text ===");
Console.WriteLine(ocrEngine.Text);
```

Τυπική έξοδος από απόδειξη μοιάζει με αυτό:

```
=== Recognized Receipt Text ===
Store: QuickMart
Date: 2024-06-15
Item 1  $2.99
Item 2  $5.49
Total   $8.48
Thank you!
```

Αν παρατηρήσετε ελλείποντες αριθμούς ή ακατάστατους χαρακτήρες, επιστρέψτε στο βήμα προεπεξεργασίας—ίσως η εικόνα χρειάζεται πιο ισχυρό επίπεδο `Denoise` ή ένα προσαρμοσμένο φίλτρο. Το καλό νέο είναι ότι μπορείτε να στοίβαξετε πολλαπλές εμφανίσεις του ίδιου φίλτρου αν χρειαστεί.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα έτοιμο για αντιγραφή‑και‑επικόλληση. Αποθηκεύστε το ως `Program.cs`, επαναφέρετε το πακέτο NuGet και τρέξτε το. Η κονσόλα θα εμφανίσει το εξαγόμενο κείμενο της απόδειξης.

```csharp
using Aspose.OCR;
using System;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create the OCR engine
            // -------------------------------------------------
            OcrEngine ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // 2️⃣  Load the image you want to process
            // -------------------------------------------------
            // Change the path to point at your own receipt file
            string imagePath = @"C:\OCRDemo\skewed_receipt.jpg";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            if (ocrEngine.Image == null)
            {
                Console.WriteLine($"Unable to load image from '{imagePath}'. Check the path and try again.");
                return;
            }

            // -------------------------------------------------
            // 3️⃣  Preprocess the image – this is where we
            //     actually **improve OCR accuracy**
            // -------------------------------------------------
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Deskew);
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.Denoise);
            ocrEngine.PreprocessFilters.Add(OcrPreprocessFilter.ContrastBoost);

            // -------------------------------------------------
            // 4️⃣  Run the OCR engine – **perform OCR on image**
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // 5️⃣  Extract and display the text – **extract text from receipt**
            // -------------------------------------------------
            Console.WriteLine("\n=== Recognized Receipt Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Αναμενόμενη Έξοδος

Η εκτέλεση του προγράμματος σε μια καθαρή, ευθυγραμμισμένη απόδειξη θα πρέπει να εκτυπώσει κάτι παρόμοιο με το απόσπασμα που εμφανίστηκε νωρίτερα. Αν λάβετε μια κενή συμβολοσειρά, ελέγξτε ξανά τη σειρά των φίλτρων προεπεξεργασίας ή δοκιμάστε να αυξήσετε το DPI της πηγαίας εικόνας.

## Συχνές Ερωτήσεις & Προβλήματα

- **What if the receipt is handwritten?**  
  Το Aspose.OCR λειτουργεί καλύτερα με τυπωμένο κείμενο. Για πλάγια ή μικτά γραμματοσειρά, ίσως χρειαστεί ένα εξειδικευμένο μοντέλο χειρόγραφης ή μια διαφορετική βιβλιοθήκη.

- **Can I process PDFs directly?**  
  Ναι—μετατρέψτε κάθε σελίδα PDF σε εικόνα (`Aspose.PDF` μπορεί να βοηθήσει) και τροφοδοτήστε αυτές τις εικόνες στην ίδια ροή εργασίας.

- **Is there a way to batch‑process many receipts?**  
  Τυλίξτε τη βασική λογική μέσα σε έναν βρόχο `foreach` που διατρέχει έναν φάκελο εικόνων. Θυμηθείτε να απελευθερώσετε το `OcrEngine` μετά από κάθε αρχείο για να ελευθερώσετε μνήμη.

- **Do I need a license?**  
  Το Aspose προσφέρει δωρεάν αξιολόγηση με υδατογράφημα. Για παραγωγική χρήση, αγοράστε άδεια ώστε να αφαιρεθεί το υδατογράφημα και να ξεκλειδωθεί η πλήρης απόδοση.

## Συμπέρασμα

Μόλις περάσαμε από το πώς να **εκτελέσετε OCR σε εικόνα** αρχεία χρησιμοποιώντας το Aspose.OCR, από το **φόρτωση εικόνας για OCR** μέχρι το **προεπεξεργασία εικόνας πριν το OCR**, και τέλος το **εξαγωγή κειμένου από απόδειξη**. Με τη σωστή σειρά των φίλτρων ευθυγράμμισης, αφαίρεσης θορύβου και ενίσχυσης αντίθεσης, συνήθως παρατηρείται μια εμφανής **βελτίωση της ακρίβειας του OCR**—ιδιαίτερα σε σαρώσεις χαμηλής ποιότητας.

Τι ακολουθεί; Δοκιμάστε να προσθέσετε μια υπόδειξη γλώσσας (`ocrEngine.Language = Language.English;`) ή πειραματιστείτε με προσαρμοσμένα φίλτρα για αντιστροφή χρώματος. Μπορείτε επίσης να διοχετεύσετε το εξαγόμενο κείμενο σε έναν απλό parser που θα εξάγει αυτόματα τα στοιχεία γραμμής και τα σύνολα.

Αν αυτός ο οδηγός σας βοήθησε να ξεπεράσετε τα συνήθη εμπόδια του OCR, δώστε του ένα αστέρι στο GitHub ή αφήστε ένα σχόλιο παρακάτω. Καλή προγραμματιστική δουλειά, και εύχομαι οι αποδείξεις σας να είναι πάντα αναγνώσιμες! 

![Διάγραμμα που δείχνει τη διαδικασία προεπεξεργασίας OCR που βοηθά στην εκτέλεση OCR σε εικόνα] 

---

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική;

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσει να κατακτήσετε πρόσθετες δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}