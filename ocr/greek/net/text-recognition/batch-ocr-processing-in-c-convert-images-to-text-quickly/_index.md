---
category: general
date: 2026-06-25
description: Το σεμινάριο επεξεργασίας παρτίδας OCR δείχνει πώς να μετατρέψετε εικόνες
  σε κείμενο και να εξάγετε κείμενο από εικόνες χρησιμοποιώντας το Aspose.OCR σε C#.
  Μάθετε την υλοποίηση βήμα‑προς‑βήμα.
draft: false
keywords:
- batch ocr processing
- convert images to text
- how to extract text from images
language: el
og_description: Η επεξεργασία OCR κατά παρτίδες σε C# σας επιτρέπει να μετατρέπετε
  γρήγορα εικόνες σε κείμενο. Ακολουθήστε αυτόν τον οδηγό για να μάθετε πώς να εξάγετε
  κείμενο από εικόνες με το Aspose.OCR.
og_title: Ομαδική Επεξεργασία OCR σε C# – Μετατροπή Εικόνων σε Κείμενο
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  headline: Batch OCR Processing in C# – Convert Images to Text Quickly
  type: TechArticle
- description: Batch OCR processing tutorial shows how to convert images to text and
    extract text from images using Aspose.OCR in C#. Learn step‑by‑step implementation.
  name: Batch OCR Processing in C# – Convert Images to Text Quickly
  steps:
  - name: Expected Output
    text: 'When you run `dotnet run`, you’ll see something like:'
  - name: What image formats are supported?
    text: Aspose.OCR handles JPEG, PNG, TIFF, BMP, and GIF out of the box. If you
      encounter a format like WebP, convert it first or use a third‑party decoder.
  - name: Can I limit the OCR language to English only?
    text: 'Yes. Set the `Language` property on the `BatchRecognizer` before calling
      `Recognize`:'
  - name: How do I process thousands of files without blowing up memory?
    text: Break the list into smaller batches (e.g., 500 files each) and run the above
      routine in a loop. This keeps the in‑memory dictionary manageable and lets you
      log progress per batch.
  - name: What if I need the OCR results in a database instead of files?
    text: 'Replace the `File.WriteAllText` call with your preferred data‑access code.
      For example, using Dapper:'
  type: HowTo
tags:
- OCR
- Aspose
- C#
title: Ομαδική επεξεργασία OCR σε C# – Γρήγορη μετατροπή εικόνων σε κείμενο
url: /el/net/text-recognition/batch-ocr-processing-in-c-convert-images-to-text-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Επεξεργασία OCR σε Παρτίδες σε C# – Γρήγορη Μετατροπή Εικόνων σε Κείμενο

Έχετε αναρωτηθεί ποτέ πώς να **batch OCR processing** ολόκληρο φάκελο σκαναρίσματος χωρίς να γράψετε ξεχωριστό βρόχο για κάθε αρχείο; Δεν είστε ο μόνος. Σε πολλά έργα—σκεφτείτε αυτοματοποίηση τιμολογίων, αρχειοθέτηση παλαιών εγγράφων ή ακόμη και ένα απλό προσωπικό εργαλείο φωτογραφία‑σε‑κείμενο—χρειάζεται να **convert images to text** μαζικά.  

Τα καλά νέα; Με το Aspose.OCR μπορείτε να το κάνετε ακριβώς αυτό με λίγες γραμμές. Αυτός ο οδηγός σας καθοδηγεί μέσα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει **how to extract text from images** χρησιμοποιώντας batch OCR processing, εξηγεί γιατί κάθε μέρος είναι σημαντικό και σας δίνει συμβουλές για την αποφυγή κοινών παγίδων.

## Τι Θα Μάθετε

- Ρυθμίστε το Aspose.OCR για λειτουργίες σε παρτίδες.
- Διαμορφώστε το parallelism για να επιταχύνετε μεγάλες εργασίες.
- Γράψτε τα αποτελέσματα OCR σε ξεχωριστά αρχεία `.txt` αυτόματα.
- Διαχειριστείτε τα γεγονότα προόδου ώστε να γνωρίζετε πάντα τι συμβαίνει.
- Επεκτείνετε τον κώδικα για προσαρμοσμένη διαχείριση σφαλμάτων ή διαφορετικές μορφές εξόδου.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· απλώς βασικές γνώσεις C# και .NET 6 (ή νεότερη) εγκατεστημένη.

---

## Βήμα 1: Προετοιμάστε το Έργο σας για Επεξεργασία OCR σε Παρτίδες

Πριν βουτήξουμε στον κώδικα, βεβαιωθείτε ότι έχετε το πακέτο NuGet Aspose.OCR. Ανοίξτε ένα τερματικό στον φάκελο του έργου σας και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

> **Pro tip:** Χρησιμοποιήστε την πιο πρόσφατη σταθερή έκδοση (από τον Ιούνιο 2026 είναι η 23.9) για βελτιώσεις απόδοσης και την πιο πρόσφατη υποστήριξη γλωσσών.

Δημιουργήστε μια νέα εφαρμογή κονσόλας αν δεν έχετε ήδη μία:

```bash
dotnet new console -n BatchOcrApp
cd BatchOcrApp
```

Τώρα είστε έτοιμοι να γράψετε την πραγματική λογική επεξεργασίας OCR σε παρτίδες.

## Βήμα 2: Ορίστε τα Αρχεία Εικόνας που Θέλετε να Μετατρέψετε

Το πρώτο κομμάτι του **batch OCR processing** είναι απλώς να πείτε στον αναγνωριστή ποια αρχεία πρέπει να επεξεργαστεί. Μπορείτε να κωδικοποιήσετε μια λίστα, να διαβάσετε από έναν κατάλογο ή ακόμη και να αντλήσετε διαδρομές από μια βάση δεδομένων. Για σαφήνεια, θα χρησιμοποιήσουμε μια στατική λίστα:

```csharp
// Step 2: List of image files to be processed
var imageFiles = new List<string>
{
    @"C:\Images\invoice1.jpg",
    @"C:\Images\receipt2.png",
    @"C:\Images\scan3.tif"
};
```

> **Why this matters:** Με τη μεταφορά μιας συλλογής, το `BatchRecognizer` μπορεί εσωτερικά να προγραμματίσει εργασία σε πολλαπλά νήματα, που είναι ο πυρήνας των γρήγορων λειτουργιών **convert images to text**.

## Βήμα 3: Δημιουργήστε και Διαμορφώστε το BatchRecognizer

Τώρα έρχεται η καρδιά του οδηγού. Η κλάση `BatchRecognizer` αφαιρεί τις λεπτομέρειες του threading για εσάς. Μπορείτε να ρυθμίσετε την ιδιότητα `Parallelism` ώστε να ταιριάζει με τον αριθμό πυρήνων του CPU σας ή μια προσαρμοσμένη τιμή αν θέλετε να αφήσετε κάποιους πυρήνες ελεύθερους για άλλη εργασία.

```csharp
// Step 3: Initialise the BatchRecognizer with optional settings
var ocrBatch = new BatchRecognizer
{
    // Number of concurrent threads (default = Environment.ProcessorCount)
    Parallelism = 4,

    // Optional: Hook into progress events for real‑time feedback
    ProgressChanged = (s, e) =>
        Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
};
```

> **Explanation:** Ορίζοντας `Parallelism = 4` λέει στη βιβλιοθήκη να εκτελεί τέσσερις εργασίες OCR ταυτόχρονα. Σε ένα τυπικό quad‑core laptop αυτό προσφέρει μια ωραία αύξηση ταχύτητας χωρίς να κορεσθεί το σύστημα. Αν τρέχετε σε διακομιστή με πολλούς πυρήνες, αυξήστε αυτόν τον αριθμό.

> **Edge case:** Αν επεξεργάζεστε εξαιρετικά μεγάλες εικόνες, μπορεί να φτάσετε τα όρια μνήμης. Σε αυτή την περίπτωση, μειώστε το parallelism ή επεξεργαστείτε τα αρχεία σε μικρότερα τμήματα.

## Βήμα 4: Εκτελέστε το OCR και Συλλέξτε τα Αποτελέσματα

Καλώντας `Recognize` στο `BatchRecognizer` επιστρέφει ένα λεξικό όπου το κλειδί είναι η αρχική διαδρομή αρχείου και η τιμή είναι ένα `OcrResult` που περιέχει το εξαγόμενο κείμενο, βαθμολογίες εμπιστοσύνης και άλλα.

```csharp
// Step 4: Execute batch OCR – returns a map of file → OcrResult
IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);
```

> **What you get:** Για κάθε εικόνα, το `OcrResult.Text` περιέχει την αναπαράσταση plain‑text. Αυτό είναι ακριβώς ό,τι χρειάζεστε όταν θέλετε **how to extract text from images** με προγραμματιστικό τρόπο.

## Βήμα 5: Αποθηκεύστε Κάθε Αποτέλεσμα σε Αρχείο .txt

Οι περισσότερες πραγματικές περιπτώσεις απαιτούν την αποθήκευση του αποτελέσματος OCR για μεταγενέστερη επεξεργασία—ίσως να το τροφοδοτήσετε σε ευρετήριο αναζήτησης ή να το συσχετίσετε με μια εγγραφή βάσης δεδομένων. Ο παρακάτω βρόχος γράφει ένα αρχείο `.txt` δίπλα σε κάθε πηγαία εικόνα, διατηρώντας το αρχικό όνομα αρχείου.

```csharp
// Step 5: Write each OCR result to a corresponding .txt file
foreach (var entry in ocrResults)
{
    string txtPath = Path.ChangeExtension(entry.Key, ".txt");
    File.WriteAllText(txtPath, entry.Value.Text);
    Console.WriteLine($"Saved OCR text to {txtPath}");
}
```

> **Tip:** Αν χρειάζεστε διαφορετική μορφή (JSON, CSV, κ.λπ.), απλώς σειριοποιήστε το `entry.Value` όπως θέλετε. Το αντικείμενο `OcrResult` εκθέτει επίσης `Confidence` και `PageCount` αν αυτά τα μετρικά είναι χρήσιμα για εσάς.

## Βήμα 6: Σήμα Ολοκλήρωσης και Χειρισμός Σφαλμάτων με Ευγένεια

Μια καθαρή λήξη κάνει το εργαλείο σας να φαίνεται πιο επαγγελματικό. Ο δείγματος κώδικας ήδη εκτυπώνει μια τελική γραμμή, αλλά ας προσθέσουμε ένα μπλοκ try‑catch για να εμφανίζονται τυχόν απρόσμενες εξαιρέσεις, όπως ελλιπή αρχεία ή μη υποστηριζόμενες μορφές εικόνας.

```csharp
try
{
    // (All steps 2‑5 go here)
    Console.WriteLine("Batch OCR processing finished successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
}
```

> **Why wrap it:** Όταν τρέχετε το πρόγραμμα σε μεγάλο φάκελο, μια μόνο κατεστραμμένη εικόνα θα μπορούσε να διακόψει ολόκληρη τη δουλειά. Με σωστό χειρισμό σφαλμάτων μπορείτε να καταγράψετε το πρόβλημα και να συνεχίσετε με τα υπόλοιπα αρχεία.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε στο `Program.cs`. Βεβαιωθείτε ότι οι διαδρομές εικόνας δείχνουν σε πραγματικά αρχεία στον υπολογιστή σας.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchExample
{
    static void Main()
    {
        try
        {
            // Step 2: Define the image files to be processed
            var imageFiles = new List<string>
            {
                @"C:\Images\invoice1.jpg",
                @"C:\Images\receipt2.png",
                @"C:\Images\scan3.tif"
            };

            // Step 3: Create a BatchRecognizer and configure optional settings
            var ocrBatch = new BatchRecognizer
            {
                // Set the degree of parallelism (default = Environment.ProcessorCount)
                Parallelism = 4,

                // Hook into progress events to monitor processing
                ProgressChanged = (s, e) =>
                    Console.WriteLine($"Processed {e.Completed}/{e.Total} – {e.CurrentFile}")
            };

            // Step 4: Run OCR on the batch of images (returns file → OcrResult)
            IDictionary<string, OcrResult> ocrResults = ocrBatch.Recognize(imageFiles);

            // Step 5: Write each OCR result to a corresponding .txt file
            foreach (var entry in ocrResults)
            {
                string txtPath = Path.ChangeExtension(entry.Key, ".txt");
                File.WriteAllText(txtPath, entry.Value.Text);
                Console.WriteLine($"Saved OCR text to {txtPath}");
            }

            // Step 6: Indicate that batch processing has completed
            Console.WriteLine("Batch OCR processing finished successfully.");
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error during batch OCR processing: {ex.Message}");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν τρέξετε `dotnet run`, θα δείτε κάτι όπως:

```
Processed 1/3 – C:\Images\invoice1.jpg
Saved OCR text to C:\Images\invoice1.txt
Processed 2/3 – C:\Images\receipt2.png
Saved OCR text to C:\Images\receipt2.txt
Processed 3/3 – C:\Images\scan3.tif
Saved OCR text to C:\Images\scan3.txt
Batch OCR processing finished successfully.
```

Κάθε αρχείο `.txt` τώρα περιέχει την plain‑text έκδοση της αντίστοιχης εικόνας—ακριβώς ό,τι χρειάζεστε για **convert images to text** σε κλίμακα.

---

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Ποιες μορφές εικόνας υποστηρίζονται;

Το Aspose.OCR διαχειρίζεται JPEG, PNG, TIFF, BMP και GIF έτοιμα. Αν συναντήσετε μορφή όπως WebP, μετατρέψτε την πρώτα ή χρησιμοποιήστε έναν αποκωδικοποιητή τρίτου.

### Μπορώ να περιορίσω τη γλώσσα OCR μόνο στα Αγγλικά;

Ναι. Ορίστε την ιδιότητα `Language` στο `BatchRecognizer` πριν καλέσετε `Recognize`:

```csharp
ocrBatch.Language = "en";
```

Ο περιορισμός της γλώσσας μπορεί να βελτιώσει την ακρίβεια και την ταχύτητα, ειδικά όταν ενδιαφέρεστε μόνο για **how to extract text from images** σε μία γλώσσα.

### Πώς να επεξεργαστώ χιλιάδες αρχεία χωρίς να εξαντλήσω τη μνήμη;

Διαιρέστε τη λίστα σε μικρότερες παρτίδες (π.χ., 500 αρχεία η κάθε μία) και τρέξτε τη παραπάνω ρουτίνα σε βρόχο. Αυτό κρατά το λεξικό στη μνήμη διαχειρίσιμο και σας επιτρέπει να καταγράφετε την πρόοδο ανά παρτίδα.

### Τι αν χρειάζομαι τα αποτελέσματα OCR σε βάση δεδομένων αντί για αρχεία;

Αντικαταστήστε την κλήση `File.WriteAllText` με τον κώδικα πρόσβασης δεδομένων που προτιμάτε. Για παράδειγμα, χρησιμοποιώντας Dapper:

```csharp
connection.Execute(
    "INSERT INTO OcrResults (FilePath, Text) VALUES (@Path, @Text)",
    new { Path = entry.Key, Text = entry.Value.Text });
```

## Συμπέρασμα

Μόλις κυριαρχήσατε στο **batch OCR processing** σε C# με το Aspose.OCR, μάθατε έναν καθαρό τρόπο για **convert images to text**, και ανακαλύψατε αρκετές πρακτικές συμβουλές για **how to extract text from images** αποδοτικά. Η πλήρης ροή εργασίας—συλλογή διαδρομών αρχείων, διαμόρφωση `BatchRecognizer`, εκτέλεση OCR και αποθήκευση αποτελεσμάτων—ενσωματώνεται σε ένα ενιαίο, εύκολο‑να‑διαβαστεί πρόγραμμα.

Τι ακολουθεί; Δοκιμάστε να αυξήσετε το `Parallelism` σε διακομιστή πολλαπλών πυρήνων, πειραματιστείτε με πακέτα γλωσσών ή προσθέστε μετα‑επεξεργασία όπως ορθογραφικό έλεγχο. Μπορείτε επίσης να εξερευνήσετε την τροφοδοσία του εξαγόμενου κειμένου στο Azure Cognitive Search ώστε τα σαρωμένα έγγραφά σας να γίνονται αναζητήσιμα σε δευτερόλεπτα.

Έχετε μια παραλλαγή που θέλετε να μοιραστείτε—ίσως OCR σε PDF ή διαχείριση πολυσελιδικών TIFF; Αφήστε ένα σχόλιο παρακάτω και ας συνεχίσουμε τη συζήτηση. Καλό κώδικα!

## Τι Θα Πρέπει Να Μάθετε Στη Σύντομη Μελλοντική

Τα παρακάτω tutorials καλύπτουν στενά σχετιζόμενα θέματα που βασίζονται στις τεχνικές που παρουσιάζονται σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε σε πρόσθετα χαρακτηριστικά API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [Εξαγωγή Κειμένου από Εικόνες Χρησιμοποιώντας Λειτουργία OCR σε Φακέλους](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Πώς να Εκτελέσετε OCR σε Εικόνες σε Παρτίδες με Λίστα στο Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Πώς να Εξάγετε Κείμενο από Αρχεία ZIP Χρησιμοποιώντας Aspose.OCR για .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}