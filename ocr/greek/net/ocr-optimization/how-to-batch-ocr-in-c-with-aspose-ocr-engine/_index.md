---
category: general
date: 2026-01-01
description: Πώς να εκτελέσετε ομαδική OCR χρησιμοποιώντας τη μηχανή Aspose OCR σε
  C#. Μάθετε να αναγνωρίζετε κείμενο από εικόνες και να εξάγετε κείμενο από αρχεία
  TIFF με επιτάχυνση GPU.
draft: false
keywords:
- how to batch OCR
- recognize text from images
- extract text from TIFF
language: el
og_description: Πώς να εκτελέσετε ομαδική OCR σε C# με τη μηχανή Aspose OCR. Αυτός
  ο οδηγός σας δείχνει πώς να αναγνωρίζετε κείμενο από εικόνες και να εξάγετε κείμενο
  από αρχεία TIFF αποδοτικά.
og_title: Πώς να κάνετε ομαδική OCR σε C# – Πλήρης Οδηγός Aspose
tags:
- OCR
- C#
- Aspose
- GPU
title: Πώς να εκτελέσετε ομαδική OCR σε C# με τη μηχανή OCR της Aspose
url: /el/net/ocr-optimization/how-to-batch-ocr-in-c-with-aspose-ocr-engine/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να κάνετε Batch OCR σε C# με τον Aspose OCR Engine

Έχετε αναρωτηθεί ποτέ **πώς να κάνετε batch OCR** όταν έχετε δεκάδες σαρωμένα έγγραφα σε έναν φάκελο; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν περνούν από την αναγνώριση μιας μόνο εικόνας στην επεξεργασία ολόκληρης συλλογής. Τα καλά νέα είναι ότι ο Aspose OCR το κάνει παιχνιδάκι, είτε τρέχετε σε CPU είτε εκμεταλλεύεστε την επιτάχυνση GPU.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πλήρες, εκτελέσιμο παράδειγμα που **αναγνωρίζει κείμενο από εικόνες** και ακόμη **εξάγει κείμενο από αρχεία TIFF** μαζικά. Χωρίς ασαφείς «δείτε τα docs» συντομεύσεις—απλώς μια αυτοσχεδία λύση που μπορείτε να αντιγράψετε‑επικολλήσετε και να τρέξετε σήμερα.

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

* .NET 6.0 ή νεότερο εγκατεστημένο (ο κώδικας στοχεύει στο .NET 6, αλλά λειτουργεί και με .NET 5).
* Πακέτο NuGet Aspose.OCR για .NET (διατίθενται εκδόσεις CPU και GPU· εγκαταστήστε αυτή που ταιριάζει στο υλικό σας).
* Έναν φάκελο με μερικά δείγματα αρχείων TIFF ή PNG που θέλετε να επεξεργαστείτε.
* Visual Studio 2022 ή οποιοδήποτε IDE προτιμάτε.

> **Συμβουλή:** Αν σκοπεύετε να χρησιμοποιήσετε την έκδοση GPU, βεβαιωθείτε ότι ο οδηγός γραφικών είναι ενημερωμένος και ότι το CUDA 11+ είναι εγκατεστημένο. Η μηχανή θα επιστρέψει αυτόματα σε CPU αν δεν βρει συμβατό GPU.

## Βήμα 1 – Ρύθμιση του Project και Εγκατάσταση του Aspose.OCR

### H2: Create a New Console App and Add Aspose.OCR

Ανοίξτε ένα τερματικό (ή το Package Manager Console στο Visual Studio) και τρέξτε:

```bash
dotnet new console -n GpuBatchDemo
cd GpuBatchDemo
dotnet add package Aspose.OCR --version 23.12
```

Αν έχετε άδεια με υποστήριξη GPU, προσθέστε το πακέτο GPU αντί αυτού:

```bash
dotnet add package Aspose.OCR.GPU --version 23.12
```

Αυτό ήταν—το project σας τώρα αναφέρεται στη βιβλιοθήκη OCR που θα χρησιμοποιήσουμε για **batch OCR**.

## Βήμα 2 – Αρχικοποίηση του OCR Engine (CPU ή GPU)

### H2: How to Batch OCR – Engine Initialization

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class GpuBatchDemo
{
    static void Main()
    {
        // Create the OCR engine. It works with both CPU and GPU builds.
        var ocrEngine = new OcrEngine();

        // OPTIONAL: Force GPU usage if a compatible device is present.
        // Setting this to true won’t break on CPU‑only machines—it simply tries GPU first.
        ocrEngine.Settings.UseGpu = true;
```

**Γιατί είναι σημαντικό:** Με την εναλλαγή του `UseGpu`, αφήνετε τον Aspose να επιλέξει τη γρηγορότερη διαδρομή. Αν το GPU δεν είναι διαθέσιμο, η μηχανή αλλάζει σιωπηλά σε CPU, ώστε η batch εργασία σας να μην καταρρεύσει λόγω έλλειψης υλικού.

## Βήμα 3 – Συλλογή των Αρχείων που Θέλετε να Επεξεργαστείτε

### H2: Recognize Text from Images – Building the File List

```csharp
        // Prepare a list of image files (TIFF, PNG, JPEG, etc.).
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // You could also populate the list dynamically:
        // var imageFiles = Directory.GetFiles(@"C:\OCR\Input", "*.tif").ToList();
```

**Σημείωση για ακραίες περιπτώσεις:** Αν έχετε μίξη μορφών, αλλάξτε το μοτίβο αναζήτησης σε `"*.*"` και φιλτράρετε κατά επέκταση μέσα στον βρόχο. Έτσι το batch παραμένει ευέλικτο.

## Βήμα 4 – Επεξεργασία Κάθε Εικόνας και Προεπισκόπηση

### H2: Extract Text from TIFF – Loop Through the Files

```csharp
        // Loop through each file, run OCR, and print a short preview.
        foreach (var filePath in imageFiles)
        {
            // Load the image into Aspose's OcrImage object.
            var ocrImage = OcrImage.FromFile(filePath);

            // Run recognition.
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Display the first 50 characters of the recognized text.
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");
        }
    }
}
```

**Τι θα δείτε:** Για κάθε TIFF, η κονσόλα εκτυπώνει κάτι σαν:

```
C:\OCR\Input\doc1.tif: The quick brown fox jumps over the laz...
C:\OCR\Input\doc2.tif: Invoice #12345
Date: 2023-11-01
Total: $1,250.00
...
```

Αυτή η προεπισκόπηση επιβεβαιώνει ότι το batch ολοκληρώθηκε χωρίς να χρειάζεται να ανοίξετε κάθε αρχείο χειροκίνητα.

## Βήμα 5 – Αποθήκευση Αποτελεσμάτων (Προαιρετικό αλλά Χρήσιμο)

### H3: Persist OCR Output to Text Files

Αν χρειάζεστε το πλήρες κείμενο για επόμενη επεξεργασία, προσθέστε αυτό μέσα στον βρόχο `foreach`:

```csharp
            // Define an output path based on the source file name.
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
```

Τώρα κάθε TIFF δημιουργεί ένα συνοδευτικό αρχείο `.txt` που περιέχει το πλήρες OCR output—ιδανικό για ευρετηρίαση, αναζήτηση ή τροφοδοσία σε μοντέλο γλώσσας.

## Βήμα 6 – Εκτέλεση του Demo και Επαλήθευση

1. Κατασκευάστε το project: `dotnet build`.
2. Εκτελέστε: `dotnet run --project GpuBatchDemo.csproj`.

Θα πρέπει να δείτε τις γραμμές προεπισκόπησης στην κονσόλα και (αν προσθέσατε το προαιρετικό βήμα) μια σειρά από αρχεία `.txt` δίπλα στις πηγαίες εικόνες.

### H3: Common Pitfalls & How to Fix Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| **Empty `ocrResult.Text`** | Image too dark or low DPI | Pre‑process images (increase contrast, upscale) or set `ocrEngine.Settings.PreprocessImage = true`. |
| **GPU error “CUDA driver version is insufficient”** | Out‑of‑date driver | Update GPU driver, or set `UseGpu = false` to force CPU. |
| **Exception “File not found”** | Wrong path separator on Linux/macOS | Use `Path.Combine` or forward slashes (`/`). |

## Βήμα 7 – Κλιμάκωση (Πέρα από Μερικά Αρχεία)

Όταν περάσετε από μερικά TIFF σε χιλιάδες, σκεφτείτε:

* **Parallel processing:** Τυλίξτε το `foreach` σε `Parallel.ForEach` (βεβαιωθείτε ότι η μηχανή είναι thread‑safe· διαφορετικά δημιουργήστε μία ανά νήμα).
* **Chunked I/O:** Διαβάζετε εικόνες σε παρτίδες για να μην εξαντλήσετε τη μνήμη RAM.
* **Logging:** Γράψτε πρόοδο σε αρχείο log· βοηθά στην επαναφορά μετά από σφάλμα.

```csharp
Parallel.ForEach(imageFiles, filePath =>
{
    // Same OCR logic as before, but each thread gets its own engine.
    var engine = new OcrEngine { Settings = { UseGpu = true } };
    // ... rest of the code
});
```

> **Θυμηθείτε:** Η μνήμη GPU μοιράζεται, οπότε η δημιουργία πάρα πολλών παράλληλων εργασιών GPU μπορεί στην πραγματικότητα να επιβραδύνει. Δοκιμάστε πρώτα με λίγα νήματα.

## Πλήρες Παράδειγμα Εργασίας (Έτοιμο για Copy‑Paste)

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1 – Create OCR engine (CPU or GPU)
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.UseGpu = true; // Try GPU, fallback to CPU automatically

        // Step 2 – List of TIFF files to process
        var imageFiles = new List<string>
        {
            @"C:\OCR\Input\doc1.tif",
            @"C:\OCR\Input\doc2.tif",
            @"C:\OCR\Input\doc3.tif"
        };

        // Step 3 – Process each file
        foreach (var filePath in imageFiles)
        {
            var ocrImage = OcrImage.FromFile(filePath);
            var ocrResult = ocrEngine.Recognize(ocrImage);

            // Show a short preview
            Console.WriteLine($"{filePath}: {ocrResult.Text.Substring(0, Math.Min(50, ocrResult.Text.Length))}...");

            // Optional: Save full text to a .txt file
            var outputPath = Path.ChangeExtension(filePath, ".txt");
            File.WriteAllText(outputPath, ocrResult.Text);
        }
    }
}
```

Η εκτέλεση αυτού του προγράμματος θα **αναγνωρίζει κείμενο από εικόνες**, **εξάγει κείμενο από TIFF**, και θα δείξει **πώς να κάνετε batch OCR** αποδοτικά.

---

## Συμπέρασμα

Τώρα έχετε ένα ολοκληρωμένο, end‑to‑end παράδειγμα του **πώς να κάνετε batch OCR** σε C# χρησιμοποιώντας τη μηχανή OCR της Aspose. Το tutorial κάλυψε τα πάντα—from τη ρύθμιση του project, την εναλλαγή επιτάχυνσης GPU, τη δημιουργία λίστας αρχείων, την επεξεργασία κάθε εικόνας, και την αποθήκευση των αποτελεσμάτων. Είτε εξάγετε κείμενο από TIFF είτε από οποιαδήποτε άλλη μορφή εικόνας, το ίδιο μοτίβο ισχύει—απλώς αλλάξτε τις επεκτάσεις αρχείων.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να ενσωματώσετε το OCR output σε ευρετήριο αναζήτησης, να τροφοδοτήσετε το κείμενο σε μεγάλο μοντέλο γλώσσας, ή να πειραματιστείτε με παράλληλη επεξεργασία για να μειώσετε λεπτά σε τεράστιες παρτίδες. Ο ουρανός είναι το όριο, και έχετε τη βάση για να χτίσετε.

Έχετε ερωτήσεις ή θέλετε να μοιραστείτε τα δικά σας batch‑OCR κόλπα; Αφήστε ένα σχόλιο παρακάτω—happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}