---
category: general
date: 2026-01-13
description: πώς να διορθώσετε την κλίση μιας εικόνας και να αφαιρέσετε τον θόρυβο
  της σε C# – μάθετε πώς να αυξήσετε την αντίθεση της εικόνας, να προεπεξεργαστείτε
  την OCR εικόνας και να εφαρμόσετε πολλαπλά φίλτρα εικόνας.
draft: false
keywords:
- how to deskew image
- remove image noise
- increase image contrast
- preprocess image ocr
- multiple image filters
language: el
og_description: πώς να διορθώσετε την κλίση μιας εικόνας και να αφαιρέσετε τον θόρυβο
  εικόνας σε C# – μάθετε πώς να αυξήσετε την αντίθεση της εικόνας, να προεπεξεργαστείτε
  το OCR της εικόνας και να εφαρμόσετε πολλαπλά φίλτρα εικόνας.
og_title: πώς να διορθώσετε την κλίση της εικόνας – Πλήρης οδηγός προεπεξεργασίας
  C# για OCR
tags:
- OCR
- C#
- Image Processing
title: πώς να διορθώσετε την κλίση εικόνας – Πλήρης οδηγός προεπεξεργασίας C# για
  OCR
url: /el/net/skew-angle-calculation/how-to-deskew-image-complete-c-pre-processing-guide-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# πώς να διορθώσετε την κλίση μιας εικόνας – Πλήρης Οδηγός Προεπεξεργασίας C# για OCR

Έχετε αναρωτηθεί ποτέ **πώς να διορθώσετε την κλίση μιας εικόνας** πριν τη δώσετε σε μια μηχανή OCR; Δεν είστε μόνοι. Σε πολλές πραγματικές περιπτώσεις—σαρωμένα συμβόλαια, αποδείξεις ή παλιές φωτοαντιγραφές—το κείμενο βρίσκεται σε μικρή γωνία, η εικόνα φαίνεται σπόρια και η αντίθεση είναι ακανόνιστη. Τα καλά νέα; Μερικές γραμμές κώδικα C# μπορούν να ευθυγραμμίσουν αυτήν την κλίση, να αφαιρέσουν τον θόρυβο της εικόνας και να ενισχύσουν την αντίθεση, παρέχοντας στη μηχανή OCR μια σταθερή βάση.

Σε αυτό το tutorial θα περάσουμε βήμα‑βήμα από ένα **πλήρες, εκτελέσιμο παράδειγμα** που δείχνει ακριβώς πώς να διορθώσετε την κλίση μιας εικόνας, να αφαιρέσετε τον θόρυβο, να αυξήσετε την αντίθεση και, στη συνέχεια, να εκτελέσετε OCR με το Aspose.OCR. Στο τέλος θα έχετε μια επαναχρησιμοποιήσιμη αλυσίδα που εφαρμόζει **πολλαπλά φίλτρα εικόνας** σε μία ενιαία, ρευστή κλήση—χωρίς εικασίες.

## Τι θα χρειαστείτε

- **.NET 6+** (ή οποιαδήποτε πρόσφατη έκδοση .NET· το API λειτουργεί το ίδιο)
- **Aspose.OCR for .NET** πακέτο NuGet (`Aspose.OCR` και `Aspose.OCR.Filters`)
- Ένα δείγμα σαρωμένης εικόνας (π.χ. `skewed_noisy.png`) που παρουσιάζει κλίση, θόρυβο και χαμηλή αντίθεση
- Το αγαπημένο σας IDE (Visual Studio, Rider, VS Code—ό,τι προτιμάτε)

Αν έχετε ήδη ένα project, απλώς προσθέστε την αναφορά NuGet:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Filters
```

> **Pro tip:** Η Aspose προσφέρει δωρεάν δοκιμή με περιορισμένο αριθμό σελίδων—ιδανική για να δοκιμάσετε τον παρακάτω κώδικα.

## Βήμα 1: Δημιουργία του αντικειμένου OCR Engine

Το πρώτο που κάνουμε είναι να δημιουργήσουμε ένα `OcrEngine`. Σκεφτείτε το ως τον εγκέφαλο που θα διαβάσει το κείμενο. Δεν υπάρχει κάτι περίπλοκο, αλλά είναι το θεμέλιο για όλα τα επόμενα βήματα.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new OcrEngine();
```

> **Γιατί είναι σημαντικό:** Η αρχικοποίηση του engine μία φορά και η επαναχρησιμοποίησή του για πολλές εικόνες αποφεύγει το κόστος φόρτωσης των δεδομένων γλώσσας κάθε φορά.

## Βήμα 2: Φόρτωση της ακατέργαστης σαρωμένης εικόνας

Στη συνέχεια φορτώνουμε την εικόνα από το δίσκο. Η μέθοδος `OcrImage.FromFile` διαβάζει το αρχείο σε μορφή που μπορεί να επεξεργαστεί το Aspose.

```csharp
        // Step 2: Load the raw scanned image (skewed, noisy, low‑contrast)
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");
```

> **Edge case:** Αν η εικόνα σας είναι σε μη‑τυπική μορφή (TIFF, BMP), το Aspose την διαχειρίζεται, αλλά ίσως θέλετε να τη μετατρέψετε σε PNG πρώτα για συνέπεια.

## Βήμα 3: Δημιουργία αλυσίδας προεπεξεργασίας (Deskew → Denoise → Contrast)

Εδώ απαντάμε στην κεντρική ερώτηση **πώς να διορθώσετε την κλίση μιας εικόνας** ενώ ταυτόχρονα **αφαιρείτε τον θόρυβο** και **αυξάνετε την αντίθεση**. Το ρευστό API του Aspose μας επιτρέπει να αλυσίδουμε φίλτρα, κάνοντας τον κώδικα να διαβάζεται σαν πρόταση.

```csharp
        // Step 3: Apply Deskew, Denoise, and Contrast filters in one pipeline
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())      // Corrects rotation
            .ApplyFilter(new DenoiseFilter())     // Reduces grainy artifacts
            .ApplyFilter(new ContrastFilter());   // Boosts foreground/background separation
```

### Τι κάνει το καθένα φίλτρο

| Φίλτρο | Σκοπός | Τυπική επίδραση |
|--------|---------|----------------|
| **DeskewFilter** | Ανιχνεύει τη γωνία των γραμμών κειμένου και περιστρέφει την εικόνα ώστε να είναι οριζόντια. | Αφαιρεί την κλίση που μπερδεύει το OCR, μειώνοντας συχνά τα σφάλματα κατά 30‑50 %. |
| **DenoiseFilter** | Εφαρμόζει αλγόριθμο εξομάλυνσης που διατηρεί τις άκρες ενώ αφαιρεί τυχαίο θόρυβο pixel. | Καθαρίζει σαρωμένες αποδείξεις ή φωτογραφίες χαμηλού φωτισμού, καθιστώντας τους χαρακτήρες πιο ευκρινείς. |
| **ContrastFilter** | Τεντώνει το ιστόγραμμα ώστε οι σκοτεινές περιοχές να γίνουν πιο σκοτεινές και οι φωτεινές πιο φωτεινές. | Βελτιώνει τη διαφορά μεταξύ κειμένου και φόντου, ιδιαίτερα χρήσιμο για ξεθωριασμένα έγγραφα. |

> **Γιατί αλυσίδωση;** Η διόρθωση κλίσης πρώτα εξασφαλίζει ότι ο αποθορυβιστής λειτουργεί σε σωστά προσανατολισμένη εικόνα· η ενίσχυση της αντίθεσης στο τέλος κάνει το καθαρισμένο κείμενο πιο εμφανές για το OCR engine.

## Βήμα 4: Εκτέλεση OCR στην επεξεργασμένη εικόνα

Τώρα που η εικόνα είναι ευθεία, καθαρή και υψηλής αντίθεσης, τη δίνουμε στο OCR engine. Θα χρησιμοποιήσουμε τα δεδομένα αγγλικής γλώσσας, αλλά το Aspose υποστηρίζει πάνω από 150 γλώσσες.

```csharp
        // Step 4: Recognize text using the English language pack
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);
```

Αν χρειάζεστε άλλη γλώσσα, απλώς αντικαταστήστε το `OcrLanguage.English` με το αντίστοιχο enum (π.χ. `OcrLanguage.Spanish`).

## Βήμα 5: Εξαγωγή του αναγνωρισμένου κειμένου

Τέλος, εκτυπώνουμε το αποτέλεσμα στην κονσόλα. Σε μια πραγματική εφαρμογή ίσως γράψετε σε αρχείο, βάση δεδομένων ή το περάσετε σε επόμενα βήματα NLP.

```csharp
        // Step 5: Display the recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

### Αναμενόμενο αποτέλεσμα

Η εκτέλεση του πλήρους προγράμματος σε μια τυπική σαρωμένη απόδειξη με κλίση δίνει κάτι σαν:

```
Invoice #12345
Date: 2025‑12‑31
Total: $1,234.56
Thank you for your business!
```

Αν το αποτέλεσμα είναι ακατάληπτο, ελέγξτε την αρχική εικόνα—υπερβολική θολότητα ή έντονη σκοτεινότητα μπορεί να απαιτούν πρόσθετη προεπεξεργασία (π.χ. φίλτρο SharpenFilter).

![how to deskew image example](images/deskewed_example.png "how to deskew image – before and after processing")

*Η παραπάνω εικόνα δείχνει το αρχικό σκυθρωπό σκανάρισμα στα αριστερά και την διορθωμένη, αποθορυβισμένη, υψηλής αντίθεσης έκδοση στα δεξιά.*

## Πρόσθετες Συμβουλές & Συνηθισμένα Πιθανά Προβλήματα

### 1. Όταν η γωνία κλίσης είναι ακραία

Αν το έγγραφο είναι κλινόμενο περισσότερο από 30°, το `DeskewFilter` μπορεί να δυσκολευτεί. Σε αυτήν την περίπτωση, περιστρέψτε την εικόνα χειροκίνητα:

```csharp
var manuallyRotated = rawImage.Rotate(45); // rotates 45 degrees clockwise
var processed = manuallyRotated.ApplyFilter(new DeskewFilter());
```

### 2. Διαχείριση έγχρωμων εικόνων

Τα φίλτρα λειτουργούν εσωτερικά σε αποχρώσεις του γκρι, αλλά μπορείτε να εξαναγκάσετε μετατροπή:

```csharp
var grayImage = rawImage.ConvertToGrayscale();
var processed = grayImage.ApplyFilter(new DeskewFilter());
```

### 3. Ρύθμιση της ισχύος αποθορυβισμού

Το `DenoiseFilter` δέχεται προαιρετική παράμετρο `strength` (0‑100). Μεγαλύτερες τιμές αφαιρούν περισσότερο θόρυβο αλλά μπορεί να θολώσουν λεπτομέρειες.

```csharp
.ApplyFilter(new DenoiseFilter(strength: 70))
```

### 4. Χρήση πολλαπλών φίλτρων πέρα από τα βασικά

Το Aspose περιλαμβάνει πολλά ακόμη φίλτρα: `SharpenFilter`, `BinarizeFilter`, `ResizeFilter`, κ.λπ. Μπορείτε να τα συνδυάσετε για να δημιουργήσετε μια προσαρμοσμένη αλυσίδα που ταιριάζει στον τύπο του εγγράφου σας.

```csharp
var processed = rawImage
    .ApplyFilter(new DeskewFilter())
    .ApplyFilter(new DenoiseFilter())
    .ApplyFilter(new BinarizeFilter())
    .ApplyFilter(new SharpenFilter());
```

## Πλήρες Παράδειγμα (Αντιγραφή‑Επικόλληση)

Ακολουθεί ολόκληρο το πρόγραμμα, έτοιμο να τοποθετηθεί σε ένα console project.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessDemo
{
    static void Main()
    {
        // Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Load the original scanned image
        var rawImage = OcrImage.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // Build preprocessing pipeline: Deskew → Denoise → Contrast
        var processedImage = rawImage
            .ApplyFilter(new DeskewFilter())
            .ApplyFilter(new DenoiseFilter())
            .ApplyFilter(new ContrastFilter());

        // Run OCR using English language
        var ocrResult = ocrEngine.Recognize(processedImage, OcrLanguage.English);

        // Output recognized text
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Τρέξτε το πρόγραμμα με `dotnet run`. Αν όλα είναι ρυθμισμένα σωστά, η κονσόλα θα εμφανίσει καθαρό, αναγνώσιμο κείμενο που εξήχθη από την αρχική, κλινή, θορυβώδη εικόνα.

## Συμπέρασμα

Καλύψαμε **πώς να διορθώσετε την κλίση μιας εικόνας** σε C# ενώ ταυτόχρονα **αφαιρέσαμε θόρυβο**, **αυξήσαμε την αντίθεση** και **προετοιμάσαμε την εικόνα για OCR** με μια αλυσίδα **πολλαπλών φίλτρων εικόνας**. Το βασικό μήνυμα είναι ότι μια καλά δομημένη αλυσίδα προεπεξεργασίας μπορεί να βελτιώσει δραματικά την ακρίβεια του OCR—συχνά μετατρέποντας μια σχεδόν αδιάβαστη σάρωση σε τέλεια ευανάγνωστο κείμενο.

Έτοιμοι για το επόμενο βήμα; Δοκιμάστε να αντικαταστήσετε το `ContrastFilter` με ένα `BinarizeFilter` για να δείτε πώς η μετατροπή σε ασπρόμαυρο επηρεάζει τα αποτελέσματα, ή πειραματιστείτε με το `ResizeFilter` για να τροφοδοτήσετε το engine με υψηλότερη ανάλυση. Το ίδιο μοτίβο ισχύει ανεξάρτητα από τα φίλτρα που θα επιλέξετε, οπότε έχετε μια ευέλικτη βάση για όλα τα μελλοντικά σας έργα OCR.

Έχετε ερωτήσεις σχετικά με την επεξεργασία PDF, πολυγλωσσικό OCR ή την ενσωμάτωση σε ASP.NET API; Αφήστε ένα σχόλιο παρακάτω, και καλή προγραμματιστική!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}