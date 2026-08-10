---
category: general
date: 2026-06-22
description: Αναγνώριση κειμένου από εικόνα χρησιμοποιώντας το Aspose OCR σε C#. Μάθετε
  πώς να διορθώνετε αυτόματα την κλίση της εικόνας, να προετοιμάζετε την εικόνα για
  OCR και να ενεργοποιείτε την αυτόματη διόρθωση κλίσης σε ένα σύντομο παράδειγμα
  OCR σε C#.
draft: false
keywords:
- recognize text from image
- auto deskew image
- preprocess image for ocr
- c# ocr example
- enable auto deskew
language: el
og_description: Αναγνώριση κειμένου από εικόνα με το Aspose OCR σε C#. Αυτός ο οδηγός
  δείχνει πώς να διορθώσετε αυτόματα την κλίση της εικόνας, να προετοιμάσετε την εικόνα
  για OCR και να ενεργοποιήσετε την αυτόματη διόρθωση κλίσης σε ένα πρακτικό παράδειγμα
  OCR σε C#.
og_title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρες παράδειγμα OCR
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  headline: Recognize Text from Image in C# – Full OCR Example
  type: TechArticle
- description: Recognize text from image using Aspose OCR in C#. Learn how to auto
    deskew image, preprocess image for OCR, and enable auto deskew in a concise c#
    ocr example.
  name: Recognize Text from Image in C# – Full OCR Example
  steps:
  - name: 1. Low Contrast or Dark Backgrounds
    text: 'Aspose.OCR offers an extra flag `PreprocessingOptions.ContrastEnhancement`.
      Add it to the `Preprocessing` line:'
  - name: 2. Non‑English Documents
    text: Swap `OcrLanguage.English` for `OcrLanguage.Spanish`, `OcrLanguage.French`,
      etc. The engine auto‑loads the appropriate language model.
  - name: 3. Large Images
    text: 'Processing a 5 MP photo can be memory‑hungry. Scale it down first:'
  - name: 4. Getting Bounding Boxes
    text: 'If you need the exact location of each word (e.g., for a UI overlay), iterate
      over `result.Regions`:'
  type: HowTo
tags:
- OCR
- C#
- Aspose
- Image Processing
title: Αναγνώριση κειμένου από εικόνα σε C# – Πλήρες παράδειγμα OCR
url: /el/net/ocr-optimization/recognize-text-from-image-in-c-full-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Αναγνώριση Κειμένου από Εικόνα σε C# – Πλήρες Παράδειγμα OCR

Έχετε αναρωτηθεί ποτέ πώς να **αναγνωρίζετε κείμενο από εικόνα** σε μια εφαρμογή C# χωρίς να τρελαίνεστε με θολές σκαναρίσματα; Δεν είστε μόνοι. Είτε ψηφιοποιείτε αποδείξεις, εξάγετε δεδομένα από φόρμες, είτε απλώς πειραματίζεστε με τεχνάσματα εικόνας με AI, η λήψη καθαρών αποτελεσμάτων OCR εξαρτάται από τη σωστή προεπεξεργασία — σκεφτείτε την αυτόματη ευθυγράμμιση (auto deskew) της εικόνας και τη μείωση θορύβου.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα **c# ocr example** που χρησιμοποιεί τη βιβλιοθήκη Aspose.OCR για να **ενεργοποιήσει το auto deskew**, να ευθυγραμμίσει αυτόματα τις κλίσεις των φωτογραφιών και να **προεπεξεργαστεί την εικόνα για OCR** με λίγες μόνο γραμμές κώδικα. Στο τέλος θα έχετε ένα εκτελέσιμο πρόγραμμα που εκτυπώνει το αναγνωρισμένο κείμενο απευθείας στην κονσόλα.

## What You’ll Learn

- Πώς να εγκαταστήσετε και να αναφέρετε το πακέτο NuGet Aspose.OCR.  
- Πώς να ρυθμίσετε ένα `OcrEngine` με υποστήριξη αγγλικής γλώσσας.  
- Πώς να ενεργοποιήσετε **auto deskew image** και άλλες επιλογές προεπεξεργασίας σε ένα βήμα.  
- Πώς να τρέξετε τη μηχανή σε μια πραγματική φωτογραφία και να διαχειριστείτε το αποτέλεσμα.  
- Συμβουλές για την αντιμετώπιση ειδικών περιπτώσεων όπως έντονα περιστραμμένες εικόνες ή σκαναρίσματα χαμηλής αντίθεσης.

> **Prerequisites** – Χρειάζεστε .NET 6 (ή νεότερη) και βασική κατανόηση της C#. Δεν απαιτείται προηγούμενη εμπειρία OCR.

---

## ## Recognize Text from Image – Install the Aspose.OCR Package

Πριν γράψουμε κώδικα, η βιβλιοθήκη πρέπει να προστεθεί στο έργο. Ανοίξτε ένα τερματικό στο φάκελο της λύσης και τρέξτε:

```bash
dotnet add package Aspose.OCR
```

Αυτή η εντολή κατεβάζει την πιο πρόσφατη σταθερή έκδοση του Aspose.OCR, η οποία περιλαμβάνει τη μηχανή OCR, τα πακέτα γλωσσών και τα εργαλεία προεπεξεργασίας που θα χρειαστούμε.  

*Pro tip:* Αν στοχεύετε .NET Framework αντί για .NET Core, χρησιμοποιήστε το UI του Visual Studio NuGet Package Manager — απλώς ψάξτε για “Aspose.OCR” και κάντε κλικ στο **Install**.

---

## ## Recognize Text from Image – Initialize the OCR Engine

Τώρα που το πακέτο είναι έτοιμο, μπορούμε να δημιουργήσουμε τη μηχανή. Το πρώτο βήμα είναι να πούμε στη μηχανή ποια γλώσσα θα περιμένει. Στις περισσότερες περιπτώσεις η αγγλική είναι αρκετή, αλλά η βιβλιοθήκη υποστηρίζει δεκάδες γλώσσες έτοιμες προς χρήση.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine and set the language to English
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,

            // Step 2: Enable preprocessing to automatically deskew and denoise the image
            Preprocessing = PreprocessingOptions.AutoDeskew | PreprocessingOptions.Denoise
        };
```

**Γιατί είναι σημαντικό:**  
- `Language = OcrLanguage.English` λέει στη μηχανή ποιο σύνολο χαρακτήρων να χρησιμοποιήσει, βελτιώνοντας δραματικά την ακρίβεια.  
- Η ιδιότητα `Preprocessing` συνδυάζει δύο σημαίες — `AutoDeskew` και `Denoise`. Αυτό το βήμα **auto deskew image** περιστρέφει την εικόνα πίσω σε οριζόντια βάση, ενώ το `Denoise` αφαιρεί σπόρια που θα μπέρδευαν τη μηχανή OCR.  

Αν παραλείψετε την προεπεξεργασία, συχνά θα δείτε ακατάληπτο κείμενο σε σκαναρίσματα αποδείξεων ή φωτογραφίες λημμάτων.

---

## ## Recognize Text from Image – Feed the Image to the Engine

Με τη μηχανή έτοιμη, το επόμενο βήμα είναι να της δώσουμε ένα αρχείο εικόνας. Το Aspose.OCR δέχεται διαδρομή ή `Stream`, ώστε να μπορείτε να δουλέψετε με τοπικά αρχεία, ενσωματωμένους πόρους ή ακόμη και εικόνες που κατεβάζονται από το διαδίκτυο.

```csharp
        // Step 3: Recognize text from the input image
        var result = engine.RecognizeImage(@"YOUR_DIRECTORY/skewed_photo.jpg");
```

**Σημείωση για edge‑case:**  
- Αν η εικόνα είναι **έντονα περιστραμμένη** (> 45°), το `AutoDeskew` θα προσπαθήσει όσο μπορεί, αλλά ίσως θελήσετε να την περιστρέψετε χειροκίνητα με `System.Drawing` ή `ImageSharp` πριν τη περάσετε στη μηχανή.  
- Για **πολυσέλιδες PDF**, καλέστε `engine.RecognizePdf` αντί για αυτό· οι ίδιες σημαίες προεπεξεργασίας ισχύουν.

---

## ## Recognize Text from Image – Output the Result

Τέλος, εμφανίζουμε το εξαγόμενο κείμενο. Το αντικείμενο `result` περιέχει περισσότερα από απλό κείμενο — προσφέρει επίσης βαθμούς εμπιστοσύνης, περιοχές (bounding boxes) και την αρχική εικόνα με επισημασμένες περιοχές. Για μια γρήγορη επίδειξη, η εκτύπωση του `result.Text` αρκεί.

```csharp
        // Step 4: Output the recognized text to the console
        System.Console.WriteLine(result.Text);
    }
}
```

Όταν τρέξετε το πρόγραμμα, θα πρέπει να δείτε κάτι σαν:

```
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!
```

Αν το αποτέλεσμα φαίνεται ακατάληπτο, ελέγξτε ξανά ότι η πηγή εικόνας είναι καθαρή, καλά φωτισμένη και ότι **preprocess image for OCR** είναι πράγματι ενεργοποιημένο (οι σημαίες `Preprocessing` παραπάνω).

---

## ## Recognize Text from Image – Handling Common Pitfalls

### 1. Low Contrast or Dark Backgrounds
Το Aspose.OCR προσφέρει μια επιπλέον σημαία `PreprocessingOptions.ContrastEnhancement`. Προσθέστε την στη γραμμή `Preprocessing`:

```csharp
Preprocessing = PreprocessingOptions.AutoDeskew |
                PreprocessingOptions.Denoise |
                PreprocessingOptions.ContrastEnhancement
```

### 2. Non‑English Documents
Αντικαταστήστε το `OcrLanguage.English` με `OcrLanguage.Spanish`, `OcrLanguage.French` κ.λπ. Η μηχανή φορτώνει αυτόματα το κατάλληλο μοντέλο γλώσσας.

### 3. Large Images
Η επεξεργασία μιας φωτογραφίας 5 MP μπορεί να καταναλώσει πολύ μνήμη. Σμικρύνετέ την πρώτα:

```csharp
engine.Image = ImageProcessor.Resize(@"YOUR_DIRECTORY/skewed_photo.jpg", 1024, 768);
```

### 4. Getting Bounding Boxes
Αν χρειάζεστε την ακριβή θέση κάθε λέξης (π.χ. για επικάλυψη UI), επαναλάβετε πάνω από `result.Regions`:

```csharp
foreach (var region in result.Regions)
{
    System.Console.WriteLine($"{region.Text} at {region.Bounds}");
}
```

---

## ## Recognize Text from Image – Full Working Example

Παρακάτω είναι το **πλήρες, αντιγραφή‑και‑επικόλληση** πρόγραμμα που ενσωματώνει όλες τις παραπάνω συμβουλές. Αποθηκεύστε το ως `Program.cs`, αντικαταστήστε το `YOUR_DIRECTORY` με το φάκελο που περιέχει τη δοκιμαστική εικόνα, και τρέξτε `dotnet run`.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;

class Program
{
    static void Main()
    {
        // Create and configure the OCR engine
        var engine = new OcrEngine
        {
            Language = OcrLanguage.English,
            // Enable auto deskew, denoise, and contrast enhancement
            Preprocessing = PreprocessingOptions.AutoDeskew |
                            PreprocessingOptions.Denoise |
                            PreprocessingOptions.ContrastEnhancement
        };

        // Path to the image you want to process
        string imagePath = @"YOUR_DIRECTORY/skewed_photo.jpg";

        // Recognize the image
        var result = engine.RecognizeImage(imagePath);

        // Output plain text
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(result.Text);
        Console.WriteLine();

        // Optional: print bounding boxes for each detected region
        Console.WriteLine("=== Detected Regions ===");
        foreach (var region in result.Regions)
        {
            Console.WriteLine($"{region.Text}  -->  {region.Bounds}");
        }
    }
}
```

**Αναμενόμενη έξοδος στην κονσόλα** (υπόθεση ότι η εικόνα περιέχει μια απλή απόδειξη):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-06-01
Total: $256.78
Thank you for your business!

=== Detected Regions ===
Invoice #12345  -->  {X=12,Y=34,Width=250,Height=20}
Date: 2026-06-01  -->  {X=12,Y=60,Width=200,Height=18}
Total: $256.78  -->  {X=12,Y=86,Width=180,Height=18}
Thank you for your business!  -->  {X=12,Y=112,Width=300,Height=22}
```

Αν δείτε το κείμενο να εκτυπώνεται καθαρά, συγχαρητήρια — έχετε επιτυχώς **recognize text from image** με auto‑deskew και προεπεξεργασία!

---

## ## Recognize Text from Image – Next Steps & Related Topics

- **Batch processing:** Τυλίξτε την κλήση της μηχανής μέσα σε βρόχο `foreach` για να επεξεργαστείτε δεκάδες φωτογραφίες ταυτόχρονα.  
- **PDF conversion:** Χρησιμοποιήστε `engine.RecognizePdf` για πολυσέλιδες έγγραφα, έπειτα συγχωνεύστε τα αποτελέσματα.  
- **Custom dictionaries:** Φορτώστε μια λίστα λέξεων στο `engine.CustomWords` για να βελτιώσετε την ακρίβεια σε εξειδικευμένη ορολογία (π.χ. ιατρικοί κωδικοί).  
- **Performance tuning:** Κρατήστε την παρουσίαση του `OcrEngine` στην μνήμη αν επεξεργάζεστε πολλές εικόνες· η δημιουργία της μηχανής είναι το πιο ακριβό βήμα.  

Αυτές οι επεκτάσεις χρησιμοποιούν τα ίδια concepts — **preprocess image for OCR**, **enable auto deskew**, και **recognize text from image** — ώστε να μπορείτε να επαναχρησιμοποιήσετε τα πρότυπα κώδικα που μόλις μάθατε.

---

## Conclusion

Μόλις διασχίσαμε ένα **c# ocr example** που δείχνει πώς να **recognize text from image** χρησιμοποιώντας το Aspose.OCR, ενώ αυτόματα ευθυγραμμίζουμε (deskew) και αφαιρούμε θόρυβο από την εικόνα. Ενεργοποιώντας το `AutoDeskew` (τη δυνατότητα **auto deskew image**) και προσθέτοντας μερικές σημαίες προεπεξεργασίας, αυξάνετε δραματικά την αξιοπιστία του OCR χωρίς να γράψετε ούτε μια γραμμή κώδικα επεξεργασίας εικόνας.

Τώρα μπορείτε να πάρετε αυτό το σκελετό, να προσθέσετε τις δικές σας εικόνες και να αρχίσετε να εξάγετε δεδομένα από τιμολόγια, ταυτότητες ή οποιοδήποτε άλλο έγγραφο που βρίσκεται σε χαρτί. Έχετε μια δύσκολη σκαναρίσματος; Δοκιμάστε τις πρόσθετες επιλογές προεπεξεργασίας που αναφέραμε ή πειραματιστείτε με προσαρμοσμένα πακέτα γλωσσών. Ο ουρανός είναι το όριο.

Αν αυτός ο οδηγός σας βοήθησε, αφήστε ένα σχόλιο, μοιραστείτε τα αποτελέσματά σας ή επικοινωνήστε μαζί μου στο GitHub — καλή προγραμματιστική δουλειά!

## What Should You Learn Next?

Τα παρακάτω tutorials καλύπτουν στενά συναφή θέματα που επεκτείνουν τις τεχνικές που παρουσιάστηκαν σε αυτόν τον οδηγό. Κάθε πόρος περιλαμβάνει πλήρη παραδείγματα κώδικα με βήμα‑βήμα εξηγήσεις για να κατακτήσετε επιπλέον δυνατότητες του API και να εξερευνήσετε εναλλακτικές προσεγγίσεις στα δικά σας έργα.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}