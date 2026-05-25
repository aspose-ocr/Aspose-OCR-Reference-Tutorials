---
category: general
date: 2026-05-25
description: Προεπεξεργασία εικόνας για OCR με το Aspose ώστε να βελτιώσετε την ακρίβεια
  του OCR και εκτέλεση OCR σε αρχεία JPEG. Μάθετε πώς να εξάγετε κείμενο χρησιμοποιώντας
  το Aspose σε έναν σαφή, βήμα‑βήμα οδηγό.
draft: false
keywords:
- preprocess image for OCR
- improve OCR accuracy
- run OCR on JPEG
- extract text using Aspose
language: el
og_description: Προεπεξεργασία εικόνας για OCR με το Aspose για βελτίωση της ακρίβειας
  του OCR. Ακολουθήστε αυτόν τον οδηγό για να εκτελέσετε OCR σε JPEG και να εξάγετε
  κείμενο χρησιμοποιώντας το Aspose σε C#.
og_title: Προεπεξεργασία εικόνας για OCR – Οδηγός Aspose C#
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Preprocess image for OCR with Aspose to improve OCR accuracy and run
    OCR on JPEG files. Learn how to extract text using Aspose in a clear, step‑by‑step
    tutorial.
  headline: Preprocess Image for OCR – Complete Aspose C# Guide
  type: TechArticle
- description: Preprocess image for OCR with Aspose to improve OCR accuracy and run
    OCR on JPEG files. Learn how to extract text using Aspose in a clear, step‑by‑step
    tutorial.
  name: Preprocess Image for OCR – Complete Aspose C# Guide
  steps:
  - name: '**Deskew** – straightens tilted documents (max 5° by default).'
    text: '**Deskew** – straightens tilted documents (max 5° by default).'
  - name: '**Denoise** – smooths out grainy backgrounds.'
    text: '**Denoise** – smooths out grainy backgrounds.'
  - name: '**Binarize** – converts the image to black‑and‑white using a threshold.'
    text: '**Binarize** – converts the image to black‑and‑white using a threshold.'
  - name: '**ContrastBoost** – makes faint characters pop.'
    text: '**ContrastBoost** – makes faint characters pop.'
  type: HowTo
tags:
- OCR
- Aspose
- C#
- Image Processing
title: Προεπεξεργασία εικόνας για OCR – Πλήρης οδηγός Aspose C#
url: /el/net/ocr-optimization/preprocess-image-for-ocr-complete-aspose-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR – Πλήρης Οδηγός Aspose C#

Έχετε αναρωτηθεί ποτέ πώς να **προεπεξεργαστείτε εικόνα για OCR** ώστε το κείμενο να βγαίνει καθαρό κάθε φορά; Δεν είστε μόνοι—οι προγραμματιστές αντιμετωπίζουν συνεχώς θορυβώδεις σκαναρίσματα, JPEG με χαμηλή αντίθεση και απρόβλεπτο φωτισμό. Το καλό νέο; Με μερικές έξυπνες ρυθμίσεις μπορείτε να **βελτιώσετε την ακρίβεια του OCR** δραματικά, και το Aspose το κάνει εύκολο.

Σε αυτό το tutorial θα περάσουμε από ένα πραγματικό παράδειγμα που δείχνει πώς να **τρέξετε OCR σε JPEG** εικόνες, να εφαρμόσετε μια προσαρμοσμένη αλυσίδα επεξεργασίας εικόνας και τελικά να **εξάγετε κείμενο χρησιμοποιώντας το Aspose**. Στο τέλος θα έχετε ένα έτοιμο κομμάτι κώδικα C# που μπορείτε να ενσωματώσετε σε οποιοδήποτε .NET project.

## Τι Θα Μάθετε

- Γιατί η προεπεξεργασία είναι σημαντική και ποια φίλτρα προσφέρουν τη μεγαλύτερη βελτίωση.
- Πώς να ρυθμίσετε το `ImageProcessingOptions` του Aspose.OCR για διόρθωση κλίσης, αποθορυβοποίηση, δυαδικοποίηση και ενίσχυση αντίθεσης.
- Τον ακριβή κώδικα που χρειάζεται για **να τρέξετε OCR σε JPEG** αρχεία και να λάβετε καθαρό κείμενο.
- Συμβουλές και παγίδες που κρατούν την αλυσίδα OCR σας αξιόπιστη σε παραγωγή.

Δεν απαιτείται προηγούμενη εμπειρία με το Aspose· αρκεί μια βασική γνώση C# και Visual Studio (ή το αγαπημένο σας IDE). Ας ξεκινήσουμε.

![Παράδειγμα προεπεξεργασίας εικόνας για OCR](preprocess-ocr.png "Προεπεξεργασία εικόνας για OCR")

## Βήμα 1: Ρύθμιση του Μηχανήματος Aspose.OCR – Προεπεξεργασία Εικόνας για OCR

Πρώτα απ’ όλα. Χρειαζόμαστε μια παρουσία `OcrEngine` και πρέπει να της πούμε ποια γλώσσα περιμένουμε. Στις περισσότερες περιπτώσεις η προεπιλογή είναι τα Αγγλικά, αλλά μπορείτε να την αλλάξετε σε Γαλλικά, Γερμανικά κ.λπ., τροποποιώντας το enum `OcrLanguage`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

// Initialize the OCR engine – this is where we’ll later plug in our preprocessing pipeline
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

**Γιατί είναι σημαντικό:** Η μηχανή είναι η καρδιά της λειτουργίας· χωρίς αυτή δεν μπορείτε να εφαρμόσετε κανένα από τα φίλτρα εικόνας που στην πραγματικότητα **προεπεξεργάζονται την εικόνα για OCR**. Σκεφτείτε τη σαν την κουζίνα όπου αναμιγνύονται όλα τα υλικά.

## Βήμα 2: Δημιουργία Προσαρμοσμένης Αλυσίδας Επεξεργασίας Εικόνας – Βελτίωση Ακρίβειας OCR

Τώρα έρχεται το νόστιμο μέρος. Το Aspose σας επιτρέπει να συνδέσετε πολλά φίλτρα μαζί. Παρακάτω ενεργοποιούμε τέσσερα από τα πιο αποτελεσματικά:

1. **Deskew** – ευθυγραμμίζει κεκλιμένα έγγραφα (μέγιστη κλίση 5° εξ ορισμού).
2. **Denoise** – εξομαλύνει θορυβώδεις φόντους.
3. **Binarize** – μετατρέπει την εικόνα σε ασπρόμαυρη χρησιμοποιώντας ένα κατώφλι.
4. **ContrastBoost** – κάνει τους αδύναμους χαρακτήρες πιο εμφανείς.

```csharp
// Attach a preprocessing pipeline to the engine
ocrEngine.ImageProcessingOptions = new ImageProcessingOptions
{
    Deskew = new DeskewOptions { Enabled = true, MaxAngle = 5.0 },
    Denoise = new DenoiseOptions { Enabled = true, Strength = 0.7 },
    Binarize = new BinarizeOptions { Enabled = true, Threshold = 120 },
    ContrastBoost = new ContrastBoostOptions { Enabled = true, Level = 1.3 }
};
```

**Pro tip:** Αν οι πηγές σας είναι ήδη καθαρές, μπορείτε να μειώσετε το `Strength` ή να απενεργοποιήσετε εντελώς ένα φίλτρο. Η υπερβολική επεξεργασία μπορεί μερικές φορές να σβήσει αδύναμους χαρακτήρες, οπότε πειραματιστείτε με πραγματικά δείγματα.

## Βήμα 3: Φόρτωση του JPEG (ή Οποιασδήποτε Εικόνας) και Εκτέλεση OCR – Εκτέλεση OCR σε JPEG

Το Aspose υποστηρίζει οποιαδήποτε μορφή εικόνας μπορεί να διαβάσει το .NET—JPEG, PNG, BMP, ό,τι θέλετε. Ακολουθεί ο τρόπος με τον οποίο τροφοδοτείτε ένα αρχείο JPEG στη μηχανή και ξεκινάτε τη διαδικασία αναγνώρισης.

```csharp
// Load the source image (replace the path with your actual file)
string imagePath = @"C:\Images\noisy_form.jpg";
var sourceImage = Image.FromFile(imagePath);

// Perform OCR – the heavy lifting happens after our preprocessing pipeline runs
string extractedText = ocrEngine.Recognize(sourceImage);
```

**Γιατί JPEG;** Η συμπίεση JPEG συχνά εισάγει τεχνουργήματα που μπερδεύουν το OCR. Η αλυσίδα προεπεξεργασίας μας, ειδικά τα βήματα αποθορυβοποίησης και δυαδικοποίησης, μετριάζουν αυτά τα προβλήματα, επιτρέποντάς σας να **τρέξετε OCR σε JPEG** με σιγουριά.

## Βήμα 4: Έξοδος του Αναγνωρισμένου Κειμένου – Εξαγωγή Κειμένου Χρησιμοποιώντας το Aspose

Τέλος, απλώς γράφουμε το κείμενο στην κονσόλα, σε αρχείο ή σε οποιαδήποτε downstream υπηρεσία. Για επίδειξη, η κονσόλα είναι αρκετή.

```csharp
// Show the result – you can also write to a file or database
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

Όταν τρέξετε το πρόγραμμα, θα δείτε κάτι σαν:

```
=== Extracted Text ===
John Doe
Invoice #12345
Total: $1,250.00
...
```

Αν η έξοδος φαίνεται ακατάστατη, επιστρέψτε στο **Βήμα 2** και προσαρμόστε τις ρυθμίσεις των φίλτρων. Μικρές προσαρμογές συχνά αποδίδουν μεγάλες βελτιώσεις στην **βελτίωση της ακρίβειας OCR**.

## Συνηθισμένες Ακραίες Περιπτώσεις και Πώς να τις Διαχειριστείτε

| Κατάσταση | Προτεινόμενη Προσαρμογή |
|-----------|------------------------|
| **Πολύ σκοτεινές εικόνες** | Αυξήστε το `ContrastBoost.Level` σε 1.5 ή περισσότερο. |
| **Κλίση > 5°** | Αυξήστε το `DeskewOptions.MaxAngle` (π.χ., 10.0) ή προ-γυρίστε την εικόνα χειροκίνητα. |
| **Χρωματικό κείμενο σε χρωματικό φόντο** | Χρησιμοποιήστε `BinarizeOptions` με προσαρμοσμένο κατώφλι ή μεταβείτε σε `AdaptiveBinarizeOptions`. |
| **Μεγάλα αρχεία ( > 5 MB )** | Φορτώστε την εικόνα σε `MemoryStream` πρώτα για να αποφύγετε προβλήματα κλειδώματος αρχείου. |

Αυτές οι ρυθμίσεις κρατούν την αλυσίδα σας ευέλικτη και έτοιμη για το μέλλον, ειδικά όταν χρειάζεται να **εξάγετε κείμενο χρησιμοποιώντας το Aspose** από διαφορετικές πηγές.

## Πλήρες Παράδειγμα – Όλα τα Βήματα σε Ένα Σημείο

Παρακάτω βρίσκεται το πλήρες, έτοιμο για αντιγραφή‑και‑επικόλληση πρόγραμμα. Συμβαδίζει με .NET 6+ και απαιτεί μόνο το πακέτο NuGet `Aspose.OCR`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Drawing; // For Image

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English,
            ImageProcessingOptions = new ImageProcessingOptions
            {
                // 2️⃣ Preprocess image for OCR
                Deskew = new DeskewOptions { Enabled = true, MaxAngle = 5.0 },
                Denoise = new DenoiseOptions { Enabled = true, Strength = 0.7 },
                Binarize = new BinarizeOptions { Enabled = true, Threshold = 120 },
                ContrastBoost = new ContrastBoostOptions { Enabled = true, Level = 1.3 }
            }
        };

        // 3️⃣ Load JPEG and run OCR
        string path = @"YOUR_DIRECTORY/noisy_form.jpg"; // ← change this
        using var img = Image.FromFile(path);
        string text = ocrEngine.Recognize(img);

        // 4️⃣ Output – extract text using Aspose
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(text);
    }
}
```

Αποθηκεύστε το ως `Program.cs`, προσθέστε το πακέτο Aspose.OCR (`dotnet add package Aspose.OCR`) και τρέξτε `dotnet run`. Θα δείτε το καθαρισμένο κείμενο να εμφανίζεται στην κονσόλα.

## Ανακεφαλαίωση – Γιατί Λειτουργεί Αυτή η Προσέγγιση

- **Προεπεξεργασία εικόνας για OCR**: Η αλυσίδα αφαιρεί τις πιο κοινές πηγές σφάλματος (κλίση, θόρυβος, χαμηλή αντίθεση).
- **Βελτίωση ακρίβειας OCR**: Κάθε φίλτρο ρυθμίζεται ώστε να αυξάνει το σήμα‑προς‑θόρυβο που βλέπει η μηχανή.
- **Εκτέλεση OCR σε JPEG**: Ακόμη και οι συμπιεσμένες εικόνες γίνονται αναγνώσιμες μετά τη διόρθωση κλίσης και τη δυαδικοποίηση.
- **Εξαγωγή κειμένου χρησιμοποιώντας το Aspose**: Η μέθοδος `Recognize` επιστρέφει μια απλή συμβολοσειρά, έτοιμη για οποιαδήποτε downstream λογική.

Συνδυαστικά, αυτά τα βήματα σας παρέχουν μια αξιόπιστη, παραγωγική λύση OCR με λίγες μόνο γραμμές κώδικα.

## Επόμενα Βήματα και Σχετικά Θέματα

- **Batch processing** – Επανάληψη πάνω σε φάκελο εικόνων και αποθήκευση κάθε αποτελέσματος σε αρχείο `.txt`.
- **Language packs** – Αντικαταστήστε το `OcrLanguage.English` με `OcrLanguage.Spanish` ή προσθέστε προσαρμοσμένα λεξικά.
- **PDF extraction** – Συνδυάστε Aspose.OCR με Aspose.PDF για άμεση εξαγωγή κειμένου από σαρωμένα PDF.
- **Performance tuning** – Εκτελέστε τη μηχανή παράλληλα με `Parallel.ForEach` για μεγάλα φορτία εργασίας.

Μη διστάσετε να πειραματιστείτε με τις τιμές των φίλτρων, να δοκιμάσετε διαφορετικές μορφές εικόνας ή να προσθέσετε επιπλέον φίλτρα Aspose όπως `SharpnessOptions`. Ο ουρανός είναι το όριο μόλις κυριαρχήσετε τα βασικά.

---

*Καλό κώδικα! Αν αντιμετωπίσετε προβλήματα, αφήστε ένα σχόλιο παρακάτω και θα τα λύσουμε μαζί.*

## Σχετικά Tutorials

- [Preprocess Image OCR with Aspose.OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}