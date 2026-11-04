---
category: general
date: 2026-04-06
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR GPU σε C#.
  Μάθετε πώς να φορτώνετε εικόνα από αρχείο και να ορίζετε το όριο μνήμης GPU σε αυτόν
  τον οδηγό βήμα‑βήμα.
draft: false
keywords:
- extract text from image
- load image from file
- set gpu memory limit
- aspose ocr example
- aspose ocr gpu
language: el
og_description: Εξάγετε κείμενο από εικόνα χρησιμοποιώντας το Aspose OCR GPU σε C#.
  Μάθετε πώς να φορτώνετε εικόνα από αρχείο και να ορίζετε όριο μνήμης GPU σε αυτόν
  τον οδηγό βήμα‑προς‑βήμα.
og_title: Εξαγωγή κειμένου από εικόνα με Aspose OCR GPU – Πλήρης οδηγός C#
tags:
- Aspose OCR
- C#
- GPU
- OCR
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR GPU – Πλήρης οδηγός C#
url: /el/net/ocr-configuration/extract-text-from-image-with-aspose-ocr-gpu-full-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εξαγωγή Κειμένου από Εικόνα με Aspose OCR GPU – Πλήρης Οδηγός C#

Έχετε χρειαστεί ποτέ να **εξάγετε κείμενο από εικόνα** αλλά να νιώσατε κολλημένοι στο σημείο που η απόδοση είχε σημασία; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν το ίδιο πρόβλημα όταν το OCR γίνεται σημείο συμφόρησης. Σε αυτό το tutorial θα σας δείξουμε ακριβώς πώς να εξάγετε κείμενο από εικόνα χρησιμοποιώντας το GPU runtime του Aspose OCR, να φορτώσετε εικόνα από αρχείο, και ακόμη να ορίσετε όριο μνήμης GPU για πιο αυστηρό έλεγχο πόρων.

Θα περάσουμε βήμα‑βήμα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα C#, θα εξηγήσουμε γιατί κάθε γραμμή είναι σημαντική, και θα επισημάνουμε κοινές παγίδες που μπορεί να συναντήσετε. Στο τέλος θα έχετε μια σταθερή βάση για την κατασκευή γρήγορων, κλιμακώσιμων pipelines OCR που τρέχουν στο GPU.

## Τι Καλύπτει Αυτός ο Οδηγός

- **Prerequisites**: .NET 6+ (ή .NET Framework 4.6+), πακέτο NuGet Aspose.OCR, ένας συμβατός οδηγός GPU.
- **Step‑by‑step code** που φορτώνει μια εικόνα από αρχείο, ρυθμίζει τη μηχανή Aspose OCR GPU, και εξάγει κείμενο.
- **Why** μπορεί να θέλετε να ορίσετε όριο μνήμης GPU και πώς να το κάνετε με ασφάλεια.
- **Edge‑case handling**: εικόνες χαμηλής ανάλυσης, έλλειψη GPU, και αντιμετώπιση προβλημάτων με τα confidence scores.
- **Next steps**: επεξεργασία σε batch, ενσωμάτωση με ASP.NET Core, και επιστροφή στην CPU εάν χρειαστεί.

> **Pro tip:** Αν δεν είστε σίγουροι αν η GPU σας χρησιμοποιείται, ελέγξτε το monitor δραστηριότητας GPU (π.χ., NVIDIA‑SMI) ενώ τρέχει το OCR. Θα δείτε μια αιχμή στη χρήση μνήμης που ταιριάζει με το όριο που ορίσατε.

---

![Διάγραμμα που δείχνει τη ροή εξαγωγής κειμένου από εικόνα χρησιμοποιώντας τη μηχανή Aspose OCR GPU engine](extract-text-from-image-aspose-ocr-gpu.png "εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR GPU")

## Βήμα 1: Αρχικοποίηση της Μηχανής Aspose OCR για Επεξεργασία με GPU

Το πρώτο πράγμα που χρειάζεστε είναι μια παρουσία `OcrEngine` που γνωρίζει ότι πρέπει να τρέχει στην GPU. Η Aspose παρέχει ένα καθαρό αντικείμενο `OcrEngineSettings` όπου μπορείτε να καθορίσετε το runtime.

```csharp
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

// Create the OCR engine and tell it to use the GPU runtime
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
});
```

**Why this matters:** Από προεπιλογή το Aspose OCR επιστρέφει στην CPU, κάτι που είναι εντάξει για μικρές εικόνες αλλά μπορεί να είναι εξαιρετικά αργό για φωτογραφίες υψηλής ανάλυσης. Ορίζοντας ρητά `Runtime = OcrRuntime.Gpu` μεταφέρει το βαρέως βάρους στην κάρτα γραφικών, προσφέροντάς σας μια αισθητή αύξηση ταχύτητας.

## Βήμα 2: (Προαιρετικό) Ορισμός Ορίου Μνήμης GPU

Αν τρέχετε σε κοινόχρηστο σταθμό εργασίας ή σε κοντέινερ με περιορισμένους πόρους GPU, μπορείτε να περιορίσετε την ποσότητα μνήμης που καταναλώνει η μηχανή OCR. Αυτό αποτρέπει καταρρεύσεις λόγω έλλειψης μνήμης και κρατά άλλες διεργασίες ευχαριστημένες.

```csharp
// Limit the GPU memory usage to 1024 MB (1 GB)
ocrEngine.Settings.GpuMemoryLimit = 1024;
```

**When to use it:**  
- **Multi‑tenant environments** όπου πολλές υπηρεσίες μοιράζονται την ίδια GPU.  
- **CI/CD pipelines** που εκχωρούν σταθερή ποσότητα μνήμης GPU ανά εργασία.  

Αν παραλείψετε αυτή τη γραμμή, η Aspose θα χρησιμοποιήσει όση μνήμη χρειάζεται, κάτι που είναι εντάξει σε αφιερωμένο σταθμό εργασίας.

## Βήμα 3: Φόρτωση Εικόνας από Αρχείο

Τώρα πρέπει να φέρουμε την εικόνα στη μνήμη. Το Aspose OCR λειτουργεί με `System.Drawing.Image`, οπότε θα χρησιμοποιήσουμε `Image.FromFile`. Βεβαιωθείτε ότι η διαδρομή δείχνει σε πραγματικό αρχείο· διαφορετικά θα εξαχθεί εξαίρεση.

```csharp
// Replace with the actual path to your high‑resolution image
string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

using (var image = Image.FromFile(imagePath))
{
    // The image is now ready for OCR processing
    // (the next step will happen inside this using block)
}
```

**Why loading from file matters:** Πολλοί προγραμματιστές προσπαθούν να τροφοδοτήσουν απευθείας έναν byte array, κάτι που λειτουργεί αλλά προσθέτει ένα περιττό βήμα μετατροπής. Η χρήση του `Image.FromFile` είναι απλή, και η δήλωση `using` εγγυάται ότι το χειριστήριο του αρχείου απελευθερώνεται άμεσα.

## Βήμα 4: Εκτέλεση OCR και Ανάκτηση του Αποτελέσματος

Με τη μηχανή ρυθμισμένη και την εικόνα φορτωμένη, μπορούμε τελικά να εξάγουμε το κείμενο. Η μέθοδος `Recognize` επιστρέφει ένα `OcrResult` που περιέχει τόσο το ακατέργαστο κείμενο όσο και ένα confidence score.

```csharp
using (var image = Image.FromFile(imagePath))
{
    // Perform OCR on the loaded image
    var ocrResult = ocrEngine.Recognize(image);

    // Display the confidence and the extracted text
    Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
    Console.WriteLine("Extracted text:");
    Console.WriteLine(ocrResult.Text);
}
```

**Understanding the output:**  
- `Confidence` είναι μια τιμή μεταξύ 0 και 1. Ένα confidence 0.95 (ή 95 %) συνήθως σημαίνει ότι το OCR είναι ακριβές.  
- `Text` περιέχει αλλαγές γραμμής όπως εμφανίζονται στην εικόνα, κάτι που είναι χρήσιμο για επεξεργασία αργότερα.

## Βήμα 5: Επαλήθευση Αποτελέσματος και Διαχείριση Edge Cases

### Έλεγχος Επιπέδων Confidence

Αν το confidence πέσει κάτω από, π.χ., 80 %, ίσως θελήσετε να επιστρέψετε στην επεξεργασία με CPU ή να εφαρμόσετε προεπεξεργασία εικόνας (π.χ., δυαδικοποίηση).

```csharp
if (ocrResult.Confidence < 0.80)
{
    Console.WriteLine("Low confidence detected – consider preprocessing or CPU fallback.");
    // Example fallback: switch to CPU runtime temporarily
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
    Console.WriteLine(cpuResult.Text);
}
```

### Διαχείριση Έλλειψης GPU

Δεν κάθε μηχάνημα διαθέτει συμβατή GPU. Η Aspose θα ρίξει ένα `OcrException` αν δεν μπορεί να αρχικοποιήσει το runtime της GPU.

```csharp
try
{
    var ocrResult = ocrEngine.Recognize(image);
    // Normal processing...
}
catch (OcrException ex) when (ex.Message.Contains("GPU"))
{
    Console.WriteLine("GPU not available – falling back to CPU.");
    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
    var cpuResult = ocrEngine.Recognize(image);
    Console.WriteLine(cpuResult.Text);
}
```

### Υψηλής Ανάλυσης Εικόνες

Πολύ μεγάλες εικόνες (π.χ., > 4000 px πλάτος) μπορούν να καταναλώσουν πολύ μνήμη GPU. Αν φτάσετε το όριο που ορίσατε νωρίτερα, η Aspose θα περικόψει την επεξεργασία. Σε τέτοιες περιπτώσεις, μειώστε πρώτα την ανάλυση της εικόνας:

```csharp
using (var original = Image.FromFile(imagePath))
{
    int maxWidth = 2000;
    var resized = new Bitmap(original, new Size(maxWidth, original.Height * maxWidth / original.Width));
    var ocrResult = ocrEngine.Recognize(resized);
    // Continue as before
}
```

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω βρίσκεται το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑και‑επικολλήσετε σε ένα νέο έργο console. Περιλαμβάνει όλα τα βήματα, τη διαχείριση σφαλμάτων, και την προαιρετική λογική fallback.

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Runtime;
using System;
using System.Drawing;

class Program
{
    static void Main()
    {
        // Step 1: Initialize OCR engine to use GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            Runtime = OcrRuntime.Gpu   // Switches processing to the GPU
        });

        // Step 2: (Optional) Limit GPU memory usage to 1 GB
        ocrEngine.Settings.GpuMemoryLimit = 1024;

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/high_res_photo.png";

        // Step 3: Load image from file
        using (var image = Image.FromFile(imagePath))
        {
            try
            {
                // Step 4: Run OCR on the image
                var ocrResult = ocrEngine.Recognize(image);

                // Step 5: Output confidence and extracted text
                Console.WriteLine($"GPU OCR confidence: {ocrResult.Confidence:P2}");
                Console.WriteLine("Extracted text:");
                Console.WriteLine(ocrResult.Text);

                // Edge‑case: low confidence handling
                if (ocrResult.Confidence < 0.80)
                {
                    Console.WriteLine("\nLow confidence detected – trying CPU fallback...");
                    ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                    var cpuResult = ocrEngine.Recognize(image);
                    Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                    Console.WriteLine(cpuResult.Text);
                }
            }
            catch (OcrException ex) when (ex.Message.Contains("GPU"))
            {
                Console.WriteLine("GPU not available – falling back to CPU runtime.");
                ocrEngine.Settings.Runtime = OcrRuntime.Cpu;
                var cpuResult = ocrEngine.Recognize(image);
                Console.WriteLine($"CPU OCR confidence: {cpuResult.Confidence:P2}");
                Console.WriteLine(cpuResult.Text);
            }
        }
    }
}
```

### Αναμενόμενο Αποτέλεσμα

```
GPU OCR confidence: 96.45%
Extracted text:
This is the text that was
found in the high‑resolution
image you supplied.

```

Αν το confidence πέσει κάτω από το όριο, θα δείτε τα επιπλέον μηνύματα fallback στην CPU.

---

## Συμπέρασμα

Τώρα ξέρετε **πώς να εξάγετε κείμενο από εικόνα** χρησιμοποιώντας τη μηχανή GPU του Aspose OCR, πώς να **φορτώνετε εικόνα από αρχείο**, και γιατί μπορεί να θέλετε να **ορίσετε όριο μνήμης GPU** για παραγωγικά φορτία εργασίας. Το παραπάνω παράδειγμα είναι μια πλήρως λειτουργική, αξιόπιστη λύση που μπορείτε να ενσωματώσετε σε οποιοδήποτε έργο .NET.

Τι ακολουθεί; Σκεφτείτε:

- **Batch processing**: επανάληψη πάνω σε φάκελο εικόνων και εγγραφή των αποτελεσμάτων σε CSV.  
- **ASP.NET Core integration**: έκθεση ενός API endpoint που δέχεται μια ανεβασμένη εικόνα και επιστρέφει το κείμενο OCR.  
- **Performance tuning**: πειραματισμός με διαφορετικές τιμές `GpuMemoryLimit` και παρακολούθηση της χρήσης GPU για το βέλτιστο σημείο.

Νιώστε ελεύθεροι να προσαρμόσετε τον κώδικα στη δική σας περίπτωση—είτε χτίζετε μια pipeline ψηφιοποίησης εγγράφων, μια εφαρμογή μετάφρασης σε πραγματικό χρόνο, ή μια υπηρεσία σάρωσης αποδείξεων. Τα θεμέλια παραμένουν τα ίδια: αρχικοποιήστε τη μηχανή GPU, διαχειριστείτε τη μνήμη σοφά, και πάντα επαληθεύστε το confidence.

Έχετε ερωτήσεις ή αντιμετωπίζετε κάποιο πρόβλημα; Αφήστε ένα σχόλιο παρακάτω, και ας το αντιμετωπίσουμε μαζί. Καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}