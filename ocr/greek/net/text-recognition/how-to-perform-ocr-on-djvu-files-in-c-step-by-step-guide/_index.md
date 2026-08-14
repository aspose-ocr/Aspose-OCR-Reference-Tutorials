---
category: general
date: 2026-02-20
description: Πώς να εκτελέσετε OCR σε αρχεία DjVu σε C#. Μάθετε να αναγνωρίζετε κείμενο
  από εικόνα και να μετατρέπετε DjVu σε κείμενο γρήγορα με το Aspose OCR.
draft: false
keywords:
- how to perform OCR
- recognize text from image
- how to read djvu
- extract text from image
- convert djvu to text
language: el
og_description: Πώς να εκτελέσετε OCR σε αρχεία DjVu με C#. Αυτό το σεμινάριο σας
  δείχνει πώς να αναγνωρίζετε κείμενο από εικόνα, να διαβάζετε DjVu και να μετατρέπετε
  DjVu σε κείμενο χρησιμοποιώντας το Aspose OCR.
og_title: Πώς να εκτελέσετε OCR σε αρχεία DjVu με C# – Πλήρης οδηγός
tags:
- OCR
- C#
- DjVu
- Aspose
title: Πώς να εκτελέσετε OCR σε αρχεία DjVu με C# – Οδηγός βήμα‑προς‑βήμα
url: /el/net/text-recognition/how-to-perform-ocr-on-djvu-files-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να Εκτελέσετε OCR σε Αρχεία DjVu με C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ **πώς να εκτελέσετε OCR** σε ένα έγγραφο DjVu χωρίς να τρελαίνεστε; Δεν είστε οι μόνοι. Πολλοί προγραμματιστές αντιμετωπίζουν δυσκολίες όταν πρέπει να **αναγνωρίσουν κείμενο από εικόνα** που βρίσκεται μέσα σε δοχεία DjVu. Τα καλά νέα; Με λίγες γραμμές C# και τη βιβλιοθήκη Aspose OCR, μπορείτε να εξάγετε αυτό το κρυφό κείμενο σε ελάχιστο χρόνο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από όλα όσα χρειάζεστε για να μετατρέψετε μια σελίδα DjVu σε απλό κείμενο. Στο τέλος θα ξέρετε **πώς να διαβάζετε DjVu**, πώς να **εξάγετε κείμενο από εικόνα**, και ακόμη πώς να **μετατρέψετε DjVu σε κείμενο** για επεξεργασία downstream. Χωρίς εξωτερικές υπηρεσίες, χωρίς ασαφείς αναφορές — μόνο ένα αυτόνομο, εκτελέσιμο παράδειγμα.

## Προαπαιτούμενα

Πριν ξεκινήσουμε, βεβαιωθείτε ότι έχετε τα εξής:

- .NET 6.0 SDK ή νεότερο (ο κώδικας λειτουργεί επίσης με .NET Framework 4.8).
- Visual Studio 2022 ή οποιονδήποτε επεξεργαστή που υποστηρίζει C#.
- Άδεια Aspose OCR for .NET (η δωρεάν δοκιμή λειτουργεί για δοκιμές).
- Ένα δείγμα αρχείου DjVu (`sample.djvu`) τοποθετημένο σε φάκελο που μπορείτε να αναφέρετε.

Η προετοιμασία αυτών θα διασφαλίσει ομαλή ροή — χωρίς εκπλήξεις «απουσία αναφοράς» αργότερα.

## Πώς να Εκτελέσετε OCR σε Σελίδα DjVu

Η βασική ιδέα είναι απλή: φορτώνετε τη σελίδα DjVu ως εικόνα, τη δίνετε στη μηχανή OCR και διαβάζετε το παραγόμενο string. Ας το αναλύσουμε βήμα‑βήμα.

### Βήμα 1: Εγκατάσταση Aspose OCR

Ανοίξτε ένα τερματικό στον φάκελο του έργου και εκτελέστε:

```bash
dotnet add package Aspose.OCR
```

Αυτό κατεβάζει τα πιο πρόσφατα binaries του Aspose OCR και τις εξαρτήσεις τους. Αν προτιμάτε το UI του NuGet Package Manager, απλώς ψάξτε για **Aspose.OCR** και κάντε κλικ στο **Install**.

### Βήμα 2: Αρχικοποίηση της Μηχανής OCR

Η δημιουργία ενός αντικειμένου `OcrEngine` είναι το πρώτο βήμα όταν θέλετε να **εκτελέσετε OCR**. Σκεφτείτε το ως ενεργοποίηση του «εγκεφάλου» του σαρωτή.

```csharp
using Aspose.OCR;

// ...

// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

> **Συμβουλή:** Η επαναχρησιμοποίηση ενός μόνο `OcrEngine` για πολλαπλές σελίδες εξοικονομεί μνήμη και επιταχύνει την επεξεργασία.

### Βήμα 3: Φόρτωση της Σελίδας DjVu ως Εικόνα

Τα αρχεία DjVu δεν υποστηρίζονται άμεσα από τις περισσότερες API εικόνας, αλλά το Aspose μπορεί να αντιμετωπίσει κάθε σελίδα ως bitmap. Εδώ χρησιμοποιούμε το `System.Drawing.Image` για να διαβάσουμε το αρχείο.

```csharp
using System.Drawing;

// ...

// Step 3: Load a DjVu page as an image
string djvuPath = @"C:\Path\To\Your\Directory\sample.djvu";
Image djvuPage = Image.FromFile(djvuPath);
```

> **Γιατί λειτουργεί:** Η `Image.FromFile` αποκωδικοποιεί αυτόματα τη ροή DjVu σε μορφή raster που καταλαβαίνει η μηχανή OCR. Αν χρειάζεται να επεξεργαστείτε μια συγκεκριμένη σελίδα από ένα πολυ‑σελιδικό DjVu, χρησιμοποιήστε το Aspose PDF ή το Aspose Imaging για να εξάγετε πρώτα τη σελίδα.

### Βήμα 4: Αναγνώριση Κειμένου από Εικόνα

Τώρα συμβαίνει η μαγεία. Η μέθοδος `Recognize` σαρώνει το bitmap και επιστρέφει ένα string που περιέχει τους ανιχνευμένους χαρακτήρες.

```csharp
// Step 4: Perform OCR to extract text from the image
string extractedText = ocrEngine.Recognize(djvuPage);
```

Σε αυτό το σημείο έχετε **αναγνωρίσει κείμενο από εικόνα** που αρχικά βρισκόταν μέσα σε ένα δοχείο DjVu. Το string μπορεί να περιέχει αλλαγές γραμμής, σημεία στίξης και ακόμη Unicode χαρακτήρες αν η γλώσσα προέλευσης τα υποστηρίζει.

### Βήμα 5: Εμφάνιση ή Αποθήκευση του Αποτελέσματος

Για έναν γρήγορο έλεγχο, απλώς εκτυπώστε το κείμενο στην κονσόλα. Σε μια πραγματική εφαρμογή, πιθανότατα θα το γράψετε σε αρχείο ή βάση δεδομένων.

```csharp
// Step 5: Display the recognized text
Console.WriteLine("=== Extracted Text ===");
Console.WriteLine(extractedText);
```

Συνδυάζοντας όλα τα παραπάνω, ιδού το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα.

```csharp
// File: DjvuOcrExample.cs
using System;
using System.Drawing;
using Aspose.OCR;

class DjvuExample
{
    static void Main()
    {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load a DjVu page as an image
        Image djvuPage = Image.FromFile(@"C:\Path\To\Your\Directory\sample.djvu");

        // Perform OCR to extract text from the image
        string extractedText = ocrEngine.Recognize(djvuPage);

        // Display the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

**Αναμενόμενο αποτέλεσμα** (κομμένο για συντομία):

```
=== Extracted Text ===
The quick brown fox jumps over the lazy dog.
Lorem ipsum dolor sit amet, consectetur...
```

Αν δείτε ακατανόητους χαρακτήρες, ελέγξτε ξανά ότι το αρχείο DjVu δεν είναι κρυπτογραφημένο και ότι έχετε ορίσει τη σωστή γλώσσα στο `ocrEngine.Language`. Από προεπιλογή υποθέτει Αγγλικά· μπορείτε να αλλάξετε σε Γαλλικά, Γερμανικά κ.λπ., ορίζοντας `ocrEngine.Language = Language.French;`.

## Αναγνώριση Κειμένου από Εικόνα – Συνηθισμένα Πιθανά Προβλήματα

Ακόμη και με ένα σταθερό παράδειγμα, οι προγραμματιστές συχνά συναντούν μερικές παγίδες:

| Πρόβλημα | Γιατί Συμβαίνει | Διόρθωση |
|----------|-----------------|----------|
| **Κενό αποτέλεσμα** | Η ανάλυση της εικόνας είναι πολύ χαμηλή (<300 dpi). | Χρησιμοποιήστε `ocrEngine.ImageResolution = 300;` πριν καλέσετε το `Recognize`. |
| **Λάθος γλώσσα** | Το OCR προεπιλογή είναι τα Αγγλικά. | Ορίστε `ocrEngine.Language = Language.Spanish;` (ή οποιαδήποτε υποστηριζόμενη γλώσσα). |
| **Διαρροή μνήμης** | Μεγάλες σελίδες DjVu παραμένουν στη μνήμη μετά την επεξεργασία. | Καλέστε `djvuPage.Dispose();` όταν τελειώσετε. |
| **Πολυ‑σελιδικό DjVu** | Φορτώνεται μόνο η πρώτη σελίδα. | Επαναλάβετε τη λούπα στις σελίδες χρησιμοποιώντας την κλάση `DjvuImage` του Aspose Imaging. |

Η αντιμετώπιση αυτών νωρίς εξοικονομεί αμέτρητες ώρες εντοπισμού σφαλμάτων.

## Πώς να Διαβάσετε Αρχεία DjVu με C# – Πέρα από το Απλό OCR

Αν το έργο σας απαιτεί περισσότερες από μία σελίδες, θα χρειαστεί να εξάγετε κάθε σελίδα ως εικόνα πρώτα. Το Aspose Imaging το κάνει εύκολο:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;

// ...

string djvuPath = @"sample.djvu";
using (DjvuImage djvu = (DjvuImage)Image.Load(djvuPath))
{
    for (int i = 0; i < djvu.Frames.Count; i++)
    {
        using (Image page = djvu.Frames[i].ConvertToRaster())
        {
            // Run OCR on each page
            string pageText = ocrEngine.Recognize(page);
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(pageText);
        }
    }
}
```

Αυτό το μοτίβο σας επιτρέπει να **μετατρέψετε DjVu σε κείμενο** σελίδα‑με‑σελίδα, ιδανικό για μαζική επεξεργασία μεγάλων αρχείων.

## Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση Ακρίβειας

Οι προεπιλεγμένες ρυθμίσεις OCR λειτουργούν καλά για καθαρές σάρωση, αλλά μπορείτε να αυξήσετε την ακρίβεια:

```csharp
ocrEngine.ImagePreprocessingOptions = new ImagePreprocessingOptions()
{
    // Binarize the image to improve contrast
    BinarizationMethod = BinarizationMethod.Otsu,
    // Deskew the image if it’s tilted
    Deskew = true,
    // Remove noise
    NoiseRemoval = true
};
```

Αυτές οι ρυθμίσεις είναι ιδιαίτερα χρήσιμες όταν η πηγή DjVu περιέχει χειρόγραφες σημειώσεις ή γραφικά χαμηλής αντίθεσης.

## Μετατροπή DjVu σε Κείμενο – Πλήρες Παράδειγμα End‑to‑End

Παρακάτω υπάρχει μια συμπαγής έκδοση που ενώνει τα πάντα: φόρτωση πολυ‑σελιδικού DjVu, προεπεξεργασία κάθε σελίδας, εκτέλεση OCR και αποθήκευση του αποτελέσματος σε αρχείο `.txt`.

```csharp
using System;
using System.IO;
using Aspose.Imaging;
using Aspose.Imaging.FileFormats.Djvu;
using Aspose.OCR;
using Aspose.OCR.Models;

class DjvuToTextConverter
{
    static void Main()
    {
        // Prepare OCR engine with preprocessing
        OcrEngine ocr = new OcrEngine
        {
            ImagePreprocessingOptions = new ImagePreprocessingOptions()
            {
                BinarizationMethod = BinarizationMethod.Otsu,
                Deskew = true,
                NoiseRemoval = true
            }
        };

        string inputPath = @"C:\Docs\sample.djvu";
        string outputPath = @"C:\Docs\sample_extracted.txt";

        using (DjvuImage djvu = (DjvuImage)Image.Load(inputPath))
        using (StreamWriter writer = new StreamWriter(outputPath))
        {
            for (int i = 0; i < djvu.Frames.Count; i++)
            {
                using (var page = djvu.Frames[i].ConvertToRaster())
                {
                    string text = ocr.Recognize(page);
                    writer.WriteLine($"--- Page {i + 1} ---");
                    writer.WriteLine(text);
                }
            }
        }

        Console.WriteLine($"Extraction complete. Text saved to {outputPath}");
    }
}
```

Η εκτέλεση αυτού του script δημιουργεί το `sample_extracted.txt` με το περιεχόμενο κάθε σελίδας χωρισμένο καθαρά. Είναι ο πιο γρήγορος τρόπος για **να μετατρέψετε DjVu σε κείμενο** για ευρετηρίαση, αναζήτηση ή αρχειοθέτηση.

## Συμπέρασμα

Καλύψαμε **πώς να εκτελέσετε OCR** σε αρχεία DjVu από την αρχή μέχρι το τέλος, εξερευνήσαμε τρόπους **να αναγνωρίσετε κείμενο από

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}