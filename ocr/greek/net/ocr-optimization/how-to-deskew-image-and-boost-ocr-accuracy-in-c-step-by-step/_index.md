---
category: general
date: 2026-04-17
description: Πώς να διορθώσετε γρήγορα την κλίση μιας εικόνας χρησιμοποιώντας το Aspose.OCR
  – μάθετε πώς να φορτώνετε εικόνα OCR, να προεπεξεργάζεστε εικόνα OCR και να αναγνωρίζετε
  κείμενο στην εικόνα με υψηλή ακρίβεια.
draft: false
keywords:
- how to deskew image
- recognize text image
- improve ocr accuracy
- load image ocr
- preprocess image ocr
language: el
og_description: Πώς να διορθώσετε την κλίση μιας εικόνας και να βελτιώσετε την ακρίβεια
  του OCR σε C#. Μάθετε πώς να φορτώνετε εικόνα OCR, να προεπεξεργάζεστε εικόνα OCR
  και να αναγνωρίζετε κείμενο σε εικόνα με το Aspose.OCR.
og_title: Πώς να διορθώσετε την κλίση εικόνας – Πλήρης οδηγός OCR σε C#
tags:
- Aspose.OCR
- C#
- Image Processing
title: Πώς να ευθυγραμμίσετε μια εικόνα και να βελτιώσετε την ακρίβεια OCR σε C# –
  Οδηγός βήμα‑βήμα
url: /el/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-in-c-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση εικόνας και να βελτιώσετε την ακρίβεια OCR σε C#

**How to deskew image** είναι ένα κοινό εμπόδιο όποτε χρειάζεται να εξάγετε κείμενο από μια φωτογραφία που δεν είναι τέλεια ευθυγραμμισμένη. Σε αυτόν τον οδηγό θα περάσουμε από τη φόρτωση της εικόνας, την προεπεξεργασία της, και τελικά **recognize text image** χρησιμοποιώντας την ισχυρή αλυσίδα φίλτρων της Aspose.OCR.

Αν έχετε ποτέ κατευθύνει την κάμερα του τηλεφώνου σας σε μια απόδειξη, μια πινακίδα ή μια σαρωμένη φόρμα και καταλήξατε με παραμορφωμένους, ακατανόητους χαρακτήρες, ξέρετε πόσο εκνευριστικό μπορεί να είναι. Τα καλά νέα; Μερικές γραμμές κώδικα C# μπορούν να ευθυγραμμίσουν αυτήν την εικόνα, να καθαρίσουν τον θόρυβο και να σας δώσουν μια καθαρή συμβολοσειρά που μπορείτε πραγματικά να χρησιμοποιήσετε. Θα αναφερθούμε επίσης στο πώς να **improve OCR accuracy** ρυθμίζοντας τα βήματα προεπεξεργασίας.

## Τι θα χρειαστείτε

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί και με .NET Core)  
- Άδεια ή δοκιμαστική έκδοση του **Aspose.OCR** (διαθέσιμη μέσω NuGet)  
- Ένα αρχείο εικόνας που είναι ελαφρώς περιστραμμένο ή θορυβώδες (π.χ., `skewed_photo.png`)  

Δεν απαιτούνται περίπλοκα εργαλεία τρίτων—μόνο η βιβλιοθήκη Aspose.OCR και λίγη γνώση C#.

![Παράδειγμα διόρθωσης κλίσης εικόνας](/images/deskew-demo.png "Διόρθωση κλίσης εικόνας – αρχική vs διορθωμένη")

---

## Βήμα 1 – Φόρτωση εικόνας OCR: Προετοιμασία του αρχείου προέλευσης

Πριν μπορέσουμε να ευθυγραμμίσουμε οτιδήποτε, πρέπει να φέρουμε την εικόνα στη μνήμη. Η μέθοδος `OcrImage.FromFile` κάνει ακριβώς αυτό.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the image you want to process
var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");
```

> **Γιατί είναι σημαντικό:** Η φόρτωση της εικόνας ως `OcrImage` δίνει στην μηχανή OCR άμεση πρόσβαση στα δεδομένα εικονοστοιχείων, κάτι που είναι απαραίτητο για τα επόμενα βήματα **preprocess image OCR**. Αν η διαδρομή του αρχείου είναι λανθασμένη, θα αντιμετωπίσετε `FileNotFoundException`, οπότε ελέγξτε ξανά τη θέση.

## Βήμα 2 – Preprocess Image OCR: Δημιουργία αλυσίδας φίλτρων Deskew

Τώρα έρχεται η καρδιά του **how to deskew image**. Η Aspose.OCR παρέχει μια συλλογή φίλτρων που μπορείτε να συνδυάσετε με οποιαδήποτε σειρά. Για τις περισσότερες πραγματικές φωτογραφίες θα θέλετε:

1. **Deskew** – διόρθωση περιστροφής  
2. **Denoise** – αφαίρεση σκόνης‑και‑πιπεριού  
3. **ContrastEnhance** – ανάδειξη αχνών χαρακτήρων  

```csharp
// Create a chain of preprocessing filters
var filterChain = new ImageFilterCollection
{
    new DeskewFilter(),          // Detects and corrects rotation
    new DenoiseFilter(),        // Reduces noise
    new ContrastEnhanceFilter() // Boosts contrast for faint text
};

// Apply the filter chain to obtain a cleaned image
var filteredImage = filterChain.Apply(ocrImage);
```

> **Pro tip:** Αν η εικόνα σας είναι ήδη καλά εκτεθειμένη, μπορείτε να παραλείψετε το `ContrastEnhanceFilter`. Λιγότερη επεξεργασία σημαίνει ταχύτερη εκτέλεση.

### Edge Cases

- **Extreme rotation (>45°):** Το `DeskewFilter` λειτουργεί καλύτερα μέχρι περίπου 30°. Για μεγαλύτερες γωνίες ίσως χρειαστεί να περιστρέψετε την εικόνα χειροκίνητα πρώτα (`filteredImage.Rotate(…)`).
- **Colored backgrounds:** Μετατρέψτε σε κλίμακα του γκρι πριν την αποθορυβοποίηση για καλύτερα αποτελέσματα (`filteredImage = filteredImage.ToGrayscale();`).

## Βήμα 3 – Recognize Text Image: Εκτέλεση της μηχανής OCR

Με ένα καθαρό, ευθυγραμμισμένο bitmap στα χέρια, ήρθε η ώρα να εξάγουμε τους χαρακτήρες.

```csharp
// Create an OCR engine instance
using var ocrEngine = new OcrEngine();

// Recognize text from the filtered image
var ocrResult = ocrEngine.Recognize(filteredImage);

// Display the recognized text
Console.WriteLine(ocrResult.Text);
```

> **Τι συμβαίνει στο παρασκήνιο;** Η `OcrEngine` εκτελεί έναν νευρωνικό αναγνώστη που απαιτεί μια σχεδόν όρθια, υψηλής αντίθεσης εικόνα. Γι' αυτό το προηγούμενο βήμα **preprocess image OCR** είναι κρίσιμο για **improve OCR accuracy**.

### Expected Output

Αν η αρχική φωτογραφία περιείχε τη γραμμή “Invoice #12345 – Total $89.99”, η κονσόλα θα εκτυπώσει κάτι όπως:

```
Invoice #12345 – Total $89.99
```

Αν δείτε ακατανόητους χαρακτήρες, επανεξετάστε την αλυσίδα φίλτρων—ίσως η εικόνα χρειάζεται επιπλέον όξυνση (`new SharpenFilter()`).

## Βήμα 4 – Fine‑Tuning for Better OCR Accuracy

Ακόμη και μετά τη διόρθωση κλίσης, το OCR μπορεί να δυσκολεύεται με ορισμένες γραμματοσειρές ή χαμηλής ανάλυσης σαρώσεις. Εδώ είναι μερικές γρήγορες ρυθμίσεις:

| Πρόβλημα | Διόρθωση |
|----------|----------|
| Μικρό μέγεθος γραμματοσειράς (<10 pt) | Αύξηση μεγέθους εικόνας (`filteredImage = filteredImage.Resize(2.0);`) |
| Ανοιχτόγκρι κείμενο σε λευκό | Περισσότερη αύξηση αντίθεσης (`new ContrastEnhanceFilter(1.5)`) |
| Κείμενο πολλαπλών γλωσσών | Ορίστε `ocrEngine.Language = OcrLanguage.Multilingual;` |

Αυτές οι προσαρμογές βελτιώνουν άμεσα **improve OCR accuracy** χωρίς να αλλάζουν τη βασική δομή του κώδικα.

## Πλήρες Παράδειγμα Εργασίας

Παρακάτω είναι το πλήρες, έτοιμο‑για‑εκτέλεση πρόγραμμα που ενσωματώνει όλα τα παραπάνω βήματα. Αντιγράψτε το σε ένα νέο πρότζεκτ κονσόλας και πατήστε **F5**.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Step 1: Load the image you want to process
        var ocrImage = OcrImage.FromFile(@"C:\Images\skewed_photo.png");

        // Step 2: Build a chain of preprocessing filters
        var filterChain = new ImageFilterCollection
        {
            new DeskewFilter(),          // Detects and corrects rotation
            new DenoiseFilter(),        // Reduces salt‑and‑pepper noise
            new ContrastEnhanceFilter() // Improves faint characters
        };

        // Step 3: Apply the filter chain to obtain a cleaned image
        var filteredImage = filterChain.Apply(ocrImage);

        // Step 4: Create an OCR engine instance
        using var ocrEngine = new OcrEngine();

        // Optional: set language or other engine options here
        // ocrEngine.Language = OcrLanguage.English;

        // Step 5: Recognize text from the filtered image
        var ocrResult = ocrEngine.Recognize(filteredImage);

        // Step 6: Display the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Εκτελέστε το πρόγραμμα και θα δείτε το καθαρό, διορθωμένο κείμενο να εμφανίζεται στην κονσόλα.

## Συχνές Ερωτήσεις & Απαντήσεις

**Q: Λειτουργεί αυτό σε PDF;**  
A: Ναι. Μετατρέψτε κάθε σελίδα PDF σε εικόνα (π.χ., χρησιμοποιώντας `Aspose.PDF`) και δώστε το παραγόμενο bitmap στην ίδια αλυσίδα φίλτρων.

**Q: Τι γίνεται αν η εικόνα μου είναι ήδη τέλεια ευθυγραμμισμένη;**  
A: Το `DeskewFilter` θα εντοπίσει γωνία σχεδόν μηδενική και θα αφήσει την εικόνα αμετάβλητη—χωρίς καμία ζημιά.

**Q: Μπορώ να επεξεργαστώ πολλές εικόνες σε batch;**  
A: Απόλυτα. Τυλίξτε τον κώδικα σε έναν βρόχο `foreach (var path in Directory.GetFiles(...))` και αποθηκεύστε κάθε `ocrResult.Text` σε λίστα ή αρχείο.

---

## Συμπέρασμα

Σας δείξαμε **how to deskew image** προγραμματιστικά, περάσαμε από το βήμα **load image OCR**, εφαρμόσαμε μια ισχυρή **preprocess image OCR** αλυσίδα, και τελικά **recognize text image** με την Aspose.OCR. Ρυθμίζοντας τα φίλτρα και προαιρετικά αυξάνοντας ή οξύνοντας, μπορείτε να **improve OCR accuracy** για ένα ευρύ φάσμα πραγματικών σεναρίων.

Έτοιμοι για την επόμενη πρόκληση; Δοκιμάστε να ενσωματώσετε αυτήν την αλυσίδα σε ένα web API, ή πειραματιστείτε με αναγνώριση χειρόγραφων σημειώσεων προσθέτοντας το `new BinarizationFilter()` πριν το deskew. Οι δυνατότητες είναι απεριόριστες—καλή προγραμματιστική!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}