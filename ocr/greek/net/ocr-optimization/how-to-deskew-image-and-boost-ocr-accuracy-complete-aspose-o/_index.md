---
category: general
date: 2026-05-21
description: Πώς να διορθώσετε την κλίση εικόνας και να προεπεξεργαστείτε την εικόνα
  για OCR χρησιμοποιώντας το Aspose OCR. Μάθετε πώς να φορτώνετε εικόνα για OCR, να
  αναγνωρίζετε κείμενο από την εικόνα και να βελτιώσετε την ακρίβεια του OCR βήμα‑βήμα.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- how to recognize text from image
- load image for ocr
- how to improve ocr accuracy
language: el
og_description: Πώς να διορθώσετε την κλίση μιας εικόνας και να βελτιώσετε την ακρίβεια
  του OCR. Ακολουθήστε αυτόν τον οδηγό για την προεπεξεργασία της εικόνας για OCR,
  τη φόρτωση της εικόνας για OCR και την αναγνώριση κειμένου από την εικόνα με το
  Aspose OCR.
og_title: Πώς να διορθώσετε την κλίση εικόνας – Πλήρης οδηγός Aspose OCR
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: How to deskew image and preprocess image for OCR using Aspose OCR.
    Learn how to load image for OCR, recognize text from image, and improve OCR accuracy
    step‑by‑step.
  headline: How to Deskew Image and Boost OCR Accuracy – Complete Aspose OCR Guide
  type: TechArticle
- description: How to deskew image and preprocess image for OCR using Aspose OCR.
    Learn how to load image for OCR, recognize text from image, and improve OCR accuracy
    step‑by‑step.
  name: How to Deskew Image and Boost OCR Accuracy – Complete Aspose OCR Guide
  steps:
  - name: Prerequisites
    text: '- .NET 6.0 or later (the code works on .NET Core, .NET Framework, and .NET
      5+). - A valid Aspose.OCR license (you can start with a free evaluation key).
      - An image file that’s skewed, noisy, or low‑contrast (e.g., `skewed_noisy.jpg`).
      - Visual Studio 2022 or any C#‑compatible IDE.'
  - name: Expected Output (sample)
    text: '``` === Recognized Text === This is a sample document. It contains several
      lines of text. The OCR engine should read this correctly now. ```'
  - name: Why This Pipeline Works
    text: '| Step | Purpose | Impact on Accuracy | |------|---------|--------------------|
      | `DeskewFilter` | Straightens rotated pages | Eliminates line‑skew errors |
      | `DenoiseFilter` | Removes random pixel noise | Reduces false character blobs
      | | `ContrastStretchFilter` | Enhances text/background separatio'
  - name: Final Thoughts
    text: You now have a complete, end‑to‑end solution that shows **how to deskew
      image**, **preprocess image for OCR**, **load image for OCR**, **how to recognize
      text from image**, and **how to improve OCR accuracy** using Aspose.OCR. The
      code is ready to drop into any .NET project, and the explanations sho
  type: HowTo
- questions:
  - answer: Yes. Deskew first, then denoise, then contrast stretch. If you denoise
      before deskew, the algorithm may misinterpret the skew angle.
    question: Does the order of filters matter?
  - answer: It’s safe to keep it; the filter detects a zero‑degree rotation and skips
      processing, adding virtually no overhead.
    question: My image is already straight—should I still use `DeskewFilter`?
  - answer: Try increasing the image resolution, or add a `SharpenFilter` before recognition.
      Also verify that the correct language pack is loaded.
    question: What if the OCR still misses characters?
  - answer: 'Absolutely. Wrap the pipeline creation in a method and call it for each
      file path. Remember to dispose of `OcrEngine` objects or reuse a single instance
      for performance. --- ## Next Steps & Related Topics - **Explore Aspose OCR’s
      `CharacterWhitelist`** to restrict recognition to digits or specific a'
    question: Can I process multiple images in a loop?
  type: FAQPage
tags:
- OCR
- Aspose
- Image Processing
title: Πώς να διορθώσετε την κλίση της εικόνας και να βελτιώσετε την ακρίβεια OCR
  – Πλήρης οδηγός Aspose OCR
url: /el/net/ocr-optimization/how-to-deskew-image-and-boost-ocr-accuracy-complete-aspose-o/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Πώς να διορθώσετε την κλίση της εικόνας και να βελτιώσετε την ακρίβεια του OCR – Πλήρης Οδηγός Aspose OCR

Η διόρθωση κλίσης της εικόνας είναι συχνά το πρώτο εμπόδιο όταν χρειάζεστε αξιόπιστα αποτελέσματα OCR. Σε αυτόν τον οδηγό θα σας καθοδηγήσουμε πώς να προεπεξεργαστείτε την εικόνα για OCR χρησιμοποιώντας τη βιβλιοθήκη Aspose.OCR, καλύπτοντας τα πάντα από τη φόρτωση της εικόνας για OCR μέχρι την αναγνώριση κειμένου από την εικόνα και τελικά πώς να βελτιώσετε την ακρίβεια του OCR με μια έξυπνη αλυσίδα φίλτρων.

Αν έχετε ποτέ κολλήσει σε ακατάληπτο αποτέλεσμα επειδή η σάρωση ήταν κεκλιμένη, θορυβώδης ή χαμηλής αντίθεσης, βρίσκεστε στο σωστό μέρος. Στο τέλος αυτού του tutorial θα έχετε μια έτοιμη για εκτέλεση εφαρμογή C# console που ευθυγραμμίζει, αφαιρεί θόρυβο και ενισχύει αυτόματα οποιαδήποτε σαρωμένη σελίδα πριν εξάγει καθαρό, αναζητήσιμο κείμενο.

## Τι Θα Μάθετε

- **Πώς να διορθώσετε την κλίση της εικόνας** με το ενσωματωμένο `DeskewFilter` της Aspose.
- Ο καλύτερος τρόπος για **προεπεξεργασία εικόνας για OCR** (αφαίρεση θορύβου, τέντωμα αντίθεσης, κ.ά.).
- Πώς να **φορτώσετε εικόνα για OCR** σωστά ώστε η μηχανή να βλέπει τα ακριβή pixel που προτίθεστε.
- Η βήμα‑βήμα διαδικασία για **πώς να αναγνωρίσετε κείμενο από εικόνα** χρησιμοποιώντας το `OcrEngine.Recognize()`.
- Αποδεδειγμένες συμβουλές για **πώς να βελτιώσετε την ακρίβεια του OCR** χωρίς να αγοράσετε ακριβά εργαλεία τρίτων.

### Προαπαιτούμενα

- .NET 6.0 ή νεότερο (ο κώδικας λειτουργεί σε .NET Core, .NET Framework και .NET 5+).
- Ένα έγκυρο άδεια Aspose.OCR (μπορείτε να ξεκινήσετε με ένα δωρεάν κλειδί αξιολόγησης).
- Ένα αρχείο εικόνας που είναι κεκλιμένο, θορυβώδες ή χαμηλής αντίθεσης (π.χ., `skewed_noisy.jpg`).
- Visual Studio 2022 ή οποιοδήποτε IDE συμβατό με C#.

> **Συμβουλή επαγγελματία:** Εάν δοκιμάζετε σε macOS ή Linux, βεβαιωθείτε ότι έχετε εγκατεστημένες τις απαιτούμενες εγγενείς εξαρτήσεις για το Aspose.OCR (δείτε την τεκμηρίωση της Aspose για λεπτομέρειες).

---

## Πώς να διορθώσετε την κλίση της εικόνας με Aspose OCR

Το `DeskewFilter` είναι μια μίας γραμμής λειτουργία που εντοπίζει τη γωνία της κυρίαρχης γραμμής κειμένου και περιστρέφει την εικόνα πίσω σε οριζόντια βάση. Σκεφτείτε το ως ένα ψηφιακό επίπεδο για σαρωμένες σελίδες.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// 1️⃣ Create the OCR engine and set the language
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};

// 2️⃣ Load the source image (a skewed, noisy scan)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");

// 3️⃣ Build the filter pipeline – start with deskew
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter()); // <-- this is how to deskew image
```

> **Γιατί είναι σημαντικό:** Μια κεκλιμένη σελίδα μπερδεύει το στάδιο διαχωρισμού χαρακτήρων, προκαλώντας τη συγχώνευση ή το λανθασμένο διαχωρισμό των γραμμάτων. Η διόρθωση κλίσης επαναφέρει τη φυσική σειρά ανάγνωσης, που αποτελεί τη βάση για οποιεσδήποτε επόμενες βελτιώσεις ακρίβειας.

## Προεπεξεργασία OCR εικόνας: Αφαίρεση θορύβου και ενίσχυση αντίθεσης

Μόλις η σελίδα είναι ευθεία, το επόμενο βήμα είναι ο καθαρισμός της. Ο θόρυβος και η χαμηλή αντίθεση είναι οι σιωπηλοί δολοφόνοι της απόδοσης OCR. Παρακάτω προσθέτουμε δύο ακόμη φίλτρα στην ίδια αλυσίδα.

```csharp
// 4️⃣ Add denoise and contrast stretch filters
filterPipeline.Add(new DenoiseFilter());          // removes speckles and grain
filterPipeline.Add(new ContrastStretchFilter()); // boosts dark/light separation
```

> **Πώς βοηθά:** `DenoiseFilter` εξομαλύνει τυχαίες διακυμάνσεις pixel που συχνά εμφανίζονται μετά τη σάρωση φθηνών εγγράφων. `ContrastStretchFilter` επεκτείνει το ιστόγραμμα ώστε το κείμενο να ξεχωρίζει έντονα από το φόντο, καθιστώντας την εργασία του αναγνωριστή πιο εύκολη.

## Φόρτωση εικόνας για OCR: Καλύτερες πρακτικές

Μπορεί να αναρωτιέστε αν πρέπει να φορτώσετε την εικόνα πριν ή μετά το φιλτράρισμα. Η σύντομη απάντηση: **φορτώστε την μία φορά, μετά χρησιμοποιήστε το ίδιο αντικείμενο `Image`**. Αυτό αποφεύγει επιπλέον I/O overhead και διασφαλίζει ότι η αλυσίδα φίλτρων λειτουργεί στα ακριβή ίδια δεδομένα pixel που θα διαβάσει αργότερα η μηχανή OCR.

```csharp
// 5️⃣ Apply the pipeline to the image (in‑place)
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

> **Κοινό λάθος:** Η επανανάγνωση του αρχείου μετά το φιλτράρισμα επαναφέρει τις βελτιώσεις, γι' αυτό πάντα αντιστοιχίστε την επεξεργασμένη εικόνα πίσω στο `ocrEngine.Image` όπως φαίνεται παραπάνω.

## Πώς να αναγνωρίσετε κείμενο από εικόνα χρησιμοποιώντας Aspose OCR

Τώρα που η εικόνα είναι ευθεία, καθαρή και υψηλής αντίθεσης, μπορούμε τελικά να εξάγουμε το κείμενο. Η μέθοδος `Recognize()` κάνει όλη τη βαριά δουλειά στο παρασκήνιο.

```csharp
// 6️⃣ Perform OCR recognition
ocrEngine.Recognize();

// 7️⃣ Output the recognized text
Console.WriteLine("=== Recognized Text ===");
Console.WriteLine(ocrEngine.Text);
```

> **Τι θα δείτε:** Αν όλα πήγαν καλά, η κονσόλα εκτυπώνει ένα μπλοκ αναγνώσιμων αγγλικών προτάσεων, χωρίς το τυπικό «?@#» ακαταλαβίστικο κείμενο που προκύπτει από μια κεκλιμένη, θορυβώδη σάρωση.

### Αναμενόμενο Αποτέλεσμα (δείγμα)

```
=== Recognized Text ===
This is a sample document.
It contains several lines of text.
The OCR engine should read this correctly now.
```

Αν το αποτέλεσμα εξακολουθεί να φαίνεται λανθασμένο, ελέγξτε ξανά την ανάλυση της αρχικής εικόνας (300 dpi είναι ένα καλό σημείο εκκίνησης) και σκεφτείτε να προσθέσετε ένα `BinarizationFilter` για δυαδικές εικόνες.

## Πώς να βελτιώσετε την ακρίβεια του OCR με μια πλήρη αλυσίδα φίλτρων

Η συνένωση όλων των στοιχείων δημιουργεί μια στιβαρή ροή εργασίας που παραδίδει σταθερά υψηλή ακρίβεια. Παρακάτω βρίσκεται το πλήρες, έτοιμο για εκτέλεση πρόγραμμα.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // 1️⃣ Initialize OCR engine – set language to English
        // -------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // -------------------------------------------------
        // 2️⃣ Load the image you want to process
        // -------------------------------------------------
        // Replace YOUR_DIRECTORY with the actual path
        ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg");

        // -------------------------------------------------
        // 3️⃣ Build a comprehensive filter pipeline
        // -------------------------------------------------
        var pipeline = new ImageFilterPipeline();

        // How to deskew image
        pipeline.Add(new DeskewFilter());

        // Remove random speckles
        pipeline.Add(new DenoiseFilter());

        // Boost contrast for better binarization
        pipeline.Add(new ContrastStretchFilter());

        // Optional: Binarize for black‑and‑white documents
        // pipeline.Add(new BinarizationFilter());

        // -------------------------------------------------
        // 4️⃣ Apply filters – this modifies ocrEngine.Image in place
        // -------------------------------------------------
        ocrEngine.Image = pipeline.Apply(ocrEngine.Image);

        // -------------------------------------------------
        // 5️⃣ Recognize text – the core of how to recognize text from image
        // -------------------------------------------------
        ocrEngine.Recognize();

        // -------------------------------------------------
        // 6️⃣ Display results – see how to improve OCR accuracy
        // -------------------------------------------------
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(ocrEngine.Text);
    }
}
```

### Γιατί λειτουργεί αυτή η αλυσίδα

| Βήμα | Σκοπός | Επίδραση στην Ακρίβεια |
|------|---------|--------------------|
| `DeskewFilter` | Ευθυγραμμίζει τις σελίδες που έχουν περιστραφεί | Καταργεί τα σφάλματα κλίσης γραμμής |
| `DenoiseFilter` | Αφαιρεί τυχαίο θόρυβο pixel | Μειώνει τα ψευδή σβώλια χαρακτήρων |
| `ContrastStretchFilter` | Βελτιώνει το διαχωρισμό κειμένου/υπόβαθρου | Βελτιώνει την ανίχνευση άκρων χαρακτήρων |
| (Optional) `BinarizationFilter` | Μετατρέπει σε καθαρό μαύρο/λευκό | Βοηθά τις μηχανές που αναμένουν δυαδική είσοδο |

> **Συμβουλή από την πραγματική ζωή:** Για πολυγλωσσικά έγγραφα, ορίστε το `Language` στο κατάλληλο enum `OcrLanguage` (π.χ., `OcrLanguage.French`). Η ανάμειξη γλωσσών μπορεί να μειώσει την ακρίβεια εκτός εάν ενεργοποιήσετε τη λειτουργία πολλαπλών γλωσσών.

## Συχνές Ερωτήσεις (FAQ)

**Q: Έχει σημασία η σειρά των φίλτρων;**  
A: Ναι. Πρώτα Deskew, μετά Denoise, τέλος ContrastStretch. Αν κάνετε Denoise πριν το Deskew, ο αλγόριθμος μπορεί να ερμηνεύσει λανθασμένα τη γωνία κλίσης.

**Q: Η εικόνα μου είναι ήδη ευθεία—πρέπει να χρησιμοποιήσω ακόμα το `DeskewFilter`;**  
A: Είναι ασφαλές να το κρατήσετε· το φίλτρο εντοπίζει μηδενική περιστροφή και παραλείπει την επεξεργασία, προσθέτοντας πρακτικά κανένα overhead.

**Q: Τι γίνεται αν το OCR εξακολουθεί να χάνει χαρακτήρες;**  
A: Δοκιμάστε να αυξήσετε την ανάλυση της εικόνας ή προσθέστε ένα `SharpenFilter` πριν την αναγνώριση. Επίσης, βεβαιωθείτε ότι το σωστό πακέτο γλώσσας είναι φορτωμένο.

**Q: Μπορώ να επεξεργαστώ πολλαπλές εικόνες σε βρόχο;**  
A: Απόλυτα. Τοποθετήστε τη δημιουργία της αλυσίδας σε μια μέθοδο και καλέστε την για κάθε διαδρομή αρχείου. Θυμηθείτε να απελευθερώσετε τα αντικείμενα `OcrEngine` ή να επαναχρησιμοποιήσετε μια μόνο παρουσία για καλύτερη απόδοση.

## Επόμενα Βήματα & Σχετικά Θέματα

- **Εξερευνήστε το `CharacterWhitelist` του Aspose OCR** για να περιορίσετε την αναγνώριση σε ψηφία ή συγκεκριμένα αλφάβητα (βοηθά όταν σκανάρετε φόρμες).  
- **Ενσωμάτωση με μετατροπή PDF** – χρησιμοποιήστε το Aspose.PDF για να ενσωματώσετε το αναγνωρισμένο κείμενο πίσω σε αναζητήσιμα PDF.  
- **Βελτιστοποίηση απόδοσης** – μετρήστε την απόδοση της αλυσίδας σε μεγάλες παρτίδες και σκεφτείτε παράλληλη επεξεργασία με `Parallel.ForEach`.  

Αν σας άρεσε να μάθετε **πώς να διορθώσετε την κλίση της εικόνας** και **πώς να βελτιώσετε την ακρίβεια του OCR**, ρίξτε μια γρήγορη ματιά στην τεκμηρίωση του Aspose.OCR για προχωρημένες επιλογές όπως η ενσωμάτωση `LayoutAnalysis` και `SpellCheck`.

### Τελευταίες Σκέψεις

Τώρα έχετε μια πλήρη, end‑to‑end λύση που δείχνει **πώς να διορθώσετε την κλίση της εικόνας**, **προεπεξεργασία εικόνας για OCR**, **φόρτωση εικόνας για OCR**, **πώς να αναγνωρίσετε κείμενο από εικόνα**, και **πώς να βελτιώσετε την ακρίβεια του OCR** χρησιμοποιώντας Aspose.OCR. Ο κώδικας είναι έτοιμος να ενσωματωθεί σε οποιοδήποτε έργο .NET, και οι εξηγήσεις θα σας δώσουν την αυτοπεποίθηση να προσαρμόσετε την αλυσίδα στα δικά σας edge cases.

Δοκιμάστε το, πειραματιστείτε με πρόσθετα φίλτρα, και παρακολουθήστε τα αποτελέσματα OCR σας να πετούν από «meh» σε «wow». Καλή προγραμματιστική!

---

![Deskewed image example](deskewed_example.png){alt="πώς να διορθώσετε την κλίση της εικόνας χρησιμοποιώντας Aspose OCR"}

## Σχετικά Tutorials

- [Προεπεξεργασία OCR εικόνας με φίλτρα Aspose.OCR για .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Πώς να ορίσετε την τιμή κατωφλίου στην αναγνώριση OCR εικόνας](/ocr/english/net/ocr-settings/set-threshold-value/)
- [Πώς να κάνετε OCR σε εικόνα – Εκτέλεση OCR σε εικόνα στην αναγνώριση OCR εικόνας](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}