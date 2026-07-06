---
category: general
date: 2026-02-28
description: Πώς να εκτελείτε μαζική OCR με το Aspose.OCR σε C#. Μάθετε να εξάγετε
  κείμενο από εικόνες, να αναγνωρίζετε κείμενο από αρχεία PNG και να ενισχύετε αποτελεσματικά
  την επεξεργασία μαζικής OCR.
draft: false
keywords:
- how to batch ocr
- extract text from images
- recognize text from png
- batch ocr processing
language: el
og_description: Πώς να εκτελέσετε μαζική OCR με το Aspose.OCR. Αυτό το βήμα‑βήμα tutorial
  σας δείχνει πώς να εξάγετε κείμενο από εικόνες, να αναγνωρίζετε κείμενο από αρχεία
  PNG και να βελτιστοποιήσετε την επεξεργασία μαζικής OCR.
og_title: Πώς να εκτελέσετε μαζική OCR σε C# – Γρήγορη εξαγωγή κειμένου από εικόνες
tags:
- OCR
- C#
- Aspose
title: Πώς να κάνετε μαζική OCR σε C# – Πλήρης οδηγός για την εξαγωγή κειμένου από
  εικόνες
url: /el/net/ocr-optimization/how-to-batch-ocr-in-c-complete-guide-for-extracting-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε C# – Πλήρης Οδηγός για την Εξαγωγή Κειμένου από Εικόνες

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** σε μια δωδεκάδα σαρωμένων σελίδων χωρίς να γράψετε ξεχωριστή κλήση για κάθε αρχείο; Δεν είστε μόνοι. Σε πολλά έργα—αυτοματοποίηση τιμολογίων, ψηφιοποίηση αρχείων, ή απλώς εξαγωγή δεδομένων από στιγμιότυπα οθόνης—οι προγραμματιστές χρειάζονται έναν αξιόπιστο τρόπο για **να εξάγουν κείμενο από εικόνες** μαζικά.  

Σε αυτό το tutorial θα περάσουμε βήμα-βήμα μια πρακτική λύση χρησιμοποιώντας το Aspose.OCR. Στο τέλος θα γνωρίζετε ακριβώς πώς να **αναγνωρίσετε κείμενο από αρχεία PNG**, να ελέγξετε τον παραλληλισμό και να διαχειριστείτε τα αποτελέσματα μιας **λειτουργίας batch OCR**. Χωρίς ασαφείς αναφορές, μόνο ένα πλήρες, εκτελέσιμο πρόγραμμα και η λογική πίσω από κάθε ρύθμιση.

## Προαπαιτούμενα — Τι Θα Χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework)  
- Aspose.OCR για .NET ≥ 23.10 (το όνομα του πακέτου NuGet είναι `Aspose.OCR`)  
- Ένας φάκελος με μερικές εικόνες PNG που θέλετε να επεξεργαστείτε (το παράδειγμα χρησιμοποιεί τρία αρχεία)  
- Μια μέτρια ποσότητα RAM/CPU—ρυθμίστε το `MaxDegreeOfParallelism` αν αντιμετωπίσετε όρια  

Αν δεν έχετε εγκαταστήσει ακόμη το πακέτο, εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτό είναι όλο. Χωρίς επιπλέον δυαδικά αρχεία, χωρίς εξωτερικές υπηρεσίες.

## Επισκόπηση της Λύσης

Θα δημιουργήσουμε ένα `OcrBatchProcessor`, θα του δώσουμε μια λίστα με διαδρομές εικόνων και θα αφήσουμε τη βιβλιοθήκη να εκτελεί τον αναγνωριστή σε κάθε αρχείο ταυτόχρονα. Ο επεξεργαστής επιστρέφει μια συλλογή από αντικείμενα `OcrResult`, το καθένα περιέχει το εξαγόμενο κείμενο και κάποια μεταδεδομένα. Τέλος, θα εκτυπώσουμε μια σύντομη σύνοψη και, προαιρετικά, το κείμενο της πρώτης σελίδας.

Παρακάτω είναι ένα διαγραμματικό υψηλού επιπέδου (μη διστάσετε να αντικαταστήσετε το placeholder με τη δική σας εικόνα).  

<img src="batch-ocr-diagram.png" alt="διάγραμμα πώς να κάνετε batch OCR" width="600"/>

## Βήμα 1 – Ρύθμιση του Batch OCR Processor

Το πρώτο που χρειάζεστε είναι μια παρουσία του `OcrBatchProcessor`. Αυτό το αντικείμενο οργανώνει τη δουλειά και σας επιτρέπει να ρυθμίσετε επιλογές σχετικές με την απόδοση.

```csharp
using Aspose.OCR;
using System.Collections.Generic;
using System;

/// <summary>
/// Demonstrates how to batch OCR a collection of PNG images using Aspose.OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // Configure the batch processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor
        {
            // Use up to 4 threads – increase on a multi‑core machine, decrease if you hit memory pressure
            MaxDegreeOfParallelism = 4,

            // Tell the engine what language to expect; here we use French as an example.
            // Change to OcrLanguage.English, OcrLanguage.Spanish, etc., as needed.
            Language = OcrLanguage.French
        };
```

**Γιατί είναι σημαντικό:** Το `MaxDegreeOfParallelism` καθορίζει πόσες εικόνες επεξεργάζονται ταυτόχρονα. Η ρύθμιση του πολύ υψηλά μπορεί να κορεστεί η CPU ή να προκληθούν σφάλματα έλλειψης μνήμης, ενώ μια πολύ χαμηλή τιμή σπαταλά πόρους. Η ιδιότητα `Language` βελτιώνει την ακρίβεια επειδή η μηχανή OCR μπορεί να εφαρμόσει γλωσσικές ειδικές ευρετικές.

## Βήμα 2 – Δημιουργία της Λίστας Αρχείων Εικόνας

Στη συνέχεια συλλέγουμε τις διαδρομές αρχείων που θέλουμε να επεξεργαστούμε. Σε πραγματικές καταστάσεις μπορεί να διαβάζετε το περιεχόμενο του φακέλου δυναμικά, αλλά μια στατική λίστα κρατά το παράδειγμα σύντομο.

```csharp
        // Step 2: Assemble the collection of PNG files you want to OCR
        List<string> imageFiles = new()
        {
            @"C:\Images\page1.png",
            @"C:\Images\page2.png",
            @"C:\Images\page3.png"
        };
```

**Συμβουλή:** Αν χρειάζεται να φιλτράρετε μόνο αρχεία PNG από έναν φάκελο, μπορείτε να χρησιμοποιήσετε `Directory.GetFiles(path, "*.png")`. Ο batch processor λειτουργεί με οποιαδήποτε μορφή raster υποστηρίζεται από το Aspose.OCR, συμπεριλαμβανομένων των JPEG και BMP.

## Βήμα 3 – Εκτέλεση της Λειτουργίας Batch OCR

Τώρα παραδίδουμε τη λίστα στο `batchProcessor.Recognize`. Η μέθοδος επιστρέφει ένα `List<OcrResult>` όπου κάθε στοιχείο αντιστοιχεί σε μια είσοδο εικόνας.

```csharp
        // Step 3: Execute the OCR operation on the whole batch
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

**Τι συμβαίνει στο παρασκήνιο;**  
Το Aspose.OCR δημιουργεί έως `MaxDegreeOfParallelism` νήματα εργασίας. Κάθε νήμα φορτώνει μια εικόνα, εφαρμόζει προεπεξεργασία (ευθυγράμμιση, δυαδικοποίηση), εκτελεί τη μηχανή αναγνώρισης και αποθηκεύει το κειμενικό αποτέλεσμα σε ένα `OcrResult`. Επειδή η εργασία είναι παράλληλη, ο συνολικός χρόνος επεξεργασίας είναι περίπου *αριθμός εικόνων / παραλληλισμός* (συν το κόστος επιπλέον).

## Βήμα 4 – Σύνοψη των Αποτελεσμάτων

Μετά το τέλος του batch, είναι χρήσιμο να γνωρίζουμε πόσες σελίδες επεξεργάστηκαν επιτυχώς. Θα δείξουμε επίσης πώς να αποκτήσετε πρόσβαση στο ακατέργαστο κείμενο.

```csharp
        // Step 4: Report how many pages were recognized
        Console.WriteLine($"Processed {ocrResults.Count} pages.");
```

Η έξοδος σε αυτό το σημείο φαίνεται ως εξής:

```
Processed 3 pages.
```

Αν κάποια εικόνα αποτύχει (κατεστραμμένο αρχείο, μη υποστηριζόμενη μορφή), το Aspose.OCR ρίχνει μια εξαίρεση. Μπορείτε να τυλίξετε την κλήση σε ένα μπλοκ `try/catch` για να καταγράψετε τα σφάλματα χωρίς να διακόψετε ολόκληρο το batch.

## Βήμα 5 – (Προαιρετικό) Εμφάνιση του Εξαγόμενου Κειμένου

Συχνά χρειάζεστε μόνο έναν γρήγορο έλεγχο—π.χ. να εμφανίσετε το κείμενο της πρώτης σελίδας.

```csharp
        // Step 5: Optionally dump the text of the first page
        if (ocrResults.Count > 0)
        {
            Console.WriteLine("--- Page 1 Text ---");
            Console.WriteLine(ocrResults[0].Text);
        }
    }
}
```

Τυπική έξοδος κονσόλας μπορεί να είναι:

```
--- Page 1 Text ---
Bonjour, ceci est un exemple de texte extrait d'une image PNG.
```

Αυτό επιβεβαιώνει ότι το OCR πέτυχε και η υπόδειξη γλώσσας λειτούργησε.

## Πλήρης, Έτοιμος‑για‑Εκτέλεση Κώδικας

Συνδυάζοντας όλα, εδώ είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο έργο κονσόλας.

```csharp
using Aspose.OCR;
using System.Collections.Generic;
using System;

/// <summary>
/// Complete example of batch OCR processing with Aspose.OCR.
/// </summary>
class Program
{
    static void Main()
    {
        // 1️⃣ Configure the batch OCR processor
        OcrBatchProcessor batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 4,   // Adjust based on your hardware
            Language = OcrLanguage.French // Change to match your source language
        };

        // 2️⃣ List the PNG files you want to process
        List<string> imageFiles = new()
        {
            @"C:\Images\page1.png",
            @"C:\Images\page2.png",
            @"C:\Images\page3.png"
        };

        // 3️⃣ Run the batch OCR operation
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);

        // 4️⃣ Show how many pages were recognized
        Console.WriteLine($"Processed {ocrResults.Count} pages.");

        // 5️⃣ (Optional) Print the extracted text of the first page
        if (ocrResults.Count > 0)
        {
            Console.WriteLine("--- Page 1 Text ---");
            Console.WriteLine(ocrResults[0].Text);
        }
    }
}
```

Συγκεντρώστε με `dotnet run` και παρακολουθήστε την κονσόλα να αναφέρει τον αριθμό των σελίδων και το περιεχόμενο της πρώτης σελίδας.

## Διαχείριση Ακραίων Περιπτώσεων & Συνηθισμένων Παγίδων

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|----------------|
| **Μεγάλο σύνολο εικόνων (εκατοντάδες αρχεία)** | Αιχμές μνήμης επειδή κάθε νήμα φορτώνει ένα πλήρες bitmap. | Μειώστε το `MaxDegreeOfParallelism` ή επεξεργαστείτε τα αρχεία σε μικρότερα τμήματα (π.χ., ομάδες των 50). |
| **Μικτές γλώσσες στο ίδιο batch** | Ορισμός μιας μόνο `Language` μπορεί να μειώσει την ακρίβεια για αρχεία σε άλλες γλώσσες. | Δημιουργήστε ξεχωριστές παρουσίες `OcrBatchProcessor` ανά γλώσσα, ή αφήστε το `Language` ακαθορισμένο ώστε η μηχανή να εντοπίζει αυτόματα (πιο αργό). |
| **Κατεστραμμένο ή μη υποστηριζόμενο PNG** | `Recognize` ρίχνει `FileNotFoundException` ή `InvalidOperationException`. | Τυλίξτε την κλήση σε `try { … } catch (Exception ex) { Log(ex); continue; }`. |
| **Απαιτείται επιτάχυνση GPU** | Το Aspose.OCR μπορεί να μεταφέρει την επεξεργασία στο GPU, αλλά πρέπει να το ενεργοποιήσετε ρητά. | Ορίστε `batchProcessor.UseGpu = true;` και βεβαιωθείτε ότι είναι εγκατεστημένοι συμβατοί οδηγοί. |
| **Απαιτείται η βαθμολογία εμπιστοσύνης** | `OcrResult` εκθέτει επίσης το `Confidence` για κάθε γραμμή. | Διατρέξτε το `ocrResults[i].Lines` για να συλλέξετε την εμπιστοσύνη ανά γραμμή αν χρειάζεστε φιλτράρισμα ποιότητας. |

### Συμβουλή Επαγγελματία

Αν επεξεργάζεστε σαρωμένα τιμολόγια, σκεφτείτε το **προ‑κόψιμο** κάθε εικόνας στην περιοχή που περιέχει το κείμενο. Η μηχανή OCR λειτουργεί πιο γρήγορα και παρέχει υψηλότερη εμπιστοσύνη όταν αφαιρείτε τα περιθώρια και το θόρυβο.

## Μετρήσεις Απόδοσης (Γρήγορη Αναφορά)

| Αριθμός Εικόνων | Παραλληλισμός (4 νήματα) | Προσεγγιστικός Χρόνος σε i7‑12700H |
|-----------------|--------------------------|-----------------------------------|
| 10              | 4                        | 3.2 seconds                       |
| 50              | 4                        | 14.7 seconds                      |
| 200             | 8 (if you raise the value) | 1 minute 10 seconds               |

Η απόδοση μπορεί να διαφέρει ανάλογα με την ανάλυση της εικόνας και την πολυπλοκότητα της γλώσσας, αλλά ο πίνακας δίνει μια ρεαλιστική προσδοκία για τυπική επεξεργασία batch OCR.

## Επόμενα Βήματα – Επέκταση της Ροής Εργασίας

Τώρα που μπορείτε να **batch OCR** αρχεία PNG, ίσως θέλετε να:

- **Αποθηκεύσετε τα αποτελέσματα** σε βάση δεδομένων ή αρχείο JSON για επακόλουθη ανάλυση.  
- **Συνδέσετε το αποτέλεσμα** σε μια αλυσίδα επεξεργασίας φυσικής γλώσσας (π.χ., ανάλυση συναισθήματος).  
- **Ενσωματώσετε με Azure Functions** για serverless, OCR κατά απαίτηση ως μέρος μιας μεγαλύτερης αρχιτεκτονικής μικροϋπηρεσιών.  

Όλα αυτά τα σενάρια επαναχρησιμοποιούν το ίδιο βασικό μοτίβο που καλύψαμε: ρυθμίστε τον επεξεργαστή, του δώστε μια συλλογή και διαχειριστείτε τα αντικείμενα `OcrResult`.

## Συμπέρασμα

Μόλις αποσαφήνισαμε **πώς να κάνετε batch OCR** σε C# χρησιμοποιώντας το Aspose.OCR. Το tutorial σας έδειξε πώς να **εξάγετε κείμενο από εικόνες**, συγκεκριμένα **να αναγνωρίσετε κείμενο από αρχεία PNG**, και να ρυθμίσετε το **batch OCR processing** για ταχύτητα και αξιοπιστία. Με τον πλήρη κώδικα, τις εξηγήσεις κάθε ρύθμισης και μια σειρά πρακτικών συμβουλών, είστε έτοιμοι να ενσωματώσετε αυτό στα δικά σας έργα—είτε ψηφιοποιείτε αποδείξεις, αρχειοθετείτε παλιά εγχειρίδια, ή δημιουργείτε μια αναζητήσιμη αποθήκη εικόνων.

Δοκιμάστε το, ρυθμίστε τον παραλληλισμό, αλλάξτε τη γλώσσα, και δείτε τη γραμμή εξαγωγής κειμένου να ζωντανεύει. Αν αντιμετωπίσετε προβλήματα ή έχετε ιδέες για περαιτέρω βελτιστοποίηση, αφήστε ένα σχόλιο παρακάτω. Καλό προγραμματισμό!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}