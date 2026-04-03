---
category: general
date: 2026-04-03
description: Μάθετε πώς να εκτελείτε OCR σε παρτίδες με το Aspose.OCR σε C#. Αυτός
  ο οδηγός σας δείχνει πώς να εξάγετε κείμενο από εικόνες PNG και να μετατρέπετε εικόνες
  σε κείμενο αποδοτικά.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: el
og_description: Ανακαλύψτε πώς να εκτελείτε μαζική OCR σε C# για την εξαγωγή κειμένου
  από εικόνες PNG και τη μετατροπή εικόνων σε κείμενο χρησιμοποιώντας το Aspose.OCR.
  Περιλαμβάνεται πλήρης κώδικας.
og_title: Πώς να κάνετε ομαδική OCR σε C# – Σύντομος οδηγός
tags:
- OCR
- C#
- Aspose
title: Πώς να κάνετε μαζική OCR σε C# – Γρήγορος τρόπος εξαγωγής κειμένου από αρχεία
  PNG
url: /el/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε C# – Γρήγορος τρόπος εξαγωγής κειμένου από αρχεία PNG

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε ολόκληρο φάκελο στιγμιότυπων χωρίς να γράψετε βρόχο για κάθε αρχείο; Δεν είστε οι μόνοι. Σε πολλά έργα—σκεφτείτε την ψηφιοποίηση τιμολογίων ή την αρχειοθέτηση σαρωμένων αποδείξεων—τελειώνετε με δεκάδες, μερικές φορές εκατοντάδες, αρχεία PNG που χρειάζονται εξαγωγή κειμένου. Τα καλά νέα; Με το Aspose.OCR μπορείτε να **εξάγετε κείμενο PNG** εικόνες παράλληλα, και όλη η διαδικασία μπορεί να ολοκληρωθεί με λίγες μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που δείχνει πώς να **μετατρέψετε εικόνες σε κείμενο** χρησιμοποιώντας έναν batch επεξεργαστή. Θα καλύψουμε τις προαπαιτήσεις, θα εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική, και θα προσθέσουμε μερικές επαγγελματικές συμβουλές ώστε να μην αντιμετωπίσετε κοινές παγίδες αργότερα.

## Προαπαιτήσεις

- **.NET 6.0** (ή νεότερο) εγκατεστημένο στον υπολογιστή σας. Παλαιότερα runtime λειτουργούν, αλλά η πιο πρόσφατη προσφέρει καλύτερη απόδοση και υποστήριξη async.
- **Aspose.OCR for .NET** πακέτο. Μπορείτε να το αποκτήσετε μέσω NuGet: `dotnet add package Aspose.OCR`.
- Ένας φάκελος γεμάτος **PNG** εικόνες που θέλετε να επεξεργαστείτε. Θα τον αναφέρουμε ως `YOUR_DIRECTORY` σε όλη την οδηγία.
- Μια μέτρια ποσότητα RAM—batch OCR μπορεί να καταναλώνει πολύ μνήμη αν αυξήσετε το parallelism, αλλά η χρήση του `Environment.ProcessorCount` το κρατά ασφαλές.

> **Pro tip:** Αν βρίσκεστε σε CI/CD pipeline, προσθέστε το αρχείο άδειας Aspose ως μυστικό για να αποφύγετε το όριο των 20 σελίδων της δωρεάν αξιολόγησης.

Τώρα, ας βάλουμε τα χέρια μας στη δουλειά.

## Βήμα 1: Ρύθμιση του Batch OCR Processor (Primary Keyword in Header)

Το πρώτο πράγμα που χρειάζεστε είναι μια παρουσία της `BatchOcrProcessor`. Αυτή η κλάση αφαιρεί τη λογική των νημάτων και σας επιτρέπει να εστιάσετε στο τι θα κάνετε με κάθε εικόνα.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Γιατί αυτό είναι σημαντικό:**  
- `Engine = new OcrEngine()` σας δίνει μια νέα μηχανή OCR για κάθε νήμα, αποφεύγοντας τον ανταγωνισμό.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` κλιμακώνεται αυτόματα στον αριθμό των πυρήνων, παρέχοντάς σας τη βέλτιστη απόδοση χωρίς χειροκίνητη ρύθμιση.

## Βήμα 2: Σύνδεση με τα Γεγονότα Προόδου (Βοηθά στην Παρακολούθηση της Εξαγωγής)

Η παρακολούθηση της προόδου είναι ουσιώδης όταν επεξεργάζεστε εκατοντάδες αρχεία. Το γεγονός `ProgressChanged` ενεργοποιείται μετά από κάθε ολοκληρωμένο αρχείο, επιτρέποντάς σας να καταγράψετε την κατάσταση.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Γιατί θα το αγαπήσετε:**  
- Η ανατροφοδότηση σε πραγματικό χρόνο αποτρέπει το ερώτημα αν η εφαρμογή έχει κολλήσει.  
- Αν χρειαστεί ποτέ να διακόψετε ή να ακυρώσετε, έχετε ήδη ένα hook για να ελέγξετε το `e.Current` έναντι του `e.Total`.

## Βήμα 3: Ορισμός Σάρωσης Φακέλου και Προτύπου Αρχείου (Extract Text PNG)

Τώρα λέμε στον επεξεργαστή πού να ψάξει και τι είδους αρχεία να πάρει. Το πρότυπο `"*.png"` εξασφαλίζει ότι χειριζόμαστε μόνο εικόνες PNG.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Γιατί αυτό είναι κλειδί:**  
- Η χρήση ενός glob pattern διατηρεί τον κώδικα ευέλικτο· αλλάξτε το `*.png` σε `*.jpg` αν αργότερα χρειαστεί να χειριστείτε JPEG.  
- Η callback λαμβάνει τόσο τη διαδρομή της εικόνας όσο και το αναγνωρισμένο κείμενο, δίνοντάς σας πλήρη έλεγχο για το επόμενο βήμα.

## Βήμα 4: Αποθήκευση Αναγνωρισμένου Κειμένου Δίπλα στην Πηγή (Convert Images to Text)

Μέσα στην callback θα γράψουμε το αποτέλεσμα OCR σε ένα αρχείο `.txt` που βρίσκεται ακριβώς δίπλα στο αρχικό PNG. Αυτός είναι ο πιο απλός τρόπος για **να μετατρέψετε εικόνες σε κείμενο** για επεξεργασία downstream.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Γιατί επιλέγουμε ένα δίπλα‑δίπλα αρχείο `.txt`:**  
- Διατηρεί τη σχέση προφανή—ανοίξτε το PNG, ανοίξτε το TXT, συγκρίνετε.  
- Δεν χρειάζεται βάση δεδομένων ή επιπλέον στρώμα αποθήκευσης σε μικρές εφαρμογές.

## Βήμα 5: Ολοκλήρωση με Φιλικό Μήνυμα Ολοκλήρωσης

Ένα καθαρό μήνυμα στην κονσόλα σας ενημερώνει πότε όλα έχουν ολοκληρωθεί.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Όταν εκτελέσετε το πρόγραμμα, θα δείτε έξοδο όπως:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Κάθε PNG τώρα έχει ένα αδελφό αρχείο `.txt` που περιέχει το εξαγόμενο κείμενο.

## Πλήρες Παράδειγμα Εργασίας (Όλα τα Βήματα Συνδυασμένα)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο έργο κονσόλας. Δεν λείπουν τμήματα—απλώς αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη διαδρομή προς τις εικόνες σας.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Αναμενόμενο Αποτέλεσμα

- Για κάθε `image.png` στο `C:\MyImages`, εμφανίζεται ένα `image.txt` δίπλα του.
- Η κονσόλα εκτυπώνει γραμμές προόδου, καθιστώντας εύκολη την παρακολούθηση μεγάλων batch.
- Χωρίς χειροκίνητο βρόχο ή διαχείριση νημάτων—το `BatchOcrProcessor` διαχειρίζεται τα πάντα.

## Συχνές Ερωτήσεις & Ακραίες Περιπτώσεις

### Τι γίνεται αν οι εικόνες μου δεν είναι PNG;

Απλώς αλλάξτε το δεύτερο όρισμα στο `ProcessFolder` σε `"*.jpg"` ή `"*.*"` για να συμπεριλάβετε όλα τα αρχεία. Η μηχανή OCR λειτουργεί με τις περισσότερες μορφές raster.

### Πόση μνήμη καταναλώνει αυτό;

`BatchOcrProcessor` φορτώνει μία εικόνα ανά νήμα. Με το `Environment.ProcessorCount` ορισμένο, π.χ., σε 8 πυρήνες, θα έχετε οκτώ εικόνες στη μνήμη ταυτόχρονα. Αν αντιμετωπίσετε εξαιρέσεις OutOfMemory, μειώστε το parallelism:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### Μπορώ να προσαρμόσω τη γλώσσα OCR;

Απόλυτα. Μετά τη δημιουργία της μηχανής, ορίστε την ιδιότητα `Language`:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Το Aspose υποστηρίζει πολλές γλώσσες· απλώς προσθέστε το κατάλληλο πακέτο NuGet αν χρειάζεται.

### Τι γίνεται με τη διαχείριση σφαλμάτων;

Τυλίξτε την callback σε μπλοκ try/catch και καταγράψτε τις αποτυχίες. Ο επεξεργαστής θα συνεχίσει με το επόμενο αρχείο, αποτρέποντας ένα μόνο κατεστραμμένο αρχείο να διακόψει ολόκληρη τη λειτουργία.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Pro Tips για Κλιμάκωση

- **Διαχωρίστε τον φάκελο**: Αν έχετε δεκάδες χιλιάδες αρχεία, χωρίστε τα σε υποφακέλους και εκτελέστε πολλαπλές εργασίες batch διαδοχικά.
- **Χρησιμοποιήστε cloud VM**: Ένα μηχάνημα με περισσότερους πυρήνες (π.χ., 32‑πυρήνα) θα ολοκληρωθεί πολύ πιο γρήγορα. Απλώς θυμηθείτε να προσαρμόσετε τα όρια άδειας.
- **Μετα‑επεξεργασία του κειμένου**: Μετά την εξαγωγή, ίσως θέλετε να τρέξετε regexes για να εξάγετε αριθμούς τιμολογίων ή ημερομηνίες. Τα αρχεία `.txt` είναι τέλεια είσοδος για τέτοιους pipelines.

## Συμπέρασμα

Τώρα έχετε μια σταθερή, έτοιμη‑για‑παραγωγή συνταγή για **πώς να κάνετε batch OCR** σε έναν φάκελο PNG, **να εξάγετε κείμενο PNG** αρχεία, και **να μετατρέψετε εικόνες σε κείμενο** χρησιμοποιώντας το Aspose.OCR σε C#. Το παράδειγμα είναι αυτόνομο, εξηγεί το “γιατί” πίσω από κάθε γραμμή, και περιλαμβάνει συμβουλές για διαχείριση μεγαλύτερων φορτίων ή διαφορετικών τύπων αρχείων.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αλλάξετε την callback ώστε να σπρώχνει τα αποτελέσματα σε μια βάση δεδομένων, ή προσθέστε προ‑επεξεργασία εικόνας (π.χ., διόρθωση κλίσης) πριν το OCR. Το μοτίβο κλιμακώνεται καλά, ώστε να το προσαρμόσετε σε οποιοδήποτε σενάριο batch‑processing που συναντάτε.

Καλή προγραμματιστική, και εύχομαι οι OCR pipelines σας να είναι γρήγοροι και χωρίς σφάλματα!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}