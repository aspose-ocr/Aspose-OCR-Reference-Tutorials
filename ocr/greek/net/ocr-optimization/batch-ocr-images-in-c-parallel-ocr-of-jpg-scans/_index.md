---
category: general
date: 2026-04-29
description: Επεξεργαστείτε μαζικά εικόνες OCR γρήγορα με το Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε κείμενο από αρχεία jpg, να διαβάζετε κείμενο από σαρώσεις και να
  επεξεργάζεστε τη λίστα εικόνων παράλληλα.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: el
og_description: Επεξεργαστείτε μαζικά εικόνες OCR γρήγορα με το Aspose OCR. Αυτός
  ο οδηγός δείχνει πώς να εξάγετε κείμενο από jpg, να διαβάσετε κείμενο από σαρώσεις
  και να επεξεργαστείτε μια λίστα εικόνων παράλληλα.
og_title: Ομαδική OCR Εικόνων σε C# – Παράλληλη OCR Σαρωμένων JPG
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Ομαδική OCR Εικόνων σε C# – Παράλληλη OCR Σαρωμάτων JPG
url: /el/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch OCR Images in C# – Parallel OCR of JPG Scans

Ποτέ χρειάστηκε να **batch OCR images** αλλά δεν ήξερες πώς να κλιμακώσεις τη δουλειά σε πολλά αρχεία; Δεν είσαι μόνος—οι προγραμματιστές συχνά συναντούν εμπόδια όταν προσπαθούν να διαβάσουν κείμενο από σκαναρίσματα ένα‑ένα. Τα καλά νέα είναι ότι με το Aspose OCR μπορείς να **extract text from jpg** αρχεία, **read text from scans**, και να **process image list** στοιχεία παράλληλα με μερικές μόνο γραμμές C#.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑να‑τρέξει παράδειγμα που δείχνει ακριβώς πώς γίνεται αυτό. Στο τέλος θα έχεις μια αυτόνομη εφαρμογή κονσόλας που αναγνωρίζει έναν φάκελο με σκαναρισμένα JPEG, εκτυπώνει το κείμενο κάθε σελίδας και σου λέει πόσο χρόνο πήρε η κάθε λειτουργία. Χωρίς εξωτερικά έγγραφα, χωρίς ημι‑συμπληρωμένα αποσπάσματα κώδικα—απλώς μια πλήρης λύση που μπορείς να ενσωματώσεις στο Visual Studio και να τρέξεις.

## What You’ll Need

- **.NET 6.0** ή νεότερο (ο κώδικας μεταγλωττίζεται επίσης σε .NET Framework 4.6+)
- **Aspose.OCR** πακέτο NuGet (`Install-Package Aspose.OCR`)
- Μια χούφτα αρχεία JPG ή σκαναρισμένες εικόνες που θέλεις να επεξεργαστείς
- Οποιοδήποτε IDE προτιμάς· εγώ χρησιμοποιώ Visual Studio 2022, αλλά το VS Code λειτουργεί επίσης

Αυτό είναι όλο. Αν ήδη έχεις το πακέτο NuGet, είσαι έτοιμος να ξεκινήσεις.

## Step 1 – Initialize the OCR Engine (Batch OCR Images Setup)

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα αντικείμενο `OcrEngine` και να του πούμε ποια γλώσσα πρέπει να αναζητήσει. Στις περισσότερες περιπτώσεις η Αγγλική είναι αρκετή, αλλά μπορείς να αντικαταστήσεις το `OcrLanguage.English` με οποιαδήποτε υποστηριζόμενη γλώσσα.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Γιατί είναι σημαντικό:* Η αρχικοποίηση του κινητήρα μία φορά και η επαναχρησιμοποίησή του σε όλες τις εικόνες είναι πολύ πιο αποδοτική από το να δημιουργείς νέο αντικείμενο για κάθε αρχείο. Επιτρέπει επίσης στο Aspose να μοιράζεται εσωτερικούς πόρους, κάτι που είναι κρίσιμο για **parallel OCR processing**.

## Step 2 – Build the List of Images (Process Image List)

Στη συνέχεια ορίζουμε τη συλλογή των διαδρομών αρχείων που θέλουμε να περάσουμε στον batch recogniser. Μπορείς να δημιουργήσεις αυτή τη λίστα δυναμικά με `Directory.GetFiles`, αλλά για σαφήνεια θα κωδικοποιήσουμε μερικές εγγραφές.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Συμβουλή:* Αν έχεις χιλιάδες σκαναρίσματα, σκέψου να χρησιμοποιήσεις `Directory.EnumerateFiles` με φίλτρο όπως `*.jpg` ώστε να μην φορτώνεις ολόκληρη τη λίστα στη μνήμη ταυτόχρονα.

## Step 3 – Run the Batch Recognition (Parallel OCR Processing)

Τώρα έρχεται η καρδιά του ζητήματος: η κλήση του `BatchRecognize`. Η μέθοδος δέχεται ένα όρισμα `maxDegreeOfParallelism`, που ελέγχει πόσα νήματα θα δημιουργήσει το Aspose. Από προεπιλογή χρησιμοποιεί τέσσερα νήματα, αλλά μπορείς να το αυξήσεις αν ο επεξεργαστής σου έχει περισσότερους πυρήνες.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*Τι συμβαίνει στο παρασκήνιο;* Το Aspose χωρίζει τη συλλογή `imagePaths` σε τμήματα, δίνει κάθε τμήμα σε ξεχωριστό νήμα και συγκεντρώνει τα αποτελέσματα. Αυτός είναι ο πιο αποδοτικός τρόπος για **extract text from jpg** αρχεία όταν έχεις μια **process image list** που μπορεί να αντιμετωπιστεί ταυτόχρονα.

## Step 4 – Display the Results (Read Text from Scans)

Τέλος, διατρέχουμε τη συλλογή `recognitionResults` και εκτυπώνουμε το κείμενο και το χρόνο επεξεργασίας για κάθε αρχείο. Το αντικείμενο `OcrResult` μας δίνει επίσης το όνομα του πηγαίου αρχείου, κάτι που βοηθά όταν χρειάζεται να καταγράψεις ή να αποθηκεύσεις το αποτέλεσμα.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Αναμενόμενη έξοδος (παράδειγμα):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Παρατήρησε πώς κάθε μπλοκ εμφανίζει το όνομα του αρχείου, το χρόνο που πήρε το OCR και το εξαγόμενο κείμενο. Αυτές είναι ακριβώς οι πληροφορίες που χρειάζεσαι όταν **reading text from scans** σε μια παραγωγική γραμμή.

## Handling Common Edge Cases

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **Missing file** | `FileNotFoundException` που ρίχνεται μέσα στο `BatchRecognize` | Επαλήθευσε τις διαδρομές με `File.Exists` πριν τις προσθέσεις στο `imagePaths`. |
| **Unsupported format** | Το Aspose υποστηρίζει μόνο raster εικόνες (JPG, PNG, BMP, TIFF). | Μετέτρεψε PDFs σε εικόνες πρώτα (χρησιμοποίησε Aspose.PDF) ή παράλειψε αυτά τα αρχεία. |
| **Memory pressure** | Πολύ μεγάλες εικόνες μπορεί να εξαντλήσουν τη RAM όταν τρέχουν πολλά νήματα. | Μείωσε το `maxDegreeOfParallelism` ή μικρύνισε τις εικόνες πριν το OCR. |
| **Non‑English text** | Η γλώσσα ορισμένη στα Αγγλικά θα αγνοήσει άλλα αλφάβητα. | Άλλαξε σε `Language = OcrLanguage.French` (ή σε πολυγλωσσικό συνδυασμό). |

Αυτές οι συμβουλές κρατούν τη batch εργασία σου αξιόπιστη, ειδικά όταν **processing an image list** προέρχεται από ανεβάσματα χρηστών ή από ένα σκαναρισμένο αρχείο.

## Pro Tip – Tuning Parallelism

Αν τρέξεις αυτό το παράδειγμα σε μηχάνημα με 8 πυρήνες, αύξησε το parallelism σε 6 ή 8 και παρατήρησε τη βελτίωση στην ταχύτητα. Ωστόσο, θυμήσου ότι κάθε νήμα καταναλώνει επίσης μνήμη για το bitmap. Ένας καλός κανόνας:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

Χρησιμοποίησε το `maxThreads` στο `BatchRecognize` για μια δυναμική, προσαρμοσμένη στη μηχανή ρύθμιση.

## Full Working Example (Copy‑Paste Ready)

Παρακάτω είναι το πλήρες πρόγραμμα, έτοιμο για μεταγλώττιση. Απλώς αντικατέστησε το `YOUR_DIRECTORY` με τη διαδρομή που περιέχει τα JPG σκαναρίσματά σου.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Note:** Η γραμμή `using System.IO;` είναι απαραίτητη για τον βοηθό `Directory`. Ο κώδικας εκτυπώνει ένα φιλικό μήνυμα αν δεν βρεθούν JPG, αποτρέποντας μια σιωπηλή αποτυχία.

## Conclusion

Δείξαμε πώς να υλοποιήσεις μια καθαρή ροή **batch OCR images** που **extracts text from jpg** αρχεία, **reads text from scans**, και επεξεργάζεται αποδοτικά μια **image list** χρησιμοποιώντας **parallel OCR processing**. Το πλήρες, εκτελέσιμο παράδειγμα δείχνει ακριβώς πώς να ρυθμίσεις τον κινητήρα, να του δώσεις μια συλλογή αρχείων και να διαχειριστείς τα αποτελέσματα—όλα ενώ διατηρείς τον έλεγχο της μνήμης και του αριθμού των νημάτων.

Έτοιμος για το επόμενο βήμα; Δοκίμασε να αλλάξεις τη γλώσσα σε Γαλλικά, πρόσθεσε μετατροπή PDF‑σε‑εικόνα, ή αποθήκευσε το κείμενο OCR σε βάση δεδομένων. Το μοτίβο παραμένει το ίδιο: αρχικοποίησε μία φορά, δώσε μια λίστα, και άφησε το Aspose να κάνει το σκληρό έργο παράλληλα.

Έχεις ερωτήσεις ή θέλεις να μοιραστείς τις δικές σου βελτιώσεις; Άφησε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

![Batch OCR images processing flow](https://example.com/placeholder.png "Διάγραμμα που απεικονίζει τη ροή επεξεργασίας batch OCR images")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}