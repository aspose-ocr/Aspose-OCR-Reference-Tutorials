---
category: general
date: 2026-03-13
description: Πώς να κάνετε μαζική OCR γρήγορα και αξιόπιστα, μαθαίνοντας πώς να εξάγετε
  κείμενο από αρχεία tiff χρησιμοποιώντας το Aspose.OCR. Ακολουθήστε αυτό το βήμα‑βήμα
  οδηγό.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: el
og_description: Μάθετε πώς να εκτελείτε μαζική OCR σε C# και να εξάγετε κείμενο από
  αρχεία tiff με το Aspose.OCR. Αυτός ο οδηγός καλύπτει τη ρύθμιση, τον κώδικα και
  συμβουλές βέλτιστων πρακτικών.
og_title: Πώς να εκτελέσετε μαζική OCR σε C# – Πλήρης Οδηγός Προγραμματισμού
tags:
- OCR
- C#
- Aspose
- Batch processing
title: Πώς να κάνετε ομαδική OCR σε C# – Πλήρης Οδηγός Προγραμματισμού
url: /el/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

blocks/products/products-backtop-button >}}

Make sure we keep them unchanged.

Now produce final content with all translations.

Check for any missed markdown: blockquote > lines, headings, lists.

Make sure bold formatting preserved.

Now output.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να εκτελέσετε OCR σε παρτίδες σε C# – Πλήρης Οδηγός Προγραμματισμού

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR σε παρτίδες** σε ένα βουνό σαρωμένων τιμολογίων χωρίς να γράψετε ξεχωριστό script για κάθε αρχείο; Δεν είστε ο μόνος. Σε πολλά πραγματικά έργα το πρόβλημα δεν είναι η ακρίβεια του OCR, αλλά ο τεράστιος όγκος των εικόνων — συχνά TIFF — που πρέπει να μετατραπούν σε αναζητήσιμο κείμενο.  

Αυτό το tutorial σας δείχνει **πώς να εκτελέσετε OCR σε παρτίδες** χρησιμοποιώντας το `BatchProcessor` του Aspose.OCR, ενώ επίσης σας διδάσκει πώς να **εξάγετε κείμενο από tiff** αρχεία σε μια ενιαία, καθαρή εκτέλεση. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή console που επεξεργάζεται ολόκληρο φάκελο, αξιοποιεί προαιρετική επιτάχυνση GPU και αποθηκεύει τα αποτελέσματα ως απλό κείμενο όπου τα χρειάζεστε.

## Τι Θα Χρειαστεί

- **.NET 6+** (ή .NET Framework 4.7.2 αν προτιμάτε το κλασικό runtime)  
- **Aspose.OCR for .NET** – μπορείτε να αποκτήσετε το πακέτο NuGet με `dotnet add package Aspose.OCR`.  
- Ένας φάκελος με εικόνες **TIFF** που θέλετε να διαβάσετε (το tutorial χρησιμοποιεί το `Invoices` ως παράδειγμα).  
- Προαιρετικά: μια GPU που υποστηρίζει DirectX 11 ή CUDA αν θέλετε να επιταχύνετε τη διαδικασία.  

Καμία επιπλέον υπηρεσία, κανένα κλειδί cloud — μόνο ένα τοπικό έργο C# και η βιβλιοθήκη Aspose.

## Βήμα 1: Ρύθμιση του Έργου και Εγκατάσταση του Aspose.OCR

Πρώτα, δημιουργήστε μια εφαρμογή console.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro tip:** Αν χρησιμοποιείτε Windows και σκοπεύετε να χρησιμοποιήσετε επιτάχυνση GPU, βεβαιωθείτε ότι είναι εγκατεστημένος ο πιο πρόσφατος οδηγός γραφικών. Διαφορετικά η σημαία `UseGpu = true` θα επιστρέψει αυτόματα στην CPU.

## Βήμα 2: Δημιουργία της Διαμόρφωσης του BatchProcessor

Τώρα θα διαμορφώσουμε το `BatchProcessor`. Αυτό είναι η καρδιά του **πώς να εκτελέσετε OCR σε παρτίδες** — λέτε στο Aspose ποια γλώσσα να περιμένει, ποια φίλτρα προεπεξεργασίας να εφαρμόσει και αν θα χρησιμοποιήσει την GPU.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Γιατί αυτές οι ρυθμίσεις;**  
- `Language = Language.English` λέει στη μηχανή να χρησιμοποιήσει το μοντέλο αγγλικής γλώσσας, το οποίο είναι πολύ πιο ακριβές από το γενικό μοντέλο.  
- `UseGpu` μπορεί να μειώσει τον χρόνο επεξεργασίας κατά το ήμισυ σε μια αξιοπρεπή GPU, αλλά είναι ασφαλές να το αφήσετε `false` αν χρησιμοποιείτε laptop χωρίς αυτήν.  
- Η αλυσίδα φίλτρων αντικατοπτρίζει αυτό που θα έκανε ένας άνθρωπος: ευθυγράμμιση της σελίδας και καθαρισμός των στίγματων πριν την τροφοδοσία του OCR engine.

## Βήμα 3: Καθορίστε τον Επεξεργαστή στον Φάκελο TIFF σας

Το επόμενο κομμάτι του **πώς να εκτελέσετε OCR σε παρτίδες** είναι να πείτε στη βιβλιοθήκη πού βρίσκονται τα αρχεία προέλευσης. Υποστηρίζονται wildcards, ώστε να μπορείτε να συλλέξετε κάθε αρχείο `.tif` με μια εντολή.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Edge case:** Αν οι εικόνες σας έχουν μικτές επεκτάσεις (`.tiff`, `.tif`, `.png`), καλέστε το `AddFolder` πολλές φορές ή χρησιμοποιήστε `*.*` και φιλτράρετε αργότερα στον κώδικα.

## Βήμα 4: Επιλέξτε Πού Θα Αποθηκευτούν τα Αποτελέσματα OCR

Μπορεί να αναρωτιέστε, “Πού καταλήγει το εξαγόμενο κείμενο?” Αυτό είναι η τρίτη στήλη του **πώς να εκτελέσετε OCR σε παρτίδες** — ο καθορισμός της τοποθεσίας και της μορφής εξόδου. Θα αποθηκεύσουμε αρχεία plain‑text δίπλα στα αρχικά.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Αν χρειάζεστε JSON ή XML αντί για plain text, απλώς αντικαταστήστε το `OutputFormat.PlainText` με `OutputFormat.Json` ή `OutputFormat.Xml`. Η βιβλιοθήκη διαχειρίζεται τη μετατροπή για εσάς.

## Βήμα 5: Εκτέλεση της Παρτίδας και Αναφορά Αποτελεσμάτων

Τέλος, ξεκινήστε τη δουλειά. Η μέθοδος `Execute` μπλοκάρει μέχρι να επεξεργαστούν όλα τα αρχεία, μετά μπορείτε να ελέγξετε το `ProcessedCount` για να επιβεβαιώσετε την επιτυχία.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

Όταν εκτελέσετε το πρόγραμμα, η κονσόλα θα εμφανίσει κάτι σαν:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

Στον φάκελο `Output` θα βρείτε ένα αρχείο `.txt` για κάθε πηγαίο TIFF, το καθένα ονομασμένο όπως η αρχική εικόνα (π.χ., `Invoice_001.txt`). Ανοίξτε οποιοδήποτε αρχείο και θα δείτε το ακατέργαστο κείμενο OCR — ιδανικό για τροφοδοσία σε ευρετήριο αναζήτησης ή σε downstream pipeline εξαγωγής δεδομένων.

## Διαχείριση Συνηθισμένων Προβλημάτων

### 1. Η GPU Δεν Είναι Διαθέσιμη

Αν `UseGpu = true` αλλά δεν βρεθεί συμβατή συσκευή, το Aspose επιστρέφει σιωπηλά στην CPU. Για να το δηλώσετε ρητά, μπορείτε να πιάσετε το `DeviceNotFoundException`:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Μη‑TIFF Αρχεία στον Ίδιο Φάκελο

Όταν έχετε έναν φάκελο με μικτά αρχεία, φιλτράρετε προγραμματιστικά:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Μεγάλα Αρχεία Που Υπερβαίνουν τη Μνήμη

Για τεράστια multi‑page TIFF, ενεργοποιήστε το streaming:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## Pro Tips για Καλύτερη Ακρίβεια Όταν **εξάγετε κείμενο από tiff**

- **Η ανάλυση μετρά** – Στοχεύστε σε 300 dpi ή περισσότερο. Κάτω από αυτό το OCR engine μπορεί να χάσει χαρακτήρες.  
- **Χρώμα vs. Γκρι κλίμακα** – Μετατρέψτε τις έγχρωμες σαρώσεις σε γκρι κλίμακα πριν το OCR· το `DeskewFilter` το κάνει ήδη, αλλά μπορείτε να προσθέσετε `ColorDepthReductionFilter` για επιπλέον ταχύτητα.  
- **Μετα-επεξεργασία** – Αφού έχετε plain‑text, εκτελέστε ορθογραφικό έλεγχο ή καθαρισμό με regex για να διορθώσετε συνηθισμένα σφάλματα OCR (π.χ., “0” vs “O”).

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι ολόκληρο το πρόγραμμα που μπορείτε να μεταγλωττίσετε και να εκτελέσετε. Απλώς αντικαταστήστε τις διαδρομές placeholder με τις δικές σας.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Μεταγλώττιση και εκτέλεση:

```bash
dotnet run
```

Τώρα θα πρέπει να έχετε ένα τακτοποιημένο σύνολο αρχείων `.txt` — το καθένα το αποτέλεσμα της **εξαγωγής κειμένου από tiff** μέσω μιας πλήρως αυτοματοποιημένης διαδικασίας παρτίδας.

## Συμπέρασμα

Διασχίσαμε **πώς να εκτελέσετε OCR σε παρτίδες** σε C# από την αρχή μέχρι το τέλος, καλύπτοντας όλα όσα χρειάζεστε για να **εξάγετε κείμενο από tiff** αρχεία αποδοτικά. Τα βασικά σημεία είναι:

1. Χρησιμοποιήστε το `BatchProcessor` του Aspose.OCR για να αποφύγετε την επαναλαμβανόμενη γραφή βρόχων.  
2. Εκμεταλλευτείτε τα φίλτρα προεπεξεργασίας (deskew, despeckle) για μεγαλύτερη ακρίβεια.  
3. Ενεργοποιήστε την επιτάχυνση GPU όταν είναι δυνατόν, αλλά πάντα να έχετε fallback στην CPU.  
4. Αποθηκεύστε τα αποτελέσματα σε μια προβλέψιμη δομή φακέλων ώστε οι downstream εργασίες να τα ανακτούν αυτόματα.

Από εδώ μπορείτε να εξερευνήσετε:

- Τροφοδοσία του plain‑text σε **ευρετήριο αναζήτησης** (π.χ., Elasticsearch) για να γίνουν τα τιμολόγια αναζητήσιμα.  
- Μετατροπή της εξόδου σε **JSON** και τροφοδοσία του σε μοντέλο μηχανικής μάθησης που εξάγει στοιχεία γραμμής.  
- Προσθήκη **διαχείρισης σφαλμάτων** για κατεστραμμένα TIFF ή προβλήματα δικαιωμάτων.

Δοκιμάστε το,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}