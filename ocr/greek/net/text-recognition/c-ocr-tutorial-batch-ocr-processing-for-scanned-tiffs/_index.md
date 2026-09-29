---
category: general
date: 2026-01-04
description: c# OCR tutorial που δείχνει πώς να μετατρέψετε μια σαρωμένη εικόνα σε
  κείμενο με επεξεργασία OCR σε παρτίδες. Μάθετε να εξάγετε κείμενο από αρχεία tiff
  σε λίγα λεπτά.
draft: false
keywords:
- c# ocr tutorial
- batch ocr processing
- convert scanned image to text
- how to extract text from scanned document
- extract text from tiff
language: el
og_description: Το tutorial C# OCR σας καθοδηγεί στη μετατροπή σαρωμένης εικόνας σε
  κείμενο, καλύπτοντας την επεξεργασία OCR σε παρτίδες και την εξαγωγή κειμένου από
  αρχεία TIFF.
og_title: c# OCR οδηγός – Μαζική επεξεργασία OCR για σαρωμένα TIFFs
tags:
- OCR
- C#
- Image Processing
title: c# OCR οδηγός – Μαζική επεξεργασία OCR για σαρωμένα TIFFs
url: /el/net/text-recognition/c-ocr-tutorial-batch-ocr-processing-for-scanned-tiffs/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR Tutorial – Επεξεργασία παρτίδας OCR για σαρωμένα TIFF

Έχετε αναρωτηθεί ποτέ πώς να **εξάγετε κείμενο από σαρωμένα έγγραφα** χωρίς να πληκτρολογείτε τα πάντα χειροκίνητα; Αυτό είναι ακριβώς αυτό που μπορεί να λύσει ένα **c# OCR tutorial**. Σε αυτόν τον οδηγό θα περάσουμε από τη μετατροπή ενός πολυσελιδικού TIFF σε κείμενο που μπορεί να αναζητηθεί, χρησιμοποιώντας μια ενιαία, καθαρή κλήση—ιδανική για επεξεργασία παρτίδας OCR.

Θα ξεκινήσουμε με το πρόβλημα, θα περάσουμε κατευθείαν στην πλήρη λύση, και θα κλείσουμε με συμβουλές που μπορείτε να εφαρμόσετε σε οποιαδήποτε σαρωμένη εικόνα. Στο τέλος θα ξέρετε **πώς να εξάγετε κείμενο από σαρωμένο έγγραφο**, **πώς να μετατρέψετε σαρωμένη εικόνα σε κείμενο**, και γιατί αυτή η προσέγγιση κλιμακώνεται άψογα για μεγάλες παρτίδες.

## What This Tutorial Covers

- Ρύθμιση της μηχανής OCR σε C#
- Φόρτωση ενός πολυσελιδικού TIFF (το κλασικό σενάριο `extract text from tiff`)
- Εκτέλεση παρτίδας OCR με μία κλήση API
- Επανάληψη στα αποτελέσματα και εκτύπωση του αναγνωρισμένου κειμένου
- Συνηθισμένα προβλήματα και πώς να τα αποφύγετε

Δεν απαιτούνται εξωτερικές βιβλιοθήκες πέρα από το OCR SDK που ήδη διαθέτετε, και ο κώδικας τρέχει σε .NET 6+ αμέσως. Έτοιμοι; Ας μπει το χέρι μας στη δουλειά.

![Diagram of OCR pipeline for batch processing of a multi‑page TIFF](/images/ocr-pipeline.png "c# OCR tutorial diagram")

*Image alt text: c# OCR tutorial diagram showing batch OCR processing of a TIFF file.*

## Prerequisites

- **.NET 6** ή νεότερο (οποιοδήποτε πρόσφατο .NET runtime)
- Βασική εξοικείωση με τη σύνταξη **C#**
- Ένα OCR SDK που εκθέτει `OcrEngine`, `OcrResult`, και `RecognizeAllPages()` (το παράδειγμα χρησιμοποιεί ένα υποθετικό αλλά αντιπροσωπευτικό API)
- Ένα πολυσελιδικό αρχείο TIFF με όνομα `multipage.tif` τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε

Αν κάτι από αυτά σας είναι άγνωστο, κάντε παύση και εγκαταστήστε το .NET SDK ή κατεβάστε τη βιβλιοθήκη OCR από τον ιστότοπο του προμηθευτή. Συνήθως είναι ένα μόνο πακέτο NuGet.

## Step 1 – Initialize the OCR Engine and Load the TIFF

Το πρώτο που χρειαζόμαστε είναι μια παρουσία του OCR engine που μπορεί να κατανοήσει τη μορφή της εικόνας. Η δημιουργία του engine είναι φθηνή· η βαριά δουλειά γίνεται όταν καλούμε το `RecognizeAllPages()` αργότερα.

```csharp
using System;
using System.Collections.Generic;

// Assume the OCR SDK lives in the OcrNamespace
using OcrNamespace;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and point it at our multi‑page TIFF
        OcrEngine ocrEngine = new OcrEngine();

        // LoadImage accepts a path; use an absolute or relative path as needed
        string imagePath = @"YOUR_DIRECTORY/multipage.tif";
        ocrEngine.LoadImage(imagePath);
```

**Why this matters:** Η φόρτωση της εικόνας μία φορά και η διατήρηση του engine ενεργού αποφεύγει επαναλαμβανόμενες ενέργειες I/O στο δίσκο, που είναι το μεγαλύτερο κέρδος απόδοσης όταν κάνετε **batch OCR processing**.

## Step 2 – Run Batch OCR on All Pages

Τώρα έρχεται η μαγική γραμμή που κάνει τη βαριά δουλειά. Αντί να κάνετε βρόχο στις σελίδες μόνοι σας, ζητάμε από το engine να αναγνωρίσει **όλες τις σελίδες** σε μία κλήση. Αυτό είναι η καρδιά του **c# OCR tutorial** και ο πιο γρήγορος τρόπος για **convert scanned image to text** για ένα πολυσελιδικό έγγραφο.

```csharp
        // Step 2: Recognize text from every page with a single call
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeAllPages();

        // At this point ocrResults contains one OcrResult per page
```

**Why this works:** Το SDK εσωτερικά διαβάζει κάθε σελίδα, εφαρμόζει το μοντέλο OCR, και επιστρέφει μια συλλογή αποτελεσμάτων. Με το batching της κλήσης μειώνουμε το κόστος και διατηρούμε τη χρήση μνήμης προβλέψιμη.

## Step 3 – Iterate Over the Results and Display the Text

Αφού το engine ολοκληρώσει, απλώς διασχίζουμε τη λίστα `ocrResults` και τυπώνουμε το κείμενο κάθε σελίδας. Μπορείτε επίσης να γράψετε το αποτέλεσμα σε αρχείο, βάση δεδομένων, ή να το τροφοδοτήσετε σε ευρετήριο αναζήτησης—ό,τι ταιριάζει στη ροή εργασίας σας.

```csharp
        // Step 3: Loop through each result and output the recognized text
        for (int pageIndex = 0; pageIndex < ocrResults.Count; pageIndex++)
        {
            Console.WriteLine($"--- Page {pageIndex + 1} ---");
            Console.WriteLine(ocrResults[pageIndex].Text);
            Console.WriteLine(); // Blank line for readability
        }

        // Clean up resources if the SDK requires it
        ocrEngine.Dispose();
    }
}
```

**Expected output** (truncated for brevity):

```
--- Page 1 ---
This is the first page of the scanned document.
It contains an introduction to the topic.

--- Page 2 ---
The second page continues with more details...
```

Αν δείτε ακατανόητους χαρακτήρες, ελέγξτε ξανά ότι τα πακέτα γλώσσας OCR είναι εγκατεστημένα και ότι το TIFF δεν είναι κατεστραμμένο.

## Pro Tip – Handling Large Batches Efficiently

Όταν χρειάζεται να επεξεργαστείτε δεκάδες ή εκατοντάδες αρχεία TIFF, τυλίξτε τη λογική παραπάνω μέσα σε βρόχο `foreach` πάνω στα μονοπάτια αρχείων. Κρατήστε έναν ενιαίο `OcrEngine` ενεργό για ολόκληρη τη παρτίδα· η επανεκκίνηση του ανά αρχείο προσθέτει περιττή καθυστέρηση.

```csharp
foreach (var file in Directory.GetFiles(@"YOUR_DIRECTORY", "*.tif"))
{
    ocrEngine.LoadImage(file);
    var results = ocrEngine.RecognizeAllPages();
    // Process results...
}
```

**Why this helps:** Ο OCR engine συχνά αποθηκεύει στην κρυφή μνήμη (cache) τα μοντέλα γλώσσας, οπότε η επαναχρήση του μειώνει τόσο τις αιχμές CPU όσο και τη μνήμη.

## Common Pitfalls & How to Avoid Them

| Πρόβλημα | Συμπτωμα | Διόρθωση |
|----------|----------|----------|
| Έλλειψη δεδομένων γλώσσας | Κενό ή μερικώς αναγνωρισμένο κείμενο | Εγκαταστήστε το κατάλληλο language pack για το OCR SDK σας |
| TIFF χαμηλής ανάλυσης (≤150 dpi) | Κακή ακρίβεια, πολλοί χαρακτήρες “?” | Επαναδείγματοληψία της εικόνας στα 300 dpi πριν τη φόρτωση |
| Πολυσελιδικό TIFF με ανάμικτες χρωματικές λειτουργίες | Καταρρεύσεις σε ορισμένες σελίδες | Μετατρέψτε όλες τις σελίδες σε μία χρωματική λειτουργία (π.χ., grayscale) |
| Μεγάλα αρχεία (>100 MB) | Εξαιρέσεις out‑of‑memory | Επεξεργαστείτε τις σελίδες σε streaming mode αν το SDK το υποστηρίζει, ή χωρίστε το TIFF |

Η αντιμετώπιση αυτών νωρίς σας σώζει από προβλήματα εντοπισμού σφαλμάτων αργότερα, ειδικά όταν κάνετε **batch OCR processing** χιλιάδων αρχείων.

## Extending the Example: Saving Results to a Text File

Αν προτιμάτε ένα μόνιμο αντίγραφο αντί για έξοδο στην κονσόλα, αντικαταστήστε το τμήμα `Console.WriteLine` με εγγραφές σε αρχείο:

```csharp
string outputPath = Path.ChangeExtension(imagePath, ".txt");
using (StreamWriter writer = new StreamWriter(outputPath))
{
    for (int i = 0; i < ocrResults.Count; i++)
    {
        writer.WriteLine($"--- Page {i + 1} ---");
        writer.WriteLine(ocrResults[i].Text);
        writer.WriteLine();
    }
}
Console.WriteLine($"OCR results saved to {outputPath}");
```

Τώρα έχετε ένα βολικό `multipage.txt` δίπλα στην αρχική εικόνα—ιδανικό για ευρετηρίαση ή περαιτέρω ανάλυση.

## Recap – What You’ve Learned

- **c# OCR tutorial** που δείχνει βήμα‑βήμα πώς να **convert scanned image to text**
- Πώς να **extract text from tiff** αρχεία με μία κλήση `RecognizeAllPages()`
- Στρατηγικές για αποδοτική **batch OCR processing** σε πολλά έγγραφα
- Πρακτικές συμβουλές για διαχείριση language packs, ανάλυσης, και περιορισμών μνήμης

Αυτά τα δομικά στοιχεία σας επιτρέπουν να αυτοματοποιήσετε την εισαγωγή δεδομένων, να ενεργοποιήσετε πλήρη αναζήτηση κειμένου σε αρχεία, ή να τροφοδοτήσετε παλιά έγγραφα σε σύγχρονες ροές εργασίας.

## What’s Next?

- Εξερευνήστε **πώς να εξάγετε κείμενο από σαρωμένα έγγραφα PDF** μετατρέποντας κάθε σελίδα σε εικόνα πρώτα.
- Δοκιμάστε διαφορετικές μηχανές OCR (π.χ., Tesseract, Azure Cognitive Services) για να συγκρίνετε την ακρίβεια.
- Συνδυάστε το αποτέλεσμα OCR με βιβλιοθήκες NLP για αυτόματη ετικετοθέτηση ή ταξινόμηση του εξαγόμενου περιεχομένου.

Νιώστε ελεύθεροι να πειραματιστείτε—αντικαταστήστε τα δικά σας αρχεία εικόνας, προσαρμόστε τη μορφή εξόδου, ή ενσωματώστε τα αποτελέσματα σε βάση δεδομένων. Ο ουρανός είναι το όριο όταν έχετε κατακτήσει τα βασικά του OCR σε C#.

Καλή προγραμματιστική, και οι σαρώσεις σας να είναι πάντα καθαρές!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}