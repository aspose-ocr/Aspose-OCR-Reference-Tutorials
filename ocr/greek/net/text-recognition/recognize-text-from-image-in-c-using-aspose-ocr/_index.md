---
category: general
date: 2026-05-31
description: Μάθετε πώς να αναγνωρίζετε κείμενο από εικόνα σε C# με το Aspose OCR,
  συμπεριλαμβανομένου του πώς να εξάγετε κείμενο από αρχεία TIFF και να φορτώνετε
  εικόνα για OCR αποδοτικά.
draft: false
keywords:
- recognize text from image
- extract text from tiff
- load image for OCR
- Aspose OCR C#
- GPU accelerated OCR
language: el
og_description: Βήμα-βήμα οδηγός για την αναγνώριση κειμένου από εικόνα με το Aspose
  OCR, καλύπτοντας την εξαγωγή από tiff και τη σωστή φόρτωση της εικόνας για OCR.
og_title: αναγνώριση κειμένου από εικόνα σε C# χρησιμοποιώντας Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to recognize text from image in C# with Aspose OCR, including
    how to extract text from tiff files and load image for OCR efficiently.
  headline: recognize text from image in C# using Aspose OCR
  type: TechArticle
- questions:
  - answer: Reduce its resolution before feeding it to the engine, or increase `GpuMemoryLimit`
      if you have enough VRAM.
    question: What if the image is huge (over 10 MB)?
  - answer: Absolutely. Just reuse the same `OcrEngine` instance and assign a new
      `ImageStream` each iteration.
    question: Can I process multiple images in a loop?
  - answer: '`OcrEngine` implements `IDisposable`. Wrap it in a `using` block for
      clean resource management, especially when working with GPU resources.'
    question: Do I need to dispose of anything?
  - answer: Set `engine.Language = OcrLanguage.Spanish` (or any supported language)
      before calling `Recognize()`.
    question: What about languages other than English?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Αναγνώριση κειμένου από εικόνα σε C# χρησιμοποιώντας Aspose OCR
url: /el/net/text-recognition/recognize-text-from-image-in-c-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση κειμένου από εικόνα σε C# χρησιμοποιώντας Aspose OCR

Έχετε ποτέ χρειαστεί να **αναγνωρίσετε κείμενο από εικόνα** αλλά δεν ήξερες από πού να ξεκινήσεις σε C#; Δεν είστε μόνοι—πολλοί προγραμματιστές αντιμετωπίζουν αυτό το πρόβλημα όταν δουλεύουν με σαρωμένα έγγραφα ή πολυ‑σελίδες TIFF. Σε αυτόν τον οδηγό θα σας καθοδηγήσουμε βήμα‑βήμα μέσα από ένα πλήρες, έτοιμο‑για‑εκτέλεση παράδειγμα που **αναγνωρίζει κείμενο από εικόνα** χρησιμοποιώντας τη βιβλιοθήκη Aspose OCR, και θα σας δείξουμε επίσης πώς να **εξάγετε κείμενο από tiff** και τον καλύτερο τρόπο για **φόρτωση εικόνας για OCR** χωρίς να τσακίζετε τα μαλλιά σας.

Θα καλύψουμε τα πάντα, από την εγκατάσταση του πακέτου NuGet μέχρι τη διαχείριση επιτάχυνσης GPU και την επιστροφή σε CPU όταν χρειαστεί. Στο τέλος αυτού του σεμιναρίου θα έχετε μια εφαρμογή κονσόλας που εκτυπώνει το αναγνωρισμένο κείμενο και το χρόνο επεξεργασίας—χωρίς κενά, χωρίς ασαφείς αναφορές.

## Τι Θα Δημιουργήσετε

- Μια απλή εφαρμογή .NET console που φορτώνει μια εικόνα (συμπεριλαμβανομένου πολυ‑σελίδων TIFF)  
- Μια μηχανή OCR ρυθμισμένη για χρήση GPU, με ομαλή εναλλακτική σε CPU  
- Εξαγωγή απλού κειμένου από την εικόνα, εκτυπωμένο στην κονσόλα  
- Πληροφορίες χρονομέτρησης ώστε να δείτε την επίδραση απόδοσης του GPU έναντι του CPU  

**Απαιτούμενα**

- .NET 6 SDK ή νεότερο (ο κώδικας λειτουργεί με .NET Core και .NET Framework)  
- Βασική εξοικείωση με C# και τη γραμμή εντολών  
- Πρόσβαση στο Internet για λήψη του πακέτου NuGet Aspose.OCR  

Αν έχετε όλα αυτά, ας ξεκινήσουμε.

![Κώδικας C# για αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR](image.png "Κώδικας C# για αναγνώριση κειμένου από εικόνα χρησιμοποιώντας Aspose OCR")

## Βήμα 1 – Αναγνώριση κειμένου από εικόνα: Ρύθμιση της μηχανής OCR

Πρώτα απ' όλα, χρειαζόμαστε μια παρουσία `OcrEngine`. Το Aspose OCR σας επιτρέπει να επιλέξετε τη συσκευή επεξεργασίας—GPU για ταχύτητα, CPU ως εφεδρική λύση. Η μηχανή δέχεται επίσης υπόδειξη περιορισμού μνήμης, κάτι χρήσιμο σε κοινόχρηστους υπολογιστές.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Create the OCR engine and request GPU acceleration.
        // If no compatible GPU is found, Aspose silently falls back to CPU.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,      // Try GPU first
            GpuMemoryLimit = 1024        // Optional: cap GPU memory usage (MB)
        };
```

**Γιατί αυτό είναι σημαντικό:**  
Η επιλογή `OcrDevice.Gpu` μπορεί να μειώσει κατά δευτερόλεπτα τον χρόνο αναγνώρισης για μεγάλες εικόνες, ειδικά πολυ‑σελίδες TIFF. Το `GpuMemoryLimit` αποτρέπει την εφαρμογή σας από το να καταναλώνει όλη τη μνήμη GPU σε κοινόχρηστο σταθμό εργασίας.

## Βήμα 2 – Φόρτωση εικόνας για OCR (συμπεριλαμβανομένης της υποστήριξης TIFF)

Τώρα τροφοδοτούμε τη μηχανή με μια εικόνα. Η μέθοδος `ImageStream.FromFile` του Aspose δέχεται **οποιαδήποτε** μορφή που υποστηρίζει η βιβλιοθήκη—TIFF, PNG, JPEG, ό,τι θέλετε. Αυτό το βήμα καλύπτει άμεσα την απαίτηση **φόρτωση εικόνας για OCR**.

```csharp
        // Load the image you want to process.
        // Replace the path with the actual location of your TIFF or other image.
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");
```

**Συμβουλή:** Αν εργάζεστε με πολυ‑σελίδες TIFF, το Aspose αντιμετωπίζει αυτόματα κάθε σελίδα ως ξεχωριστό καρέ, και η μηχανή θα τις επεξεργαστεί διαδοχικά. Δεν απαιτείται επιπλέον κώδικας.

## Βήμα 3 – Εκτέλεση της αναγνώρισης και **εξαγωγή κειμένου από tiff**

Με τη μηχανή έτοιμη και την εικόνα φορτωμένη, ξεκινάμε τη λειτουργία OCR. Η μέθοδος `Recognize` επιστρέφει ένα `OcrResult` που περιέχει το απλό κείμενο, τις βαθμολογίες εμπιστοσύνης και λεπτομέρειες χρονομέτρησης.

```csharp
        // Perform the OCR operation.
        OcrResult result = engine.Recognize();
```

**Διαχείριση ειδικών περιπτώσεων:**  
Αν το GPU δεν είναι διαθέσιμο, το `engine.Recognize()` λειτουργεί κανονικά επειδή η μηχανή αλλάζει σιωπηλά σε CPU. Μπορείτε να ελέγξετε το `engine.Device` μετά την αναγνώριση αν χρειάζεται να καταγράψετε ποια συσκευή χρησιμοποιήθηκε πραγματικά.

## Βήμα 4 – Ανάκτηση του αναγνωρισμένου απλού κειμένου

Η εξαγωγή του κειμένου είναι απλή—απλώς διαβάζετε την ιδιότητα `Text`. Εδώ τελικά **εξάγουμε κείμενο από tiff** (ή οποιαδήποτε άλλη εικόνα) και το παρουσιάζουμε στον χρήστη.

```csharp
        // Output the plain text that was extracted.
        Console.WriteLine($"Text:\n{result.Text}");
```

Θα δείτε τους ακατέργαστους χαρακτήρες, με τις αλλαγές γραμμής όπως εμφανίζονται στην πηγή εικόνας. Για πιο δομημένη έξοδο (π.χ. JSON ή CSV), μπορείτε να εξερευνήσετε τα `result.Regions` και `result.Lines`, αλλά το απλό κείμενο συνήθως αρκεί για γρήγορα σενάρια.

## Βήμα 5 – Μέτρηση χρόνου επεξεργασίας και διαχείριση εναλλακτικού GPU

Η απόδοση μετράει, ειδικά όταν επεξεργάζεστε δεκάδες σελίδες. Η ιδιότητα `ProcessingTime` σας λέει ακριβώς πόσο χρόνο πήρε το OCR, ανεξάρτητα από το αν εκτελέστηκε σε GPU ή CPU.

```csharp
        // Show how long the recognition took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Γιατί πρέπει να σας ενδιαφέρει:**  
Αν παρατηρήσετε ότι ο χρόνος αυξάνεται, ίσως θελήσετε να ρυθμίσετε το `GpuMemoryLimit` ή να μεταβείτε ρητά σε CPU (`Device = OcrDevice.Cpu`). Αντίστροφα, ένα αποτέλεσμα κάτω του δευτερολέπτου σε μεγάλη TIFF σημαίνει ότι η επιτάχυνση GPU κάνει τη δουλειά της.

## Πλήρες, Έτοιμο‑για‑Εκτέλεση Παράδειγμα

Αντιγράψτε τον παρακάτω κώδικα σε ένα νέο έργο console (`dotnet new console -n OcrDemo`) και εκτελέστε `dotnet add package Aspose.OCR`. Στη συνέχεια αντικαταστήστε το `YOUR_DIRECTORY/sample_multi_page.tif` με τη διαδρομή προς την εικόνα σας.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine with GPU preference.
        OcrEngine engine = new OcrEngine
        {
            Device = OcrDevice.Gpu,
            GpuMemoryLimit = 1024
        };

        // Step 2: Load image for OCR (supports TIFF, PNG, JPEG, etc.).
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/sample_multi_page.tif");

        // Step 3: Run recognition – this will also **extract text from tiff**.
        OcrResult result = engine.Recognize();

        // Step 4: Retrieve and display the recognized plain text.
        Console.WriteLine($"Text:\n{result.Text}");

        // Step 5: Display how long the operation took.
        Console.WriteLine($"Time elapsed: {result.ProcessingTime.TotalSeconds}s");
    }
}
```

**Αναμενόμενη έξοδος (κομμένη για συντομία):**

```
Text:
Invoice #12345
Date: 2026-05-01
Total: $1,250.00
...
Time elapsed: 1.42s
```

Αν ο υπολογιστής σας δεν διαθέτει ικανό GPU, ο χρόνος εκτέλεσης μπορεί να είναι μερικά δευτερόλεπτα μεγαλύτερος, αλλά το κείμενο θα εξαχθεί σωστά.

## Συχνές Ερωτήσεις & Παγίδες

- **Τι γίνεται αν η εικόνα είναι τεράστια (πάνω από 10 MB);**  
  Μειώστε την ανάλυση πριν τη δώσετε στη μηχανή, ή αυξήστε το `GpuMemoryLimit` αν έχετε αρκετή VRAM.  
- **Μπορώ να επεξεργαστώ πολλές εικόνες σε βρόχο;**  
  Φυσικά. Απλώς επαναχρησιμοποιήστε την ίδια παρουσία `OcrEngine` και ορίστε ένα νέο `ImageStream` σε κάθε επανάληψη.  
- **Πρέπει να απελευθερώσω κάτι;**  
  Η `OcrEngine` υλοποιεί το `IDisposable`. Τυλίξτε την σε ένα `using` block για καθαρό χειρισμό πόρων, ειδικά όταν χρησιμοποιείτε πόρους GPU.  

```csharp
using (OcrEngine engine = new OcrEngine { Device = OcrDevice.Gpu })
{
    // ... same steps as before
}
```

- **Τι γίνεται με γλώσσες εκτός των Αγγλικών;**  
  Ορίστε `engine.Language = OcrLanguage.Spanish` (ή οποιαδήποτε υποστηριζόμενη γλώσσα) πριν καλέσετε το `Recognize()`.  

## Συμπέρασμα

Τώρα έχετε μια πλήρη, ολοκληρωμένη λύση που **αναγνωρίζει κείμενο από εικόνα** σε C# χρησιμοποιώντας Aspose OCR. Ο οδηγός κάλυψε πώς να **φορτώσετε εικόνα για OCR**, πώς να **εξάγετε κείμενο από tiff**, και πώς να μετρήσετε την απόδοση ενώ διαχειρίζεστε ομαλά την εναλλακτική GPU.

Από εδώ μπορείτε:

- Να πειραματιστείτε με διαφορετικές μορφές εικόνας (BMP, PDF) για να δείτε πώς τις διαχειρίζεται το Aspose.  
- Να εμβαθύνετε στα `result.Regions` για δεδομένα περιορισμού εάν χρειάζεστε πληροφορίες διάταξης  

## Τι Θα Μάθετε Στη Στη συνέχεια;

- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract Text from Image – Recognize Line with Aspose.OCR](/ocr/english/net/image-and-drawing-recognition/recognize-line/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}