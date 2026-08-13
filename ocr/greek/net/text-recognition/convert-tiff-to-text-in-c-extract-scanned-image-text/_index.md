---
category: general
date: 2026-03-05
description: Μετατρέψτε TIFF σε κείμενο σε C# με το Aspose OCR—εξάγετε γρήγορα κείμενο
  από σαρωμένες εικόνες και μάθετε πώς να φορτώνετε αρχείο εικόνας σε C# για επεξεργασία
  OCR.
draft: false
keywords:
- convert TIFF to text
- extract text scanned image
- load image file C#
language: el
og_description: Μετατρέψτε TIFF σε κείμενο σε C# χρησιμοποιώντας το Aspose OCR. Μάθετε
  τη πλήρη διαδικασία εξαγωγής κειμένου από σαρωμένες εικόνες και φόρτωσης αρχείων
  εικόνας αποδοτικά.
og_title: Μετατροπή TIFF σε Κείμενο σε C# – Εξαγωγή Κειμένου από Σαρωμένη Εικόνα
tags:
- OCR
- C#
- Aspose
title: Μετατροπή TIFF σε Κείμενο σε C# – Εξαγωγή Κειμένου από Σαρωμένη Εικόνα
url: /el/net/text-recognition/convert-tiff-to-text-in-c-extract-scanned-image-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Μετατροπή TIFF σε Κείμενο σε C# – Εξαγωγή Κειμένου από Σαρωμένη Εικόνα

Χρειάζεστε **convert TIFF to text in C#**; Δεν είστε ο μόνος που παλεύει με πολυ‑σελίδες σαρωμένες εικόνες που αρνούνται να γίνουν αναζητήσιμες συμβολοσειρές.  
Σε αυτόν τον οδηγό θα περάσουμε βήμα‑βήμα από μια πλήρη, έτοιμη για εκτέλεση λύση που παίρνει ένα αρχείο TIFF, το στέλνει στο Aspose OCR και εξάγει απλό κείμενο — χωρίς επιπλέον υπηρεσίες, χωρίς κρυφή μαγεία.

> **Pro tip:** Αν εργάζεστε με σαρώσεις υψηλής ανάλυσης, η ενεργοποίηση επεξεργασίας GPU μπορεί να μειώσει μερικά δευτερόλεπτα ανά σελίδα.

Θα δείξουμε επίσης πώς να **extract text scanned image** αρχεία και τον καλύτερο τρόπο να **load image file C#** στο OCR engine, ώστε να ενσωματώσετε αυτή τη λογική σε οποιοδήποτε .NET project σήμερα.

---

## What You’ll Need

Πριν προχωρήσουμε, βεβαιωθείτε ότι έχετε τα παρακάτω στη μηχανή σας:

| Requirement | Reason |
|-------------|--------|
| .NET 6.0+ (ή .NET Framework 4.7.2+) | Σύγχρονο runtime, υποστηρίζει `Span<T>` και async I/O |
| Aspose.OCR for .NET (NuGet package `Aspose.OCR`) | Η μηχανή OCR που θα χρησιμοποιήσουμε |
| Ένα έγκυρο αρχείο άδειας Aspose OCR (`Aspose.OCR.lic`) | Χωρίς αυτό θα αντιμετωπίσετε περιορισμούς αξιολόγησης |
| Ένα αρχείο TIFF (μονή ή πολυ‑σελίδα) για δοκιμή | Παράδειγμα: `scanned_multi_page.tif` |
| GPU με CUDA 11+ (προαιρετικό) | Επιταχύνει την αναγνώριση όταν `EngineMode = Gpu` |

Αν λείπει κάποιο από αυτά, κατεβάστε το NuGet package τώρα:

```bash
dotnet add package Aspose.OCR
```

---

## Step 1: Set Up the Project and Import Namespaces

Δημιουργήστε μια νέα εφαρμογή console (ή προσθέστε τον κώδικα σε υπάρχον project). Το πρώτο πράγμα που κάνουμε είναι να εισάγουμε τις κλάσεις που θα χρειαστούμε.

```csharp
using System;
using Aspose.OCR;          // Core OCR classes
using Aspose.OCR.Image;   // ImageStream helper
```

> **Why this matters:** Η εισαγωγή του `Aspose.OCR.Image` μας δίνει το εργοστάσιο `ImageStream`, το οποίο μπορεί να διαβάσει αρχεία TIFF απευθείας από δίσκο ή ροή. Η παράλειψη αυτού του βήματος θα προκαλέσει σφάλμα κατά τη μεταγλώττιση.

---

## Step 2: Initialize the OCR Engine and Choose Processing Mode

Η μηχανή OCR πρέπει να ρυθμιστεί **πριν** αναθέσετε οποιαδήποτε εικόνα. Εδώ αποφασίζουμε αν θα τρέξει στον CPU ή θα αξιοποιήσει το GPU.

```csharp
// Step 2: Initialize the OCR engine and enable GPU processing (must be set before any OCR work)
OcrEngine ocrEngine = new OcrEngine();

// Choose the processing mode that fits your environment.
// Options: Cpu (default) | Gpu | Auto
ocrEngine.EngineMode = OcrEngineMode.Gpu;   // Switch to Cpu if you don’t have a compatible GPU
```

*Αν βρίσκεστε σε headless server χωρίς κάρτα γραφικών, αλλάξτε το `Gpu` σε `Cpu` ή `Auto`.*  
Η λειτουργία του engine επηρεάζει την κατανομή μνήμης και την ταχύτητα· η λειτουργία GPU μπορεί να είναι 2‑3× γρηγορότερη σε μεγάλα, υψηλής ανάλυσης TIFF.

---

## Step 3: Apply Your Aspose OCR License

Η εκτέλεση χωρίς άδεια περιορίζει σε λίγες σελίδες και προσθέτει υδατογραφήματα. Φορτώστε την άδειά σας νωρίς ώστε κάθε επόμενη λειτουργία να είναι απεριόριστη.

```csharp
// Step 3: Apply the Aspose OCR license (replace with your own license file if needed)
ocrEngine.SetLicense("Aspose.OCR.lic");
```

> **Common pitfall:** Τοποθετώντας το `SetLicense` μετά το `Recognize()` θα κάνει τη μηχανή να επιστρέψει σε λειτουργία δοκιμής για εκείνη την κλήση.

---

## Step 4: Load the TIFF File – Handling Single and Multi‑Page Images

Το Aspose OCR μπορεί να διαβάσει πολυ‑σελίδες TIFF αμέσως, αλλά πρέπει να του δώσετε τη σωστή ροή. Ακολουθεί ένα ανθεκτικό μοτίβο που λειτουργεί και για τις δύο περιπτώσεις.

```csharp
// Step 4: Load the image to be recognized
string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

using (var imageStream = ImageStream.FromFile(tiffPath))
{
    // Step 5: Assign the image to the engine
    ocrEngine.Image = imageStream;

    // Step 6: Perform the OCR operation
    OcrResult ocrResult = ocrEngine.Recognize();

    // Step 7: Output the recognized text
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
```

### Why use `ImageStream.FromFile`?

- Απομονώνει το υποκείμενο `FileStream`, διαχειριζόμενο εσωτερικά την αρίθμηση σελίδων TIFF.  
- Λειτουργεί επίσης με `MemoryStream`, ώστε να μπορείτε να φορτώνετε εικόνες από βάση δεδομένων ή web API χωρίς να αγγίξετε το σύστημα αρχείων.

### Edge case: Very large TIFFs

Αν το TIFF σας ξεπερνά τα 200 MB, σκεφτείτε να το φορτώνετε σελίδα‑με‑σελίδα για να αποφύγετε εξαιρέσεις out‑of‑memory:

```csharp
int pageCount = ImageInfo.GetPageCount(tiffPath);
for (int i = 0; i < pageCount; i++)
{
    using var pageStream = ImageStream.FromFile(tiffPath, i);
    ocrEngine.Image = pageStream;
    var pageResult = ocrEngine.Recognize();
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(pageResult.Text);
}
```

---

## Step 5: Verify the Output

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,250.00
Thank you for your business!
```

Αν το κείμενο εμφανίζεται παραμορφωμένο, ελέγξτε:

1. **Resolution** – Το OCR λειτουργεί καλύτερα με 300 dpi ή περισσότερο.  
2. **EngineMode** – Αλλάξτε σε `Cpu` αν ο οδηγός GPU είναι παλιός.  
3. **License** – Βεβαιωθείτε ότι το μονοπάτι του αρχείου άδειας είναι σωστό και ότι το αρχείο είναι αναγνώσιμο.

---

## Frequently Asked Questions (FAQ)

### Does this work with other image formats?

Απολύτως. Το `ImageStream.FromFile` υποστηρίζει JPEG, PNG, BMP, και ακόμη PDF (μέσω Aspose.PDF). Απλώς αντικαταστήστε την επέκταση του αρχείου.

### What if I need to process images stored in a database?

Διαβάστε το BLOB σε ένα `MemoryStream` και περάστε το στο `ImageStream.FromStream(memoryStream)`. Η μηχανή OCR το αντιμετωπίζει όπως μια ροή αρχείου.

### Can I run this on Linux?

Ναι—το Aspose OCR είναι cross‑platform. Εγκαταστήστε το κατάλληλο .NET runtime και βεβαιωθείτε ότι οι απαιτούμενες βιβλιοθήκες native για GPU (αν χρησιμοποιούνται) είναι διαθέσιμες.

---

## Full Working Example (Copy‑Paste Ready)

Παρακάτω βρίσκεται ολόκληρο το πρόγραμμα, έτοιμο για μεταγλώττιση. Αντικαταστήστε το `YOUR_DIRECTORY` και το μονοπάτι του αρχείου άδειας με τις πραγματικές σας τοποθεσίες.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Image;

namespace TiffToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Choose processing mode: Gpu, Cpu, or Auto
            ocrEngine.EngineMode = OcrEngineMode.Gpu; // Change to Cpu if no GPU

            // Apply license (skip if you only need a trial)
            ocrEngine.SetLicense("Aspose.OCR.lic");

            // Path to the TIFF file
            string tiffPath = @"YOUR_DIRECTORY\scanned_multi_page.tif";

            // Load the TIFF (handles multi‑page automatically)
            using (var imageStream = ImageStream.FromFile(tiffPath))
            {
                // Assign image to engine
                ocrEngine.Image = imageStream;

                // Run OCR
                OcrResult result = ocrEngine.Recognize();

                // Display result
                Console.WriteLine("=== OCR Output ===");
                Console.WriteLine(result.Text);
            }

            // Optional: Process each page individually for huge files
            // int pages = ImageInfo.GetPageCount(tiffPath);
            // for (int i = 0; i < pages; i++) { ... }
        }
    }
}
```

Αποθηκεύστε το ως `Program.cs`, τρέξτε `dotnet run`, και παρακολουθήστε το κείμενο

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}