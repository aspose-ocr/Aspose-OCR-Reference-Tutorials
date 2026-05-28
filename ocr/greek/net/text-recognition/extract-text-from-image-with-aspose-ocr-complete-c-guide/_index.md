---
category: general
date: 2026-05-28
description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας Aspose OCR σε C#. Μάθετε
  πώς να εξάγετε κείμενο OCR, να φορτώνετε εικόνα για OCR και να αναγνωρίζετε κείμενο
  από αρχεία TIF γρήγορα.
draft: false
keywords:
- extract text from image
- how to extract ocr text
- load image for ocr
- recognize text from tif
language: el
og_description: Εξαγωγή κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Αυτό
  το σεμινάριο δείχνει πώς να εξάγετε κείμενο OCR, να φορτώσετε εικόνα για OCR και
  να αναγνωρίσετε κείμενο από αρχεία TIF.
og_title: Εξαγωγή κειμένου από εικόνα με το Aspose OCR – Πλήρης οδηγός C#
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  headline: Extract Text from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract text from image using Aspose OCR in C#. Learn how to extract
    OCR text, load image for OCR, and recognize text from TIF files quickly.
  name: Extract Text from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
    text: '**Wrong file path** – A typo leads to a `FileNotFoundException`. Double‑check
      the path or use `Path.Combine` for cross‑platform safety.'
  - name: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
    text: '**Unsupported format** – Aspose OCR supports PNG, JPEG, BMP, and TIFF.
      Trying a PDF directly will throw an `UnsupportedFormatException`. Convert first
      if needed.'
  - name: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
    text: '**Large image size** – Very high‑resolution TIFFs can consume memory. Consider
      down‑scaling with `engine.Options.Dpi = 300` before recognition.'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Εξαγωγή κειμένου από εικόνα με Aspose OCR – Πλήρης οδηγός C#
url: /el/net/text-recognition/extract-text-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Απόσπαση Κειμένου από Εικόνα με Aspose OCR – Πλήρης Οδηγός C# 

Η απόσπαση κειμένου από εικόνα είναι ένα κοινό εμπόδιο όταν χρειάζεται να ψηφιοποιήσετε σαρωμένα έγγραφα, αποδείξεις ή ακόμη και μια φωτογραφία από λευκό πίνακα. Αν αναρωτιέστε **πώς να εξάγετε κείμενο OCR** σε ένα .NET project, βρίσκεστε στο σωστό σημείο—αυτός ο οδηγός σας καθοδηγεί μέσα από όλη τη διαδικασία, από τη φόρτωση της εικόνας μέχρι την εξαγωγή των αναγνωρισμένων χαρακτήρων από ένα αρχείο TIF.  

Θα καλύψουμε όλα όσα χρειάζεστε: τη δημιουργία της μηχανής OCR, τη φόρτωση της εικόνας για OCR, την εκτέλεση ασύγχρονης αναγνώρισης και τέλος την εκτύπωση του εξαγόμενου κειμένου στην κονσόλα. Στο τέλος θα έχετε ένα εκτελέσιμο απόσπασμα που λειτουργεί με οποιοδήποτε TIFF (ή άλλες υποστηριζόμενες μορφές) και μια σαφή κατανόηση του γιατί κάθε μέρος είναι σημαντικό.  

## Τι Θα Χρειαστεί

- .NET 6 ή νεότερο (ο κώδικας επίσης μεταγλωττίζεται σε .NET Core 3.1+)
- Ένα πακέτο NuGet Aspose.OCR (`Aspose.OCR`) εγκατεστημένο στο project σας
- Μια δείγμα TIFF εικόνα (`page1.tif`) τοποθετημένη κάπου που μπορείτε να την αναφέρετε
- Ένας επεξεργαστής κώδικα ή IDE (Visual Studio, VS Code, Rider—ό,τι προτιμάτε)

Χωρίς επιπλέον αρχεία ρυθμίσεων, χωρίς βαριές μηχανές OCR για τοπική εγκατάσταση—η Aspose αναλαμβάνει τη βαριά δουλειά για εσάς.  

## Απόσπαση Κειμένου από Εικόνα – Βήμα 1: Αρχικοποίηση της Μηχανής OCR

Πριν επεξεργαστεί οποιαδήποτε εικόνα, χρειάζεστε μια παρουσία του `OcrEngine`. Σκεφτείτε τη μηχανή ως τον εγκέφαλο που ξέρει πώς να διαβάζει χαρακτήρες· χωρίς αυτήν, το υπόλοιπο pipeline δεν έχει τίποτα να τροφοδοτήσει.  

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Step 1: Create an OCR engine instance
        var engine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:** Το `OcrEngine` ενσωματώνει τους αλγόριθμους αναγνώρισης και τα πακέτα γλώσσας. Η δημιουργία του μία φορά ανά λειτουργία διατηρεί τη χρήση μνήμης χαμηλή και σας παρέχει ένα καθαρό σημείο για να ρυθμίσετε τις ρυθμίσεις αργότερα (π.χ., γλώσσα, DPI).  

## Πώς να Εξάγετε Κείμενο OCR – Βήμα 2: Φόρτωση Εικόνας για OCR

Τώρα που η μηχανή είναι έτοιμη, πρέπει να την κατευθύνουμε προς την εικόνα που θέλουμε να διαβάσουμε. Η Aspose παρέχει το `ImageStream.FromFile`, το οποίο μεταδίδει το αρχείο χωρίς να φορτώνει ολόκληρο το bitmap στη μνήμη—ένα ωραίο κέρδος στην απόδοση για μεγάλα TIFF.  

```csharp
        // Step 2: Load the image to be recognized
        engine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/page1.tif");
```

> **Συμβουλή:** Αντικαταστήστε το `YOUR_DIRECTORY` με την απόλυτη ή σχετική διαδρομή προς την εικόνα σας. Αν εκτελείτε την εφαρμογή από το φάκελο του project, το `@"./page1.tif"` λειτουργεί καλά.  
> **Περίπτωση άκρης:** Τα αρχεία TIFF μπορούν να περιέχουν πολλαπλές σελίδες. Το `ImageStream.FromFile` διαβάζει την πρώτη σελίδα εξ ορισμού· αν χρειάζεστε διαφορετική σελίδα, χρησιμοποιήστε `ImageStream.FromFile(path, pageNumber)`.  

## Αναγνώριση Κειμένου από TIF – Βήμα 3: Εκτέλεση Ασύγχρονης OCR

Το μπλοκάρισμα του νήματος που καλεί ενώ η μηχανή OCR λειτουργεί μπορεί να παγώσει τις UI εφαρμογές ή να σπαταλήσει πόρους του διακομιστή. Η χρήση του `RecognizeAsync` επιτρέπει στην λειτουργία να τρέξει στο παρασκήνιο, επιστρέφοντας ένα `Task<string>` που λύνει το εξαγόμενο κείμενο.  

```csharp
        // Step 3: Perform OCR asynchronously (does not block the calling thread)
        string extractedText = await engine.RecognizeAsync();
```

> **Γιατί async;** Σε ένα web API ή desktop εφαρμογή, θέλετε η ομάδα νήματος να παραμένει ανταποκρινόμενη. Το `await` επιστρέφει τον έλεγχο στον καλούντα μέχρι να ολοκληρωθεί η OCR, διατηρώντας το UI ομαλό ή το νήμα της αίτησης ελεύθερο για άλλη εργασία.  

## Έξοδος του Εξαγόμενου Κειμένου – Βήμα 4: Εκτύπωση ή Αποθήκευση

Τέλος, απλώς γράφουμε το αποτέλεσμα στην κονσόλα. Σε πραγματικές περιπτώσεις μπορεί να γράψετε σε μια βάση δεδομένων, σε αρχείο ή να περάσετε τη συμβολοσειρά σε άλλη υπηρεσία.  

```csharp
        // Step 4: Output the recognized text
        Console.WriteLine(extractedText);
    }
}
```

### Αναμενόμενη Έξοδος

Αν το `page1.tif` περιέχει το κείμενο *«Hello, Aspose OCR!»*, η κονσόλα θα εμφανίσει:  

```
Hello, Aspose OCR!
```

Αν η εικόνα είναι θορυβώδης, μπορεί να δείτε επιπλέον αλλαγές γραμμής ή λανθασμένους χαρακτήρες—ρυθμίστε τις `Options` της μηχανής (π.χ., `engine.Options.DetectLanguage = true`) για να βελτιώσετε την ακρίβεια.  

## Συνηθισμένα Πιθανά Σφάλματα Κατά τη Φόρτωση Εικόνας για OCR

1. **Λάθος διαδρομή αρχείου** – Ένα τυπογραφικό λάθος οδηγεί σε `FileNotFoundException`. Ελέγξτε ξανά τη διαδρομή ή χρησιμοποιήστε `Path.Combine` για ασφάλεια μεταξύ πλατφορμών.  
2. **Μη υποστηριζόμενη μορφή** – Η Aspose OCR υποστηρίζει PNG, JPEG, BMP και TIFF. Η άμεση προσπάθεια με PDF θα προκαλέσει `UnsupportedFormatException`. Μετατρέψτε πρώτα αν χρειάζεται.  
3. **Μεγάλο μέγεθος εικόνας** – Πολύ υψηλής ανάλυσης TIFFs μπορεί να καταναλώσουν μνήμη. Σκεφτείτε τη μείωση κλίμακας με `engine.Options.Dpi = 300` πριν την αναγνώριση.  

## Προχωρώντας Περαιτέρω: Ρύθμιση Παραμέτρων Αναγνώρισης

Η Aspose.OCR παρέχει μια σειρά από επιλογές που μπορείτε να ρυθμίσετε:  

```csharp
engine.Options.Language = Language.English;      // Force English if you know the language
engine.Options.Dpi = 200;                       // Reduce DPI for faster processing
engine.Options.IsAutoRotate = true;            // Auto‑rotate skewed pages
```

Δοκιμάστε τα για να βρείτε την ισορροπία μεταξύ ταχύτητας και ακρίβειας.  

## Πλήρες, Εκτελέσιμο Παράδειγμα (Έτοιμο για Αντιγραφή‑Επικόλληση)

Παρακάτω είναι το πλήρες πρόγραμμα που μπορείτε να ενσωματώσετε σε ένα νέο console project. Περιλαμβάνει τις προαιρετικές ρυθμίσεις που συζητήθηκαν παραπάνω.  

```csharp
using System;
using System.Threading.Tasks;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static async Task Main()
    {
        // Create the OCR engine
        var engine = new OcrEngine();

        // Optional: fine‑tune recognition
        engine.Options.Language = Language.English;
        engine.Options.Dpi = 200;
        engine.Options.IsAutoRotate = true;

        // Load the image (replace with your actual path)
        engine.Image = ImageStream.FromFile(@"./page1.tif");

        // Run OCR asynchronously
        string extractedText = await engine.RecognizeAsync();

        // Show the result
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

Αποθηκεύστε το αρχείο ως `Program.cs`, τρέξτε `dotnet add package Aspose.OCR`, μετά `dotnet run`. Θα πρέπει να δείτε το εξαγόμενο κείμενο να εκτυπώνεται στην κονσόλα.  

## Ανακεφαλαίωση

Μόλις δείξαμε **πώς να εξάγετε κείμενο OCR** από μια εικόνα TIFF χρησιμοποιώντας Aspose OCR σε C#. Τα βήματα—αρχικοποίηση της μηχανής, φόρτωση της εικόνας για OCR, αναγνώριση κειμένου από TIF ασύγχρονα, και έξοδος του αποτελέσματος—καλύπτουν ολόκληρο τον κύκλο ζωής της εξαγωγής κειμένου από αρχεία εικόνας.  

Αν είστε έτοιμοι να προχωρήσετε πέρα από το απλό κείμενο, εξερευνήστε το `PdfConverter` της Aspose για να ενσωματώσετε το αποτέλεσμα OCR σε αναζητήσιμα PDF, ή χρησιμοποιήστε `engine.Options` για να διαχειριστείτε έγγραφα πολλαπλών γλωσσών.  

## Τι Ακολουθεί;

- **Επεξεργασία παρτίδας:** Επανάληψη σε φάκελο με TIFFs και αποθήκευση κάθε αποτελέσματος σε βάση δεδομένων.  
- **Προεπεξεργασία εικόνας:** Χρησιμοποιήστε `System.Drawing` ή `ImageSharp` για να καθαρίσετε θορυβώδεις σάρωση πριν τα δώσετε στη μηχανή OCR.  
- **Ενσωμάτωση με ASP.NET Core:** Εκθέστε ένα endpoint που δέχεται μια ανεβασμένη εικόνα και επιστρέφει το αναγνωρισμένο κείμενο ως JSON.  

Νιώστε ελεύθεροι να πειραματιστείτε, να σπάσετε πράγματα, και μετά να επιστρέψετε σε αυτόν τον οδηγό για ανανέωση. Αν αντιμετωπίσετε προβλήματα, η τεκμηρίωση Aspose OCR είναι ένας αξιόπιστος σύντροφος, αλλά το βασικό μοτίβο παραμένει το ίδιο: **απόσπαση κειμένου από εικόνα**, **φόρτωση εικόνας για OCR**, **αναγνώριση κειμένου από TIF**, και διαχείριση του αποτελέσματος.  

Καλό κώδικα, και εύχομαι οι εικόνες σας πάντα να είναι κρυστάλλινα καθαρές!  

## Σχετικά Μαθήματα

- [Εξαγωγή κειμένου εικόνας C# με επιλογή γλώσσας χρησιμοποιώντας Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Εξαγωγή Κειμένου από Εικόνα – Βελτιστοποίηση OCR με Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/)
- [Πώς να Εξάγετε Κείμενο από Εικόνα Προετοιμάζοντας Ορθογώνια στην OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}