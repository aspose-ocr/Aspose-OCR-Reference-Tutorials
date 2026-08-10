---
category: general
date: 2026-06-16
description: Προεπεξεργασία εικόνας για OCR χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να βελτιώσετε την αντίθεση της εικόνας και να αφαιρέσετε τον θόρυβο από τη σαρωμένη
  εικόνα για ακριβή εξαγωγή κειμένου.
draft: false
keywords:
- preprocess image for OCR
- enhance image contrast
- remove noise from scanned image
language: el
og_description: Προεπεξεργασία εικόνας για OCR με το Aspose OCR. Βελτιώστε την ακρίβεια
  ενισχύοντας την αντίθεση της εικόνας και αφαιρώντας τον θόρυβο από τη σαρωμένη εικόνα.
og_title: Προεπεξεργασία εικόνας για OCR σε C# – Πλήρης οδηγός
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  headline: Preprocess Image for OCR in C# – Complete Guide
  type: TechArticle
- description: Preprocess image for OCR using Aspose OCR in C#. Learn to enhance image
    contrast and remove noise from scanned image for accurate text extraction.
  name: Preprocess Image for OCR in C# – Complete Guide
  steps:
  - name: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
    text: '**Heavy Salt‑and‑Pepper Noise** – Increase the aggressiveness of `DenoiseFilter`
      by passing a custom `DenoiseOptions` object (e.g., `new DenoiseFilter(new DenoiseOptions
      { Strength = 2 })`).'
  - name: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
    text: '**Faded Ink on Yellow Paper** – Pair `ContrastEnhanceFilter` with a `BrightnessAdjustFilter`
      to lift the background tone before boosting contrast.'
  - name: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
    text: '**Colored Text** – Convert the image to grayscale first (`new GrayscaleFilter()`)
      because most OCR engines, including Aspose, work best on single‑channel data.'
  - name: '**Build** the console project (`dotnet build`).'
    text: '**Build** the console project (`dotnet build`).'
  - name: '**Run** (`dotnet run`). You should see something like:'
    text: '**Run** (`dotnet run`). You should see something like:'
  type: HowTo
tags:
- OCR
- C#
- Image Processing
title: Προεπεξεργασία εικόνας για OCR σε C# – Πλήρης οδηγός
url: /el/net/ocr-optimization/preprocess-image-for-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Προεπεξεργασία Εικόνας για OCR σε C# – Πλήρης Οδηγός

Έχετε αναρωτηθεί ποτέ γιατί τα αποτελέσματα του OCR σας μοιάζουν με ακατάστατο μπερδεμένο κείμενο παρόλο που η πηγή φωτογραφίας είναι σχετικά καθαρή; Η αλήθεια είναι ότι οι περισσότεροι κινητήρες OCR — συμπεριλαμβανομένου του Aspose OCR — αναμένουν μια καθαρή, καλά ευθυγραμμισμένη εικόνα. **Preprocess image for OCR** είναι το πρώτο βήμα για να μετατρέψετε μια τρεμάμενη, χαμηλής αντίθεσης σάρωση σε καθαρό, μηχανικά αναγνώσιμο κείμενο.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα πρακτικό, ολοκληρωμένο παράδειγμα που όχι μόνο **preprocess image for OCR** αλλά δείχνει επίσης πώς να **enhance image contrast** και **remove noise from scanned image** χρησιμοποιώντας τα ενσωματωμένα φίλτρα της Aspose. Στο τέλος θα έχετε μια έτοιμη για εκτέλεση εφαρμογή C# console που παρέχει πολύ πιο αξιόπιστα αποτελέσματα αναγνώρισης.

---

## What You’ll Need

- **.NET 6.0 ή νεότερο** (ο κώδικας λειτουργεί επίσης με .NET Framework 4.6+)  
- **Aspose.OCR for .NET** – μπορείτε να κατεβάσετε το πακέτο NuGet `Aspose.OCR`  
- Μια δείγμα εικόνας που παρουσιάζει θόρυβο, κλίση ή χαμηλή αντίθεση (θα χρησιμοποιήσουμε το `skewed-photo.jpg` στην επίδειξη)  
- Οποιοδήποτε IDE προτιμάτε – Visual Studio, Rider ή VS Code αρκεί  

Δεν απαιτούνται επιπλέον εγγενές βιβλιοθήκες ή πολύπλοκες εγκαταστάσεις· όλα βρίσκονται μέσα στο πακέτο Aspose.

---

## ## Preprocess Image for OCR – Step‑by‑Step Implementation

Παρακάτω βρίσκεται το πλήρες αρχείο πηγαίου κώδικα που θα μεταγλωττίσετε. Μπορείτε να το αντιγράψετε‑και‑επικολλήσετε σε ένα νέο console project και να πατήσετε **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Add preprocessing filters to improve recognition.
        // 2a – Remove noise from scanned image.
        ocrEngine.Settings.Filters.Add(new DenoiseFilter()); // Reduces random speckles.
        // 2b – Correct skew (deskew) that often appears in photographed documents.
        ocrEngine.Settings.Filters.Add(new DeskewFilter()); // Straightens the baseline.
        // 2c – Enhance image contrast for better character separation.
        ocrEngine.Settings.Filters.Add(new ContrastEnhanceFilter()); // Boosts contrast.

        // Step 3: (Optional) Rotate the image if it was captured at an angle.
        // Negative values rotate clockwise, positive counter‑clockwise.
        ocrEngine.Settings.Filters.Add(new RotateFilter(-3)); // Small correction.

        // Step 4: Perform OCR on the image file.
        // Replace the path with the actual location of your test image.
        string extractedText = ocrEngine.RecognizeImage("YOUR_DIRECTORY/skewed-photo.jpg");

        // Step 5: Display the recognized text.
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(extractedText);
    }
}
```

### Why Each Filter Matters

| Filter | What it does | Why it helps OCR |
|--------|--------------|-----------------|
| **DenoiseFilter** | Αφαιρεί τυχαίο θόρυβο εικονοστοιχείων που συχνά εμφανίζεται σε σάρωσεις χαμηλού φωτισμού. | Ο θόρυβος μπορεί να λανθασμένα ληφθεί ως θραύσματα γλυφών, αλλοιώνοντας τα σχήματα των χαρακτήρων. |
| **DeskewFilter** | Ανιχνεύει τη κυρίαρχη γωνία γραμμής κειμένου και περιστρέφει την εικόνα στο 0°. | Οι κλίσεις των βάσεων κάνουν τον κινητήρα OCR να θεωρεί ότι οι χαρακτήρες είναι κεκλιμένοι, οδηγώντας σε λανθασμένη αναγνώριση. |
| **ContrastEnhanceFilter** | Αυξάνει τη διαφορά μεταξύ του σκοτεινού κειμένου και του φωτεινού υποβάθρου. | Η υψηλότερη αντίθεση βελτιώνει το βήμα δυαδικοποίησης στα περισσότερα pipelines OCR. |
| **RotateFilter** (optional) | Εφαρμόζει μια χειροκίνητη περιστροφή που καθορίζετε. | Χρήσιμο όταν η αυτόματη διόρθωση κλίσης δεν είναι αρκετή, π.χ. φωτογραφία ληφθείσα υπό μικρή γωνία. |

> **Pro tip:** Εάν η πηγή σας είναι PDF σάρωσης, εξάγετε πρώτα τη σελίδα ως εικόνα (π.χ., χρησιμοποιώντας `PdfRenderer`) και μετά την τροφοδοτήστε στην ίδια αλυσίδα φίλτρων. Η ίδια λογική προεπεξεργασίας ισχύει.

---

## ## Enhance Image Contrast Before OCR – Visual Confirmation

Είναι ένα πράγμα να προσθέσετε ένα φίλτρο· είναι άλλο να δείτε το αποτέλεσμα. Παρακάτω υπάρχει μια απλή εικονογράφηση πριν‑και‑μετά (αντικαταστήστε με τα δικά σας στιγμιότυπα όταν δοκιμάσετε).

![Diagram of preprocess image for OCR pipeline](image.png){alt="Diagram of preprocess image for OCR pipeline"}

Η αριστερή πλευρά δείχνει τη ακατέργαστη, θορυβώδη σάρωση, ενώ η δεξιά πλευρά εμφανίζει την ίδια εικόνα μετά από **enhance image contrast**, **remove noise from scanned image**, και deskewing. Παρατηρήστε πώς οι χαρακτήρες γίνονται καθαροί και απομονωμένοι — ακριβώς αυτό που χρειάζεται η μηχανή OCR.

---

## ## Remove Noise from Scanned Image – Edge Cases & Tips

Δεν κάθε έγγραφο υποφέρει από τον ίδιο τύπο θορύβου. Εδώ είναι μερικά σενάρια που μπορεί να συναντήσετε και πώς να ρυθμίσετε την αλυσίδα:

1. **Βαθύς θόρυβος «αλάτι‑και‑πίπερο»** – Αυξήστε την επιθετικότητα του `DenoiseFilter` περνώντας ένα προσαρμοσμένο αντικείμενο `DenoiseOptions` (π.χ., `new DenoiseFilter(new DenoiseOptions { Strength = 2 })`).  
2. **Ξεθωριασμένο μελάνι σε κίτρινο χαρτί** – Συνδυάστε το `ContrastEnhanceFilter` με ένα `BrightnessAdjustFilter` για να ανεβάσετε τον τόνο του υποβάθρου πριν ενισχύσετε την αντίθεση.  
3. **Χρωματιστό κείμενο** – Μετατρέψτε πρώτα την εικόνα σε γκρι κλίμακα (`new GrayscaleFilter()`) επειδή οι περισσότεροι κινητήρες OCR, συμπεριλαμβανομένου του Aspose, λειτουργούν καλύτερα με μονοκαναλικά δεδομένα.  

Η πειραματική αλλαγή της σειράς των φίλτρων μπορεί επίσης να έχει σημασία. Στην πράξη, τοποθετώ το `DenoiseFilter` **πριν** το `DeskewFilter` επειδή μια καθαρότερη εικόνα παρέχει πιο αξιόπιστα δεδομένα άκρων στον αλγόριθμο διόρθωσης κλίσης.

---

## ## Running the Demo & Verifying Output

1. **Build** το console project (`dotnet build`).  
2. **Run** (`dotnet run`). Θα πρέπει να δείτε κάτι σαν:

```
=== OCR RESULT ===
The quick brown fox jumps over the lazy dog.
```

Εάν η έξοδος εξακολουθεί να περιέχει ακατάληπτους χαρακτήρες, ελέγξτε ξανά ότι η διαδρομή της εικόνας είναι σωστή και ότι το αρχείο πηγής δεν είναι ήδη πολύ χαμηλής ανάλυσης (συνιστάται τουλάχιστον 300 dpi για τις περισσότερες εργασίες OCR).

---

## Conclusion

Τώρα έχετε ένα σταθερό, έτοιμο για παραγωγή πρότυπο για **preprocess image for OCR** σε C#. Συνδυάζοντας τα `DenoiseFilter`, `DeskewFilter` και `ContrastEnhanceFilter` της Aspose — και προαιρετικά ένα `RotateFilter` — μπορείτε να **enhance image contrast**, **remove noise from scanned image**, και να αυξήσετε δραματικά την ακρίβεια της επακόλουθης εξαγωγής κειμένου.

Τι ακολουθεί; Δοκιμάστε να τροφοδοτήσετε την καθαρισμένη εικόνα σε άλλα βήματα μετά‑επεξεργασίας όπως ορθογραφικός έλεγχος, ανίχνευση γλώσσας, ή η ενσωμάτωση του ακατέργαστου κειμένου σε μια ροή φυσικής γλώσσας. Μπορείτε επίσης να εξερευνήσετε το `BinarizationFilter` της Aspose για ροές μόνο δυαδικών εικόνων, ή να μεταβείτε σε διαφορετικό κινητήρα OCR (Tesseract, Microsoft OCR) ενώ επαναχρησιμοποιείτε την ίδια αλυσίδα προεπεξεργασίας.

Έχετε μια δύσκολη εικόνα που ακόμα δεν συνεργάζεται; Αφήστε ένα σχόλιο και θα το αντιμετωπίσουμε μαζί. Καλή προγραμματιστική δουλειά, και εύχομαι τα αποτελέσματα OCR σας να είναι πάντα κρυστάλλινα καθαρά!

## What Should You Learn Next?

Οι παρακάτω οδηγίες καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη λειτουργικό κώδικα με βήμα‑βήμα εξηγήσεις για να σας βοηθήσουν να κυριαρχήσετε επιπλέον δυνατότητες API και να εξερευνήσετε εναλλακτικές προσεγγίσεις υλοποίησης στα δικά σας έργα.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}