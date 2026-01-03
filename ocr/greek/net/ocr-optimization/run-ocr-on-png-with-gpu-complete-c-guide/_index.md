---
category: general
date: 2026-01-02
description: Εκτελέστε OCR σε PNG γρήγορα χρησιμοποιώντας το Aspose OCR και υποστήριξη
  GPU. Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα, να εξάγετε κείμενο από εικόνα
  και να ορίσετε όριο μνήμης GPU.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: el
og_description: Εκτελέστε OCR σε PNG αποδοτικά χρησιμοποιώντας το Aspose OCR και την
  επιτάχυνση GPU. Αυτό το εκπαιδευτικό δείχνει πώς να αναγνωρίζετε κείμενο από εικόνα,
  να εξάγετε κείμενο από εικόνα και να ελέγχετε τη χρήση μνήμης GPU.
og_title: Εκτέλεση OCR σε PNG με GPU – Πλήρης Οδηγός C#
tags:
- OCR
- C#
- GPU
title: Εκτέλεση OCR σε PNG με GPU – Πλήρης Οδηγός C#
url: /el/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Εκτέλεση OCR σε PNG με GPU – Πλήρης Οδηγός C#

Ever needed to **run OCR on PNG** files but felt stuck at the performance line? You're not the only one. In many real‑world pipelines a single high‑resolution PNG can throttle a CPU‑only OCR engine, turning what should be a quick lookup into a minute‑long wait.  

Τα καλά νέα είναι ότι το Aspose OCR παρέχει επεκτάσεις GPU που σας επιτρέπουν να **recognize text from image** αρχεία σε κλάσμα του χρόνου. Σε αυτό το tutorial θα περάσουμε από ένα πρακτικό παράδειγμα που δείχνει ακριβώς πώς να **run OCR on PNG** χρησιμοποιώντας C#, πώς να **extract text from image**, και ακόμη πώς να **set GPU memory limit** ώστε να παραμείνετε εντός του προϋπολογισμού του υλικού σας.  

Θα καλύψουμε επίσης το “πώς” και το “γιατί” πίσω από κάθε βήμα, ώστε να φύγετε με ένα στέρεο νοητικό μοντέλο—όχι μόνο ένα κομμάτι κώδικα αντιγραφής‑επικόλλησης.

## Τι Θα Μάθετε

- Τα προαπαιτούμενα για τη χρήση της υποστήριξης GPU του Aspose OCR.  
- Πώς να φορτώσετε ένα PNG σε ένα `Bitmap` και να το δώσετε στη μηχανή OCR.  
- Πώς να ρυθμίσετε το `GpuDevice` και το `GpuMemoryLimitMb` για βέλτιστη απόδοση.  
- Πώς να **recognize text from image** και να ανακτήσετε το αποτέλεσμα plain‑text.  
- Συμβουλές για τη διαχείριση κοινών περιπτώσεων όπως GPUs με χαμηλή μνήμη ή PNG πολλαπλών σελίδων.  

Στο τέλος αυτού του οδηγού θα μπορείτε να **run OCR on PNG** αρχεία με ταχύτητα GPU και να ελέγχετε με σιγουριά το αποτύπωμα μνήμης των εργασιών OCR σας.

![Diagram showing run OCR on PNG with GPU acceleration](run-ocr-on-png-diagram.png "run OCR on PNG example")

## Προαπαιτούμενα

Πριν βουτήξουμε, βεβαιωθείτε ότι έχετε:

1. .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Core και .NET Framework).  
2. Μια κάρτα NVIDIA GPU με υποστήριξη CUDA (το παράδειγμα επιλέγει δείκτη συσκευής 0).  
3. Το πακέτο NuGet Aspose.OCR και τις επεκτάσεις GPU του (`Aspose.OCR.Extensions`).  
4. Ένα δείγμα PNG (`input.png`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε από το πρόγραμμά σας.  

Αν κάποιο από αυτά σας φαίνεται άγνωστο, μην ανησυχείτε—θα σημειώσουμε εναλλακτικές όπου είναι σχετικό.

---

## Βήμα 1 – Εγκατάσταση Aspose OCR και Επεκτάσεων GPU

Πρώτα απ' όλα. Χωρίς τις σωστές βιβλιοθήκες, το υπόλοιπο του κώδικα δεν θα μεταγλωττιστεί.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

Το πακέτο `Aspose.OCR.Extensions` φέρνει τα εγγενή δυαδικά αρχεία CUDA που απαιτούνται για επιτάχυνση GPU.  
*Pro tip:* Αν βρίσκεστε σε μηχάνημα χωρίς GPU, μπορείτε ακόμη να μεταγλωττίσετε το έργο· απλώς ορίστε `PreferGpu = false` αργότερα.

---

## Βήμα 2 – Φόρτωση του PNG που Θέλετε να Επεξεργαστείτε

Τώρα εκτελούμε πραγματικά **run OCR on PNG** φορτώνοντάς το σε ένα `Bitmap`. Αυτό το βήμα είναι απλό αλλά αξίζει μια σύντομη σημείωση: το `Bitmap` αναμένει διαδρομή αρχείου, οπότε βεβαιωθείτε ότι η διαδρομή είναι σωστή σε σχέση με το εκτελέσιμο σας.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

Αν το PNG είναι ασυνήθιστα μεγάλο (π.χ., > 5000 px σε μια πλευρά), ίσως θελήσετε να το μειώσετε πρώτα για να αποφύγετε την εξάντληση της μνήμης GPU. Εκεί είναι χρήσιμη η επιλογή **set GPU memory limit** αργότερα.

---

## Βήμα 3 – Δημιουργία και Διαμόρφωση της Μηχανής OCR για Χρήση GPU

Αυτή είναι η καρδιά του tutorial: διαμόρφωση της μηχανής OCR για **recognize text from image** χρησιμοποιώντας το GPU. Δύο ιδιότητες είναι κλειδιά:

- `GpuDevice` – επιλέγει ποια συσκευή CUDA θα χρησιμοποιηθεί.  
- `GpuMemoryLimitMb` – περιορίζει την ποσότητα μνήμης GPU που μπορεί να εκχωρήσει η μηχανή.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Γιατί να ορίσετε όριο μνήμης;** Κάποιες GPU μοιράζονται μνήμη με την οθόνη ή εκτελούν πολλαπλά φορτία εργασίας ταυτόχρονα. Με τον περιορισμό της εκχώρησης αποτρέπετε καταρρεύσεις έλλειψης μνήμης, ειδικά όταν επεξεργάζεστε πολλά PNG παράλληλα.

---

## Βήμα 4 – Ορισμός Επιλογών Αναγνώρισης (Γλώσσα & Προτίμηση GPU)

Το αντικείμενο `RecognitionOptions` λέει στη μηχανή ποια γλώσσα να αναζητήσει και αν θα **prefer GPU** ακόμη και για μικρές εικόνες. Για τα περισσότερα αγγλικά έγγραφα αυτό είναι επαρκές, αλλά μπορείτε να αντικαταστήσετε το `Language.English` με άλλες υποστηριζόμενες τοπικές ρυθμίσεις.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Αν ποτέ χρειαστείτε να **extract text from image** σε γλώσσα διαφορετική από τα Αγγλικά, απλώς αλλάξτε το enum `Language`. Η βιβλιοθήκη υποστηρίζει δεκάδες γλώσσες έτοιμες προς χρήση.

---

## Βήμα 5 – Εκτέλεση του OCR και Ανάκτηση του Αποτελέσματος

Με όλα συνδεδεμένα, η τελική κλήση είναι μια μόνο γραμμή που πραγματικά **run OCR on PNG** και επιστρέφει ένα πλούσιο αντικείμενο αποτελέσματος.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

Το `OcrResult` περιέχει όχι μόνο απλό κείμενο (`ocrResult.Text`) αλλά και βαθμούς εμπιστοσύνης, περιοχές (bounding boxes) και ακόμη την αρχική εικόνα με επισημασμένες λέξεις—χρήσιμο αν χρειαστεί να εντοπίσετε σφάλματα ή να οπτικοποιήσετε την εξαγωγή.

**Αναμενόμενο αποτέλεσμα** (για ένα δείγμα PNG που λέει “Hello World”):

```
=== OCR Output ===
Hello World
```

Αν το κείμενο εμφανίζεται παραμορφωμένο, ελέγξτε ξανά ότι το PNG δεν είναι κατεστραμμένο και ότι το όριο μνήμης GPU δεν είναι πολύ χαμηλό για το μέγεθος της εικόνας.

---

## Βήμα 6 – Διαχείριση Ακραίων Περιπτώσεων και Συμβουλές Καλών Πρακτικών

### GPUs με Χαμηλή Μνήμη

Αν δείτε εξαίρεση όπως `CudaException: out of memory`, μειώστε το `GpuMemoryLimitMb` ή χωρίστε το PNG σε πλακίδια πριν την επεξεργασία. Η δημιουργία πλακιδίων μπορεί να γίνει με `Graphics.DrawImage` σε ένα κλώνο `Bitmap`.

### Πολλαπλά PNG σε Παρτίδα

Κατά την επεξεργασία φακέλου PNG, επαναχρησιμοποιήστε το ίδιο αντικείμενο `OcrEngine`—η αρχικοποίηση του μία φορά εξοικονομεί εναλλαγές περιβάλλοντος GPU.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### Εναλλακτική σε CPU

Αν δεν υπάρχει GPU, απλώς ορίστε `PreferGpu = false`. Η μηχανή θα επιστρέψει αυτόματα σε CPU χωρίς αλλαγές κώδικα.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Πλήρες Παράδειγμα Λειτουργίας

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να αντιγράψετε‑επικολλήσετε σε ένα νέο έργο κονσόλας. Περιλαμβάνει όλα τα παραπάνω βήματα, συν μερικούς ελέγχους ασφαλείας.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Αποθηκεύστε το αρχείο ως `Program.cs`, εκτελέστε `dotnet run`, και θα πρέπει να δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα.

---

## Συμπέρασμα

Μόλις δείξαμε πώς να **run OCR on PNG** αρχεία χρησιμοποιώντας τις επεκτάσεις GPU του Aspose OCR, πώς να **recognize text from image**, και πώς να **extract text from image** ελέγχοντας το **set GPU memory limit**. Διαμορφώνοντας το `GpuDevice` και το `GpuMemoryLimitMb` διατηρείτε την εφαρμογή σας γρήγορη και σταθερή, ακόμη και σε μετριοπαθείς GPUs.

Από εδώ μπορείτε να:

- Πειραματιστείτε με άλλες γλώσσες (`Language.French`, `Language.Spanish`).  
- Ενσωματώσετε το βήμα OCR σε μια μεγαλύτερη αλυσίδα επεξεργασίας εγγράφων.  
- Προσθέσετε μετα-επεξεργασία όπως ορθογραφικό έλεγχο ή εξαγωγή οντοτήτων για να βελτιώσετε το ακατέργαστο κείμενο.  

Θυμηθείτε, το κλειδί δεν είναι μόνο ο κώδικας αλλά η κατανόηση του γιατί κάθε ρύθμιση έχει σημασία. Όταν ξέρετε πώς να **set GPU memory limit** και πότε να επιστρέψετε σε CPU, θα δημιουργήσετε λύσεις OCR που κλιμακώνονται ομαλά.

Έχετε ερωτήσεις σχετικά με συγκεκριμένο μέγεθος PNG, multi‑page TIFFs, ή αντιμετώπιση σφαλμάτων GPU; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}